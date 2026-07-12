# ChatGPT/OpenAI outer tool-call limit experiment

This temporary branch isolates the ChatGPT/OpenAI tool-call path from the GitHub API limit.

## Layers under test

1. Model serialization of a literal tool argument.
2. ChatGPT/OpenAI outer safety and request handling.
3. GitHub connector action.
4. GitHub API.

GitHub API capacity is already controlled separately and is not the target of this run.

## Evidence rules

A result counts only when the payload reaches a persistent GitHub path or returns a Git blob SHA that can be matched to a precomputed value.

Classifications:

- exact success: request accepted and byte-exact readback/hash verification passes;
- blocked: OpenAI outer safety explicitly rejects before GitHub;
- transport/tool failure: non-safety request failure;
- invalid sample: the call reaches GitHub but the literal payload differs from the intended bytes.

## Test stages

### Stage A — persistent outer transport envelope

Use dedicated `create_file` paths with deterministic repeated lines, then read them back and measure exact bytes. Planned sizes: 64 KiB, 96 KiB, 128 KiB, 192 KiB, 256 KiB, followed by bisection after the first failure.

### Stage B — `create_blob(encoding="base64")` complexity curve

Use calibrated legal base64 periodic blocks with periods of 64, 256, 1024 and 4096 characters. Test the same total sizes to distinguish payload size from content complexity.

### Stage C — real high-entropy binary confirmation

Near the observed boundary, test real JPEG/base64 data at 48k, 56k, 60k, 62k and 64k characters, three attempts per point where byte-exact sample construction is possible.

## Boundary definition

- stable working maximum: largest point with 3/3 byte-exact successes;
- unstable zone: mixed success/block/failure outcomes;
- observed failure minimum: smallest point with 0/3 outer-layer blocks;
- no result is described as a permanent platform hard limit without repeated evidence.

## Cleanup

After consolidation into the retained `mcp-payload-lab` evidence branch, this temporary branch and one-off payload files will be deleted. Unreferenced Git blobs cannot be explicitly deleted and are left to GitHub garbage collection.