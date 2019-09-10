# Javascript Promises

From https://medium.com/javascript-in-plain-english/truly-understanding-promises-in-javascript-cb31ee487860

'Promises saves you from Callback Hell'

Promises: 
- After a promise is made, something will happen :)
- Can be kept or broken
- We can't on them immediately

The `Promise` object represents the asynchronous operation.
You need to:
- Create the Promise
- Handle the Promise

## Creation

```javascript
let promise=  new Promise(function(resolve, reject) {
    if (promise_kept) {
        resolve("done");
    } else {
        reject(new Error("Some error happened..."));
    }
});
```

- resolve and reject are callback functions
- Promises in in one of 3 states:
    - pending
    - fulfilled
    - rejected

## Handling and Consuming the Promise

```javascript
const isDone = new Promise();

const checkIfDOne = () => {
    isDone.then(ok => {
        console.log(ok);
    })
    .catch(err => {
        console.error(error);
    })
};
```

## Chaining Promises

```javascript
new Promise(function(resolve, reject) {
    setTimeout(() => resolve(1), 1000);
}).then(function(result) {
    alert(result);
    return result * 3;
}).then(function(result) {
    alert(result);
    return result * 4;
}).then(function(result) {
    alert(result);
    return result * 6;
})
```