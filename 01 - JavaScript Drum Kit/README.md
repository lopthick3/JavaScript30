# 01 - JavaScript Drum Kit

![](https://github.com/lopthick3/JavaScript30/blob/master/01%20-%20JavaScript%20Drum%20Kit/Drum%20Kit.png)

## 主題

透過 JS 在按下鍵盤後播出對應按鍵的聲音，並與網頁上顯示一個特效，在按下其他鍵後會移除該特效並在新按鍵顯示。

## 摘要

#### 新增 keydown listener

利用`window.addEventListener('keydown', playSound);`來監聽鍵盤動作。

#### 建立 function`playSound`

1. 利用傳入的 e.keyCode 來取得對應的`audio`標籤及該按鍵的`div`標籤
2. 判斷傳入的 e.keyCode 是否有對應的`audio`標籤，若無則退出
3. `key.classList.add("playing")`使對應的`div`加上`playing`CSS 樣式，產生對應的點擊特效
4. `audio.currentTime = 0`使對應的`audio`播放時間為 0
5. `audio.play()`播放對應的音檔

#### 新增 transitionend listener

1. 偵測所有包含`className='key'`的元件
2. 當該元件觸發特效並結束時(`transitionend`)，呼叫`removeTransition`

#### 建立 function`removeTransition`

1. 判斷傳入的 propretyName 是否為 transform，若否則退出
2. 若為 transform，則移除`playing`樣式

## JavaScript 語法&備註

### element.classList：

這個會回傳 element 的 class 值(陣列)，  
範例用到了 classList 的方法`add()`及`remove()`

```
classList.add('aaa', 'bbb', 'ccc'); //新增多個className
classList.remove('aaa', 'bbb', 'ccc'); //移除多個className
```

如果已經存在/不存在的 className 則會被忽略。

> 還有其他方法如:  
> `toggle()`偵測是否存在這個 className，存在則刪除/不存在則新增  
> `contains()`偵測是否存在這個 className, 返回 true/false  
> 參閱：[MDN-Element.classList](https://developer.mozilla.org/en-US/docs/Web/API/Element/classList)

### HTMLmediaElement(audio)：

HTML 的`audio`標籤，在 HTML 放置如下標籤指定音源

```
<audio src="sound/a.mp3"></audio>
```

透過 javascript 來操作：  
`element.play()`:進行播放  
`element.currentTime`:指定播放秒數  
範例中使用`currentTime`是為了讓音效在重複點擊按鍵時，能夠立即播放音效。

> 參閱：[MDN-HTMLMediaElement](https://developer.mozilla.org/en-US/docs/Web/API/HTMLMediaElement)

### document.querySelectAll()：

回傳的是 NodeList 不是 Array ，
NodeList 和陣列很像都有索引值，
但是 NodeList 不能用 Array 的方法。
