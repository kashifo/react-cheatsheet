# 🧠 React Core Concepts

---

## ✅ Functional Components

**What is it?**
A JavaScript function that returns JSX. It's the standard way to build components in React today.

### Syntax

```jsx
function MyComponent() {
  return <h1>Hello React!</h1>;
}
```

👉 Use functional components for all UI blocks. They support hooks and are easier to test.

---

## ✅ Props and State

**What is it?**
**Props** are inputs to a component. **State** is managed internally by the component.

### Syntax

```jsx
function Greeting({ name }) {
  return <h1>Hello, {name}!</h1>;
}

function App() {
  return <Greeting name="Kashif" />;
}
```

---

## ✅ useState

**What is it?**
A hook to store and update local state in functional components.

### Syntax

```js
const [state, setState] = useState(initialValue);
```

### Example

```jsx
function LikeButton() {
  const [likes, setLikes] = useState(0);

  return (
    <button onClick={() => setLikes(likes + 1)}>
      Likes: {likes}
    </button>
  );
}
```

---

## ✅ useEffect

**What is it?**
A hook to run side-effects like data fetch, timers, DOM changes.

### Syntax

```js
useEffect(() => {
  // effect logic
  return () => cleanupFunction();
}, [dependencies]);
```

### Example

```jsx
function Timer() {
  const [seconds, setSeconds] = useState(0);

  useEffect(() => {
    const interval = setInterval(() => {
      setSeconds((prev) => prev + 1);
    }, 1000);
    return () => clearInterval(interval);
  }, []);

  return <p>Seconds: {seconds}</p>;
}
```

---

## ✅ Event Handling

**What is it?**
Attach interaction logic to JSX elements.

### Syntax

```jsx
<button onClick={handleClick}>Click Me</button>
```

### Example

```jsx
function Counter() {
  const [count, setCount] = useState(0);
  function handleClick() {
    setCount(count + 1);
  }
  return <button onClick={handleClick}>Count: {count}</button>;
}
```

---

## ✅ Conditional Rendering

**What is it?**
Render elements based on conditions.

### Syntax

```jsx
{condition ? <A /> : <B />}
```

### Example

```jsx
function Welcome({ isLoggedIn }) {
  return <h1>{isLoggedIn ? "Welcome back!" : "Please sign in"}</h1>;
}
```

---

## ✅ Lists and Keys

**What is it?**
Rendering arrays of elements. Each needs a unique `key` prop.

### Example

```jsx
function TaskList({ tasks }) {
  return (
    <ul>
      {tasks.map(task => (
        <li key={task.id}>{task.name}</li>
      ))}
    </ul>
  );
}
```

---

## ✅ CSS Modules

**What is it?**
Scoped CSS for React components.

### Usage

```jsx
import styles from './Button.module.css';

function Button() {
  return <button className={styles.primary}>Click</button>;
}
```

---

# 📈 Advanced React Concepts

---

## ✅ React Router (v6+)

**What is it?**
Client-side routing for SPAs.

### Syntax (Basic Setup)

```jsx
<BrowserRouter>
  <Routes>
    <Route path="/" element={<Home />} />
    <Route path="/about" element={<About />} />
  </Routes>
</BrowserRouter>
```

### Dynamic Routes

```jsx
<Route path="/product/:id" element={<ProductPage />} />
```

```jsx
function ProductPage() {
  const { id } = useParams();
  return <h1>Product ID: {id}</h1>;
}
```

---

## ✅ Forms: Controlled vs Uncontrolled

### Controlled Component

```jsx
const [name, setName] = useState('');
<input value={name} onChange={e => setName(e.target.value)} />
```

### Uncontrolled Component (not recommended)

```jsx
<input ref={inputRef} />
```

---

## ✅ useContext

**What is it?**
Access shared data (global state) without prop drilling.

### Example

```jsx
const ThemeContext = React.createContext();

function App() {
  return (
    <ThemeContext.Provider value="dark">
      <Toolbar />
    </ThemeContext.Provider>
  );
}

function Toolbar() {
  const theme = useContext(ThemeContext);
  return <div>Theme: {theme}</div>;
}
```

---

## ✅ Context API for Global State

**What is it?**
Manage app-wide state using React's built-in `createContext` and `useContext`.

### When to use?

* User login
* Theme
* Language
* Cart state

---

## ✅ useRef

**What is it?**
Access DOM nodes or persist values across renders (without triggering re-renders).

### Example (DOM access)

```jsx
const inputRef = useRef();

function focusInput() {
  inputRef.current.focus();
}

<input ref={inputRef} />
<button onClick={focusInput}>Focus</button>
```

---

## ✅ Redux (Simple Explanation)

**What is it?**
A state management library for global and predictable state.

### Basic Steps:

1. Create a reducer

```js
function counterReducer(state = 0, action) {
  switch(action.type) {
    case "INCREMENT": return state + 1;
    default: return state;
  }
}
```

2. Create a store

```js
const store = createStore(counterReducer);
```

3. Dispatch actions

```js
store.dispatch({ type: "INCREMENT" });
```

4. Connect to React (using `Provider` and `useSelector`, `useDispatch`)

---

## ✅ Optimizing Performance

### `React.memo` – Prevent re-renders if props don't change

```js
const MyComponent = React.memo(function MyComponent(props) { ... });
```

### `useCallback` – Memoize a function

```js
const memoFn = useCallback(() => {...}, [deps]);
```

### `useMemo` – Memoize a calculated value

```js
const memoValue = useMemo(() => expensiveCalc(), [deps]);
```

---
