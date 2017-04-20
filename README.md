# Advanced Javascript (from my point of view)

In this markdown I am gonna be throwing interesting information about Javascript that I experience / read.

So, first of all something very important is that the web console, node etc. are JavaScript-like. They are not behaving as the core Javascript spec expects. The only way to do that is to write Javascript on an empty file and run it on the browser!

## Primitive Types

In a statically typed language (C++, Java) we refer to a type as a description for what can go in a variable.
In dynamic languages (Javascript) we think of types as __value-types__ instead of ~~container-types~~.

So a pragmatic definition of Primitive Type (which is mentioned in the JS spec for the non-believers of its existence in Javascript) could be the following: *the set of intrinsic behaviours that we can expect, given any particular realm*.

__Primitive types__
1. __undefined__ (it is not the same with “not defined”. Not defined in JS means not declared. undefined means the variable exists but doesn’t have any value at the moment)
2. __string__
3. __number__
4. __boolean__
5. __object__
6. __symbol__ (new in ECMAScript 6)
7. __function__ (not in the specs, not a real first class primitive type. It is actually a subset of the object type, mentioned as *callable object*)
8. __null__ (not in the specs, definitely true that null is a primitive type. The fact that ` typeof null; // “object” ` is a bug admitted by Brendan Eich creator of the Javascript language several times. Bad thing is it cannot be fixed)

__Primitive types: special values__
1. __NaN__
2. __Infinity, -Infinity__
3. __null__
4. __undefined (void)__
5. __+0, -0__

Let's have a look at **NaN**.  
Supposedly NaN stands for “Not a Number”. Any time you try to take a value and convert it to a number and that conversion fails the resultant value is to tell you “this was an invalid number”.  
Whatever operation you try to do with NaN, NaN is going to come out.  
`typeof NaN; // “number”`  
`NaN === NaN; // false` (NaN is never equal to its self)  
So to check if a value is NaN we have the function isNaN:  
`isNaN(NaN); // true`  
But,  
`isNaN("foo”); // true` this is a bug because if you pass something that is not already a number to isNaN it is trying to convert this value to a number first and then test to see if it resulted into NaN. So by the time isNaN checks the value “foo” is already NaN. Fatal flaw!  
To fix that bug we can use the following:
```
if (!Number.isNaN) {
	Number.isNaN = function isNaN(num){
		return num != num;
	}
}
```

Let's have a look at **+0 and -0** now.  
`var foo = 0 / -3;`  
`foo === -0; // true`  
`foo === 0; // true`  
`0 === -0; // true`  
`(0/-3) === (0/3); // true`  
`foo; // 0`  
There are no negative literals in JS.  
JS parses “negative literals” as: the literal, then it’s operated on the unary negate - operator.  

The explanation of `0 === -0; // true` from the JS specs is:
```
The comparison x === y, where x and y are values, produces true or false. Such a comparison is performed as follows:

If Type(x) is Number, then
    ....
    - If x is +0 and y is −0, return true.
    - If x is −0 and y is +0, return true.
    ...
```

A *Reliable check for Negative Zero* is the following:

```
function isNeg0(x) {
	return x===0 && (1/x)===-Infinity;
}

isNeg0(0 / -3); // true
isNeg0(0 / 3); // false
```
