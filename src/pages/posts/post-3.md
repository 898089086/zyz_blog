---
layout: ../../layouts/MarkdownPostLayout.astro
title: 我的第三篇博客文章
author: Astro 学习者
description: "我遇到了一些问题，但是在社区里面提问真的很有帮助！"
image:
    url: "https://docs.astro.build/assets/rays.webp"
    alt: "Thumbnail of Astro rays."
pubDate: 2022-07-15
tags: ["astro", "learning in public", "setbacks", "community"]
---
## es6的新特性

### 1.增加了let和const 变量

let 和const 定义的变量是块级作用域’{}‘。一个花括号就是一个块级作用域，它俩的区别就是const声明的常量不可变，let声明的可以变，他们都不可以重新赋值。

#### let 和var的区别

##### 1.作用域

let作用域是块级’{}‘，意味着{}内定义的变量，{}外不可访问

var作用域是函数作用域或者全局作用域，意味着只要在函数内，在{}内用var定义的变量，在函数内{}外也可以访问。

##### 2.变量提升

var 声明的变量存在变量提升，用var定义的变量会在执行代码前，先全部声明变量并且初始化为undefined。

```js
console.log(x); // 输出 undefined
var x = 10;
```

用let声明的变量在声明前访问就会存在暂时性死区

```js
console.log(x); // ReferenceError: Cannot access 'x' before initialization
let x = 10;
```

##### 3.重复声明

var可以重复声明，let会报错

##### 4.全局对象

使用var在全局声明的变量会变成全局对象的属性，例如window，可以通过全局对象来访问。

let不会

### 2.箭头函数

结构：（）=>{} 

#### 箭头函数的特点

##### 1.出现的作用就是简化函数操作

当箭头函数的函数体中只有一句函数时候，不用写return 

##### 2.箭头函数没有自己的this 

这里就引出了this的概念，在js中，this指向的是调用它的对象，例如：

```js
const obj ={
    name:'sam',
    thisfuncation:funcation(){
    console.log(this)
}
}
obj.thisfuncation()
// 会输出obj对象

```

this的指向是可以改变的，有三个函数的方法，bind，call，apply

bind会创建一个新的函数，将指定的对象绑定为新函数的this值，并且返回函数。

```js
const obj ={
    name:'alice'
}
function log(){
    console.log(this.name)//这里指定的this指向就是全局的window
}
const func = log.bind(obj) //这里的this指向的是obj
```

call会立即执行函数，并且可以传递参数

```js
const obj ={
    name:'alice'
}
function log(canshu){
    console.log(this.name,canshu)//这里指定的this指向就是全局的window
}
log.call(obj,'canshu') //这里的this指向的是obj,第二个就是传递的参数

```

apply会立即执行函数，并且可以传递参数,但是传递的参数是一个数组。

```js
const obj = { name: 'Alice' };

function greet(greeting) {
  console.log(`${greeting}, ${this.name}!`);
}

greet.apply(obj, ['Good afternoon']); // 输出 'Good afternoon, Alice!'

```



##### 3.**没有 `arguments` 对象**：

- 箭头函数没有自己的 `arguments` 对象，但是可以访问父作用域中的 `arguments`。

**`arguments`** 介绍

**`arguments`** 对象是一个类数组对象，它允许你访问你调用函数时传递的所有参数；

```js
function sum (){
    let total = 0;
    for(let i =0;i<arguments.length;i++){
        total += arguments[i]
    }
     console.log(total)
}
sum(1,2,3,4)//会输出10
```



### 3.模板字符串

此功能是一种特殊的定义字符串的方法，并且可以在字符串中嵌入变量、表达式和换行符，从而使字符串的创建更加灵活和简洁。

``使用这两个符号包括起来就可以定义

```js
`string`
`string ${bianlian}` //变量
`srting    //换行
text
`
```

### 4.扩展运算符

他是一种新的语法，用于展开可迭代的数组，类数组或者字符串，并且将他们转换为多个参数或者元素。

采用的是三个...，下面是一些常用的场景。

```js
const arr = [1,2,3]
const arr2 = [4,5,6]
const mergearray = [...arr,...arr2] //合并数组
const arrfuzhi = [...arr2]	//复制数组
const str = '123'
const charArray = [...str] //展开字符串
// 同样的用法也可以用到对象上面
```

### 5.解构赋值

用法如名，它可以从数组或者对象中提取值，然后直接赋值给变量。

```js
const [a,b,c] = [1,2,3]
const obj = {name :'alice',age:'30'}
const {name,age} = obj 
//默认值 当obj中没有name时，name就会赋'unkonwn'
const {name = 'unkonwn',age, } = obj 
// 剩余元素 这里的rest是[2,3,4]
const [first,...rest] =[1,2,3,4]

```

### 6.默认参数值

```js
function greet(name = 'World') {
  console.log(`Hello, ${name}!`);
}

greet(); // 输出 'Hello, World!'
greet('Alice'); // 输出 'Hello, Alice!'
```

### 7.模块化

使用export和import 就可以将js分开写

```js
// function
export function square(x) {
  return x * x;
}
```

```js
// app.js
import {square} form function.js
console.log(square(3))

```

### 8.promise对象

promise 是js中处理异步操作的对象，它代表一个异步操作的成功或者失败，以及返回的结果值。

#### 1.promise基本概念

- 状态：promise有三种状态，分别是pending（进行中），fulfilled（已成功），rejected（失败）。
- 状态转换：promise对象只能从pending转换到fulfilled，或者从pending中转换到rejected，并且状态一旦发生改变就不可逆。

#### 2.创建promise对象

```
const promise = new Promise ((resolve,reject)=>
{
// 异步操作
setTimeout(()=>{
resolve('传递的数值') // 改变Promise的状态
})
}
)
```

#### 3.处理promise对象

```js
promise.then((result)=>{
    console.log('success',result)
}).catch((error) => {
  console.error('Error:', error);
})
```

#### 4.定义promise对象的两种方法

```js
// 定义一个全新的promise对象，需要传入一个函数，并且这个函数会立即执行
new Promise((resolve,reject)=>{
})
/* 当传入的参数是一个普通的值（非 Promise 对象）时，Promise.resolve() 方法会返回一个状态为 fulfilled 的 Promise 对象，并将传入的值作为 Promise 对象的结果值。
如果传入的参数是一个 Promise 对象，则会直接返回这个 Promise 对象，不会进行额外的处理。*/
Promise.resolve('success')
```

### 9.es8出现的await和async

await和async是promise的高级语法糖，它提供一种异步操作更加同步的写法。

在开始我总是想要理解await和async与promise中的.then方法对应，这样理解起来反而更难了。

所幸我就分来理解，promise就是promise，await就是await

使用了async定义的函数会返回一个promise对象，这时可以用这个函数进行.then,.catch方法。

await必须要和async一起使用，一般是在await后方加入异步操作，await代表着等待，只有等待这个异步操作完成以后，才会往下执行，它使我们的回调地狱问题写起来都不用像promise中的.then的链式调用，直接像同步的写法一样就可以

在我看来它们的使用场景有一些不同，promise更适合多个异步操作，await 适合一个异步操作后接下的的异步操作需要上一个异步操作。

async/await使得异步代码看起来像同步代码，这正是它的魔力所在

```js
async function data(){
    const response = await //异步操作
    const response2 = await //异步操作，并且参数需要response
}
```





