# MCP payload lab

This branch is the retained evidence branch for ChatGPT/GitHub MCP payload experiments. It intentionally contains no production credentials, one-time workflow files, or trigger files.

## Durable binary-transfer rule

For GitHub binary data, encode the original bytes as base64 and call `create_blob(encoding="base64")`. Do not send the base64 text as `encoding="utf-8"`.

`encoding="base64"` is the correct data path, but it does not guarantee that the ChatGPT/OpenAI outer tool-call layer will accept arbitrarily large high-entropy arguments.

## End-to-end image result

The same 17,693-byte, 525×394 JPEG was transferred in two forms:

- `8,000 + 8,000 + 7,592` base64 characters;
- `6,000 + 6,000 + 6,000 + 5,592` base64 characters.

GitHub Actions reassembled both results. Both have SHA-256:

`affcd721922a68130806759b985ddd38c394b2f38b2a96bb0d46c9d9ca15b699`

The two final JPEGs are byte-for-byte identical.

- [8k×3 result](actions-results/8k-x3/result.jpg)
- [6k×4 result](actions-results/6k-x4/result.jpg)
- [Verification record](actions-results/verification.txt)
- [Image transfer manifest](actions-results/image-transfer-manifest.json)

## Observed boundaries

### ChatGPT/OpenAI outer tool-call layer

- An 8,000-character JPEG base64 segment sent as UTF-8 text was blocked once; the same content later succeeded with `encoding="base64"`.
- An approximately 61,440-character high-entropy base64 argument sent with `encoding="base64"` was blocked once before reaching GitHub.
- These are observed failures, not a permanent hard limit. The exact outer-layer boundary remains unresolved because the connector accepts literal strings rather than a local file reference; model-mediated copying of very long payloads is not byte-exact evidence unless the returned Git blob SHA matches the precomputed value.

### GitHub create_blob API, Actions-side control

- 12,000 through 60,000 base64 characters succeeded three times per size with exact Git blob SHA matching.
- Valid base64 blob creation later succeeded through **52 MiB of base64 characters** (39 MiB decoded bytes).
- **54 MiB of base64 characters** (40.5 MiB decoded bytes) returned HTTP 422: `Sorry, your input was too large to process`.
- The current observed GitHub API boundary is therefore between **52 and 54 MiB of base64 characters**. This is a GitHub API result, not the ChatGPT/OpenAI outer-layer limit.
- Commit-message probes up to 256 MiB of JSON body reached GitHub and returned the intended 422 without creating commits, so the blob failure is endpoint-specific rather than a general HTTP body limit in that range.

## Practical default

For ChatGPT → GitHub binary transfers, keep **8,000 base64 characters per chunk** as the evidence-backed default, retain an ordered manifest, and verify final byte size and SHA-256 after reconstruction. GitHub itself accepts much larger payloads; the conservative chunk size is for the ChatGPT tool-call path.

## Evidence index

- `round-1/`: visible small-image proof.
- `actions-results/8k-x3/` and `actions-results/6k-x4/`: retained chunks and reconstructed JPEGs.
- `actions-results/blob-size-ladder-v1/report.json`: 12k–60k, three repeats per size.
- `actions-results/blob-upper-bound-v2/report.json`: first upper-bound run; its invalid-encoding transport row is superseded.
- `actions-results/payload-envelope-v3/report.json`: valid large base64 creates and no-object request-body probes.
- `actions-results/blob-boundary-v4/report.json`: final 48–54 MiB-character interval test.

## Cleanup

Temporary runner branches are removed after evidence is consolidated here. Individual orphan Git blobs cannot be explicitly deleted through the Git Data API; unreachable test objects are left for GitHub garbage collection, with accidental side effects documented in the retained reports.
