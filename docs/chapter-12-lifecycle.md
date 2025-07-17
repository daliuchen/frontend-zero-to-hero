# React.js 零基础学习计划 - 第 12 章：函数组件的生命周期与 useEffect

## 前言

随着 React 16.8 及之后的版本，函数组件成为主流。函数组件没有传统的生命周期方法，而是通过 Hook（特别是 useEffect）来管理副作用和生命周期相关操作。本章将重点介绍 useEffect 的用法、原理和最佳实践。

---

## 一、函数组件的“生命周期”是什么？

虽然函数组件没有 componentDidMount、componentDidUpdate、componentWillUnmount 这些生命周期方法，但可以通过 useEffect 在不同阶段执行副作用操作，实现类似的生命周期管理。

---

## 二、useEffect 的基本用法

useEffect 是 React 提供的一个 Hook，用于在函数组件中处理副作用（如数据请求、事件监听、定时器等）。

**基本语法：**
```jsx
import { useEffect } from 'react';

function Demo() {
  useEffect(() => {
    // 这里写副作用逻辑（如数据请求、订阅等）
    return () => {
      // 这里写清理逻辑（如取消订阅、清理定时器等）
    };
  }, []); // 依赖数组
  return <div>内容</div>;
}
```

---

## 三、useEffect 的生命周期模拟

- **componentDidMount（挂载）**  
  依赖数组为空（[]）时，useEffect 只在组件首次渲染后执行一次。
  ```jsx
  useEffect(() => {
    // 只在挂载时执行
  }, []);
  ```

- **componentDidUpdate（更新）**  
  依赖数组中指定的变量变化时，useEffect 会重新执行。
  ```jsx
  useEffect(() => {
    // id 变化时执行
  }, [id]);
  ```

- **componentWillUnmount（卸载）**  
  useEffect 返回的函数会在组件卸载时执行，用于清理副作用。
  ```jsx
  useEffect(() => {
    // 订阅
    return () => {
      // 取消订阅
    };
  }, []);
  ```

---

## 四、常见应用场景

- 数据请求（如获取远程数据）
- 事件监听与清理（如 window.addEventListener）
- 定时器的设置与清理
- 依赖 props 或 state 变化时执行逻辑

**示例：定时器组件**
```jsx
import { useState, useEffect } from 'react';

function Timer() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    const timer = setInterval(() => setCount(c => c + 1), 1000);
    return () => clearInterval(timer); // 清理定时器
  }, []);

  return <div>计时：{count} 秒</div>;
}
```

---

## 五、useEffect 的注意事项

- **依赖数组**  
  - 空数组 []：只在挂载和卸载时执行一次
  - [a, b]：a 或 b 变化时执行
  - 不写依赖数组：每次渲染都会执行（不推荐）

- **清理副作用**  
  - 返回的函数用于清理（如取消订阅、清理定时器）

- **避免死循环**  
  - 依赖数组中要包含所有用到的外部变量，否则可能出现 bug 或死循环

---

## 六、与类组件生命周期的对比

| 生命周期阶段         | 类组件方法                | 函数组件（useEffect）         |
|----------------------|---------------------------|-------------------------------|
| 挂载                 | componentDidMount         | useEffect(() => {}, [])       |
| 更新                 | componentDidUpdate        | useEffect(() => {}, [deps])   |
| 卸载                 | componentWillUnmount      | useEffect 返回的清理函数      |

---

## 七、专业名词解释

- **useEffect**：React 的 Hook，用于在函数组件中处理副作用和生命周期相关操作。
- **副作用（Side Effect）**：如数据请求、定时器、事件监听等对外部环境有影响的操作。
- **依赖数组**：决定 useEffect 何时执行的参数。

---

## 八、进阶阅读

- [React 官方文档：useEffect](https://react.dev/reference/react/useEffect)
- [React 官方文档：Hooks 概览](https://react.dev/reference/react/hooks)

---

## 九、总结

本章重点介绍了函数组件中 useEffect 的用法及其生命周期管理能力。掌握 useEffect，有助于你在现代 React 项目中高效处理副作用和资源管理。

---

下一章将带你学习 Hooks 基础，敬请期待！ 