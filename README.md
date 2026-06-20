[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.20752769.svg)](https://doi.org/10.5281/zenodo.20752769) [![License](https://img.shields.io/badge/License-All%20Rights%20Reserved-red)]() [![TernML Site](https://img.shields.io/badge/TernML-Live%20Site-blue?style=for-the-badge)](https://fakeonomics.github.io/TernML-overview/)

# TernML: Multi-Architecture Ternary Machine Learning Framework

First neural network framework with **discrete ternary weights** {-1, 0, +1}.  
**1.58 bits/param · 5 architectures · 84% CIFAR-10 · 0 DSP inference · C codegen for Cortex-M0+**

Supports **5 architectures**: GraphKAN, CNN, Transformer, RNN/LSTM, Vision Transformer (ViT).  
All with the same 4-phase QAT pipeline and **regularization-by-quantization** effect.

## Key Results

| Architecture | Dataset | Accuracy | Model Size |
|-------------|---------|:--------:|:----------:|
| GraphKAN 256→100→10 | MNIST | **96.15%** | **15.4 KB** |
| GraphKAN 256→100→10 | Fashion-MNIST | **84.67%** | **15.4 KB** |
| CNN conv32→64→128→10 | CIFAR-10 | **84.03%** | **~100 KB** |
| CNN conv32→64→FC128→10 | Fashion-MNIST | **92.02%** | **102.8 KB** |
| Transformer 2L/4H/128d | CIFAR-10 | TBD | TBD |
| LSTM 128d | Sequence | TBD | TBD |
| ViT patch8/128d | CIFAR-10 | TBD | TBD |

All improve over float baseline — **regularization-by-quantization**.

## Features

- **5 architectures**: Graph, CNN, Transformer, RNN, ViT — unified `TernMLayer`
- **C codegen**: Cortex-M0+ output, p/m bit-sliced format (32 trits/chunk)
- **ELM mode**: Frozen random ternary hidden layer + closed-form least squares
- **95 passing tests**: core + transformer + rnn + codegen + vit + pm_format
- **Gamma absorption**: Absorb scaling into batch norm during inference

## Novel Contributions

1. **Universal ternary framework** — 5 architectures, one QAT pipeline
2. **Regularization-by-quantization** — ternary improves accuracy over float baseline
3. **p/m bit-sliced packing** — 32 trits → 8 bytes (positive mask + negative mask as uint32 LE)
4. **Cortex-M0+ codegen** — output pure C with no DSP, no FPU
5. **Hardware-efficient** — weight multiplication is a multiplexer (pass/negate/zero)

## Hardware Targets

| Target | Memory | Suitability |
|--------|:------:|:-----------:|
| Cortex-M0+ ($0.50 MCU) | 16 KB L1 | ✅ Codegen target |
| ESP32-S3 | 512 KB SRAM | ✅ Full pipeline |
| RISC-V GD32V | 32 KB | ✅ Core models |
| MIK32 Amur (Микрон) | 8 KB | ✅ Sub-8KB models |

## Status

Proprietary technology — All Rights Reserved.  
Codebase is private. [Paper on Zenodo](https://doi.org/10.5281/zenodo.20752769).  
For licensing inquiries, contact via GitHub.
