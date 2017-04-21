## Coercion

Abstract operations (e.g. ToString)

ToString examples
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

ToNumber examples
