## Coercion

Abstract operations (e.g. ToString)

__ToString__ examples
```
            null  "null"
       undefined  "undefined"
            true  "true"
           false  "false"
         3.14159  "3.14159"
               0  "0"
              -0  "0"

              []  ""
         [1,2,3]  "1,2,3"
[null,undefined]  ","
 [[[],[],[]],[]]  ",,,"
          [,,,,]  ",,,"

              {}  "[object Object]"
           {a:2}  "[object Object]"
```

__Aside__  
Javascript spec: `Edition 5 clarifies the fact that a trailing comma at the end of an ArrayInitialiser does not add to the length of the array`

__ToNumber__ examples
```
              ""  0
             "0"  0
            "-0"  -0
         " 009 "  9
       "3.14159"  3.14159
            "0."  0
            ".0"  0
             "."  NaN
          "0xaf"  175

           false  0
            true  1
            null  0
       undefined  NaN

ToNumber(object)  ToPrimitive(number)

            [""]  0
           ["0"]  0
          ["-0"]  -0
          [null]  0
     [undefined]  0
         [1,2,3]  NaN
        [[[[]]]]  0

```

Falsy : if you have a value and you dispatch the ToBoolean operation on it, it will always produce false  
examples and __only__ falsy values ("", 0, +0, -0, null, NaN, false, undefined)

Truthy : something is a truthy value if it's not on the Falsy list

__These rules only apply if the `ToBoolean` operation is invoked!__
