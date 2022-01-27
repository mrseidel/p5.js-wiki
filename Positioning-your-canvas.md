<!--
  Hello editor!

  For more background on this tutorial, or to leave comments on it, see:

  https://github.com/processing/p5.js/issues/1333
-->

By default, your p5 sketch’s canvas is added to the end of the web page it’s in, and no styling is applied to it.

However, it’s possible to position and style it any way you want with a bit of [HTML and CSS](Intro-to-HTML-and-CSS).

Let's start with a simple sketch:

```html
<html>
  <head>
    <title>My Sketch</title>
    <script src="http://cdnjs.cloudflare.com/ajax/libs/p5.js/0.5.6/p5.js"></script>
    <script src="sketch.js"></script>
  </head>
  <body>
  </body>
</html>
```

```js
// sketch.js

function setup() {
  createCanvas(100, 100);
  background(255, 0, 200);
}
```

This will display a 100×100 pink square at the top-left of your browser window.


## Making the canvas fill the window

The canvas can be made to automatically fill the window by using the built-in variables `windowWidth` and `windowHeight`:
```js
function setup() {
  createCanvas(windowWidth, windowHeight);
  background(255, 0, 200);
}
```

If you want the canvas to automatically resize to fill the window whenever the window is resized, you can define the `windowResized` function in your sketch:
```js
function setup() {
  createCanvas(windowWidth, windowHeight);
  background(255, 0, 200);
}

function windowResized() {
  resizeCanvas(windowWidth, windowHeight);
}
```

You may notice that even though the canvas is exactly the same size as the window in this case, scrollbars may appear. This is default behavior of some browsers. To avoid this, you can set the style property `display:block` for the canvas element. Something like this:
```js
function setup() {
  var cnv = createCanvas(windowWidth, windowHeight);
  cnv.style('display', 'block');
  background(255, 0, 200);
}
```

## Centering the sketch on the page with CSS

We can add a stylesheet that uses [flexible box layout](https://css-tricks.com/snippets/css/a-guide-to-flexbox/) to vertically and horizontally center our sketch on the page:

```html
<html>
  <head>
    <title>My Sketch</title>

    <!-- Link to our stylesheet! -->
    <link rel="stylesheet" href="style.css">

    <script src="http://cdnjs.cloudflare.com/ajax/libs/p5.js/0.5.6/p5.js"></script>
    <script src="sketch.js"></script>
  </head>
  <body>
  </body>
</html>
```

```css
/* style.css */

html, body {
  height: 100%;
}

body {
  margin: 0;
  display: flex;

  /* This centers our sketch horizontally. */
  justify-content: center;

  /* This centers our sketch vertically. */
  align-items: center;
}
```

Note that at the time of this writing, flexible box layout (or “flexbox”, as it’s often called) is a relatively new feature in CSS. As such, the above CSS will work on the latest browsers, but older browsers may not position it accurately. To fully support older browsers, you may want to use [vendor prefixing](http://shouldiprefix.com/#flexbox) in your CSS.

## Centering the sketch on the page with JS

One advantage of the CSS approach is that it doesn’t require modifying your sketch at all. However, the fact that supporting older browsers requires vendor prefixing makes the solution a bit less elegant. It’s also not straightforward to tweak: positioning your canvas 12 pixels from the bottom-right of the page, for example, would require learning more about CSS, which can be daunting for newcomers.

With the web, though, there’s almost always more than one way to get something done, and that’s the case here as well. We can actually reposition our canvas using pure JavaScript and a bit of math. For this we’ll need the p5.dom library. You will need to add a link to it in the head of your HTML file.

```html
<html>
  <head>
    <title>My Sketch</title>
    <script src="http://cdnjs.cloudflare.com/ajax/libs/p5.js/0.5.6/p5.js"></script>
    <script src="http://cdnjs.cloudflare.com/ajax/libs/p5.js/0.5.6/addons/p5.dom.js"></script>
    <script src="sketch.js"></script>
  </head>
  <body>
  </body>
</html>
```

Then the p5.js code looks like this:

```js
// sketch.js

function setup() {
  var cnv = createCanvas(100, 100);
  var x = (windowWidth - width) / 2;
  var y = (windowHeight - height) / 2;
  cnv.position(x, y);
  background(255, 0, 200);
}
```

However, you might notice that, unlike the CSS-based solution, resizing your browser window (or changing the orientation of your mobile device) doesn’t re-center your sketch. We can solve this by reusing the canvas-centering logic in a [`windowResized()`](http://p5js.org/reference/#/p5/windowResized) function:

```js
// sketch.js

var cnv;

function centerCanvas() {
  var x = (windowWidth - width) / 2;
  var y = (windowHeight - height) / 2;
  cnv.position(x, y);
}

function setup() {
  cnv = createCanvas(100, 100);
  centerCanvas();
  background(255, 0, 200);
}

function windowResized() {
  centerCanvas();
}
```

As you can see, there’s trade-offs here: what was once a very simple sketch is now a bit more complex. So feel free to try both the CSS and JS solutions and use whichever you’re most comfortable with.

## Relocating the canvas

Alternatively, you may want to position your canvas in the midst of other information on your page. This can be done by using p5’s [`p5.Element.parent()`](http://p5js.org/reference/#/p5.Element/parent) function to move our sketch inside an existing HTML element on our page, rather than leaving it at the very end of the page:

```html
<html>
  <head>
    <title>My Sketch</title>
    <script src="http://cdnjs.cloudflare.com/ajax/libs/p5.js/0.5.6/p5.js"></script>
    <script src="sketch.js"></script>
  </head>
  <body>
    <p>Here is my sketch:</p>
    <div id="sketch-holder">
      <!-- Our sketch will go here! -->
    </div>
    <p>Pretty cool, eh?</p>
  </body>
</html>
```

```js
// sketch.js

function setup() {
  var canvas = createCanvas(100, 100);
 
  // Move the canvas so it’s inside our <div id="sketch-holder">.
  canvas.parent('sketch-holder');

  background(255, 0, 200);
}
```
