# Pentafox – JavaScript Assessment (My Submitted Code)

This file contains **my submitted answers** for the **Pentafox JavaScript assessment**.  
The code below is written exactly as provided during the assessment.

---


```js

import { useCallback, useEffect, useRef, useState } from "react"

Question 1: Fetch Multiple Users

async function getUsers(userIds){
    const result=userIds.map(id=>fetch('/users/${id}'))
    responses=await result.all(result)
    finalResult=await result.all(responses.map(response.json()))
    return finalResult
}

Question 3: Count States

function countStates(orders){
    return orders.reduce((acc,cO)=>){
        const status=cO.status
        if(acc[status]){
            acc[status]++
        }
        else{
            acc[status]=1
        }
        return acc
    }
}

Question 4: Dark Mode Timer (React)

function App() {
    const [darkMode, setDarkMode] = useState(false);
    
    const darkModeRef=useRef(darkMode)

    useEffect(()=>{darkModeRef.current=darkMode},[darkMode])

    const handleStart = () => {
        setTimeout(() => {
            alert(`Dark Mode is: ${darkMode}`); // BUG: Shows old state
        }, 5000);
    };

    return (
        <div>
            <input
                type="checkbox"
                checked={darkMode}
                onChange={e => setDarkMode(e.target.checked)}
            />
            <button onClick={handleStart}>Start Timer</button>
        </div>
    );
}

Question 5: User Profile Fetch

function UserProfile({ userId }) {
    const [user, setUser] = useState(null);
   
    const fetchUser = useCallback(async()=> {
        const res = await fetch(`/api/users/${userId}`);
        setUser(await res.json());
    },[userId])

    useEffect(() => {
        fetchUser();
    }, [fetchUser]); 

    return <div>{user?.name}</div>;
}

Question 6: Custom Debounce Hook

const useDebounce=(value,delay)=>{
    const [debouncedValue,setDebouncedValue]=useState(value)

    useEffect(()=>{
        const handler=setTimeout(()=>{
            setDebouncedValue(value)
        },delay)

        return()=>{
            clearTimeout(handler)
        }
    },[value,delay])

    return debouncedValue
}

Author
Seshagiri G
