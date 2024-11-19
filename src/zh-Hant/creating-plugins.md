---
id: creating-plugins
title: 創建插件
layout: default
---

# 創建插件 <span class="r-version-badge new">4.0.0</span>

我們提供了一個輕量級的插件規範和 API。這被我們的預設插件如[代碼高亮](/zh-hant/code/)和 [Markdown](/zh-hant/markdown/) 使用，但也可以用來創建你自己的插件。

## 插件定義

插件是包含以下屬性的對象。

| 屬性                                         | 值                                                                                                                                                                                                                                                                                                                                             |
| :------------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| id <span class="r-var-type">字符串</span>    | 插件的唯一 ID。這可以用來通過 `Reveal.getPlugin(<id>)` 檢索插件實例。                                                                                                                                                                                                                                                                           |
| init <span class="r-var-type">函數</span>    | 可選的函數，當插件應該運行時被調用。它被調用時有一個參數；插件導入的[簡報實例](/zh-hant/api/)的引用。<br><br>init 函數可以選擇性地返回一個 [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)。如果返回了 Promise，reveal.js 將等待它解析完成，然後簡報初始化完成並觸發[準備好的事件](/zh-hant/events/#%E5%B0%B1%E7%B7%92)。 |
| destroy <span class="r-var-type">函數</span> | 可選的函數，當這個插件導入的 reveal.js 實例被卸載時調用。                                                                                                                                                                                                                                                                                        |

{.key-value}

這裡是一個範例插件，當按下 T 鍵時，它會在簡報中洗牌所有幻燈片。注意，我們導出一個返回新插件對象的函數。這樣做是因為同一頁面上可能有[多個簡報實例](/zh-hant/initialization/#multiple-presentations)，而每個實例都應該擁有我們插件的自己的實例。

```js
// toaster.js
export default () => ({
  id: 'toaster',
  init: (deck) => {
    deck.addKeyBinding({ keyCode: 84, key: 'T' }, () => {
      deck.shuffle();
      console.log('🍻');
    });
  },
});
```

## 導入插件

插件通過將它們包含在[配置選項](/zh-hant/config/)的 `plugins` 數組中來導入。你也可以在運行時使用 `Reveal.registerPlugin( Plugin )` 導入插件。

```js
import Reveal from 'dist/reveal.esm.js';
import Toaster from 'toaster.js';

Reveal.initialize({
  plugins: [Toaster],
});
```

### 異步插件

如果你的插件需要在 reveal.js 完成初始化之前運行異步代碼，它可以返回一個 Promise。這裡是一個會延遲初始化三秒的範例插件。

```js
let WaitForIt = {
  id: 'wait-for-it',
  init: (deck) => {
    return new Promise((resolve) => setTimeout(resolve, 3000));
  },
};

Reveal.initialize({ plugins: [WaitForIt] }).then(() => {
  console.log('Three seconds later...');
});
```
