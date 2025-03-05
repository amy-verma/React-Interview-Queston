Q1: What is useRef, and how is it different from useState?
- useRef is a React Hook that lets you reference a value that's not needed for redering
- It doesn’t trigger re-renders when updated.
✅ Unlike useState, updating useRef does not trigger a re-render.

import {useState,useRef} from "react";

const Counter=()=>{
     const [count,setCount]=useState(0);
        const countRef=useRef(0);

        const incrementState=()=>{
            setCount(count+1);
        };
        const incrementRef=()=>{
            countRef.current +=1;
            console.log("Ref count",countRef.curent)
        };
    return(
       <div>
       <button onClick={incrementState}>Increment State</button>
       <button onClick={incrementRef}>Increment State</button>
       </div>
    )
}
✅ Key Difference:

useState updates cause re-renders.
useRef holds values across renders but does not trigger re-renders.
---------------------------------------------------------------------------------------------------------------
Q2: How can useRef be used to access DOM elements?
✅ useRef is commonly used to directly reference DOM elements in React.
Example: Focusing an Input Field

import {useRef} from "raect";

const InputFocus=()=>{
    const inputRef=useRef(null);

    const handleFocus=()=>{
        inputRef.current.focus();
    };
    return(
        <div>
        <input ref={inputRef} type="text" placeholder="type here..">
        <button onClick={handleFocus}>Focus Inpur</button>
        </div>
    )
}
--------------------------------------------------------------------------------------------------------
Q3: How can useRef be used to store previous state values?
--------------------------------------------------------------------------------------------------------
Q4: Can useRef be used to store a function reference?
------------------------------------------------------------------------------------------------
Q5: How can useRef be used to create a persistent interval?
-----------------------------------------------------------------------------------------
Q6: What are some common mistakes when using useRef?





