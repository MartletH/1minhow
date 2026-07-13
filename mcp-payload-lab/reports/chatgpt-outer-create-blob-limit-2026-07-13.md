# ChatGPT/OpenAI outer tool-call payload test — 2026-07-13

## Scope

This report tests the path:

`ChatGPT/OpenAI tool-call outer layer → GitHub MCP create_blob(encoding="base64") → GitHub Git Data API`

It does **not** use GitHub Actions as the payload transport.

## Source sample

- Source file: `curious_fox_in_a_vineyard.png`
- Format: PNG
- Dimensions: 1448 × 1086
- File bytes: 2,309,141
- File SHA-256: `ac65acd5a1c56a0faa59e5516f4a0840b6a876fc6d2e901a6a14f6bc5a2fb76c`
- Test content: exact continuous bytes from the PNG `IDAT` compressed-image-data stream
- No resize, re-encoding, recompression, or image regeneration was performed.

## Classification rules

- `success_exact`: tool call reached GitHub and returned/created the precomputed Git blob SHA.
- `blocked_outer`: OpenAI outer safety checks blocked the call before GitHub.
- `delivered_but_distorted`: GitHub received a blob, but its SHA did not match the precomputed sample.
- `invalid_before_valid_call`: the literal argument was malformed or duplicated before a valid tool call existed.

## Exact-success results

| Base64 chars | Decoded bytes | Expected Git blob SHA | Result |
|---:|---:|---|---|
| 12,000 | 9,000 | `0ccee7e7cd073be6163f143071419fe3e6805d33` | `success_exact` |
| 24,000 | 18,000 | `b9fdadb8961b223b118e2981337e594c5960f3e3` | `success_exact` |
| 48,000 | 36,000 | `7f1f0f0fe2d0cc9a501b23e4e77d5753d4538b29` | `success_exact` |
| 60,000 | 45,000 | `4e3c797f7ecf36ed96716b48c9ed09b1361bbbac` | `success_exact` |
| 61,440 | 46,080 | `ed985597470ff09a759ac1e3d74544ddc1b39cb4` | `success_exact`; independently referenceable by SHA |
| 64,000 | 48,000 | `6fca0618275488c9d7f8b21b081a5ad4333e2ef3` | `success_exact`; independently referenceable by SHA |

The 61,440- and 64,000-character expected blobs were independently checked by constructing a Git tree that referenced both expected blob SHAs. GitHub accepted the references; neither object was missing.

## Invalid/non-limit observation

An earlier 32,000-character attempt based on the PNG file prefix returned blob SHA:

`809185496e5d1e7ca461196e5608ab0d8d722231`

instead of expected:

`c3904d08319e2adf6c47b1d79670944c1c81a0dc`

It is classified as `delivered_but_distorted`, not as an outer-layer size failure. Later 48k–64k IDAT samples succeeded exactly, confirming that 32k was not a hard limit.

## Historical comparison

Earlier evidence includes:

- An 8,000-character JPEG base64 chunk was blocked when incorrectly sent as `encoding="utf-8"`; the same binary content succeeded when correctly sent with `encoding="base64"`.
- A separate 61,440-character high-entropy base64 call using `encoding="base64"` was once blocked by OpenAI outer safety checks before reaching GitHub.
- A 57,600-character low-entropy legal base64 payload succeeded.
- A 512-character single-line sample succeeded, while the same data with a newline was blocked once.

Therefore, the outer behavior is content/format-sensitive and non-deterministic; it is not a simple fixed character ceiling.

## Current conclusion

- No fixed outer-layer limit was found at or below **64,000 base64 characters** for a single-line, real PNG IDAT sample using `create_blob(encoding="base64")`.
- The experimentally demonstrated exact-success lower bound is **at least 64,000 base64 characters / 48,000 decoded bytes**.
- The previous 61,440-character block is not evidence of a hard 61,440-character ceiling.
- The absolute upper limit remains unknown.

## Production rule

For binary payloads:

1. Convert binary bytes to base64.
2. Use `create_blob(encoding="base64")`.
3. Do not send the base64 text as `encoding="utf-8"`.
4. Prefer conservative chunks (currently 8,000 base64 characters) for production reliability.
5. Verify decoded byte count, SHA-256, and Git blob SHA after transfer.

Direct `create_blob` probes create unreferenced Git objects unless attached to a commit. GitHub's Git Data API does not provide per-blob deletion; unreferenced objects are left for normal GitHub garbage collection.