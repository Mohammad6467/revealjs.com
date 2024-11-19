---
id: pdf-export
title: PDF 輸出
layout: default
---

# PDF 輸出

簡報可以通過特殊的列印樣式表導出為 PDF。這裡有一個已經上傳到 SlideShare 的導出簡報的範例：https://slideshare.net/hakimel/revealjs-300。

注意：此功能目前僅確認在 [Google Chrome](https://google.com/chrome) 和 [Chromium](https://www.chromium.org/Home) 中可行。

## 操作說明

1. 使用包含 `print-pdf` 的查詢字符串打開你的簡報，例如：`http://localhost:8000/?print-pdf`。你可以在 [revealjs.com/demo?print-pdf](/zh-hant/demo/?print-pdf) 測試這個功能。
1. 打開瀏覽器中的列印對話框（CTRL/CMD+P）。
1. 將 **目的地** 設置更改為 **保存為 PDF**。
1. 將 **佈局** 更改為 **橫向**。
1. 將 **邊距** 更改為 **無**。
1. 啟用 **背景圖形** 選項。
1. 點擊 **保存** 🎉

![Chrome Print Settings](https://s3.amazonaws.com/hakim-static/reveal-js/pdf-print-settings-2.png)

## 演講者筆記

你的[演講者筆記](/zh-hant/speaker-view/)可以通過啟用 `showNotes` 選項包含在輸出的 PDF 中。

```js
Reveal.configure({ showNotes: true });
```

筆記將在幻燈片上方的一個覆蓋框中列印。如果你希望將它們列印在幻燈片後面的單獨頁面上，將 `showNotes` 設置為 `"separate-page"`。

```js
Reveal.configure({ showNotes: 'separate-page' });
```

## 頁碼

如果你想在列印頁面上加上頁碼，請確保啟用[幻燈片編號](/zh-hant/slide-numbers/)。

## 頁面大小

導出尺寸是從配置的[簡報大小](/zh-hant/presentation-size/)中推斷出來的。如果幻燈片過高無法放在單一頁面內，它將擴展到多個頁面。你可以使用 `pdfMaxPagesPerSlide` 配置選項來限制一個幻燈片可能擴展到的頁面數量。例如，要確保沒有任何幻燈片超過一頁，你可以將它設置為 1。

```js
Reveal.configure({ pdfMaxPagesPerSlide: 1 });
```

## 分段的單獨頁面

[分段](/zh-hant/fragments/) 默認在單獨的幻燈片上列印。這意味著，如果你有一個包含三個分段步驟的幻燈片，它將生成三個單獨的幻燈片，其中的分段會逐步顯示。

如果你喜歡在同一幻燈片上列印所有可見狀態的分段，你可以使用 `pdfSeparateFragments` 配置選項。

```js
Reveal.configure({ pdfSeparateFragments: false });
```

## 替代的導出方式

你也可以使用 [decktape](https://github.com/astefanutti/decktape) 通過命令行將你的簡報轉換為 PDF。
