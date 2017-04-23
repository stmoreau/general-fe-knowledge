## Modules

There are two characteristics implicit in this definition of modules and __both of these characteristics need to be present for you to be using the module pattern__.  
- The first characteristic is that there has to be an outer enclosing function that runs at least once.
- There needs to be at least one internal function that returns back in the public API that has closure over the internal state.

Benefits:
- Encapsulation (hiding) of things we don't want to expose
- organizing your code

Downsides:
- Testability (how are you going to do function testing?)

### What's not a module

```
var foo = {
  o: { bar: "bar" },
  bar() {
    console.log(this.o.bar);
  }
};

foo.bar();      // "bar"
```
So everyone has access to `foo.o`.

### Classic module pattern

```
var foo = (function() {
  var o = { bar: "bar" };

  return {
    bar: function() {
      console.log(o.bar);
    }
  };
})();

foo.bar();      // "bar"
```
In this way `o` cannot be accessed outside of the function.

### Classic module pattern: modified

With this way we gain the benefit that we can access our "public API" internally.

```
var foo = (function() {
  var publicAPI = {
    bar: function() {
      publicAPI.baz();
    },
    baz: function() {
      console.log("baz");
    }
  };
  return publicAPI;
})();

foo.bar();      // "baz"
```

### Modern module pattern

```
define("foo", function(){
  var o = { bar: "bar" };

  return {
    bar: function(){
      console.log(o.bar);
    }
  };
});
```

### ES6+ module pattern

foo.js
```
var o = { bar: "bar" };

export function bar() {
  return o.bar;
};
```
```
import { bar } from "foo.js";

bar();      // "bar"

import * as foo from "foo.js";

foo.bar();  //"bar"
```
