# Neura Programming Language

<div align="center">

**A domain-specific programming language for AI, neural networks, and machine learning**

*Combining Python's simplicity with C++'s performance for ML workflows*

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)
[![Rust](https://img.shields.io/badge/Rust-1.70%2B-orange.svg)](https://www.rust-lang.org/)
[![Status](https://img.shields.io/badge/Status-In%20Development-yellow.svg)]()

</div>

---

## 🚀 Overview

Neura is a cutting-edge programming language designed specifically for AI researchers, data scientists, and ML practitioners. It provides native support for tensor operations, automatic differentiation, distributed computing, and ML workflows—all with minimal boilerplate and maximum performance.

### Why Neura?

- **🎯 ML-First Design**: Built from the ground up for neural networks and deep learning
- **⚡ High Performance**: Compiled to optimized machine code with native GPU support
- **🐍 Familiar Syntax**: Python-inspired, declarative syntax for rapid prototyping
- **🔧 Deep Control**: Fine-grained control over memory, hardware, and optimizations
- **🔗 Seamless Interop**: Native integration with Python, PyTorch, and TensorFlow
- **🛠️ Developer Experience**: First-class tooling with REPL, gradient inspection, and visualization

## ✨ Key Features

### Native Tensor Operations
```neura
tensor[float32, (64, 784)] inputs
tensor[float32, (784, 10)] weights
tensor[float32, (64, 10)] output = inputs @ weights  # Shape-checked at compile time
```

### Declarative Model Definitions
```neura
model Transformer:
  layers:
    MultiHeadAttention(heads=8)  # Context-aware defaults
    FeedForward(units=2048, activation=gelu)
    LayerNorm
  stack: 6
```

### Streamlined Data Pipelines
```neura
pipeline data:
  source: "corpus.txt" -> tokenize(vocab_size=50000) -> batch(size=64)
```

### Elegant Training Configuration
```neura
train model:
  data: data
  optimizer: AdamW(learning_rate=0.0001)
  loss: CrossEntropy
  epochs: 50
  distribute: [gpu(0), gpu(1)]
  checkpoint: "model-v{epoch}.ckpt" { hyperparameters }
  inspect: gradients(layer=2)
```

## 🎯 Design Goals

1. **Simplicity**: Python-inspired syntax for rapid prototyping and readability
2. **Performance**: Compiled execution rivaling C++ with zero-cost abstractions
3. **Domain Focus**: Streamlined for neural network design, training, and inference
4. **Interoperability**: Seamless integration with existing ML ecosystems
5. **Productivity**: First-class tooling tailored for ML workflows

## 🔧 Tech Stack

### Frontend
- **REPL Interface**: Rust's std with reedline for enhanced UX
- **IDE Plugin**: TypeScript for VS Code extension
- **Visualization**: TensorBoard integration and Tauri-based dashboard

### Backend
- **Language**: Rust
- **Compiler**: LLVM-based with WASM target support
- **IR**: Custom MLIR-inspired intermediate representation
- **GPU**: CUDA (via cust), OpenCL (via opencl3)
- **Tensor Runtime**: candle (LLM inference), tch-rs (training), tract (ONNX)
- **Auto Differentiation**: tch-rs (reverse-mode AD), custom engine
- **Parallelism**: Rayon for multi-threading, MPI for clusters

### Key Libraries
- **Parser**: pest (Rust-native PEG parser)
- **Tokenization**: tokenizers (BPE, SentencePiece)
- **Model I/O**: safetensors, tract (ONNX), ggml-rs (GGUF)
- **Python Interop**: PyO3 with maturin
- **Testing**: cargo test, criterion (benchmarks)

## 📦 Installation

> **Note**: Neura is currently in active development. Installation instructions will be provided as we approach the first release.

```bash
# Clone the repository
git clone https://github.com/andreimotin/neura.git
cd neura

# Build from source
cargo build --release

# Run tests
cargo test
```

## 🚦 Getting Started

### Hello World
Create a file `hello.neura`:

```neura
# File: hello.neura
model SimpleNN:
  layers:
    Dense(units=128, activation=relu)
    Dense(units=10, activation=softmax)

pipeline data:
  source: "mnist.csv" -> normalize -> batch(size=32)

train SimpleNN:
  data: data
  optimizer: AdamW(learning_rate=0.001)
  loss: CrossEntropy
  epochs: 10
```

### Run in REPL
```bash
neura repl
> load "hello.neura"
> inspect: model
> visualize: training_loss
```

## 📚 Example Programs

### Simple Neural Network
```neura
model MLP:
  layers:
    Dense(units=128, activation=relu)
    Dense(units=64, activation=relu)
    Dense(units=10, activation=softmax)

pipeline data:
  source: "data.csv" -> normalize -> shuffle -> batch(size=64)

train MLP:
  data: data
  optimizer: SGD(learning_rate=0.01)
  loss: CrossEntropy
  epochs: 20
  distribute: [gpu(0)]
```

### Transformer for LLMs
```neura
model SimpleLLM:
  layers:
    MultiHeadAttention(heads=8)
    FeedForward(units=2048, activation=gelu)
    LayerNorm
  stack: 4

pipeline data:
  source: "wiki.txt" -> tokenize(vocab_size=50000) -> batch(size=64)

train SimpleLLM:
  data: data
  optimizer: AdamW(learning_rate=0.0001)
  loss: CrossEntropy
  epochs: 20
  checkpoint: "llm-v{epoch}.ckpt" { hyperparameters }
  inspect: gradients(layer=1)

predict SimpleLLM:
  input: tokenize("Hello, AI!")
  output: next_token
```

## 🗺️ Roadmap

### Phase 1: Core Language (Months 1-2)
- ✅ Project setup and infrastructure
- 🔄 Parser and AST implementation using pest
- 🔄 Type system with tensor support
- 🔄 Basic compiler infrastructure with LLVM

### Phase 2: Runtime & ML Primitives (Months 2-4)
- ⏳ Tensor runtime with automatic differentiation
- ⏳ CUDA code generation for GPU support
- ⏳ Neural network primitives (Dense, Conv2D, Attention)
- ⏳ Data pipeline implementation

### Phase 3: Developer Tools (Months 4-5)
- ⏳ REPL environment with reedline
- ⏳ Python interoperability via PyO3
- ⏳ Basic visualization and gradient inspection
- ⏳ Comprehensive test suite

### Phase 4: Polish & Release (Months 5-6)
- ⏳ Documentation and examples
- ⏳ Performance optimizations
- ⏳ Community feedback integration
- ⏳ MVP public release

**Legend**: ✅ Complete | 🔄 In Progress | ⏳ Planned

## 🎯 Success Metrics

We're aiming for:
- **100+ GitHub stars** within first month after public release
- **10+ external contributors** within 3 months
- **3+ research papers** citing Neura usage within 1 year
- **30% reduction** in code size vs. equivalent PyTorch implementations
- **2x performance improvement** over Python implementations

## 🤝 Contributing

We welcome contributions! Neura is an open-source project licensed under Apache 2.0.

> **Note**: Detailed contribution guidelines will be available in `CONTRIBUTING.md` soon.

### How to Contribute
1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'feat: add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Development Setup
```bash
# Install Rust toolchain
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

# Clone and build
git clone https://github.com/andreimotin/neura.git
cd neura
cargo build

# Run tests
cargo test
```

## 📖 Documentation

- [Language Specification](neura-spec.md) - Complete language design and syntax
- [Getting Started Guide](docs/getting_started.md) - *(Coming Soon)*
- [API Reference](docs/api.md) - *(Coming Soon)*
- [Examples](examples/) - Sample Neura programs

## 🌟 Why Choose Neura?

| Feature | Python/PyTorch | Julia | C++ | Neura |
|---------|---------------|-------|-----|-------|
| ML-Specific Syntax | ❌ | ⚠️ | ❌ | ✅ |
| Compile-Time Shape Checking | ❌ | ⚠️ | ❌ | ✅ |
| Native GPU Support | ⚠️ | ⚠️ | ✅ | ✅ |
| Declarative Models | ⚠️ | ❌ | ❌ | ✅ |
| Python Interop | ✅ | ⚠️ | ❌ | ✅ |
| Zero-Cost Abstractions | ❌ | ⚠️ | ✅ | ✅ |
| Built-in Visualization | ⚠️ | ⚠️ | ❌ | ✅ |

## 📄 License

This project is licensed under the Apache License 2.0 - see the [LICENSE](LICENSE) file for details.

## 🔗 Links

- **Repository**: [github.com/andreimotin/neura](https://github.com/andreimotin/neura)
- **Website**: [neuralang.github.io](https://neuralang.github.io/)
- **Documentation**: *(Coming Soon)*
- **Discord Community**: *(Coming Soon)*
- **Twitter**: *(Coming Soon)*

## 🙏 Acknowledgments

Neura builds upon the excellent work of many open-source projects:
- [Rust Programming Language](https://www.rust-lang.org/)
- [LLVM Compiler Infrastructure](https://llvm.org/)
- [Candle ML Framework](https://github.com/huggingface/candle)
- [PyTorch](https://pytorch.org/)
- And many more...

---

<div align="center">

**Built with ❤️ for the ML community**

*Star ⭐ this repo if you find it interesting!*

</div>

