# React.js 零基础学习计划 - 第 10 章：受控与非受控组件

## 前言

在表单开发中，React 推荐使用“受控组件”来管理表单数据，但在某些场景下也可以使用“非受控组件”。本章将带你理解受控与非受控组件的区别、各自的用法和适用场景，并通过代码示例加深理解。

---

## 一、什么是受控组件

受控组件（Controlled Component）指的是表单元素的值完全由 React 的 state（状态）控制。每当用户输入内容时，都会触发 onChange 事件，进而更新 state，最终由 state 决定输入框的显示内容。

---

## 二、受控组件的实现方式

受控组件的核心是“value 受 state 控制，onChange 负责更新 state”。

示例：
```jsx
import { useState } from 'react';

function NameInput() {
  const [name, setName] = useState('');
  return (
    <div>
      <input value={name} onChange={e => setName(e.target.value)} />
      <p>你输入的名字是：{name}</p>
    </div>
  );
}
```

---

## 三、什么是非受控组件

非受控组件（Uncontrolled Component）指的是表单元素的值由 DOM 自己管理，React 不直接控制其值。通常通过 ref（引用）来获取或操作表单元素的值。

### 适用场景举例
- 需要与第三方库集成（如文件上传、富文本编辑器等）
- 表单内容不需要实时校验或联动
- 简单的、一次性读取表单内容的场景

---

## 四、非受控组件的实现方式

在函数组件中，通常使用 React 的 useRef 获取 DOM 元素的当前值。

> useRef 是 React 的一个 Hook，用于在函数组件中创建“引用对象”，可以用来访问 DOM 元素或保存可变数据。

示例：
```jsx
import { useRef } from 'react';

function NameInputUncontrolled() {
  // useRef 用于获取 input 元素的引用
  const inputRef = useRef(null);

  const handleSubmit = () => {
    // 通过 inputRef.current.value 获取输入框的值
    alert('你输入的名字是：' + inputRef.current.value);
  };

  return (
    <div>
      <input ref={inputRef} />
      <button onClick={handleSubmit}>提交</button>
    </div>
  );
}
```

---

## 五、受控与非受控组件的区别

| 特点           | 受控组件                           | 非受控组件                       |
|----------------|------------------------------------|----------------------------------|
| 数据来源       | React state                        | DOM（通过 ref 访问）             |
| 适合场景       | 需要实时校验、联动、受控逻辑复杂    | 简单表单、无需频繁读取表单内容   |
| 代码复杂度     | 稍高，需要管理 state               | 较低，无需 state                 |
| 推荐程度       | 推荐（React 官方最佳实践）         | 特殊场景可用                     |

---

## 六、受控组件的优势

- 便于做表单校验、联动、重置等操作
- 状态统一由 React 管理，数据流清晰
- 更易于测试和维护

---

## 七、常见错误与注意事项

- 不要同时为同一个表单元素设置 value 和 defaultValue，否则会导致行为异常。
- 不要混用受控和非受控写法（如一开始用 value，后面又用 ref 取值）。
- 受控组件必须有 onChange 事件，否则输入框内容无法修改。
- 非受控组件无法实现复杂的表单联动和实时校验。

---

## 八、专业名词解释

- **受控组件（Controlled Component）**：表单元素的值由 React state 控制。
- **非受控组件（Uncontrolled Component）**：表单元素的值由 DOM 自己管理，通过 ref 获取。
- **ref（引用）**：React 提供的访问 DOM 元素或组件实例的方法。
- **useRef**：React 的一个 Hook，用于在函数组件中创建引用对象，常用于获取 DOM 元素或保存可变数据。
- **state（状态）**：React 组件的数据源，决定组件的显示和行为。

---

## 九、进阶阅读

- [React 官方文档：受控组件](https://react.dev/learn/sharing-state-between-components#controlled-components)
- [React 官方文档：非受控组件与 ref](https://react.dev/reference/react/useRef)
- [MDN：HTML 表单元素](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input)

---

## 十、总结

本章介绍了受控与非受控组件的概念、实现方式、区别和适用场景，并提醒了常见表单处理误区。实际开发中，推荐优先使用受控组件，只有在特殊需求下才考虑非受控组件。掌握这两种表单处理方式，有助于开发更健壮、灵活的 React 应用。

---

下一章将带你学习组件通信，敬请期待！ 