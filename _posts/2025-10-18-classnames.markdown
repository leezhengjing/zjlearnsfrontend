---
layout: post
title: "Implement Classnames"
date: 2025-10-18 20:43:00 +0800
categories: javascript, typescript, coding
math: true
---

# Question

A common functionality which you might have seen in `clsx` or `tailwindMerge`,
but basically a utility function to combine CSS class names together into one string.

Implement the `classnames` function that does this from scratch.

## Criteria

```javascript
classNames("foo", "bar"); // 'foo bar'
classNames("foo", { bar: true }); // 'foo bar'
classNames({ "foo-bar": true }); // 'foo-bar'
classNames({ "foo-bar": false }); // ''
classNames({ foo: true }, { bar: true }); // 'foo bar'
classNames({ foo: true, bar: true }); // 'foo bar'
classNames({ foo: true, bar: false, qux: true }); // 'foo qux'
```

Arrays will be recursively flattened as per the rules above.

```javascript
classNames("a", ["b", { c: true, d: false }]); // 'a b c'
```

Values can be mixed.

```javascript
classNames(
  "foo",
  {
    bar: true,
    duck: false,
  },
  "baz",
  { quux: true },
); // 'foo bar baz quux'
```

Falsey values are ignored.

```javascript
classNames(null, false, "bar", undefined, { baz: null }, ""); // 'bar'
```

In addition, the returned string should not have any leading or trailing whitespace.

## Solution

```typescript
export type ClassValue =
  | ClassArray
  | ClassDictionary
  | string
  | number
  | null
  | boolean
  | undefined;

export type ClassDictionary = Record<string, any>;
export type ClassArray = Array<ClassValue>;

export default function classNames(...args: Array<ClassValue>): string {
  const classes: Array<string> = [];

  args.forEach((arg) => {
    // handle null, boolean, undefined
    if (!arg) {
      return;
    }

    const argType = typeof arg;
    // handle string, number
    if (argType === "string" || argType === "number") {
      classes.push(String(arg);
      return;
    }

    // handle array
    if (Array.isArray(arg)) {
      classes.push(classNames(...arg));
      return;
    }

    // handle objects
    if (argType === "object") {
      const argObj = arg as ClassDictionary;
      for (const key in argObj) {
        if (Object.hasOwn(argObj, key) && argObj[key]) {
          classes.push(key);
        }
      }
      return;
    }
  });

  return classes.join(' ');
}
```

## Write-up

### Clarifying Questions

The important thing before proceeding is to gather all the requirements and asking
clarification questions. Some good questions, if there aren't boilerplate code
provided, would be:

> "What are all the possible type of classnames I need to handle?"

There are many types of classnames, including arrays and objects.

> "Can there be duplicated classes in the input? Should the output contain duplicated classes?"

Yes, there can be. In this case we will allow duplicated classes in the output.

> "What if a class is added and then later added again but turned off? E.g. `classnames('foo', {'foo':false})`"

For this question, we will accept the final output to be 'foo', although it can
be argued that the developer likely does not intend for 'foo' to be in the final output.

With the clarifying questions out of the way, we can begin implementing.

### Splitting up the task

We can look at this task as a simple pattern matching, handling each possible
type of classname in our list of ...args, and adding that to our res array/set
as we iterate through the ...args.

There is a certain level of recursion with our definition of the classname types,
particularly regarding Arrays of classnames.

It's a good idea to write down the types at this point and how we will handle them.

1. String/number : Add to result
2. Array: Recursively call our `classnames` function on the array.
3. Object: Loop through the key/value pairs and add the keys with truthy values
   into the `classes` collection.

### Notes:

- Calling `typeof` on an array returns `"object"` actually, so we need to do an
  `Array.isArray` check to handle the array case before the object case.
- You should mention that:
  - Stack overflow: Possibility of stack overflow with any recursive solution.
  - Circular references: Possibility of circular references for arrays and objects.
    This applies to any input which has arbitrary depth.

## Follow-up questions

Can you handle de-duplicating classes? Without de-duplication, `classnames('foo', 'foo')`
will give you `'foo foo'` which is unnecessary as far as CSS is concerned.

Furthermore, can you handle the case where false appears later in the arguments,
removing it from the final result?

## Library Implementation

This is how the npm package [`classnames` npm package](https://github.com/JedWatson/classnames) is implemented:

```typescript
var hasOwn = {}.hasOwnProperty;

export default function classNames() {
  var classes = [];

  for (var i = 0; i < arguments.length; i++) {
    var arg = arguments[i];
    if (!arg) continue;

    var argType = typeof arg;

    if (argType === "string" || argType === "number") {
      classes.push(arg);
    } else if (Array.isArray(arg)) {
      if (arg.length) {
        var inner = classNames.apply(null, arg);
        if (inner) {
          classes.push(inner);
        }
      }
    } else if (argType === "object") {
      if (arg.toString === Object.prototype.toString) {
        for (var key in arg) {
          if (hasOwn.call(arg, key) && arg[key]) {
            classes.push(key);
          }
        }
      } else {
        classes.push(arg.toString());
      }
    }
  }

  return classes.join(" ");
}
```

And this is how the [`clsx` npm package](https://github.com/lukeed/clsx/blob/master/src/index.js) implements it.

```javascript
function toVal(mix) {
  var k,
    y,
    str = "";

  if (typeof mix === "string" || typeof mix === "number") {
    str += mix;
  } else if (typeof mix === "object") {
    if (Array.isArray(mix)) {
      var len = mix.length;
      for (k = 0; k < len; k++) {
        if (mix[k]) {
          if ((y = toVal(mix[k]))) {
            str && (str += " ");
            str += y;
          }
        }
      }
    } else {
      for (y in mix) {
        if (mix[y]) {
          str && (str += " ");
          str += y;
        }
      }
    }
  }

  return str;
}

export function clsx() {
  var i = 0,
    tmp,
    x,
    str = "",
    len = arguments.length;
  for (; i < len; i++) {
    if ((tmp = arguments[i])) {
      if ((x = toVal(tmp))) {
        str && (str += " ");
        str += x;
      }
    }
  }
  return str;
}

export default clsx;
```
