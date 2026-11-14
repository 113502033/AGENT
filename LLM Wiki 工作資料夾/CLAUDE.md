# AGENTS.md / CLAUDE.md — LLM Wiki 維護手冊與系統規範

> 本檔案為 LLM Agent（如 Antigravity, Claude Code, OpenAI Codex, OpenCode 等）在維護本知識庫時遵循的最高行動規範。
> 本知識庫遵循 **Andrej Karpathy 提出的 LLM Wiki 範式**：將 Wiki 視為隨時間演化、具複利效應（Compounding）的長效知識架構，而非僅作單次無狀態的 RAG 檢索。

---

## 1. 核心哲學 (Core Philosophy)

1. **持久複利架構（Persistent, Compounding Artifact）**：
   - 傳統 RAG 是每次提問時重新檢索片段並從頭推理；本 Wiki 則是每一次攝入新文獻或完成深思後，將精華與洞見編譯成結構化的 Markdown 頁面並長久保存。
   - 知識庫越讀越厚、跨文件連結越結越密、觀點衝突被即時標記、全局綜合視角持續迭代。
2. **人機分工定義（Division of Labor）**：
   - **人類研究員（User）**：掌控資訊輸入來源（Sourcing）、探索方向、提出高價值研究假說與關鍵問題。
   - **Agent（LLM）**：負責全部繁重瑣碎的維護工作（Summarizing、Cross-referencing、Filing、Bookkeeping、Contradiction checking、Linting）。
3. **工作介面隱喻**：
   - **Obsidian 是 IDE**（人類可視化閱讀、瀏覽關聯圖譜 Graph View、點擊跳轉）。
   - **LLM Agent 是工程師**（編寫、重構、索引、除錯與維護 Wiki）。
   - **Wiki 是 Codebase**（結構分明、強型別/標準 Frontmatter、高內聚低耦合的知識程式庫）。
   - **Raw Sources 是唯讀資料庫**（不可篡改的事實來源）。

---

## 2. 目錄階層與分類體系 (Directory Hierarchy & Taxonomy)

```
LLM Wiki 工作目錄
├── raw/                         # 【唯讀原始資料層】客觀事實依歸 (Agent 唯讀)
│   ├── papers/                  # 學術論文 (PDF, Markdown)
│   ├── articles/                # 技術部落格、專欄文章
│   ├── notes/                   # 研究員原始速記、靈感碎片
│   └── assets/                  # 圖片與附件 (Obsidian 剪藏圖片)
├── wiki/                        # 【核心知識資產層】LLM 全權維護與重構
│   ├── concepts/                # 核心理論與機制 (如 test-time-compute.md)
│   ├── models/                  # 模型技術剖析 (如 deepseek-r1.md)
│   ├── architectures/           # 主幹網路架構 (如 transformer.md)
│   ├── methods/                 # 演算法與微調框架 (如 grpo.md, crct-framework.md)
│   ├── agents/                  # 智慧體與協議生態 (如 mcp-protocol.md)
│   ├── evaluations/             # 基準評測集 (如 swe-bench.md)
│   ├── organizations/           # 頂尖實驗室與機構動態
│   ├── comparisons/             # 橫向對比沉澱 (如 reasoning-models-comparison.md)
│   └── syntheses/               # 演化中的全景綜述 (如 llm-research-landscape.md)
├── notes/                       # 【研究產物層】基於 Wiki 推導的專案深度筆記 (100% Wiki 純度)
├── slides/                      # 【簡報展示層】
│   ├── markdown/                # 逐頁內容大綱 (.md)
│   └── html/                    # 自包含互動 HTML 簡報 (.html)
├── templates/                   # 標準頁面模板
├── AGENTS.md / CLAUDE.md        # 系統規範手冊 (即本檔案)
├── index.md                     # 全局目錄索引 (附一句話核心摘要)
└── log.md                       # 只追加（Append-only）演化日誌
```

---

## 3. 三大核心工作流 (Workflows)

### 流程一：文獻攝入（Ingest Workflow）
當使用者將新資料放入 `raw/`（或直接在對話中貼上）並發出處理指令時執行：
1. **保存原始檔案**：若使用者直接貼文字，優先以乾淨 Markdown 完整保存至 `raw/papers/` 或 `raw/articles/`。
2. **深度研讀與精煉**：解析動機、數學機制、實證結論。
3. **連鎖擴散更新（Ripple Updates）**：
   - 一篇新文獻必須主動擴散更新 **3 到 10 個相關頁面**（如新建模型頁、更新訓練演算法頁、補充概念頁）。
4. **觀點演進與矛盾標註（Contradiction Flagging）**：
   - 若新實驗推翻早期論斷，必須在相關頁面使用引號標記：
     > ⚠️ **觀點演進與分歧**：早期文獻認為 ...；然而最新實驗證明 ...
5. **合約實時同步**：同步登錄 `index.md` 與追加 `log.md`。

### 流程二：深度查詢、研究筆記與成果回流（Query & Compound）
當使用者提出專題研究或要求生成 Notes / Slides 時執行：
1. **知識純度守則（Strict Grounding）**：
   - 產出 `notes/` 研究筆記時，**正文必須 100% 依據既有 Wiki 頁面撰寫**，凡引述術語均包裹 `[[wiki/...]]` 內部連結。
2. **外部文獻搜尋隔離**：
   - 外部搜尋到的最新文獻**嚴禁混入筆記正文**，必須統一置於文末「建議參考文獻」中，並附上直鏈下載 PDF、arXiv 頁面與推薦理由。
3. **簡報產物自動化**：
   - 同步產出 `slides/markdown/` 逐頁大綱與 `slides/html/` 現代諮詢卡片風格互動簡報。
4. **成果回流（Filing Back）**：
   - 凡具備深度橫向評比或綜述價值的回答，主動提議沉澱為 `wiki/comparisons/` 或 `wiki/syntheses/`。

### 流程三：健康巡檢（Lint Workflow）
當使用者下達巡檢指令或定期維護時執行：
1. **孤島檢測（Orphan Pages）**：找出無入站連結的頁面並補齊關聯。
2. **斷鏈檢測（Broken Links）**：清理指向不存在檔案的 Wikilinks。
3. **矛盾與陳舊論述（Stale Claims）**：標注已被超越的舊觀點。
4. **缺失實體建議（Missing Entities）**：掃描提及超過 3 次但尚未建頁的技術概念，提議新建。

---

## 4. 格式與元數據規範 (Styling Standards)

### 4.1 YAML Frontmatter
所有 `wiki/` 頁面必須包含標準 Frontmatter：
```markdown
---
title: "頁面繁體中文名稱 (English Title)"
aliases: ["常用簡稱", "英文縮寫"]
type: concept | model | architecture | method | agent | evaluation | organization | comparison | synthesis
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

### 4.2 雙向連結與排版
- 內部連結：`[[wiki/路徑/檔名|顯示名稱]]`。
- 數學公式：KaTeX 相容，行內 `$ ... $`，獨立塊 `$$ ... $$`。
- 術語規範：繁體中文（核心英文詞），例如：上下文條件化（Context Conditioning）、測試時計算（Test-time Compute）。

---

## 5. 檔案命名規範 (Naming Conventions)

1. **Wiki 內部頁面**：全小寫、連字號（kebab-case），如 `test-time-compute.md`、`deepseek-r1.md`。
2. **研究筆記（`notes/`）**：`YYYY-MM-DD-topic-name.md`，如 `2026-11-06-reasoning-paradigm-shift.md`。
3. **簡報檔案（`slides/`）**：`topic-slides.md` 與 `topic-presentation.html`。

---

## 6. AI 協同維護七大鐵律 (Agent Ground Rules)

1. **嚴禁破壞原始文獻**：絕對不改動或刪除 `raw/` 內任何檔案。
2. **筆記內容純度守則**：`notes/` 正文論述 100% 來自 Wiki，不混入外部未收錄資訊。
3. **連鎖擴散更新守則**：攝入新文獻時必須連鎖更新 3~10 個相關頁面，拒絕孤島。
4. **觀點演進主動標註**：新文獻推翻舊主張時，以 `> ⚠️ 觀點演進與分歧` 明確標記。
5. **雙向編織防孤島**：新建頁面必須至少主動連結 2 個既有頁面，且在相關頁面建立反向連結。
6. **核心合約實時同步**：任何異動必須即時同步 `index.md` 與 `log.md`。
7. **研究成果主動回流**：對話與筆記精華主動回流沉澱為長期資產，實現知識複利。
