---
title: Intro to Canvas, in class challenge solutions
length: 30
tags: canvas, tears
---


### Intro to HTML5 Canvas: In Class Challenge Solutions

This is a walk through of solutions to the `Your Turn` challenges of the `Animating Canvas` section in [Object Oriented JS with HTML5 Canvas](http://frontend.turing.io/lessons/html5-canvas-object-oriented-js.html)

#### Starting Code

We'll be using the started code set-up outlined in the `Canvas Basics` section of the Object Oriented JS with HTML5 Canvas lesson. You can also find the code [here](https://github.com/stevekinney/advanced-js-fundamentals-ck/tree/gh-pages/demos/canvas-blocks).

This walk through also assumes you have worked your way through the `Animating Canvas` section and have added the following code to your `script.js` file:

```js
var canvas = document.getElementById('game');
var context = canvas.getContext('2d');

var x = 50;
var y = 50;
var width = 10;
var height = 10;

requestAnimationFrame(function gameLoop() {
  context.clearRect(0, 0, canvas.width, canvas.height);
  context.fillRect(x++, y, width, height);
  requestAnimationFrame(gameLoop);
});
```

Now that you're all set up, let's tackle the `Your Turn` challenges!

### The Challenges

Below are the `Your Turn` challenges from the lesson. Let's start at the top and work our way through them!

---

* Draw a small rectangle to the canvas.
* Use `requestAnimationFrame()` to move the rectangle one pixel down each time it is called.
  * _Extension_: Can you make the block stop when it reaches the end of the canvas? Can you make it turn around and go the other way when it reaches the end of the canvas?
* Can you add four more blocks that behave the same way?

---

Let's break these down just a little further into distinct tasks:

* Draw a rectangle to the canvas
* Use `requestAnimationFrame()` to move the rectangle one pixel down each time it is called
* Make the block stop when it reaches the end of the canvas
* Make it turn around and go the other way when it reaches the end of the canvas
* Add four more blocks that turn around and go the other way when they reach the end of the canvas

Now we can see that we actually have 5 small problems to work through with each problem building on the previous problem's solution. Great! Let's get started.

#### Challenge 1: Draw a rectangle

You've already got this down! Let's go through it again:
