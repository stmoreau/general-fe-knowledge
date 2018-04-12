## Anonymous and Named Function Expressions

```
var clickHandler = function(){
  // ...
}

var keykHandler = function keykHandler(){
  // ...
}
```

The first function is called **anonymous function expression**  
The second function is called **named function expression**

You should always use **named function expression** and there are three reasons for that:

1. Handy function self-reference (e.g. recursion)
2. More debuggable stack traces
3. More self-documenting code
