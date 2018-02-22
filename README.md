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

```javascript
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

```javascript
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

```javascript
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

```javascript
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

```javascript
const x // SyntaxError: Missing initializer in const declaration

const a = 10
console.log(a) // 10

a = 11 // TypeError: Assignment to constant variable.
```

Since `const` and `let` are both block scoped, we can use the two in similar situations. The `const` variable is bound to the scope of each iteration in a loop (it is redefined each loop), so, although we can't change the value once declared, we can still use them:

```javascript
for (let i = 0; i < 5; i++) {
	const timer = performance.now()
	console.log(timer) // Outputs the time in milliseconds each loop
}

console.log(timer) // ReferenceError: timer is not defined
```

When assigning to a `const` variable a value, such as `const a = 5`, `a`
_contains_ the value `5`. If we assign an object to a `const`, instead of assigning a value, the variable points to a place in memory where that object's data is stored. This means that while a `const` value can't be redefined, the underlying objects they may reference are still mutable:

```javascript
const humans = []
console.log(humans) // outputs []
humans.push('Steve')
console.log(humans)  // outputs ['Steve']
```

#### When to Use `const`

Using `const` on any variables you know you won't need to redefine can help
prevent unforeseen errors, such as conflicting name assignments. When you use
`const`, you're also indicating to future readers of your code that this
variable is meant to be fixed.

It is often the best practice to default to using this strictest scope you can
when declaring variables; if a `let` works in place of a `var`, use `let` to
keep your variable only within the scope you need. If the variable should
never be reassigned after declaration, then use `const`.

#### Summary

In general, we want to be 'strict' with our `var`, `let`, `const` usage, that is: pick the tightest bound, most restricting option available. If you aren't already in the habit of doing this, follow this logic flow when deciding what to use until it becomes second nature:
```javascript
function pickAVariableType(myVariable) {
  if ("I can use const and it works correctly") {
    return const
  } else if ("I can use let and it works correctly") {
    return let
  }
  return var
}
```

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
multiple values that stay in order. We can declare arrays in a variety of ways:

```javascript
const w = new Array // (e.g. const w = [])
console.log(w) // []
const x = new Array(5).fill("hi")
console.log(x) // [ 'hi', 'hi', 'hi', 'hi', 'hi' ]
```

Arrays can store all sorts of data types, and are useful when we need to
iterate through a collection in a specific order:

```javascript
const a = [1, 2, 3]
const b = ["a", "b", "c"]
const c = [true, true, false]
const d = [{id: 1}, {id: 2}]
const e = [ (() => console.log("hello")), (function(x) {alert(x)}) ]
```

Arrays have a number of specific methods that are very useful for reading
and manipulating collections. Most of our higher order iterators are built on [forEach](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/foreach), so make sure to review the [documentation for it](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/foreach) now:

#### [Map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)

```javascript
const a = [1, 2, 3, 4, 5]
const b = a.map(element => element + 1)

console.log(a) // [ 1, 2, 3, 4, 5 ]
console.log(b) // [ 2, 3, 4, 5, 6 ]
```

#### [Filter](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)

```javascript
const a = [1, 2, 3, 4, 5]
const b = a.filter(element => element > 3)

console.log(a) // [ 1, 2, 3, 4, 5 ]
console.log(b) // [ 4, 5 ]

const c = ["a", "b", "c"]
const d = c.filter(element => element !== "b")

console.log(c) // [ "a", "b", "c" ]
console.log(d) // [ "a", "c" ]
```

#### [Reduce](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)

```javascript
const a = [1, 2, 3, 4, 5]
const b = a.reduce((accumulator, currentValue) => accumulator + currentValue)

console.log(a) // [ 1, 2, 3, 4, 5 ]
console.log(b) // 15, the sum of all values in the array

const c = [[1], [2, 3], [4, 5]]
const d = c.reduce((accumulator, currentValue) => accumulator.concat(currentValue))

console.log(c) // [ [1], [2, 3], [4, 5] ]
console.log(d) // [ 1, 2, 3, 4, 5 ]
```

#### [Splice](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)

```javascript
const a = ["x", "y", "z"]
const b = a.splice(1, 1)

console.log(a) // [ "x", "z" ]
console.log(b) // [ "y" ]

const c = ["a", "b", "d", "e"]
const d = c.splice(2, 0, "c")

console.log(c) // [ "a", "b", "c", "d", "e" ]
console.log(d) // []
```

#### Using the Spread Operator (Destructuring) on Arrays

The spread operator is a new feature of ES6 that can be used to make a copy of
an array and in place of array concatenation:

```javascript
const a = [1, 2, 3]
const b = a

console.log(b) // [ 1, 2, 3 ]
console.log(a === b) // true, because they both reference the same object in memory

const c = [1, 2, 3]
const d = [...c]

console.log(d) // [ 1, 2, 3 ]
console.log(c === d) // false, because the spread operator has created a new object in memory

const e = [1, 2, 3]
const d = [...e, 4]

console.log(d) // [ 1, 2, 3, 4 ]
```

### Objects

Objects can contain multiple values, with each value mapped to a corresponding key:

```javascript
const a = new Object // (e.g. const a = {})
```

Objects are great for storing sets of related data, including functions.

```
const a = {name: "Steve", sayHi: () => console.log("hello")}
```

This makes objects very versatile and handy when you have complex return values.

```javascript
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

const person = returnPerson() // {id: 1, name: "Steve", sayHi: ƒ}
person.sayHi() // outputs 'hi'
```

#### Iterating Using Objects

It is possible to iterate over both the keys and values of objects:

```javascript
const a = {id: 1, name: "Steve", password: "123"}

const keys = Object.keys(a)
console.log(keys) // the object's keys: [ "id", "name", "password" ]

const values = Object.values(a)
console.log(values) // the object's values: [ 1, "Steve", "123" ]
```

#### The Advantages of Instant Lookup

As each value in an object has a corresponding [hash](https://en.wikipedia.org/wiki/Hash_function) (its key), looking up something stored in an object is instant. In contrast, looking up a value in an array requires us to iterate through the array, so the amount of time will depend on the length of the array. When unique values (keys) can be mapped to the data you would like to store (values), objects should be used over arrays for this reason. Consider the following, in which we would like to access the information about a student:

```javascript

const studentArr = [
	{id: 1, name: "Molly"},
	{id: 2, name: "Mike"}
]

const studentObj = {
	"Molly": {id: 1, name: "Molly"},
	"Mike": {id: 2, name: "Mike"}
}

// to find Mike we must iterate:
const mike = studentArr.find(student => student.name === "Mike")
// first examines {id: 1, name: "Molly"}, then {id: 2, name: "Mike"}

// to find Mike in an object:
const mike = studentObj["Mike"]
// jumps straight to {id: 2, name: "Mike"} due to the hashed nature of JavaScript object keys

```

#### Destructuring Objects

Another new feature in JavaScript is the destructuring of objects into variables named after the keys, with the corresponding values:

```javascript
const a = {id: 1, name: "Steve", password: "123"}
const { id, name, password } = a;

console.log(id, name, password) // 1 "Steve" "123"
```

This can be useful for making your code more readable and is also handy for
extracting specific values of an object being passed into a function:

```javascript
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

```javascript
const id = 1
const a = {id}
console.log(a) // outputs {id: 1}
```

#### Using the Spread Operator on Objects

When the spread operator is used on an object it returns
a copy of the object it is applied to. This can be useful when we need to
modify a specific part of an object, or add a key/value:

```javascript
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

Arrow functions were introduced in ES6. All three of the below functions are valid:

```javascript
// 1 named function
function sayHi() {
	return "hi"
}

// 2 anonymous function
(function() { return 'hi' })

// 3 anonymous function
(() => { return 'hi' })

sayHi()
sayHi2()
sayHi3()
```

While both of our anonymous function can be assigned to variables (i.e. `const a = () => { return 'hi' }`, there is an important difference between them and named functions:
* anonymous functions are initialized and assigned when the program executes the line they are on _while running_ (aka "at runtime"), making it only invokable _after_ its point of definition. Declaring a function in the traditional form, `function sayHi() {...}`, will _hoist_ the function, making it available for use throughout the scope, i.e.:

```JavaScript
x() // 'choux is a good cat'

function x() {
  console.log('choux is a good cat');
}
```

#### Arrow Functions

Arrow functions provide a shorter way to define functions, while also providing some additional features. All three of the following functions would return the same value if executed:

```javascript
() => { return 'hi' }

() => ( 'hi' )

() => 'hi'
```

In an arrow function using `{ }` does not have an explicit `return` statement, then `undefined` is returned by default. Using `( )` instead allows for the implicit return of the last expression. For single line functions, no parentheses or curly brackets are needed, the function will return the value of the expression.

#### Immediately Invoked Function Expressions

An Immediately Invoked Function Expressions (IIFE) defines and then invokes a function all in one fell swoop.

```javascript
// normal arrow function definition and call on two lines
const a = () => console.log('hi')
a()

// This IIFE defines and invokes in one expression
(() => console.log('hi'))()
```

There is no magic behind this. To understand why it is possible, and syntactically logical, answer the question: "What does a function definition _itself_ (not a function invocation!) return?"

#### Closures

---

* [Closures](https://github.com/learn-co-curriculum/js-advanced-scope-closures-readme)
* [Closures Lab](https://github.com/learn-co-curriculum/js-advanced-scope-closures-lab)

---

A closure is a fancy name for a simple implementation of JavaScript scoping rules. A closure encapsulates variables, meaning they are accessible from within the closure and not from without. Let's look at this in action:

```javascript
function a() {
	let x = 5
	return (y) => {
		console.log(x + y)
	}
}

const b = a()
b(2) // outputs 7
console.log(x) // ReferenceError: x is not defined
```

The variable `x` can be considered locked inside of the closure that function `a` forms. While it can't be accessed directly from outside of the closure, we see that it can be accessed by invoking functions that exist within the same closure that use the variable! This logically adds up: `let`'s scoping rules allow it to be accessed anywhere within its enclosing block, including children blocks/functions of that enclosing block.

## Your Challenge

These are core concepts of JavaScript that you should be seeking to master. The more second nature they become, the easier it will be develop solutions to novel problems. Think of yourself as an industrial plumbing engineer: you need to know your pipes, tools, and basic fluid dynamics in order to provide effective solutions for city wide plumbing disasters.

It is not expected that all of these concepts perfectly comfortable right now. Review the links provided and online official documentation and work your way in that direction. We find that one of the best ways to solidify these concepts is to explain them to others, so make sure to engage your peers!

Once you are ready, approach one of your instructors and walk them through these core concepts as if they know programming, but not the nuances of JavaScript. 
