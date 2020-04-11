# `var` vs `let`

`let` allows you to declare variables that are limited in scope to the block, statement, or expression on which it is used. This is unlike the `var` keyword, which defines a variable globally, or locally to an entire function regardless of block scope.

```js
for (var i = 1; i <= 5; i++) {
  setTimeout(function() {
    console.log('i : ' + i);
  }, i * 1000);
}
```

When you run the above code it will print `i : 6` five times.  
There are two reasons why:

* `i` is `6` at the end of the loop and all these timers run a lot later, so it's going to print `6` (surface reason)
* Why don't we get a new `i` for each iteration? Because we use the `var`. We made one `i` attached to the existing scope (deeper reason)

To create a new `i` every time we can either replace `var` with `let`, or use an `IIFE` like so:

```js
for (var i = 1; i <= 5; i++) {
  (function(i) {
    setTimeout(function() {
      console.log('i : ' + i);
    }, i * 1000);
  })(i);
}
```
