# React.js 零基础学习计划 - 第 3 章：JSX 语法

## 前言

在 React 开发中，JSX 是最常见的语法形式。它让我们可以像写 HTML 一样编写组件界面，同时拥有 JavaScript 的强大能力。本章将带你全面了解 JSX 的语法规则和使用方法。

---

## 一、什么是 JSX？

JSX（JavaScript XML）是一种 JavaScript 的语法扩展。它最初由 React 团队提出，目的是让 UI 代码更直观、声明式，主要为 React 框架服务。通过 JSX，开发者可以在 JavaScript 代码中直接书写类似 HTML 的标签结构，让界面描述更加直观、易读。

需要注意的是，JSX 并不是 JavaScript 官方标准，也不是浏览器原生支持的语法。它最终会被编译为普通的 JavaScript 代码后才能在浏览器中运行。虽然有部分其他前端库（如 Preact、Vue 3 的部分用法）也支持 JSX，但它并不是通用的 Web 标准，而是在实际开发中主要用于 React 及其生态系统。

---

## 二、JSX 的基本语法规则

1. **必须有根元素**：每个 JSX 片段只能有一个根节点。
2. **标签必须闭合**：单标签（如 `<img />`、`<input />`）必须自闭合。
3. **属性名采用小驼峰命名**：如 `className`、`htmlFor`。
4. **JSX 代码块用小括号包裹更清晰**。

示例：
```jsx
return (
  <div>
    <h1>Hello, React!</h1>
  </div>
)
```

---

## 三、表达式插值

在 JSX 中，可以用花括号 `{}` 插入任意 JavaScript 表达式（变量、运算、函数调用等）。

示例：
```jsx
const name = 'React';
return <h1>Hello, {name}!</h1>;
```

---

## 四、属性绑定

JSX 属性可以绑定变量或表达式，也可以直接写字符串。

示例：
```jsx
const url = 'https://react.dev';
// 变量绑定
return <a href={url}>React 官网</a>;
// 字符串写法
return <a href="https://react.dev">React 官网</a>;
```

---

## 五、注释写法

JSX 中的注释需要用 `{/* 注释内容 */}` 的形式，不能用 `//` 或 `/* */`。

示例：
```jsx
return (
  <div>
    {/* 这是一个注释 */}
    <h1>Hello, React!</h1>
  </div>
)
```

---

## 六、JSX 的本质与注意事项

- JSX 其实是 `React.createElement` 的语法糖。
- JSX 里不能直接写 if/else 语句，但可以用三元运算符或逻辑与（&&）表达式。
- 属性名和 HTML 有区别，如 `class` 要写成 `className`。
- 不能在 JSX 外层返回多个兄弟元素，可用 `<></>`（Fragment）包裹。

---

## 七、常见错误与调试

- 忘记闭合标签。
- 属性名拼写错误。
- 花括号内写了语句而不是表达式。
- 返回多个根元素。

遇到报错时，仔细检查 JSX 结构和语法。

---

## 八、总结

JSX 让 React 组件的界面描述更加直观和强大，是 React 开发的基础。掌握 JSX 语法，有助于你更高效地编写和维护前端代码。

---

如有疑问，欢迎留言讨论。下一章将带你学习组件的基础知识，敬请期待！ 