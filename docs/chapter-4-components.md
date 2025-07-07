# React.js 零基础学习计划 - 第 4 章：组件基础

## 前言

组件是 React 的核心思想之一。通过组件化开发，我们可以将界面拆分为独立、可复用的模块，让代码更易维护和扩展。本章将带你了解组件的基本概念、写法和使用方法。

---

## 一、什么是组件？

组件（Component）是 React 应用的基本构建单元。每个组件负责页面中的一部分内容和逻辑，可以像搭积木一样组合成完整的应用。组件让代码结构更清晰、复用性更高。

---

## 二、函数组件与类组件的区别

React 支持两种创建组件的方式：函数组件和类组件。

- **函数组件**：用 JavaScript 函数定义，写法简洁，推荐使用。
- **类组件**：用 ES6 class 定义，语法较复杂，主要用于需要生命周期和 state 的场景（早期写法）。

> 目前主流开发推荐使用函数组件，配合 Hooks 实现状态和副作用管理。

---

## 三、函数组件写法示例

```jsx
// 文件名：Hello.js
function Hello(props) {
  return <h1>Hello, {props.name}!</h1>;
}

export default Hello;
```

---

## 四、类组件写法示例

```jsx
// 文件名：HelloClass.js
import React from 'react';

class HelloClass extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}!</h1>;
  }
}

export default HelloClass;
```

---

## 五、组件的导入与导出

- **导出组件**：使用 `export default` 导出。
- **导入组件**：在需要使用的文件中用 `import` 引入。

示例：
```jsx
import Hello from './Hello';
import HelloClass from './HelloClass';

function App() {
  return (
    <div>
      <Hello name="React" />
      <HelloClass name="World" />
    </div>
  );
}
```

---

## 六、组件命名规范与组织建议

- 组件名首字母大写，文件名与组件名保持一致。
- 每个组件建议单独一个文件，便于维护和复用。
- 目录结构清晰，常见做法：`components/` 文件夹专门存放组件。

---

## 七、总结

本章介绍了 React 组件的基本概念、函数组件和类组件的写法，以及组件的导入导出和命名规范。掌握组件基础，是深入学习 React 的关键一步。

---

如有疑问，欢迎留言讨论。下一章将带你学习 Props（属性）的用法，敬请期待！ 