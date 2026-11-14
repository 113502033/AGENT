---
marp: true
theme: default
paginate: true
header: "LLM Wiki 系統規範與工程指南 | Architecture & Standards"
footer: "Karpathy LLM Wiki 範式 · 現代諮詢模組風格"
---

# LLM Wiki 知識庫系統規範與工程指南
## 頁面結構 · 格式標準 · 命名體系 · AI 協同守則

**報告人**：LLM Wiki 架構助理  
**日期**：2026-11-06  
**規範合約基準**：`[[AGENTS.md]]` · `[[README.md]]` · `[[index.md]]`

---

## 核心理念：打造持久複利的知識程式庫

> 傳統 RAG 是每一次提問從頭檢索的無狀態推理；LLM Wiki 則是隨時間沉澱、越用越厚的長效代碼庫。

### 人機分工的終極平衡
- **Obsidian 是 IDE**：人類研究員視覺化閱讀、瀏覽關聯圖譜、點擊跳轉。
- **LLM Agent 是工程師**：負責繁瑣的編寫、重構、交叉引用、索引與除錯。
- **Wiki 是 Codebase**：高內聚、低耦合、標準化 Frontmatter 的知識資產。
- **Raw Sources 是唯讀資料庫**：不可篡改的事實來源。

---

## 模組化頁面結構標準 (Page Structure)

### 1. Wiki 核心知識頁 (`wiki/`)
- **YAML Frontmatter**：標準元數據與分類標籤
- **核心定義與動機**：1~2 句話直擊理論痛點
- **機制與數學/架構圖解**：$\LaTeX$ 公式與 Mermaid 流程圖
- **實務應用與結論**：主流模型案例與消融實驗
- **⚠️ 觀點演進與局限性**：標註矛盾與邊界條件
- **雙向導航**：連結至 Synthesis 與相關 Model/Concept

### 2. 專案研究筆記 (`notes/`)
- **核心假說** $\rightarrow$ **縱深論證（100% 依據 Wiki）** $\rightarrow$ **橫向矩陣** $\rightarrow$ **建議文獻（直鏈下載）**

---

## 標準元數據與 Frontmatter 規範

```yaml
---
title: "頁面繁體中文名稱 (English Title)"
aliases: ["常用簡稱", "英文縮寫"]
type: concept | model | architecture | method | comparison | synthesis
tags:
  - llm/reasoning
  - research/scaling-laws
created: 2026-11-06
updated: 2026-11-06
status: seed | evolving | mature
sources:
  - "[[raw/papers/deepseek-r1.md]]"
---
```

### 演化狀態的三大生命週期
- `seed`（種子草稿）：初始建立，僅包含核心定義與初步關係。
- `evolving`（持續演化）：經歷多次 Ingest 與連鎖擴散，網絡逐步緊密。
- `mature`（成熟體系）：理論完備、實驗數據齊全且經過健康巡檢驗證。

---

## 雙向連結與排版格式規範

### 1. Obsidian 雙向連結（Wikilinks）
- 格式：`[[wiki/路徑/檔名|顯示文字]]`
- 目的：點亮 Obsidian Graph View，形成星系般的關聯網絡。

### 2. 數學公式與圖表規範
- **$\LaTeX$ 數學公式**：行內 `$ ... $`、塊狀 `$$ ... $$`（如注意力機制、GRPO 公式）。
- **Mermaid 向量圖**：`flowchart LR/TD` 呈現資料流；`classDiagram` 呈現模組封裝。

### 3. 術語中英雙標原則
- 繁體中文（核心英文詞），例如：
  - *Context Conditioning* $\rightarrow$ 上下文條件化
  - *Test-time Compute* $\rightarrow$ 測試時計算

---

## 目錄放置體系與職責邊界 (Hierarchy)

| 資料夾路徑 | 職責定義 | 讀寫權限 | 範例內容 |
| :--- | :--- | :--- | :--- |
| **`raw/`** | 唯讀事實來源 (Immutable) | **Agent 唯讀** | 論文 PDF、剪藏文章、個人手記、圖片 |
| **`wiki/`** | 核心知識資產庫 | **Agent 全權維護** | concepts, models, methods, architectures |
| **`notes/`** | 專案深度研究筆記 | **Agent 生成** | 100% 依據 Wiki 推導之深度報告 |
| **`slides/`** | 簡報產物（MD / HTML） | **Agent 生成** | 演講投影片、獨立網頁簡報 |
| **根目錄** | 合約與導航中樞 | **人機共同維護** | `AGENTS.md`, `index.md`, `log.md` |

---

## 檔案命名規範體系 (Naming Conventions)

### 1. Wiki 內部知識頁面
- **全小寫、連字號（kebab-case）**，以核心英文術語命名。
- 範例：`test-time-compute.md`、`deepseek-r1.md`、`crct-framework.md`。

### 2. 研究筆記檔案 (`notes/`)
- **日期前綴 + 英文主題**，清晰呈現知識演化時間戳。
- 範例：`2026-11-06-reasoning-paradigm-shift.md`。

### 3. 簡報展示檔案 (`slides/`)
- 與主題精準對應，區隔大綱與網頁產物：
  - `slides/markdown/topic-slides.md`
  - `slides/html/topic-presentation.html`

---

## AI 協同維護鐵律（上）：知識純度與連鎖更新

### 鐵律 1：原始資料不可篡改性 (Immutability)
- Agent 絕對不修改、刪除 `raw/` 內任何原始檔案，確保事實來源永不失真。

### 鐵律 2：研究筆記知識純度守則 (Strict Grounding)
- 產出 `notes/` 時，正文內容必須 **100% 源自 Wiki 既有頁面**，並附帶 `[[wiki/...]]` 內部連結。外部資訊僅能列於文末建議文獻中。

### 鐵律 3：連鎖擴散更新原則 (Ripple Update Rule)
- 攝入一篇新文獻，**必須動態擴散更新 3~10 個相關頁面**（概念、模型、架構、全景圖），嚴禁孤立建檔。

---

## AI 協同維護鐵律（下）：矛盾標註與成果回流

### 鐵律 4：觀點演進與矛盾主動標註 (Contradiction Flagging)
- 若新實驗推翻舊觀點，必須使用 `> ⚠️ 觀點演進與分歧：...` 明確標記，記錄認知演化歷史。

### 鐵律 5：雙向編織防孤島 (Anti-Orphan Policy)
- 新建頁面必須至少主動連結 2 個既有頁面，且在相關頁面建立反向連結。

### 鐵律 6：雙合約實時同步 (Contract Synchronization)
- 任何異動必須即時同步 **`index.md`（一句話要旨）** 與 **`log.md`（統一前綴日誌）**。

### 鐵律 7：研究成果主動回流 (Karpathy Compounding)
- 高品質的對話與筆記橫向分析，主動沉澱回 `wiki/comparisons/` 或 `wiki/syntheses/`。

---

## 總結：人機共生的人工智慧研究工作流

```
[人類研究員] ──> 收集優質文獻至 raw/ ──> 下達 Ingest 指令
                        │
                        ▼
[LLM Agent]  ──> 連鎖編譯至 wiki/ ──> 維護雙向連結與索引
                        │
                        ▼
[人機協同]   ──> 提出高價值研究問題 ──> 生成 100% Wiki 純度之 Notes 與 Slides
                        │
                        ▼
[成果回流]   ──> 沉澱橫向綜述回 Wiki ──> 實現知識複利（Compounding）
```

**歡迎點擊文末直鏈開啟 HTML 簡報進行全螢幕放映！**
