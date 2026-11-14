# LLM Wiki 演化與操作日誌 (Log)

> 本日誌採 Append-only（唯追加）原則記錄。
> 統一前綴格式規範：
> - `## [YYYY-MM-DD] init | <項目描述>`
> - `## [YYYY-MM-DD] ingest | <文獻標題>`
> - `## [YYYY-MM-DD] query | <主題沉澱或查詢評析>`
> - `## [YYYY-MM-DD] lint | <巡檢結果>`
>
> 方便使用 Unix 指令進行分析檢索，例如：`grep "^## \[" log.md | tail -5`

---

## [2026-11-06] init | 初始化 LLM Wiki 知識庫架構
- **操作者**：LLM Agent (Antigravity) 協同使用者
- **完成項目**：
  - 建立繁體中文規範手冊 `AGENTS.md`，定義三層架構、Ingest/Query/Lint 工作流與術語標準。
  - 建立全套分類資料夾：`raw/`（含 papers, articles, notes, assets）、`wiki/`（9 大專業分類）、`templates/`。
  - 建立全局目錄 `index.md` 與事件日誌 `log.md`。
  - 建立 5 篇種子頁面作為網絡起點：
    - `wiki/syntheses/llm-research-landscape.md`（LLM 技術研究全景圖）
    - `wiki/concepts/test-time-compute.md`（測試時計算概念剖析）
    - `wiki/architectures/transformer.md`（Transformer 核心架構）
    - `wiki/methods/grpo.md`（GRPO 強化學習演算法）
    - `wiki/models/deepseek-r1.md`（DeepSeek-R1 推理模型剖析）
- **後續建議**：人類研究員可將感興趣的最新論文或閱讀筆記放入 `raw/papers/` 或 `raw/articles/`，並下達 `Ingest` 指令啟動自動編譯。

## [2026-11-06] ingest | 提示詞工程之結構化設計與最適化策略研究
- **操作者**：LLM Agent (Antigravity)
- **原始來源**：`raw/papers/structural-prompt-engineering.md`
- **新建頁面**：
  - `wiki/concepts/prompt-engineering.md`（提示詞工程與上下文條件化理論、Prompt as Code）
  - `wiki/methods/crct-framework.md`（CRCT 四元組模型與 XML 標籤隔離工程實踐）
  - `wiki/concepts/chain-of-thought.md`（思維鏈 CoT 機制，標注從 Prompt 誘發到 RL 自主湧現的演化分歧）
- **連鎖更新 (Ripple Updates)**：
  - `wiki/concepts/test-time-compute.md`（關聯長思維鏈的提示詞起源與測試時計算差異）
  - `wiki/syntheses/llm-research-landscape.md`（宏觀技術全景新增提示詞工程與上下文條件化支柱）
  - `index.md`（同步更新至 8 篇，追加條目與一句話精要）

## [2026-11-06] query | 大語言模型「推理能力」的典範轉移：從提示詞誘發到測試時計算自主湧現
- **操作者**：LLM Agent (Antigravity) 協同使用者
- **研究產物**：
  - 研究筆記：`notes/2026-11-06-reasoning-paradigm-shift.md`（100% 依據既有 Wiki 撰寫，文末含 4 篇外部 arXiv PDF 直鏈文獻）
  - 逐頁簡報內容：`slides/markdown/reasoning-paradigm-shift-slides.md`
  - 現代諮詢風格 HTML 簡報：`slides/html/reasoning-paradigm-shift-presentation.html`（自包含 Reveal.js + KaTeX 數學引擎，方案 C 卡片設計）

## [2026-11-06] query | LLM Wiki 系統規範與協同維護手冊簡報
- **操作者**：LLM Agent (Antigravity) 協同使用者
- **研究產物**：
  - 系統手冊筆記：`notes/2026-11-06-wiki-system-specifications.md`（完整收錄頁面結構、格式標準、命名放置與 AI 七大鐵律）
  - 逐頁簡報大綱：`slides/markdown/wiki-system-specifications-slides.md`
  - 獨立 HTML 簡報檔：`slides/html/wiki-system-specifications-presentation.html`（方案 C 現代諮詢卡片風格，自包含 Reveal.js + KaTeX）

## [2026-11-14] query | 建立單一檔案 AI 簡報作品集首頁 (index.html)
- **操作者**：LLM Agent (Antigravity) 協同使用者
- **新增產物**：
  - 專案首頁：`index.html`（單一自包含 HTML 檔案，整合深淺色切換、簡報卡片、即時 Modal 預覽、研究管線與知識庫導航）
