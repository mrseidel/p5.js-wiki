# Overview of differences

The p5.js language looks very similar to the Processing language, with a few changes:

+ Because you can think of your sketch as more than just the drawing canvas, `size()` has been replaced with `createCanvas()`, to suggest the possibility of creating other elements.
+ `frameRate(num)` sets the frame rate, but the `frameRate` variable has been removed. To get the current frame rate, call `frameRate()` with no arguments.
+ JavaScript doesn't always load things synchronously, so there are a couple options to deal with this:
     + All load methods take an optional callback argument. That is, a function that gets called after the file has been loaded. 
     + Alternatively, you can place load calls in a `preload()` method that happens before `setup()`. If a preload method exists, setup waits until everything inside is loaded, see this [image example](http://p5js.org/examples/image-alpha-mask.html).
+ The variable `mousePressed` has been replaced with `mouseIsPressed`.
+ In addition to mouse events, there are touch events. The mapping is like this:
     + `mouseX` ~ `touchX`
     + `mouseY` ~ `touchY`
     + `mousePressed()` ~ `touchStarted()`
     + `mouseDragged()` ~ `touchMoved()`
     + `mouseReleased()` ~ `touchEnded()`
     + There is a `touches[]` array that contains a series of objects with x and y properties corresponding to the position of each finger.
+ `push/popMatrix()`, and `push/popStyle()` have been replaced with `push()` and `pop()`, the equivalent of calling both matrix and style methods together.
+ By default, everything is in the global namespace, and you can create your sketches like you do with Processing. However, there is something we call "instance mode" for creating a p5 sketch that plays nice with the rest of the code running on your page. See this [instance mode example](http://p5js.org/examples/instance-mode-instantiation.html) and this [global vs instance mode tutorial](https://github.com/processing/p5.js/wiki/Global-and-instance-mode).
+ In global mode, p5 variable and function names are not available outside `setup()`, `draw()`, `mousePressed()`, etc. (Except in the case where they are placed inside functions that are called by one of these methods.) What this means is that when declaring variables before `setup()`, you will need to assign them values inside `setup()` if you wish to use p5 functions. For example:

  ```javascript
  let n;
  function setup() {
    createCanvas(100, 100);
    n = random(100);
  }
  ```

+ The function `println()` is not available in p5.js. Use `print()` or `console.log()`.
+ The origin (0, 0, 0) for WEBGL mode is in the center of the canvas, rather than the top left as it is in 2D mode.

+ Not everything in Processing is implemented in p5.js, but we are working on it! Right now there is no PShape equivalent. The camera model in p5js is yet very basic, with only eye position and no "look at" or axis direction. See the [reference](http://p5js.org/reference/) for up-to-date documentation of what functions work.
 
# Some things about JavaScript
+ Variables do not have a type. Use [`let`] or [`const`] instead of `float`, `int`, `double`, `long`, `char`, `String`, `Array`, etc. You do not need to specify return types or parameter types for functions.
+ A variable can be anything – any of the types mentioned, but also functions.
+ Arrays are constructed very simply (no need for Processing’s `ArrayList` anymore) and have many built-in features. See this [array example](http://p5js.org/examples/arrays-array.html) and learn more about JS arrays [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array).
+ JavaScript uses something called prototypes to form something similar to Java class objects. See this [objects example](http://p5js.org/examples/objects-objects.html) and learn more about JS objects [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects).

# Conversion examples

## Basic sketch

This is the basic setup for a Processing and p5.js sketch. Note that p5.js will also require an empty HTML file that links to the p5.js library and your sketch file in the header (see [getting started](http://p5js.org/get-started/)).

```java
void setup() {
  // setup stuff
}

void draw() {
  // draw stuff
}
```

```javascript
function setup() {
  // setup stuff
}

function draw() {
  // draw stuff
}
```

## Converting a Processing sketch to p5.js

Here are two examples of sketches that have been converted from Processing to p5.js. The changes made are shown in the comments, all the other lines remained the same.

```javascript
/**
 * This example can be found in the Processing examples package
 * that comes with the Processing PDE.v
 * Processing > Examples > Basics > Form > Bezier
 * Adapted by Evelyn Eastmond
 */

function setup() {           // **change** void setup() to function setup()
  createCanvas(640, 360);    // **change** size() to createCanvas()
  stroke(255);               // stroke() is the same
  noFill();                  // noFill() is the same
}

function draw() {                         // **change** void draw() to function draw()
  background(0);                          // background() is the same
  for (let i = 0; i < 200; i += 20) {     // **change** int i to let i
    bezier(mouseX-(i/2.0), 40+i, 410, 20, 440, 300, 240-(i/16.0), 300+(i/8.0)); // bezier() is the same
  }
}
```

```javascript

/**
 * This example can be found in the Processing examples package
 * that comes with the Processing PDE.
 * Processing > Examples > Topics > Interaction > Follow3
 * Adapted by Evelyn Eastmond
 */

const x = new Array(20);  // **change** float[] x = new float[20] to new Array(20)
const y = new Array(20);  // **change** float[] y = new float[20] to new Array(20)
const segLength = 18;                                 // **change** float to const

function setup() {                          // **change** void setup() to function setup()
  createCanvas(640, 360);                   // **change** size() to createCanvas()
  strokeWeight(9);                          // strokeWeight() is the same
  stroke(255, 100);                         // stroke() is the same
  for(let i=0; i<x.length; i++) {         // initialize the array
    x[i]=0;
    y[i]=0;
  }
}

function draw() {                           // **change** void draw() to function draw()
  background(0);                            // background() is the same
  drawSegment(0, mouseX, mouseY);           // functions calls, mouseX and mouseY are the same
  for(let i=0; i<x.length-1; i++) {         // **change** int i to let i
    drawSegment(i+1, x[i], y[i]);           // function calls are the same
  }
}

function drawSegment(i, xin, yin) {         // **change** void drawSegment() to function drawSegment(), remove type declarations
  const dx = xin - x[i];                      // **change** float to const
  const dy = yin - y[i];                      // **change** float to const
  const angle = atan2(dy, dx);                // **change** float to const, atan2() is the same
  x[i] = xin - cos(angle) * segLength;      // cos() is the same
  y[i] = yin - sin(angle) * segLength;      // sin() is the same
  segment(x[i], y[i], angle);               // function calls are the same
}

function segment(x, y, a) {                 // **change** void segment() to function segment(), remove type declarations
  push();                            		// pushMatrix() becomes push()
  translate(x, y);                          // translate() is the same
  rotate(a);                                // rotate() is the same
  line(0, 0, segLength, 0);                 // line() is the same
  pop();                              		// popMatrix() becomes pop()
}
```

## Converting a p5.js sketch to Processing

Here are two examples of sketches that have been converted from p5.js to Processing. The changes made are shown in the comments, all the other lines remained the same.

```java
/**
 * This example can be found in the Processing examples package
 * that comes with the Processing PDE.
 * Processing > Examples > Basics > Form > Bezier
 */

void setup() {                         // **change** function setup() to void setup()
  size(640, 360);                      // **change** createCanvas() to size()
  stroke(255);
  noFill();
}

void draw() {                          // **change** function draw() to void draw()
  background(0);
  for (int i = 0; i < 200; i += 20) {  // **change** let i to int i
    bezier(mouseX-(i/2.0), 40+i, 410, 20, 440, 300, 240-(i/16.0), 300+(i/8.0));
  }
}
```

```java
/**
 * This example can be found in the Processing examples package
 * that comes with the Processing PDE.
 * Processing > Examples > Topics > Interaction > Follow3
 * Based on code from Keith Peters. 
 */

float[] x = new float[20];                       // **change** array of 0's to be float[] x = new float[20]
float[] y = new float[20];                       // **change** array of 0's to be float[] x = new float[20]
float segLength = 18;                            // **change** const to float

void setup() {                                   // **change** function setup() to void setup() 
  size(640, 360);                                // **change** createCanvas() to size()
  strokeWeight(9);
  stroke(255, 100);
}

void draw() {                                    // **change** function draw() void draw()
  background(0);
  dragSegment(0, mouseX, mouseY);
  for(int i=0; i<x.length-1; i++) {              // **change** let i to int i
    dragSegment(i+1, x[i], y[i]);
  }
}

void dragSegment(int i, float xin, float yin) {  // **change** function drawSegment() to void drawSegment(). add type declarations.
  float dx = xin - x[i];                         // **change** const to float
  float dy = yin - y[i];                         // **change** const to float
  float angle = atan2(dy, dx);                   // **change** const to float
  x[i] = xin - cos(angle) * segLength;
  y[i] = yin - sin(angle) * segLength;
  segment(x[i], y[i], angle);
}

void segment(float x, float y, float a) {        // **change** function segment() to void segment(). add type declarations.
  pushMatrix();
  translate(x, y);
  rotate(a);
  line(0, 0, segLength, 0);
  popMatrix();
}
```

# Declaring variables

In p5.js, all variables (whether they are numbers, strings, arrays, functions, objects, whatever!) are declared using [`let`] or [`const`]. Unlike in Processing, you don’t have to specify the variable type.

For example, instead of:

```javascript
boolean button = false;
```

you'd write
```javascript
let button = false;
```

or 

instead of:

```javascript
float x = 100.3;
```

you'd write
```javascript
let x = 100.3;
```

Here is a summary of the supported Processing data types (table borrowed from [Getting Started with Processing](http://shop.oreilly.com/product/0636920000570.do)).

Name | Description | Range of values
--- | --- | ---
int | Integers (whole numbers) | -2,147,483,648 to 2,147,483,647
float | Floating-point values | -3.40282347E+38 to 3.40282347E+38
boolean | Logical value | true or false
char | Single character | A-z, 0-9, and symbols
String | Sequence of characters | Any letter, word, sentence, and so on
PImage | PNG, JPG, or GIF image | N/A
PFont | VLW font; use the Create Font tool to make | N/A
PShape | SVG file | N/A

[`let`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let
[`const`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const


# What next?

+ Check out the [p5.js reference](http://p5js.org/reference/) for up-to-date documentation.
+ Play with the examples and demos on the [tutorials page](https://p5js.org/learn).