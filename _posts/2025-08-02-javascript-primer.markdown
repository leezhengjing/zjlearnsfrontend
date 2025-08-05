---
layout: post
title: "javascript data structures"
date: 2025-08-02 01:38:00 +0800
categories: thoughts
math: true
---

## Javascript Primer
The de-facto programming language for frontend, JavaScript. If you told me to write some JS code for you now, I probably couldn't.

So this first post will be dedicated to me learning about the JS language. 

The material in this post heavily references Getting Started with Javascript by Kyle Simpson and Algomonster's Javascript Cheatsheet.

Just want to preface that any content in my blog posts are largely my thoughts. I will do my best to ensure their correctness by googling and reading documentation, but I will likely have some gaps in my CS knowledge as I ramble on. If you see anything weird, do reach out to me.

### Values
Values are the basic building blocks of every programming language. Let's see what Javascript offers.

#### Primitives
```javascript
// Numbers, both of them are the same type in JS!
42
3.14

// Classic string
"Hello world"

// Boolean
true
false

// Interestingly, there are two "nothing" values
null
undefined
```

#### Objects

```javascript
[1, 2, 3] // classic array
{ name: "Zheng Jing" } // and classic Javascript objects
```

### Operations

We have the usual binary operators like + and -, and unary operators like !.

Uno, dos, tres? (Flexing my Spanish 1k)

```javascript
1 + 5 // Some basic arithmetic, between the left and right operands.
43 - 1

"Zheng " + "Jing" // String concatenation

// Fancy term in programming, overloading! The + operator is overloaded here.

!false //

3.0 == 3 // Comparison, we've got two in Javascript! This is the loose equality operator.
// Basically asking, are these two values equal to each other?
3.0 === 3 // Triple equals is very similar to the the Object.is method, where if we were to compare two different Objects, they must point to the same thing. There are some key differences though, which will be covered later.

3 < 4 // less than
3 > 4 // greater than

true || false // or operator
true && false // and operator

```

### Types
typeof is actually an unary operator, and we can use it on some values in Javascript to see what type they are.
```javascript
typeof 42 // "number"

typeof "Zheng Jing" // "string"

typeof true // "boolean"

typeof undefined // "undefined"

typeof { age: 39 } // "object"

typeof null // "object"

typeof [1, 2, 3] // "object"

```
### Variable
A variable is a place in memory, a symbolic representation, something like a "pointer" or "address" to some place in our computer memory.

Let's see how we declare variables in javascript.

```javascript
var name = "Zheng Jing";

var age;
age = 39;

var friends = [ "Kurt", "Si Yuan" ];

console.log(friends.length);
console.log(friends[1]);
```

### Expressions and Statements
Statements end with a semi-colon, expressions are part of statements. Quick exercise, how many expressions are in this code example?
```javascript
var age = 24;

age = 1 + (age * 2);
```
In line 1, there is an assignment expression `age = 24`. 

In line 3, there are actually 6 expressions! Each literal is actually one expression, so 1 is an expression, 2 is an expression and age is also an expression. Then there are the addition and multiplication expression, and finally the assignment expression.

### Decisions
if statements, how do they look in Javascript?
```javascript
var age = 24;
if (age >= 18) {
	goArmy();
}

if (isEmployed()) {
	wakeUpForWork();
} else {
	sleepIn();
}
```

### Loops
This is important.
```javascript
var students = [ /*..*/ ];
for (let i = 0; i < students.length; i++) {
	greetStudent(students[i]);
}
// Looks exactly like a C++ for loop! You have your initialize counter, a condition to continue the loop, and an expression to increment ourcounter to ultimately break out of our loop.

for (let student of students) {
	greetStudent(student);
}

while (students.length > 0) {
	let students = students.pop();
	greetStudent(student);
}
```

### Functions
The idea of grouping code into a reusable procedure. A collection of things we want to do.

The word function also exists in the world of Math, remember something like $y = f(x)$. This kind of implies returning something from the function, as we assign that returned value to $y$. In programming, not all functions return something.
```javascript
function greetStudent(student) {
	console.log(
		`Hello, ${student.name}.` // This is an interpolated string, where we can insert other variable values in using $ and curly braces.
	)
}

function timeRemaining(timeElapsed, endTime) {
	return endTime - timeElapsed;
}

```

## Exercises

### Instructions

1. Define an `addFavoriteBook(..)` function that receives a single parameter, called `bookName`.

2. If the provided `bookName` string does *NOT* have the word "Great" in it, add it to the `favoriteBooks` array.

	Hints:

	- `someString.includes(anotherString)` will return `true` if `anotherString` is found inside `someString`, or `false` otherwise.

	- Use `!` to negate a boolean value (change `true` to `false` or vice versa).

	- `someArray.push(value)` will add a value to the end of the array.

3. Define a `printFavoriteBooks()` function that receives no parameters.

4. `printFavoriteBooks()` should first print a message like "Favorite Books: ..", and include the number of books in the `favoriteBooks` array.

	Hint:

	- Use the \` back-tick operators for strings that need to include values in them.

	- Use `console.log(..)` to print a message to the screen.

5. Finally, `printFavoriteBooks()` should loop through the `favoriteBooks` array and print out each value.

	Make sure to then call the `printFavoriteBooks()` function at the end of the program.

	Hint: Use the `for ( let .. of .. ) { }` style loop.



```javascript
// TODO: define addFavoriteBook(..) function
function addFavoriteBook(bookName) {
	if (!bookName.includes("Great")) {
		favoriteBooks.push(bookName);
	}
}

// TODO: define printFavoriteBooks() function
function printFavoriteBooks() {
	console.log(`Favorite Books: ${favoriteBooks.length}`);

	for (let bookName of favoriteBooks) {
		console.log(bookName);
	}
}

var favoriteBooks = [];

addFavoriteBook("A Song of Ice and Fire");
addFavoriteBook("The Great Gatsby");
addFavoriteBook("Crime & Punishment");
addFavoriteBook("Great Expectations");
addFavoriteBook("You Don't Know JS");

// TODO: print out favorite books
printFavoriteBooks();
```

## Types & Coercion
### Primitive Types
Kind of mentioned in values, but let's consolidate.

Primitive types in Javascript:
- undefined
- string
- number
- boolean
- object
- symbol

Debatable:
- null. This is actually a primitive type in JS, but if you hit `typeof`, you get an object. Weird!

Objects in Javascript:
- function. This is a subtype of the object type.
- object

Key mechanic of JS, variables don't have types. Only values do. This is due to the dynamically typed nature of JS.

```javascript
var v;
typeof v; // "undefined"
v = "1";
typeof v; // "string"
v = 1
typeof v; // "number"
v = false;
typeof v; // "boolean"
v = {};
typeof v; // "object"
v = Symbol();
typeof v; // "symbol"
```
If you try `typeof` and a variable that has never been declared, it will also give "undefined"!

```javascript
typeof doesntExist; // "undefined"

var v = null;
typeof v; // "object"

v = function(){};
typeof v; // "function"

v = [1, 2 ,3];
typeof v; // "object"
```

That's weird, if everything is an objcet, how can we distinguish values beyond just objects? We have some built in JS methods, which we will explore later.

### NaN
NaN is a special value that indicates that we've had an invalid numerical operation of some sort.
```javascript
var greeting = "Hello, class!";

var something = greeting / 2; // ??!??!?
something; // NaN
Number.isNaN(something); // true
```

### Fundamental Objects
These were historically copied from a programming language like Java, which we have in Javascript too. JS created object wrappers around these values, and we want to use the new keyword to instantiate instances of those.

We also have other fundamental objects where we don't want to use the `new` keyword, we want to use them as functions.

| ✅ Use `new` | ❌ Don't use `new`|
|--------------|------------------|
| `Object()`               | `String()` |
| `Array()`                | `Number()` |
| `Function()`             | `Boolean()`|
| `Date()`                 |            |
| `RegExp()`               |            |
| `Error()`                |            |

```javascript
var yesterday = new Date("August 2, 2025");
yesterday.toUTCString();

var myCAP = String(4.15); // 4.15
```

## Coercion (Converting of Types)
All languages require conversion of types, and in a dynamically typed language like JS, we introduce the concept of coercion.

### Example 1: String concatenation
An implicit coercion of numStudents into a string in order to perform string concatenation.
```javascript
var msg1 = "There are ";
var numStudents = 16;
var msg2 = " students.";
console.log(msg1 + numStudents + msg2); // There are 16 students.
console.log(`There are ${numStudents+""} students.` // Also implicit
```
In Javascript, it always prefers string concatenation if any operands are of the string type.

```javascript
function addAStudent(numStudents) {
	return numStudents + 1;
}

addAStudent(
	Number(studentsInputElem.value)
);
```

### Booleans
On top of the standard booleans, in JS there's this concept of `falsy` and `truthy`. Falsy values will be converted to the false boolean, and truthy values will be converted to the true boolean, if there is a type coercion.

Apart from the small list of `falsy` values, everything else in Javascript is `truthy`.

`falsy` values include: `""`, `0`, `-0`, `null`, `NaN`, `false` and `undefined`.

```javascript
if (studentsInputElem.value) {
	numStudents = Number(studentsInputElem.value);
}
while (newStudents.length) {
	enrollStudents(newStudents.pop());
}

// explicit coercion
if (!!studentsInputElem.value) {
	numStudents = Number(studentsInputElem.value);
}
while (newStudents.length > 0) {
	enollStudents(newStudents.pop());
}
```
A case where implicit conversion could be good in making things less cluttered.
```javascript
var workshopEnrollment1 = 16;
var workshopEnrollment2 = workshop2Elem.value;

if (Number(workshopEnrollment1) < Number(workshopEnrollment2)) {
	// ...
}

if (workshopEnrollment1 < workshopEnrollment2) { // lt and gt automatically coerces into numbers, unless both are strings then there is some alphanumerical comparison
	// ... 
}
```

### Coercion Best Practices
> "If a feature is sometimes useful and sometimes dangerous and if there is a better option  
> then always use the better option."  
>   
> — *"The Good Parts"*, Crockford

A lot of parts of this quote is lacking defintions, like what is useful, what is dangerous and what is better?

To answer that question:
- __Useful__: when the reader is focused on what's important
- __Dangerous__: when the reader is focused on smth but can't tell what will happen
- __Better__: when the reader understands the code

### Equality
Many explain the equal operators as follows:

`==` checks value (loose)

`===` checks value and type (strict)

In actuality, this is wrong, and the real explanation would be:

`==` allows coercion (type different)

`===` disallows coercion (type same)

In all cases (zero edge cases), when two variables are the same type already, if double equals returns true, triple return also returns true.
```javascript
var studentName1 = "Frank";
var studentName2 = `${studentName1}`;

var workshopEnrollment1 = 16;
var workshopEnrollment2 = workshopEnrollment1 + 0;

studentName1 == studentName2;
studentName1 === studentName2;

workshopEnrollment1 == workshopEnrollment2;
workshopEnrollment1 === workshopEnrollment2;
```

```javascript
var workshop1 = { topic: null };
var workshop2 = {};

if (
	(workshop1.topic === null || workshop1.topic === undefined) &&
	(workshop2.topic === null || workshop2.topic === undefined)
) {
	// ...
}

// functionally equivalent, arguably better code as it is more readable
// and focused on the right thing: whether workshop is empty
// javascript coerces null to undefined vice versa
if (
	workshop1.topic == null &&
	workshop2.topic == null
) {
	// ...
}
```

> `==` is not about comparison with unknown types. `==` is about comparisons with known type(s). Optionally, where conversions are helpful.
>
> — *"Getting Started with Javascript, v2"*, Kyle Simpson

## Scope
### Scope
What is scope? It means where to look for things, be it variables, function definitions, you name it. If you've gone through your first intro to programming class, CS1101S flashback in NUS, you would know this very well from the programming quizzes they made you do in source.

But each programming language handles scope slightly differently, and I was shocked at how JS does it. Let's take a look below:
```javascript
var teacher = "Kyle";

function otherClass() {
	teacher = "Suzy";
	topic = "React";
	console.log("Welcome!");
}

otherClass(); // Welcome!

teacher; // ??
topic; // ??
```
What do you think the return result is?

The answer is, teacher and topic returns "Suzy" and "React"! This might come as a shock for you, because for me, I thought it would be "Kyle" and undefined. This doesn't make sense right? the function scope should be like a "local" scope, while the global scope where teacher has been declared as "Kyle" should remain untouched by the function call. But not in JS, apparently since it cant be declared in the scope of otherClass, it gets bumped up to the global scope. Crazy!

### Undefined vs Undeclared
A state of a variable being undeclared is distinctly different from something that is undefined. Something that is undefined is a variable that has been declared but doesn't have a value. A variable that has never been declared, the javascript engine has no idea where it is.

### Function Expressions
What is a function expression?

It is a function that is assigned as a value. This allows functions to be assigned to variables, passed as arguments or even returned from other functions. This is a first-class value in a programming language.

```javascript
// Anonymous function expression
var clickHandler = function() {
	// ..
}

// Named function expression
var keyHandler = function keyHandler() {
	// ..
}

// Typically, we see anonymous function expressions more in the form of arrow functions!
var ids = people.map(person => person.id);

var ids = people.map(function getId(person){
	return person.id;
});

getPerson()
.then(person => getData(person.id))
.then(renderData);

getPerson()
.then(function getDataFrom(person){
	return getData(person.id);
})
.then(renderData);
```

### Function Scoping with IIFEs
Immediately invoked function expressions. The main end result of running a IIFE is to get a new block of scope, aka a function scope. Take a look at the example below:
```javascript
var teacher = "Kyle";

( function anotherTeacher() {
	var teacher = "Suzy";
	console.log(teacher); // Suzy
} )(); // immediately executed!

console.log(teacher) // Kyle
```

### Block Scoping with `let`
This is probably the most common way of creating scope that I see in my day to day work. The `let` keyword. This enables block scoping!
```javascript
var teacher = "Kyle";

{
	let teacher = "Suzy";
	console.log(teacher); // Suzy
}

console.log(teacher); // Kyle
```
Another example:
```javascript
function diff(x, y) {
	if (x > y) {
		let tmp = x; // tmp is only available in this curly block!
		x =  y; // x doesnt exist in this block, goes up one scope to find the x
		y = tmp; // same
	}
	return y - x;
	

}
```

```javascript
function repeat(fn, n) {
	var result; // still use var here, stylistic choice when we dont need block scope

	for (let i = 0; i < n; i++) {
		result = fn(result, i);
	}

	return result;
}

```

```javascript
function formatStr(str) {
	{ let prefix, rest;
		prefix = str.slice(0, 3);
		rest = str.slice(3);
		str = prefix.toUpperCase() + rest;
	}
	
	if (/^FOO:/.test(str)) {
		return str;
	}
	return str.slice(4);
}

```
### Closure
> "You really can't get closure unless you understand the scope that goes underneath it."
Just thought it was a pretty funny quote.

Definition: Closure is when a function "remembers" the variables outside of it, even if you pass the function somewhere.
- The key thing is that its accessing variables in an outer scope.
- So what happens when we pass this function elsewhere, where it enters a different scope?

```javascript
function ask(question) {
	setTimeout(function waitASec() {
		console.log(question); // we say that the function waitASec has closure over the question variable.
	}, 100);
}

ask("What is a closure?");
```
Normally, if you think about it, once ask() is called, and then it calls setTimeout(), ask has already finished and should delete all its variables, including question. But because setTimeout still has that 100ms with waitASec in its memory and waitASec references question and has closure over the question variable, it keeps the scope and hence the variables alive.

```javascript
function ask(question) {
	return function holdYourQuestion() {
		console.log(question);
	};
}

var myQuestion = ask("What is closure?");

// ...

myQuestion(); // What is closure?
```

## this & Prototypes
### this - dynamic context
A function's this references the execution context for the call, determined entirely by how the function was called.

A this-aware function can thus have a different context each time its called, which makes it more flexible & reusable.

```javascript
var workshop = {
	teacher: "Kyle",
	ask(question) {
		console.log(this.teacher, question);
	},
};

workshop.ask("What is implicit binding?");
// Kyle What is implicit binding?
}
```
So it might appear that this refers to the workshop in its definition, so it will always return Kyle What is implicit binding?. But it is actually only because of the way we executed the call, and then it will look for an implicit binding. Since we did `workshop.ask`, there is an implicit binding of the ask function to the workshop object. This is more obvious in the following example, where we have a this aware function.

```javascript
function ask(question) {
	console.log(this.teacher, question);
}

function otherClass() {
	var myContext = {
		teacher: "Suzy"
	};
	ask.call(myContext, "Why?"); // Suzy Why? 
}

otherClass();
```
In line 9, we introduce a new way of calling the this-aware function, `ask.call`, telling it to use `myContext` object as the this keyword.

### Prototypes
How classes in Javascript actually works under the hood! and how to use prototype add methods to the class definition.

creating a this aware function turns it into a constructor. To add methods into the defintiion of the workshop class, you add it to the prototype of the the workshop.

A prototype means it is an object where any instances are going to be linked to/delegated to.

The new keyword is going to invoke the Workshop function, and the object that gets created is going to be linked to Workshop.prototype. Since the prototype has an ask method on it, on line 11, the deepJS instance can call .ask().

It is important to see that deepJS (the object) does not have an ask method. But instead it is prototype linked to workshop.prototype. So when we do deepJS.ask, we go up the prototype chain by one level up to Workshop.prototype. Then when we invoke the ask() function on deepJS, we invoke it with the this context of the deepJS object.

When we invoked workshop to create deepJS, it ran that function workshop, and when it was running the this keyword, it was pointing at teacher which was the object we gave to deepJS.

So when we invoke ask(), and from line 11 to line 5 we see this.teacher, its pointing to deepJS.teacher. On line 14 -> line 5, we are saying reactJS.teacher.
```javascript
function Workshop(teacher) {
	this.teacher = teacher;
}

Workshop.prototype.ask = function(question) {
	console.log(this.teacher,question);
}

var deepJS = new Workshop("Kyle");
var reactJS = new Workshop("Suzy");

deepJS.ask("Is 'prototype' a class?");

reactJS.ask("Isn't 'prototype' ugly?");
```

### Classes
Now that we understand the prototype system and the `this` keyword, we now explore class keyword, which is layered on top of the prototype system. It gives us some syntax that we recognise as the usual class stuff with other programming languages.

This was introduced with ES6.

```javascript
class Workshop {
	constructor(teacher) {
		this.teacher = teacher;
	}
	ask(question) {
		console.log(this.teacher, question);
	}
}

var deepJS = new Workshop("Kyle");
var reactJS = new Workshop("Suzy");

deepJS.ask("Is 'class' a class?");

reactJS.ask("Is this class OK?");

```

## Exercise - Three Pillars of JS

This is an exercise to briefly practice the three pillars of JS: Types / Coercion, Scope / Closures, and `this` / Prototypes.

### Instructions

The code of this exercise can be executed via Node.js or in the console tab of your browser's developer tools.

1. In the `printFavoriteBooks()` function, make sure there's no accidental type conversion (ie, from number to string).

	Hint: Use `String(..)` to coerce something to a string type.

2. Move the `addFavoriteBook(..)` and `printFavoriteBooks()` functions into the `Bookshelf` class as methods. Modify them so they use the `this` keyword to access the `favoriteBooks` array.

	Hint: `class` methods don't use the `function` keyword, just their name.

3. Fill out the definition of the `loadBooks(..)` function, which should receive an instance of the `Bookshelf` class that you will pass to it.

4. `loadBooks(..)` should call the provided `fakeAjax(..)`, using `BOOK_API` as the URL and an inline function expression as the callback.

5. The callback will be passed an array of book names. Loop through this array, passing each book name to the `addFavoriteBook(..)` method of the `Bookshelf` instance passed to `loadBooks(..)`. Then call the `printFavoriteBooks()` method.

6. Create an instance of `Bookshelf` class, and pass it as an argument to `loadBooks(..)`.

	Hint: Class instantiation: `new Whatever()`.

```javascript
class Bookshelf {
	constructor() {
		this.favoriteBooks = [];
	}

	// TODO: define methods `addFavoriteBook(..)`
	// and `printFavoriteBooks()`
	addFavoriteBook(bookName) {
		if (!bookName.includes("Great")) {
			this.favoriteBooks.push(bookName);
		}
	}

	printFavoriteBooks() {
		console.log(`Favorite Books: ${String(this.favoriteBooks.length)}`);
		for (let bookName of this.favoriteBooks) {
			console.log(bookName);
		}
	}
}

function loadBooks(bookShelf) {
	// TODO: call fakeAjax( .. );
	fakeAjax(BOOK_API, (arr) => {
		for (const bookName of arr) {
			bookShelf.addFavoriteBook(bookName);
		}
		bookShelf.printFavoriteBooks();
	});
}

var BOOK_API = "https://some.url/api";


// ***********************

// NOTE: don't modify this function at all
function fakeAjax(url,cb) {
	setTimeout(function fakeLoadingDelay(){
		cb([
			"A Song of Ice and Fire",
			"The Great Gatsby",
			"Crime & Punishment",
			"Great Expectations",
			"You Don't Know JS"
		]);
	},500);
}
var myBooks = new Bookshelf();
loadBooks(myBooks);

```


## Basic Data Structures
I think one way to learn the syntax for a programming language is to get familiar with the data structures you can use, and put em to test in some leetcode questions :). 

### Arrays
Based on some quick research, arrays in JavaScript are dynamically-sized, so the underlying JavaScript engine (more on this in the future!) handles the array resizing for you (memory allocation and copying elements when the array needs to be expanded or contracted).

```javascript
const arr = [0, 1, 2, 3, 4, 5]

```
If you are familiar with other programming languages like Java or C++, arrays are fixed-size, meaning you would have to declare the type and size of the array when instantiating them. We know this is because traditionally, arrays as a data structure would just be a contiguous block of allocated memory. To perform operations on a contiguous block of memory, we would need to know its initial memory location, and to access individual elements in the array, we would need to know the byte size of each element (aka the type) in order to add to that initial memory address.

Enough rambling, let's see how we can do some common operations in Javascript. I use python for most of my leetcode practice, and common uses would be accessing the array, appending to it, and maybe performing some slicing.
```javascript
const arr = [0, 1, 2, 3, 4, 5]
let subarray = arr.slice(1, 3);
// console.log(subarray) -> [1, 2], same as python indexing, inclusive left and exclusive right
subarray = arr.slice(-2);
// console.log(subarray) -> [4, 5], we can do this as well to slice 2 elements from the last index
```

Some other useful array methods:

```javascript
arr.length
// returns the size of the array
arr.push(6)
// appends the item and returns the size of the new array, amortized O(1)
arr.pop()
// removes and returns the last element of the array, O(1)
arr.shift()
// removes and returns the first element of the array, O(n)
arr.unshift(1)
// takes in an item, adds item to the start of the array and returns the new array length, O(n)
arr.splice(start_index, count_to_remove, add_item1, add_item2, ...) 
// removes and returns count_to_remove item(s) from an array given their index and (optionally) replaces them with add_items, O(n)
```

After running all those commands, I noticed that I was actually modifying arr when it was a const! So it appears that we can run these array methods on the const, but we can't reassign a new array to arr.


Looping through an array:

```javascript
const arr = [1, 2, 3, 4, 5]

// Method 1: Looks like a C++ for loop
for (let i = 0; i < arr.length; i++) {
	const num = arr[i];
	console.log(num)
}

// Method 2: Built in forEach array method, gets the item and index
arr.forEach(function(item, index) {
	console.log(`${item} ${index}`);
});

// Method 3:
for (const num of arr) {
	console.log(num);
}

```

### Linked Lists
