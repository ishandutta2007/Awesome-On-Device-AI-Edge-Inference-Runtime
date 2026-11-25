# Awesome-On-Device-AI-Edge-Inference-Runtime

# Awesome On-Device AI & Edge Inference Runtime

> A curated list of top On-Device AI and Edge Inference Runtime platforms — both SaaS/Hosted commercial solutions and open-source alternatives for running foundation models locally on laptops, desktops, and edge hardware.
> 🌟 Star this repo if you find it useful! 🌟

---

## 📋 Table of Contents

- [SaaS / Hosted Platforms](#-saas--hosted-platforms)
  - [Ollama Cloud](#ollama-cloud)
  - [LM Studio](#lm-studio)
- [Open-Source Software](#-open-source-software)
  - [Ollama (Local)](#ollama-local)
  - [Jan](#jan)
  - [LocalAI](#localai)
  - [llamafile](#llamafile)
  - [Exo](#exo)
  - [mlx-serve](#mlx-serve)
  - [vLLM](#vllm)
  - [TrnRT (RunanywhereAI)](#trnrt-runanywhereai)

---

## 🟦 SaaS / Hosted Platforms

Commercial, cloud-hosted inference services that complement on-device workflows. These are not open-source but are included as reference points for feature comparison.

### Ollama Cloud
**Type:** Cloud-hosted model inference within the Ollama ecosystem
Ollama Cloud extends the Ollama platform with cloud-hosted models that remain accessible through local tools and integrations. Cloud models run in Ollama's infrastructure but are invoked via the same CLI, local API, and official libraries used for local models. Users sign in with `ollama signin` and run cloud models with the `:cloud` suffix (e.g., `gemma4:cloud`). **Important:** Cloud access requires a paid plan or purchased usage credits [citation:2].  
**Best for:** Ollama users wanting to offload inference to the cloud for larger models while keeping their local tooling and workflows intact.

### LM Studio
**Type:** Desktop GUI for local and remote model inference
LM Studio provides a polished desktop application for running local models, with a built-in model browser, chat interface, and OpenAI-compatible API server. Recent releases added support for MTP draft models and Anthropic-compatible `/v1/messages` endpoints [citation:10]. **Important:** LM Studio is **not open-source**—its core application is proprietary, though it uses open-source runtimes like llama.cpp underneath. A comparison table notes it is "GUI-managed" and cannot be embedded in headless pipelines [citation:6].  
**Best for:** Users wanting a user-friendly desktop GUI for local model experimentation without command-line configuration.

---

## 🟩 Open-Source Software

Self-hosted, community-driven on-device inference runtimes and local AI platforms.

### Ollama (Local)
**Stack:** Go / llama.cpp | **License:** MIT
Ollama is the most accessible open-source tool for running LLMs locally, with a single-binary installation, a built-in model library, and an OpenAI-compatible API. It uses llama.cpp under the hood and is the default choice for local development and experimentation with open models. The platform supports macOS, Windows, and Linux, with full offline operation once models are downloaded.  
**Best for:** Developers wanting the simplest path to running models locally on laptops or workstations, accepting lower throughput than production-grade serving engines.

### Jan
**Stack:** TypeScript / llama.cpp / MCP | **License:** Apache-2.0
Jan is an open-source alternative to Claude and ChatGPT that runs entirely on your hardware, with built-in foundation models and an application ecosystem. Key capabilities include autonomous AI agents that can read files, manage calendars, and take actions via WhatsApp, Discord, or Slack; MCP server integration; and a local OpenAI-compatible API server. The platform is available for macOS, Windows, and Linux with full offline support [citation:4].  
**Best for:** Users wanting a complete local AI assistant with agent capabilities and MCP integration, built on an open-source foundation.

### LocalAI
**Stack:** Go / llama.cpp / multiple backends | **License:** MIT
LocalAI is an open-source OpenAI-compatible API that runs models locally across multiple backends, supporting text generation, image generation, audio transcription, and embeddings. It provides a unified local API surface across multiple model types without cloud dependencies.  
**Best for:** Teams wanting a single local API for diverse model types (text, image, audio) while maintaining full data privacy.

### llamafile
**Stack:** Cosmopolitan Libc / llama.cpp | **License:** Apache-2.0
llamafile packages a model and the inference engine into a single executable file that runs on multiple operating systems without installation. It uses the Cosmopolitan Libc to create portable binaries, making it the simplest way to distribute a self-contained local model.  
**Best for:** Users wanting a zero-dependency, single-file local inference experience that works across platforms without setup.

### Exo
**Stack:** Python / MLX | **License:** Open Source (GitHub)
Exo is open-source software that connects multiple devices into a single AI cluster, splitting large models across machines so you can run models bigger than any single device holds. It uses Apple's MLX for inference and serves OpenAI, Claude Messages, and Ollama-compatible APIs. Devices find each other automatically, and Exo measures each device's memory and link speed to decide how to split the model [citation:12].  
**Best for:** Users with multiple Apple Silicon Macs wanting to pool resources to run models that exceed single-device memory limits.

### mlx-serve
**Stack:** Python / MLX / Apple Silicon | **License:** MIT
mlx-serve is a local inference server for Apple Silicon that hot-swaps MLX models on demand, supporting text, vision, embeddings, TTS, STT, and decision models. It loads exactly one model at a time to stay within unified memory limits, with subprocess isolation for text/vision models and auto-unload on inactivity. Key features include an OpenAI-compatible API, prompt caching, and per-request `keep_alive` controls [citation:6].  
**Best for:** Apple Silicon users wanting a headless, scriptable MLX inference server with multi-model support and memory management.

### vLLM
**Stack:** Python / CUDA | **License:** Apache-2.0
vLLM is the leading open-source high-throughput LLM inference and serving engine, widely used for self-hosted production inference. It powers many commercial inference platforms behind the scenes and is the de facto standard for teams with GPU infrastructure. Recent versions include support for speculative decoding and specialized hardware backends [citation:7][citation:14].  
**Best for:** Teams with dedicated GPU infrastructure wanting maximum throughput and efficient GPU utilization for self-hosted LLM serving.

### TrnRT (RunanywhereAI)
**Stack:** Python / AWS Trainium / NKI | **License:** Open Source (per repository)
TrnRT is an open inference engine for large language models on **AWS Trainium**. It serves an OpenAI-compatible API from a single `trn2.48xlarge` instance, runs decode as NKI megakernels (approximately one kernel per layer half), and maintains a prefix cache across device and host memory. **GLM-5.3-Flash is the first supported model**, with more open models planned. Features include 1M-token context via sparse attention and linear attention, a radix-tree prefix cache over FP8 KV pages, and offline compilation on x86_64 hosts [citation:8].  
**Best for:** Teams deploying on AWS Trainium hardware wanting an open, high-performance inference engine with OpenAI API compatibility.

---

## 📊 Comparison at a Glance

| Software | License | Stack | Hardware | Multi-Device | OpenAI API | Best For |
|----------|---------|-------|----------|--------------|------------|----------|
| **Ollama Cloud** | Proprietary | Cloud | Cloud | ❌ | ✅ | Cloud offload for Ollama users |
| **LM Studio** | Proprietary | Desktop | Local | ❌ | ✅ | GUI-based local inference |
| **Ollama (Local)** | MIT | Go/llama.cpp | Local | ❌ | ✅ | Simplest local setup |
| **Jan** | Apache-2.0 | TypeScript | Local | ❌ | ✅ | Local AI assistant + agents |
| **LocalAI** | MIT | Go/multi-backend | Local | ❌ | ✅ | Unified multi-modal local API |
| **llamafile** | Apache-2.0 | Cosmopolitan | Local | ❌ | (Check) | Single-file portable inference |
| **Exo** | Open Source | Python/MLX | Apple Silicon | ✅ | ✅ | Pooling multiple Macs |
| **mlx-serve** | MIT | Python/MLX | Apple Silicon | ❌ | ✅ | Headless MLX server |
| **vLLM** | Apache-2.0 | Python/CUDA | NVIDIA GPU | ❌ | ✅ | High-throughput production |
| **TrnRT** | Open Source | Python/Trainium | AWS Trainium | ❌ | ✅ | Trainium-native inference |

---

## 🤝 Contributing

Contributions are welcome! If you know of an open-source on-device AI or edge inference runtime that should be listed here, please open a pull request with:

- Project name and URL
- Brief description (1–2 sentences)
- Stack and license
- Why it stands out

Please ensure the project is actively maintained (releases within the last 12 months) and genuinely open-source.

**Note on the ecosystem:** The on-device AI and edge inference landscape splits between **local desktop tools** (Ollama, Jan, LM Studio) for individual users, **Apple Silicon-optimized runtimes** (mlx-serve, Exo) for Mac hardware, and **production serving engines** (vLLM, TrnRT) for GPU and specialized accelerator infrastructure. **Ollama** remains the simplest entry point for local experimentation . **Jan** offers the most complete open-source local AI assistant with agent capabilities and MCP integration . **Exo** uniquely enables pooling multiple Macs to run models larger than any single device can hold . **vLLM** is the standard for self-hosted production inference on NVIDIA GPUs, while **TrnRT** fills the gap for AWS Trainium users . No single open-source project covers every hardware target and use case, but these tools collectively address the full spectrum of on-device and edge inference needs.

---

## 📄 License

This list is released under CC0 1.0 Universal (Public Domain). The software projects listed retain their respective licenses.

---

⭐ **If this list helped you discover a useful tool, please star the repo!** ⭐
