# AI Hardware - Comprehensive Guide

## Overview
GCP provides specialized hardware for accelerating Machine Learning (ML) workloads, High Performance Computing (HPC), and massive simulations.

---

## 1. Tensor Processing Units (TPUs)
- **What is it?**: A custom ASIC (Application-Specific Integrated Circuit) designed by Google specifically for machine learning.
- **Architecture**:
  - **Matrix Multiplication Unit (MXU)**: The core engine.
  - **High Bandwidth Memory (HBM)**: Extremely fast memory on-chip.
  - **Interconnect**: Ultra-fast chip-to-chip communication (TPU Pods).
- **Use Cases**:
  - **Training**: Large Neural Networks (BERT, ResNet, TensorFlow/JAX models).
  - **Batch Size**: Performs best with **very large batch sizes**.
  - **Frameworks**: Optimized for TensorFlow and JAX. PyTorch support is available via XLA.
- **Configurations**:
  - **Single Device**: For smaller jobs.
  - **TPU Pod/Slice**: A cluster of TPUs connected via high-speed interconnect. Used for training massive foundation models (like PaLM/Gemini).

## 2. Graphic Processing Units (GPUs)
- **What is it?**: General-purpose accelerator from NVIDIA.
- **Series**:
  - **A3 / A4 / A4X (H100/H200/Blackwell)**: Cutting edge, for massive LLM training.
  - **A2 (A100)**: Previous gen, excellent for training.
  - **L4**: Optimized for **Inference** and Video/Graphics.
  - **T4**: Cost-effective inference and standard ML.
- **Use Cases**:
  - **Custom Ops**: Models with custom C++ CUDA kernels.
  - **Frameworks**: Native support for PyTorch, TensorFlow, etc.
  - **Graphics**: Rendering, VDI, Video Transcoding (L4/T4).

## 3. Comparison (Exam Critical)

| Feature | TPU | GPU |
| :--- | :--- | :--- |
| **Best For** | Massive Matrix Math (Linear Algebra), Large Batch Sizes, Standard NN architectures. | Custom Operations, complex logic loops, smaller batch sizes, Graphics/Rendering. |
| **Framework** | TensorFlow / JAX (Native), PyTorch (XLA). | PyTorch / TensorFlow / CUDA. |
| **Cost** | Generally more cost-effective for pure training throughput on supported models. | More versatile but can be pricier for raw training capability. |
| **Flexibility** | Less flexible (harder to write custom kernels). | Very flexible (CUDA ecosystem). |

---

## 4. Maintenance & Availability
- **Live Migration**:
  - **GPUs**: **NOT Supported**. GPU instances must restart during Host Maintenance.
  - **Notice**: You get a **60-minute** advance notice (Termination Warning) for GPUs (Standard VMs get 60 seconds).
  - **Action**: Use a Shutdown Script to checkpoint your checkpoints to Cloud Storage.
- **TPU Availability**:
  - **Preemptible TPUs**: Cheaper (~70% off), but can be reclaimed at any time. Good for fault-tolerant training jobs (using `tf.distribute` or similar checkpointing).

---

## 5. AI Hypercomputer
- **Marketing Term**: Refers to the integrated stack of:
  - **Compute**: TPUs/GPUs.
  - **Storage**: Cloud Storage FUSE, Parallelstore.
  - **Network**: Jupiter Data Center Network (Titanium).
  - **Software**: Vertex AI, JAX/PyTorch/TensorFlow optimizations.
- **Goal**: To provide supercomputer-level performance for AI training.
