## What is `useState`?
`useState` is a React Hook that lets you add state to functional components.

It returns two values:
1. **State variable** – Stores the current value.
2. **State updater function** – Used to modify the state and trigger a re-render.

## Basic Syntax of `useState`
```jsx
const [state, setState] = useState(initialValue);
```
- `state` → Holds the current value.
- `setState(newValue)` → Updates the state and causes a re-render.
- `initialValue` → Can be a number, string, object, array, boolean, etc.

## Example 1: Counter with `useState`
```jsx
import React, { useState } from "react";

const [count,setCount] = useState(0);
    const inc = () => {
        setCount(count+1);
    }
    const dec = () => {
        setCount(count-1);
    }
    return(
        <div>
            <button onClick={inc}>+</button>
            <button onClick={dec}>-</button>
            <p>Count: {count}</p>
        </div>
    );
};

export default Counter;
```
✅ State changes when the button is clicked, causing the component to re-render.

---

## Updating State Correctly
### Using a Function for State Updates
Since state updates may be asynchronous, use a function when updating based on previous state.
```jsx
setCount(prevCount => prevCount + 1);
```
✅ **Why?**
If multiple state updates happen in a single render, using a function ensures the latest state is used.

### Example: Incorrect vs Correct Update
#### ❌ Incorrect
```jsx
const Counter = () => {
    const [count, setCount] = useState(0);

    const incrementThreeTimes = () => {
        setCount(count + 1);
        setCount(count + 1);
        setCount(count + 1);
    };

    return (
        <div>
            <p>Count: {count}</p>
            <button onClick={incrementThreeTimes}>Increment x3</button>
        </div>
    );
};
```
❌ Issue: React batches state updates, so count won’t actually increase by 3.

#### ✅ Correct Version Using Function
```jsx
const incrementThreeTimes = () => {
    setCount(prevCount => prevCount + 1);
    setCount(prevCount => prevCount + 1);
    setCount(prevCount => prevCount + 1);
};
```
✅ This ensures count updates correctly! 🎯

---

## Working with Complex State Types

### Updating State in an Object
```jsx
const [user, setUser] = useState({ name: "SNSP", age: 22 });

const updateAge = () => {
    setUser(prevUser => ({ ...prevUser, age: prevUser.age + 1 }));
};
```
✅ Always spread the previous state (`...prevUser`) to avoid losing other properties.

### Updating State in an Array
```jsx
const [items, setItems] = useState([1, 2, 3]);

const addItem = () => {
    setItems(prevItems => [...prevItems, prevItems.length + 1]);
};
```
✅ Always create a new array (`[...prevItems]`) to maintain immutability.

---

## Lazy Initialization (`useState` with a Function)
If the initial state is expensive to calculate, use a function:
```jsx
const [count, setCount] = useState(() => {
    console.log("Initial render!");
    return 10;
});
```
✅ Function runs only on first render, not on re-renders.

---
