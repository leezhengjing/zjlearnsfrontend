---
layout: post
title: "Implement jQuery's css"
date: 2025-11-08 00:00:00 +0800
categories: javascript, coding
math: true
---

# Question

Implement the jQuery single-character function $ which only needs to supports the css() method that either gets the value of a computed style property or sets a CSS property on the matched element.

Example usage:

```
$('button')
.css('color', 'red')
.css('backgroundColor', 'tomato')
.css('fontSize', '16px');
```

## Solution

```typescript
interface JQuery {
  css: (
    prop: string,
    value?: boolean | string | number,
  ) => JQuery | string | undefined;
}

export default function $(selector: string): JQuery {
  const element = document.querySelector(selector) as HTMLElement | null;

  return {
    css: function (prop, value) {
      if (value === undefined) {
        if (selector === null) {
          return undefined;
        }

        const value = element.style[prop as any];
        return value === "" ? undefined : value;
      }

      if (element !== null) {
        element.style[prop as any] = String(value);
      }

      return this;
    },
  };
}
```

```typescript
class jQuery {
  element: HTMLElement | null;

  constructor(selector: string) {
    this.element = document.querySelector(selector) as HTMLElement | null;
  }

  css(
    prop: string,
    value?: boolean | string | number,
  ): jQuery | string | undefined {
    if (value === undefined) {
      if (this.element === null) {
        return undefined;
      }
      const value = this.element.style[prop as any];
      return value === "" ? undefined : value;
    }

    if (this.element != null) {
      this.element.style[prop as any] = String(value);
    }

    return this;
  }
}

export default function $(selector: string): jQuery {
  return new jQuery(selector);
}
```

### Notes

The requirements for this implementation of jQuery's css is slightly different from the
actual implementation.

> Get the value of a computed style property for the first element in the set of matched elements or set one or more CSS properties for every matched element.

[jQuery's $ css docs](https://api.jquery.com/css/)

# In Vanilla JavaScript, the way to set styles on an element would be as follows:

```javascript
const buttonEl = document.querySelector("button");
buttonEl.style.color = "red";
buttonEl.style.backgroundColor = "tomato";
buttonEl.style.fontSize = "16px";
```

jQuery is a library that simplifies DOM manipulation (among other things). With jQuery (using the $ alias function), the above can be simplified into:

```javascript
const buttonEl = $("button");
buttonEl.css("color", "red");
buttonEl.css("backgroundColor", "tomato");
buttonEl.css("fontSize", "16px");
```

The return value of most jQuery manipulation APIs return the jQuery object itself, so that method calls can be chained. The above can be further simplified again:

```
$('button')
.css('color', 'red')
.css('backgroundColor', 'tomato')
.css('fontSize', '16px');
```

Additionally, if the second parameter is omitted, the value of that style property is returned.

```
// <button style="color: red">Submit</button>
$('button').css('color'); // 'red'
```
