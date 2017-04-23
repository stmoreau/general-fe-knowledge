## this

Every function (except arrow functions), while executing, has a reference to its current execution context, called `this`.

> The only thing that matters is __how__ the function was called

__Ask these questions in this order, and stop when the first rule applies.__

1. Is the function called with `new` (__new binding__)? If so, `this` is the newly constructed object.  
`var bar = new foo()`

2. Is the function called with `call` or `apply` (__explicit binding__), even hidden inside a `bind` *hard binding*? If so, `this` is the explicitly specified object.  
`var bar = foo.call( obj2 )`

3. Is the function called with a context (__implicit binding__), otherwise known as an owning or containing object? If so, `this` is that context object.  
`var bar = obj1.foo()`

4. Otherwise, default the `this` (default binding). If in `strict mode`, pick `undefined`, otherwise pick the `global` object.  
`var bar = foo()`


Be careful of accidental/unintentional invoking of the *default binding* rule. In cases where you want to "safely" ignore a `this` binding, a "DMZ" object like `ø = Object.create(null)` is a good placeholder value that protects the `global` object from unintended side-effects.

Instead of the four standard binding rules, ES6 arrow-functions use lexical scoping for `this` binding, which means they adopt the `this` binding (whatever it is) from its enclosing function call. They are essentially a syntactic replacement of `self = this` in pre-ES6 coding.


__Note__  
The four things that the `new` keyword actually does when we put it in front of a function call.
1. It creates a brand new empty object out of thin air
2. That newly created object gets linked to another object
3. That newly created object gets passed in as as the `this` context to the function call
4. If that function does not already `return` its own object the `new` keyword assumes that you meant to return that object it was passed in
