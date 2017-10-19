# JS Allonge Notes from the book #

### October 9th 2017 ###
- `for (int i = 0; i < array.length; i++){...}` where i is block scoped. In ES6 the standard is `const` and `let` which both allow block scoping in functions without IIFE.

### October 10th 2017 ###
- All values are expressions.
- Strings are values, so they are also expressions, but having them be connected with an operator like "+" makes them just expressions.
- Strings and integers can never have the `===` between them obviously.
- Even when we obtain a string, number, or boolean as the result of evaluating an expression, it is identical to another value of the same type with the same "content".

### October 11th 2017 ###
- Every time we call `new` with a function and get an object back, we get a unique object. We could call these “Objects created with the `new` keyword,” but this would be cumbersome. So we’re going to call them instances. Instances of what? Instances of the function that creates them. So given `const i = new Ur()`, we say that `i` is an instance of `Ur`.

### October 12th 2017 ###
- In computer science, a literal is a notation for representing a fixed value in source code.
- If we start a literal with a zero, it is an octal literal. So the literal 042 is 42 base 8, which is actually 34 base 10.
- For example, the largest integer JavaScript can safely1 handle is 9007199254740991, or 2^53 - 1.
- A computer’s internal representation for a floating point number is binary, while our literal number was in base ten. This makes no meaningful difference for integers, but it does for fractions, because some fractions base 10 do not have exact representations base 2.

### October 14th 2017 ###
- `() => 0` a function that applies no values and returns 0.
- We have two types of values with respect to identity: Value types and reference types. Value types share the same identity if they have the same contents. Reference types do not. "Function" is a reference type.
- We apply functions to arguments.
- `(() => 0)()` outputs `=> 0`. Since we aren't giving the function any arguments we are leaving the last `()` empty.
- We can make a function that returns a value by putting the value to the right of the arrow.

### October 15th 2017 ###
- The comma operator in JavaScript is interesting. It takes two arguments, evaluates them both, and itself evaluates to the value of the right-hand argument. `(1, 2)` would be `2`.
- A block has zero or more statements, separated by semicolons.
- Returns the result of evaluating a block that has no statements. So `(() => {})()` would throw out `undefined`.
- `undefined` is a value that means “I don’t have a value.” But it’s still a value.
- `void` is an operator that takes any value and evaluates to `undefined`, always. By convention we are suppose to use `void 0`, which throws out `void 0 = > undefined`.
- A block is a list of JS statements separated by semicolons. `(() => { 1 + 1; 2 + 2 })()` for instance spits out `undefined`.
- A block with one expression does not behave like an expression, and a block with more than one expression does not behave like an expression constructed with the comma operator.
- So how do we get a function that evaluates a block to return a value when applied? With the `return` keyword and any expression: `(() => { return 1 })()` spits out 1.
- Statements belong inside blocks and only inside blocks.

### October 16th 2017 ###
- `() => () => true` a function that evaluates to another function which returns `true`.
- To apply a function with an argument (or arguments), we put the argument (or arguments) within the parentheses, like this: `((diameter) => diameter * 3.14159265)(2)` which returns `6.2831853`. You give the function a parameter `2` which is the diameter and it runs the code in the body, thus returning a result.
- `((room, board) => room + board)(800, 150)` writing a functions with two arguments. Here we are doing addittion. 
- Like most contemporary programming languages, JavaScript uses the “call by value” evaluation strategy (when to evaluate the arguments).

### October 17th 2017 ###
- `(x) => (y) => x` where the first `x` is an argument, `y` is another argument and the last `x` is an expression referring to a variable.
- Invoking a function means applying zero or more arguments.
- Call by sharing is generally understood to be a specialization of call by value, and it explains why some values are known as value types and other values are known as reference types.

### October 18th 2017 ###
- The function `(y) => x` is interesting. It contains a free variable, `x`. A free variable is one that is not bound within the function.
- Functions containing no free variables are called pure functions. Functions containing one or more free variables are called closures. A pure function can contain a closure.

### October 19th 2017 ###
- `(x) => x` is called the I Combinator, or the Identity Function. `(x) => (y)` => x is called the K Combinator, or Kestrel.
- `(x) => (y) => (z) => x + y + z` is the exact same as `(x, y, z) => x + y + z`
- The first function is the result of currying the second function. Calling a curried function with only some of its arguments is sometimes called partial application.
- JavaScript always searches for a binding starting with the functions own environment and then each parent in turn until it finds one.
- (x) => (x, y) => (w, z) => (w) => x + y + z. When evaluating x + y + z, JavaScript will find x and y in the great-grandparent scope and z in the parent scope. The x in the great-great-grandparent scope is ignored, as are both ws. When a variable has the same name as an ancestor environment’s binding, it is said to *shadow* the ancestor.