## this

Every function (except arrow functions), while executing, has a reference to its current execution context, called `this`.

> The only thing that matters is **how** the function was called

**Ask these questions in this order, and stop when the first rule applies.**

1.  Is the function called with `new` (**new binding**)? If so, `this` is the newly constructed object.  
    `var bar = new foo()`

2.  Is the function called with `call` or `apply` (**explicit binding**), `bind` which effectively uses `apply` (**hard binding**)? If so, `this` is the explicitly specified object.  
    `var bar = foo.call( obj2 )`

3.  Is the function called with a context (**implicit binding**), otherwise known as an owning or containing object? If so, `this` is that context object.  
    `var bar = obj1.foo()`

4.  Otherwise, default the `this` (default binding). If in `strict mode`, pick `undefined`, otherwise pick the `global` object.  
    `var bar = foo()`

Be careful of accidental/unintentional invoking of the _default binding_ rule. In cases where you want to "safely" ignore a `this` binding, a "DMZ" object like `ø = Object.create(null)` is a good placeholder value that protects the `global` object from unintended side-effects.

Instead of the four standard binding rules, ES6 arrow-functions use lexical scoping for `this` binding, which means they adopt the `this` binding (whatever it is) from its enclosing function call. They are essentially a syntactic replacement of `self = this` in pre-ES6 coding.

**Note**

Arrow functions don't have `this` as a special keyword. `this` in arrow functions is going to look up the lexical scope like any other variable.
