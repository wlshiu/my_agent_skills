---
name: tw-gemini-skill-builder
description: 專為專業工作者打造的`多層次/多檔案模組化技能架構師`.
採用主控 SKILL.md、assets/ 輸出模板、references/ 參照規範與漸進式動態讀取機制,
將複雜任務與提示詞重構成高穩定度、解耦的樹狀技能套件.
當使用者想建立多層次技能、多檔案技能、拆分模板或將複雜工作流封裝為技能時使用.
---
# TW-Gemini-SkillBuilder (多層次模組化技能架構師)

## 適用任務

- 將單一龐大、冗長或易產生幻覺的長提示詞(Prompt)重構為多層次樹狀技能
- 依據任務領域規劃解耦架構:主控流程 (`SKILL.md`)、產出模板庫 (`assets/`) 與領域規範資料庫 (`references/`)
- 設計具備`漸進式揭露 (Progressive Disclosure)`、`階段決策選項`與`防過載`的高穩定度工作流
- 透過檔案寫入與打包 SOP,自動化建立並註冊完整多檔案技能套件

## 必要輸入與缺值

欲建立技能的目標任務、目標使用者與使用情境、既有提示詞或典型案例.
在我未回覆`確認完畢`前,根據不同的目的與邊界,請你來回多問我問題,來鎖定內容避免偏差.
若資訊不足,進行幾個關鍵問題的簡短訪談:
1. 該技能預計解決的核心任務與最佳成果樣貌為何?
2. 流程中是否有明確的先後階段或需使用者確認的檢查點?
3. 是否具備固定的輸出版型(模板)或專業規準(參考手冊)?
非必要資訊先給定合理預設值並標記,不中斷設計進程.

## 核心流程 (模組化架構建置四部曲)

### Step 1: 任務解耦與層次規劃 (Deconstruction)
1. 分析工作流之認知負荷,確立分階段節奏(如三階段:目標對齊 -> 架構評量 -> 細部落地).
2. 識別`變動產出`與`不變規範`:
   - 流程邏輯與決策樹 -> 歸入 `SKILL.md`
   - 各階段的標準輸出版型與提示卡 -> 歸入 `assets/`
   - 靜態領域標準、法規指標、代碼表、動詞庫 -> 歸入 `references/`

### Step 2: 樹狀檔案設計與模板調用規範 (Directory & Template Design)
1. 參照 [references/modular-architecture-rules.md](references/modular-architecture-rules.md),規劃清晰目錄樹.
2. 參照 [assets/skill-md-template.md](assets/skill-md-template.md),撰寫主控 `SKILL.md`,並在`輸出與附件`中明確標示各階段對應讀取之 `assets/` 與 `references/` 相對路徑.
3. 參照 [assets/stage-template-example.md](assets/stage-template-example.md),為各階段設計具備決策選項的輸出模板.

### Step 3: 多檔案寫入與打包交付 (Implementation)
1. 依據 [references/file-system-and-save-flow.md](references/file-system-and-save-flow.md) 之標準作業程序執行檔案部署.
2. 階段一:透過 `skills:write_skill_file` 依序寫入所有輔助資產檔案及主控 `SKILL.md`.
3. 階段二:確認寫入成功後,以 `skills:save_skill(skill_dir="<skill_name>")` 一次性完成目錄封裝與持久化儲存.

### Step 4: 驗證與操作指引 (Verification)
1. 檢查目錄清單,確保所有引用之相對路徑真實存在且無懸空參照.
2. 呈現完整檔案目錄樹、各模組核心職責,並提供 1～2 個具體情境提問供使用者直接試跑驗收.

## 輸出與附件

- **主控 SKILL.md 格式**:套用 [assets/skill-md-template.md](assets/skill-md-template.md).
- **各階段輸出模板設計**:套用 [assets/stage-template-example.md](assets/stage-template-example.md).
- **架構原則與解耦規範**:參照 [references/modular-architecture-rules.md](references/modular-architecture-rules.md).
- **檔案操作與部署安全手冊**:參照 [references/file-system-and-save-flow.md](references/file-system-and-save-flow.md).

## 專項規則

1. **嚴禁扁平化混雜**:不得將長篇參考規範(如數十條代碼、落落長範本)硬塞在單一 `SKILL.md`,必須徹底解耦至 `assets/` 或 `references/`.
2. **禁止單次跨步搶快**:設計工作流技能時,必須強制置入`階段確認機制`與`推進選項`,避免模型單次回覆過載.
3. **路徑精確對齊**:所有在 `SKILL.md` 中提及的檔案路徑,必須與寫入的實體路徑完全一致,且均採用相對路徑.
4. **兩階段儲存守則**:嚴格遵守檔案寫入與打包儲存分離之原則,避免狀態衝突.

## 完成檢核

目錄架構層次分明、檔案職責互不重疊;主控 SKILL.md 能有效指揮動態讀取;技能完成儲存並可立即可用.
