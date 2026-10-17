# 多層次技能解耦原則與架構規範 (Modular Architecture Rules)

## 一、為什麼需要多層次解耦架構?

傳統`單一巨型提示詞 (Monolithic Prompt)`常見三大致命傷:
1. **Context Window 暴增與漂移**:一次性注入數萬字的標準代碼、範本與規則,容易稀釋注意力,導致模型遺忘核心限制.
2. **輸出過載 (Cognitive Overload)**:模型急於一次回答全部內容,產出過度冗長、粗糙或缺乏深度的半成品.
3. **維護與重構困難**:當需要更新某個表格樣式或課綱指標時,需在萬字長文裡尋找,極易破壞其他指令.

多層次解耦架構將技能劃分為三層職責:
- **Orchestration Layer (主控排程層 - `SKILL.md`)**:掌管流程順序、狀態跳轉、輸入驗證與防護規則.保持輕量(建議 150 行以內).
- **Presentation / Asset Layer (表現與模板層 - `assets/`)**:掌管各階段輸出該長成什麼樣子、包含哪些結構化欄位與決策選項.
- **Domain Knowledge Layer (領域知識層 - `references/`)**:掌管法規、指標清單、術語字典、評量規準等靜態不變之核心依據.

---

## 二、標準目錄樹 (Standard File Tree)

```text
[skill-name]/
├── SKILL.md                          # [必備] 主控流程與觸發核心
├── assets/                           # [表現層] 產出模板與成果骨架
│   ├── stage1-xxx-template.md        # 階段一輸出模板
│   ├── stage2-xxx-template.md        # 階段二輸出模板
│   └── stage3-xxx-template.md        # 階段三輸出模板
└── references/                       # [知識層] 領域手冊與法規參照
    ├── domain-standards-guide.md     # 核心標準/法規/指標表
    └── best-practices.md             # 最佳實踐與避坑指引
```

---

## 三、漸進式揭露 (Progressive Disclosure) 設計心法

1. **三階段黃金節奏**:
   - **Stage 1 (目標與輸入對齊)**:確認核心意圖、利害關係人、成功判准.
   - **Stage 2 (架構與關鍵機制)**:搭建骨架、驗證核心模型、設定檢核點.
   - **Stage 3 (細部落地與深層鷹架)**:時間流、逐字話術、具體產出與邊界例外處遇.
2. **決策按鈕化 (Elicitation Prompts)**:
   - 永遠不要以開放式`您覺得如何?`作結.
   - 每階段結尾提供 **2 個具體分歧選項 + 1 個預設推進選項**,讓使用者按一下或回 1 個字就能推進.
