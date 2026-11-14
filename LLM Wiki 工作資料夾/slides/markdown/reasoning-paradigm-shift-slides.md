---
marp: true
theme: default
paginate: true
header: "LLM 推理能力的典範轉移 | LLM Wiki Research"
footer: "基於 LLM Wiki 知識庫 · 現代諮詢模組風格"
---

# 大語言模型「推理能力」的典範轉移
## 從提示詞誘發到測試時計算自主湧現

**報告人**：LLM Wiki 研究助理  
**日期**：2026-11-06  
**研究維基錨點**：`[[wiki/syntheses/llm-research-landscape]]` · `[[wiki/concepts/test-time-compute]]`

---

## 執行摘要：兩代推理範式的本質躍遷

> 大語言模型在處理複雜邏輯運算與多步驟推理時，已完成從「外部格式約束」到「內部認知搜尋」的重大變革。

### 兩代範式核心速覽
- **第一代：提示詞誘發 (Prompt-Driven)**
  - 核心機制：透過上下文條件化（Context Conditioning）與「一步步思考」提示詞。
  - 本質特徵：**格式模仿與自迴歸概率收斂**，推理容量受限於固定層數前向傳遞。
- **第二代：測試時計算自主湧現 (Emergent Test-time Compute)**
  - 核心機制：純強化學習（如 GRPO）驅動數萬 Token 的長思維鏈。
  - 本質特徵：**探索、試錯、回溯與自檢**，自發湧現啟發式認知閉環（Aha Moment）。

---

## 第一代範式：提示詞工程與上下文條件化

```
P(w_t | w_1, w_2, ..., w_{t-1})
```

### 1. 機率空間收斂機制
- 自迴歸模型預設處於高自由度的通用語意空間中，極易引發隨機幻覺。
- 提示詞工程的理論本質為 **上下文條件化（Context Conditioning）**。

### 2. CRCT 四元組模組化架構
- **Role (角色)**：限制詞彙選擇，將分佈收斂至專家語意空間。
- **Context (情境)**：提供具體業務細節，錨定真實場景。
- **Targets (目標)**：明確定義核心產出物清單。
- **Rules (約束)**：修剪潛在的不良生成路徑（負面限制與格式邊界）。

---

## 初代思維鏈 (CoT) 的本質：計算負擔之序列攤提

$$\text{Attention}(Q, K, V) = \text{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right)V$$

### 為什麼直接回答容易產生邏輯跳躍？
- 在標準 Transformer Decoder 中，每一層的自注意力計算開銷是固定不可變的。
- 若要求模型在單步 Token 內輸出最終答案，計算容量被固定層數嚴格卡死。

### 思維鏈的解題智慧
- **將複雜計算分攤至時間序列維度**：
  Zero-shot / Few-shot CoT 引導模型生成中間步驟，使後續 Token 能依賴前序推導作為注意力鍵值，大幅提升運算準確率。

---

## 提示詞誘發推理的三大核心瓶頸

```
[問題輸入] ──> [提示詞引導] ──> [單向自迴歸生成] ──> [中間出錯無法回溯] ──> [產生邏輯幻覺]
```

1. **單向不可逆性 (Irreversibility)**
   - 自迴歸解碼一旦在前序產出錯誤 Token，後續注意力將以此錯誤為前提推演，模型無法自行「撤銷」。
2. **缺乏客觀驗證閉環 (No Verification)**
   - 提示詞僅能引導模型「模仿人類思考的語氣格式」，並未賦予模型客觀的自我驗證能力。
3. **固定推論預算 (Static Compute Budget)**
   - 無論面臨簡單問題或競賽級奧數，靜態提示詞無法動態提供深度的思考算力空間。

---

## 第二代範式：測試時計算擴展 (Test-time Compute)

$$\text{總體智能水平} \approx f(\text{預訓練計算量}, \text{後訓練計算量}, \text{測試時計算量})$$

### 突破預訓練擴展邊際效益遞減
- 傳統 Scaling Laws 單純依賴參數量與訓練 Token 數。
- 測試時計算開闢第三維度：**在推論（Inference）階段投入額外計算資源，換取極致的推理深度。**

### 三大落地技術路徑
- **隱式長思維鏈 (Long CoT)**：自主產出數千至上萬 Token 內部思考。
- **搜尋與取樣擴展**：Best-of-N 取樣與 PRM 過程驗證引導。
- **動態自適應配置**：依題目難度動態調整思考 Token 消耗量。

---

## 演算法核心：群組相對策略優化 (GRPO)

$$A_i = \frac{r_i - \text{mean}(\{r_1, \dots, r_G\})}{\text{std}(\{r_1, \dots, r_G\})}$$

### 1. 擺脫 Critic 價值網路 (Critic-Free)
- 傳統 PPO 需維護等大尺寸的 Critic 模型，顯存開銷巨大。
- GRPO 完全取消 Critic，直接在同一個 Prompt 取樣一組輸出進行內部相對優勢歸一化，**顯存節省約 40% ~ 50%**。

### 2. 客觀規則獎勵 (Rule-Based Rewards)
- 在數學與代碼任務中，以準確率規則（正則判定、編譯器測試）作為獎勵信號 $r_i$。
- 徹底避免了神經網路 Reward Model 容易被破解（Reward Hacking）的缺陷。

---

## 頓悟現象 (Aha Moment) 與認知自省湧現

> *"...Wait, wait. Wait. That's an error. Let me recalculate that..."*  
> —— DeepSeek-R1-Zero 思考軌跡真實紀錄

### 自發湧現的三大高階認知特徵
1. **自主反思與檢驗 (Self-Verification)**
   - 模型在沒有任何人類標註指導下，學會回頭審查上一公式，發現矛盾即刻暫停並重算。
2. **探索與回溯 (Exploration & Backtracking)**
   - 遭遇邏輯死胡同時，主動推翻前序假設，開闢全新推演分支。
3. **動態思考鏈伸展**
   - 根據問題求解難度，自動在 `<think>...</think>` 中展開深層搜索。

---

## 兩代推理範式全方位對照總表

| 評估維度 | 第一代：提示詞誘發 (Prompt-Driven) | 第二代：測試時計算自主湧現 (Test-time Compute) |
| :--- | :--- | :--- |
| **驅動來源** | 外部指示詞、Few-shot 範例 | 內部純強化學習（GRPO）+ 規則獎勵 |
| **思考本質** | 表面格式模仿 (Surface Mimicry) | 探索、試錯、回溯之認知搜尋 (Cognitive Search) |
| **推論長度** | 相對靜態，數百至一千 Token | 自主拉伸，動輒上萬 Token |
| **錯誤自省** | 幾無自省能力，容易將錯就錯 | 具備強大自我反思與重算能力 (Aha Moment) |
| **計算代價** | 首字延遲低，顯存負擔輕 | KV 快取顯存開銷劇增，首字延遲顯著拉長 |
| **代表實體** | Zero-Shot CoT、CRCT 提示詞框架 | DeepSeek-R1、OpenAI o1 / o3 |

---

## 未來融合與硬體工程挑戰

### 1. 兩大範式之深度融合
- 具備強大測試時計算能力的模型，仍需依託 **CRCT 架構** 進行精準的角色定義與邊界規範，避免任務目標偏移。

### 2. 前沿工程架構挑戰
- **KV 快取顯存爆炸**：超長思考鏈考驗顯存帶寬，催生 MLA（多頭潛在注意力）架構需求。
- **過度思考 (Overthinking)**：需建立動態早停機制，避免在簡單問題上空耗算力。
- **能力蒸餾普及**：將 R1 類別的長思考推理能力蒸餾至 1.5B ~ 70B 開源小模型。

---

## 延伸閱讀與 Wiki 擴充文獻（直接點擊下載）

1. **[📄 下載 DeepSeek-R1 論文 PDF](https://arxiv.org/pdf/2501.12948.pdf)**  
   *DeepSeek-AI (2025)* — 純 RL 自主湧現長思維鏈與 GRPO 演算法奠基作。
2. **[📄 下載 Scaling Test-Time Compute 論文 PDF](https://arxiv.org/pdf/2408.03314.pdf)**  
   *UC Berkeley & Google DeepMind (2024)* — 測試時計算擴展法則理論證明。
3. **[📄 下載 Chain-of-Thought Prompting 論文 PDF](https://arxiv.org/pdf/2201.11903.pdf)**  
   *Google Research (2022)* — 思維鏈提示開山之作。
4. **[📄 下載 Let's Verify Step by Step 論文 PDF](https://arxiv.org/pdf/2305.20050.pdf)**  
   *OpenAI (2023)* — 單步過程獎勵模型 (PRM) 評估思維鏈。
