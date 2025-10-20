---
layout: post
title: "Implement Promise.all()"
date: 2025-10-20 00:00:00 +0800
categories: javascript, typescript, coding
math: true
---

# Question

> Promise.all() is a method that takes an iterable of elements (usually Promises) as an input, and returns a single Promise that resolves to an array of the results of the input promises. This returned promise will resolve when all of the input's promises have resolved, or if the input iterable contains no promises. It rejects immediately upon any of the input promises rejecting or non-promises throwing an error, and will reject with this first rejection message / error.

Source: [Promise.all() docs](https://arc.net/l/quote/ixduzltp)

Promise.all() is frequently used when there are multiple concurrent API requests and we want to wait for all of them to have completed to continue with code execution, usually because we depend on data from both responses.

```typescript
const [userData, postsData, tagsData] = await Promise.all([
  fetch("/api/user"),
  fetch("/api/posts"),
  fetch("/api/tags"),
]);
```

For this task, implement `promiseAll()`, a function that does what Promise.all() does with the difference that we take in a array instead of an iterable.

## Solution

```typescript
type ReturnValue<T> = { -readonly [P in keyof T]: Awaited<T[P]> };

export default function promiseAll<T extends readonly unknown[] | []>(
  iterable: T,
): Promise<ReturnValue<T>> {
  return new Promise((resolve, reject) => {
    const res = new Array(iterable.length);
    let unresolved = iterable.length;

    if (unresolved === 0) {
      resolve(res as ReturnValue<T>);
      return;
    }

    iterable.forEach((item, index) => {
      Promise.resolve(item).then(
        (val) => {
          res[index] = val;
          unresolved -= 1;

          if (unresolved === 0) {
            resolve(res as ReturnValue<T>);
            return;
          }
        },
        (err) => {
          reject(err);
          return;
        },
      );
    });
  });
}
```
