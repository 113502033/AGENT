# LLM Wiki 全局目錄索引 (Index)

> 本目錄由 LLM Agent 自動維護，匯總知識庫所有精煉頁面與核心要旨。
> 查閱檢索或提出深度問題時，Agent 將優先以此索引作為導航錨點。
>
> **最後更新時間**：2026-11-06  
> **頁面總數**：8 篇

---

## 🧭 核心綜述與研究全景 (Syntheses)
- [[wiki/syntheses/llm-research-landscape|LLM 研究技術全景圖 (Research Landscape)]] — 宏觀梳理大模型從預訓練、後訓練對齊、測試時計算到自主 Agent 的演化脈絡。

## 🧠 核心技術概念 (Concepts)
- [[wiki/concepts/test-time-compute|測試時計算與推理擴展 (Test-time Compute)]] — 探討模型於推論階段投入額外計算資源（思考鏈、MCTS、自省校驗）提升難題求解率之擴展法則。
- [[wiki/concepts/prompt-engineering|提示詞工程與上下文條件化 (Prompt Engineering)]] — 透過上下文條件化引導自迴歸模型收斂語意空間，結合 Prompt as Code 與邊界隔離抑制幻覺。
- [[wiki/concepts/chain-of-thought|思維鏈技術 (Chain-of-Thought, CoT)]] — 透過中間推導步驟將單步複雜運算分攤至序列維度，並串聯提示引導與自主反思之演化脈絡。

## 🏛️ 模型架構與演化 (Architectures)
- [[wiki/architectures/transformer|Transformer 架構基礎與演進 (Transformer Architecture)]] — 自注意力機制、多頭注意力、位置編碼與 Decoder-only 主流架構技術剖析。

## ⚙️ 訓練與微調演算法 (Methods)
- [[wiki/methods/grpo|群組相對策略優化 (GRPO)]] — 擺脫 Critic 價值網路模型，利用組內相對獎勵降低顯存負擔之 RL 訓練法。
- [[wiki/methods/crct-framework|CRCT 結構化 Prompt 設計模型 (CRCT Framework)]] — 將提示詞解構為 Role、Context、Targets、Rules 四元組並配合 XML 標籤隔離之工程化框架。

## 🤖 模型實體與家族 (Models)
- [[wiki/models/deepseek-r1|DeepSeek-R1 推理大模型剖析]] — 開源大規模推理模型，結合純強化學習自我湧現思考鏈與多階段蒸餾技術。

## 🔬 評測基準與指標 (Evaluations)
*（尚無收錄頁面，待攝入文獻後自動建立）*

## 🏢 關鍵研究機構與實驗室 (Organizations)
*（尚無收錄頁面，待攝入文獻後自動建立）*

## ⚖️ 橫向對比與專題評析 (Comparisons)
*（尚無收錄頁面，待深思查詢後沉澱建立）*

## 🌐 智慧體與工具生態 (Agents)
*（尚無收錄頁面，待攝入文獻後自動建立）*
