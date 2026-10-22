# 本機 PDF 工作台

一個打開瀏覽器就能用的 PDF 工具箱。檔案只在使用者自己的瀏覽器裡處理，**不會上傳到任何伺服器**。

最常用的功能是把多頁 PDF 拆成一頁一個檔案：把 PDF 拖到首頁的拖放區，就會自動開啟「拆分 PDF」，預設每一頁存成獨立的 PDF，可以一次打包成 ZIP 下載。

## 功能

| 分類 | 工具 | 說明 |
|---|---|---|
| 整理頁面 | 合併 PDF | 依排好的順序把多個 PDF 合成一份 |
| | 拆分 PDF | 每頁一檔、依頁碼範圍、每 N 頁，或挑選頁面合成新檔 |
| | 旋轉 PDF | 整份或單頁轉 90°，可一次處理多個檔案 |
| | 裁剪 PDF | 框出要保留的範圍，套用到單頁或整份 |
| 縮小與比對 | 壓縮 PDF | 無損整理，或轉成影像大幅縮小（輕度／建議／強力） |
| | 比較 PDF | 文字逐行比對，或用影像疊圖找出版面變動 |
| 從 PDF 轉出 | PDF 轉 Word | 擷取段落與標題，輸出 .docx |
| | PDF 轉 PowerPoint | 每頁一張投影片，可選頁面圖片或可編輯文字方塊 |
| | PDF 轉 Excel | 依文字位置還原表格欄位，輸出 .xlsx |
| | PDF 轉 JPG | 每頁轉成 JPG／PNG，或擷取 PDF 內嵌的圖片 |
| | PDF 轉 Markdown | 保留標題、條列、表格與連結 |
| 編輯與簽署 | 編輯 PDF | 加文字、方框、螢光筆、手寫、圖片，或用白框遮蓋內容 |
| | PDF 簽名 | 手寫、打字或上傳簽名圖，放到頁面任何位置 |
| | 添加浮水印 | 文字或圖片浮水印，可調透明度、角度、位置、平鋪 |
| | PDF 表單 | 填寫既有欄位，或新增文字欄與勾選框 |
| 安全與保密 | PDF 解鎖 | 輸入密碼移除開啟密碼與權限限制 |
| | PDF 加密 | 設定開啟密碼，限制列印、複製、修改 |
| | PDF 標記密文 | 永久塗黑敏感內容，可自動偵測身分證字號、手機號碼、Email |
| 自動化 | 建立工作流程 | 把多個步驟串成流程，批次套用到多個檔案並儲存重複使用 |

每個工具都有「用範例檔試試」按鈕，不必用自己的檔案也能先測試。

> 在 Claude 裡開啟時另有「AI 摘要產生器」與「PDF 翻譯」；網站版會自動隱藏這兩項。

## 檔案

| 檔案 | 用途 |
|---|---|
| `index.html` | 工具頁面本身 |
| `pdfdata.js` | 中文、日文、韓文 PDF 需要的字元對照表與標準字型資料 |
| `README.md` | 本說明 |

`index.html` 和 `pdfdata.js` **必須放在同一個資料夾**。少了 `pdfdata.js`，部分沒有內嵌字型的中文 PDF 會顯示成空白或亂碼。

## 發布到 GitHub Pages

1. 在 GitHub 建立一個 **Public** repository，例如 `pdf-tools`。
2. 上傳 `index.html`、`pdfdata.js`、`README.md`。
3. 到 **Settings → Pages**，Source 選「Deploy from a branch」，Branch 選 `main`、資料夾選 `/ (root)`，按 Save。
4. 等 1～2 分鐘，網址會是 `https://你的帳號.github.io/pdf-tools/`。

## 嵌入 Google 協作平台

1. 在協作平台的頁面選 **插入 → 嵌入 → 依網址**，貼上 GitHub Pages 網址，選「整個頁面」。
2. 把嵌入框拉大（建議寬度拉滿、高度 900 以上）。
3. 建議另外 **插入 → 按鈕**，名稱「在新分頁開啟 PDF 工具」，連到同一個網址。
   協作平台的嵌入框限制較多，部分瀏覽器會擋下框內的下載；按「儲存」沒有反應時，從新分頁開啟就能正常下載。
4. 按「發布」。

## 使用須知

- 第一次開啟需要連網，會從 `cdn.jsdelivr.net` 載入 PDF 處理元件。學校網路若封鎖這個網域，頁面會顯示「PDF 元件沒有載入成功」，需請網管開放。
- 壓縮（輕度／建議／強力）、標記密文，以及少數特殊加密檔的解鎖，會把頁面重新存成影像，處理後文字無法選取或搜尋。
- 轉 Word／PowerPoint／Excel 是依文字位置還原內容。單欄文件與簡單表格效果最好；多欄排版較粗略；掃描檔沒有文字層，轉 Word 時會改放頁面圖片。
- PDF 簽名是把簽名以影像蓋在頁面上，不是具法律效力的數位憑證簽章。
- 建立工作流程時，流程會存在使用者自己的瀏覽器裡；為了安全，密碼不會被儲存。
- 請只解鎖自己有權使用的檔案。

## 隱私

所有處理都在瀏覽器內完成。PDF 不會傳到 GitHub、Google 或任何第三方；關閉分頁後，檔案就不會留在任何地方。

## 使用的開源元件

| 元件 | 版本 | 用途 | 授權 |
|---|---|---|---|
| [PDF.js](https://github.com/mozilla/pdf.js) | 3.11.174 | 讀取與繪製 PDF、擷取文字 | Apache-2.0 |
| [@cantoo/pdf-lib](https://github.com/cantoo-scribe/pdf-lib) | 2.3.2 | 建立與修改 PDF、加密與解密 | MIT |
| [JSZip](https://github.com/Stuk/jszip) | 3.10.1 | 打包 ZIP | MIT / GPLv3 |
| [PptxGenJS](https://github.com/gitbrent/PptxGenJS) | 3.12.0 | 產生 PowerPoint | MIT |
| [SheetJS](https://github.com/SheetJS/sheetjs) | 0.18.5 | 產生 Excel | Apache-2.0 |
| [docx](https://github.com/dolanmiu/docx) | 8.5.0 | 產生 Word | MIT |

`pdfdata.js` 內含 PDF.js 隨附的 CMap 與標準字型資料，依其原始授權（Adobe CMap、Foxit、Liberation 字型授權）散布。

字型：Noto Sans TC、JetBrains Mono、LXGW WenKai TC、Great Vibes，經 Google Fonts 載入（SIL Open Font License）。
