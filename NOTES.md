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

### October 20th 2017 ###
- In order to bind 3.14159265 to the name PI, we’ll need a function with a parameter of PI applied to an argument of 3.14159265. If we put our function expression in parentheses, we can apply it to the argument of 3.14159265: `((PI) => (diameter) => diameter * PI)(3.1415)`.
- We can bind anything we want in an expression by wrapping it in a function that is immediately invoked with the value we want to bind.

### October 21st 2017 ###
- We can turn things inside-out by putting the binding inside our diameter calculating function, like this: `(diameter) => ((PI) => diameter * PI)(3.14159265)`. The “outer” function describes its parameters. Everything else is encapsulated in its body. 
- Invoking functions is considerably more expensive than evaluating expressions.
- Pass PI along with the diameter argument: `(diameter, PI) => diameter * PI`.
- We have one binding in the environment representing our regular argument, and another our “constant.”
- We use the `const` keyword in a _const statement_. _const statements_ occur inside blocks, we can’t use them when we write a fat arrow that has an expression as its body.
- This underscores what we’ve said: if we have an expression that evaluates to a function, we apply it with `()`. A name that’s bound to a function is a valid expression evaluating to a function.

### October 22nd 2017 ###
- Lexical scoping, because we can discover where a name is bound by looking at the source code for the program.
- Binding values to names with const works just like binding values to names with parameter invocations, it uses lexical scope.
- We say that when we bind a variable using a parameter inside another binding, the inner binding shadows the outer binding. It has effect inside its own scope, but does not affect the binding in the enclosing scope.
- Names bound with const shadow enclosing bindings just like parameters.
- `if (true) {// an immediately invoked block statement (IIBS)}`

### October 23rd 2017 ###
- `const repeat = (str) => str + str` This syntax binds an anonymous function to a name in an environment, but the function itself remains anonymous.

### October 25th 2017 ###
- Placing a name between the `function` keyword and the argument list names the function. 
- `const double = function repeat (str) {return str + str;}` where `double` is the name of the environment and `repeat` is the actual name of the function. This is a named function expression. 

### October 27th 2017 ###
- Function declarations are hoisted to the top of the function in which they occur.
- This behaviour is intentional on the part of JavaScript’s design to facilitate a certain style of programming where you put the main logic up front, and the “helper functions” at the bottom.