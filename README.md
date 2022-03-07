# 《DOM 事件模型》

1. 什么是捕获，什么是冒泡？

```
<div class=爷爷>
  <div class=爸爸>
    <div class=儿子>
    文字
    </div>
  </div>
</div>
//即 .爷爷>.爸爸>.儿子

```
爷爷=>爸爸=>儿子,从外向内找监听函数叫事件捕获。
儿子=>爸爸=>爷爷,从内向外找监听函数叫事件冒泡。

---

2. 事件绑定API

先捕获还是先冒泡？2002 年，W3C 发布标准规定浏览器应该同时支持两种调用顺序：
首先按爷爷=>爸爸=>儿子顺序看有没有函数监听
然后按儿子=>爸爸=>爷爷顺序看有没有函数监听
有监听函数就调用，并提供事件信息，没有就跳过
```
W3C：baba.addEventListener('click', fn, bool)
// bool = false 则为冒泡， bool = true 则为捕获
```
bool值为falsy，即当浏览器在冒泡阶段发现 baba 有 fn 监听函数，就会调用 fn，并提供事件信息。

---
3. target vs currentTarget
区别：
```
e.target - 用户操作的元素
e.currentTarget - 程序员监听的元素

```
举例：
```
div > span{文字}，用户点击文字
e.target 就是 span
e.currentTarget 就是 div

```