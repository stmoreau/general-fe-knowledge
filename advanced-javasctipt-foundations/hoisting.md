## Hoisting

Hoisting is a term you will not find in the JavaScript docs. Hoisting was **thought up** as a general way of thinking about how execution context (specifically the creation and execution phases) work in JavaScript. But, hoisting can lead to misunderstandings. For example, hoisting teaches that variable and function declarations are physically moved to the top of your coding, but this is not what happens at all. What does happen is that variable and function declarations are put into memory during the compile phase, but stays exactly where you typed it in your coding.

```js
a; // ???
b; // ???
var a = b;
var b = 2;
b; // 2
a; // ???
```

What happens in reality is the following:

* Compiler parses the code and finds two formally declared variables so it stores them
* Then on the second run javascript basically sees this code

```js
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

Example no2

```js
var a = b();
var c = d();
a; // ???
c; // ???

function b() {
  return c;
}

var d = function() {
  return b();
};
```

This block of code after compilation essentially becomes (not exactly, but has that behaviour):

```js
function b() {
  return c;
}
var a;
var c;
vad d;

a = b();
c = d();
a;
c;
d = function () {
  return b();
}
```

JavaScript only hoists declarations, not initializations. If a variable is declared and initialized after using it, the value will be undefined. For example:

```js
console.log(num); // Returns undefined
var num;
num = 6;
```

_Hoisting is adding your variable to the enclosing lexical scope._

There is a misconception that `let` doesn't hoist, but technically both `var` and `let` hoist.
Both `var` and `let` technically hoist, since they both add the variables to the enclosing lexical scope.
The difference between them is that `var` also initializes the variables defaulting to `undefined`, while `let` doesn't do that second part.
