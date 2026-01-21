# A^3: Attention-Aware Accurate KV Cache Fusion for Fast \\ Large Language Model Serving


## Table of Contents

- [Introduction](#introduction)
- [Installation](#installation)
- [Usage](#usage)

## Introduction
Large language models (LLMs) have demonstrated strong capabilities in processing long contexts, enabling them to tackle tasks involving long textual inputs such as multi-turn conversations, legal documents, or retrieved documents in Retrieval-Augmented Generation (RAG) systems. 
However, despite their ability to handle long sequences, the resulting decoding latency and memory overhead remain substantial, posing challenges for real-world deployment.
Recent advances in KV Cache reuse have shown potential to mitigate these costs, but still suffer from notable performance degradation. To address this issue, we conduct an in-depth investigation of recomputation-based reuse methods and observe that the recomputed tokens often fail to align with the context segments most relevant to the question. This misalignment hinders proper updates to the critical contextual representations. 
Therefore, we propose the \textbf{A}ttention-\textbf{A}ware \textbf{A}ccurate KV Cache Fusion algorithm ($A^3$), which precomputes and selectively fuses the KV Cache of text chunks based on their relevance to the question, achieving accurate integration with minimal computational overhead.
Extensive experiments on various benchmarks and LLMs demonstrate that $A^3$ achieves the best task performance compared to four baselines while reducing the time-to-first-token (TTFT) by 2×.

## Installation

1. Create a Conda environment using the YAML file:

    ```bash
    pip install -r requirements.txt
    ```

## Usage

```bash
cd a3kv

# step 1 - chunk long contexts
python ./chunk_longbench.py
python ./chunk_needle.py
python ./chunk_ruler.py

# step 2 - precompute
bash ./scripts/precompute.sh

# step 3 - evaluate
# for longbench
bash ./scripts/eval_longbench.sh

# for needle
bash ./scripts/eval_needle.sh
python ./visualize.py

# for ruler
bash ./scripts/eval_ruler.sh
python .scripts/copy_results_ruler.py

## Paper
https://arxiv.org/abs/2511.17560
