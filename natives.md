## Natives

Natives are: String, Number, Boolean, Function, Object, Array, RegExp, Date, Error etc.

I don't think these are ~~Native Types~~, nor ~~Native Objects~~ (not really appropriate), nor ~~Native Constructors~~ (we almost never want to call them with the `new` in front), but maybe they should be called **Native Functions**.

**As a rule prefer literal expressions!**

When we use Natives as Constructors they basically create an object around the value, so `new String('foo')` returns

```
String0: "f"1: "o"2: "o"length: 3__proto__: String[[PrimitiveValue]]: "foo"
```

This can be a problem because for example: 0 as a primitive value is falsy, 0 as a number object is truthy.

Don't do `foo = new Array(1,2,3);`, do `foo = [1,2,3];`  
Don't do `foo = new Object(); foo.a = 1; foo.b = 2; foo.c = 3;` do `foo = { a:1, b:2, c:3 };`

For RegExp prefer literal expression when possible `foo = /a*b/g;` but if you have to dynamically create that expression it's fine to use the Constructor form `new RegExp('a*b','g');`

There is no date literal! So we have to use `foo = new Date();`. Most of the times we use `new Date()` because we want to get the current timestamp. There is a much better way to do that and this is `Date.now()`.
