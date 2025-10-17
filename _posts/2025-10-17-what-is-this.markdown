---
layout: post
title: "what is `this` in Javascript?"
date: 2025-10-17 01:38:00 +0800
categories: javascript, trivia
math: true
---

# Explain what is `this` in Javascript

> It is the dynamic reference to the context in which a function is called.

## What are the seven different scenarios that `this` behaves differently?

1. Using the `new` keyword with a function constructor, the `this` inside the function refers to the newly created object.
2. Using the `new` keyword with a class constructor, the `this` inside the `constructor` refers to the newly created object.
3. Using `call(obj)`, `apply(obj)` and `bind(obj)` to set a function's `this` with the wrapped object that's passed in as an argument.
4. If a function is called as a method (e.g. obj.method()) - `this` is the object that the function is a property of.
5. If the function is called as a standalone function (free function invocation), `this` is the global object. In the browser,
   the global object is `window`. If in strict mode (`use strict`;), `this` will be `undefined` instead of the global object.
6. If multiple of the above rules apply, the rule that is higher wins and will set the `this` value.
7. If the function is an ES6 arrow function, it ignores all other rules and sets `this` to the value it receives from its surrounding
   scope at the time it is created.

### Scenario 1

```javascript
function Person(name) {
  this.name = name;
}

const me = new Person("Zheng Jing");
console.log(me.name); // "Zheng Jing"
```

### Scenario 2

```javascript
class Person(name) {
    constructor(name) {
        this.name = name;
    }

    printThis() {
        console.log(this):
    }
}

const me = new Person("Zheng Jing");
me.printThis(); // { name: "Zheng Jing }

```

### Within a regular function call

```javascript
function printThis() {
  console.log(this);
}

printThis(); // In non-strict mode: window object. In strict mode: undefined
```

### Within a method call

```javascript
const obj = {
  name: "Zheng Jing",
  printThis: function () {
    console.log(this);
  },
};

obj.printThis(); // { name: "Zheng Jing", printThis: f }

const printThisStandalone = objj.printThis;
printThisStandalone(); // window object (non-strict mode) or undefined (strict mode)
```
