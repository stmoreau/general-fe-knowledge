## Javascript is a compiled language

Javascript is a ~~interpreted~~ compiled language.

When people say javascript is not a compiled language, it's a dynamic interpreted language and they compare it to C++, or Java what they 're usually thinking of is the distribution model for the end result of the compilation.  
They're usually thinking that the compiled language, I run it through a compiler and I produce some executable code on the outside and then I take that executable code and I distribute it.

One of the **many** ways to prove that Javascript is a compiled language:

Every Javascript developer has had a Javascript bug...  
Some of these where syntactic errors (forgot a comma, left of a curly brace).  
In that scenario did you ever think why even that bug was on line 10, but when you went to run the program line it did not run lines 1-9 first and then give the error on line 10.  
When did it give the error? Before it even run line 1.  
The Javascript engine compiled the code first and the compilation validated the syntax long before it ever handed off to some part of the engine to execute!!

If you cannot recall such a situation go ahead and open the following HTML in your browser and open the console.

```
<!DOCTYPE html>
<html>
<head>
	<title>Javascript is a compiled language</title>
</head>
<body>

<script type="text/javascript">
	console.log("Hello World!");
	console.log("Hello World!");
	console.log("Hello World!");
	console.log("Hello World!");
	console.log("Hello World!");
	console.log("Hello World!");
	console.log("Hello World!");
	console.log("Hello World!");
	console.log("Hello World!");
	console.log("Hello World!);
</script>

</body>
</html>
```

The last `console.log("Hello World!);` is missing the ending `"` but if Javascript was a interpreted language all the previous `console.log("Hello World!");` should be in the console. Instead we only see `Uncaught SyntaxError: Invalid or unexpected token`.

Another way of proving is by just opening the source code of V8, or Mozilla Spidermonkey.
If we watch closely we'll see that there is a compiler in both of them.
