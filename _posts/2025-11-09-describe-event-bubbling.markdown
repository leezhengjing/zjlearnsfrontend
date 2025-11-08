---
layout: post
title: "Describe event bubbling"
date: 2025-11-09 00:00:00 +0800
categories: javascript, typescript, coding
math: true
---

# What is event bubbling?

Event bubbling is a propagation mechanism in the DOM (Document Object Model) where an event, such as a click or a keyboard event, is first triggered on the target element that initiated the event and then propagates upward (bubbles) through the DOM tree to the root of the document.

Note: even before the event bubbling phase happens is the event capturing phase which is the opposite of bubbling where the event goes down from the document root to the target element.

## Bubbling phase

During the bubbling phase, the event starts at the target element and bubbles up through its ancestors in the DOM hierarchy. This means that the event handlers attached to the target element and its ancestors can all potentially receive and respond to the event.

You can actually try this in your chrome dev tools and just add some event listeners via addEventListener, to html elements with a parent child relationship. Then you will notice that clicking on the child will also cause the parent's event handler to trigger. (I tried it on this very website, on the sidebar element with the id of
sidebar, and just injected some id manually into the nav items to test this.)

## Stopping the bubbling

Event bubbling can be stopped during the bubbling phase using the stopPropagation() method.

```javascript
child.addEventListener("click", (event) => {
  console.log("Child element clicked");
  event.stopPropagation(); // Stops propagation to parent
});
```

Event bubbling is the basis for a technique called event delegation, where you attach a single event handler to a common ancestor of multiple elements and use event delegation to handle events for those elements efficiently.

## Benefits

- Cleaner code: Reduced number of event listeners improves code readability and maintainability.
- Efficient event handling: Minimizes performance overhead by attaching fewer listeners.
- Flexibility: Allows handling events happening on child elements without directly attaching listeners to them.

## Pitfalls

- Accidental event handling: Be mindful that parent elements might unintentionally capture events meant for children. Use event.target to identify the specific element that triggered the event.
- Event order: Events bubble up in a specific order. If multiple parents have event listeners, their order of execution depends on the DOM hierarchy.
- Over-delegation: While delegating events to a common ancestor is efficient, attaching a listener too high in the DOM tree might capture unintended events.
