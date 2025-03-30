What is a hook?
- Hooks lets you to use differnet react features from your components.
- They are designed to work with functional componenets allows them to manage state and side effects


1. What is useState in React?

✅ Answer:
useState is a React Hook that allows functional components to manage state. It returns an array with two values:
 the current state and a function to update the state.

import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0); // count state initialized with 0

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
--------------------------------------------------------------------------------------
2. Can we update state directly in useState?
❌ No! You should never modify state directly. Always use the setter function.
------------------------------------------------------------------------------------------
3. How can we update state based on the previous state in useState?

- Use the functional update pattern to ensure you’re working with the latest state.

const [count, setCount] = useState(0);

const increment = () => {
  setCount(prevCount => prevCount + 1); // ✅ Using previous state safely //to avoid stale changes
};
This ensures React correctly updates the state even if there are multiple state updates in quick succession.
------------------------------------------------------------------------------------------------------------------------
4. Can useState hold an object or an array?
- Yes,useState can store objects,arrays or any data type
📌 Example (Object state):

const [user,setUser]=useState({name:"Amit",age:25});

const updateAge=()=>{
    setUser(prevUser =>((...prevUser,age:prevUser.age+1)))// ✅ Spread operator to keep old values
}
📌 Example (Array state):

const [items,setItems]=useState([]);
const addItem =()=>{
    setItem(prevItms=>[...prevItems,"New Items"])// ✅ Updating an array safely
}
-----------------------------------------------------------------------------------------------------
5. What happens if we call setState multiple times in one function?
- React batches state updates inside event handles foe better performance.
- if you update state for multiple times, React may merge them into single render.

const [count,setCount]=useState(0);

const handle=()={
    setCount(count+1)
    setCount(count+1)
    setCount(count+1)
};
<button onClick={handleClick}>Click Me</button>;
🔹 You might expect count to increase by 3, but it only increases by 1 because React batches updates.
🔹 To avoid this issue, use the functional update pattern:
setCount(prevCount=>prevCount+1)
setCount(prevCount=>prevCount+1)
setCount(prevCount=>prevCount+1)

Now, count will increase correctly by 3.
---------------------------------------------------------------------------------------------------
6. Does useState update the state immediately?
❌ No! useState updates the state asynchronously. The new state value is not available immediately after calling setState().

const [count, setCount] = useState(0);

const handleClick = () => {
  setCount(count + 1);
  console.log(count); // Still logs the old value because update is async!
};//🔹 To get the updated value immediately, use useEffect or functional updates.
--------------------------------------------------------------------------------------------------
7. What is the initial state of useState when given a function?
✅ Answer:
If you pass a function as an argument to useState, React calls the function only once (lazy initialization).

const [count, setCount] = useState(() => {
  console.log("Initializing...");
  return 0;
});//🔹 This is useful for expensive calculations that should run only on the first render.



