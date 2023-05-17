<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@300;400&display=swap');

div {
    font-family: 'Montserrat', sans-serif;
    font-size: 16px;
    text-align: justify;
}
</style>
<div>

# Stale Closure
This is when a variable has an outdated value. Translated to React, is when a state´s value doesn´t updates in time when changed.
## Example of Stale Closure
``` javascript
cosnt createIncrement = (incBy) => {
    let value = 0;

    const increment = () => {
        value += incBy;
        console.log(value);
    }

    const message = `Current value is ${value}`;
    const log = () => {
        console.log(message);
    }
    
    return [increment, log];
}

const [increment, log] = createIncrement(1);
increment(); // logs 1
increment(); // logs 2
increment(); // logs 3
// Does not work!
log();      // logs "Current value is 0"
```
In this example we are returning two functions: one adds *`incBy`* value to the previous value and the other one logs the current value to the terminal. In this example the __`increment`__ function works as espected but, __`log`__ function doesn´t; it always returns 0.
## How to Solve the Stale Closure
One simple way to solve the stale is to move the `message` variable inside the __`log`__ function. This is caused because in the initial case `message` is out of the dominion of the returning function.
``` javascript
cosnt createIncrement = (incBy) => {
    let value = 0;

    const increment = () => {
        value += incBy;
        console.log(value);
    }

    const log = () => {
        const message = `Current value is ${value}`;  // <= Moved Message Here
        console.log(message);
    }
    
    return [increment, log];
}

const [increment, log] = createIncrement(1);
increment(); // logs 1
increment(); // logs 2
increment(); // logs 3
// Works!
log();      // logs "Current value is 3"
```
## Stale Closure in useEffect()
``` javascript
const WatchCount = () => {
    const [count, setCount] = useState(0);

    useEffect(function() {
        setInterval(function log() {
        console.log(`Count is: ${count}`);
        }, 2000);
    }, []);

    return (
        <div>
        {count}
        <button onClick={() => setCount(count + 1) }>
            Increase
        </button>
        </div>
    );
}
```
In this case `useEffect()` returns a function with a `setInterval()` that returns a function `log()` which logs to the console the actual value of *`count`* state. What happens here is that the actual value of *`count`* does updates in every click and rerenders in the screen the new value, but in the console the shown value is 0. This is because the value that `log()` takes to log at the moment of instanciation is the initial value of the state, whitch is 0. The log function get instanciated only once because is declarated inside the useEffect hook, this makes that on each rerender the function remain the same with the same values. The proper way to solve this stale is to add a dependency to useEffect:
``` javascript
const WatchCount = () => {
    const [count, setCount] = useState(0);

    useEffect(function() {
        setInterval(function log() {
        console.log(`Count is: ${count}`);
        }, 2000);
    }, [count]); // <= Variable added to the dependencies list.

    return (
        <div>
            {count}
            <button onClick={() => setCount(count + 1)}>
                Increase
            </button>
        </div>
    );
}
```
## Stale With useState()
The proper way is to use the function parameter for the `setState()`, this is the sintax:
``` javascript 
// Simpler Way
setState(actualStateValue => newStateValue);
// Complete Way
setState(actualStateValue => {
    // Do Some Operations.....
    return newStateValue;
});
```
## Resources
https://dmitripavlutin.com/react-hooks-stale-closures/
https://dilshankelsen.com/understanding-stale-closures-in-javascript/
</div>