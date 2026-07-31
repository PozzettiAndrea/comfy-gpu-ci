# comfy-ci

Central CUDA CI dispatcher for ComfyUI custom nodes.

CPU tests run per-repo on GitHub-hosted runners (free). CUDA tests run here on self-hosted runners with NVIDIA GPUs, inside Docker containers for isolation.

## How it works

1. Dashboard or manual dispatch triggers `test-cuda.yml` with `node_repo`, `branch`, and `platform`
2. Self-hosted runner picks up the job
3. `comfy-test run --cuda --publish` runs inside a Docker container with GPU passthrough
4. Results (screenshots, videos, logs, results.json) are pushed to the node repo's gh-pages branch
5. The node repo's PR gate checks gh-pages for passing results matching the PR commit

## Supported platforms

- `windows-cuda` — Windows container with NVIDIA GPU passthrough (`--isolation=process --device class/...`)
- `linux-cuda` — Linux container with `--gpus all`
- `windows-portable-cuda` — Portable ComfyUI build on Windows GPU

## Runners

Self-hosted runners registered to this repo:
- `andrej-windows` (Xeon 18C/36T, 32GB, RTX 3090)
- `andredupuy-windows` (Ryzen 6C/12T, 32GB, RTX 5060)
- `andrew-windows` (Ryzen 6C/12T, 16GB, RTX 4060 Ti)
- `andrea-windows` (Xeon 20C/40T, 64GB, RTX 3090)
- `ondrej-linux` (Xeon 14C/28T, 32GB, RTX 2060 Super)
