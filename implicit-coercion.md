## Implicit Coercion

Implicit: happens as a side effect of some other operations

### string <--> number

```
var foo = "123";
var baz = foo - 0;
baz;                 // 123

baz = foo - "0";
baz;                 // 123

baz = foo / 1;
baz;                 // 123

baz = 456;
foo = baz + "";
foo;                 // "456"

foo = baz - "";
foo;                 // 456 ... WAT!?
```

The `-` operator (as well as `/`, `*` and `%`) is specifically designed to only do math. If you give it something that is not already a number it's gonna call the `ToNumber` abstract operation and produce the number equivalent.

The `+` operator is overloaded and says if either one of my operants is already a string prefer string concatenation, otherwise do numeric addition.

### \* --> boolean

```
var foo = "123";
if(foo) {                 // yup
  alert("Sure.");
}

foo = 0;
if(foo) {                 // nope
  alert("Right.");
}
if(foo == false) {        // yup
  alert("Yeah.");
}

var baz = foo || "foo";
baz;                      // "foo"
```

**Explanation of `foo == false` returning true**  
`==` Prefers to compare numbers. So what is actually happening under the hood is that `ToNumber` abstract operation is invoked to `false` and it returns `0`.  
So after that `0 == 0` happens.

The `||` and `&&` are called **logical operators** so in their original design they produced a logical value (true or false).  
This is not how these operators work in Javascript (or Python, or Ruby).  
The `||` and `&&` are more like **selection operators**. They take two operants, they do a boolean coercion test against the first one and based on the result pick one of the two.

```
var foo = "123";
if(foo == true) {       // nope!
  alert("WAT!?");
}

foo = [];
if(foo) {               // yup
  alert("Sure.");
}
if (foo == false) {     // yup!
  alert("WAT!?");
}
```

`==` prefers to compare numbers like we said, so it invokes the `ToNumber` abstract operation to both `foo` and `true` and then it does `NaN == 1`.

`foo == false` returns `true` on the last example because again `ToNumber` abstract operation is invoked to both `[]` and `false`, so the comparison is `0 == 0`.

Ask yourself

1. Can either value be `true` or `false`?
2. Can either value ever be `[]`, `""`, or `0`?

In these cases I would suggest using `===` instead of `==`.

### Primitive <--> Native

```
var foo = "123";
foo.length;               // 3

foo.charAt(2);            // 3

foo = new String("123");
var baz = foo + "";
typeof baz;               // "string"
```

### Coercive Equality `==` vs `===`

First of all let's have a look at the specs:

> 7.2.13 Abstract Equality Comparison
>
> The comparison x == y, where x and y are values, produces true or false. Such a comparison is performed as follows:
>
> 1. If Type(x) is the same as Type(y), then
>    a. Return the result of performing Strict Equality Comparison x === y.
> 2. If x is null and y is undefined, return true.
> 3. If x is undefined and y is null, return true.
> 4. If Type(x) is Number and Type(y) is String, return the result of the comparison x == ToNumber(y).
> 5. If Type(x) is String and Type(y) is Number, return the result of the comparison ToNumber(x) == y.
> 6. If Type(x) is Boolean, return the result of the comparison ToNumber(x) == y.
> 7. If Type(y) is Boolean, return the result of the comparison x == ToNumber(y).
> 8. If Type(x) is either String, Number, or Symbol and Type(y) is Object, return the result of the comparison x == ToPrimitive(y).
> 9. If Type(x) is Object and Type(y) is either String, Number, or Symbol, return the result of the comparison ToPrimitive(x) == y.
> 10. Return false.

So:

~~`==` checks value~~  
~~`===` checks value and type~~

== allows coercion  
=== disallows coercion

```
var foo = [];
var baz = "";
if(foo == baz) {        // yup
  alert("Doh!");
}
if(foo === baz) {       // nope
  alert("Phew!");
}

foo = 0;
if(foo == "") {         // yup
  alert("Argh.");
}
if(foo === "") {        // nope
  alert("Phew.");
}
```

BUT `==` can help in various situations

```
var foo = "3";
if (foo === 3 || foo === "3") {               // yup
  alert("Thanks, but...");
}

if (foo == 3) {                               // yup
  alert("This is nicer!");
}

if (typeof foo === "string") {                // yup
  alert("typeof always returns a string");
}
```

What about the performance of `==` or `===`?

Since the difference between them is that `==` allows coercion and `===` disallows coercion it seems that `==` is less performant than `===`.  
If the types are the same though, `==` behaves exactly like `===` as we see in "Abstract Equality Comparison" in point 1.

```
var x = 2;
var y = 2;
var z = "2";

x == y;
x == z;         // slower

x === y;
x === z;        // same
```

`===` is ~30% faster than `==`, but if we decide to only use `===` we'll have to replace almost every `==` operation with two `===` operations (aka slower than one `==`).
