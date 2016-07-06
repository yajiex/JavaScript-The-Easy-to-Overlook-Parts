# JavaScript: The XX part for me

## JavaScript in HTML

1. A `<script>` element using the `src` attribute should not include additional JavaScript code between the `<script>` and `</script>` tags. If both are provided, the script file is downloaded and executed while the inline code is ignored
2. Both `defer` and `async` attributes apply only to external scripts and scripts will begin to download immediately without pausing HTML parsing.
    - Without any attributes: HTML parsing will pause, the script will be fetched and executed before the parsing is resumed.
    - `async`: scripts are guaranteed to execute before `load`, scripts are not guaranteed to execute in the order in which they are specified, 
    - `defer`: scripts will be executed in the order in which they appear, scripts execute after HTML Parsing finishes but before `DOMContentLoaded`
3. Content contained in `<noscript>` will be displayed either the browser doesn't support scripting or scripting support is turned off.

## Grammar

1. The first character of identifiers could be a dollar sign (`$`). Letters in an identifier may include extended ASCII or Unicode letter characters such as `À` and `Æ`.
2. The `for-in` is used to enumerate the properties of an object, the order in which property names are returned cannot necessarily be predicted.
3. It's possible to `label` statements for later use
4. The `switch` statement compares values using the identically equal operators(`===`), so no type coercion occurs.

### Operator

1. Rules for increment(`++`) and decrement(`--`) operators:
     - When used on a string that is a valid representation of a number, convert to a number and apply the change. The variable is changed from a string to a number.
     - When used on a string that is not a valid number, the variable's value is set to `NaN`. The variable is changed from a string to a number.
2.  When the unary plus(`+`) is applied to a nonnumeric value, it performs the same conversion as the `Number()` casting function.
3. All numbers in ECMAScript are stored in IEEE-754 64-bit format, but the bitwise operations don't work directly on the 64-bit representations. Instead, the value is converted into a 32-bit integer, the operation takes place, and the result is converted back into 64 bits.
4. `NaN` and `Infinity` are treated as equivalent to 0 when used in bitwise operations.
5. Bitwise NOT: negates the number and substracts 1.
6. Left shift preserves the sign of the number it's operating on. `-2 << 5` => `-64`
7. ECMAScript fills empty bits produced by signed right shift with the value in the sign bit to create a complete number, while fills them with zeros when unsigned right shifting.
8. The unsigned-right-shift operator considers the binary representation of the negative number to be representative of a positive number instead. Negative number is the two's complement of its absolute value.
9. Logical AND(`&`) rules:
     - If the first operand is an object, then the second operand is always returned.
     - If the second operand is an object, then the object is returned only if the first operand evaluates to `true`.
     - If both operands are objects, then the second operand is returned.
10. Multiplicative operators(`* /`) rules:
      - `Infinity * 0` => `NaN`
      - `Infinity/Infinity` => `NaN`
      - If `Infinity` is divided by any nonzero number, the result is either `Infinity` or `-Infinity`, depending on the sign of the second operand.
11. Modulus(`%`) rules
      - If the dividend is an infinite number and the divisor is a finite number, the result is `NaN`
      - If the dividend is a finite number and the divisor is 0, the result is `NaN`
      - `Infinity%Infinity` => `NaN`
      - If the dividend is a finite number and the divisor is an infinite number, then the result is the dividend
12. Additive operators(`+ -`) rules
      - `Infinity + (-Infinity)` => `NaN`
      - `(+0) + (-0)` => `+0`
13. Relational operators rules
      - If two operands are strings, compare the character codes of each corresponding character in the string
      - If one operand is a number, convert the other operand to a number and perform a numeric comparison
      - The result of any relational operation with `NaN` is `false`
14. Equal operators rules
      - If an operand is a Boolean value, convert it into a numeric value before checking for equality. `false` => `0`, `true` => `1`, `true == 2` => `false`
      - `null == undefined` => `true`, `null === undefined` => `false`
      - Values of `null` and `undefined` cannot be converted into any other values for equality checking, `undefined == 0` => `false`
      - If either operand is `NaN`, the equal operator returns `false` and the not-equal operator returns `true`
      - If both operands are objects, then they are compared to see if they point to the same object

### Type

1. Five primitive types: `Undefined, Null, Boolean, Number, String`, they can't have properties added to them; One complex type: `Object`
     - When a primitive value is assigned from one variable to another, the value stored on the variable object is created and copied into the location for the new variable. These values are completely separated.
     - When a reference value is assigned from one variable to another, two variables point to exactly the same object, so changes to one are reflected on the other.
     
2. Referring undeclared variable will cause an error. Only `typeof` can be called on an undeclared variable. The `typeof` operator will both return `undefined` when called on uninitialized or undeclared variable.
3. `typeof null` will return `"object"`, as `null` is considered to be an empty object reference
4. `typeof` works well for primitive values, while `instanceof` is used for reference type. If `instanceof` is used with a primitive value, it will always return `false`, because primitives aren't objects.
    
#### Boolean

1. Any nonzero number (including `infinity`) => true, `0, NaN` => `false`
2. Any nonempty string => `true`, ""(empty string) => `false`
3. Any object => `true`
4. `!!` => `Boolean()`
6. 

#### Number

1. Any negative number that can't be represented is `-Infinity`, and any positive number that can't be represented is `Infinity`. If a calculation returns either positive or negative `Infinity`, that value cannot be used in any further calculations. To determine if a value is finite, use `isFinite()` function.
2. Any operation involving `NaN` always returns `NaN`, `NaN` is not equal to any value, including `NaN`
3. `isNaN()` is used to determine if the value is "not a number", it will attempt to convert argument into a number. `isNaN` can be applied to objects. The object's `valueOf()` method is first called to determine if the returned value can be converted into a number. If not, the `toString()` method is called.
4. `Number.MIN_VALUE` => `5e-324`, `Number.MAX_VALUE` => `1.7976931348623157e+308`
5. `Number.NEGATIVE_INFINITY` => `-Infinity`, `Number.POSITIVE_INFINITY` => `Infinity`
6. `0/0` => `NaN`, `1/0` => `Infinity`, `(-1)/0` => `-Infinity`
7. `Number` function conversion rules:
     - When applied to `null`, `Number()` returns `0`
     - When applied to `undefined`, `Number()` returns `NaN`
     - `011` => `11` (leading zeros are ignored)
     - When applied to objects, the `valueOf` method is called and the returned value is converted based on the previously described rules. If that conversion results in `NaN`, the `toString()` method is called and the rules for converting strings are applied.
8. `ParseInt` conversion rules:
     - `parseInt("1234blue")` => `1234`
     - `parseInt("")` => `NaN`
     - `parseInt("070")` => `70` (ECMAScript 5)
9. `parseFloat()` parses only decimal values. If the string represents a whole number (no decimal point or only a zero after the decimal point), `parseFloat()` returns an integer. `parseFloat("1234blue")` => `1234`
10. When outputting a negative number as a binary string, you get the binary code of the absolute value preceded by a minus sign, `-18.toString(2)` => `"-10010"`
11. By default, all integers are represented as singed in ECMAScript.


#### String

1. Character literals such as `\n` `\unnnn` will be interpreted as if they were a single character.
2. `toString()` is not available for `null` and `undefined`.
3. `String(null)` => `"null"`, `String(undefined)` => `"undefined"`

## Function

1. The values of `arguments` always stay in sync with the values of the corresponding named parameters. This doesn't mean that both access the same memory space, though; their memory spaces are separate but happen to be kept in sync. The length of the `arguments` object is set based on the number of arguments passed in, not the number of named arguments listed for the function.
2. All arguments in ECMAScript are passed by value, it's not possible to pass arguments by reference.


    