# Asynchronous programming

If you have any I/O-bound needs (such as requesting data from a network or
accessing a database), you'll want to utilize asynchronous programming. You
could also have CPU-bound code, such as performing an expensive calculation,
which is also a good scenario for writing async code.

## Materials & Resources

### Materials

| Material                                                                 |  Time |
| :----------------------------------------------------------------------- | ----: |
| [CPU Bound vs. I/O Bound](https://www.youtube.com/watch?v=Wsv07g4ml8I)   | 15:01 |
| [Promises Part 1](https://www.youtube.com/watch?v=QO4NXhWo_NM)           | 24:52 |
| [Promises Part 2](https://www.youtube.com/watch?v=AwyoVjVXnLk)           | 11:49 |
| [async/await Part 1](https://www.youtube.com/watch?v=XO77Fib9tSI)        |  6:40 |
| [async/await Part 2](https://www.youtube.com/watch?v=chavThlNz3s)        | 10:07 |
| [try / catch with Promises](https://www.youtube.com/watch?v=BztW_u6HDbs) |  7:27 |

### Optional

| Material                                                     |  Time |
| :----------------------------------------------------------- | ----: |
| [Promise.all()](https://www.youtube.com/watch?v=01RTj1MWec0) | 11:43 |

## Material Review

- Give an example of an I/O-bound and a CPU-bound work<!--
  Reading a file from the disk, or a network request is I/O bound
  Compressing files to create an archive or audio/video processing is CPU
  bound -->
- How does asynchronous programming help with I/O or CPU bound work?<!--
  Makes your code more efficient by letting the CPU not wait idle for an
  operation to complete, e.g. the CPU can work on other tasks until the HTTP
  response arrives-->
- What's a Promise in JavaScript?<!--
  It's an object that represents value in the future you can wait for.
  E.g. the fetch function returns a Promise, and you can wait for the value to
  be available once the response completes-->
- What are the potential states of a Promise?<!--
  Pending: still waiting for the value
  Fulfilled: the value successfully arrived
  Rejected: something bad happened -->
- How to handle a fulfilled Promise?<!--
  Using the `then()` method -->
- What's the return value of the `then()` method and why is that useful?<!--
  The `then()` method **always** returns a Promise, that's guaranteed.
  It might be rejected but it's still a Promise.
  This is great because we can chain promises together -->
- What's the benefit of chaining Promises together?<!--
  It makes the code more readable compared to using callbacks-->
- How to handle a rejected Promise?<!--
  Using the `catch()` method -->
- How to create your own Promise?<!--
  Using the Promise constructor function -->
- How can you turn a function with a callback to a Promise?<!--
  Be wrapping the function around with a Promise, see example below -->
- What's an `async` method?<!--
  A method returning a Promise. It automatically wraps the result into a
  Promise -->
- What does the `await` keyword do?<!--
  It means asynchronous wait, meaning wait for the promise to be resolved but
  let the thread do other things in the meantime.
  In the background it actually calls the `.then()` method on the Promise
  for you and  -->
- What's the benefit of using the `await` keyword?<!--
  It's a syntax sugar: the code looks more like regular code instead of
  having all the `.then()` method call. -->
- What happens when using the `await` keyword on a rejected Promise?<!--
  It's going to throw an exception -->
- (Optional) How to wait for multiple promises simultaneously?<!--
  Using the Promise.all() method, which returns a promise which is fulfilled
  once every promise is fulfilled -->

## Workshop

### Promise

You've already used Promises:

```javascript
let promise1 = fetch('http://example.com');

let promise2 = promise1.then(res => res.json());

let promise3 = promise2.then(data => console.log(data));
```

#### Chaining

One of the biggest benefits of using Promises is chaining. You can chain
multiple HTTP calls after each other:

```javascript
fetch('http://example.com/api/users/me')
  .then(res => res.json())
  .then(user => fetch(`http://example.com/api/profiles/${user.id}`))
  .then(res => res.json())
  .then(profile => console.log(profile))
  .catch(error => console.error(error));
```

Note that you only needed one `catch()` at the end of the chain which handles
any error in the chain.

Do the following exercise to practice Promises:

- [Chaining](./chaining/js.md)

### Making Promises

It's fairly easy to turn every function which uses a callback to use a Promise:

```javascript
// This function wraps the setTimeout method in a Promise
function delay(timeout) {
  return new Promise(resolve => setTimeout(resolve, timeout));
}

// ...

// waiting for a second is easy now:
await delay(1000);
```

Practice turning callbacks into Promises:

- [Promisify](./promisify/README.md)

### Async/Await

Await makes Promises easier to read by removing the need for using the `.then()`
method:

```javascript
let response = await fetch('http://example.com');
let body = await response.json();

console.log(body);
```

Solve the following exercise using async/await:

- [Fetch some joke](fetch-some-joke/README.md)

Go back to one of the previous workshops and rewrite your solution using
async/await.

![](https://media.giphy.com/media/b44FwP4st6v3G/source.gif)
