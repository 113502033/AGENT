---
title: "LLM Wiki 系統規範與協同維護手冊 (LLM Wiki System Specifications)"
date: 2026-11-06
author: "LLM Wiki Agent (Antigravity)"
type: research-note
tags:
  - wiki/system-spec
  - research/framework
  - workflow/standards
status: completed
---

# LLM Wiki 系統規範與協同維護手冊

> **本筆記定位**：系統化彙整本 LLM Wiki 的四大核心支柱：**頁面結構、格式標準、命名與放置階層、AI 協同維護規則**。本規範是確保本知識庫在長時間、多文獻攝入下持續發揮「知識複利效應（Compounding）」而不崩潰失序的最高執行標準。

---

## 1. 頁面結構標準 (Page Structure)

知識庫中的不同檔案承載不同職責，其內部結構嚴格模組化：

### 1.1 Wiki 核心知識頁面 (`wiki/`)
適用於 `concepts/`, `models/`, `architectures/`, `methods/` 等核心資產，遵循 6 模組標準：
1. **YAML Frontmatter**：包含標題、別名、類型、標籤、演化狀態與來源。
2. **核心定義與直覺動機**：1~2 句話直擊核心痛點與理論意義。
3. **深入機制與數學/架構圖解**：以 $\LaTeX$ 數學公式、Mermaid 流程圖深入剖析資料流與演算法。
4. **實務應用與關鍵結論**：在具體大模型中的應用、消融實驗結論與效能取捨。
5. **⚠️ 觀點演進與局限性 / 矛盾分歧**：標註技術邊界、早期假設被推翻的對比。
6. **關聯維基頁面導航**：雙向 Wikilinks 連結至相關概念、架構與模型。

### 1.2 專案研究筆記 (`notes/`)
由特定問題或研究假說觸發的多文檔推導產物：
1. **研究聲明與摘要**：清楚交代核心假說與 Executive Takeaways。
2. **縱深論證章節**：**100% 嚴格源自 Wiki 既有文件**，所有引述均包裹 `[[wiki/...]]` 雙向連結。
3. **多維度橫向對照表**：矩陣式梳理不同技術路線、演算法或模型的優缺點。
4. **前沿挑戰與融合趨勢**：系統工程瓶頸與演進走向。
5. **建議參考文獻**：文末補充之外部前沿文獻，附帶直鏈下載 PDF、arXiv 頁面與推薦理由。

### 1.3 簡報內容架構 (`slides/`)
遵循「單頁單一主題（One Idea Per Slide）」原則：
- 封面 $\rightarrow$ 執行摘要 $\rightarrow$ 核心概念拆解 $\rightarrow$ 數學/架構原理 $\rightarrow$ 瓶頸痛點 $\rightarrow$ 新範式躍遷 $\rightarrow$ 橫向對照表 $\rightarrow$ 前沿挑戰 $\rightarrow$ 外部文獻直鏈下載。

---

## 2. 新增內容時要遵守的格式標準 (Formatting Standards)

### 2.1 標準 YAML Frontmatter
```yaml
---
title: "頁面繁體中文名稱 (English Title)"
aliases: ["常用縮寫", "英文簡稱"]
type: concept | model | architecture | method | agent | evaluation | organization | comparison | synthesis
tags:
  - llm/subtopic
  - research/area
created: 2026-11-06
updated: 2026-11-06
status: seed | evolving | mature
sources:
  - "[[raw/papers/example.md]]"
---
```

### 2.2 雙向連結與排版
- **雙向連結**：`[[wiki/路徑/檔名|顯示名稱]]`，保持 Obsidian Graph View 的連通度。
- **LaTeX 數學公式**：行內公式用 `$ ... $`；獨立公式塊用 `$$ ... $$`。
- **Mermaid 向量圖**：使用 `flowchart LR/TD` 繪製流程與訓練管線；`classDiagram` 呈現模組封裝。
- **術語中英雙標**：繁體中文（核心英文詞），例如：上下文條件化（Context Conditioning）、群組相對策略優化（GRPO）。

---

## 3. 檔案命名與放置體系 (Naming & Placement Hierarchy)

```text
LLM Wiki 工作目錄/
├── raw/                 # 【唯讀原始資料層】immutable，不可篡改的事實來源
│   ├── papers/          # 原始論文（PDF、論文轉 Markdown）
│   ├── articles/        # 技術部落格、專欄文章
│   ├── notes/           # 研究員原始速記、非結構化靈感
│   └── assets/          # 圖表附件
├── wiki/                # 【知識資產層】由 AI 持續維護重構
│   ├── concepts/        # 核心理論與機制
│   ├── models/          # 具體模型技術剖析
│   ├── architectures/   # 網絡骨架與注意力機制
│   ├── methods/         # 訓練演算法與工程框架
│   ├── agents/          # 智慧體與協議生態
│   ├── evaluations/     # 基準評測集與指標
│   ├── organizations/   # 實驗室與機構動態
│   ├── comparisons/     # 橫向對比沉澱
│   └── syntheses/       # 宏觀全景綜述
├── notes/               # 【研究產物層】基於 Wiki 嚴格推導的專案深度筆記
├── slides/              # 【簡報展示層】markdown/ 逐頁大綱與 html/ 獨立網頁簡報
├── templates/           # 【標準模板庫】
├── AGENTS.md            # 最高維護合約手冊
├── index.md             # 全局目錄索引
└── log.md               # 演化時間日誌
```

- **Wiki 內部頁面**：全小寫、連字號（kebab-case），如 `test-time-compute.md`。
- **研究筆記**：日期前綴 + 英文主題，如 `2026-11-06-reasoning-paradigm-shift.md`。
- **簡報產物**：語意對應，如 `topic-slides.md` 與 `topic-presentation.html`。

---

## 4. AI 修改或新增內容時需要遵守的七大鐵律 (Agent Ground Rules)

1. **原始文獻不可篡改性**：嚴禁改動或刪除 `raw/` 內的任何原始檔案。
2. **筆記內容純度溯源**：`notes/` 正文論述必須 100% 來自 `wiki/` 既有內容，外部文獻僅能置於文末建議清單。
3. **連鎖擴散更新守則 (Ripple Update)**：攝入新文獻時，必須主動擴散更新 3~10 個相關 Concept / Model / Synthesis 頁面。
4. **觀點演進與矛盾標註 (Contradiction Flagging)**：新實驗推翻舊結論時，必須以 `> ⚠️ 觀點演進與分歧：...` 明確標記。
5. **雙向編織防孤島 (Anti-Orphan Policy)**：新建頁面必須至少主動連結 2 個既有頁面，並在相關頁面建立反向連結。
6. **雙核心合約同步 (Contract Synchronization)**：任何新增或重大異動，必須同步更新 `index.md`（一句話要旨）與 `log.md`（統一前綴追加）。
7. **研究成果主動回流 (Karpathy Compounding)**：深度問答與筆記中沉澱的高價值橫向對比，主動回流進 `wiki/comparisons/` 或 `wiki/syntheses/`。
