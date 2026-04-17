# 齒輪軸承孔工具 (Gear Bearing Hole Tool)

上傳齒輪 SVG → 自動加上中心軸承孔、4 個固定螺絲孔、標籤文字 → 輸出已分好圖層的 SVG,直接在 Illustrator 打開就能編輯。

## 功能

- 🎯 **自動偵測齒輪中心**(也可手動點選覆蓋)
- 🔩 **中心孔 & 固定孔獨立設定**(直徑可相同或不同)
- 📏 **常用軸承規格預設**(623 / 624 / 625 / 626 / 608 / 6800)
- 🏷️ **標籤文字**從檔名自動抓取(例:`secondgearmi130.svg` → `M130`)
- 📄 **輸出 SVG 分好圖層**:`Gear` / `Bearing Hole` / `Mounting Holes` / `Label`
- 🔒 **完全離線運作**,檔案不會上傳到任何伺服器

## 本地使用

直接用瀏覽器打開 `index.html` 即可,不需要任何依賴。

```bash
open index.html
```

## 部署到 GitHub Pages

1. 在 GitHub 建立新的 repo(例如 `gear-tool`)
2. 把這個資料夾裡的檔案推上去:

   ```bash
   cd /Users/anny.li/Desktop/Gear/gear-tool
   git init
   git add .
   git commit -m "Initial commit"
   git branch -M main
   git remote add origin https://github.com/你的帳號/gear-tool.git
   git push -u origin main
   ```

3. 進 GitHub repo → **Settings** → **Pages**
4. Source 選 **Deploy from a branch**,Branch 選 `main` / `/ (root)` → Save
5. 等 1-2 分鐘,網址會是 `https://你的帳號.github.io/gear-tool/`
6. 把這個網址傳給學生即可

## 使用流程

1. **上傳** 齒輪 SVG(拖放或點選)
2. **確認中心**:預設自動偵測 SVG 裡最小的圓當中心;不對可取消「自動偵測」改點預覽圖
3. **設定中心孔**:選預設規格或直接輸入直徑(mm)
4. **設定固定孔**:輸入直徑和距中心距離(若不需要可取消勾選)
5. **設定標籤**:預設從檔名抓,可手動改
6. **下載** SVG,在 Illustrator 打開,圖層面板會看到 4 層分好

## Illustrator 開啟時的圖層

打開下載的 SVG 時,Illustrator 會依據每個 `<g>` 的 `id` 建立對應圖層:

| 圖層名 | 內容 |
|---|---|
| `Gear` | 原始齒輪所有內容(不會動到) |
| `Bearing Hole` | 中心的軸承孔(1 個圓) |
| `Mounting Holes` | 4 個十字排列的固定孔(可設定為 8 個) |
| `Label` | 紅色文字標籤 |

如果圖層沒有正確分開,在 AI 開啟 SVG 時請勾選「轉換為物件」相關選項。

## 常見問題

**Q: 中心偵測跑掉怎麼辦?**
A: 取消勾選「自動偵測中心點」,然後在左邊預覽圖上點一下齒輪中心。

**Q: 想批次處理多個齒輪?**
A: 目前一次一個,如果有需要可以擴充成批次處理(丟一堆檔案進來按一個鍵全部輸出)。

**Q: 軸承孔畫的是外徑還是內徑?**
A: 預設下拉選單列的是**外徑**(孔徑要比軸承外徑大一點才塞得進去,請自行調整);如果要畫軸心(例:Ø3/Ø5 軸心),選擇「軸心」類的預設。

## 技術細節

- 純前端 HTML/CSS/JS,沒有任何外部依賴
- SVG 解析使用 DOMParser,中心點偵測使用 `getCTM()` 處理 transform 串鏈
- 單位依據 SVG 本身的單位(典型齒輪 SVG 使用 mm)
