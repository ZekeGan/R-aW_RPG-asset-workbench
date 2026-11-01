# 0.5.8 文件去重與版控設定 — 2026-11-01

- 刪除 `docs/handoff-2026-10-23/reference/` 內與正本逐 byte 相同的副本（Mockup 五張 PNG、DESIGN_INDEX、SPEC_REVIEW、TECHNICAL_BASELINE、UPDATE_0.4.0），MOCKUP_MAP 連結改指向 `spec-v1.0.0/design/mockups/`；說明見該資料夾 README。
- `.gitignore` 加入 `docs/evidence/**/*.png`，避免 Electron smoke 重跑把截圖再次納入版本控制；刪除本機舊 log（本來即被忽略）。
- 新增 `.gitattributes`（`text=auto`，圖片為 binary）統一換行。
- 修正 `DEVELOPMENT_0.5.md` 中已刪截圖的檔名。
- 沒有程式變更，未重跑測試。
