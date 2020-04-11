# What are the differences between a promise and an observable?

### A Promise is eager, whereas an Observable is lazy

Let’s start with the following Promise:

```js
const greetingPoster = new Promise((resolve, reject) => {
  console.log('Inside Promise (proof of being eager)');
  resolve('Welcome! Nice to meet you.');
});

console.log('Before calling then on Promise');

greetingPoster.then((res) => console.log(`Greeting from promise: ${res}`));
```

**The Promise in the above example is eager, since the callback function provided to a Promise constructor function is executed immediatelly**. If you execute the code, you will see that the message from within the Promise is displayed before calling a then method on the Promise object.

**On the contrary, an Observable is lazy.**

```js
const { Observable } = rxjs;

const greetingLady$ = new Observable((observer) => {
  console.log('Inside Observable (proof of being lazy)');
  observer.next('Hello! I am glad to get to know you.');
  observer.complete();
});

console.log('Before calling subscribe on Observable');

greetingLady$.subscribe({
  next: console.log,
  complete: () => console.log('End of conversation with preety lady'),
});
```

**If you create an Observable, you provide a callback function that will be called upon invoking subscribe method on the Observable object.** As you can see, the message ‘Before calling subscribe…’ will appear before the console.log from within the Observable.

You may compare the above examples to a situation in which you arrive at the hotel and you see a greeting poster (Promise-already prepared and available to read by calling then method), whereas an Observable is a greeting lady who greets each new guest when he arrives (calling subscribe method on an Observable).

### Observable can be synchronous

**Promise is always asynchronous. Even if it’s immediatelly resolved.**

```js
const greetingPoster = new Promise((resolve, reject) => {
  resolve('Welcome! Nice to meet you.');
});

console.log('Before calling then on Promise');

greetingPoster.then((res) => console.log(`Greeting from promise: ${res}`));

console.log('After calling then on Promise (proof of being always async)');
```

The message from within then method callback function will be the last one even though the Promise is resolved without a delay, since the call is added to the microtasks queue which will be processed after the current macrotask’s completion.

**However, an Observable can be synchronous.**

```js
const { Observable } = rxjs;

const greetingLady$ = new Observable((observer) => {
  observer.next('Hello! I am glad to get to know you.');
  observer.complete();
});

console.log('Before calling subscribe on Observable');

greetingLady$.subscribe({
  next: console.log,
  complete: () => console.log('End of conversation with preety lady'),
});

console.log('After calling subscribe on Observable (proof of being able to execute sync)');
```

In the above example, the order of messages is kept.

**On the other hand, an Observable can also be asynchronous.**

```js
const tiredGreetingLady$ = new Observable((observer) => {
  setTimeout(() => {
    observer.next('Hello! I am glad to get to know you.');
    observer.complete();
  }, 2000);
});

console.log('Before calling subscribe on Observable');

tiredGreetingLady$.subscribe({
  next: console.log,
  complete: () => console.log('End of conversation with tired preety lady'),
});

console.log('After calling subscribe on Observable (proof of being able to execute async)');
```

Now the notifications for an observer are delayed, therefore the Observable is asynchronous and both next and complete methods are called after ‘After calling subscribe…’ console.log.

### Observable can emit multiple values

**The next difference is that a Promise object may provide only a single value. It can be an array but it’s still a single object. On the contrary, an Observable may emit multiple values over time.**

```js
const { Observable } = rxjs;

const notifications$ = new Observable((observer) => {
  const interval = setInterval(() => {
    observer.next('New notification');
  }, 2000);

  return () => clearInterval(interval);
});

const subscription = notifications$.subscribe(console.log);

setTimeout(() => subscription.unsubscribe(), 8000);
```

In the above example, the Observable provides a new notification every 2 seconds. The subscription is cancelled after 8s.

As mentioned above, a Promise is a greeting poster (it’s done and you can read its message), whereas an Observable is a greeting person (she has to perform the same activity every time a new guest arrives).

## In a nutshell

The main differences between a Promise and an Observable are as follows:

- a Promise is eager, whereas an Observable is lazy
- a Promise is always asynchronous, while an Observable can be either synchronous or asynchronous
- a Promise can provide a single value, whereas an Observable is a stream of values (from 0 to multiple values)
- you can apply RxJS operators to an Observable to get a new tailored stream
