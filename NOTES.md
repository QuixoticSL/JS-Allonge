# JS Allonge Notes from the book #

### October 9th 2017 ###
- `for (int i = 0; i < array.length; i++){...}` where i is block scoped. In ES6 the standard is `const` and `let` which both allow block scoping in functions without IIFE.

### October 10th 2017 ###
- All values are expressions.
- Strings are values, so they are also expressions, but having them be connected with an operator like "+" makes them just expressions.
- Strings and integers can never have the `===` between them obviously.
- ```(2 + 2 === 4) === (2 !== 5)
  //=> true
  ```
- Even when we obtain a string, number, or boolean as the result of evaluating an expression, it is identical to another value of the same type with the same "content".

### October 11th 2017 ###
- Every time we call `new` with a function and get an object back, we get a unique object. We could call these “Objects created with the `new` keyword,” but this would be cumbersome. So we’re going to call them instances. Instances of what? Instances of the function that creates them. So given `const i = new Ur()`, we say that `i` is an instance of `Ur`.