## Explicit Coercion

Explicit: it's obvious from the code that you're doing it

### string <--> number
```
var foo = "123";
var baz = parseInt(foo,10);
baz;                        // 123

baz = Number(foo);
baz;                        // 123

baz = +foo;                 // explicit?
baz;                        // 123

baz = 456;
foo = baz.toString();
foo;                        // "456"

foo = String(baz);
foo;                        // "456"
```

`parseInt(string,radix)` goes parses the string and as soon as it finds a character that doesn't exist in base of radix it stops so for example `parseInt('15px', 10); // 15`. It stops when it finds `p` because it's not a character in base10 and returns `15`.

`parseInt` was not created for coercion. So don't use `parseInt` for coercion and the opposite.

`+foo` does exactly the same with `Number(foo)` under the hood. The only difference is that even though we find way more often `+foo` in open source projects etc. it is not communicating very well the explicit coercion so I think it's better to use `Number(foo)` since anyone seeing the code for the first time can understand what this line is supposed to do.

### * --> boolean
```
var foo = "123";
var baz = Boolean(foo);
baz;                        // true

baz = !!foo;
baz;                        // true

// explicitly implicit
baz = foo ? true : false;
baz;                        // true
```

`Boolean(foo);` in my opinion communicates better the explicit coercion we are aiming for.

`!!` explanation:  
The first `!` (right one) if the value is not already a boolean it invokes the ToBoolean operation and it's going to produce a real boolean. Then it's going to negate it.  
Then the other `!` negates it again to "undo" the first negation.

__TIP__  
If you want to check if a character is inside a value a good way is this one:  
```
var foo = "foo";
// ~N -> -(N+1)
if(~foo.indexOf("f")) {
  alert("found it!");
}
```
