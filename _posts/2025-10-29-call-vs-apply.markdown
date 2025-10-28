---
layout: post
title: "Implement flatten"
date: 2025-10-28 00:00:00 +0800
categories: javascript, typescript, coding
math: true
---

# Question

What is the difference between `.call` and `.apply` in Javascript?

## Write-up

`.call` and `.apply` are both used to invoke functions with a specific `this` context and arguments.
The primary difference lies in how they accept arguments:

- `.call(thisArg, arg1, arg2, ...)`: Takes arguments individually.
- `.apply(thisArg, [argsArray])`: Takes arguments as an array.

Assuming we have a function `add`, the function can be invoked using `.call` and `.apply` in
the following manner:

```typescript
function add(a, b) {
  return a + b;
}

console.log(add.call(null, 1, 2)); // 3
console.log(add.apply(null, [1, 2])); // 3
```

An easy way to remember this is C for comma separated and A for array of arguments.

With ES6 syntax, we can invoke `call` using an array along with the spread operator for the arguments.

```javascript
function add(a, b) {
  return a + b;
}

console.log(add.call(null, ...[1, 2]));
```

### Use cases

1. Context Management
   `.call` and `.apply` can set the `this` context explicitly when invoking methods on different objects.

```typescript
const person = {
  name: "John",
  greet() {
    console.log(`Hello, my name is ${this.name}`);
  },
};

const anotherPerson = { name: "Alice" };

person.greet.call(anotherPerson);
person.greet.apply(anotherPerson);
```

### Function borrowing

Both `.call` and `.apply` allow borrowing methods from one object and using them in the context of another.

```typescript
function greet() {
  console.log(`Hello, my name is ${this.name}`);
}

const person1 = { name: "John" };
const person2 = { name: "Alice" };

greet.call(person1); // Hello, my name is John
greet.apply(person2); // Hello, my name is Alice
```

### Alternative syntax to calling methods on objects

`.apply` can be used with object methods by passing the object as the first argument followed by the
usual parameters.

```typescript
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];

Array.prototype.push.apply(arr1, arr2); // Same as arr1.push(4, 5, 6)

console.log(arr1); // [1, 2, 3, 4, 5, 6]
```

Deconstructing the above:

1. The first object, `arr1` will be used as the `this` value.
2. `.push()` is called on `arr1` using `arr2` as arguments as an array because its using .apply().
3. `Array.prototype.push.apply(arr1, arr2)` is equivalent to `arr1.push(...arr2)`.

Lastly, it may not be obvious, but `Array.prototype.push.apply(arr1, arr2)` causes modification to `arr1.`
It's clearer to call methods using the OOP-centric way instead where possible.
