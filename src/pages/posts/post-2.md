---
layout: ../../layouts/MarkdownPostLayout.astro
title: 我的第二篇博客文章
author: Astro 学习者
description: "学习了一些 Astro 后，我根本停不下来！"
image:
    url: "https://docs.astro.build/assets/arc.webp"
    alt: "Thumbnail of Astro arcs."
pubDate: 2022-07-08
tags: ["astro", "blogging", "learning in public", "successes"]
---
# 什么是html5

html5在我看来不仅仅是一个标记语言的新版本，而是代表着它制定了一系列的web应用的开发标准。

## html5新特性

### 	1.语义化标签

html引入了很多语义化标签，例如<haeder>，<fotter>，<article>，<nav>等，它们用起来和div是一样的，相当于 ：

```javascript
<div class="header"> == <header>
```

这些语义化标签使得网页结构更加清晰，也有助于搜索引擎理解页面的内容。

### 2. 多媒体支持

在以前，网页想要播放视频，必须要用到flash插件，但是有的用户并没有安装flash，html5提供了一些原生的支持，通过<audio><video>标签，可以直接在网页中嵌入音频和视频文件，而不再需要依赖第三方插件。

### 3.canvas绘图

<canvas id="myCanvas" width="500" height="300"></canvas>

```js
//获取dom元素
var canvas = document.getElementById('myCanvas');
//获取2d上下文
var context = canvas.getContext('2d');
context.strokeRect(20, 20, 30, 30); // 描边矩形
context.fillRect(20, 20, 30, 30); // 填充矩形
```

### 4.本地存储

引入了localStorage和sessionStorage api，允许网页把数据存储在客户端

```js
// 使用 localStorage 存储的数据将一直存在，直到用户显式删除或清除浏览器缓存。下面是 localStorage 的一般用法：
localStorage.setItem('key',value) //存储数据
localStorage.getItem('key') // 获取数据
localStorage.removeItem('key') // 清除数据
localStorage.clear() // 清除所有数据
// 使用 sessionStorage 存储的数据只在当前会话期间有效，即当用户关闭浏览器标签页或窗口时，存储的数据将被清除。下面是 sessionStorage 的一般用法：
sessionStorage.setItem('key',value) //存储数据
sessionStorage.getItem('key') // 获取数据
sessionStorage.removeItem('key') // 清除数据
sessionStorage.clear() // 清除所有数据

```

---

 注意事项：

- 由于 `localStorage` 和 `sessionStorage` 存储的数据仅限于同源的页面之间共享，因此无法跨域访问。
- 存储的数据是以字符串形式存储的，如果需要存储复杂类型的数据（如对象），需要先将其转换为字符串再存储，取出时需要再转换为原来的类型。
- 存储的数据量通常限制在 5MB 左右，超出限制可能会导致存储失败。

这些 API 可以用于在客户端存储一些需要在页面会话之间或页面关闭后仍然保持的数据，比如用户的偏好设置、登录状态等。

```js
// 存数据
var obj = { name: 'John', age: 30 }; 
var str = JSON.stringify(obj); 
localStorage.setItem('user', str);
// 取数据
var objs = JOSN.parse(localStorage.getItem('user'))
```

### 5.新的表单控件

例如:<input type='data'></input>,<input type='url'></input>,<input type='email'></input>等，不同的type代表不同的输入类型

### 6.增加了css3中的媒体查询

媒体查询就是根据设备的特性，例如屏幕宽度，设备方向，来设置不同的样式

```css
@media screen and (max-width:768px){
   /*  针对小屏幕设置的样式*/
}
@media screen and (min-width: 768px) and (max-width: 992px) {
  /* 在这里设置针对中等屏幕设备的样式 */
}
@media screen and (max-width: 768px) {
    .jj {
        background: black;
        width: 300px;
        height: 300px;
    }
}

@media screen and (min-width: 768px) {
    .jj {
        background: wheat;
        width: 300px;
        height: 300px;
    }
}
// 记住在and后面要加上空格，不然会出现语法错误导致代码不生效
```

### 7.web works

Web Worker 是在浏览器中新开了一个线程来执行 JavaScript 代码的，避免主线程的阻塞。

### 8.Geolocation  api

1. **getCurrentPosition()**：该方法用于获取用户的当前地理位置信息。它接收三个参数：一个成功回调函数、一个失败回调函数和一个选项对象，用于指定获取位置信息的一些参数。当成功获取用户位置信息时，成功回调函数将被调用并传入一个包含位置信息的 Position 对象；当获取位置信息失败时，失败回调函数将被调用并传入一个包含错误信息的 PositionError 对象。
2. **watchPosition()**：该方法用于持续监测用户的地理位置变化。它接收三个参数：一个成功回调函数、一个失败回调函数和一个选项对象。成功回调函数和失败回调函数的参数与 getCurrentPosition() 方法相同。watchPosition() 方法会返回一个用于取消监测的 WatchPosition ID，你可以使用 clearWatch() 方法来取消监测。
3. **clearWatch()**：该方法用于取消使用 watchPosition() 方法进行的位置监测。它接收一个 WatchPosition ID 作为参数，该 ID 是 watchPosition() 方法返回的值。

```js
// 获取用户当前地理位置信息
navigator.geolocation.getCurrentPosition(
  // 成功回调函数
  function(position) {
    // 获取到用户的地理位置信息
    var latitude = position.coords.latitude; // 纬度
    var longitude = position.coords.longitude; // 经度
    var accuracy = position.coords.accuracy; // 精确度

    console.log('Latitude:', latitude);
    console.log('Longitude:', longitude);
    console.log('Accuracy:', accuracy);
  },
  // 失败回调函数
  function(error) {
    // 获取位置信息失败
    console.error('Error occurred:', error.message);
  }
);
```



