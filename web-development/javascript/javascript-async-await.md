# Javascript Async Await

## Async

Async functions enable us to write promise based code as if it were synchronous but without blocking the execution thread.

It operates asynchronously via the event loop.

They always return a promise.

```javascript
async function firstAsync() {
    return 27;
}

firstAsync().then(function(age) {
    console.log(`life was good at ${age}`)
});
```

## Await

The await operator is used to wait for a Promise.

It can be used inside an Async block only.

It only makes the `async` function block wait and not the whole program execution.

```javascript
async function firstAsync() {
    let promise = new Promise( (resolve, reject) => {
        setTimeout(() => resolve("Now it's done!", 1000))
    });

    let result = await promise;

    alert(result;)
};

firstAsync();
```

## To remmember when using Async Await

- You can't use `await` inside regular functions
- Async Await makes execution sequencial
- You can achieve parallel execution of Promises by using `Promise.all()`
    - The `Promise.all()` method returns a single `Promise` that resolves when all of the promises passed as an iterable have resolved. It rejects with the reason of the first promise that rejects.

    ```javascript
    async function sequence() {
        await Promise.all([promise1(), promise2()])
        return "done!";
    }
    ```


