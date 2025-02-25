1️⃣ What is useEffect and why is it used?
     UseEffect is  a React Hook that allows you to perform side effects in functional components
 - Commonly used for:
 1. Fetching data from API 
 2. Updating DOM 
 3. Subscribing to or cleaning up event listners 
 4. Managing Timers and Intervals

 Example- 
 useEffect(()=>{

 },[])//here the useEffect runs only when the coponents mounts
---------------------------------------------------------------------------------------------------------------------
2️⃣ When does useEffect run?

 - useEffect runs in three scenarios depending on the dependency array:
1. Without Dependencies ([])->Runs once (on Mount)

useEffect(()=>{

},[])//>Runs once (on Mount)

2. With dependencies ([state]) → Runs when state changes

useEffect(()=>{
        console.log("State changed to:", count);
},[count])

3. Without a dependency array
useEffect(()=>{
    console.log("Runs on every render");
})
--
When does it run?	On mount, updates, or every render depending on dependencies
-----------------------------------------------------------------------------------------------------------------------------------
3️⃣ What happens if we don’t provide a dependency array in useEffect?
 If you don't provive a dependency array ,useEfect runs after every render

useEffect(() => {
    console.log("Runs on every render!");
});//This can cause performance issue if it runs too frequently
------------------------------------------------------------------------------------------------------------------------------------------
4️⃣ How do you clean up an effect in useEffect?
- to clean up an effect,return a function inside useEffect
useEffect(()=>{
    const interval=setInterval(()=>{
        clg("Interval Running...")
    },1000)

    return ()=>{
        clearInterval(interval);
        console.log("Interval Cleared")
    };
},[])//🔹 Cleanup happens when the component unmounts.
------------------------------------------------------------------------------------------------------------------------
5️⃣ Can useEffect be asynchronous?
- useEffect cannot be async but you can use an async function inside it.
Example-
useEffect(()=>{
    const fetchData=async()=>{
        const res=await fetch(");
        const data=await res.json();
        console.log(data)
    };
    fetchData();
},[])
🚀 Never make useEffect itself async! Use an async function inside it.

--------------------------------------------------------------------------------------------------------------------
6️⃣ What is the difference between useEffect and componentDidMount?

Feature	                        useEffect (React Hooks)	                    componentDidMount (Class Component)
Where it's used	            Functional components                                   	Class components
Runs on mount               	✅ Yes (if [] provided)	                                        ✅ Yes
Runs on updates             	✅ Yes (if dependencies exist)	                                ❌ No
Cleanup function	            ✅ Yes (returns a function)                                    	❌ No
---------
Example of componentDidMount (Class Component)

  class MyComponents extends Rect.Components{
    componenetDidMount(){
        console.og("Componenet Mounted)
    }
  }
-------------
Equivalent using useEffect (Functional Component)

useEffect(() => {
    console.log("Component Mounted!");
}, []);

-----------------------------------------------------------------------------------------------------------------

7️⃣ How do you prevent useEffect from running on initial render?
- You can use  a useRef to track the initial render and prevent useEffect from running

const isFirstRender = useRef(true);

useEffect(() => {
    if (isFirstRender.current) {
        isFirstRender.current = false;
        return;
    }
    console.log("Runs after first render");
}, [someState]);

✅ Now, useEffect will only run when someState changes but NOT on the first render.

------------------------------------------------------------------------------------------------------------------
8️⃣ Can you have multiple useEffect hooks in a component?
- Yes! You can have multiple useEffect hooks in a component, and they will run separately.

useEffect(() => {
    console.log("Effect 1: Runs on mount");
}, []);

useEffect(() => {
    console.log("Effect 2: Runs when count changes");
}, [count]);
----------------------------------------------------------------------------------------------------------------------------
9️⃣ How does useEffect work with event listeners?
useEffect(() => {
    const handleScroll = () => {
        console.log("User scrolled!");
    };
    
    window.addEventListener("scroll", handleScroll);

    return () => {
        window.removeEventListener("scroll", handleScroll);
        console.log("Cleanup: Event listener removed!");
    };
}, []);
✅ Now, the event listener is removed when the component unmounts.
----------------------------------------------------------------------------------------------------------
🔟 What are some common mistakes with useEffect?
❌ Forgetting the dependency array → Causes unnecessary re-renders.
❌ Modifying state inside useEffect without dependencies → Leads to an infinite loop.
❌ Using an async function directly in useEffect → Use a separate async function instead.
❌ Not cleaning up side effects → Can cause memory leaks.

11. Bonus Question: How can you optimize performance in useEffect?
- use the dependency array ([]) to prevent unnecessary execution.
2. useCallback and useMemo to optimize funtion and value dependencies.
3. Use the cleanup function to prevent memory leaks















import { useEffect, useState } from "react";

const BgChanger=()=>{
    const [color,setColor]=useState('bg-gray-500');

    useEffect(()=>{
        console.log(`useEffect Called: Background changed to ${color}`)
    },[])

    return(
        <div className={`w-full relative h-screen  ${color}`}>
            <div className="flex items-center justify-center absolute bottom-20 -translate-x-1/2 left-1/2">
                <button className="px-2 py-4 border text-white bg-black" onClick={()=>{
                    setColor("bg-blue-500")
                    console.log("usestate called")
                }}>
                    Click me
                </button>
                <button className="px-2 py-4 border text-white bg-black" onClick={()=>{
                    setColor("bg-purple-500")
                    console.log("usestate called")
                }}>
                    Purple
                </button>
              
            </div>
        </div>
    )
}

export default BgChanger;