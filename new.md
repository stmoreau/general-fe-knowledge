## `new`

The four things that the `new` keyword actually does when we put it in front of a function call.

1.  It creates a brand new empty object
2.  That newly created object gets linked to another object
3.  That newly created object gets passed in as as the `this` context to the function call
4.  If that function does not already `return` its own object the `new` keyword assumes that you meant to return that object it was passed in

### The new operator implemented in JavaScript

```js
function newOperator(Constr, args) {
  var thisValue = Object.create(Constr.prototype); // (1)
  var result = Constr.apply(thisValue, args);
  if (typeof result === 'object' && result !== null) {
    return result; // (2)
  }
  return thisValue;
}
```

Line 1: The prototype of a `new` instance of a constructor `Constr` is `Constr.prototype`
Line 2: The implementor of a constructor can override that the `new` operators returns `this`, by returning an object. This is useful when a constructor should return an instance of a sub-constructor.
