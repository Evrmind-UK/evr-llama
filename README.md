# EVR-Llama Runtime Binaries

Pre-built binaries for running [Evrmind EVR-1](https://huggingface.co/evrmind) GGUF models locally. Built from [llama.cpp](https://github.com/ggerganov/llama.cpp) with EVR tensor support.

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

**Linux (CUDA):**

```bash
mkdir -p linux-cuda && tar xzf evrmind-linux-cuda.tar.gz -C linux-cuda
cd linux-cuda
LD_LIBRARY_PATH=. ./llama-cli -m /path/to/model.gguf -ngl 99
```

**macOS (Apple Silicon):**

```bash
mkdir -p metal && tar xzf evrmind-macos-metal.tar.gz -C metal
cd metal
./llama-cli -m /path/to/model.gguf -ngl 99
```

**Windows (CUDA):**

Extract `evrmind-windows-cuda.zip` into a folder called `windows-cuda`, then:

```cmd
cd windows-cuda
llama-cli.exe -m \path\to\model.gguf -ngl 99
```

**Android (Termux):**

```bash
mkdir -p android-vulkan && tar xzf evrmind-android-vulkan.tar.gz -C android-vulkan
cd android-vulkan
LD_LIBRARY_PATH=. ./llama-cli -m /path/to/model.gguf -ngl 99
```

The same binaries work with all EVR-1 models. Just point them at whichever GGUF you want to run.

## Web UI

Each model repository on HuggingFace includes a `start-server.sh` (Linux/macOS/Android) and `start-server.bat` (Windows) that launches a browser-based chat interface on http://localhost:8080. See the model README for details.

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
| EVR-1 Maano-8b-Instruct (coming soon) | Llama 3.1 8B Instruct | Chat, instruction following |
| EVR-1 Bafethu-8b-Reasoning (coming soon) | DeepSeek R1 Distill Llama 8B | Math, logic, coding |

## System Requirements

- 6 GiB RAM minimum (8 GiB recommended)
- GPU recommended for usable speeds (NVIDIA CUDA 12, Apple Silicon, or Vulkan)
- CPU-only mode is supported but slower (use `-ngl 0`)

## License

The binaries are built from llama.cpp (MIT License) with modifications by Evrmind. See the model repositories on HuggingFace for model-specific license terms.

## Contact

hello@evrmind.io
