---
title: "{{模型全名}} 技術剖析 ({{Model Name}} Deep Dive)"
aliases: ["{{常用縮寫}}", "{{模型名稱}}"]
type: model
tags:
  - llm/models
  - research/{{開源或閉源標籤}}
created: {{YYYY-MM-DD}}
updated: {{YYYY-MM-DD}}
status: seed # seed | evolving | mature
sources:
  - "[[raw/papers/{{論文檔名.pdf}}]]"
---

# {{模型全名}} 技術剖析 ({{Model Name}} Deep Dive)

## 1. 模型概覽與開創性貢獻
- **研發機構**：[[wiki/organizations/{{機構名}}|{{機構名}}]]
- **模型規模**：總參數 / 啟動參數 / 上下文長度
- **核心突破**：一至三點最具指標性的技術或實驗創新。

## 2. 模型架構細節 (Architecture Details)
- **基礎結構**：Dense / MoE
- **注意力機制**：MHA / GQA / MLA，搭配之 RoPE 配置
- **激活函數與正規化**：SwiGLU, RMSNorm 等

## 3. 訓練管線與演算法 (Training Pipeline)
- **預訓練數據與策略**：Token 規模、語料配比、退火（Annealing）技巧
- **後訓練與對齊**：採用的微調或強化學習演算法（如 [[wiki/methods/...|...]]）

## 4. 評測基準與關鍵實驗結果 (Evaluations & Benchmarks)
- 在核心基準（如 MMLU, GSM8K, MATH, SWE-bench 等）上的數據對比。

## 5. 關聯維基頁面導航
- **機構背景**：[[wiki/organizations/...|...]]
- **核心架構**：[[wiki/architectures/...|...]]
- **關聯演算法**：[[wiki/methods/...|...]]
- **橫向比較**：[[wiki/comparisons/...|...]]
