## Scope

Scope means where to look for things (the set of rules that helps us figure out where stuff is found)

Scope is a compiletime process.

The program goes through a compile step and it is at the compile step that all the scope decisions will happen.  
We like to think of it as a runtime thing but it is not that way.  
Refer to [Javascript is a compiled language](javascript-is-a-compiled-language.md).

### Javascript has almost only function scope

```
var foo = "bar";

function bar() {
  var foo = "baz";
}

function baz(foo) {
  foo = "bam";
  bam = "yay";
}
```

The fact that we use the same name for a variable in the global scope and inside a function is called __shadowing__.  
One fact we have to remember about shadowing is that you cannot access the one above except if it's the global scope where we can do `window.foo;`

- In the global scope we have `foo`, `bar`, `baz` and `bam`.  
`bam` is in the global scope because since a `bam` variable is not formally declared in the scope of `baz` we have to go up one level (global scope) and if it is not formally declared there (which is not), go up again, but we can't because global is the last scope so if it doesn't exist javascript creates this variable `bam` for us.  
- In the `bar` scope we have `foo` because it is formally declared in the function.  
- In the `baz` scope we have `foo` because it is formally declared in the `baz` function, passed as a parameter.

__TIP__  
Always in your javascript files use `"use strict";`
