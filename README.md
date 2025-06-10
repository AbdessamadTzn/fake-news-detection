# Fake News Detection — LLM Fine-Tuning Environment Setup

## Objective

Setting up a local environment to train and fine-tune LLMs (LLaMA or GGUF-based) for the task of **fake news detection**, possibly using tools like instructlab, llama.cpp, and optionally vLLM.

---

## Initial Setup Summary

### Base System Preparation

- Using WSL or Linux-based CLI for development.
- Created a Python virtual environment using python3 -m venv venv and source venv/bin/activate
- Installed base tools and dependencies with sudo apt update && sudo apt install -y build-essential cmake

### Installed ninja

- Installed ninja build system to speed up compilation (required by some low-level libraries like llama.cpp or when building PyTorch from source).
- Command used: sudo apt install ninja-build

📌 **Why:** Faster builds during native C++ compilation and compatibility with LLaMA-related tooling (like llama.cpp, instructlab).

### Installed instructlab

- Installed instructlab, Red Hat's tool for community-driven LLM fine-tuning.
- Command used: pip install instructlab --upgrade

⚠️ Faced dependency conflicts (especially around torch, transformers, and vllm).

---

## Problems Faced

### vLLM Installation Conflicts

- Tried installing vllm==0.9.0.post1 → version not available.
- Attempted install of vllm==0.9.0.1:
  - Forced downgrades of torch, transformers, torchvision
  - Broke existing installations (instructlab, etc.)
  - Caused out-of-memory crash (Killed error).

    **Lesson:** vLLM is extremely sensitive to PyTorch version compatibility (usually demands torch==2.7.0 and specific transformer versions).

### RAM/CPU Constraints

- Hit Killed errors due to high memory usage when trying to install or compile large packages (e.g., torch, gguf, or during vllm install).
- Likely causes:
  - Limited WSL memory config or swap space.
  - Heavy packages requiring >4GB+ RAM to compile or install.

**Potential Fixes (TBD):**
- Avoid memory-heavy tools like vllm unless GPU+RAM is sufficient.
- Use lighter tools like llama.cpp for local inference.
- Consider increasing WSL memory/swap settings if possible.

---

## Current Status

- Environment partially set up.
- Planning to restart clean due to package conflicts.
- Will proceed with installing only the minimum required tools to fine-tune a LLaMA model or GGUF format without vllm.

---