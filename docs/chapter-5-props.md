# React.js 零基础学习计划 - 第 5 章：Props（属性）

## 前言

在 React 组件开发中，Props（属性）是组件之间通信和数据传递的基础。理解和正确使用 Props，是掌握组件化开发的关键。本章将带你全面了解 Props 的用法和注意事项。

---

## 一、什么是 Props？

Props（Properties，属性）是父组件向子组件传递数据的机制。通过 Props，父组件可以将数据、回调函数等传递给子组件，实现组件间的灵活通信。

---

## 二、Props 的传递方式

父组件在使用子组件时，通过类似 HTML 属性的方式传递数据，子组件通过参数（props 对象）接收。

示例：
```jsx
// 父组件
function App() {
  return <Welcome name="React" age={10} />;
}

// 子组件（常规写法）
function Welcome(props) {
  return <h1>Hello, {props.name}! 你今年 {props.age} 岁。</h1>;
}
```

除了常规的 props 访问方式，还可以使用“解构赋值”直接获取属性：

```jsx
// 子组件（解构赋值写法）
function Welcome({ name, age }) {
  return <h1>Hello, {name}! 你今年 {age} 岁。</h1>;
}
```

在现代 React 函数组件开发中，解构赋值是最常见、最推荐的写法。它让代码更简洁、清晰，便于维护和阅读。

---

## 三、Props 的只读特性

Props 是只读的，子组件不能直接修改从父组件传递下来的 Props。如果需要修改数据，应通过回调函数通知父组件，由父组件更新数据后再传递给子组件。

---

## 四、父子组件通信示例

父组件通过 Props 向子组件传递数据和回调函数，子组件通过调用回调函数与父组件通信。

示例：
```jsx
// 父组件
function App() {
  const handleClick = () => {
    alert('子组件点击了按钮！');
  };
  return <Child onButtonClick={handleClick} />;
}

// 子组件
function Child(props) {
  return <button onClick={props.onButtonClick}>点我</button>;
}
```

---

## 五、常见错误与调试

- 忘记 props 前的 `this`（类组件中）。
- props 类型不匹配。
- 试图在子组件中直接修改 props。
- 父组件未传递必需的 props。

遇到问题时，建议检查 props 的传递和类型定义。

---

## 六、总结

本章介绍了 Props 的基本概念、传递方式、只读特性以及父子组件通信方法。掌握 Props 的用法，是实现组件间高效通信的基础。

---

如有疑问，欢迎留言讨论。下一章将带你学习 State（状态）的用法，敬请期待！ 