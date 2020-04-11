# What are closures?

_Closure is when a function "remembers" its lexical scope even when the function is executed outside that lexical scope._

Example

```js
function outer() {
  let counter = 0;
  function inner() {
    return counter++;
  }
  return inner;
}

const myFunc = outer();
myFunc();
```
