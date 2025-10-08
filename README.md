# BlockRank: Scalable In-context Ranking with Generative Models

[![Paper](https://img.shields.io/badge/Paper-arXiv-b31b1b.svg)](https://arxiv.org/abs/2510.05396)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Status](https://img.shields.io/badge/Code-Coming%20Soon-orange.svg)](#code-coming-soon)

---

### Overview

Large Language Models (LLMs) are rapidly becoming the fundamental unit of computation — powering reasoning, generation, and increasingly, *retrieval*.  While modern Information Retrieval (IR) systems already leverage LLMs for contextual ranking, they often treat them as *black boxes*, relying on general intelligence but ignoring structural efficiency.

This work introduces BlockRank, a method designed to make LLMs efficient and scalable for in-context ranking by aligning their internal attention and inference mechanisms with the structure of the in-context ranking task.

---

### What is BlockRank?

**BlockRank (Blockwise In-context Ranking)** is a specialized architecture and fine-tuning approach for scalable in-context retrieval and ranking. It’s built on two key insights about LLMs fine-tuned for ranking tasks:

1. **Inter-document block sparsity**
  → Attention is dense within each document but sparse across documents — meaning full quadratic attention is unnecessary.

2. **Query-token retrieval signals**
  → Certain query tokens (e.g., delimiters) encode strong relevance signals in their attention patterns during the prefill stage.

### Method Summary

Based on these observations, BlockRank modifies both the architecture and training of an LLM:

- **Structured Sparse Attention**  
  Enforces attention only within document blocks and to shared instruction tokens, cutting complexity from *quadratic → linear*.

- **Auxiliary Contrastive Attention Loss**  
  Adds a mid-layer contrastive objective to directly optimize query–document attention, improving both relevance and interpretability.

- **Attention-based Inference**  
  Uses attention maps (from the prefill stage) to compute document relevance scores directly — eliminating the need for auto-regressive decoding.

<p align="center">
  <img src="assets/blockrank_diagram.png" alt="BlockRank Architecture Overview" width="700"/>
  <br/>
  <em>Figure: BlockRank imposes blockwise sparse attention and leverages query-token attention signals for efficient in-context ranking.</em>
</p>

---

### Results Summary

- Strong zero-shot generalization on BEIR, matches or outperforms state-of-the-art listwise rankers (e.g., RankZephyr, FIRST)
- 4.7× faster inference on MSMarco (100 documents) compared to standard decoding based implementation
- Scales linearly with in-context documents
- Works with existing open LLMs (e.g., Mistral, Llama)  

---

## Code for Reproduction

Stay tuned — full training and inference code will be available here soon.
- [ ] Kernelized Blockwise Attention Implementation
- [ ] Fine-tuning scripts for Mistral-7B
- [ ] Evaluation pipelines for BEIR, MSMarco, and NQ

## Citation

If you find this work useful, please cite:

```bibtex
@article{gupta2025blockrank,
  title={Scalable In-context Ranking with Generative Models},
  author={Gupta, Nilesh and You, Chong and Bhojanapalli, Srinadh and Kumar, Sanjiv and Dhillon, Inderjit and Yu, Felix},
  journal={arXiv preprint arXiv:2510.05396},
  year={2025}
}
```
