---
layout: post
title: "Implement make counter"
date: 2025-10-17 23:49:00 +0800
categories: javascript, typescript, coding
math: true
---

# Question

Implement a function `makeCounter` that takes an optional integer and returns a
function. When the returned function is called for the first time, the initial
value is returned. Subsequent calls of the same function returns 1 more than the
previous returned value.

## Solution

```javascript
export default funciton makeCounter(initialValue = 0) {
  let count = initialValue;
  return () => {
    return count++;
  }

  // oneliner: return () => initialValue++;
}
```

## Write-up

Since the requirement is to return a function that returns the initial value,
and every subsequent call returns an incremented value, we need to have a variable
in the outer function to capture this state. Then the return is a function, where
we opt to use a arrow function so that it has lexical scope and captures the
variable we just declared.

In the one liner solution, we omit the declaration of the new variable to capture
this state, and just reuse the argument provided. Mutating an argument is generally
not recommended, due to causing side effects. But since `initialValue` is a
primitive, incrementing it will not cause any side effects.
