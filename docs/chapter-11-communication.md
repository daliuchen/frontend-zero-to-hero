# React.js 零基础学习计划 - 第 11 章：组件通信

## 前言

在实际开发中，组件之间经常需要传递数据或触发行为，这就是“组件通信”。React 提供了多种组件通信方式，包括 props、回调函数、Context 等。本章将带你系统学习父子、兄弟、跨层级组件通信的方法和场景。

---

## 一、父子组件通信

最常见的通信方式是通过 props（属性）将数据从父组件传递给子组件。

### 1. 父传子（props）

示例：
```jsx
function Child({ message }) {
  return <p>子组件收到：{message}</p>;
}

function Parent() {
  return <Child message="你好，子组件！" />;
}
```

### 2. 子传父（回调函数）

父组件可以将一个函数作为 props 传递给子组件，子组件通过调用该函数实现“子传父”。

示例：
```jsx
function Child({ onSend }) {
  return <button onClick={() => onSend('来自子组件的数据')}>发送数据给父组件</button>;
}

function Parent() {
  const handleReceive = data => {
    alert('父组件收到：' + data);
  };
  return <Child onSend={handleReceive} />;
}
```

---

## 二、兄弟组件通信

兄弟组件之间不能直接通信，通常通过“提升 state”到它们的共同父组件来实现。

示例：
```jsx
function SiblingA({ onChange }) {
  return <button onClick={() => onChange('A 发来的消息')}>A 发送</button>;
}

function SiblingB({ message }) {
  return <p>B 收到：{message}</p>;
}

function Parent() {
  const [msg, setMsg] = useState('');
  return (
    <div>
      <SiblingA onChange={setMsg} />
      <SiblingB message={msg} />
    </div>
  );
}
```

---

## 三、跨层级通信（Context）

### 1. 为什么需要 Context（Prop Drilling 问题）

在 React 应用中，组件通常是树状结构。父组件通过 props 向子组件传递数据，这种方式简单直观。但当某些数据（如主题、用户信息、语言设置等）需要被很多层级的组件共享时，单纯依靠 props 传递会出现“层层传递”（Prop Drilling）问题：
- 某些数据需要从顶层组件传递到很深层的子组件，中间的每一层都要“转手”这些 props，即使中间组件并不需要用到这些数据。
- 这样会让代码变得冗长、难以维护，组件之间的耦合度也会增加。

**举例：**
```
<App>
  <Layout>
    <Sidebar>
      <UserProfile user={user} />  // 这里需要 user
    </Sidebar>
  </Layout>
</App>
```
如果 user 数据在 App 顶层，必须一层层通过 props 传递到 UserProfile，哪怕 Layout 和 Sidebar 并不关心 user。

### 2. Context 能解决什么问题

Context 提供了一种“全局共享数据”的机制，可以让你在组件树中任何位置读取到某个数据，而不需要通过每一层 props 传递。
- 只需在顶层用 Provider 提供数据，任意深度的子组件都可以用 useContext 直接获取。
- 这样可以避免“层层传递”，让代码更简洁、组件更独立。

### 3. Context 的优点

1. 避免冗余的 props 传递，让中间组件不再为不需要的数据“中转”，降低了组件之间的耦合。
2. 全局数据共享，适合存放全局性的配置或状态（如主题、登录信息、多语言等）。
3. 让代码更易维护，组件结构更清晰，数据流更直观，维护和扩展都更方便。
4. 可以与自定义 Hook 结合，封装更强大的全局状态管理逻辑。

### 4. Context 的缺点

虽然 Context 解决了“层层传递”问题，但也有一些局限和注意事项：

1. **所有消费组件都会重新渲染**：当 Context 的 value 发生变化时，所有使用该 Context 的子组件都会重新渲染，可能导致性能下降，尤其是在大型应用中。
2. **不适合频繁变化的数据**：Context 更适合存放全局、稳定的数据。如果用来存放频繁变化的数据，会导致大量不必要的渲染。
3. **调试和追踪数据流变得困难**：Context 让数据流变得隐蔽，调试和维护时需要额外关注 Context 的变化。
4. **滥用会降低组件复用性**：如果把所有数据都放到 Context，组件会过度依赖全局状态，降低独立性和可复用性。
5. **类型和结构变更影响范围大**：Context 的结构或类型一旦变更，所有依赖它的组件都需要同步调整，维护成本较高。

**结论：Context 应按需使用，适合全局性、稳定性较高的数据。对于频繁变化或局部状态，仍推荐使用 props 或本地 state。**

### 5. Context 的详细用法

Context 的使用主要包括以下几个步骤：

#### （1）创建 Context

使用 `createContext` 创建一个 Context 对象，可以指定默认值。

```jsx
import { createContext } from 'react';

// 创建一个 ThemeContext，默认值为 'light'
const ThemeContext = createContext('light');
```

#### （2）Provider 提供数据

使用 Context 的 Provider 组件包裹需要共享数据的组件树，通过 value 属性传递数据。

```jsx
function App() {
  return (
    <ThemeContext.Provider value="dark">
      <Toolbar />
    </ThemeContext.Provider>
  );
}
```

#### （3）useContext/Consumer 消费数据

**推荐：useContext（函数组件）**

```jsx
import { useContext } from 'react';

function Toolbar() {
  const theme = useContext(ThemeContext);
  return <div>当前主题：{theme}</div>;
}
```

**传统写法：Consumer（适用于类组件或特殊场景）**

```jsx
<ThemeContext.Consumer>
  {theme => <div>当前主题：{theme}</div>}
</ThemeContext.Consumer>
```

#### （4）多层嵌套与多个 Context

Context 可以嵌套使用，也可以同时使用多个 Context。

```jsx
const UserContext = createContext(null);

function App() {
  return (
    <UserContext.Provider value={{ name: '小明' }}>
      <ThemeContext.Provider value="dark">
        <Profile />
      </ThemeContext.Provider>
    </UserContext.Provider>
  );
}

function Profile() {
  const user = useContext(UserContext);
  const theme = useContext(ThemeContext);
  return <div>{user.name} 的主题：{theme}</div>;
}
```

#### （5）默认值

如果组件没有被 Provider 包裹，则会使用 createContext 时指定的默认值。

```jsx
const ThemeContext = createContext('light');

function Demo() {
  const theme = useContext(ThemeContext); // 如果外层没有 Provider，这里为 'light'
  return <div>{theme}</div>;
}
```

#### （6）动态更新

Context 的 value 可以是 state，这样就能动态更新。

```jsx
import { useState } from 'react';

function App() {
  const [theme, setTheme] = useState('light');
  return (
    <ThemeContext.Provider value={theme}>
      <button onClick={() => setTheme(theme === 'light' ? 'dark' : 'light')}>切换主题</button>
      <Toolbar />
    </ThemeContext.Provider>
  );
}
```

### 6. Context 可以存放哪些数据结构

Context 的 value 属性可以存放任意 JavaScript 数据类型，包括：
- 基本类型：字符串、数字、布尔值等
- 对象：如配置对象、用户信息、主题设置等
- 数组：如菜单列表、权限列表等
- 函数：如全局方法、事件处理器等
- 组合结构：对象中嵌套数组、函数等

**可以自定义复杂数据结构**

你可以根据实际需求，将任意自定义的数据结构放入 Context。例如：

```jsx
const AppContext = createContext({});

const initialValue = {
  user: { name: '小明', age: 18 },
  theme: 'dark',
  setUser: () => {},
  logout: () => {},
  permissions: ['read', 'write']
};

function App() {
  const [user, setUser] = useState(initialValue.user);
  const logout = () => setUser(null);
  return (
    <AppContext.Provider value={{ user, theme: 'dark', setUser, logout, permissions: ['read', 'write'] }}>
      <MainPage />
    </AppContext.Provider>
  );
}
```

在子组件中可以通过 useContext(AppContext) 直接获取整个对象，并按需解构使用。

**注意事项**
- Context 的 value 变化会导致所有消费组件重新渲染，建议 value 结构尽量扁平、明确。
- 如果 value 是对象，推荐用 useMemo 优化，避免不必要的渲染。
- 不建议将所有应用状态都放入 Context，应按需拆分多个 Context，保持单一职责。

**总结：Context 支持任意类型和自定义结构，灵活性很高，但要注意性能和结构设计。**

---

## 四、常见通信场景总结

- 父传子：props
- 子传父：回调函数
- 兄弟通信：提升 state 到父组件
- 跨层级通信：Context

---

## 五、专业名词解释

- **props（属性）**：父组件向子组件传递数据的方式，只读。
- **回调函数**：父组件传递给子组件的函数，子组件调用后可通知父组件。
- **Context（上下文）**：React 提供的全局数据共享机制，适合跨层级通信。
- **useContext**：React 的 Hook，用于在函数组件中读取 Context 的值。
- **提升 state（Lifting State Up）**：将 state 放到最近的共同父组件，实现兄弟组件间通信。

---

## 六、进阶阅读

- [React 官方文档：组件通信](https://react.dev/learn/passing-props-to-a-component)
- [React 官方文档：Context](https://react.dev/learn/passing-data-deeply-with-context)
- [React 官方文档：提升 state](https://react.dev/learn/sharing-state-between-components)

---

## 七、总结

本章介绍了 React 组件通信的常见方式，包括父子、兄弟、跨层级通信及其实现方法。掌握这些通信技巧，有助于开发结构清晰、功能强大的 React 应用。

---

下一章将带你学习类组件的生命周期，敬请期待！ 