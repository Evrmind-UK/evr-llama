# EVR-Llama Runtime Binaries

Pre-built binaries for running [Evrmind EVR-1](https://huggingface.co/evrmind) GGUF models locally. Built from [llama.cpp](https://github.com/ggerganov/llama.cpp) with EVR compression support.

EVR (Evrmind Reconstruction) is a novel compression method developed independently by Evrmind. On standard benchmarks, EVR achieves near-parity with industry-standard quantizations refined over years by the open-source llama.cpp community.

| Benchmark | EVR (3.93 GiB) | Q3_K_M (3.83 GiB) | Q4_K_M (4.69 GiB) |
|-----------|----------------|--------------------|--------------------|
| ARC-Challenge (25-shot, 1172q) | 59.8% | 60.8% | 61.3% |
| Perplexity (wikitext-2) | 6.19 | 6.13 | 5.74 |

## Supported Platforms

| Platform | Archive | GPU |
|----------|---------|-----|
| Linux + NVIDIA | `evrmind-linux-cuda.tar.gz` | CUDA 12 |
| Linux + Any GPU | `evrmind-linux-vulkan.tar.gz` | Vulkan |
| macOS (Apple Silicon) | `evrmind-macos-metal.tar.gz` | Apple Silicon |
| Windows + NVIDIA | `evrmind-windows-cuda.zip` | CUDA 12 |
| Windows + Any GPU | `evrmind-windows-vulkan.zip` | Vulkan |
| Android (Termux) | `evrmind-android-vulkan.tar.gz` | Vulkan |

## Quick Start

1. Download a model from HuggingFace (see [Available Models](#available-models))
2. Download the binary for your platform from [Releases](https://github.com/evrmind-uk/evr-llama/releases/tag/v1.0.0)
3. Extract and run:

**Linux + NVIDIA (CUDA):**

```bash
mkdir -p linux-cuda && tar xzf evrmind-linux-cuda.tar.gz -C linux-cuda
cd linux-cuda
LD_LIBRARY_PATH=. ./llama-cli -m /path/to/model.gguf -ngl 99
```

**Linux + Any GPU (Vulkan):**

```bash
mkdir -p linux-vulkan && tar xzf evrmind-linux-vulkan.tar.gz -C linux-vulkan
cd linux-vulkan
LD_LIBRARY_PATH=. ./llama-cli -m /path/to/model.gguf -ngl 99
```

**macOS (Apple Silicon):**

```bash
mkdir -p metal && tar xzf evrmind-macos-metal.tar.gz -C metal
cd metal
./llama-cli -m /path/to/model.gguf -ngl 99
```

**Windows + NVIDIA (CUDA):**

Extract `evrmind-windows-cuda.zip` into a folder called `windows-cuda`, then:

```cmd
cd windows-cuda
llama-cli.exe -m ..\model.gguf -ngl 99
```

**Windows + Any GPU (Vulkan):**

Extract `evrmind-windows-vulkan.zip` into a folder called `windows-vulkan`, then:

```cmd
cd windows-vulkan
llama-cli.exe -m ..\model.gguf -ngl 99
```

**Android (Termux):**

```bash
mkdir -p android-vulkan && tar xzf evrmind-android-vulkan.tar.gz -C android-vulkan
cd android-vulkan
LD_LIBRARY_PATH=. ./llama-cli -m /path/to/model.gguf -ngl 99
```

**CPU-only (any platform):**

Use `-ngl 0` instead of `-ngl 99` to run entirely on CPU. Slower, but works without a GPU.

The same binaries work with all EVR-1 models. Just point them at whichever GGUF you want to run.

## Web UI

Each model repository on HuggingFace includes `start-server.sh` (Linux/macOS/Android) and `start-server.bat` (Windows) that launch a browser-based interface on http://localhost:8080. See the model README for setup details.

## Included Binaries

Each archive contains:

| Binary | Purpose |
|--------|---------|
| `llama-cli` | Interactive text generation |
| `llama-server` | HTTP server with OpenAI-compatible API and web UI |
| `llama-completion` | Single-shot text completion |
| `llama-bench` | Performance benchmarking |
| `llama-quantize` | Model quantization tools |
| `llama-gguf` | GGUF file inspection |
| `llama-gguf-hash` | GGUF file hash verification |
| `llama-gguf-split` | Split/merge large GGUF files |

## Available Models

| Model | Base | Use Case |
|-------|------|----------|
| [EVR-1 Maano-8b](https://huggingface.co/evrmind/evr-1-maano-8b) | Llama 3.1 8B | Text completion, creative writing |
| [EVR-1 Maano-8b-Instruct](https://huggingface.co/evrmind/evr-1-maano-8b-instruct) | Llama 3.1 8B Instruct | Chat, instruction following |
| [EVR-1 Bafethu-8b-Reasoning](https://huggingface.co/evrmind/evr-1-bafethu-8b-reasoning) | DeepSeek R1 Distill Llama 8B | Math, logic, coding |

## System Requirements

- 6 GiB RAM minimum (8 GiB recommended)
- GPU recommended for usable speeds (NVIDIA CUDA 12, Apple Silicon, or Vulkan)
- CPU-only mode is supported but slower (use `-ngl 0`)

## Build Info

These binaries are built from llama.cpp (commit b5549, 2026-02) with added support for EVR tensor types. The `llama-completion` binary is a custom addition for single-shot text completion.

## License

MIT License (see [LICENSE](LICENSE)). Built from llama.cpp with modifications by Evrmind. Model-specific license terms are available in each model's HuggingFace repository.

## Contact

hello@evrmind.io
