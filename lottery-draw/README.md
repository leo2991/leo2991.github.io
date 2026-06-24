# 抽獎頁範本

這個頁面會從 GitHub 上固定的 Excel 檔讀取抽獎名單，使用者只需要輸入獎品名稱和抽取人數。

## Excel 名單格式

請把名單放在 Excel 第一個工作表，至少需要一欄姓名。建議欄位：

| 姓名 | 部門 | Email |
| --- | --- | --- |
| 王小明 | 產品部 | ming@example.com |
| 陳怡君 | 設計部 | yi@example.com |

支援的姓名欄位名稱包含：`姓名`、`名字`、`Name`、`name`、`中文姓名`、`參加者`、`員工姓名`。

## 設定固定 Excel 檔

1. 將 Excel 檔上傳到 GitHub repository，例如 `data/participants.xlsx`。
2. 開啟檔案頁面，按 `Raw`，複製 raw URL。
3. 在 `lottery-draw/index.html` 中找到：

```js
const CONFIG = {
  rosterUrl: "",
};
```

4. 改成：

```js
const CONFIG = {
  rosterUrl: "https://raw.githubusercontent.com/帳號/repo/main/data/participants.xlsx",
};
```

如果貼的是 GitHub `blob` 網址，頁面也會自動轉成 raw URL。

## 注意

- 頁面使用 SheetJS 官方 CDN 讀取 Excel。
- 抽獎紀錄只存在目前瀏覽器的 `localStorage`，不會寫回 GitHub。
- 如果 Excel 放在私有 repo，GitHub Pages 通常無法直接讀取；建議使用公開可讀的 raw URL。
