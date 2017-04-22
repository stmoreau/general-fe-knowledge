## Anonymous and Named Function Expressions

```
var clickHandler = function(){
  // ...
}

var keykHandler = function keykHandler(){
  // ...
}
```

The first function is called __anonymous function expression__  
The second function is called __named function expression__

You should always use __named function expression__ and there are three reasons for that:
1. Handy function self-reference (e.g. recursion)
2. More debuggable stack traces
3. More self-documenting code
