# Basic Javascript

- 2 Major syntactic categories: 
    - statements 
        - Statements do things
    - expressions
        - Expressions produce values
- Semicolons
    - terminates statements but not blocks
- Values
    - All values have properties
    - You can create properties on the fly for objects
    - Primitive Values Versus Objects
        - Primitive values
            - booleans, numbers, strings, null, undefined
            - Compared by value using '==='
            - Always immutable
       - Objects
            - e.g.
                - Plain objects created by object literals
                - Arrays
                - Regular Expressions
            - has a unique identity 
            - Compared by reference using '==='
            - Mutable by default
        - undefined and null
            - undefined means "no value"
                - used whenever values are expected but absent
            - null means "no object"
                - used whenever objects are expected but absent
            - They have no properties
- Categorising values using 'typeof' and 'instanceof'
    - 'typeof' use for primitive values
        - results:
            - typeof undefined -> 'undefined'
            - typeof null      -> 'object'
                This is a bug as `null instanceof Object === false`
            - typeof boolean   -> 'boolean'
            - typeof number    -> 'number'
            - typeof string    -> 'string'
            - typeof function  -> 'function'
            - typeof _         -> 'object'
    - 'instanceof' used for objects
        ```javascript
            > var b = new Bar();
            > b instanceof Bar
            true
        ```
- Booleans
    - Truthy and Falsy
        - "false" -> false, 0, undefined, null, NaN, and ''
        - "true"  -> everything else
    - Equality operator
        - strict comparison: '===', '!=='
            - ` "1" === 1 -> False `
            - Always use!
        - type converting comparison: '==', '!=='
            - ` "1" === 1 -> True `
- Numbers
    - All numbers are floating-point
    - Special numbers:
        - NaN
        - Infinity
- Strings
    - Single characters are like arrays of characters
        - `"abc"[1] -> b`
        - `"abc".length -> 3`
    - Strings are immutable
- If block
    - As expected :)
    - switch statement
        ```javascript
        switch (fruit) {
            case 'banana'
                //...
                break
            case 'apple'
                //...
                break
            default:
                //...
        }
        ```
- Loops
    - like C++ or Java
    - `for`, `while`, `do { ... } while ()`
    - `break` leaves the loop
    - `continue` starts a new loop iteration
- Functions
    - via function declaration
        ```javascript
        function add(param1, param2) {
            return param1 + param2;
        }
        ```
    - via function expression
        ```javascript
        var add = function (param1, param2) {
            return param1 + param2;
        }
        ```
    - Function declarations are hoisted - i.e. moved - to the beginning of the current scope. Not so with function expression.
    - Special Variable: `arguments` (not an Array!)
        ```javascript
        > function f() { return arguments }
        > f('a', 'b', 'c').length 
        3
        ```
        - Convert `arguments` to an Array 
            ```javascript
            function toArray(arrayLikeObject) {
                return Array.prototype.slice.call(arrayLikeObject);
            }
            ```
    - Too Many or Too Few Arguments
        - Too many -> picked up by `arguments`
        - Too few  -> set as undefined
    - Optional parameters
        - Pattern for setting defaults
            ```javascript
            function pair(x,y) {
                x = x || 0;
                y = y || 0;
                return [x, y];
            }
            ```
    - Enforcing an Arity
        - Explicitely check arguments.length
            ```javascript
                function pair(x, y)
                if (arguments.length !== 2) {
                    throw new Error('Need exactly 2 arguments');
                }
            ```
- Exception Handling
    - As expected... `throw`, `try`, `catch`
- Strict Mode
    - enables more warnings
    - type in a JS file, function, or in a `<script>` tag:
        `use strict`
- Variable Scoping and Closures
    - Variables are function-scoped
    - Variables are hoisted to the beginning of the function
    - The IIFE (Immediately Invoked Function Expression) Pattern: Introducing a new Scope
        ```javascript
        (function () {
            var tmp = ...; // not a global variable
        }())
        ```
- Objects and Constructors
    - single objects
        ```javascript 
        var jane = {
            name: 'Jane',
            describe: function () {
                return 'Person named ' + this.name;
            }
        }
        ```
    - `in` operator check whether a property exists
    - `delete` operator removes a property
    - Arbitrary Property Keys
        ```javascript
        > var obj = { 'not an identifier': 123 }
        > obj['not an identifier']
        123
        ```
    - Extracting Methods
        - Extracting a method loses its connection with the object
            - `this` has value undefined
            ```javascript
            > var func = jane.describe;
            > func()
            TypeError: Cannot read property 'name' of undefined
            ```
        - Solution: use the method `bind()`
            ```javascript
            > var func2 = jane.describe.bind(jane);
            > func2()
            'Person named Jane'
            ```
    











