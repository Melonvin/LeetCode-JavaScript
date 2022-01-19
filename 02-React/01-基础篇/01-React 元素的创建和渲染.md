# React 元素的创建和渲染

**React** 是一个用于构建用户界面的 JavaScript 库

它包括两个库：**react.js** 和 **react-dom.js**

- `react.js`：React 的核心库，提供了 React.js 的核心功能，比如创建 React 组件、组件的生命周期等
- `react-dom.js`：提供了和浏览器交互的 DOM 功能，比如：将组件渲染到页面上

## React 和 ReactDOM

我们可以通过官方提供的 CDN 链接引入 react.js 和 react-dom.js 这两个库，从而在 HTML 中使用

```html
<script crossorigin src="https://unpkg.com/react@16/umd/react.production.min.js"></script>
<script crossorigin src="https://unpkg.com/react-dom@16/umd/react-dom.production.min.js"></script>
```

> `React` 是 React 库的入口。如果你通过使用 `<script>` 标签的方式来加载 React，则可以通过 `React` 全局变量对象来获得 React 的顶层 API
>
> 如果你使用一个 `<script>` 标签引入 react-dom，所有的顶层 API 都能在全局 `ReactDOM` 上调用

先来看看 React 和 ReactDOM 是什么：

```js
console.log(React)
console.log(ReactDOM)
```

`React`

![Snipaste_2022-01-12_17-02-08](https://melonvin-1302080640.cos.ap-shanghai.myqcloud.com/Snipaste_2022-01-12_17-02-08.png)

`ReactDOM`

![Snipaste_2022-01-12_17-03-20](https://melonvin-1302080640.cos.ap-shanghai.myqcloud.com/Snipaste_2022-01-12_17-03-20.png)

可以看到是两个对象，并且拥有很多方法，暂时不必深究每个方法

## React 初体验

首先我们在 html 中引入：react.js react-dom.js

```html
<script crossorigin src="https://unpkg.com/react@17/umd/react.development.js"></script>
    <script crossorigin src="https://unpkg.com/react-dom@17/umd/react-dom.development.js"></script>
```

目前我们的代码写在 html 中，所以都通过 script 标签引入这两个库（后续不再赘述）

接着我们在界面上添加一个根元素：

```html
<div id="root"></div>
```

如果我们想给这个根元素添加一段文字比如： Hello,React! ，我们可以这么做：

```html
<div id="root">
    Hello,React!
</div>
```



现在用 React 的方式来将这个标题渲染到页面上

我们要用到 ReactDOM 提供的 API ：`ReactDOM.render()`

```js
ReactDOM.render("Hello, React!", document.getElementById("root"), () => {
      console.log("渲染完执行回调函数");
});
```

[在线代码](https://codesandbox.io/s/react-01-nv8m4?file=/index.html)（可以点击在线代码查看效果）

事实上，render 方法接受 3 个参数：

- 要渲染的内容（"Hello, React!"）
- 渲染内容的接收容器（此处的根元素）
- 可选的回调函数（回调函数会在内容被渲染后执行）

## 创建 React 元素

如果我们想要渲染的内容是一个标题 h1 或者一个段落 p ，甚至是更复杂的元素嵌套该怎么办呢

```html
<!-- 比如 -->
<h1>Hello,React!</h1>
<p>第一次学习React，太简单了吧</p>
<!-- 甚至 -->
<div>
    <header>
        <h1>Hello,React!</h1>
    </header>
    <section>
        <p>第一次学习React，太简单了吧</p>
    </section>
</div>
```

React 提供了**创建并返回 React 元素**的 API：

```js
React.createElement(
  type,
  [props],
  [...children]
)
```

该方法接受 3 个参数：

- type：指定元素类型，比如 'h1'、'p'

- props：可选参数，元素的属性值对对象，比如

  `{className: 'bg-red', id: 'title'}`

- 可选参数，元素的子元素



**创建元素并渲染到指定容器**

```js
const h1 = React.createElement("h1", null, "Hello,React!");
const p = React.createElement("p", null, "第一次学react，太简单了吧");

const header = React.createElement("header", { id: "title" }, h1);
const section = React.createElement("section", null, p);
const div = React.createElement("div", null, header, section);
```

渲染到根元素：

```js
ReactDOM.render(div, document.querySelector("#root"));
```

[在线代码](https://codesandbox.io/s/react-02-wt9ep?file=/index.html:539-921)



**注意**

1. render 方法可以接受 createElement 创建的 React 元素作为渲染对象
2. render 方法属于 ReactDOM 对象
3. createElement 方法属于 React 对象

## JSX

每个 React 元素都用 createElement 创建有点麻烦啊，有没有简单点的办法

事实上，对于：

```js
const h1 = React.createElement("h1", null, "Hello,React!");
const p = React.createElement("p", null, "第一次学react，太简单了吧");

const header = React.createElement("header", { id: "title" }, h1);
const section = React.createElement("section", null, p);
const div = React.createElement("div", null, header, section);
```

可以这么写：

```jsx
const h1 = <h1>Hello,React!</h1>;
const p = <p>第一次学react，太简单了吧</p>;

const header = (
    <header>
        <h1>Hello,React!</h1>
    </header>
);
const section = (
    <section>
        <p>第一次学react，太简单了吧</p>
    </section>
);

const div = (
    <div>
        <header>
            <h1>Hello,React!</h1>
        </header>
        <section>
            <p>第一次学react，太简单了吧</p>
        </section>
    </div>
);
```

这种标签语法既不是字符串也不是 HTML

它被称为 **JSX**，是 JavaScript 的语法扩展

事实上，每个 JSX 元素一个语法糖，它们最终还是会调用`React.createElement(component, props, ...children)` 方法来创建 React 元素。不过我们写起来更加简单且直观

## JSX 初体验

我们将所有 createElement 创建的元素改写成 JSX

得到如下完整 HTML 页面

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <meta http-equiv="X-UA-Compatible" content="ie=edge" />
  <title>Static Template</title>
  <script crossorigin src="https://unpkg.com/react@17/umd/react.development.js"></script>
  <script crossorigin src="https://unpkg.com/react-dom@17/umd/react-dom.development.js"></script>
</head>

<body>
  <div id="root"></div>
</body>
<script>
  const h1 = <h1>Hello,React!</h1>;
  const p = <p>第一次学react，太简单了吧</p>;

  const header = (
    <header>
      <h1>Hello,React!</h1>
    </header>
  );
  const section = (
    <section>
      <p>第一次学react，太简单了吧</p>
    </section>
  );

  const div = (
    <div>
      <header>
        <h1>Hello,React!</h1>
      </header>
      <section>
        <p>第一次学react，太简单了吧</p>
      </section>
    </div>
  );

  ReactDOM.render(div, document.querySelector("#root"));
</script>

</html>
```

在浏览器中打开，会发现页面上的元素并没有得到正确的渲染

并且控制台输出了错误：`Uncaught SyntaxError: Unexpected token '<'`

这是因为浏览器并不认识 JSX，JSX 只是 React 团队自己造的东西，我们需要把 JSX 转换成符合 JS 规范的语法，这样浏览器就认识了

这跟将 ES6 语法转换成 ES5 差不多

什么东西能把 ES6 语法转换成 ES5 ？

没错，**Babel**



同样，借助 Babel 我们可以将 JSX 转换成 JS 语法

在页面中添加如下 script 标签

```html
<script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
```

并将 script 标签（指包含 JSX 语法的 script）的 type 属性改为：text/babel

```html
<script type="text/babel">
  const h1 = <h1>Hello,React!</h1>;
</script>
```

现在，元素可以正确的显示了

[在线代码](https://codesandbox.io/s/react-03-zv613?file=/index.html)



现在，我们已经学会了如何用 React 来创建元素和渲染元素，也知道了创建元素的语法糖 JSX。

我们已经知道怎么在页面上显示 `Hello,React!`，但是如果我想要显示的不是`Hello,React!`而是可以随意变动的值、或者是可以根据不同条件显示不同的值呢、又或者是一个数组中的全部内容呢？



