### Using SetInterval in React.useEffect

A simple note but can lead to bugs when not used properly: 

Example: 

```
const [counter, setCounter] = useState(0);

  useEffect(() => {
    setInterval(() => {
      setCounter((prevCounter) => prevCounter + 1);
    }, 1000);

  }, []);

  return (
    <div className="App">
      <h1>Counter: {counter}</h1>
    </div>
  );
```
Let's run this and the result will be not like we expect.   
As the setInterval defined inside useEffect, it gets called every time when the component renders  
The component renders when one of state change? But in here when does the state change? When the setInterval func is called

So we don't want call setInterval function every time. We need to clear intervals every time component rerender
We can do it when a component is destroyed.  
Using the return inside useEffect function to solve this problem: 

```
 const interval = setInterval(() => {
      setCounter((prevCounter) => prevCounter + 1);
    }, 1000);

    return () => clearInterval(interval);
  }, []);
```