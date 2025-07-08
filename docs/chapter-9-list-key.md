# React.js 零基础学习计划 - 第 9 章：列表渲染与 key

## 前言

在实际开发中，我们经常需要根据一组数据动态生成多个组件或元素，比如渲染学生名单、商品列表等。React 提供了高效的列表渲染方式，并要求为每个列表项指定唯一的 key。本章将带你学习列表渲染的常用方法、key 的作用与选择原则，并解释相关专业名词。

---

## 一、什么是列表渲染

列表渲染（List Rendering）指的是根据一组数据，动态生成多个组件或元素的过程。在 React 中，通常使用 JavaScript 的 map 方法遍历数组并生成 JSX 元素。

---

## 二、使用 map 渲染列表

最常见的做法是用 map 方法遍历数组，返回一个新的元素数组。

示例：
```jsx
function StudentList({ students }) {
  return (
    <ul>
      {students.map(student => (
        <li key={student.id}>{student.name}</li>
      ))}
    </ul>
  );
}

// 使用示例：
// <StudentList students={[{ id: 1, name: '小明' }, { id: 2, name: '小红' }]} />
```

---

## 三、key 的作用与选择原则

在渲染列表时，React 要求每个元素都要有一个唯一的 key 属性。

- **key 的作用**：帮助 React 高效地识别哪些元素发生了变化、被添加或删除。
- **选择原则**：
  - key 应该在同一列表中保持唯一。
  - 通常使用数据的唯一标识（如 id）。
  - 不推荐用数组索引作为 key，除非列表不会变动。

示例：
```jsx
function ProductList({ products }) {
  return (
    <div>
      {products.map(product => (
        <div key={product.sku}>
          <h3>{product.name}</h3>
          <p>价格：{product.price} 元</p>
        </div>
      ))}
    </div>
  );
}
```

---

## 四、key 的常见错误

- 使用重复的 key，导致渲染异常。
- 用数组索引作为 key，列表顺序变化时会导致状态错乱。

示例（不推荐）：
```jsx
function BadList({ items }) {
  return (
    <ul>
      {items.map((item, index) => (
        <li key={index}>{item}</li> // 不推荐用 index 作为 key
      ))}
    </ul>
  );
}
```

---

## 五、key 重复的后果

当 key 重复时，React 无法正确区分每个列表项的身份，会导致界面出现以下问题：

1. **渲染异常**：React 可能会错误地复用、更新或删除元素，导致渲染结果与预期不符。
2. **状态错乱**：如果列表项中有输入框、选中状态等本地状态，key 重复会导致状态“串台”或丢失。例如，编辑一个输入框内容时，另一个输入框的内容也可能被意外改变。
3. **动画或过渡效果异常**：使用动画库时，key 重复会导致动画效果混乱，出现闪烁、错位等问题。

### 具体界面表现举例

假设有如下代码，key 使用了数组索引，且数据顺序发生变化：

```jsx
function BadList({ items }) {
  return (
    <ul>
      {items.map((item, index) => (
        <li key={index}>
          <input defaultValue={item} />
        </li>
      ))}
    </ul>
  );
}
```

如果 items 从 `['A', 'B', 'C']` 变为 `['B', 'A', 'C']`，你在第一个输入框输入了“Hello”，切换顺序后，输入内容可能会跑到第二个输入框，界面表现为内容错位或丢失。

**结论：key 必须保证在同一层级唯一，否则会导致渲染异常、状态错乱、动画混乱等问题，影响用户体验和程序的可维护性。**

---

## 六、渲染多层嵌套列表

如果有多层嵌套数据，也可以多次使用 map，并为每一层元素分配唯一 key。

示例：
```jsx
function ClassList({ classes }) {
  return (
    <div>
      {classes.map(classItem => (
        <div key={classItem.classId}>
          <h2>{classItem.className}</h2>
          <ul>
            {classItem.students.map(student => (
              <li key={student.id}>{student.name}</li>
            ))}
          </ul>
        </div>
      ))}
    </div>
  );
}
```

---

## 七、专业名词解释

- **列表渲染（List Rendering）**：根据数据数组动态生成多个组件或元素的过程。
- **key**：React 用于标识每个列表元素的特殊属性，必须在同一层级唯一。
- **map 方法**：JavaScript 数组的内置方法，用于遍历数组并返回新数组。

---

## 八、进阶阅读

- [React 官方文档：渲染列表](https://react.dev/learn/rendering-lists)
- [React 官方文档：key 的用法](https://react.dev/learn/rendering-lists#keeping-list-items-in-order-with-key)
- [MDN：Array.prototype.map](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/map)

---

## 九、总结

本章介绍了 React 列表渲染的基本用法、key 的作用与选择原则，以及常见错误和嵌套列表的处理方法。掌握列表渲染和 key 的正确用法，是开发高效、可维护 React 应用的基础。

---

下一章将带你学习受控与非受控组件，敬请期待！ 