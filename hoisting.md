## Hoisting

Hoisting is a term you will not find in the JavaScript docs. Hoisting was **thought up** as a general way of thinking about how execution context (specifically the creation and execution phases) work in JavaScript. But, hoisting can lead to misunderstandings. For example, hoisting teaches that variable and function declarations are physically moved to the top of your coding, but this is not what happens at all. What does happen is that variable and function declarations are put into memory during the compile phase, but stays exactly where you typed it in your coding.

```
a;          // ???
b;          // ???
var a = b;
var b = 2;
b;          // 2
a;          // ???
```

What happens in reality is the following:

* Compiler parses the code and finds two formally declared variables so it stores them
* Then on the second run javascript basically sees this code

```
a;
b;
a = b;
b = 2;
b;
a;
```

So the value of the first `a` is `undefined` because it has been declared but has no value at the moment.  
The value of the first `b` is `undefined` because it has been declared but has no value at the moment.  
Then `a` gets the value of `b`, which is `undefined` and `b` get the value of `2`.  
So the second `b` obviously has the value `2`, but the `a` has still the value `undefined`.
