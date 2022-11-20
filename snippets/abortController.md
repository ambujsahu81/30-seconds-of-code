---
title: Remove event listeners using AbortController
tags: browser,event
expertise: intermediate
cover: blog_images/snowy-mountains.jpg
firstSeen: 2022-11-21T00:40:30+03:00
---

Use AbortController to remove single/Multiple event listeners at once.

- Chrome 88 added the ability to pass an `AbortController‘s signal` into `EventTarget.addEventListener()`.so by using `controller.abort()` we can remove the event listeners.
- AbortController is capable of aborting multiple cancelable requests. Hence we can use it to cancel multiple Event Listeners at once.


```js
const controller = new AbortController();
eventTarget.addEventListener('event-type', handler, { signal: controller.signal });
controller.abort();
```

```js
const controller = new AbortController();
const {signal} = controller;

const handler = () => console.log('Mouse event triggered');
document.querySelector('.my-element').addEventListener('click', handler, { signal });
document.querySelector('.my-element').addEventListener('mousedown', handler, { signal });

const removeAllListener = () => controller.abort(); // Removes both listeners
```
