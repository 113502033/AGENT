---
title: "群組相對策略優化 (Group Relative Policy Optimization, GRPO)"
aliases: ["GRPO", "Group Relative Policy Optimization"]
type: method
tags:
  - llm/post-training
  - research/reinforcement-learning
  - research/alignment
created: 2026-11-06
updated: 2026-11-06
status: evolving
sources:
  - "DeepSeekMath: Pushing the Limits of Mathematical Reasoning in Open Language Models (Shao et al., 2024)"
  - "DeepSeek-R1 Technical Report (2025)"
---

# 群組相對策略優化 (Group Relative Policy Optimization, GRPO)

## 1. 演算法提出背景與動機

在傳統針對大模型的近端策略優化（PPO）演算法中，系統通常需要載入四個相同或相近規模的模型：
1. **Actor**（當前策略模型）
2. **Critic**（價值評估模型，通常與 Actor 同尺寸以準確估計 Value）
3. **Reference Model**（參考基準模型，計算 KL 散度懲罰）
4. **Reward Model**（獎勵模型）

在訓練 70B+ 等級的超大規模模型時，Critic 網路帶來的顯存開銷與通訊成本極其高昂。
**GRPO (Group Relative Policy Optimization)** 的核心創新在於：**完全取消 Critic 價值網路模型，改由策略模型對同一 Prompt 採樣多個輸出，透過群組內部表現的相對評估來計算優勢（Advantage）。**

---

## 2. 核心數學原理

對於給定的問題 $q$，當前策略模型 $\pi_\theta$ 取樣一組輸出行（Group of outputs）$\{o_1, o_2, \dots, o_G\}$，並透過獎勵函數（如準確率規則、格式約束）計算各輸出的純量得分 $\{r_1, r_2, \dots, r_G\}$。

### 2.1 組內優勢標準化 (Group Relative Advantage)
第 $i$ 個輸出的優勢值 $A_i$ 直接由組內分數正規化計算：

$$A_i = \frac{r_i - \text{mean}(\{r_1, \dots, r_G\})}{\text{std}(\{r_1, \dots, r_G\})}$$

- 若某輸出得分高於同組平均，其優勢值為正，梯度更新將增加其生成機率。
- 若得分低於組內平均，優勢值為負，將降低其生成機率。

### 2.2 目標函數 (Objective Function)
目標函數沿用 PPO 的剪切機制（Clipping）與 KL 散度約束：

$$\mathcal{J}_{GRPO}(\theta) = \mathbb{E}_{\substack{q \sim P(Q) \\ \{o_i\}_{i=1}^G \sim \pi_{\theta_{\text{old}}}(O|q)}} \left[ \frac{1}{G} \sum_{i=1}^G \min \left( \frac{\pi_\theta(o_i|q)}{\pi_{\theta_{\text{old}}}(o_i|q)} A_i, \text{clip}\left(\frac{\pi_\theta(o_i|q)}{\pi_{\theta_{\text{old}}}(o_i|q)}, 1-\epsilon, 1+\epsilon\right) A_i \right) - \beta \mathbb{D}_{KL}(\pi_\theta || \pi_{\text{ref}}) \right]$$

---

## 3. GRPO 的主要優勢與工程價值

1. **極致的顯存節省（Critic-free）**：
   - 省去與策略模型等大的 Critic 網絡，顯存開銷降低約 40% ~ 50%，讓訓練集群能夠把寶貴的顯存讓給更大批次（Batch size）或更長的思維鏈上下文。
2. **原生契合規則獎勵 (Rule-based Rewards)**：
   - 在數學（如 LeetCode、GSM8K、MATH）與程式碼生成等有標準答案或編譯測試的客觀任務中，獎勵信號非常精準，無需仰賴脆弱易被破解（Reward Hacking）的神經網路 Reward Model。
3. **催生測試時計算能力**：
   - 是 [[wiki/models/deepseek-r1|DeepSeek-R1]] 實現無 SFT 冷啟動、純 RL 湧現長思維鏈自省能力（Aha Moment）的關鍵推手。

---

## 4. 關聯維基頁面導航
- **核心實踐模型**：[[wiki/models/deepseek-r1|DeepSeek-R1]]
- **概念理論**：[[wiki/concepts/test-time-compute|測試時計算與推理擴展]]
- **全景梳理**：[[wiki/syntheses/llm-research-landscape|LLM 研究技術全景圖]]
