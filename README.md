# JavaScript: The Easy-to-Overlook Parts

## JavaScript Language 

### Grammar

1. The first character of identifiers could be a dollar sign (`$`). Letters in an identifier may include extended ASCII or Unicode letter characters such as `À` and `Æ`.
2. `first-name` is not a legal JavaScript name while `first_name` is.
3. The `for-in` is used to enumerate the properties of an object, the order in which property names are returned cannot necessarily be predicted. There is also the problem with unexpected properties being dredged up from the prototype chain.
4. It's possible to `label` statements for later use
5. The `switch` statement compares values using the identically equal operators(`===`), so no type coercion occurs.
6. JavaScript will never tell you if you've declared the same variable more than once; it simply ignores all subsequent declarations (though it will honor initializations).
7. Module Pattern:
     - It creates a new object
     - It optionally defines private instance variables and methods
     - It augments that new object with methods
     - It returns that new object
     
     Here is a pseudocode template:   
         
         var constructor = function (spec, my) {
             var that, other private instance variables;
             my = my || {};
             Add shared variables and functions to my
             that = a new object;
             Add privileged methods to that
             return that;
         };
         
         var mammal = function (spec) {
             var that = {};
             that.get_name = function ( ) {
                 return spec.name;
             };
             that.says = function ( ) {
                 return spec.saying || '';
             };
             return that;
         };
         var myMammal = mammal({name: 'Herb'});
8. `ninja = 5`, this statement returns `undefined`
9. The function context (`this`) is unaffected by `with` statement.
10. Unreferenced assignments that are not to an existing property on the `with` scope's object are made to the global context.
11. It's very important to understand that any return statements in either the `try` or the `catch` portion will be ignored if a `finally` clause is also included in your code.
12. When the `throw` operator is used, code execution stops immediately and continues only if a trycatch statement catches the value that was thrown.
13. An `onerror` event handler doesn't create an `event` object in any browser, instead, it receives three arguments: the error message, the URL on which the error occurred, and the line number.
14. Images also support an `error` event. Any time the URL in an image's src attribute doesn't return a recognized image format, the error event fires.

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
4. The `typeof` operator reports that the type of an `array` is `'object'`, which isn't very helpful.
5. `typeof` works well for primitive values, while `instanceof` is used for reference type. If `instanceof` is used with a primitive value, it will always return `false`, because primitives aren't objects.
6. Calling a primitive wrapper constructor using `new` is not the same as calling the casting function of the same name, for example:
         
        var value = "25";
        var number = Number(value);
        alert(typeof number); //"number"
         
        var obj = new Number(value);
        alert(typeof obj); //"object"    
7. A `Boolean` object is an instance of the `Boolean` type and will return `true` when used with the `instanceof` operator, whereas a primitive value returns `false`
8. The `instanceof` operator is problematic in that it's difficult to use when multiple global scopes are present, such as when there are multiple frames. The classic example of this problem is attempting to identify an object as an array using the following code: `var isArray = value instanceof Array;` This code returns `true` only if value is an array and was created in the same global scope as the `Array` constructor. (Remember, Array is a property of window.) If value is an array from another frame, this code returns false.
    
### Boolean

1. Any nonzero number (including `infinity`) => true, `0, NaN` => `false`
2. Any nonempty string => `true`, ""(empty string) => `false`
3. Any object => `true`
4. `!!` => `Boolean()`, the `!!` construct is a simple way of turning any JavaScript expression into its Boolean equivalent
5. 

### Number

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
12. `toFixed()` method returns a string representation of a number with a specified number of decimal points. If the number has more than the given number of decimal places, the result is rounded to the nearest decimal place.
13. `toExponential()` returns a string with the number formatted in exponential notation.
14. `toPrecision()` returns either the fixed or the exponential representation of a number, depending on which makes the most sense. This method takes on argument, which is the total number of digits to use to represent the number (not including exponents).


### String

1. Character literals such as `\n` `\unnnn` will be interpreted as if they were a single character.
2. `toString()` is not available for `null` and `undefined`.
3. `String(null)` => `"null"`, `String(undefined)` => `"undefined"`
4. Any time a string value is accessed in read mode, the following three steps occur:
     - Create an instance of the `String` type
     - Call the specified method on the instance
     - Destroy the instance
5. Automatically created primitive wrapper objects exist for only one line of code before they are destroyed. This means that properties and methods cannot be added at runtime. Take this for example:
             
        var s1 = "some test";
        s1.color = "red";
        alert(s1.color); //undefined
   `String` object that was created in the second line is destroyed by the time the third line is executed. The third line creates its own `String` object, which doesn't have the `color` property.
6. ECMAScript provides `replace()` method to simplify replacing substrings. If the first argument is a string, then only the first occurrence of the substring will be replaced. The only way to replace all instances of a substring is to provide a regular expression with the global flag specified.   

### Methods
1. `encodeURI()` does not encode special characters that are part of a URI, such as the colon(`:`), forward slash(`/`), question mark(`?`), and pound sign(`&`), whereas `encodeURIComponent()` encodes every nonstandard character it finds.
2. `Math.random()` returns a random number between 0(inclusive) and 1(exclusive) [0, 1)
3. For `eval()`, anything that isn't a simple variable, primitive, or assignment will need to be wrapped in parentheses in order for the correct value to be returned.

### Object

1. Data properties have four attributes describing their behavior:
     - `Configurable`: indicates if the property may be redefined by removing the property via `delete`, changing the property's attributes, or changing the property into an accessor property.
     - `Enumerable`: indicates if the property will be returned in a `for-in` loop.
     - `Writable`: indicates if the property's value can be changed.
     - `Value`: 
2. To change any of the default property attributes, use `Object.defineProperty()`; To change any of the default property attributes, use `Object.defineProperty()`; 
3. Once a property has been defined as nonconfigurable, it cannot become configurable again. Any attempt to call `Object.defineProperty()` and change any attribute other than `writable` causes an error.
4. `Object.getOwnPropertyDescriptor()`: retrieve the property descriptor for a given property, it works only on instance properties; to retrieve the descriptor of a prototype property, call `Object.getOwnPropertyDescriptor()` on the prototype object directly.
5. `isPrototypeOf()`: determine if this relationship exists between objects
6. `Object.getPrototypeOf()`: return the value of `Prototype`.
7. For `in` operator, when used on its own, the `in` operator returns `true` when a property of the given name is accessible by the object, which is to say that the property may exist on the instance or on the prototype.
8. `Object.keys()`: return an array of strings containing the names of all enumerable properties
9. `Object.getOwnPropertyNames()`: return all instance properties, whether enumerable or not
10. Be aware that all instances will share the properties on the prototype, including reference values (like array).
11. JavaScript provides a method called `hasOwnProperty()`, which can be used to determine whether properties are actually defined on an object instance versus imported from a prototype.
12. The native `toString()` method of Object can be called with any value to return a string in the format `"[object NativeConstructorName]"`. Each object has an internal `[[Class]]` property that specifies the constructor name that is returned as part of this string.
13. `Object.preventExtensions()` => new properties and methods cannot be added to the object.
14. `Object.isExtensible()` => determine that an object can't have extensions
15. Sealed objects aren't extensible and existing object members have their `[[Configurable]]` attribute set to false. This means properties and methods can't be deleted as data properties cannot be changed to accessor properties or vice versa using `Object.defineProperty()`. Property values can still be changed. You can seal an object by using the `Object.seal()` method. You can determine if an object is sealed by using `Object.isSealed()`.
16. The strictest type of tamper-proof object is a frozen object. Frozen objects aren't extensible and are sealed, and also data properties have their `[[Writable]]` attribute set to false. Accessor properties may still be written to but only if a `[[Set]]` function has been defined. ECMAScript 5 defines `Object.freeze()` to allow freezing of objects.
17. There is also an `Object.isFrozen()` method to detect frozen objects

### Function

1. The last argument of a variable argument list to the `Function` constructor is always the code that will become the body of the function. Any preceding arguments represent he names of the parameters for the function. No closures are created when functions are created via the `Function` constructor.
1. The values of `arguments` always stay in sync with the values of the corresponding named parameters. This doesn't mean that both access the same memory space, though; their memory spaces are separate but happen to be kept in sync.
2. Both `arguments` and `function` have a `length` property
    - The `length` of the `arguments` object is set based on the number of arguments passed in
    - The `length` of function indicates the number of named arguments that the function expects.
3. All arguments in ECMAScript are passed by value, it's not possible to pass arguments by reference.
4. `arguments` object has `callee` and `caller` properties:
    - `callee`: a pointer to the function that owns the arguments object.
    - `caller`: results in an error in strict mode and is always undefined outside of strict mode. This is to clear up confusion between `arguments.caller` and the `caller` property of functions.
5. Because functions are objects, function names are simply pointers to function objects. So the global `sayHello()` function and `o.sayHello()`point to the same function event though they execute in different contexts.
6. Function declarations are read and available in an execution context before any code is executed, whereas function expressions aren't complete until the execution reaches that line of code. As the code is being evaluated, the JavaScript engine does a first pass for function declarations and pulls them to the top of the source tree. So even though the function declaration appears after its usage in the actual source code, the engine changes this to boist the function declarations to the top.
7. ECMAScript 5 formalizes an additional property on a function object: `caller`, it contains a reference to the function that called this function or `null` of the function was called from the global scope.
8. All functions have a property named `name` that stores the function's name as a string. Functions with no name still possess this property, set to the empty string. Please be aware in the following sample, the function `name` is still empty string.
         
        var shout = function() {};
9. Closures are functions that have access to variables from another function's scope. A `closure` is the scope created when a function is declared that allows the function to access and manipulate variables that are external to that function. A declared function can be called at any later time, even after the scope in which it was declared has gone away.
10. In JavaScript, variables are scoped based upon the `closure` they're in.
11. `closures` remember references to included variables — not just their values at the time at which they're created.
12. Anonymous functions are not bound to an object in `this` context, meaning the `this` object points to `window` unless executing in strict mode (where `this` is `undefined`). 
          
         var name = "The window";
         var object = {
             name: "My Object",
             getNameFunc: function() {
                 return function() {
                     return this.name;
                 };
             }
         };
         alert(object.getNameFunc()()); // "The window"
13. In the following example, because the value of the assignment expression is the function itself, the `this` value is not maintained, and so `The window` is returned.
          
         var name = "The window";
         var object = {
             name: "My object",
             getName: function() {
                 return this.name;
             }
         };
         (object.getName = object.getName)(); //"The window"
14. A function always returns a value. If the return value is not specified, then `undefined` is returned.
15. JavaScript sees the `function` keyword as the beginning of a function declaration, and function declarations cannot be followed by parentheses. Function expressions, however, can be followed by parentheses. So the following code causes errors:
          
         function() {
         }(); // error!
16. Every function object is created with a `prototype` property. Its value is an object with a `constructor` property whose value is the function. When a function object is created, the `Function` constructor that produces the function object runs some code like this: `this.prototype = {constructor: this};` The new function object is given a `prototype` property whose value is an object containing a `constructor` property whose value is the new function object.
17. In the following Constructor Pattern sample, `person1` and `person2` both have a `constructor` property that points back to `Person`. The major downside to constructors is that methods are created once for each instance.    
         
        function Person(name, age) {
            this.name = name;
            this.age = age;
        }
        var person1 = new Person("Nicholas", 29);
        var person2 = new Person("Greg", 27);
18. In the following Prototype Pattern sample, `Person.prototype` points to the prototype object but `Person.prototype.constructor` points back to `Person`.
         
        function Person() {}
        Person.prototype.name = "Nicholas";
        var person1 = new Person();
        person1.name = "Greg";
        delete person1.name;
        alert(person1.name); // Nicholas - from the prototype
      Once a property is added to the object instance, it shadows any properties of the same name on the prototype, which means that it blocks access to the property on the prototype without altering it. Setting the property to `null` only sets the property on the instance and doesn't restore the link to the prototype. The `delete` operator, however, completely removes the instance property and allows the `prototype` property to be accessed again.
19.  In the following example, the `constructor` property no longer points to `Person`. `constructor` property is equal to that of a completely new object (the `Object` constructor) instead of the function itself. Overwriting the prototype on the constructor means that new instances will reference the new prototype while any previously existing object instances still reference the old prototype.
         
        function Person(){}
        Person.prototype = {
            name: "Nicholas"
        };
20. The most common way of defining custom types is to combine the constructor and prototype patterns. The constructor pattern defines instance properties, whereas the prototype pattern defines methods and shared properties.
21. If the function was invoked with the `new` prefix and the return value is not an object, then `this` (the new object) is returned instead.
22. Instance members created inside a `constructor` will occlude properties of the same name defined in the `prototype`. Binding operations within the `constructor` always take precedence over those in the `prototype`.
23. The best technique for creating prototype chain is to use an instance of an `object` as the other object's prototype: `SubClass.prototype = new SuperClass();`. We advise strongly against to use the `Person` prototype object directly as the `Ninja` prototype, like this: `Ninja.prototype = Person.prototype;`. By doing this, any changes to the `Ninja` prototype will also change the `Person` prototype because they're the same object, and that's bound to have undesirable side effects.
24. The expression `this instanceof arguments.callee` will evaluate to `true` when executed within a constructor, but `false` when executed within a regular function.
25. Some languages offer the tail recursion optimization. This means that if a function returns the result of invoking itself recursively, then the invocation is replaced with a loop, which can significantly speed things up. Unfortunately, JavaScript does not currently provide tail recursion optimization. Functions that recurse very deeply can fail by exhausting the return stack
26. If we have methods return `this` instead of undefined, we can enable cascades.
27. Function currying creates functions that have one or more arguments already set (also called partial function application). 
     
        function curry(fn){
          var args = Array.prototype.slice.call(arguments, 1);
          return function(){
            var innerArgs = Array.prototype.slice.call(arguments),
            finalArgs = args.concat(innerArgs);
            return fn.apply(null, finalArgs);
          };
        }
28. Make use of function properties:
          
        var store = {
          nextId: 1,
          cache: {},
          add: function(fn) {
            if (!fn.id) {
              fn.id = store.nextId++;
              return !!(store.cache[fn.id] = fn);
            }
          }
        };
29. `Memoization` is the process of building a function that's capable of remembering its previously computed values.
          
        function isPrime(value) {
          if (!isPrime.anwers) isPrime.answers = {};
          if (isPrime.answers[value] != null) {
            return isPrime.answers[value];
          }
          var prime = value != 1; // 1 can never be prime
          for (var i = 2; i < value; i++) {
            if (value % i == 0) {
              prime = false;
              break;
            }
          }
          return isPrime.answers[value] = prime;
        }
30. Memorize DOM elements:
          
        function getElements(name) {
          if (!getElements.cache) getElements.cache = {};
          return getElements.cache[name] =
            getElements.cache[name] ||
            document.getElementsByTagName(name);
          }
31. A method-overloading function:
          
        function addMethod(object, name, fn) {
          var old = object[name];
          object[name] = function(){
            if (fn.length == arguments.length)
              return fn.apply(this, arguments)
            else if (typeof old == 'function')
              return old.apply(this, arguments);
          };
        }
32. A polyfill for `Function.prototype.bind`:
          
        Function.prototype.bind = function(){
            var fn = this,
                args = Array.prototype.slice.call(arguments), 
                object = args.shift();
            return function(){
                return fn.apply(object, args.concat(Array.prototype.slice.call(arguments)));
            };
        };   
33. A polyfill for `Function.prototype.partial`
          
        Function.prototype.partial = function() {
            var fn = this,
                args = Array.prototype.slice.call(arguments);
            return function() {
                var arg = 0;
                for (var i = 0; i < args.length && arg < arguments.length; i++) {
                    if (args[i] === undefined) {
                        args[i] = arguments[arg++];
                    }
                }
                return fn.apply(this, args);
            };
        };  
34. A polyfill for Function wrapping, which is a technique for encapsulating the logic of a function while overwriting it with new or extended functionality in a single step.
          
        function wrap(object, method, wrapper) {
            var fn = object[method];
            return object[method] = function() {
                return wrapper.apply(this, [fn.bind(this)].concat(
                    Array.prototype.slice.call(arguments)));
            };
        }
          
        if (Prototype.Browser.Opera) {
            wrap(Element.Methods, "readAttribute", function(original, elem, attr) {
                return attr == "title" ? elem.title : original(elem, attr);
            });
        }                                              
### Array

1. JavaScript doesn't have **real** kind of array, it just provides an object that has some array-like characteristics. Retrieval and updating of properties work the same as with objects, except that there is a special trick with integer property names.
2. Since JavaScript's arrays are really objects, the `delete` operator can be used to remove elements from an array. Unfortunately, that leaves a hole in the array. This is because the elements to the right of the deleted element retain their original names
3. JavaScript arrays have a `splice` method. It can do surgery on an array, deleting some number of elements and replacing them with other elements. Because every property after the deleted property must be removed and reinserted with a new key, this might not go quickly for large arrays.
4. `length` is not read-only. By setting the `length` property, you can easily remove items from or add item to the end of the array. If the `length` were set to a number greater than the number of items in the array, the new items would each get filled with the value of `undefined`. Making the `length` larger does not allocate more space for the array. Making the `length` smaller will cause all properties with a subscript that is greater than or equal to the new `length` to be deleted.
5. If you store an element with a subscript that is greater than or equal to the current `length`, the length will increase to contain the new element. There is no array bounds error
6. The `[]` postfix subscript operator converts its expression to a string using the expression's `toString` method if it has one.
7. Use `Array.isArray` to detect arrays.  A polyfill for accurately detecting array:
                                               
        var is_array = function (value) {
            return value && typeof value === 'object' && value.constructor === Array;
        };

### Regex

1. Fundamentals:
    - `[abc]`: signify that we want to match any of the characters `'a'`, `'b'`, or `'c'`. Note that even though this expression spans five characters, it matches only a single character in the candidate string.
    - `[^abc]`: any character but `'a'`, `'b'`, or `'c'`
    - `[a-m]`: all characters from `'a'` though `'m'` inclusive (and lexicographically) are included in the set.
    - The caret character (`^`), when used as the first character of the regex, anchors the match at the beginning of the string
    - The dollar sign (`$`) signifies that the pattern must appear at the end of the string
    - Predefined character class and character terms:
        - `\t` => Horizontal tab
        - `\b` => Backspace
        - `\v` => Vertical tab
        - `\f` => Form feed
        - `\r` => Carriage return
        - `\n` => Newline
        - `\cA : \cZ` => Control characters
        - `\x0000 : \xFFFF` => Unicode hexadecimal
        - `\x00 : \xFF` => ASCII hexadecimal
        - `.` => Any character, except for newline (\n)
        - `\d` => Any decimal digit; equivalent to [0-9]
        - `\D` => Any character but a decimal digit; equivalent to [^0-9]
        - `\w` => Any alphanumeric character including underscore; equivalent to `[A-Za-z0-9_]`
        - `\W` => Any character but alphanumeric and underscore characters; equivalent to `[^A-Za-z0-9_]`
        - `\s` => Any whitespace character (space, tab, form feed, and so on)
        - `\S` => Any character but a whitespace character
        - `\b` => A word boundary
        - `\B` => Not a word boundary (inside a word)
    - `/(ab)+/` matches one or more consecutive occurrences of the substring `ab`       
2. Three supported flags represent matching modes:
     - `g`: global mode
     - `i`: case-insensitive mode
     - `m`: multiline mode
3. All metacharacters must be double-escaped, such as `\n` (the `\` character, which is normally escaped in strings as `\\` becomes `\\\\` when used in a regular-expression string).
4. The inherited methods of `toLocaleString()` and `toString()` each return the literal representation of the regular expression, regardless of how it was created. The `valueOf()` method for a regular expression returns the regular expression itself.
5. The methods that work with regular expressions are `regexp.exec`, `regexp.test`, `string.match`, `string.replace`, `string.search`, and `string.split`.
6. The `(?:...)?` indicates an optional noncapturing group. It is usually better to use noncapturing groups instead of the less ugly capturing groups because capturing has a performance penalty.
7. A regexp choice contains one or more regexp sequences. It attempts to match each of the sequences in order. So: `"into".match(/in|int/)` matches the `in` in `into`. It wouldn't match `int` because the match of `in` was successful.
8. Repeated occurrences as follows, any of these repetition operators can be greedy or nongreedy. By default, they're greedy they will consume all the possible characters that comprise a match. Annotating the operator with a `?` character (an overload of the `?` operator), as in `a+?`, makes the operation nongreedy: it will consume only enough characters to make a match. For example, if we were matching against the string `aaa`, the regular expression `/a+/` would match all three a characters, whereas the nongreedy expression `/a+?/` would match only one a character, because a single a character is all that's needed to satisfy the `a+` term.
    - We can specify that a character is optional (in other words, can appear either once or not at all) by following it with `?`. For example, `/t?est/` matches both `test` and `est`.
    - If we want a character to appear one or many times, we use `+`, as in `/t+est/`, which matches `test`, `ttest`, and `tttest`, but not `est`.
    - If we want the character to appear zero or many times, `*` is used, as in `/t*est/`, which matches `test`, `ttest`, `tttest`, and `est`.
    - We can specify a fixed number of repetitions with the number of allowed repetitions between braces. For example, `/a{4}/` indicates a match on four consecutive `a` characters.
    - We can also specify a range for the repetition count by specifying the range with a comma separator. For example, `/a{4,10}/` matches any string of four through ten consecutive `a` characters.
    - The second value in a range can be omitted (but leaving the comma) to indicate an open-ended range. The regex `/a{4,}/` matches any string of four or more consecutive `a` characters.
9. Back Reference: An example could be `/^([dtn])a\1/`, which matches a string that starts with any of the `d`, `t`, or `n` characters, followed by an `a`, followed by whatever character matched the first capture. This latter point is important! This isn't the same as `/[dtn] a[dtn]/`. The character following the `a` can't be any of `d`, or `t`, or `n`, but must be whichever one of those triggered the match for the first character. As such, which character the `\1` will match can't be known until evaluation time.
10. `/<(\w+)>(.+)<\/\1>/` => matching XML-type markup elements.
11. Compiling a regex once and storing it in a variable for later reference can be an important optimization.
12. Each regex has a unique object representation: every time a regular expression is created (and thus compiled), a new regular expression object is created. This is unlike other primitive types (like string, number, and so on) because the result will always be unique.
13. The array returned by match always includes the entire match in the first index, and then each subsequent capture following.
14. Using a local regular expression (one without the global flag) with the String object's `match()` methods returns an array containing the entire matched string, along with any matched captures in the operation. But when we supply a global regular expression (one with the `g` flag included), `match()` returns something rather different. It's still an array of results, but in the case of a global regular expression, which matches all possibilities in the candidate string rather than just the first match, the array returned contains the global matches; captures within each match aren't returned in this case.
15. `exec()` can be repeatedly called against a regular expression, causing it to return the next matched set of information every time it's called.
16. There's a way to get capture references within the replace string of a call to the `replace()` method. Instead of using the backreference codes, we use the syntax of `$1`, `$2`, `$3`, up through each capture number. Here's an example of such usage:
      
        assert("fontFamily".replace(/([A-Z])/g, "-$1").toLowerCase() == "font-family", "Convert the camelCase into dashed notation.");
17. To allow us to indicate that a set of parentheses should not result in a capture, the regular expression syntax lets us put the notation `?:` immediately after the opening parenthesis. This is known as a passive subexpression. `var pattern = /((?:ninja-)+)sword/;` causes only the outer set of parentheses to create a capture. The inner parentheses have been converted to a passive subexpression.
18. `replace()` has the ability to provide a function as the replacement value rather than a fixed string. When the replacement value (the second argument) is a function, it's invoked for each match found (remember that a global search will match all instances of the pattern in the source string) with a variable list of parameter, the value returned from the function serves as the replacement value.
  - The full text of the match
  - The captures of the match, one parameter for each
  - The index of the match within the original string
  - The source string
19. Trimming a string:
  - `(str || "").replace(/^\s+|\s+$/g, "");`
  - `str.replace(/^\s\s*/, '').replace(/\s\s*$/, '');`
  - `var str = str.replace(/^\s\s*/, ''), ws = /\s/, i = str.length; while (ws.test(str.charAt(--i))); return str.slice(0, i + 1);`
20. Matching newlines:
  - `/[\S\s]*/`
  - `/(?:.|\s)*/`
21. Unicode: `/[\w\u0080-\uFFFF_-]+/`. Includes the entire range of Unicode characters in the match by creating a character class that includes the `\w` term, to match all the "normal" word characters, plus a range that spans the entire set of Unicode characters above character code 128 (hex 0x80). Starting at 128 gives us some high ASCII characters along with all Unicode characters. The astute among you might note that by adding the entire range of Unicode haracters above \u0080, we match not only alphabetic characters, but also all Unicode unctuation and other special characters (arrows, for example).
22. Escaped characters: `/^((\w+)|(\\.))+$/`, this regular expression allows any sequence composed of a sequence of word characters, a backslash followed by any character (even a backslash), or both

## JavaScript in HTML

1. A `<script>` element using the `src` attribute should not include additional JavaScript code between the `<script>` and `</script>` tags. If both are provided, the script file is downloaded and executed while the inline code is ignored
2. Both `defer` and `async` attributes apply only to external scripts and scripts will begin to download immediately without pausing HTML parsing.
    - Without any attributes: HTML parsing will pause, the script will be fetched and executed before the parsing is resumed.
    - `async`: scripts are guaranteed to execute before `load`, scripts are not guaranteed to execute in the order in which they are specified, 
    - `defer`: scripts will be executed in the order in which they appear, scripts execute after HTML Parsing finishes but before `DOMContentLoaded`
3. Content contained in `<noscript>` will be displayed either the browser doesn't support scripting or scripting support is turned off.
4. Browsers will ignore any `script` type that it doesn't understand. We can force the browser to completely ignore a `script` block (and use it for whatever nefarious purposes we want) by using a type value that's not standard
5. The `postMessage()` method accepts two arguments: a message and a string indicating the intended recipient origin. It is possible to allow posting to any origin by passing in `"*"` as the second argument to `postMessage()`, but this is not recommended.
6. A `message` event is fired on a window when an XDM (Cross-document messaging) message is received. The `event` object that is passed to an `onmessage` event handler has three important pieces of information:
  - `data` => The string data that was passed as the first argument to `postMessage()`.
  - `origin` => The origin of the document that sent the message
  - `source` => A proxy for the `window` object of the document that sent the message. This proxy object is used primarily to execute the `postMessage()` method on the window that sent the last message.
7. The `dragenter` event (similar to the `mouseover` event) fires as soon as the item is dragged over the drop target. Immediately after the `dragenter` event fires, the `dragover` event fires and continues to fire as the item is being dragged within the boundaries of the drop target. When the item is dragged outside of the drop target, `dragover` stops firing and the `dragleave` event is fired (similar to `mouseout`). If the dragged item is actually dropped on the target, the `drop` event fires instead of `dragleave`. The target of these events is the drop target element.
8. If you drag an element over something that doesn't allow a drop, the drop event will never fi re regardless of the user action. However, you can turn any element into a valid drop target by overriding the default behavior of both the `dragenter` and the `dragover` events.
9. The `dataTransfer` object has two primary methods: `getData()` and `setData()`.
10. The `dropEffect` property is used to tell the browser which type of drop behaviors are allowed. Each of these values causes a different cursor to be displayed when an item is dragged over the drop target. The `dropEffect` property is useless, unless you also set the `effectAllowed`. This property indicates which `dropEffect` is allowed for the dragged item. `dropEffect` property has the following four possible values:
  - `"none"` => A dragged item cannot be dropped here. This is the default value for everything except text boxes.
  - `"move"` => The dragged item should be moved to the drop target.
  - `"copy"` => The dragged item should be copied to the drop target.
  - `"link"` => Indicates that the drop target will navigate to the dragged item (but only if it is a URL).
11. `history.pushState()` method accepts three arguments: a `data` object, the title of the new state, and an optional relative URL. As soon as `pushState()` executes, the state information is pushed onto the history stack and the browser's address bar changes to reflect the new relative URL.
12. You can update the current state information by using `replaceState()` and passing in the same first two arguments as `pushState()`. Doing so does not create a new entry in history, it just overwrites the current state.
13. HTML5 defines a `navigator.onLine` property that is `true` when an Internet connection is available or `false` when it's not. 
14. HTML5 defines two events to better track when the network is available or not: `online` and `offline`. Each event is fired as the network status changes from online to offline or vice versa respectively.
15. The server sends a `Set-Cookie` HTTP header containing session information as part of any response to an HTTP request. Browsers store such session information and send it back to the server via the Cookie HTTP header for every request after that point
16. When a cookie is set, it is sent along with requests to the same domain from which it was created.
17. Cookies are made up of the following pieces of information stored by the browser:
  - `Name` => A unique name to identify the cookie. Cookie names are case-insensitive
  - `Value`
  - `Domain` => This value can include a subdomain (such as www.wrox.com) or exclude it (such as .wrox.com, which is valid for all subdomains of wrox .com). If not explicitly set, the domain is assumed to be the one from which the cookie was set.
  - `Path` => The path within the specified domain for which the cookie should be sent to the server
  - `Expiration` => By default, all cookies are deleted when the browse session ends; however, it's possible to set another time for the deletion. Cookies can be deleted immediately by setting an expiration date that has already occurred
  - `Secure flag` => When specified, the cookie information is sent to the server only if an SSL connection is used.
18. Setting `document.cookie` does not overwrite any cookies unless the name of the cookie being set is already in use.
19. There is also a type of cookie called `HTTP-only`. `HTTP-only` cookies can be set either from the browser or from the server but can be read only from the server, because JavaScript cannot get the value of `HTTP-only` cookies.
20. The `sessionStorage` object stores data only for a session, meaning that the data is stored until the browser is closed. This is the equivalent of a session cookie that disappears when the browser is closed. Data stored on `sessionStorage` persists across page refreshes and may also be available if the browser crashes and is restarted, depending on the browser vendor.
21. In order to access the same `localStorage` object, pages must be served from the same domain (subdomains aren't valid), using the same protocol, and on the same port.
22.  Most computer monitors refresh at a rate of 60Hz, which basically means there's a repaint 60 times per second. Most computer monitors refresh at a rate of 60Hz, which basically means there’s a repaint 60 times per second.
23. Each browser window, tab, or frame has its own code execution queue. This means that the timing of cross-frame or cross-window JavaScript calls may result in race conditions when code is executed synchronously.

## BOM

1. Global variables cannot be removed using the `delete` operator, while properties defined directly on `window` can. Attempting to access an undeclared variable throws an error, but it is possible to check for the existence of a potentially undeclared variable by looking on the `window` object.
2. The second argument of `setTimeout()` tells the JavaScript engine to add this task onto the queue after a set number of milliseconds. If the queue is empty, then that code is executed immediately; if the queue is not empty, the code must wait its turn. In the following example, the `setTimeout()` will always have at least a 10 ms delay after the previous callback execution (it may end up being more, but never less), whereas `setInterval()` will attempt to execute a callback every 10 ms regardless of when the last callback was executed.
      
        setTimeout(function repeatMe() {
          /* Some long block of code... */
          setTimeout(repeatMe, 10);
        }, 10);
        setInterval(function() {
          /* Some long block of code... */
        }, 10);
3. The browser will not queue up more than one instance of a specific `interval` handler. True intervals are rarely used in production environments because this time between the end of one interval and the beginning of the next is not necessarily guaranteed, and some intervals may be skipped. Using timeouts ensures that can't happen.
4. Timers are provided as part of the objects and methods that the web browser makes available. This means that if we choose to use JavaScript in a non-browser environment, it's very likely that timers may not exist
5. `setTimeout(callback, interval, arg1, arg2, arg3)` would cause arguments arg1, arg2, and arg3 to be passed to the timeout callback.

## DOM

1. Browsers will add properties to the `<form>` element for each of the input elements within the `form` that reference the element. If that `id` value just happens to be an already-used property of the `form` element, such as `action` or `submit`, those original properties are replaced by the new property.
2. Cases where `property` names and `attribute` names differ
      
        Attribute name => Property name
        for => htmlFor
        class => className
        readonly => readOnly
        maxlength => maxLength
        cellspacing => cellSpacing
        rowspan => rowSpan
        colspan => colSpan
        tabindex =>tabIndex
        cellpadding => cellPadding
        usemap => useMap
        frameborder => frameBorder
        contenteditable => contentEditable
3. In general, `property` access is faster than the corresponding DOM `attribute` methods
4. when accessing a `property` that references a URL (such as `href`, `src`, or `action`) the URL value is automatically converted from its original form into a full canonical URL.
5. The `offsetHeight` and `offsetWidth` properties provide a fairly reliable means to access the actual `height` and `width` of an element. But be aware that the values assigned to these two properties include the `padding` of the element.
6. Obtain non-hidden dimensions for hidden elements (`display: none`):
  - Change the `display` property to `block`.
  - Set `visibility` to `hidden`.
  - Set `position` to `absolute`.
  - Grab the dimension values.
  - Restore the changed properties.
7. CSS3 color formats:
  - keyword: Any of the recognized HTML color keywords (`red`, `green`, `maroon`, and so on), extended SVG color keywords (`bisque`, `chocolate`, `darkred`, and so on), or the keyword `transparent` (which is equivalent to `rgba(0,0,0,0)`—see below).
  - `#rgb`: Short hexadecimal RGB (`red`, `green`, `blue`) color values, where each portion is a value from 0 to f.
  - `#rrggbb`: Long hexadecimal RGB (`red`, `green`, `blue`) color values, where each portion is a value from 00 to ff.
  - `rgb(r, g, b)`: RGB notation where each value is a decimal value from 0 to 255, or 0% to 100%.
  - `rgba(r, g, b, a)`: RGB notation with the addition of an alpha channel. The alpha value ranges from 0.0 (transparent) to 1.0 (fully opaque).
  - `hsl(h, s, l)`: HSL notation where the values represent hue, saturation, and lightness. The hue value ranges from 0 to 360 (the angle on the color wheel), and saturation and lightness range from 0% to 100%.
  - `hsla(h, s, l, a)`: HSL notation with the addition of the alpha channel.
8. Every node has a `nodeType` property that indicates the type of node that it is.
9. `NodeList`, `NamedNodeMap` objects are actually queries being run against the DOM structure, so changes will be reflected in `NodeList` objects automatically.
10. The `ownerDocument` property is a pointer to the document node that represents the entire document.
11. If the node passed into `appendChild()` is already part of the document, it is removed from its previous location and placed at the new location.
12. The `cloneNode()` method doesn't copy JavaScript properties that you add to DOM nodes, such as event handlers. This method copies only attributes and, optionally, child nodes. Everything else is lost.
13. `documentElement` property always points to the `<html>` element in an HTML page.
14. `var doctype = document.doctype; // get reference to <!DOCTYPE>`
15. Changing the value of the `title` property does not change the `<title>` element at all.
16. `document.domain` can never be set to a domain that the URL doesn't contain. Pages from different subdomains can't communicate with one another via JavaScript because of cross-domain security restrictions. By setting `document.domain` in each page to the same value, the pages can access `JavaScript` objects from each other. A further restriction in the browser disallows tightening of the `domain` property once it has been loosened.
17. `HTMLCollection` object has an method `namedItem`, that lets you reference an item in the collection via its `name` attribute. You can also access named items by using bracket notation.
18. To retrieve all elements in the document, pass in `"*"` to `getElementsByTagName()`.
19. Special Collections:
  - `document.anchors` => Contains all `<a>` elements with a `name` attribute in the document.
  - `document.forms` => Contains all `<form>` elements in the document.
  - `document.images` => Contains all `<img>` elements in the document.
  - `document.links` => Contains all `<a>` elements with an `href` attribute in the document.
20. The `document.implementation` property is an object containing information and functionality tied directly to the browser's implementation of the DOM. `var hasXmlDom = document.implementation.hasFeature("XML", "1.0");`
21. Even though the following code looks correct, the closing `"</script>"` string is interpreted as matching the outermost `<script>` tag. To avoid this, you simply need to change the string as `"<\/script>"`
      
        <html>
        <head></head>
        <body>
          script type="text/javascript">
            document.write("<script></script>");
          </script>
        </body>
        </html>
22. If `document.write()` is called after the page has been completely loaded, the content overwrites the entire page. Neither `open()` nor `close()` is required to be used when `write()` or `writeln()` is used during the course of page loading.
23. Every HTML element `HTMLElement` has a property `dir`, indicates the direction of the language, `"ltr"` or `"rtl"`
24. When `normalize()` is called on a parent of two or more text nodes, those nodes are merged into one text node whose `nodeValue` is equal to the concatenation of the `nodeValue` properties of each text node.
25. The `splitText()` method splits a text node into two text nodes, separating the `nodeValue` at a given offset. The method returns the new text node, which has the same `parentNode` as the original.
26. `querySelectorAll` returns a static instance of `NodeList`, its underlying implementation acts as a snapshot of elements rather than a dynamic query that is constantly reexecuted against a document.
27. If multiple class names are specified for `getElementsByClassName()`, the order is considered unimportant.
28. HTML5 introduces a way to manipulate class names: `classList`, `add(value)`, `contains(value)`, `remove(value)`, `toggle(value)`
29. `document.activeElement` always contains a pointer to the DOM element that currently has focus. By default, `document.activeElement` is set to `document.body` when the document is first loaded. Before the document is fully loaded, `document.activeElement` is null. And `document.hasFocus()` returns a Boolean value indicating if the document has focus.
30. The `readyState` property for `document` has two possible values:
  1. `loading` => The document is loading
  2. `complete` => The document is completely loaded
31. When in standards mode, `document.compatMode` is equal to `CSS1Compat`; when in quirks mode, `document.compatMode` is `BackCompat`
32. The `charset` property indicates the actual character set being used by the document and by default this value is `"UTF-16"`. The `defaultCharset` property indicates what the default character set for the document should be based on default browser and system settings.
33. When a custom data attribute is defined, it can be accessed via the `dataset` property of the element.
34. `innerHTML` returns the HTML representing all of the child nodes, including elements, comments, and text nodes.
35. `outerHTML` returns the HTML of the element on which it is called, as well as its child nodes.
36. `insertAdjacentHTML()` accepts two arguments: the position in which to insert and the HTML text to insert, the first argument must be one of the following values:
  - `"beforebegin"` => Insert just before the element as a previous sibling
  - `"afterbegin"` => Insert just inside of the element as a new child or series of children before the first child
  - `"beforeend"` => Insert just inside of the element as a new child or series of children after the last child
  - `"afterend"` => Insert just after the element as a next sibling
37. Inserting a large amount of new HTML is more efficient through `innerHTML` than through multiple DOM operations to create nodes and assign relationships between them. This is because an HTML parser is created whenever a value is set to `innerHTML` (or `outerHTML`). This parser runs in browser-level code (often written in C++), which is must faster than JavaScript.
38. The `scrollIntoView()` method exists on all HTML elements and scrolls the browser window or container element so the element is visible in the viewport. If an argument of `true` is supplied or the argument is omitted, the window scrolls so that the top of the element is at the top of the viewport (if possible); otherwise, the element is scrolled so that it is fully visible in the viewport but may not be aligned at the top.
39. Force a particular document mode by using the `X-UA-Compatible` HTTP header or by using the `<meta>` tag equivalent: `<meta http-equiv="X-UA-Compatible" content="IE=IEVersion">`
40. You can determine the document mode for a given page using the `document.documentMode` property.
41. The `contains()` method is called on the ancestor node from which the search should begin and accepts a single argument, which is the suspected descendant node. If the node exists as a descendant of the root node, the method returns `true`; otherwise it returns `false`
42. `compareDocumentPosition()` could also determine node relationships, it returns a bitmask indicating the relationship.
43. Scrolling:
  - `scrollIntoViewIfNeeded(alignCenter)` => Scrolls the browser window or container element so that the element is visible in the viewport only if it's not already visible; if the element is already visible in the viewport, this method does nothing. The optional `alignCenter` argument will attempt to place the element in the center of the viewport if set to `true`
  - `scrollByLines(lineCount)`
  - `scrollByPages(pageCount)` 
44. Namespace are specified using the `xmlns` attribute. You can explicitly create a prefix for an XML namespace using `xmlns`, followed by a colon, followed by the prefix.
45. The `Node` type evolves in DOM Level 2 to include the following namespace-specific properties:
  - `localName` => The node name without the namespace prefix
  - `namespaceURI` => The namespace URI of the code or `null` if not specified
  - `prefix` => The namespace prefix or `null` if not specified
46. DOM Level 3 goes one step further and introduces the following methods to work with namespaces:
  - `isDefaultNamespace(namespaceURI)` => Returns `true` when the specified `namespaceURI` is the default namespace for the node
  - `lookupNamespaceURI(prefix)` => Returns the namespace URI for the given `prefix`
  - `lookupPrefix(namespaceURI)` => Returns the prefix for the given `namespaceURI`
47. The `Document` type is changed in DOM Level 2 to include the following namespace-specific methods:
  - `createElementNS(namespaceURI, tagName)` => Creates a new element with the given `tagName` as part of the namespace indicated by `namespaceURI`
  - `createAttributeNS(namespaceURI, attributeName)` => Creates a new attribute node as part of the namespace indicated by `namespaceURI`
  - `getElementsByTagNameNS(namespaceURI, tagName)` => Returns a `NodeList` of elements with the given `tagName` that are also a part of the namespace indicated by `namespaceURI`
48. The purpose of `importNode()` is to take a node from a different document and import it into a new document so that it can be added into the document structure. Remember, every node has an `ownerDocument` property that indicates the document it belongs to. If a method such as `appendChild()` is called and a node with a different `ownerDocument` is passed in, an error will occur. Calling `importNode()` on a node from a different document returns a new version of the node that is owned by the appropriate document.
49. `defaultView` is a pointer to the window (or frame) that owns the given document.
50. The DOM Level 2 HTML module also adds a method called `createHTMLDocument()` to `document.implementation`. The purpose of this method is to create a complete HTML document, including the `<html>`, `<head>`, `<title>`, and `<body>` elements. This method accepts a single argument, which is the title of the newly created document (the string to go in the `<title>` element)
51. `isSupported()` indicates what the node is capable of doing, it accepts two arguments: the feature name and the feature version.
52. DOM Level 3 introduces two methods to help compare nodes: `isSameNode()` and `isEqualNode()`. Both methods accept a single node as an argument and return true if that node is the same as or equal to the reference node. Two nodes are the same when they reference the same object. Two nodes are equal when they are of the same type and have properties that are equal (`nodeName`, `nodeValue`, and so on), and their attributes and `childNodes` properties are equivalent (containing equivalent values in the same positions).
53. The `setUserData()` method assigns data to a node and accepts three arguments: the key to set, the actual data (which may be of any data type), and a handler function. The handler function for `setUserData()` is called whenever the node with the data is cloned, removed, renamed, or imported into another document. The handler function accepts five arguments: a number indicating the type of operation (1 for clone, 2 for import, 3 for delete, or 4 for rename), the data key, the data value, the source node, and the destination node. The source node is null when the node is being deleted, and the destination node is `null` unless the node is being cloned.
54. For Frames and iframes, `contentDocument` contains a pointer to the `document` object representing the contents of the frame. Access to the `document` object of a frame or iframe is limited based on cross-domain security restrictions.
55. When in standards mode, all measurements have to include a unit of measure, like `"20px"`
56. Several properties for `style` object:
  - `length` => The number of CSS properties applied to the element.
  - `getPropertyCSSValue(propertyName)` => Returns a CSSValue object containing the value of the given property.
  - `getPropertyPriority(propertyName)` => Returns `“important”` if the given property is set using `!important`; otherwise it returns an empty string.
  - `getPropertyValue(propertyName)` => Returns the string value of the given property.
  - `removeProperty(propertyName)` => Removes the given property from the style.
57. `getPropertyCSSValue()` returns a `CSSValue` object that has two properties: `cssText` and `cssValueType`. The `cssText` property is the same as the value returned from `getPropertyValue()`. The `cssValueType` property is a numeric constant indicating the type of value being represented: 0 for an inherited value, 1 for a primitive value, 2 for a list, or 3 for a custom value.
58. Removing a property using `removeProperty()` means that any default styling for that property (cascading from other style sheets) will be applied.
59. The `style` object offers information about the `style` attribute on any element that supports it but contains no information about the styles that have cascaded from style sheets and affect the element.
60. `getComputedStyle()` accepts two arguments: the lement to get the computed style for and a pseudo-element string (such as `":after"`)
61. Several properties for `StyleSheet`, with the exception of `disabled`, the rest are read-only
  - `disabled` => A Boolean value indicating if the style sheet is disabled. This property is read/write, so setting its value to true will disable a style sheet.
  - `href` => The URL of the style sheet if it is included using `<link>`; otherwise, this is `null`.
  - `media` => A collection of media types supported by this style sheet.
  - `ownerNode` => Pointer to the node that owns the style sheet
  - `parentStyleSheet` => When a style sheet is included via `@import`, this is a pointer to the style sheet that imported it.
  - `title` => The value of the title attribute on the `ownerNode`.
62. `CSSStyleSheet` also supports:
  - `cssRules` => collection of rules contained in the style sheet.
  - `ownerRule` => If the style sheet was included using `@import`, this is a pointer to the rule representing the import; otherwise, this is `null`.
  - `deleteRule(index)` => Deletes the rule at the given location in the `cssRules` collection.
  - `insertRule(rule, index)` => Inserts the given string rule at the position specified in the `cssRules` collection.
63. The list of style sheets available on the `document` is represented by `document.styleSheets`
64. The DOM specifies a property called `sheet` that contains the `CSSStyleSheet` object.
65. Several properties for `CSSRule`, which represents each rule in a style sheet
  - `cssText` => Returns the text for the entire rule.
  - `parentRule` => If this rule is imported, this is the import rule; otherwise, this is `null`.
  - `parentStyleSheet` => The style sheet that this rule is a part of.
  - `selectorText` => Returns the selector text for the rule.
  - `style` => A `CSSStyleDeclaration` object that allows the setting and getting of specific style values for the rule. It is read-only, whereas `style.cssText` may be overwritten.
  - `type` => A constant indicating the type of rule.
66. Offset dimensions incorporate all of the visual space that an element takes up on the screen, including all padding, scrollbars, and borders (but not including margins), the following four properties are used to retrieve offset dimensions:
  - `offsetHeight` => The amount of vertical space, in pixels, taken up by the element, including its height, the height of a horizontal scrollbar (if visible), the top border height, and the bottom border height.
  - `offsetLeft` => The number of pixels between the element’s outside left border and the containing element’s inside left border.
  - `offsetTop` => The number of pixels between the element’s outside top border and the containing element’s inside top border.
  - `offsetWidth` => The amount of horizontal space taken up by the element, including its width, the width of a vertical scrollbar (if visible), the left border width, and the right border width.
67. The `offsetLeft` and `offsetTop` properties are in relation to the containing element, which is stored in the `offsetParent` property. The `offsetParent` may not necessarily be the same as the `parentNode`. For example, the `offsetParent` of a `<td>` element is the `<table>` element that it’s an ancestor of, because the `<table>` is the first element in the hierarchy that provides dimensions.
68. Client dimensions comprise the space occupied by the element's content and its padding. The `clientWidth` property is the width of the content area plus the width of both the left and the right padding. The `clientHeight` property is the height of the content area plus the height of both the top and the bottom padding. The `clientWidth` property is the width of the content area plus the width of both the left and the right padding. The `clientHeight` property is the height of the content area plus the height of both the top and the bottom padding.
69. The four scroll dimension properties are as follows:
  - `scrollHeight` => The total height of the content if there were no scrollbars present.
  - `scrollLeft` => The number of pixels that are hidden to the left of the content area. This property can be set to change the scroll position of the element.
  - `scrollTop` => The number of pixels that are hidden in the top of the content area. This property can be set to change the scroll position of the element.
  - `scrollWidth` => The total width of the content if there were no scrollbars present.
70. When trying to determine the total height of a document, including the minimum height based on the viewport, you must take the maximum value of `scrollWidth/clientWidth` and `scrollHeight/clientHeight` to guarantee accurate results across browsers.
71. The `scrollLeft` and `scrollTop` properties can be used either to determine the current scroll settings on an element or to set them.
72. A new instance of `NodeIterator` can be created using the `document.createNodeIterator()` method. The two primary method of `NodeIterator` are `nextNode()` and `previousNode()`, `nextNode()` returns `null` when it has reached the end of the DOM subtree. `document.createNodeIterator()` method accepts the following four arguments:
  - `root` => The node in the tree that you want to start searching from.
  - `whatToShow` => A numerical code indicating which nodes should be visited. It's a bitmask that determines which node to visit by applying one or more filters.
  - `filter` => A `NodeFilter` object or a function indicating whether a particular node should be accepted or rejected.
  - `entityReferenceExpansion` => A Boolean value indicating whether entity references should be expanded. This has no effect in HTML pages, because entity references are never expanded.
73. `TreeWalker` is a more advanced version of `NodeIterator`. It has the same functionality, including `nextNode()` and `previousNode()`, and adds the following methods to traverse a DOM structure in different directions:
  - `parentNode()` => Travels to the current node’s parent.
  - `firstChild()` => Travels to the fi rst child of the current node.
  - `lastChild()` => Travels to the last child of the current node.
  - `nextSibling()` => Travels to the next sibling of the current node.
  - `previousSibling()` => Travels to the previous sibling of the current node.
74. When used with a `TreeWalker` object, `NodeFilter.FILTER_SKIP` skips over the node and goes on to the next node in the subtree, whereas `NodeFilter.FILTER_REJECT` skips over that node and that node’s entire subtree.
75. The ·TreeWalker· type also has a property called ·currentNode· that indicates the node that was last returned from the traversal via any of the traversal methods. This property can also be set to change where the traversal continues from when it resumes
76. `document.createRange()`, several properties for `Range` type:
  - `startContainer` => The node within which the range starts (the parent of the first node in the selection).
  - `startOffset` => The offset within the `startContainer` where the range starts. If `startContainer` is a text node, comment node, or `CData` node, the `startOffset` is the number of characters skipped before the range starts; otherwise, the offset is the index of the first child node in the range.
  - `endContainer` => The node within which the range ends (the parent of the last node in the selection).
  - `endOffset` => The offset within the `endContainer` where the range ends (follows the same rules as `startOffset`).
  - `commonAncestorContainer` => The deepest node in the document that has both `startContainer` and `endContainer` as descendants.
77. The simplest way to select a part of the document using a range is to use either `selectNode()` or `selectNodeContents()`. These methods each accept one argument, a DOM node, and fill a range with information from that node. The `selectNode()` method selects the entire node, including its children, whereas `selectNodeContents()` selects only the node’s children.
78. When `selectNode()` is called, `startContainer`, `endContainer`, and `commonAncestorContainer` are all equal to the parent node of the node that was passed in, the `startOffset` property is equal to the index of the given node within the parent’s childNodes collection
79. When `selectNodeContents()` is called, `startContainer`, `endContainer`, and `commonAncestorContainer` are equal to the node that was passed in, the `startOffset` property is always equal to 0, since the range begins with the first child of the given node, whereas `endOffset` is equal to the number of child nodes (`node.childNodes.length`).
80. It’s possible to get more fine-grained control over which nodes are included in the selection by using the following range methods:
  - `setStartBefore(refNode)`
  - `setStartAfter(refNode)`
  - `setEndBefore(refNode)`
  - `setEndAfter(refNode)`
81. Creating complex ranges requires the use of the `setStart()` and `setEnd()` methods. Both methods accept two arguments: a reference node and an offset. For `setStart()`, the reference node becomes the `startContainer`, and the offset becomes the `startOffset`. For `setEnd()`, the reference node becomes the `endContainer`, and the offset becomes the `endOffset`.
82. `deleteContents()` simply deletes the contents of the range from the document, the range selection process altered the underlying DOM structure to remain well formed
83. `extractContents()` also removes the range selection from the document, it returns the range's document fragement as the function value.
84. When a document fragment is passed into `appendChild()`, only the fragment’s children are added, not the fragment itself
85. `cloneContents()` can be used to create a clone of range, the document fragement returned by `cloneContents()` contains clones of the nodes contained in the range instead of the actual nodes.
86. The splitting of nodes ensures that a well-formed document isn’t produced until one of these methods is called. The original HTML remains intact right up until the point that the DOM is modified.
87. The `insertNode()` method enables you to insert a node at the beginning of the range selection.
88. `surroundContents()` method accepts one argument, which is the node that surrounds the range contents. Behind the scenes, the following steps are taken:
  - The contents of the range are extracted (similarly to using `extractContents()`).
  - The given node is inserted into the position in the original document where the range was.
  - The contents of the document fragment are added to the given node.
89. You can collapse a range by using the `collapse()` method, which accepts a single argument: a Boolean value indicating which end of the range to collapse to. If the argument is `true`, then the range is collapsed to its starting point; if it is `false`, the range is collapsed to its ending point. To determine if a range is already collapsed, you can use the `collapsed` property
90. You can use the `compareBoundaryPoints()` method to determine if the ranges have any boundaries (start or end) in common. The method accepts two arguments: the range to compare to and how to compare
91. `detach()` method detaches the range from the document on which it was created
92. `HTMLFormElement` has the following additional properties and methods:
  - `acceptCharset` => The character sets that the server can process; equivalent to the HTML `accept-charset` attribute.
  - `action` => The URL to send the request to; equivalent to the HTML `action` attribute.
  - `elements` => An `HTMLCollection` of all controls in the form.
  - `enctype` => The encoding type of the request; equivalent to the HTML `enctype` attribute.
  - `length` => The number of controls in the form.
  - `method` => The type of HTTP request to send, typically `"get"` or `"post"`; equivalent to the HTML `method` attribute.
  - `name` => The name of the form; equivalent to the HTML `name` attribute.
  - `reset()` => Resets all form fields to their default values.
  - `submit()` => Submits the form.
  - `target` => The name of the window to use for sending the request and receiving the response; equivalent to the HTML `target` attribute.
93. Image buttons are defined using the `<input>` element with a type attribute of `"image"`
94. When a form is submitted by pressing `Enter` on the keyboard while a `form` control has focus, the `submit` event fires right before the request is sent to the server. This gives you the opportunity to validate the form data and decide whether to allow the form submission to occur. Preventing the event's default behavior cancels the form submission
95. When a form is submitted via `submit()`, the submit event does not fire, so be sure to do data validation before calling the method.
96. Reset buttons are created using either the `<input>` or the `<button>` element with a type attribute of `"reset"`. When a form is reset by the user clicking a reset button, the `reset` event fires. `reset()` fires the reset event the same as if a reset button were clicked.
97. HTML5 introduces an `autofocus` attribute for form fields that causes supporting browsers to automatically set the focus to that element without the use of JavaScript
98. For `<input>` and `<textarea>` elements, the `change` event fires when the field loses focus and the value has changed since the time the control got focus. For `<select>` elements, however, the change event fires whenever the user changes the selected option; the control need not lose focus for change to fire.
99. By default, the `<input>` element displays a text box, even when the `type` attribute is omitted (the default value is `"text"`). The `size` attribute can then be used to specify how wide the textbox should be in terms of visible characters. The `maxlength` attribute specifies the maximum number of characters allowed in the text box
100. `select()` selects all of the text in a text box. Most browsers automatically set focus to the text box when the `select()` method is called
101. The `select` event fires once the user has finished selecting text. The `select` event also fires when the `select()` method is called.
102. `selectionStart` and `selectionEnd` contain zero-based numbers indicating the text-selection boundaries (the offset of the beginning of text selection and the offset of end of text selection, respectively).
103. `setSelectionRange()` takes two arguments: the index of the first character to select and the index at which to stop the selection
104. The following six events are related to the clipboard:
  - `beforecopy` => Fires just before the copy operation takes place.
  - `copy` => Fires when the copy operation takes place.
  - `beforecut` => Fires just before the cut operation takes place.
  - `cut` => Fires when the cut operation takes place.
  - `beforepaste` => Fires just before the paste operation takes place.
  - `paste` => Fires when the paste operation takes place.
105. The `beforecopy`, `beforecut`, and `beforepaste` events give you the opportunity to change the data being sent to or retrieved from the clipboard before the actual event occurs. However, canceling these events does not cancel the clipboard operation — you must cancel the `copy`, `cut`, or `paste` event to prevent the operation from occurring.
106. There are three methods on the `clipboardData` object: `getData()`, `setData()`, and `clearData()`.
107. Any field marked as `required` must have a value in order for the form to be submitted.
108. The `pattern` attribute was introduced for text fields in HTML5. This attribute specifies a regular expression with which the input value must match. Note that `^` and `$` are assumed at the beginning and end of the pattern, respectively. Specifying a `pattern` does not prevent the user from entering invalid text. The `pattern` is applied to the value, and the browser then knows if the value is valid or not.
109. You can check if any given field on the form is valid by using the `checkValidity()` method
110. You can instruct a form not to apply any validation to a form by specifying the `novalidate` attribute. If there are multiple submit buttons in a form, you can specify that the form not validate when a particular submit button is used by adding the `formnovalidate` attribute to the button itself
111. `HTMLSelectElement` type provides the following properties and methods in addition to those that are available on all form fields:
  - `add(newOption, relOption)` => Adds a new `<option>` element to the control before the related option.
  - `multiple` => A Boolean value indicating if multiple selections are allowed; equivalent to the HTML `multiple` attribute.
  - `options` => An `HTMLCollection` of `<option>` elements in the control.
  - `remove(index)` => Removes the option in the given position.
  - `selectedIndex` => The zero-based index of the selected option or `–1` if no options are selected. For select boxes that allow multiple selections, this is always the first option in the selection.
  - `size` => The number of rows visible in the select box; equivalent to the HTML `size` attribute.
112. The `type` property for a select box is either `"select-one"` or `"select-multiple"`, depending on the absence or presence of the `multiple` attribute. The option that is currently selected determines a select box's value property according to the following rules:
  - If there is no option selected, the value of a select box is an empty string.
  - If an option is selected and it has a value `attribute` specified, then the select box’s value is the `value` attribute of the selected option. This is true even if the `value` attribute is an empty string.
  - If an option is selected and it doesn't have a `value` attribute specified, then the select box's value is the text of the option.
  - If multiple options are selected, then the select box's value is taken from the first selected option according to the previous two rules.
113. It's worth noting that setting the `selected` property to `false` has no effect in a single-select select box.
114. Rich text (also called **what you see is what your get**), the basic technique of it is to embed an `iframe` containing a blank HTML file in the page. Through the `designMode` property, this blank document can be made editable, at which point you're editing the HTML of the page's `<body>` element.
115. The `contenteditable` attribute can be applied to any element on a page and instantly makes that element editable by the user.
116. The primary method of interacting with a rich text editor is through the use of `document.execCommand()`. There are three possible arguments for `document.execCommand()`: the name of the command to execute, a Boolean value indicating if the browser should provide a user interface for the command, and a value necessary for the command to work (or `null` if none is necessary).
117. `queryCommandEnabled()` determines if a command can be executed given the current text selection or caret position. This method accepts a single argument, the command name to check, and returns true if the command is allowed given the state of the editable area or `false` if not.
118. The `queryCommandState()` method lets you determine if a given command has been applied to the current text selection.
119. `queryCommandValue()` is intended to return the value with which a command was executed.


## Events

1. Inside an event handler, the `this` object is always equal to the value of `currentTarget`, whereas `target` contains only the actual target of the event.
2. Any event that can be canceled using `preventDefault()` will have its `cancelable` property set to true
3. The `<img>` element need not be added to the document for the image download to begin; it begins as soon as the `src` property is set.
4. Unlike images, JavaScript files start downloading only after the `src` property has been assigned and the element has been added into the document
5. Several Focus events:
  - `blur` => Fires when an element has lost focus. This event doesn't bubble
  - `focus` => Fires when an element has received focus. This event doesn't bubble
  - `focusin` => Fires when an element has received focus. This is a bubbling version of the `focus` HTML event
  - `focusout` => Fires when an element has lost focus. This is a generic version of the `blur` HTML event
6. When focus is moved from one element to another on the page, the following order of events is followed:
  - `focusout` => fires on the element losing focus.
  - `focusin` => fires on the element receiving focus.
  - `blur` => fires on the element losing focus.
  - `DOMFocusOut` => fires on the element losing focus.
  - `focus` => fires on the element receiving focus.
  - `DOMFocusIn` => fires on the element receiving focus.
7. Several mouse events:
  - `click` => Fires when user clicks the primary mouse button or when the user presses the Enter key. A `click` event can be fired only if a `mousedown` event is fired and followed by a `mouseup` event on the same element
  - `mouseenter` => Fires when the mouse cursor is outside of an element and then the user moves it outside of that element's boundaries. This event does not bubble and does not fire when cursor moves over descendant elements
  - `mouseleave` => Fires when the mouse cursor is over an element and then the user moves it outside of that element's boundaries. This event does not bubble and does not fire when the cursor moves over descendant elements
  - `mouseout` => Fires when the mouse cursor is over an element and then the user moves it over another element. The element moved to may be outside of the bounds of the original element or a child of the original element. 
  - `mouseover` => Fires when the mouse cursor is outside of an element and then the user first moves it inside of the boundaries of the element. 
8. The order is 
  - `mouserdown`
  - `mouseup`
  - `click`
  - `mousedown`
  - `mouseup`
  - `click`
  - `dbclick`
9. A `click` event can be fired only if a `mousedown` event is fired and followed by a `mouseup` event on the same element
10. The DOM provides information about related elements via the `relatedTarget` property on the `event` object. This property contains a value only for the `mouseover` and `mouseout` events; it is `null` for all other events.
11. For mouse events, `detail` contains a number indicating how many times a click has occurred at the given location. Clicks are considered to be a `mousedown` event followed by a `mouseup` event at the same pixel location. The value of detail starts at 1 and is incremented every time a click occurs. If the mouse is moved between `mousedown` and `mouseup`, then `detail` is set back to 0.
12. Three keyboard events:
  - `keydown` => Fires when the user presses a key on the keyboard and fires repeatedly while the key is being held down.
  - `keypress` => Fires when the user presses a key on the keyboard that results in a character and fires repeatedly while the key is being held down. This event also fires for the `Esc` key.
  - `keyup` => Fires when the user releases a key on the keyboard.
13. When the user presses a character key once on the keyboard, the `keydown` event is fired first, followed by the `keypress` event, followed by the `keyup` event. Note that both `keydown` and `keypress` are fired before any change has been made to the text box, whereas the `keyup` event fires after changes have been made to the text box. If a character key is pressed and held down, `keydown` and `keypress` are fired repeatedly and don't stop until the key is released.
14. There is only one text event and it is called `textInput`. This event is an augmentation of `keypress` intended to make it easier to intercept text input before being displayed to the user. The `textInput` event fires just before text is inserted into a text box. Since the `textInput` event is interested primarily in characters, it provides a `data` property on the `event` object that contains the character that was inserted (not the character code). The value of `data` is always the exact character that was inserted, so if the `S` key is pressed without `Shift`, data is `"s"`, but if the same key is pressed holding `Shift` down, then data is `"S"`.
15. Difference between `keypress` and `textInput`: 
  - `keypress` fires on any element that can have focus but `textInput` fires only on editable areas
  - `textInput` fires only for keys that result in a new character being inserted, whereas `keypress` fires for keys that affect text in any way (including `Backspace`).
16. There are three composition events:
  - `compositionstart` => Fires when the text composition system of the IME is opened, indicating that input is about to commence.
  - `compositionupdate` => Fires when a new character has been inserted into the input field.
  - `compositionend` => Fires when the text composition system is closed, indicating a return to normal keyboard input.
17. When a composition event fires, the target is the input field receiving the text. The only additional event property is `data`, which contains one of the following:
  - When accessed during `compositionstart`, contains the text being edited (for instance, if text has been selected and will now be replaced).
  - When accessed during `compositionupdate`, contains the new character being inserted.
  - When accessed during `compositionend`, contains all of the input entered during this composition session.
18. The mutation events defined in DOM Level 2 are as follows:
  - `DOMSubtreeModified` => Fires when any change occurs to the DOM structure. This is a catchall event that fires after any of the other events fire.
  - `DOMNodeInserted` => Fires after a node is inserted as a child of another node.
  - `DOMNodeRemoved` => Fires before a node is removed from its parent node.
  - `DOMNodeInsertedIntoDocument` => Fires after a node has been inserted either directly or by inserting the subtree in which it exists. This event fires after `DOMNodeInserted`.
  - `DOMNodeRemovedFromDocument` => Fires before a node is removed either directly or by having the subtree in which it exists removed. This event fires after `DOMNodeRemoved`.
  - `DOMAttrModified` => Fires when an attribute has been modified.
  - `DOMCharacterDataModified` => Fires when a change is made to the value of a text node.
19. When a node is removed from the DOM using `removeChild()` or `replaceChild()`, the `DOMNodeRemoved` event is fired first. The target of this event is the removed node, and the `event.relatedNode` property contains a reference to the parent node. At the point that this event fires, the node has not yet been removed from its parent, so its `parentNode` property still points to the parent (same as `event.relatedNode`). This event bubbles, so the event can be handled at any level of the DOM. If the removed node has any child nodes, the `DOMNodeRemovedFromDocument` event fires on each of those child nodes and then on the removed node. This event doesn’t bubble, so an event handler is called only if it’s attached directly to one of the child nodes. The target of this event is the child node or the node that was removed, and the event object provides no additional information. After that, the `DOMSubtreeModified` event fires. The target of this event is the parent of the node that was removed. The event object provides no additional information about this event.
20. When a node is inserted into the DOM using `appendChild()`, `replaceChild()`, or `insertBefore()`, the `DOMNodeInserted` event is fired first. The target of this event is the inserted node, and the `event.relatedNode` property contains a reference to the parent node. At the point that this event fires, the node has already been added to the new parent. This event bubbles, so the event can be handled at any level of the DOM. Next, the `DOMNodeInsertedIntoDocument` event fires on the newly inserted node. This event doesn’t bubble, so the event handler must be attached to the node before it is inserted. The target of this event is the inserted node, and the event object provides no additional information. The last event to fire is `DOMSubtreeModified`, which fires on the parent node of the newly inserted node.
21. Each object that supports the `readystatechange` event has a `readyState` property that can have one of the following five possible string values:
  - `uninitialized` => The object exists but has not been initialized.
  - `1loading` => The object is loading data.
  - `loaded` => The object has finished loading its data.
  - `interactive` => The object can be interacted with but it’s not fully loaded.
  - `complete` => The object is completely loaded.
22. back-forward cache (bfcache) is designed to speed up page transitions when using the browser’s Back and Forward buttons. The cache stores not only page data but also the DOM and JavaScript state, effectively keeping the entire page in memory. If a page is in the bfcache, the load event will not fire when the page is navigated to.
23. `pageshow`, fires whenever a page is displayed, whether from the bfcache or not. On a newly loaded page, `pageshow` fires after the `load` event; on a page in the bfcache, `pageshow` fires as soon as the page's state has been completely restored. The event handler must be attached to `window`. The `event` object for `pageshow` includes a property called `persisted`. This is a Boolean value that is set to `true` if the page is stored in the bfcache or false if the page is not.
24. `pagehide`, fires immediately before the `unload` event. `persistent` is set to `true` if the page will be stored in the bfcache once unloaded.
25. `hashchange` event handler must be attached to the `window`

## Canvas

1. The `<canvas>` element requires at least its `width` and `height` attributes to be set in order to indicate the size of the drawing to be created. Any content appearing between the opening and closing tags is fallback data that is displayed only if the `<canvas>` element isn't supported.
2. Images created on a `<canvas>` element can be exported using the `toDataURL()` method. This method accepts a single argument, the MIME type format of the image to produce, and is applicable regardless of the context used to create the image. The `toDataURL()` method throws an error if an image from a different domain is drawn onto a canvas.
3. You can erase an area of the canvas by using the `clearRect()` method. This method is used to make an area of the drawing context transparent.
4. `isPointInPath()` accepts an x-coordinate and a y-coordinate as arguments. This method can be called anytime before the path is closed to determine if a point exists on the path
5. `translate(x, y)` => Moves the origin to the point (x,y). After performing this operation, the coordinates (0,0) are located at the point previously described as (x,y).
6. `save` and `restore()`
7. The 2D context will automatically draw a shadow along with a shape or path based on the value of several properties:
  - `shadowColor` => The CSS color in which the shadow should be drawn. The default is black.
  - `shadowOffsetX` => The x-coordinate offset from the x-coordinate of the shape or path. The default is 0.
  - `shadowOffsetY` => The y-coordinate offset from the y-coordinate of the shape or path. The default is 0.
  - `shadowBlur` => The number of pixels to blur. If set to 0, the shadow has no blur. The default is 0.
8. `createLinearGradient()` accepts four arguments: the starting x-coordinate, the starting y-coordinate, the ending x-coordinate, and the ending y-coordinate.
9. `createRadialGradient()` accepts six arguments corresponding to the center of a circle and its radius. The first three arguments define the starting circle's center (x and y) and radius, while the last three define the same for the ending circle.
10. To create a new pattern, call the `createPattern()` method and pass in two arguments: an HTML `<img>`, `<video>` or `<canvas>` element and a string indicating how the image should be repeated. The second argument is the same as the values for the CSS `background-repeat` property: `"repeat"`, `"repeat-x"`, `"repeat-y"`, and `"no-repeat"`.
11. `getImageData()` method retrieves raw image data, it accepts four arguments: the left and top position of the first pixel whose data should be retrieved, and the pixel width and the pixel height to retrieve.
12. The `globalAlpha` property is a number between 0 and 1, inclusive, that specifies the alpha value for all drawings.
13. The `globalCompositionOperation` property indicates how newly drawn shapes should merge with the already-existing image on the context.

## JSON

1. There is no trailing semicolon (not needed since this isn't a JavaScript statement). Once again, the quotes around the property name are required to be valid JSON.
2. When serializing a JavaScript object, all functions and prototype members are intentionally omitted from the result. Additionally, any property whose value is undefined is also skipped. You're left with just a representation of the instance properties that are one of the JSON data types.
3. The `JSON.stringify()` method actually accepts two arguments in addition to the object to serialize. These arguments allow you to specify alternate ways to serialize a JavaScript object. The first argument is a filter, which can be either an array or a function, and the second argument is an option for indenting the resulting JSON string. 
4. If the argument is an array, then `JSON.stringify()` will include only object properties that are listed in the array. 
5. When the second argument is a function, the behavior is slightly different. The provided function receives two arguments: the property key name and the property value. In order to change the serialization of the object, return the value that should be included for that key. Keep in mind that returning undefined will result in the property being omitted from the result.
6. The third argument of `JSON.stringify()` controls indentation and white space. When this argument is a number, it represents the number of spaces to indent each level. `JSON.stringify()` also inserts new lines into the JSON string for easier reading. This happens for all valid indentation argument values. The maximum numeric indentation value is 10; passing in a value larger than 10 automatically sets the value to 10. If the indentation argument is a string instead of a number, then the string is used as the indentation character for the JSON string instead of a space. There is a ten-character limit on the indentation string to use. If a string longer than ten characters is used, then it is truncated to the first ten characters.
7. you can add a `toJSON()` method to the object and have it return the proper JSON representation for itself.
8. When an object is passed into `JSON.stringify()`, the following steps are taken:
  - Call the `toJSON()` method if it's available to retrieve the actual value. Use the default serialization otherwise.
  - If the second argument is provided, apply the filter. The value that is passed into a filter function will be the value returned from step 1.
  - Each value from step 2 is serialized appropriately.
  - If the third argument is provided, format appropriately. It's important to understand this order when deciding whether to create
9. The `JSON.parse()` method also accepts an additional argument, which is a function that is called on each key-value pair. The function is called a `reviver` function. If the `reviver` function returns `undefined`, then the key is removed from the result; if it returns any other value, that value is inserted into the result.

## AJAX

1. To begin using an XHR object, you will first call the method `open()`, which accepts three arguments: the type of request to be sent ("get", "post", and so on), the URL for the request, and a Boolean value indicating if the request should be sent asynchronously. The URL is relative to the page on which the code is called, although an absolute path can be given as well. The call to `open()` does not actually send the request; it simply prepares a request to be sent. You can access only URLs that exist on the same origin, which means the same domain, using the same port, and with the same protocol. If the URL specifies any of these differently than the page making the request, a security error is thrown.
2. The status code of 304 indicates that a resource hasn't been modified and is being served from the browser's cache, which also means a response is available
3. The XHR object has a `readyState` property that indicates what phase of the request/response cycle is currently active. The possible values are as follows:
  - `0` => Uninitialized. The `open()` method hasn't been called yet.
  - `1` => Open. The `open()` method has been called but `send()` has not been called.
  - `2` => Sent. The `send()` method has been called but no response has been received.
  - `3` => Receiving. Some response data has been retrieved.
  - `4` => Complete. All of the response data has been retrieved and is available.
4. You can cancel an asynchronous request before a response is received by calling the `abort()` method
5. You can retrieve the response headers from an XHR object by using the `getResponseHeader()` method and passing in the name of the header to retrieve. It's also possible to retrieve all headers as a long string by using the `getAllResponseHeaders()` method.
6. The `onprogress` event listener receives an `event` object whose target is the XHR object and contains three additional properties: `lengthComputable`, a Boolean indicating if progress information is available; `position`, which is the number of bytes that have already been received; and `totalSize`, which is the total number of expected bytes as defined by the `Content-Length` response header.
7. There are some additional limitations on a cross-domain XHR object that are necessary for security purposes. They are as follows:
  - Custom headers cannot be set using `setRequestHeader()`.
  - Cookies are neither sent nor received.
  - The `getAllResponseHeaders()` method always returns an empty string.
8. There are two popular approaches to Comet: long polling and streaming.
  - Long polling => The page initiates a request to the server and the server holds that connection open until it has data to send. Once the data is sent, the connection is closed by the browser and a new connection is immediately opened up to the server. This process continues for as long as the page is open in the browser.
  - HTTP streaming => The browser sends a request to the server and the server holds that connection open, periodically sending data through the connection to the server.
9. Server-Sent Events (SSE) is an API and pattern for read-only Comet interactions.
10. You must pass in an absolute URL to the `WebSocket` constructor. The same-origin policy does not apply to Web Sockets, so you can open a connection to any site.
11. When an unauthorized system is able to access a resource, it is considered a cross-site request forgery (CSRF) attack.