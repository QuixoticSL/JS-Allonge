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