# JavaScript Fundamentals Review

This lab is intended as a review of some of the core concepts and syntax of
modern JavaScript. Links are provided in each section to labs that are
important to complete and review to ensure a clear understanding of concepts.

## Variables

---

* [Data Types Readme](https://github.com/learn-co-curriculum/js-basics-data-types-readme)
* [Data Types Quiz](https://github.com/learn-co-curriculum/javascript-data-types-quiz)
* [Variables](https://github.com/learn-co-curriculum/js-basics-variables-readme)
* [Variables Quiz](https://github.com/learn-co-curriculum/js-basics-variables-lab)
* [Scope](https://github.com/learn-co-curriculum/intro-javascript-discussion-questions)
* [Scope Lab](https://github.com/learn-co-curriculum/js-principles-scope-lab)

---

There are three types of variables, `var`, `let`, and `const`, that can be used to store data. Each type acts slightly differently, particularly in regards to scope.

### `var`

* Are function scoped - variables declared using `var` can be read or rewritten anywhere within the function they are declared in, including inside any nested blocks. If a `var` is declared outside of an enclosing function, it will be accessible at the global scope
* Are **hoisted**, meaning they are accessible before being assigned
* Can be redeclared in the same scope

```
// global scope
var a = 1

// function scope
function x() {
  var b = 2
  console.log(a) // 1
}

// block scope
for (let idx = 0; idx < 1; idx++) {
  var c = 3
}

x()              // 1
console.log(a)   // 1
console.log(b)   // ReferenceError: b is not defined
console.log(c)   // 3
```

#### When to Use `var`

The `var` variable type is useful when declaring variables that you want accessible and changeable throughout a function.  While there are times when this is necessary, more often than not, we are declaring variables within a specific scope and do not need them elsewhere.  In these cases, we can be more specific than `var` and use `let` or `const`.

### `let`

* Block scoped - variables declared using `let` can only be accessed within the block they are declared in
* Are not **hoisted**, meaning they are not accessible before they are assigned
* Cannot be redeclared in the same scope

```
// global scope
let a = 1

// function scope
function x() {
  let b = 2
  console.log(a) // 1
}

// block scope
for (let idx = 0; idx < 1; idx++) {
  let c = 3
}

x()              // 1
console.log(a)   // 1
console.log(b)   // ReferenceError: b is not defined
console.log(c)   // ReferenceError: c is not defined

// block scope
for (let idx = 0; idx < 1; idx++) {
  a = 4
}

console.log(a)   // 4
```

Take a moment to consider the following questions, and explain your answers to a peer or teacher when you feel you have a strong description:
* why did `x()` correctly log `a`s value?
* understanding that `let` keeps block scope, why did the value 4, assigned to `a` in the last for loop's block scope, persist outside of the for loop's block scope?

#### When to Use `let`

Using `let` restricts a variable to a tighter bound scope, which keeps our namespaces cleaner and makes us less likely to screw up as programmers. If the variable does not need to be accessed outside of a block, but needs to be reassignable, use `let`.

Try running the following two for loops in your browser console:

```
for (var x = 0; x < 5; x++) {
  console.log('hello')
}

for (let y = 0; y < 5; y++) {
  console.log('world')
}

console.log(x) // logging 'x' outputs 5

console.log(y) // ReferenceError: y is not defined
```

It is unlikely we need to access `x` outside of the for loop above, but using `var` will make it accessible. If you had another `var x` somewhere in your code, this could potentially *overwrite* that variable. Using `let` in blocks keeps your function scope clear of these unnecessary variables. It also provides some slightly different functionality in closures, compared to `var`. For example, `let` stays bound within the scope of each loop in the following code:

```
for (let i = 0; i < 5; ++i) {
  setTimeout(function () {
    console.log("i: ",i);
  }, 100);  
}

//Output:
//i: 1
//i: 2
//i: 3
//i: 4
//i: 5
```

Try replacing `let` with `var` in the code above. The output will be `5`, five
times.

### `const`

* Cannot be overwritten
* Block scoped - variables declared using `const` can only be accessed within the block (same scoping restrictinos as `let`)
* Are not **hoisted**, meaning they are not accessible before they are assigned
* Must be _defined_ when they are _declared_, e.g. a value must be provided when they are created (see `x` example below)

```
const x // SyntaxError: Missing initializer in const declaration

const a = 10
console.log(a) // 10

a = 11 // TypeError: Assignment to constant variable.



```

Since `const` and `let` are both block scoped, we can use the two in similar situations. The `const` variable is bound to the scope of each iteration in a loop (it is redefined each loop), so, although we can't change the value once declared, we can still use them:

```
for (let i = 0; i < 5; i++) {
	const timer = performance.now()
	console.log(timer) // Outputs the time in milliseconds each loop
}

console.log(timer) // ReferenceError: timer is not defined
```

When assigning to a `const` variable a value, such as `const a = 5`, `a`
_contains_ the value `5`. If we assign an array or object to a `const`, instead of assigning a direct value, the variable points to a reference in memory of that object. This means that while a `const` value can't be redefined, `const` objects are still mutable:

```
const humans = []
console.log(humans) // outputs []
humans.push('Steve')
console.log(humans)  // outputs ['Steve']
```

#### When to Use `const`

Using `const` on any variables you know you wont need to redefine can help
prevent unforeseen errors, such as conflicting name assignments. When you use
`const`, you're also indicating to future readers of your code that this
variable is meant to be unchanged

It is often the best practice to default to using this strictest scope you can
when declaring variables; if a `let` works in place of a `var`, use `let` to
keep your variable only within the scope you need. If the variable should
never be reassigned after declaration, then use `const`.

## Arrays and Objects

---

* [Arrays](https://github.com/learn-co-curriculum/js-data-structures-arrays-readme)
* [Arrays Lab](https://github.com/learn-co-curriculum/js-data-structures-arrays-lab)
* [Objects](https://github.com/learn-co-curriculum/js-data-structures-objects-readme)
* [Objects Lab](https://github.com/learn-co-curriculum/js-data-structures-objects-lab)
* [Objects and Arrays Quiz](https://github.com/learn-co-curriculum/js-data-structures-objects-and-arrays-quiz)

---

### Arrays

From the labs, we know that arrays are a type of object that can contain
multiple values in a list. We can declare arrays in a variety of ways:

```
const w = new Array
console.log(w) // []
const x = new Array(5).fill("hi")
console.log(x) // ["hi","hi","hi","hi","hi"]

const y = []
console.log(y) // []
const z = ["hello"]
console.log(z) // ["hello"]
```

Arrays can stored all sorts of data types, and are useful when we need to
iterate through a list in a specific order:

```
const a = [1,2,3]
const b = ["a","b","c"]
const c = [true, true, false]
const d = [{id: 1}, {id: 2}]
const e = [() => console.log("hello"), () => alert("world")]
```

Arrays have a number of specific methods that are very useful for reading
and manipulating lists:

#### [Map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)

```
const a = [1,2,3,4,5]
const b = a.map(element => element + 1)

console.log(a) // [1,2,3,4,5]
console.log(b) // [2,3,4,5,6]
```

#### [Filter](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)

```
const a = [1,2,3,4,5]
const b = a.filter(element => element > 3)

console.log(a) // [1,2,3,4,5]
console.log(b) // [4,5]

const c = ["a", "b", "c"]
const d = c.filter(element => element !== "b")

console.log(c) // ["a", "b", "c"]
console.log(d) // ["a", "c"]
```

#### [Reduce](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)

```
const a = [1,2,3,4,5]
const b = a.reduce((accumulator, currentValue) => accumulator + currentValue)

console.log(a) // [1,2,3,4,5]
console.log(b) // 15, the sum of all values in the array

const c = [[1], [2, 3], [4, 5]]
const d = c.reduce((accumulator, currentValue) => accumulator.concat(currentValue))

console.log(c) // [[1], [2, 3], [4, 5]]
console.log(d) // [1, 2, 3, 4, 5]
```

#### [Splice](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)

```
const a = ["x","y","z"]
const b = a.splice(1,1)

console.log(a) // ["x", "z"]
console.log(b) // ["y"]

const c = ["a","b","d","e"]
const d = c.splice(2,0,"c")

console.log(c) // ["a","b","c","d","e"]
console.log(d) // []
```

#### Using the Spread Operator on Arrays

The spread operator is a new feature of ES6 that can be used to make a copy of
an array and in place of array concatenation:

```
const a = [1,2,3]
const b = a

console.log(b) // [1,2,3]
console.log(a === b) // true, because they both reference the same point in memory

const c = [1,2,3]
const d = [...c]

console.log(d) // [1,2,3]
console.log(c === d) // false, because the spread operator has created a new array reference

const e = [1,2,3]
const d = [...e, 4]

console.log(d) // [1,2,3,4]
```

### Objects

Objects, like arrays, can contain multiple values, but instead of storing
them in a list, each value is store with a corresponding key:

```
const a = new Object // a === {}
const b = {} // b === {}
```

Objects are great for storing sets of related data, including functions.

```
const a = {name: "Steve", sayHi: () => console.log("hello")}
```

This makes objects very versatile and handy when you have complex return values.

```
function returnPerson() {
	const id = 1
	const name = "Steve"
	const sayHi = () => console.log('hi')

	return {
		id: id,
		name: name,
		sayHi: sayHi
	}
}

const a = returnPerson() // a === {id: 1, name: "Steve", sayHi: ƒ}
a.sayHi() // outputs 'hi'
```

#### Iterating Using Objects

It is possible to iterate over the values in any object like an array using
Object.keys():

```
const a = {id: 1, name: "Steve", password: "123"}
const b = Object.keys(a)
console.log(b) // ["id", "name", "password"]

const c = b.map(element => a[element])
console.log(c) // [1, "Steve", "123"]
```

#### The Advantages of Instant Lookup

Because each value in an object has a corresponding key, looking up something
stored in an object is instant. On the other hand, finding something in an
array requires us to iterate through the array, so the amount of time will
depend on the length of the array. When dealing with large sets of data, even a
list, it is more performant to use objects:

```
const a = [
	{id: 1, name: "Steve"},
	{id: 2, name: "Mike"}
]
const b = {
	"Steve": {id: 1, name: "Steve"},
	"Mike": {id: 2, name: "Mike"}
}

// to find Mike the array above, you must iterate through it:
const c = a.find(element => element.name === "Mike")

// to find Mike in an object:
const d = b["Mike"]
```

#### Destructuring Objects

Another new feature in JavaScript is the destructuring of objects into
variables assigned to the objects values:

```
const a = {id: 1, name: "Steve", password: "123"}
const { id, name, password } = a;

console.log(id, name, password) // 1 "Steve" "123"
```

This can be useful for making your code more readable and is also handy for
extracting specific values of an object being passed into a function:

```
const a = {id: 1, name: "Steve", password: "123"}

sayName(a)

function sayName({name}) {
	console.log(name) // outputs "Steve"
}
```

The above examples refer to key/value pairs using a new ES6 shorthand syntax.
Instead of having to write out a key and value, if you provide just a variable
name, JS will interpret it as the key and assign that key the value of the
variable:

```
const id = 1
const a = {id}
console.log(a) // outputs {id: 1}
```

#### Using the Spread Operator on Objects

When the spread operator is used on an object, like arrays, it returns
a copy of the object it is applied to. This can be useful when we need to
modify a specific part of an object, or add a key/value:

```
const a = {id: 1, name: "Steve"}
const b = Object.assign({}, a)

console.log(b) // {id: 1, name: "Steve"}

const c = {id: 1, name: "Steve"}
const d = {...c}

console.log(d) // {id: 1, name: "Steve"}

const e = {id: 1, name: "Steve"}
const f = {...e, name: "Mike"}

console.log(f) // {id: 1, name: "Mike"}

const f = {id: 1, name: "Steve"}
const g = {...f, password: "123"}

console.log(g) // {id: 1, name: "Steve", password: "123"}
```

## Functions

---

* [Functions Intro](https://github.com/learn-co-curriculum/js-basics-functions-readme)
* [Functions Lab](https://github.com/learn-co-curriculum/js-basics-functions-lab)
* [First Class Functions](https://github.com/learn-co-curriculum/js-advanced-functions-first-class-functions-readme)
* [First Class Functions Lab](https://github.com/learn-co-curriculum/js-advanced-functions-first-class-functions-lab)

---

Arrow functions were introduced in ES6, so there are now a variety of ways to
declare a function. All 3 of the below functions are valid:

```
function sayHi() {
	return "hi"
}

const sayHi2 = function() {
	return 'hi'
}

const sayHi3 = () => {
	return 'hi'
}

sayHi();
sayHi2();
sayHi3();
```

One difference to note: if you're assigning a function to a `let` or `const`,
the function will be initialized and assigned when called, making it only
accessible _after_ it is defined. Declaring a function in the traditional form,
`function sayHi() {...}`, will hoist and initialize the function at the
beginning of the execution context, making it available throughout the scope.

#### Arrow Functions

Arrow functions provide a shorter way to declare functions, while also
providing some additional features. All three of the following function
definitions return the same value:

```
const a = () => {
	const x = 'hi'
	return x
}
const b = () => (
	const x = 'hi'
	x
)
const c = () => 'hi'
```

Using `{ }` in an arrow function requires an explicit `return` statement to
indicate which value should be returned. Using `( )` instead allows for the
implicit return of the last line. For single line functions, no parentheses or
curly brackets are needed, the function will return the value of the statement.

#### Anonymous Functions and Immediately Invoked Function Expressions

There are often times when we need to declare a function for a specific use,
but do not need to assign it a name. In these cases, we use 'anonymous'
functions:

```
const a = [1,2,3]

//normal function declaration
const addOne = element => {
	element+1
}

//to use this function in a map, we pass in the definition
const b = a.map(addOne) // b === [2,3,4]

//with an anonymous function, we define the function in the same line
const c = a.map(element => element + 1) // c === [2,3,4]
```

Immediately Invoked Function Expressions are a type of anonymous function that
is defined and called immediately:

```
// normal arrow function definition and call on two lines
const a = () => console.log('hi')
a()

//This IIFE defines and calls on the same line
(() => console.log('hi'))()
```

#### Closures

---

* [Closures](https://github.com/learn-co-curriculum/js-advanced-scope-closures-readme)
* [Closures Lab](https://github.com/learn-co-curriculum/js-advanced-scope-closures-lab)

---

In JavaScript, functions are actually a type of object, and can be returned
from a function in the same way a value can:

```
const a = () => {
	return () => {
		console.log('hi')
	}
}

const b = a()

console.log(b) // outputs the definition () => {console.log('hi')}

b() // outputs 'hi'
```

In the above example, b is assigned the definition of the returned function in
`a()`. This may seem redundant, but it's actually one of the most powerful
features of JavaScript! Closures have a special ability: any variables declared
in the same scope as the function being returned will be stored as well.

```
const a = () => {
	const x = 5
	return (y) => {
		console.log(x+y) // x is defined in the closure, y is an input for the returned function
	}
}

const b = a()
b(2) // outputs 7, 5 + 2
const c = a()
c(3) // outputs 8, 5 + 3
```

The variable `x` can be considered a sort of 'private' variable. It can't be
accessed directly, but can be read, and if declared using `let`, modified.

## Your Challenge

Let's put these concepts to use and practice some of the fundamentals...
