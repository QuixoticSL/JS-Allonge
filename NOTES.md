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

### October 28th 2017 ###
- Function declarations are formally only supposed to be made at what we might call the “top level” of a function. Function declarations are not supposed to occur inside of blocks.
- Another caveat is that a function declaration cannot exist inside of any expression, otherwise it’s a function expression, for instance: `(function trueDat () { return true })` is a function expression because it is in parentheses.
- Generally speaking, a function that either takes functions as arguments, or returns a function, or both, is referred to as a “higher-order” function.
- A combinator is a higher-order function that uses only function application and earlier defined combinators to define a result from its arguments. In JS terms this refers to: Higher-order pure functions that take only functions as arguments and return a function.
- The *Compose* combinator: `const compose = (a, b) => (c) => a(b(c))`
- *Compose* in an example: `const addOne = (number) => number + 1;` would turn into: `const doubleOfAddOne = (number) => doubleOf(addOne(number))`. Looks like an onion with it's many different layers or functionality.

### October 29th 2017 ###
- Code that uses a lot of combinators tends to name the verbs and adverbs (like doubleOf, addOne, and compose) while avoiding language keywords and the names of nouns (like number).
- A *function decorator* is a higher-order function that takes one function as an argument, returns another function, and the returned function is a variation of the argument function. Example: `const not = (fn) => (x) => !fn(x)`
- Function decorators aren’t strict about being pure functions, so there’s more latitude for making decorators than combinators.

### October 30th 2017 ###
- One of the most basic of these building blocks is composition: `const cookAndEat = (food) => eat(cook(food));` which means chaining two functions together. Writing functions that can be composed in various ways.
- A decorator called *Once* which is only called once obviously, but it ensures that certain side effects don't happene to be repeated. A decorator called *Maybe* which does nothing if it is given the value of nothing (in this case `null` or `undefined`) as an argument.
- These decorators become really useful when chained together, for example transfering money: `const invokeTransfer = once(maybe(actuallyTransfer(...)));`
- Another basic building block is *partial application*. When a function takes multiple arguments, we “apply” the function to the arguments by evaluating it with all of the arguments, producing a value. But what if we only supply some of the arguments? In that case, we can’t get the final value, but we can get a function that represents *part* of our application.
- The "Underscore" library provides a higher-order function called *map* which applies another function to each element of an array: `_.map([1, 2, 3], (n) => n * n) //=> [1, 4, 9]`
- `mapWith` takes any function as an argument and returns a partially applied map function.

### October 31st 2017 ###
- Although `arguments` looks like an array, it isn’t an array: It’s more like an object that happens to bind some values to properties with names that look like integers starting with zero.
- `arguments` always contains all of the arguments passed to a function, regardless of how many are declared.
- The most common use of the `arguments` binding is to build functions that can take a variable number of arguments.

### November 1st 2017 ###
- Instead of being bound when the function is invoked, the fat arrow function always acquires the bindings for `this` and `arguments` from its enclosing scope, just like any other binding.
- Fat arrow functions are designed to be very lightweight and are often used with constructs like mapping or callbacks to emulate syntax.
- Arguments in functions are passed by sharing which is also known as "pass by value".
- Fat arrow functions have blocks as their bodies.
- Function declarations are always *hoisted to the top*.

### November 2nd 2017 ###
- “Unary” is a function decorator that modifies the number of arguments a function takes: Unary takes any function and turns it into a function taking exactly one argument. The most common use case is to fix a problem. JavaScript has a `.map` method for arrays, and many libraries offer a `map` function with the same semantics: `['1', '2', '3'].map(parseFloat)` which transforms the strings in the array into floats.
- JavaScript’s `map` actually calls each function with three arguments: The element, the index of the element in the array, and the array itself.
- One of the most basic combinators is the “K Combinator,” nicknamed the “Kestrel:” `const K = (x) => (y) => x;`

### November 3rd 2017 ###
- The "K Combinator" has some surprising applications. One is when you want to do something with a value for side-effects, but keep the value around. 
- `tap` is a traditional name borrowed from various Unix shell commands. It takes a value and returns a function that always returns the value, but if you pass it a function, it executes the function for side-effects.
- A common problem in programming is checking for `null` or `undefined` (hereafter called “nothing,” while all other values including `0`, `[]` and `false` will be called “something”).
- `maybe` reduces the logic of checking for nothing to a function call: `maybe((a, b, c) => a + b + c)(1, 2, 3) //=> 6`
- `once` is an extremely helpful combinator. It ensures that a function can only be called, well, once. You pass it a function, and you get a function back. That function will call your function once, and thereafter will return `undefined` whenever it is called.
- *Left-Variadic Functions* or a *variadic function* is a function that is designed to accept a variable number of arguments. ECMAScript 2015 only permits gathering parameters from the end of the parameter list. Not the beginning!
- a *right-variadic* function, meaning that it has one or more fixed arguments, and the rest are gathered into the rightmost argument

### November 4th 2017 ###
- *compose3 syntax*: `const compose3 = (a, b, c) => (d) => a(b(c(d)))`
- First step to writing a recursive compose is writing the *degenerate* case, for instance if `compose` only took one argument: `const compose = (a) => a`.
- The next thing is to have a way of breaking a piece off the problem. We can do this with a variadic function: `const compose = (a, ...rest) => "to be determined".
- To compose a series of functions together, creating a new one. And the value is the same: We can write smaller, single purpose functions and put them together in different ways.
- Sometimes it makes more sense to compose functions in data flow order, as in “The value flows through a and then through b.” For this, we can use the `pipeline` function.
- Comparing `pipeline` to `compose`, pipeline says “add one to the number and then double it.” Compose says, “double the result of adding one to the number.” Both do the same job, but communicate their intention in opposite ways.

### November 5th 2017 ###
- JavaScript inherited an operator from the C family of languages, the ternary operator. It’s the only operator that takes three arguments. It looks like this: `first ? second : third`. It evaluates `first`, and if `first` is “truthy”, it evaluates `second` and that is its value. If `first` is not truthy, it evaluates `third` and that is its value.
- The ternary operator is an *expression* and not a *statement*.
- JavaScript always evaluates the expressions for parameters before passing the values to a function to invoke.

### November 6th 2017 ###
- Array literals are expressions, and arrays are reference types. We can see that each time an array literal is evaluated, we get a new, distinct array, even if it contains the exact same elements.

### November 7th 2017 ###
- Arrays store references to the things you put in them and not the actual values, just references.
- Array literal: `const wrap = (something) => [something];`
- Sometimes we need to extract arrays from arrays. Here is the most common pattern: Extracting the head and gathering everything but the head from an array.
- `...` is a *gatherer*. `const oneTwoThree = ["one", "two", "three"];` followed by `["zero", ...oneTwoThree]` does `["zero", "one", "two", "three"]`.

### November 8th 2017 ###
- But we can also define a list by describing a rule for building lists. One of the simplest, and longest-standing in computer science, is to say that a list is: Empty or consists of an element concatenated with a list.


### November 9th 2017 ###
- Recursive algorithms follow the “divide and conquer” strategy for solving a problem: divide the problem into smaller problems, if a smaller problem is solvable solve the small problem, if a smaller problem is not solvable divide and conquer that problem, when all small problems have been solved, compose the solution into one big solution. This simpler form of “divide and conquer” is called *linear recursion*.
- Sometimes we want to *flatten* an array, that is, an array of arrays needs to be turned into one array of elements that aren’t arrays.
- How do we decide whether a smaller problem is solvable? We need a test for the terminal case: `isArray`.
- The usual “terminal case” will be that flattening an empty array will produce an empty array. The next terminal case is that if an element isn’t an array, we don’t flatten it, and can put it together with the rest of our solution directly. Whereas if an element is an array, we’ll flatten it and put it together with the rest of our solution.

### November 10th 2017 ###
- Another common problem is applying a function to every element of an array. By using linear recursion to solve this problem we are using something called *mapping*.