---
layout: post
title: Not everything in JavaScript is an object, how?
subtitle: Everything in JavaScript is or act like an object
bigimg: /img/start.jpg
---

### Not everything in JavaScript is an object, how?
Most of the time we have heard that everything in JS is an object which is not true. Let me prove it through an example.

```javascript
 var name = "jitendra";
 name.hi = "hi";
 console.log(name.hi);
 //it will print undefined
```
It means we are not allowed to add property "hi" on literal name. If it was an object we should have been able to add the properties
on that object.  Therefore, everything cannot be an object in JavaScript.
