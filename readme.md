---
title: Intro to Canvas, in class challenge solutions
length: 30
tags: canvas, tears
---


### Intro to HTML5 Canvas: In Class Challenge Solutions

This is a walk through of solutions to the `Your Turn` challenges of the `Animating Canvas` section in [Object Oriented JS with HTML5 Canvas](http://frontend.turing.io/lessons/html5-canvas-object-oriented-js.html)

#### Starting Code

We'll be using the starter code set-up outlined in the `Canvas Basics` section of the Object Oriented JS with HTML5 Canvas lesson. You can also find the code [here](https://github.com/stevekinney/advanced-js-fundamentals-ck/tree/gh-pages/demos/canvas-blocks).

You'll have 4 files: `helpers.js`, `index.html`, `script.js`, and `style.css`. Get the starter code into those files. We'll be working in the `script.js` file.

This walk through assumes you have worked your way through the `Animating Canvas` section and have the following code to your `script.js` file:

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

Before we start on the challenges, let's take a quick walk back through what's going on here:

 - Our `canvas` variable allows us to reference our canvas object (TIP: remember that we specify width and height directly inline on this element rather in our CSS), and `context` gives us a reference so we can begin to draw on that canvas. We see that we're passing in the context `2d` -- while there are several different contexts supported by the Canvas API, for our purposes we only need to worry about creating a 2-dimensional drawing space.

 - We have created variables with hard-coded values for `x`, `y`, `width`, and `height` . We'll be using these to pass in as arguments when we call `context.fillRect` inside the game loop.

 - Speaking of our game loop: in the last line inside of or `gameLoop` function, we're introducing the concept of _recursion_. Basically, we want to call the function that gets passed as an argument to `requestAnimationFrame` _inside of itself_ so it will run over and over again. We're more or less creating a controlled infinite loop which is what allows us to redraw the canvas every frame creating an animation.

_Something to keep in mind: this block of code is not going to stop moving our block once it has reached the end of our canvas. The block will scoot right off the canvas. It's important to remember that just because we can't see it doesn't mean that it's not still out there, just scooting along all alone out there in no man's land. Our loop doesn't stop running just because our block leaves the visible canvas. It's not going to break, there isn't anything wrong with it, but it's important to remember that just because we can't see our block doesn't mean it's gone._

Because of the nature of the challenges, you'll want to comment out this code leaving only the `canvas` and `context` variables uncommented. We'll be walking back through drawing a rectangle and setting up our gameLoop from scratch, might as well start with a blank-ish slate. Practice is a good thing!

Now that you're all set up, let's tackle the `Your Turn` challenges!

### The Challenges

Below are the `Your Turn` challenges from the lesson. Let's start at the top and work our way through them.

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

---

* Draw a rectangle to the canvas

---

This is a bit of a step backwards from where we ended up at the end of the `Animating Canvas` section, but it's good review so let's go over it again.

Before we can move anything, we need to have something on the screen to move. We'll assume you have already defined the variables `canvas` and `context` (if you're not sure what those are for, refer back to the original lesson for a refresher on why we need those variables and what they do for us):

```js
var canvas = document.getElementById('game');
var context = canvas.getContext('2d');

context.fillRect(10, 10, 50, 50);
```

Boom! All we have to do to draw a stationary rectangle is call the `fillRect` (which stands for "fill rectangle") method on our `context` object. `fillRect` takes 4 arguments that define the position of our rectangle inside of our canvas with x and y values (i.e. the pixel distance from the upper left corner. `x` represents the X-axis, `y` represents the Y-axis), and the height and width of the rectangle we want to draw, `fillRect(x, y, width, height)`. In the example above, we're saying that the rectangle should be positioned 10px from the left side of our canvas, 15px from the top of our canvas, and it should be 50px wide with a height of 30px.

One down, 4 to go -- on to the next challenge!

#### Challenge 2: Move the rectangle down each time the gameLoop runs

---

* Use `requestAnimationFrame()` to move the rectangle one pixel down each time it is called

---

Back to the fun stuff! Drawing a rectangle is all well and good, but where things get interesting is when we start moving that rectangle on the screen. This should be very familiar, since we've already created a block that moves to the right each time our gameLoop runs. Let's get this slight variation of block movement implemented (we'll assume that you've got your `canvas` and `context` variables set up and won't show them in the code sample below):

```js
var x = 50;
var y = 50;
var width = 40;
var height = 40;

requestAnimationFrame(function gameLoop () {
  context.clearRect(0,0, canvas.width, canvas.height);
  context.fillRect(x, y++, width, height);
  requestAnimationFrame(gameLoop);
})
```

That was pretty easy, right? We just incremented on the value of `y` instead of `x`. Next challenge, please!


#### Challenge 3: Make the block stop at the end of the canvas

---

* Can you make the block stop when it reaches the end of the canvas? Can you make it turn around and go the other way when it reaches the end of the canvas?

---

Let's break this down. We know that we'll want our block to move across the canvas (something we already know how to do), and then we'll want to stop incrementing on the `x` (or `y`) value when the block reaches the edge of the canvas. Basically, we have 2 things we want to happen.

We can start with the code we have from the previous challenge, but let's make the `y` starting value smaller so our block starts at the top of our canvas:

```js
var x = 50;
var y = 0;
var width = 40;
var height = 40;

requestAnimationFrame(function gameLoop () {
  context.clearRect(0,0, canvas.width, canvas.height);
  context.fillRect(x, y++, width, height);
  requestAnimationFrame(gameLoop);
})
```

Our block moves from the top to the bottom, now let's make it stop when it reaches the end of our canvas.

A simple way of doing this is to use an `if/else` statement. We'll set a conditional that will move the block downwards as long as its true, and once that condition is no longer true we'll make the block stop. Here's what it looks like:

```js
var x = 50;
var y = 0;
var width = 40;
var height = 40;

requestAnimationFrame(function gameLoop () {
  context.clearRect(0, 0, canvas.width, canvas.height);
  if (y <= (canvas.height - height)) {
    context.fillRect(x, y++, width, height);
  } else {
    context.fillRect(x, y, width, height);
  }
  requestAnimationFrame(gameLoop);
});
```

Let's talk through this:

To start, we keep our `context.clearRect` as the first line inside our `gameLoop` so we have a single block moving across the screen.

Next, we hit our `if/else` statement. Our conditional checks that the value of `y` is less than or equal to the value of the total height of the canvas (`canvas.height`) minus the height of our block (`height`). This means that the block will stop when its bottom edge is even with the bottom of the canvas. If we just checked the value of `y` against the value of `canvas.height` it would push our block just out of our view, so it would stop but we wouldn't be able to tell!

Last, we recursively run the `gameLoop` function so our animation keeps looping.

Any just like that, you've stopped your block! Next challenge!

#### Challenge 4: Make the block stop at the end of the canvas

---



---
