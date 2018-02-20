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

There are three types of variables, `var`, `let`, and `const` that can be used
to store data. Each type acts slightly differently in regards to scope.

### Var

* Can be redefined or changed
* Function scoped - variables declared using `var` can be read or rewritten
  anywhere within the function they are declared in, including inside any nested
  blocks. If a `var` is declared outside of any function, it will be accessible
  at the global scope.
* are accessible before being assigned
* can be redeclared in the same scope

```
var a = "a"
{
	var b = "b"
}

console.log(a,b) // outputs 'b c'

var c = []
console.log(c) // outputs '[]'
var c = "hello"
console.log(c) // outputs 'hello'
```

#### When to Use `var`

The `var` variable type is useful when declaring variables that you want
accessible and changeable throughout a function.

### Let

* Can be redefined or changed
* Block scoped - variables declared using `let` can only be accessed within
  the block it is declared in.
* are not accessible before they are assigned
* Cannot be redeclared in the same scope

```
let a = "a"
{
	let b = "b"
}
//will return a reference error:
console.log(b,c)
```

Because `b` was declared inside of a block, it is not accessible to the
`console.log`. However, changing `a` inside the block will work, as `a` is
declared in the same scope (or above) the `console.log`:

```
let a = "a"
{
	a = "c"
}
//will output 'c'
console.log(a)
```

#### When to Use `let`

Using `let` gives us more options when dealing with scope, and is useful for
any variables you need within a block, such as a loop, that you do not want
escaping.

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

Using `let` in blocks keeps your function scope clear of unnecessary variables.
It also provides some slightly different functionality in closures, compared to
`var`. For example, `let` stays bound within the scope of each loop in the
following code:

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

Try replacing let with var in the code above. The output will be `5`, five
times.

### Const

* Cannot be redefined, changed or redeclared
* Block scoped - variables declared using `const` can only be accessed within
  the block.
* Must be initialized with a value

```
const a = 10
console.log(a) // 10

a = 11 // TypeError: Assignment to constant variable.

const b // SyntaxError: Missing initializer in const declaration
```

Since `const` and `let` are both block scoped, we can use the two in similar
situations. The `const` variable is bound to the scope of each iteration in a
loop, so, although we can't change the value once declared, we can still use
them:

```
for(let i = 0; i < 5; i++) {
	const timer = performance.now()
	console.log(timer) // Outputs the time in milliseconds of each console.log
}

console.log(timer) // ReferenceError: timer is not defined
```

The `const` variable can't be redefined, but it is mutable:

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
let w = new Array
console.log(w) // []
let x = new Array(5).fill("hi")
console.log(x) // ["hi","hi","hi","hi","hi"]

let y = []
console.log(y) // []
let z = ["hello"]
console.log(z) // ["hello"]
```

Arrays can stored all sorts of data types, and are useful when we need to
iterate through a list in a specific order:

```
let a = [1,2,3]
let b = ["a","b","c"]
let c = [true, true, false]
let d = [{id: 1}, {id: 2}]
let e = [() => console.log("hello"), () => alert("world")]
```

Arrays have a number of specific methods that are very useful for reading
and manipulating lists:

#### [Map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)

```
let a = [1,2,3,4,5]
let b = a.map(element => element + 1)

console.log(a) // [1,2,3,4,5]
console.log(b) // [2,3,4,5,6]
```

#### [Filter](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)

```
let a = [1,2,3,4,5]
let b = a.filter(element => element > 3)

console.log(a) // [1,2,3,4,5]
console.log(b) // [4,5]

let c = ["a", "b", "c"]
let d = c.filter(element => element !== "b")

console.log(c) // ["a", "b", "c"]
console.log(d) // ["a", "c"]
```

#### [Reduce](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)

```
let a = [1,2,3,4,5]
let b = a.reduce((accumulator, currentValue) => accumulator + currentValue)

console.log(a) // [1,2,3,4,5]
console.log(b) // 15, the sum of all values in the array

let c = [[1], [2, 3], [4, 5]]
let d = c.reduce((accumulator, currentValue) => accumulator.concat(currentValue))

console.log(c) // [[1], [2, 3], [4, 5]]
console.log(d) // [1, 2, 3, 4, 5]
```

#### [Splice](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)

```
let a = ["x","y","z"]
let b = a.splice(1,1)

console.log(a) // ["x", "z"]
console.log(b) // ["y"]

let c = ["a","b","d","e"]
let d = a.splice(2,0,"c")

console.log(c) // ["a","b","c","d","e"]
console.log(d) // []
```

#### Using the Spread Operator on Arrays

The spread operator is new feature of ES6 that can be used to make a copy of
an array and in place of array concatenation:

```
let a = [1,2,3]
let b = a

console.log(b) // [1,2,3]

let c = [1,2,3]
let d = [...c]

console.log(d) // [1,2,3]

let e = [1,2,3]
let d = [...e, 4]

console.log(d) // [1,2,3,4]
```

### Objects

Objects, like arrays, can contain multiple values, but instead of storing
them in a list, each value is store with a corresponding key:

```
let a = new Object // a === {}
let b = {} // b === {}
```

Objects are great for storing sets of related data, including functions.

```
let a = {name: "Steve", sayHi: () => console.log("hello")}
```

This makes objects very versatile and handy when you have complex return values.

#### Iterating Using Objects

It is possible to iterate over the values in any object like an array using
Object.keys():

```
let a = {id: 1, name: "Steve", password: "123"}
let b = Object.keys(a)
console.log(b) // ["id", "name", "password"]

let c = b.map(element => a[element])
console.log(c) // [1, "Steve", "123"]
```

#### The Advantages of Instant Lookup - O(1)

Because each value in an object has a corresponding key, looking up something
stored in an object is instant. Arrays on the other hand, are O(n), meaning the
amount of time it takes to look through and find a value in an array depends on
the length of the array. When dealing with large sets of data, even a list, it
is more performant to use objects:

```
let a = [{id: 1, name: "Steve"}, {id: 2, name: "Mike"}]
let b = {"Steve": {id: 1, name: "Steve"}, "Mike": {id: 2, name: "Mike"}}

// to find Mike the array above, you must iterate through it:
let c = a.find(element => element.name === "Mike")

// to find Mike in object:
let d = b["Mike"]
```

#### Destructuring Objects

Another new feature in JavaScript is the destructuring of objects into
variables assigned to the objects values:

```
let a = {id: 1, name: "Steve", password: "123"}
const { id, name, password } = a;

console.log(id, name, password) // 1 "Steve" "123"
```

This can be useful for making your code more readable and is also handy for
extracting specific values of an object being passed into a function:

```
let a = {id: 1, name: "Steve", password: "123"}

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
let id = 1
let a = {id}
console.log(a) // {id: 1}
```

#### Using the Spread Operator on Objects

When the spread operator is used on an object, like arrays, it creates returns
a copy of the object it is applied to. This can be useful when we need to
modify a specific part of an object, or add a key:

```
let a = {id: 1, name: "Steve"}
let b = Object.assign({}, a)

console.log(b) // {id: 1, name: "Steve"}

let c = {id: 1, name: "Steve"}
let d = {...c}

console.log(d) // {id: 1, name: "Steve"}

let e = {id: 1, name: "Steve"}
let f = {...e, name: "Mike"}

console.log(f) // {id: 1, name: "Mike"}

let f = {id: 1, name: "Steve"}
let g = {...f, password: "123"}

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
declare a function. All 3 functions below operate the same:

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
accessible _after_ it is defined. Declaring a function in the traditional form
(`function sayHi() {...}`) will hoist and initialize the function at the
beginning of the execution context, making it available throughout the scope.

#### Arrow Functions

Arrow functions provide a shorter way to declare functions, while also
providing some additional features. All three of the following function
definitions return the same value:

```
let a = () => {
	let x = 'hi'
	return x
}
let b = () => (
	let x = 'hi'
	x
)
let c = () => 'hi'
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
let a = [1,2,3]

//normal function declaration
let addOne = (element) => {
	element+1
}

//to use this function in a map, we pass in the definition
let b = a.map(addOne) // b === [2,3,4]

//with an anonymous function, we define the function in the same line
let c = a.map((element) => element + 1) // c === [2,3,4]
```

Immediately Invoked Function Expressions are a type of anonymous function that
is defined and called immediately:

```
// normal arrow function definition and call on the next line
let a = () => console.log('hi')
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
let a = () => {
	return () => {
		console.log('hi')
	}
}
let b = a()
console.log(b) // outputs the definition () => {console.log('hi')}
b() // outputs 'hi'
```

In the above example, b is assigned the definition of the returned function in
`a()`. This may seem redundant, but it's actually one of the most powerful
features of JavaScript! Closures have a special ability: any variables declared
in the same scope as the function being returned will be stored as well.

```
let a = () => {
	let x = 5
	return (y) => {
		console.log(x+y) // x is defined in the closure, y is an input for the returned function
	}
}

let b = a()
b(2) // outputs 7, 5 + 2
let c = a()
c(3) // outputs 8, 5 + 3
```

The variable `x` can be considered a sort of 'private' variable. It can't be
accessed directly, but can be read or modified.
