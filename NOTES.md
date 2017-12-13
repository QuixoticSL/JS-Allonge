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

### November 14th 2017 ###
- A “tail-call” occurs when a function’s last act is to invoke another function, and then return whatever the other function returns.
- This is a very important characteristic of JavaScript: *If a function makes a call in tail position, JavaScript optimizes away the function call overhead and stack space.*

### November 15th 2017 ###
- Our `[first, ...rest]` approach to recursion is slow because that it creates a lot of temporary arrays, and it spends an enormous amount of time copying elements into arrays that end up being discarded.
- The 704 had a 36-bit word, meaning that it was very fast to store and retrieve 36-bit values. The CPU’s instruction set featured two important macros: `CAR` would fetch 15 bits representing the Contents of the Address part of the Register, while `CDR` would fetch the Contents of the Decrement part of the Register.
- Having these instructions be very fast was important to those early designers: They were working on one of the first high-level languages (COBOL and FORTRAN being the others), and computers in the late 1950s were extremely small and slow by today’s standards. Although the 704 used core memory, it still used vacuum tubes for its logic. Thus, the design of programming languages and algorithms was driven by what could be accomplished with limited memory and performance.

- Using two-element arrays to represent cons cells:
```javascript
const cons = (a, d) => [a, d],
car  = ([a, d]) => a,
cdr  = ([a, d]) => d;
```

- A linked list:
```javascript
const node5 = [5,null],
node4 = [4, node5],
node3 = [3, node4],
node2 = [2, node3],
node1 = [1, node2];
    
const oneToFive = node1;
```

- Again, it’s just extracting a reference from a cons cell, it’s very fast. In Lisp, it’s blazingly fast because it happens in hardware. There’s no making copies of arrays, the time to `cdr` a list with five elements is the same as the time to `cdr a list with 5,000 elements, and no temporary arrays are needed. In JavaScript, it’s still much, much, much faster to get all the elements except the head from a linked list than from an array. Getting one reference to a structure that already exists is faster than copying a bunch of elements.

### November 16th 2017 ###
- Linked lists are fast for a few things, like taking the front element off a list, and taking the remainder of a list. But not for iterating over a list: Pointer chasing through memory is quite a bit slower than incrementing an index. In addition to the extra fetches to dereference pointers, pointer chasing suffers from cache misses. And if you want an arbitrary item from a list, you have to iterate through the list element by element, whereas with the indexed array you just fetch it.
- Arrays avoid this problem by pessimistically copying all the references whenever we extract an element or sequence of elements from them

### November 17th 2017 ###
- Lists are not the only way to represent collections of things, but they are the “oldest” data structure in the history of high level languages, because they map very closely to the way the hardware is organized in a computer.
- Dictionaries store key-value pairs, so instead of binding `NAME` to `0` and then storing a name in an array at index 0, we can bind a name directly to `name` in a dictionary, and we let JavaScript sort out whether the implementation is a list of key-value pairs, a hashed collection, a tree of some sort, or anything else.
- JavaScript has dictionaries, and it calls them “objects.” The word “object” is loaded in programming circles, due to the widespread use of the term “object-oriented programming” that was coined by Alan Kay but has since come to mean many, many things to many different people.
- `{ year: 2012, month: 6, day: 14}`
- Objects use [] to access the values by name, using a string:  

```javascript
{ year: 2012, month: 6, day: 14}
['day'] //14
```

- `date['day'] === date.day //true` If the name is an alphanumeric string conforming to the same rules as names of variables, there’s a simplified syntax for accessing the values.

### November 18th 2017 ###
- Destructuring objects:

```javascript
const {name: { first: given, last: surname}, occupation: { title: title } } = us\
er;

surname
  //=> "Braithwaite"

title
  //=> "Author"
```

### November 19th 2017 ###
- Linked lists are constructed back-to-front, but we iterate through them front-to-back. So to copy a list, we have to save all the bits on the call stack and then construct the list from back-to-front as all the recursive calls return.
- In JavaScript, almost every type of value can mutate. Their identities stay the same, but not their structure. Specifically, arrays and objects can mutate.
(Adding, changing values of arrays and objects)

- Shadowing:
```javascript
const allHallowsEve = [2012, 10, 31];
(function (halloween) {
  halloween = [2013, 10, 31];
})(allHallowsEve);
allHallowsEve
  //=> [2012, 10, 31]
```
The outer value of `allHallowsEve` was not changed because all we did was rebind the name `halloween` within the inner environment. However, what happens if we mutate the value in the inner environment?

```javascript
const allHallowsEve = [2012, 10, 31];
(function (halloween) {
  halloween[0] = 2013;
})(allHallowsEve);
allHallowsEve
  //=> [2013, 10, 31]
```
We haven’t rebound the inner name to a different variable, we’ve mutated the value that both bindings share.

- Declaring a variable `const` does not prevent us from mutating its value, only from rebinding its name. This is an important distinction.

### November 21st 2017 ###
- Linked lists often use structure sharing. Structure sharing is what makes linked lists so fast for taking everything but the first item of a list: We aren’t making a new list, we’re using some of the old list.
- We don’t have to remember to use copying operations when we pass it as a value to a function, or extract some data from it. We just use the data, and the less we mutate it, the fewer the times we have to think about whether making changes will be “safe.”

### November 22nd 2017 ###
- JavaScript does not permit us to rebind a name that has been bound with `const`. We can shadow it by using const to declare a new binding with a new function or block scope, but we cannot rebind a name that was bound with `const` in an existing scope.
- Rebinding parameters is usually avoided, but what about rebinding names we declare within a function? What we want is a statement that works like `const`, but permits us to rebind variables. JavaScript has such a thing, it’s called `let`.
- Some programmers dislike deliberately shadowing variables. The suggestion is that shadowing a variable is confusing code. If you buy that argument, the way that shadowing works in JavaScript exists to protect us from accidentally shadowing a variable when we move code around.
- Shadowing a `const` with a `let` does not permit it to be rebound in its original scope.

### November 23rd 2017 ###
- Declaring `age` twice does not cause an error(!), and the inner declaration does not shadow the outer declaration. All `var` declarations behave as if they were hoisted to the top of the function, a little like function declarations.
- But, again, it is unwise to expect consistency. A function declaration can appear anywhere within a function, but the declaration and the definition are hoisted.
- In that way, `var` is a little like `const` and `let`, we should always declare and bind names before using them.

### November 24th 2017 ###
- If you have an array, and you take it’s “rest,” your “child” array is a copy of the elements of the parent array. And therefore, modifications to the parent do not affect the child, and modifications to the child do not affect the parent.
- If you have a linked list, and you take it’s “rest,” your “child” list shares its nodes with the “parent” list. And therefore, modifications to the parent also modify the child, and modifications to the child also modify the parent.

### November 25th 2017 ###
- “copy-on-read”, because when we attempt the parent to “read” the value of a child of the list, we make a copy and read the copy of the child. Thereafter, we can write to the parent or the copy of the child freely.
- Why are we copying? In case we modify a child list. Ok, what if we do this: Make the copy when we know we are modifying the list. When do we know that? When we call `set`.
- Copy-on-write is the name given to the policy that whenever a task attempts to make a change to the shared information, it should first create a separate (private) copy of that information to prevent its changes from becoming visible to all the other tasks. It’s much cheaper than pessimistically copying structures when you make an infrequent number of small changes, but if you tend to make a lot of changes to some that you aren’t sharing, it’s more expensive.

```javascript
const EMPTY = null;

const isEmpty = (node) => node === EMPTY;

const pair = (first, rest = EMPTY) => ({first, rest});

const list = (...elements) => {
  const [first, ...rest] = elements;
  
  return elements.length === 0
    ? EMPTY
    : pair(first, list(...rest))
}

const forceAppend = (list1, list2) => {
  if (isEmpty(list1)) {
    return "FAIL!"
  }
  if (isEmpty(list1.rest)) {
    list1.rest = list2;
  }
  else {
    forceAppend(list1.rest, list2);
  }
}

const tortoiseAndHare = (aPair) => {
  let tortoisePair = aPair,
      harePair = aPair.rest;
  
  while (true) {
    if (isEmpty(tortoisePair) || isEmpty(harePair)) {
      return false;
    }
    if (tortoisePair.first === harePair.first) {
      return true;
    }
    
    harePair = harePair.rest;
    
    if (isEmpty(harePair)) {
      return false;
    }
    if (tortoisePair.first === harePair.first) {
      return true;
    }
    
    tortoisePair = tortoisePair.rest;
    harePair = harePair.rest;
  }
};

const aList = list(1, 2, 3, 4, 5);

tortoiseAndHare(aList)
  //=> false

forceAppend(aList, aList.rest.rest);

tortoiseAndHare(aList);
  //=> true
```
This algorithm is called “The Tortoise and the Hare,” and was discovered by Robert Floyd in the 1960s. You have two node references, and one traverses the list at twice the speed of the other. No matter how large it is, you will eventually have the fast reference equal to the slow reference, and thus you’ll detect the loop.

### November 27th 2017 ###
- JavaScript has a particularly low-level version of for loop that mimics the semantics of the C language. Summing the elements of an array can be accomplished with:
```javascript
const arraySum = (array) => {
  let sum = 0;

  for (let i = 0; i < array.length; ++i) {
    sum += array[i];
  }
  return sum
}

arraySum([1, 4, 9, 16, 25])
  //=> 55
```

- Iterators are functions. When they iterate over an array or linked list, they are traversing something that is already there. But they could just as easily manufacture the data as they go.
- A function that starts with a seed and expands it into a data structure is called an unfold. It’s the opposite of a fold. It’s possible to write a generic unfold mechanism

### November 28th 2017 ###
- Please note that unlike most of the other functions discussed in this book, iterators are stateful. There are some important implications of stateful functions. One is that while functions like `take(...)` appear to create an entirely new iterator, in reality they return a decorated reference to the original iterator.
- For all intents and purposes, once you pass an iterator to a function, you can expect that you no longer “own” that iterator, and that its state either has changed or will change.
- Kestrel, Idiot Bird and Vireo:
```javascript
const K = (x) => (y) => x;
const I = (x) => (x);
const V = (x) => (y) => (z) => z(x)(y);
```
- A constant function is a function that always returns the same thing, no matter what you give it. For example, `(x) => 42` is a constant function that always evaluates to 42. The kestrel, or `K`, is a function that makes constant functions. You give it a value, and it returns a constant function that gives that value.
- The identity function is a function that evaluates to whatever parameter you pass it. So I(42) => 42. Very simple, but useful. 
- This is very interesting. Given two values, we can say that K always returns the first value, and given two values, K(I) always returns the second value.

### November 29th 2017 ###
- As an aside, the Vireo is a little like JavaScript’s `.apply` function. It says, “take these two values and apply them to this function.” There are other, similar combinators that apply values to functions. One notable example is the “thrush” or T combinator: It takes one value and applies it to a function. It is known to most programmers as `.tap`.
- We can use pure functions to represent a linked list.
- `aPair === EMPTY ? doSomething : doSomethingElse` follows the pattern that the function doing the work inspects the data structure.
- Empty list syntax: `const EMPTYLIST = (whenEmpty, unlessEmpty) => whenEmpty()`
- Node of a list syntax: `const node = (x) => (y) => (whenEmpty, unlessEmpty) => unlessEmpty(pair(x)(y));`
- Practically speaking, languages like JavaScript already provide arrays with mapping and folding methods, choice operations, and other rich constructs. Knowing how to make a linked list out of functions is not really necessary for the working programmer. (Knowing that it can be done, on the other hand, is very important to understanding computer science.)
- Having a list know itself whether it is empty hides implementation information from the code that uses lists. This is a fundamental principle of good design. It is a tenet of Object-Oriented Programming, but it is not exclusive to OOP: We can and should design data structures to hide implementation information from the code that use them, whether we are working with functions, objects, or both.
- Hiding implementation information: Instead of directly manipulating part of an entity, pass it a function and have it call our function with the part we want. And instead of testing some property of an entity and making a choice of our own with `?:` (or `if`), pass the entity the work we want done for each case and let it test itself.

### November 30th 2017 ###
- In JavaScript, arrays have a `.map` method. Map takes a function as an argument, and applies it to each of the elements of the array, then returns the results in another array.
- `const map = (list, fn) => list.map(fn);` a function that behaves like `.map`
- `mapWith`, a function that wraps around map and turns any other function into a mapper. `mapWith` is very simple: `const mapWith = (fn) => (list) => list.map(fn);`
- It reverses the arguments, taking the function first and the list second. It also “curries” the function: Instead of taking two arguments, it takes one argument and returns a function that takes another argument.
- Assigning properties from one object to another (also called “cloning” or “shallow copying”) is a basic building block that we will later use to implement more advanced paradigms like mixins.

### December 1st 2017 ###
- The Y combinator enables you to make recursive functions without needing to bind a function to a name in an environment. With fixed-point combinators it’s possible to compute everything computable without binding names.
- An expression is any valid unit of code that resolves to a value.
- JavaScript supports *quasi-literal* strings, a/k/a “Template Strings” or “String Interpolation Expressions.” A quasi-literal string is something that looks like a string literal, but is actually an expression. Quasi-literal strings are denoted with back quotes, and most strings that can be expressed as literals have the exact same meaning as quasi-literals
- A quasi-literal can contain an expression to be evaluated. This is called *interpolation*
- A popular number for nerds is ${40 + 2} //=> 'A popular number for nerds is 42'
- JavaScript evaluates the quasi-literal when the function is invoked and the quasi-literal inside the function’s body is evaluated.
- OOP to me means only messaging, local retention and protection and hiding of state-process, and extreme late-binding of all things.

### December 2nd 2017 ###
- Information hiding is the ability to prevent certain aspects of a class or software component from being accessible to its clients, using either programming language features (like private variables) or an explicit exporting policy.
- Consider a stack data structure. There are three basic operations: Pushing a value onto the top (`push`), popping a value off the top (`pop`), and testing to see whether the stack is empty or not (`isEmpty`). These three operations are the stable interface.
- Hiding information (or “state”) is the design principle that allows us to limit the coupling between components of software.
- Given an object that holds our state (an array and an index39), we can easily implement our three operations as functions. Bundling the functions with the state does not require any special “magic” features. JavaScript objects can have elements of any type, including functions.
- Other languages may separate methods from functions very strictly, but in JavaScript every method is a function, but not all functions are methods.
- A deeply fundamental practice is to build components out of smaller components. The choice of how to divide a component into smaller components is called factoring, after the operation in number theory.
- Each component is a value, and the components can be put together into a single object or encapsulated with a closure.
- Another practice that many people consider fundamental is to extend an implementation. Meaning, they wish to define a new data structure in terms of adding new operations and semantics to an existing data structure.
- Encapsulation and Extension exist in a natural state of tension. A program with elaborate encapsulation resists breakage but can also be difficult to refactor in other ways. Be mindful of when it’s best to Compose and when it’s best to Extend.

### December 3rd ###
- Closures couple functions to environments, and that makes them very elegant in the small, and very handy for making opaque data structures. Alas, their strength in the small is their weakness in the large. When you’re trying to make reusable components, this coupling is sometimes a hindrance.
- Any time we must do the same repetitive thing over and over and over again, we industrial humans try to build a machine to do it for us. JavaScript is one such machine. When we write a function expression using the compact method syntax (or use the `function` keyword instead of the fat arrow), and then invoke that function using `.` notation, JavaScript binds the “receiver” of a “method invocation” to the special name `this`.
- Now we are relying on JavaScript to set the value of `this` whenever we invoke one of these functions using the `.` or `[` and `]` operators.
- Every time you invoke a function that is a member of an object, JavaScript binds that object to the name `this` in the environment of the function just as if it was an argument.
- Being able to copy objects is an example of a larger concern: Being able to share functions between objects. That’s how classes work. That’s how extending objects works. Being able to share functions means being able to compose and reuse functionality.
- Closures tightly couple functions to the environments where they are created limiting their flexibility. Using `this` alleviates the coupling.

### December 4th 2017 ###
- JavaScript programmers talk about functions having a “context” when being called. `this` is bound to the context.
- The important thing to understand is that the context for a function being called is set by the way the function is called, not the function itself.

### December 5th 2017 ###
- We learned that a decorator takes a function as an argument, returns a function, and there’s a semantic relationship between the two.

### December 6th 2017 ###
- *Fibonacci number*
```javascript
const fibonacci = (n) =>
  n < 2
    ? n
    : fibonacci(n-2) + fibonacci(n-1);

[0,1,2,3,4,5,6,7,8].map(fibonacci)
//=> [0,1,1,2,3,5,8,13,21]
```
- `Memoized` is used with functions so they can remember what they have calculated, so that they don't have to recalculate the same value a second time. A function has to be "idempotent", which means the function always returns the same results given the same arguments.
- `getWith` is an interesting function: it takes the name of an attribute and returns a function. That function then extracts the value of that attribute from an object.

```javascript
const getWith = (attr) => (object) => object[attr]
```
Example code for the function `getWith`.

- `pluckWith` is a combination between `getWith` and `mapWith`.

### December 7th 2017 ###
- JavaScript has objects, and by default, those objects are dictionaries. By default, objects directly manipulate each other’s state. Methods can be added to, or removed from objects at run time. 
- In JavaScript, object and array literals construct objects that delegate behaviour to the standard library’s object prototype and array prototype, respectively. JavaScript also supports using `Object.create` to construct objects with or without a prototype, and `new` to construct objects using a constructor function.
- JavaScript also has a `class` keyword that provides syntactic sugar for writing constructor functions and prototypes in a declarative fashion.

### December 8th 2017 ###
- Acting on the elements of a collection one at a time is called iterating over the contents, and JavaScript has a standard way to iterate over the contents of collections.
- In programs involving large collections of objects, it can be handy to implement iterators as objects, rather than functions. 
- To ensure that the method would not conflict with any existing code, JavaScript provides a *symbol*. Symbols are unique constants that are guaranteed not to conflict with existing strings. The expression `Symbol.iterator` evaluates to a special symbol representing the name of the method that objects should use if they return an iterator object.
- The `for...of` loop works directly with any object that is iterable, meaning it works with any object that has a `Symbol.iterator` method that returns an object iterator. 

### December 9th 2017 ###
- Attempting to spread an infinite iterable into an array is always going to fail: `firstAndSecondElement(...Numbers) //Infinite loop`
- *Ordered collections* are collections where every time you iterate over them/it, you get the elements of the collection in order, starting from the beginning.
```javascript
const abc = ["a","b","c"];

for (const i of abc){
  console.log(i);
} // Always returns: a b c
```
- Using `mapWith` on ordered collections:
```javascript
const mapWith = (fn, collection) = >
  ({
    [Symbol.iterator] () {
      const iterator = collection[Symbol.iterator]();

      return {
        next (){
          const {done, value} = iterator.next();

          return ({done, value: done ? undefined : fn(value)})
        }
      }
    }
  });
```
- This illustrates the general pattern of working with ordered collections: We make them iterables, meaning that they have a `[Symbol.iterator]` method, that returns an iterator.
- JS's in house `Array` has a property called `.from` which gathers an iterable into a particular collection type.
```javascript
Array.from(UpTo1000) //[1,81,121,361,441,841,961]
```

### December 10th 2017 ###
- Fibonacci sequence generator:
```javascript
const fibonacci = () => {
  let a, b;

  console.log(a = 0);
  console.log(b = 1);

  while(true) {
    [a, b] = [b, a + b];
    console.log(b);
  }
}
fibonacci() //0 1 1 2 3 5 8 13...
```
- The generation version has state, but it’s implicit in JavaScript’s linear control flow. Whereas the iteration version must make that state explicit.
- There are two diferences when writing a js generator function: the declaration must be `function *` and we use `yield` instead of `return`.
- When we invoke such a function we get an iterator object back:
```javascript
function * only (something) {
  yield something;
};

only("you").next() //{"done": false, value: "you"}
```
- Generators are *coroutines* meaning they are computer program components that generalize subroutines for nonpreemptive multitasking, by allowing multiple entry points for suspending and resuming execution at certain locations.
- There are two execution contexts that are going on in iterators: the producer, which is the iterator and the consumer, which is the code that iterates over.

### December 12th 2017 ###
```javascript
const ThreeNumbers = {
  *[Symbol.iterator] () {
    yield 1;
    yield 2;
    yield 3
  }
}
```
- Using `[Symbol.iterator]` makes it iterable, but not an iterator. The star symbol makes it a generator, as written before.

- Fibonacci sequence generator.
```javascript
function * fibonacci () {
  let a, b;

  yield a = 0;
  yield b = 1;
  
  while (true) {
    [a, b] = [b, a + b]
    yield b;
  }
}

for (const i of fibonacci()) {
  console.log(i);
} // 0 1 1 2 3 5 8 13 21 34...
```
- A function that returns an iterable is usually much more simpler if you write it as a genarator, rather than a function that returns an iterable object.

- `yield *` yield all of the elements of an iterable, in order. It comes in handy when writing generator functions that operate on or create iterables.
- Generator utiliziting `mapWith`
```javascript
function * mapWith (fn, iterable) {
  for (const element of iterable) {
    yield fn(element);
  }
}
```
- In JS we build single-responsibility functions and objects, so that we can compose these together to build more full-featured objects and algorithms.
- This “fat object” style springs from a misunderstanding: When we say a collection should know how to perform a map over itself, we don’t need for the collection to handle every single detail. That would be like saying that when we ask a bank teller for some cash, they personally print every bank note.

### December 13th 2017 ###
- In terms of programming laziness means not doing anything remotely towards working untill you know you need the result of the work.

```javascript
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
  .map((x) => x * x)
  .filter((x) => x % 2 == 0)
  .reduce((seed, element) => seed + element, 0)

Pair.from([1, 2, 3, 4, 5, 6, 7, 8, 9, 10])
  .map((x) => x * x)
  .filter((x) => x % 2 == 0)
  .reduce((seed, element) => seed + element, 0)
```
In practice the array here is better since it works within the engine, while the linked list does its work in JS. `.map` and `.filter` produce new arrays when they are gathering results. They produce two temp arrays which are then discarded.
- *Eager* collections, similar to arrays, return a collection of their own type from each of the methods. Any collection can be *Eager* if it is gatherable, meaning that it contains a `.from` method.