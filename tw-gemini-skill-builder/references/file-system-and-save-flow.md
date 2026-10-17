# 實體檔案操作與打包儲存標準作業程序 (Save Workflow SOP)

在 Gemini 技能架構中建立多檔案技能時,必須嚴格遵守以下兩階段作業流程:

---

## 一、兩階段儲存原則 (Two-Step Save Principle)

### 階段一:寫入所有檔案 (Write Phase)
- 使用 `skills:write_skill_file` 建立所有檔案.
- 每個檔案呼叫一次 `skills:write_skill_file(skill_name="...", path="...", content="...")`.
- **絕對嚴禁**:在呼叫 `write_skill_file` 的同一次回應中呼叫 `skills:save_skill`!這會造成暫存區狀態競態與打包失敗.

### 階段二:打包並持久化註冊 (Package & Save Phase)
- 等待所有檔案寫入成功的回應後,在獨立的回應中呼叫:
  `skills:save_skill(skill_dir="<skill_name>")`
- **參數規定**:當使用目錄打包時,**只能提供 `skill_dir`**,不可同時傳入 `content`.

---

## 二、檔案操作防錯清單

1. **路徑一致性**:
   - 程式碼內部寫入之路徑（如 `assets/stage1-template.md`）必須與 `SKILL.md` 中引用的相對路徑 100% 吻合,大小寫與橫線須嚴格一致.
2. **命名規範**:
   - 技能名稱必須符合:小寫英文、數字、連字號 (`kebab-case`),長度不大於 64 字元.
   - 目錄名稱必須與技能名稱完全一致.
3. **覆蓋與存在衝突處理**:
   - 若 `save_skill` 回傳 `already_exists`,需先向使用者確認是否更新;若要更新現有技能,使用更新流程或請使用者確認覆蓋.
