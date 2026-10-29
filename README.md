# 相冊本本

專為 iPhone / iOS Safari 優化的 PWA 相冊紀錄工具。

## 功能

- 拍照／選圖上傳（前端 Canvas 壓縮）
- 3 欄 IG 風格網格
- 分類篩選、新增／改名／刪除分類
- 全螢幕檢視：雙指縮放、雙擊放大、旋轉、編輯、刪除
- 操作列固定在最上層，不會被相片擋住
- Supabase Storage + `notepad_data`（id=`photos`）
- 可加入主畫面全螢幕執行

## GitHub Pages 部署

1. 新建 Repository，上傳本資料夾全部檔案
2. Settings → Pages → Source 選 `main` branch、`/ (root)`
3. 等 1～2 分鐘，開啟 `https://<你的帳號>.github.io/<repo>/`
4. iPhone Safari 開啟網址 → 分享 → **加入主畫面**

## 必要檔案

```
index.html
manifest.webmanifest
sw.js
icon-192.png
icon-512.png
apple-touch-icon.png
```

## Supabase 設定

Project URL 與 Anon Key 已寫在 `index.html`。  
請確認：

1. Storage bucket `photos` 為 Public，並允許 anon upload / read / delete  
2. `notepad_data` 有 id=`photos` 這一列，且 anon 可 SELECT / INSERT / UPDATE  

```sql
INSERT INTO public.notepad_data (id, data)
VALUES (
  'photos',
  '{"photos":[],"categories":["全部","美食","生活","工作","旅行"]}'::jsonb
)
ON CONFLICT (id) DO NOTHING;
```

## 手勢說明（全螢幕檢視）

| 手勢 | 功能 |
|------|------|
| 雙指捏合 | 放大／縮小（1x～5x） |
| 單指拖曳 | 放大後移動畫面 |
| 雙擊 | 在 1x ↔ 2.5x 切換 |
| 旋轉按鈕 | 每次順時針 90° |
| 滾輪（桌面） | 縮放 |

## 授權

自用／隨意修改。
