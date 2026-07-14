# Mona Lisa Cat cloud-counting image upload manifest

This branch was created for testing how to publish generated image assets into the public `1minhow` GitHub repository.

Branch:

```text
media/mona-lisa-cat-cloud-counting-stars
```

Source image:

```text
mona-lisa-cat-cloud-counting-stars.png
B: cloud-counting stars scene
1122 x 1402 px
original PNG about 3.1-3.2 MiB
```

## Requested tiers

Only the two useful compressed tiers are tracked here:

| Tier | Local filename | Size | Dimensions | SHA-256 | Google Drive status |
|---:|---|---:|---:|---|---|
| 256 KiB | `mona-lisa-cat-cloud-counting-stars-256kb.jpg` | 260,702 bytes | 1122 x 1402 | `4d61de6a7811240a9050fe784330bc8ef835b324cddda2e0f83cc14efde6f99c` | uploaded to `media-share`: `1zLUJ47QHqIJl3di4VHzHYJSy7K3mJvzb` |
| 512 KiB | `mona-lisa-cat-cloud-counting-stars-512kb.jpg` | 523,959 bytes | 1122 x 1402 | `212b56187258a204505e4049084f2b60fa013e9b4ff3f2413dc634eac775df05` | uploaded to `media-share`: `1bsMuzUudx6Uct0AhIIYyVcy0eU0N_RHX` |

Drive links:

- 256 KiB: https://drive.google.com/file/d/1zLUJ47QHqIJl3di4VHzHYJSy7K3mJvzb/view?usp=drivesdk
- 512 KiB: https://drive.google.com/file/d/1bsMuzUudx6Uct0AhIIYyVcy0eU0N_RHX/view?usp=drivesdk

## Connector boundary found

The current ChatGPT GitHub connector can write small UTF-8 text files through `create_file` and can create Git blobs from base64. However, for binary image upload there are two different paths:

1. `create_file`: text-only wrapper; not suitable for raw JPEG bytes.
2. `create_blob`: can create binary blobs from base64, but the connector call requires the full base64 string in one argument. For these files that would be about 348k chars for 256 KiB and about 699k chars for 512 KiB.

Because this project is specifically testing 16k-safe transfer behavior, using one huge base64 argument would defeat the purpose of the test. Therefore this branch currently records the asset metadata and Drive-backed files, but does not claim that the JPEG bytes were committed to GitHub as binary blobs through a 16k chunk-safe path.

## Recommended future upload method

For actual public GitHub image hosting, use a local git/Codex workflow rather than ChatGPT Web connector literal transfer:

```bash
repo=~/path/to/1minhow
branch=media/mona-lisa-cat-cloud-counting-stars
asset_dir=assets/images/mona-lisa-cat-cloud-counting-stars

git -C "$repo" fetch origin
git -C "$repo" checkout -B "$branch" origin/main
mkdir -p "$repo/$asset_dir"
cp /path/to/mona-lisa-cat-cloud-counting-stars-256kb.jpg "$repo/$asset_dir/"
cp /path/to/mona-lisa-cat-cloud-counting-stars-512kb.jpg "$repo/$asset_dir/"
sha256sum "$repo/$asset_dir"/*.jpg

git -C "$repo" add "$asset_dir"
git -C "$repo" commit -m "media: add Mona Lisa cat compressed images"
git -C "$repo" push -u origin "$branch"
```

That route avoids copying image bytes through ChatGPT message/tool-call literals. It also preserves the real binary files directly in GitHub where GitHub can render or serve them normally.

## Memory-worthy rule

For future image upload to GitHub:

- Do not use ChatGPT Web `create_file` for binary image bytes; it is a text wrapper.
- Do not paste large base64 into one connector argument when the goal is 16k-safe fidelity.
- Preferred route: upload/generate image locally or in Drive, then ask Codex/local git to copy binary files into the repo and push a branch.
- If connector-only transfer is unavoidable, record it as a connector-base64 blob upload, not a 16k-safe chunked transfer.
