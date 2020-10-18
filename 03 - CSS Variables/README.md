# **03 - CSS Variables**

![](https://github.com/lopthick3/JavaScript30/blob/master/03%20-%20CSS%20Variables/image/CSS%20Variables.png)

## **主題**

用 JS 與 CSS 搭配製作一個即時的濾淨效果，
特效為調整內距、模糊、邊框色。

## **摘要**

#### Step1

利用 CSS variable 來定義 CSS 的變數(有點像 sass 的感覺)

#### Step2

利用 addEventLinstener 來綁 HTML 的控制桿，  
並更新值到 CSS 變數中來達到即時調整的效果。

## **Javascript 語法&備註**

### **dataset**

用`dataset`可以取出對象的`data-*`屬性，也等同於`getAttribute`

```javascript
<div id="test" data-no="123"></div>;
document.querySelector("#test").dataset.no; // 輸出123
document.querySelector("#test ").getAttribute("data-no"); // 輸出123
```

而`this.dataset`會出現該選取項目中所有自己定義的`data-`的項目及值，是一個 object 物件。

```javascript
<div id="test" data-sizing="px" data-name="YuHan" data-cool="poop"></div>
```

![](https://github.com/lopthick3/JavaScript30/blob/master/03%20-%20CSS%20Variables/image/dataset.png)

### **style.setProperty()**

等同於 style.cssPropertyName

```javascript
style.setProperty("padding", "15px");
/* 等同於 */
style.padding = "15px";
```

但在實際應用中，前者的做法會很方便帶參數進去。

> 參照:[MDN-setProperty](https://developer.mozilla.org/en-US/docs/Web/API/CSSStyleDeclaration/setProperty)

### **document.querySelectAll()：**

回傳的是 NodeList 不是 Array ，
NodeList 和陣列很像都有索引值、forEach() 可以用，  
其他像是 map() reduce() ...其餘 Array 的方法都不能使用。

## **CSS 語法&備註**

### **:root{}**

`:root`是 DOM 元件的根元素，相當於`<html>`，一般會把 CSS 的變數聲明在內，CSS3 原生的變數表示法: `--variable`;

```CSS
\\宣告方式
:root {
        --base: #ffc600;
        --spacing: 10px;
        --blur: 10px;
      }

\\使用方式
      img {
        padding: var(--spacing);
        background: var(--base);
        filter: blur(var(--blur));
      }

      .hl {
        color: var(--base);
      }
```

### **filter:blur()**

CSS3 的濾鏡功能，blur 是高斯模糊，參數越高越模糊。

> 參照:[MDN-filter](https://developer.mozilla.org/en-US/docs/Web/CSS/filter)
