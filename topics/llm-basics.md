# LLM Basics

## TL;DR
Large Language Models (LLMs) are transformer-based models trained on massive text corpora to predict the next token. With good prompting and adaptation, they can perform a wide range of language and reasoning tasks.

## Intuition
- LLMs learn statistical patterns of language and world knowledge from data.
- With instructions and examples, we can "steer" them toward useful behavior.
- They are best used as reasoning + synthesis engines, not exact databases.

## Core Concepts
- Transformers and self-attention (high level).
- Pretraining vs finetuning vs instruction tuning.
- Context window and tokenization.
- Decoding strategies (greedy, sampling, top-k, top-p).

## Simple Example
- Prompt: instruction + optional examples + question.
- Model generates continuation token by token.
- Adjust temperature / top-p to control randomness.

## Gotchas & Common Pitfalls
- Hallucinations / confident but wrong answers.
- Sensitivity to prompt phrasing.
- Context window limits and truncation issues.

## Connections
- Related topics:
  - [[rag]]
  - [[agents-and-tools]]
- Related projects:
  - [[mini-rag-bot]]

## References / Resources
- Paper / blog:
- Notes:
