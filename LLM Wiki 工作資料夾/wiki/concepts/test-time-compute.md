---
title: "測試時計算與推理擴展 (Test-time Compute Scaling)"
aliases: ["Test-time Compute", "Inference Scaling", "推論時計算擴展", "思考鏈擴展"]
type: concept
tags:
  - llm/reasoning
  - llm/inference
  - research/scaling-laws
created: 2026-11-06
updated: 2026-11-06
status: evolving
sources:
  - "OpenAI o1 System Card"
  - "DeepSeek-R1 Technical Report"
---

# 測試時計算與推理擴展 (Test-time Compute Scaling)

## 1. 概念定義與核心動機

在傳統大模型縮放法則（Scaling Laws）中，模型的性能主要由**預訓練計算量**（Pre-training Compute，即參數規模與訓練 Token 數）決定。然而，隨著高品質人類文字資料逐漸枯竭，單純依賴預訓練擴展的邊際效益開始遞減。

**測試時計算（Test-time Compute）** 提出了全新的維度：**在推論（Inference）階段投入額外的計算資源，以換取更高的求解準確率與推理深度。**

```
總體智能水平 ≈ f(預訓練計算量, 後訓練計算量, 測試時計算量)
```

---

## 2. 實現機制與技術路徑

測試時計算的落地主要有以下幾種架構路徑：

### 2.1 隱式長思維鏈 (Long Chain-of-Thought, CoT)
- **代表實踐**：[[wiki/models/deepseek-r1|DeepSeek-R1]]、OpenAI o1 / o3。
- **演進源流**：源自早期提示詞層級的 [[wiki/concepts/chain-of-thought|思維鏈 (Chain-of-Thought)]]，但現代推理模型擺脫了對外部 [[wiki/concepts/prompt-engineering|提示詞工程]] 刻意引導（如「一步步思考」）的依賴，轉由純強化學習讓模型自主湧現思考過程。
- **運作機制**：模型在給出最終答案前，自主輸出數千至上萬 Token 的內部思考鏈（Thinking tokens）。
- **關鍵行為**：在思考過程中自發湧現「提出假設 $\rightarrow$ 自我驗證 $\rightarrow$ 發現錯誤 $\rightarrow$ 反思回溯 $\rightarrow$ 重新構思」的認知閉環。

### 2.2 搜尋與取樣擴展 (Search & Sampling Strategies)
- **Best-of-N 取樣**：並行生成 $N$ 個候選答案，透過過程獎勵模型（Process Reward Model, PRM）評分選出最優解。
- **樹狀搜尋 (MCTS / Tree Search)**：以 Token 或步驟（Step-level）為節點展開搜尋樹，結合價值評估函數動態剪枝。

### 2.3 驗證器引導與自我校正 (Verifier-guided Self-correction)
- 利用外部代碼編譯器（Python REPL）、形式化證明器（Lean 4）或客觀評判器對推論中間步驟進行嚴格檢驗，未通過時觸發重新推導。

---

## 3. 與傳統後訓練的關鍵差異

| 維度 | 傳統 SFT / 對齊 | 測試時計算驅動之推理模型 |
| :--- | :--- | :--- |
| **目標** | 學習標準回答語調與知識格式 | 學習動態探索問題解空間的能力 |
| **推論長度** | 簡明扼要，直奔答案 | 動態伸展思考長度，依難題複雜度調整 Token 消耗 |
| **訓練演算法** | SFT / PPO / DPO | 大規模強化學習（如 [[wiki/methods/grpo|GRPO]]）配合獎勵信號 |
| **主要適用場景** | 聊天、摘要、一般問答 | 競賽級數學、演算法代碼、複雜邏輯與形式化證明 |

---

## 4. 關聯研究與前沿挑戰

- **效率與延遲 (Latency & Cost)**：產生過多 Thinking Tokens 會導致推論延遲顯著增加，需要配合投機解碼（Speculative Decoding）或思考鏈蒸餾技術進行壓縮。
- **過度思考 (Overthinking)**：在簡單問題上可能浪費不必要的計算資源，甚至把原本正確的答案「反思」成錯誤答案。
- **維基內部關聯**：
  - 思維鏈本源：[[wiki/concepts/chain-of-thought|思維鏈技術 (CoT)]] 與 [[wiki/concepts/prompt-engineering|提示詞工程]]
  - 演算法依託：[[wiki/methods/grpo|群組相對策略優化 (GRPO)]]
  - 代表模型實踐：[[wiki/models/deepseek-r1|DeepSeek-R1]]
  - 宏觀地圖：[[wiki/syntheses/llm-research-landscape|LLM 研究技術全景圖]]
