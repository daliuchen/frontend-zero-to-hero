# React.js 零基础学习计划 - 第 8 章：条件渲染

## 前言

在实际开发中，我们经常需要根据不同的条件来决定界面上显示什么内容，这就是“条件渲染”。React 提供了多种实现条件渲染的方式，包括 if/else 语句、三元运算符、逻辑与（&&）等。本章将带你系统学习这些用法，并解释相关专业名词。

---

## 一、什么是条件渲染

条件渲染（Conditional Rendering）指的是根据某个条件，动态决定组件或元素是否渲染到页面上。它类似于 JavaScript 中的条件判断，只不过应用在 JSX 语法中。

---

## 二、if/else 语句实现条件渲染

最直观的方式是用 if/else 语句，在渲染前决定要显示的内容。这里我们采用对象结构赋值（解构）来获取参数。

示例：
```jsx
function Greeting({ isLoggedIn }) {
  if (isLoggedIn) {
    return <h1>欢迎回来！</h1>;
  } else {
    return <h1>请先登录。</h1>;
  }
}
```

---

## 三、三元运算符实现条件渲染

三元运算符（?:）可以在 JSX 中直接使用，适合简单的条件判断。

示例：
```jsx
function Greeting({ isLoggedIn }) {
  return (
    <h1>{isLoggedIn ? '欢迎回来！' : '请先登录。'}</h1>
  );
}
```

---

## 四、逻辑与（&&）实现条件渲染

逻辑与（&&）运算符可以根据条件决定是否渲染某个元素。当条件为 true 时，&& 后面的内容才会被渲染。

示例：
```jsx
function Mailbox({ unreadMessages }) {
  return (
    <div>
      <h1>收件箱</h1>
      {/* 只有有未读消息时才显示提示 */}
      {unreadMessages.length > 0 && (
        <p>你有 {unreadMessages.length} 条未读消息。</p>
      )}
    </div>
  );
}
```

---

## 五、元素变量的条件渲染

有时可以先用变量保存要渲染的内容，再在 JSX 中引用。

示例：
```jsx
function LoginControl({ isLoggedIn }) {
  let button;
  if (isLoggedIn) {
    button = <button>登出</button>;
  } else {
    button = <button>登录</button>;
  }
  return (
    <div>{button}</div>
  );
}
```

---

## 六、隐藏元素的方式

如果你不想渲染某个元素，可以让 render 返回 null，React 会跳过渲染。

示例：
```jsx
function WarningBanner({ warn }) {
  if (!warn) {
    return null; // 不渲染任何内容
  }
  return <div className="warning">警告！</div>;
}
```

---

## 七、专业名词解释

- **条件渲染（Conditional Rendering）**：根据条件动态决定渲染内容的技术。
- **三元运算符（?:）**：JavaScript 表达式，格式为 条件 ? 值1 : 值2。
- **逻辑与（&&）**：只有左侧条件为 true 时，右侧表达式才会执行。
- **JSX**：JavaScript XML，React 推荐的模板语法，允许在 JavaScript 代码中写 HTML 结构。

---

## 八、进阶阅读

- [React 官方文档：条件渲染](https://react.dev/learn/conditional-rendering)
- [MDN：三元运算符](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Conditional_Operator)
- [MDN：逻辑与运算符](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Logical_AND)

---

## 九、总结

本章介绍了 React 条件渲染的多种实现方式，包括 if/else、三元运算符、逻辑与（&&）、元素变量和返回 null 隐藏元素。条件渲染是实现动态界面和交互逻辑的基础能力，掌握这些技巧能让你的组件更加灵活和智能。

---

下一章将带你学习列表渲染与 key 的用法，敬请期待！ 