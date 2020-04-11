# What is NaN? What is its type? How can you reliably test if a value is equal to NaN?

The `NaN` property represents a value that is “not a number”. This special value results from an operation that could not be performed either because one of the operands was non-numeric (e.g., `"abc" / 4`), or because the result of the operation is non-numeric.

While this seems straightforward enough, there are a couple of somewhat surprising characteristics of NaN that can result in hair-pulling bugs if one is not aware of them.

For one thing, although `NaN` means “not a number”, its type is, believe it or not, `Number`:

```js
console.log(typeof NaN === 'number'); // logs "true"
```

Additionally, `NaN` compared to anything – even itself! – is false:

```js
console.log(NaN === NaN); // logs "false"
```

A _semi-reliable_ way to test whether a number is equal to NaN is with the built-in function `isNaN()`, but even [using `isNaN()` is an imperfect solution](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/isNaN#Confusing_special-case_behavior).

A better solution would either be to use `value !== value`, which would only produce true if the value is equal to NaN. Also, ES6 offers a new [`Number.isNaN()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/isNaN) function, which is a different and more reliable than the old global isNaN() function.
