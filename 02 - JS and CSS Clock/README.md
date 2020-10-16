# 02 - JS and CSS Clock

![](https://github.com/lopthick3/JavaScript30/blob/master/02%20-%20JS%20and%20CSS%20Clock/Clock.png)

## 主題

用 JS 與 CSS 搭配製作一個實時的時鐘效果。

## 摘要

#### 製作時針、分針、秒針

利用 class`hand`樣式來製作出時針、分針、秒針

#### 設定定時器

利用`setInterval(setDate, 1000);`設置每次執行時間、執行時的內容。

#### 建立 function`setDate`

利用`now = new Date()`將分秒時取出，並計算出對應角度  
再透過`element.style.tranform`來變更 CSS 效果，產生位移的感覺。

## **CSS 語法&備註**

### **transform-origin**

橫線使用 transform:rotate(90deg)會變成直線，
預設情況下，會以中心點當作軸心旋轉(50%)，
若要移動軸心則要使用 transform-origin:100%(最右側)。

### **transform:rotate()**

旋轉物件，數值後方要加上角度`deg`，  
可超過 360 度，正值為順時針轉，負值為逆時針旋轉。

### **transition-timing-function: cubic-bezier()**

設定動畫轉場所依據的貝茲曲線，可以透過 chrome 的開發者工具來進行可視化調整。

## JavaScript 語法&備註

### Date()

取得時間的函數，一定要搭配 new 來使用`new Date()`  
`date.getSeconds()`：取得當前秒  
`date.getMinutes()`：取得當前分鐘  
`date.getHours()`：取得當前小時

### setInterval()

定時器，有兩個參數`setInterval(callback, time)`  
第一個是要執行的 function，第二個是時間(毫秒)

### transform:rotate 的彈跳問題

為了要讓指針從 12 點方向(0 點)開始計算，
作者將指針.hand 都加上了 rotate(90deg)來轉，
並在計算時間的 function 內最終結果也都+90。

作者最後提到的一個小問題，若指針在 354 度切到 90 度時，  
會使指針往前彈回去，這是因為有使用 transtion，在角度做切換時會加上的動畫效果，  
354→90 度會認為是往前，而非轉一圈回到起點，所以動畫先往前轉到 90。  
為了避免這個反彈的怪現象，我另外加上了一個 function 來處理角度

```javascript
function setRotate(deg) {
  if (deg === 90) {
    secondsHand.style.transition = "none";
    minsHand.style.transition = "none";
    hoursHand.style.transition = "none";
  } else {
    secondsHand.style.transition = "";
    minsHand.style.transition = "";
    hoursHand.style.transition = "";
  }
  return `rotate(${deg}deg)`;
}
```

當計算角度為 90 時，動畫效果設定 "none" 暫時不顯示，其餘設定" "，就會使用原先設定的 CSS 樣式不去更改。

> 參閱：[stack-overflow](https://stackoverflow.com/questions/11131875/what-is-the-cleanest-way-to-disable-css-transition-effects-temporarily/16575811)
