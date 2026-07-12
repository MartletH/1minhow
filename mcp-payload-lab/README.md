# MCP payload lab

This branch is reserved for public connector payload verification.

## Round 1 visible GitHub proof

The image below was written by the GitHub MCP path:

`create_blob(encoding=base64) -> create_tree -> create_commit -> update_ref`

![GitHub MCP base64 proof](round-1/github-base64-proof.jpg)

Verification metadata is stored in [`round-1/manifest.json`](round-1/manifest.json).

The visible proof image is a 160×120 derivative kept below the conservative 8k-class base64 payload threshold. The previously tested full-size 525×394 image passed three-chunk read-back, reconstruction, and SHA-256 verification.
