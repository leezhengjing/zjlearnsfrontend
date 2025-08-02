---
layout: post
title: "javascript data structures"
date: 2025-08-02 01:38:00 +0800
categories: thoughts
---

# Javascript Primer
The de-facto programming language for frontend, JavaScript. If you told me to write some JS code for you now, I probably couldn't.

So this first post will be dedicated to me learning about the JS language. 

The material in this post heavily references Getting Started with Javascript by Kyle Simpson and Algomonster's Javascript Cheatsheet.

Just want to preface that any content in my blog posts are largely my thoughts. I will do my best to ensure their correctness by googling and reading documentation, but I will likely have some gaps in my CS knowledge as I ramble on. If you see anything weird, do reach out to me.

## Values
Values are the basic building blocks of every programming language. Let's see what Javascript offers.

### Primitives
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

### Objects

```javascript
[1, 2, 3] // classic array
{ name: "Zheng Jing" } // and classic Javascript objects
```

## Operations

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

## Types
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
## Variable
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
