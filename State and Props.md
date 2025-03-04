# State and Props in React

## 🏛 Understanding State in React

State is like a component's personal notebook. It holds information that **can change** over time and affects what gets displayed on the screen.

- State is **mutable** (can change).
- Each component **manages its own state**.
- When state updates, React **re-renders** the component.
- State is used to store **dynamic data** (e.g., user inputs, API responses).

### 📜 Example of State:
```jsx
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0); // Declaring state using useState

  return (
    <div>
      <h1>Count: {count}</h1>
      <button onClick={() => setCount(count + 1)}>Increase</button>
    </div>
  );
}

export default Counter;
```

📝 **Breakdown:**
- `useState(0)`: Initializes state `count` with a value of `0`.
- `setCount(count + 1)`: Updates the state when the button is clicked.
- React automatically re-renders the component when `count` changes.

---

## 🔄 What Are Props?
Props (short for **Properties**) are **read-only** inputs to a component. They allow data to be passed **from a parent component to a child component**.

- Props are **immutable** (cannot be changed by the child component).
- Used to pass **data** and **functions** between components.
- Helps in creating **reusable** components.

### 📜 Example of Props:
```jsx
import React from 'react';

function Greeting(props) {
  return <h1>Hello, {props.name}!</h1>;
}

function App() {
  return <Greeting name="SNSP" />;
}

export default App;
```

📝 **Breakdown:**
- `Greeting` is a child component that receives `name` as a **prop**.
- `App` component **passes** `"SNSP"` as a prop.
- The output will be **Hello, SNSP!**

---

## 🎭 State vs Props
| Feature    | State 🏛 | Props 📦 |
|------------|---------|---------|
| Mutability | Can change (mutable) | Cannot change (immutable) |
| Scope | Local to the component | Passed from parent to child |
| Usage | Stores data that changes over time | Passes data and functions |
| Update Method | `useState()` or `this.setState()` | Cannot be directly modified |

🎯 **When to use what?**
- Use **State** when you need to track changing data.
- Use **Props** when passing data from one component to another.

---

## 🔄 Props are **Immutable**
Props are a way to pass information between the components. But what if we want to modify them rather than passing them as is...

Imagine you have two components, In one you are taking the input from user and storing it in a variable or constant, then you are passing it to another component.

In another component you can copy the props into another variable or constant and then you can modify it but modifying props directly doesn't work, So this is how **Immutability** works

### 📜 Example of Props Immutabilty:
```jsx
import React from 'react';

function App() {
const Parent = () => {
        const num=10;
        return <Child  n={num}/>
    }
    const Child = (props) => {
        {props.n}=12;  // Props can'be changed directly as they are immutable
        return <p>{props.n}</p>;
    }
    return(
        <Parent />
    )
}
export default App;
```
OUTPUT :- Error 

### 📜 Example of How can we modify Props according to our need:
```jsx
import React from 'react';

function App() {
const Parent = () => {
        const num=10;
        return <Child  n={num}/>
    }
    const Child = (props) => {
        var res=props.n;
        res=20;
        return <p>{res}</p>;
    }
    return(
        <Parent />
    )
}
export default App;
```
OUTPUT :- 20
