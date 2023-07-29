# IBI Group Web Development Placement Test

## Q1. What are the differences between cookie, local storage and session storage?

**Answer** - Cookies are small pieces of data that can be stored on the client-side with limited capacity and different lifetimes. Local storage has a larger capacity (5-10MB) and persists even after the browser is closed. Session storage has a similar capacity but is limited to the current session and clears when the session ends. Cookies are accessible on both client and server sides, while local and session storage can only be accessed using JavaScript. Cookies are commonly used for authentication and tracking, local storage for long-term storage, and session storage for temporary data during a user's session. The choice depends on data size, persistence needs, and accessibility requirements.

## Q2. Explain the output of the above-given code and explain why?

```javascript
for (var i = 0; i < 5; i++) {
  setTimeout(() => console.log(i), 100);
}
```

**Answer** - Output will be -

```bash
5
5
5
5
5
```

_Explanation_ - The given code uses a for loop to iterate from 0 to 4 (5 times).The `setTimeout` function is asynchronous, so it doesn't block the loop. When the loop finishes executing, the value of 'i' is 5. After the delay, the `console.log(i)` is executed five times, displaying 5 each time. This is because the arrow function inside `setTimeout` uses the reference to the 'i' variable, which has a final value of 5 when the functions are executed, resulting in the output: 5, 5, 5, 5, 5. If we do `let = 0` instead of `var i =0` then each iteration of the loop will create a new block-scoped variable 'i', and the closure inside `setTimeout` will capture the value of 'i' for each iteration separately. This means that when the arrow function is executed after the timeout, it will log the correct value of 'i' for each iteration, which will be -

```
0
1
2
3
4
```

## Q3. What is Sharding in MongoDB, and how does it work?

**Answer** - Sharding in MongoDB is a data partitioning technique used to distribute data across multiple servers or shards. It helps MongoDB handle large datasets and heavy workloads efficiently. Each shard holds a subset of the data, and MongoDB's balancer ensures data distribution among shards. When a query is made, MongoDB's router (mongos) routes it to the appropriate shard. This horizontal scaling approach allows MongoDB to scale out, improving performance and handling increased data volumes.

## Q4. What is promise chaining? Explain with an example.

**Answer** - Promise chaining is a technique in JavaScript used to perform a sequence of asynchronous operations in a more readable and manageable way. It involves chaining multiple promises together to ensure that one operation is executed after the previous one is resolved. Each operation returns a new promise, allowing further chaining.

_Example_ -

```javascript
// Asynchronous functions returning promises
function fetchUserData() {
  return fetch("https://api.example.com/user");
}

function parseJSON(response) {
  return response.json();
}

function displayUserData(userData) {
  console.log(userData);
}

// Promise chaining
fetchUserData()
  .then(parseJSON)
  .then(displayUserData)
  .catch((error) => console.error("Error:", error));
```

In this example, `fetchUserData` fetches user data, `parseJSON` parses the response, and `displayUserData` shows the parsed data. Promise chaining ensures the sequence is maintained, making the code more concise and readable.

## Q5. What are Higher-Order Components (HOC) in React and how do they work?

**Answer** - Higher-Order Components (HOC) in React are a design pattern used to enhance component reusability and logic sharing. They are functions that take a component as input and return a new component with additional props or behavior. HOCs enable cross-cutting concerns, like authentication or logging, to be encapsulated and reused across multiple components.

_Example_ -

```jsx
// HOC to add a loading spinner to a component
const withLoadingSpinner = (WrappedComponent) => {
  return ({ isLoading, ...otherProps }) => {
    return isLoading ? <Spinner /> : <WrappedComponent {...otherProps} />;
  };
};

// Usage of the HOC with a component
const MyComponent = ({ data }) => {
  return <div>{data}</div>;
};

const MyComponentWithLoading = withLoadingSpinner(MyComponent);
```

In this example, the `withLoadingSpinner` HOC takes `MyComponent` as input and returns a new component (`MyComponentWithLoading`) with a loading spinner displayed while the data is loading.

## Q6. What is callback hell? Explain different ways to solve callback hell with examples each.

**Answer** - Callback hell, also known as the Pyramid of Doom, is a situation in asynchronous programming where multiple nested callbacks make the code difficult to read, maintain, and debug. This occurs when multiple asynchronous operations depend on the results of previous ones, leading to deeply nested callbacks.

_Example_ -

```javascript
// Nested callbacks
doAsyncTask1((result1) => {
  doAsyncTask2(result1, (result2) => {
    doAsyncTask3(result2, (result3) => {
      // More nested callbacks...
    });
  });
});
```

Here are different ways to solve callback hell -

**1. Using Named Functions:**

```javascript
// Using named functions
function handleResult1(result1) {
  doAsyncTask2(result1, handleResult2);
}

function handleResult2(result2) {
  doAsyncTask3(result2, handleResult3);
}

doAsyncTask1(handleResult1);
```

**2. Using Promises:**

```javascript
// Using Promises
doAsyncTask1()
  .then((result1) => doAsyncTask2(result1))
  .then((result2) => doAsyncTask3(result2))
  .then((result3) => {
    // Continue with the final result...
  })
  .catch((error) => console.error("Error:", error));
```

**3. Using Async/Await:**

```javascript
// Using Async/Await
async function fetchData() {
  try {
    const result1 = await doAsyncTask1();
    const result2 = await doAsyncTask2(result1);
    const result3 = await doAsyncTask3(result2);
    // Continue with the final result...
  } catch (error) {
    console.error("Error:", error);
  }
}
fetchData();
```

Each method simplifies the control flow and makes the code more readable and maintainable by handling asynchronous operations in a more organized way, preventing callback hell. The choice of method depends on the specific use case and the version of JavaScript being used. Promises and Async/Await are widely preferred in modern JavaScript development.

## Q7. Use Array.reduce() method to reverse the following given array

`const arr = [1, 2, 3, 4, 5]`

**Answer** -

```javascript
const arr = [1, 2, 3, 4, 5];

const reversedArr = arr.reduce((accumulator, currentValue) => {
  return [currentValue, ...accumulator];
}, []);

console.log(reversedArr); // Output: [5, 4, 3, 2, 1]
```

## Q8. In what order will the numbers 1-4 be logged to the console when the code below is executed? Why?

```javascript
(function () {
  console.log(1);

  setTimeout(function () {
    console.log(2);
  }, 1000);

  setTimeout(function () {
    console.log(3);
  }, 0);

  console.log(4);
})();
```

**Answer** - The numbers 1, 4, 3, and 2 will be logged to the console in the following order:

- `console.log(1);` - This is the first statement inside the immediately invoked function expression (IIFE), so 1 will be logged to the console first.
- `console.log(4);` - This is the next statement after the first `console.log`, so 4 will be logged to the console.
- `setTimeout(function () { console.log(3); }, 0);` - This sets a timer with a delay of 0 milliseconds, but it won't be executed immediately. It will be moved to the event queue to execute after the current execution context completes.
- `console.log(2);` - This is inside a `setTimeout` with a delay of 1000 milliseconds (1 second), so 2 will be logged to the console after a delay of 1 second.

So, the order of logs will be: 1, 4, 3, and 2. This behavior occurs because JavaScript is single-threaded, and asynchronous operations like `setTimeout` are placed in the event queue and executed after the current execution context is complete.

## Q9. What will the code below output to the console and why?

```javascript
var arr1 = "john".split("");

var arr2 = arr1.reverse();

var arr3 = "jones".split("");

arr2.push(arr3);

console.log("array 1: length=" + arr1.length + " last=" + arr1.slice(-1));

console.log("array 2: length=" + arr2.length + " last=" + arr2.slice(-1));
```

**Answer** - The code will output the following to the console -

```bash
array 1: length=5 last=j,o,n,e,s
array 2: length=5 last=j,o,n,e,s
```

_Explanation_ -

- `arr1` is initialized as `['j', 'o', 'h', 'n']`.
- `arr2` is assigned the reversed `arr1`, which becomes `['n', 'h', 'o', 'j']`.
- `arr3` is initialized as `['j', 'o', 'n', 'e', 's']`.
- `arr3` is pushed as a single element to the end of `arr2`, making `arr2` `['n', 'h', 'o', 'j', ['j', 'o', 'n', 'e', 's']]`.
- When logging `arr1.length`, it's 5 because `arr1` still holds `['j', 'o', 'h', 'n']`.
- Logging `arr1.slice(-1)` and `arr2.slice(-1)` prints the last element of each array, which is the same, `['j', 'o', 'n', 'e', 's']`. Both `arr1` and `arr2` are referencing the same array in memory, so any changes to one will affect the other.

## Q10. What will the following code's output be in sequence and explain why?

```javascript
function printNumber(num) {
  console.log(num);
}

console.log(1);

setTimeout(printNumber, 0, 2);

setTimeout(printNumber, 100, 3);

console.log(4);
```

**Answer** - The output of the code will be as follows -

```bash
1
4
2
3
```

_Explanation_ -

- `console.log(1);`: The number 1 is logged to the console first.

- `console.log(4);`: The number 4 is logged to the console next.

- `setTimeout(printNumber, 0, 2);`: A `setTimeout` with a delay of 0 milliseconds is scheduled, but it won't be executed immediately. Instead, it will be moved to the event queue to execute after the current execution context completes. It will log the number 2.

- `setTimeout(printNumber, 100, 3);`: Another `setTimeout` is scheduled, this time with a delay of 100 milliseconds. It will be executed after the previous `setTimeout`. It will log the number 3.

The output sequence is determined by the JavaScript event loop. The initial execution will log 1 and 4 immediately, followed by the two `setTimeout` callbacks, which log 2 and 3 after a brief delay. The order of logs might slightly vary, but the relative sequence remains the same.

## Q11. Check the below given code, if there are any issues, fix them and explain the output

```javascript
const numbers = [1, 2, 3, 4, 5];

const result = numbers.reduce((acc, num) => {
  if (num % 2 === 0) {
    acc.evens.push(num);
  } else {
    acc.odds.push(num);
  }

  return acc;
});

console.log(result);
```

**Answer** - The code has an issue with the initial value provided to the `Array.reduce()` method. When using `Array.reduce()`, it's crucial to provide an initial value for the accumulator (the second argument of `reduce`). Otherwise, the first element of the array will be used as the initial value, and the iteration will start from the second element. In this case, since an initial value is missing, the iteration will start from `2`, and the result will be unexpected.

To fix this issue, we need to provide an initial value to the `reduce` method. We can initialize the accumulator with an object containing `evens` and `odds` arrays to correctly collect even and odd numbers.

```javascript
const numbers = [1, 2, 3, 4, 5];

const result = numbers.reduce(
  (acc, num) => {
    if (num % 2 === 0) {
      acc.evens.push(num);
    } else {
      acc.odds.push(num);
    }

    return acc;
  },
  { evens: [], odds: [] }
);

console.log(result);
```

Output -

```javascript
{ evens: [2, 4], odds: [1, 3, 5] }
```

With the correct initial value, the `Array.reduce()` method accumulates the even numbers in the `evens` array and the odd numbers in the `odds` array. The final result is an object with two arrays: `{ evens: [2, 4], odds: [1, 3, 5] }`.
