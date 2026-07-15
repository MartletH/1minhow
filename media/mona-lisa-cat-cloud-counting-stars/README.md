# Mona Lisa Cat cloud-counting stars — 16k base64 chunk transfer test

This branch is reserved for testing image transfer into GitHub using 16 KiB base64 chunks.

Requested asset:

- `mona-lisa-cat-cloud-counting-stars-256kb.jpg`
- `mona-lisa-cat-cloud-counting-stars-512kb.jpg`

Planned branch:

- `mona-lisa-cat-cloud-counting-stars`

## Current status

Branch created successfully.

The ChatGPT GitHub connector available in this session can create UTF-8 text files, branches, blobs, trees, and commits, but it does not expose a direct local-file or directory upload parameter for `create_file`.

Therefore, a direct upload of many local generated chunk files is not automatic in this connector. The safe production path is to run the chunking script locally/Codex-side and push with `git`.

## Chunk format

Each image should be converted to base64 and split into exactly 16 KiB text chunks:

```bash
python3 - <<'PY'
from pathlib import Path
import base64, hashlib, json

chunk_chars = 16 * 1024
for p in [
    Path('mona-lisa-cat-cloud-counting-stars-256kb.jpg'),
    Path('mona-lisa-cat-cloud-counting-stars-512kb.jpg'),
]:
    raw = p.read_bytes()
    b64 = base64.b64encode(raw).decode('ascii')
    out = Path(p.stem)
    out.mkdir(parents=True, exist_ok=True)
    chunks = [b64[i:i+chunk_chars] for i in range(0, len(b64), chunk_chars)]
    for i, chunk in enumerate(chunks, 1):
        (out / f'chunk-{i:03d}.b64').write_text(chunk, encoding='ascii')
    (out / 'manifest.json').write_text(json.dumps({
        'source_filename': p.name,
        'binary_bytes': len(raw),
        'binary_sha256': hashlib.sha256(raw).hexdigest(),
        'base64_chars': len(b64),
        'base64_sha256': hashlib.sha256(b64.encode('ascii')).hexdigest(),
        'chunk_chars': chunk_chars,
        'chunk_count': len(chunks),
        'last_chunk_chars': len(chunks[-1]),
    }, indent=2), encoding='utf-8')
PY
```

## Reconstruct

```bash
cat mona-lisa-cat-cloud-counting-stars-256kb/chunk-*.b64 | base64 -d > mona-lisa-cat-cloud-counting-stars-256kb.jpg
cat mona-lisa-cat-cloud-counting-stars-512kb/chunk-*.b64 | base64 -d > mona-lisa-cat-cloud-counting-stars-512kb.jpg
sha256sum mona-lisa-cat-cloud-counting-stars-*.jpg
```

## Expected local metadata from this ChatGPT session

```json
{
  "256kb": {
    "binary_bytes": 260702,
    "binary_sha256": "4d61de6a7811240a9050fe784330bc8ef835b324cddda2e0f83cc14efde6f99c",
    "base64_chars": 347604,
    "chunk_count": 22,
    "last_chunk_chars": 3540
  },
  "512kb": {
    "binary_bytes": 523959,
    "binary_sha256": "212b56187258a204505e4049084f2b60fa013e9b4ff3f2413dc634eac775df05",
    "base64_chars": 698612,
    "chunk_count": 43,
    "last_chunk_chars": 10484
  }
}
```

## Important distinction

This is a segmented text transfer path, not a single tool-call image upload and not a one-shot literal fidelity test.

Recommended production path:

1. Generate image variants locally or in Codex.
2. Split to 16 KiB `.b64` chunks.
3. Commit the chunk files and manifests with `git`.
4. Push to a dedicated media branch.
5. Reconstruct and verify SHA before using the image.
