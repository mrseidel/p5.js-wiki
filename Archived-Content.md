# Research documentation

This project developed out of a Fellowship with the Processing Foundation exploring the future of Processing with JavaScript. Documentation of research in process and references is below.

## Starting points

### Possibilities
+ what would be gained/lost by js, removing java altogether
+ processing-lite, js syntax
+ processing-js bridge to c++ compiles
+ installations without c++
+ processing as web dev

### Approaches
+ a bunch of different scenarios - writing out what code for that would look like
+ speculative source code - examples or hack usable

### Goals
+ processing identity - running in browser, barrier to entry low
+ primary audience - hard-core programmers, 19yr old design students
+ system+api
+ as a library, focus what processing does and doesn’t do

### Questions

+ What is unique about javascript?
+ What are main ways it diverges/differs from java/processing?
	+ dynamic vs static
	+ loosely-typed vs strongly-typed
	+ prototypal vs classical inheritance
	+ functions as classes, constructors, methods
	+ classical objects are hard, the only way to add a new member to a hard object is to create a new class. js objects are soft, a new member can be added to a soft object by simple assignment. shallow hierarchies are efficient and expressive, deep hierarchies are often inappropriate.
	+ event driven vs linear/loop based
+ Focus on browser experience? What about node, etc.
+ Network connectivity, manipulating dom, interfacing with other elts outside canvas, user interface built-on elts that processing doesn't have, multiple drawing surfaces, interfaces with other libraries / also spec for other - maybe IDE adds in auto (like import library feature).
+ question - limited to canvas?

### Considerations

+ Prototypal inheritance vs emulating classical inheritance.
	+  tool to make it more clear
+ Optimization
	+  Embed instead of having to learn speed tricks?
+ Callbacks/async
	+ helper fxn like newThread() method
	+ identify what sync/async, async ones have callback methods. if you have your own, here's how, and how to specify callback or not
	+ start everything with a
	+ use async module
+ Library spec
+ https://github.com/daniellmb/JavaScript-Scope-Context-Coloring
+ http://codemirror.net/
+ http://www.jslint.com/


### Core classes
PImage, PFont, PShape and PShader, PGraphics (needed to create offscreen drawing surfaces), and PVector.


### What js things could be improved?
+ libraries - documentready annoying, processing-js handles loading order for you (modernizer.js, queue.js), waits to execute
+ (controlled loading and execution built-in)
+ canvas/error handling

### Other notes
+ Library spec?
+ dynamic typing - better typeof method, switch statement
+ strict typeof
+ enforce a type of code, scope
+ jslint strict mode
+ pokeyoke
+ easy way to define your own events, bind listeners


### Current Processing JavaScript mode
+ [processing.org/learning/javascript/](http://processing.org/learning/javascript/)
+ [github.com/jeresig/processing-js](https://github.com/jeresig/processing-js)
+ Processing.js is really two things: a Processing-to-JavaScript translator; and an implementation of the Processing API (e.g., functions like line(), stroke(), etc.) written in JavaScript instead of Java.
+ Nothing new to learn - Processing.js automatically converts your Processing code to JavaScript. This means that you don't have to learn JavaScript in order to run your code in a browser.
+ Does not currently support libraries.
+ Possible to write native JS code inside sketch, but not intended use.
+ Simulates synchronous I/O using Directives (preloading assets).

### Notes / considerations
+ web developer tools
+ processing-js as entry point to web development
+ more transparent, more standard web structure
+ standard javascript - quasi auto complete, strict mode, viz of var scope, sequence
+ live, quasi-live coding environment, dev tools built in
+ also use processing methods
+ visually represent what's going on, in terms of inheritance
+ find in reference
+ not too cluttered
+ all the benefits, but executes like it's in the browser

### Tools
+ [JSHint](http://www.jshint.com/) -  tool to detect errors and potential problems in JavaScript code and to enforce chosen coding conventions, flexible, easily adjusted to enforce particular coding guidelines and environment
+ [JSLint](http://www.jslint.com/)

### Editors
+ [Comparison of JavaScript-based source code editors](http://en.wikipedia.org/wiki/Comparison_of_JavaScript-based_source_code_editors)
+ [atom.io](https://atom.io/) - open source, hackable editor created by github
+ [CodeCosmos](http://bob.ippoli.to/archives/2013/07/18/codecosmos-tech/)
+ [Khan Academy Computer Science](https://www.khanacademy.org/cs)
    + built on top of ace editor, processingjs, jshint
    + real-time code execution - many tools to take advantage of this (number pickers, color picker, image picker)
    + extensive error correction / suggestion
    + [philosophy behind khan academy cs](http://ejohn.org/blog/introducing-khan-cs/)

+ [Studio Sketchpad](http://sketchpad.cc)
+ [Light Table](http://www.lighttable.com) - desktop editor allows realtime modification of running code
+ [Brackets](http://brackets.io/) - "open-source editor for web design and development built on top of web technologies such as HTML, CSS and JavaScript"
+ [Sublime](http://www.sublimetext.com/)
+ [sketch.paperjs.org](http://sketch.paperjs.org/) / [paper.js editor](http://paperjs.org/static/editor/) 
+ [github.com/daniellmb/JavaScript-Scope-Context-Coloring](https://github.com/daniellmb/JavaScript-Scope-Context-Coloring) - Experiment in switching between syntax highlighting and scope colorizing built on JSLint and CodeMirror.
+ [CodeMirror](http://codemirror.net/) - JavaScript component that provides a code editor in the browser. For supported languages, it will color your code, and optionally help with indentation. Also provides API and CSS theming system for customizing to fit your application, and extending it with new functionality.
+ [sketch.processing.org](http://sketch.processing.org/)
+ [Processing helper](http://processingjs.org/tools/processing-helper.html)

+ [Komodo Edit](http://www.activestate.com/komodo-edit) - free, open source version based on Mozilla XULRunner (like Firefox), comes with SpiderMonkey JS engine included and uses Scintilla as code editor
+ [ICE Coder](http://icecoder.net/) - pure browser IDE
+ [ACE editor](http://ace.ajax.org/)
+ [codebender](http://codebender.cc/) - arduino editor with sharing [github.com/codebendercc](https://github.com/codebendercc/)
+ [dat.GUI](https://code.google.com/p/dat-gui/)
+ [tributary](http://tributary.io/tributary/2958568/) - experimental environment for rapidly prototyping visualization code
+ [jsfiddle](http://jsfiddle.net/)
+ [livecoding.io](https://github.com/gabrielflorit/livecoding)
+ [codepen](http://codepen.io/)
+ [OpenProcessing](http://www.openprocessing.org/sketch/create) - has a page to create, run, stop a simple sketch from scratch
+ [HasCanvas](http://hascanvas.com/) - tool for creating and sharing Processing sketches

### IDEs / learning

See References on IDE page [github.com/lmccart/js-processing/wiki/IDE-thoughts#references](https://github.com/lmccart/js-processing/wiki/IDE-thoughts#references)

### JS creative coding libraries

+ [Plask](http://www.plask.org) - JS based creative coding env, Uses: V8, Skia, NodeJS, Cocoa & OpenGL, FreeImage, Syphon
+ [Plask on github](https://github.com/deanm/plask)
+ [two.js](http://jonobr1.github.io/two.js/) - two-dimensional drawing api geared towards modern web browsers. It is renderer agnostic enabling the same api to draw in multiple contexts: svg, canvas, and webgl. Aims to make the creation and animation of flat shapes easier and more concise, does not support text or image. Built in scene graph, animation loop, svg interpreter.
+ [paper.js](http://paperjs.org/) - vector graphics scripting framework that runs on top of the HTML5 Canvas. It offers a clean Scene Graph / DOM and a lot of powerful functionality to create and work with vector graphics and bezier curves, largely compatible with Scriptographer

### Processing / JavaScript + other languages
+ [Ruby-Processing](https://github.com/jashkenas/ruby-processing) - Ruby syntax but utilizes the ease of Processing for drawing
    + Uses regular Ruby for generating sketches, exporting applications and applets; and uses Java via JRuby for running Processing.
    + Supports live coding, includes a control panel.
    + Convenience method for searching through methods $app.find_method("ellipse") will return a list of the method names that may match what you’re looking for: “ellipse”, “ellipseMode”, and “ellipse_mode”.
    + Transliteration vs. translation (Despite the fact that the entire Processing API is available to you, it’s best to work in idiomatic Ruby as much as possible.)
    + [Ruby-Processing in practice](https://github.com/jashkenas/learning-processing-with-ruby)
+ [ofxJavaScript (running JS in OF)](https://code.google.com/p/ofxjavascript/)
    + Uses [Mozilla SpiderMonkey](https://developer.mozilla.org/en-US/docs/SpiderMonkey). 
    + Exposes several classes of openframeworks library to Javascript, allows you to call C++ functions from Javascript, call Javascript functions from C++, or create your "own" Javascript classes.
    + [ofLiveCoding](https://code.google.com/p/oflivecoding)
+ [Ringo](http://ringojs.org) - (based on Rhino) runs JS on Java and adds "goodies"
    + allows use of any java class
    + [Ringo Java integration docs](http://ringojs.org/documentation/java_integration)
+ [quil](https://github.com/quil/quil) - processing + clojure
+ [python mode for processing](https://github.com/martinleopold/PythonMode)
+ [another processing in python lib](https://github.com/jdf/processing.py)
+ [coffeescript mode for processing](https://github.com/fjenett/coffeescript-mode-processing) 
+ [scala + processing](http://technically.us/spde.html)

### Other native code on web
+ [Chrome Native Client](https://developers.google.com/native-client)
+ [Flash c++ compiler](http://gaming.adobe.com/technologies/flascc/)

### JavaScript engines / performance
+ Explains differences in JS engines quite nicely
[http://stackoverflow.com/questions/2137320/javascript-engines-advantages](http://stackoverflow.com/questions/2137320/javascript-engines-advantages)
+ Performance
[http://stackoverflow.com/questions/9060841/rhino-vs-spidermonkey-performance-tests](http://stackoverflow.com/questions/9060841/rhino-vs-spidermonkey-performance-tests)
+ C++ binding 
[http://stackoverflow.com/questions/93692/which-javascript-engine-would-you-embed-in-your-application](http://stackoverflow.com/questions/93692/which-javascript-engine-would-you-embed-in-your-application)

### JS desktop app platforms / libs
+ desktop JS development [http://stackoverflow.com/questions/109399/can-you-do-desktop-development-using-javascript](http://stackoverflow.com/questions/109399/can-you-do-desktop-development-using-javascript)
+ [appjs](http://appjs.com/) - HTML5 / CSS3, nodejs as backbone
+ [Awesomium](http://awesomium.com/
+ [QT Webkit](http://qt.digia.com/Product/Library/Qt-WebKit/)
+ [Berkelium](http://berkelium.org/)

## References and Research

### JS and physical computing 
+ [coder for rPi](http://googlecreativelab.github.io/coder/)
+ [espruino](http://www.kickstarter.com/projects/48651611/espruino-javascript-for-things)


### Other references (for extensions)
+ [jQuery API](http://api.jquery.com/)
+ [HTML5 overview](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/HTML5)

## Starting points

### Goal

Basic concept description / goals

This Processing+JavaScript library starts with the original goal of Processing at it's beginning, to serve as a software sketchbook and to teach computer programming fundamentals within a visual context, and reimagines it for today, based on JavaScript instead of Java. The focus will first be on basic API and 2D drawing functionality, leaving more advanced graphics features, like shaders and 3D, for later.

start with canvas, reveal

something about syntax, API

Spec out and test a JavaScript library that would enable Processing-like syntax for drawing using Canvas and WebGL. It's both about the syntax and how to code.

Bring "Processing" ideas to JavaScript, rather than to emulate Processing/Java through JavaScript. Explore how to take positive parts of what Processing does, and see what the affordances of JS add/remove to the equation.

Involves both "language design" and "ide design".

Idea of Processing syntax-wise was to take some of the nastiness out of writing Java code (having to define classes, threaded animation loops, etc) before you could make things show up on screen. Starting from scratch with JavaScript as the base language would ideally 1) use the nice bits of JS, and 2) hide the uglier bits.

Current work on the Processing JS port is focused on being able to be code compatible and having things run right out of the box (which is great!), but comes at the cost of keeping some of Java's quirks, while potentially hiding the nicer parts of JS. (Strictly speaking, you can still do JS inside of that mode, but it's not necessarily the intent or the current setup.) 

### References

+ [Khan Academy Computer Science](https://www.khanacademy.org/cs)
+ [Studio Sketchpad](http://sketchpad.cc)
+ [Light Table](http://www.lighttable.com)
+ [Sublime](http://www.sublimetext.com/)
+ [paper.js](http://paperjs.org/static/editor/) 
+ [Ruby-Processing](https://github.com/jashkenas/ruby-processing) - Ruby syntax but utilizes the ease of Processing for drawing
+ [Ruby-Processing in practice](https://github.com/jashkenas/learning-processing-with-ruby)

### Processing core values

+ Programming in a visual arts context
+ Made for teaching programming
+ Bridge to other languages
+ Simple publishing for sharing
+ Provide educational infrastructure (tutorials, videos, books)
+ Community infrastructure
+ Extensible through libraries
+ Import/Export to diverse media and formats
+ Concise IDE, scale to professional IDE
+ Free to download
+ Open Source
+ Developed through workshops, forums, etc.
        
# Instantiation Cases

## Global Mode

```javascript  
// API 
preload(): runs once, first  
setup(): runs once, second 
draw(): loops, indefinitely  
createCanvas(w, h): creates a canvas element at the 0,0 with input size  
 
// CASE 1  
// Only setup(). 
// setup() runs once and createCanvas() gets called automatically with defaults. 
function setup() { 
  background(255, 0, 0); 
  noStroke();  
  ellipse(0, 0, 50, 50); 
}  
 
// CASE 2  
// Only setup() and createCanvas().  
// setup() runs once and createCanvas() returns a pointer to the canvas created  
// with the input size, at 0,0.  Holding the pointer is optional.  
function setup() { 
  createCanvas(400, 400);  
  background(255, 0, 0); 
  noStroke();  
  ellipse(0, 0, 50, 50); 
}  
 
// CASE 3  
// Only draw().  
// createCanvas() is called automatically with defaults. 
function draw() {  
  ellipse(random(0, 400), random(0, 400), 50, 50); 
}  
 
// CASE 4  
// setup() and draw() without createCanvas().  
// createCanvas() is called automatically with defaults. 
function setup() { 
  background(255, 0, 0); 
}  
function draw() {  
  ellipse(random(0, 400), random(0, 400), 50, 50); 
}  
 
// CASE 5  
// setup() and draw() with createCanvas(). 
function setup() { 
  createCanvas(400, 400);  
  background(255, 255, 0); 
}  
function draw() {  
  ellipse(random(0, 400), random(0, 400), 50, 50); 
}  
 
// CASE 6  
// setup() and draw() with createCanvas(), holding pointer 
var canvas;  
function setup() { 
  canvas = createCanvas(400, 400); 
  canvas.position(100, 50); // allows you to set position, id, etc 
  background(255, 255, 0); 
}  
function draw() {  
  ellipse(random(0, 400), random(0, 400), 50, 50); 
}  
 
// CASE 7  
// holding pointer, calling methods explicitly on that object  
function setup() { 
  var cnv = createCanvas(400, 400);  
  cnv.background(255, 0, 0); 
  cnv.noStroke();  
  cnv.ellipse(0, 0, 50, 50); 
}  
```  
 
## Instance Mode  
 
```javascript  
// CASE 0: no node specified 
// Canvas is auto-generated and appended to body.  
var sketch = function (p) {  
  var gray = 0;  
 
  p.setup = function () {  
    p.createCanvas(600, 400);  
  }; 
 
  p.draw = function () { 
    p.background(gray);  
    p.rect(p.width/2, p.height/2, 200, 200); 
  }; 
 
  p.mousePressed = function () { 
    gray = (gray + 16) % 256;  
  }; 
}; 
 
new p5(sketch);  
 
// CASE 1: node specified  
// Node is either a canvas element or any generic element. 
// If it is a canvas, P5 will attach to it.  
// If it is another type of element, a canvas with P5 attached will be inserted inside of it.  
// Note that "sketch" is arbitrary and a user may replace it w/ any variable name. 
 
var sketch = function (p) {  
  var gray = 0;  
 
  p.setup = function () {  
    p.createCanvas(600, 400);  
  }; 
 
  p.draw = function () { 
    p.background(gray);  
    p.rect(p.width/2, p.height/2, 200, 200); 
  }; 
 
  p.mousePressed = function () { 
    gray = (gray + 16) % 256;  
  }; 
}; 
 
new p5(sketch, node);  
```  
 
Note that the above is functionally equivalent to below, either may be used, but the above will be the recommended syntax for beginners as we feel it's clearer. 
 
```javascript  
new p5(function (p) {  
  var gray = 0;  
 
  p.setup = function () {  
    p.createCanvas(600, 400);  
    noLoop();  
  }; 
 
  p.draw = function () { 
    p.background(gray);  
    p.rect(p.width>>1, p.height>>1, 200, 200); 
  }; 
 
  p.mousePressed = function () { 
    gray = (gray + 020) % 0x100; 
    redraw();  
  }; 
}, node);  
```

# ITP Working Group

**[DEVELOPER DOC](https://github.com/processing/p5.js/wiki/Development)
**[INLINE DOCS GUIDE](https://github.com/processing/p5.js/wiki/Inline-documentation)

**If you are working on one of these things, create an issue on github and place your github username in brackets in the title, so others can collaborate rather than duplicate!**

## Projects list

1. **DOM manipulation.** The intention with this library is not to limit to the canvas, and to allow access to DIVs and other elements. It's not meant to replace jQuery, but to give some basic access to the DOM in a way that is intuitive and useful. This [tutorial](https://github.com/processing/p5.js/wiki/DOM-Extensions) describes the current functionality. This area of functionality is just a first draft, and some further thought in terms of functionality and syntax would be really useful.
 * https://github.com/processing/p5.js/issues/389
 * https://github.com/processing/p5.js/issues/391
 * https://github.com/processing/p5.js/issues/395
 * https://github.com/processing/p5.js/issues/394

2. **Touch interactions.** Examples 5-0 through 5-3 here http://p5js.org/workshop/, demonstrate the current supported touch functionality. However, there are a few more questions to think about.
     * Should there be some notion of a touch id for the touches[] array? This could be useful for persistently tracking touches.
     * [Example 5-2](http://p5js.org/workshop/examples/example_5-2/sketch.js) demonstrates how to write your sketch to support both touch and mouse depending on device, but maybe we want a smart function or wrapper that automatically returns mouseX/Y or touchX/Y depending on device.
     * Right now there is `touchStarted`, `touchMoved`, and `touchEnded`. Should there be more functions to support touch?

3. Some file I/O stuff to finish up: https://github.com/processing/p5.js/issues/40

4. Thinking about text:
 * https://github.com/processing/p5.js/issues/60
 * https://github.com/processing/p5.js/issues/356
 * [Some materials are here from my A to Z class](http://shiffman.net/teaching/a2z/visualization/)

5. Thinking about svgs and pdf export:
 * https://github.com/processing/p5.js/issues/37

6. Various [bugs and issues](https://github.com/processing/p5.js/issues).

7. **Tutorial for sketch instantiation** -- global and instance modes. This functionality was recently added! Now we need some explanation:
     * Why use global vs instance mode?
     * Explanation of syntax for each setup. For instance mode, some explanation of closures, scope.
     * What are the different options for using each?
The [global](https://github.com/processing/p5.js/tree/main/examples/instantiation-global) and [instance](https://github.com/processing/p5.js/tree/main/examples/instantiation-instance) example cases are a good place to start.

8. **Developer page, extended version. [LUISA]** This could be a great task for someone less experienced with JS or JS development. You could start by copying the [current developer page](https://github.com/processing/p5.js/wiki/Development) into a new wiki page, then working through each step of the development setup process, and add a few sentences/paragraphs of lay mans explanation anywhere you would have liked to see it.

9. Other documentation currently needed: https://github.com/processing/p5.js/issues/346

10. **Something else you are excited about?**
     * Sound module, data module, module template. And what is a "module" called anyway? Extension, addon, module?
     * IDE
     * WebGL 
     * Node.js + Websockets + p5.js
     * Arduino or Physical stuff + p5.js


# Education
**This is a place for p5.js related teaching resources -- links to syllabi, workshop materials, helper tools for teaching / classroom. Feel free to add things you create here (just click the "Edit" button). For examples and demos without related syllabi or teaching materials please see the [contributed tools page](https://github.com/processing/p5.js/wiki/Contributed-Tools,-Projects,-Demos).**

Note that examples included may be using older versions of p5.js and might not be up to date.

## Class / workshop syllabi

* [Intro to Computational Media, NYU ITP F15](https://github.com/ITPNYU/ICM-2015)
* [Creative Coding, NYU IDM](http://creative-coding.decontextualize.com/)
* [Generative Art with Processing, Bennington College F15](http://curriculum.bennington.edu/fall2015/2015/05/14/generative-art-with-processing/)
* [Creative JavaScript, NYU ITP F14](http://github.com/lmccart/itp-creative-js) - examples and notes
* [Intro to Creative Programming, RISD D+M F13](http://risd-creative-programming.github.io/fa13-introtocreativeprogramming/index.html) - many examples
* [Introduction to Interactive Computing, TCNJ F14](http://coursescript.com/calendar.php?course=5) - examples and notes
* [Programming from A to Z](https://github.com/shiffman/Programming-from-A-to-Z-F15) - procedural analysis and generation of text-based data using JavaScript and p5.js
* [Mobile Art Workshop](https://github.com/whichlight/mobile-art-intro) - intro to p5, websockets, interactivity, and sound for mobile web art
* [Web Media, Moore College of Art S15](https://github.com/lee2sman/PDA203WebMedia) - intro to html, p5 and p5.js to generate web-based art projects
* [Code as Medium, RISD S15](http://risd-creative-programming.github.io/s15-codeasmedium/examples.html) (Evelyn Eastmond) - many interactive codepen examples!
* [Creative Coding for the Web, Culture Hub S15](https://github.com/futuremarc/p5-creative-coding-course) - syllabus and notes
* [Intro to Media Computing @ the School of Creative Media, Hong Kong](http://rednoise.org/imc)
* [Arduino + p5.js examples](https://github.com/tigoe/GraphingSketches)
* [Physics Programming Lab with Processing](http://www.physics.ohio-state.edu/~orban/processing_2015/)
* [Creative Coding with p5.js tutorial](http://bsk.education/SE8_p5js/)
* [JS Course with p5.js](https://github.com/mveteanu/JSCourse)

## Tools
* [WordPress p5.js embedder](https://github.com/lmccart/p5.js-wp-embedder) - plugin to embed p5.js sketches into WordPress pages and posts (**Discontinued, use at own risk**)

## Tutorials
* [Embedding p5.js](https://github.com/processing/p5.js/wiki/Embedding-p5.js) - different ways of including sketches on existing sites or blogs.

## Videos
- [Daniel Shiffman Learning p5.js Vimeo channel](https://vimeo.com/channels/learningp5js/) - no ads
- [Daniel Shiffman Learning p5.js YouTube playlist](https://www.youtube.com/playlist?list=PLRqwX-V7Uu6Zy51Q-x9tMWIv9cueOFTFA) - has ads
- [Kadenze course](https://www.kadenze.com/courses/introduction-to-programming-for-the-visual-arts-with-p5-js/info) -- coming soon!
- [Envato Tuts+ Course: How to Program Interactive Art With p5.js](https://code.tutsplus.com/courses/how-to-program-interactive-art-with-p5js) - register to watch free

## Books 
* [Introduction to Programming with JavaScript, P5, and Processing ](http://www.amazon.com/Introduction-Programming-JavaScript-Processing-Cooks-ebook/dp/B010R0VMQS), Robert Cook - [interactive examples (jsfiddle)](http://jsfiddle.net/user/bobcook/fiddles/)
* [Getting Started with p5.js](http://amzn.to/1PmztVt), Lauren McCarthy, Casey Reas, Ben Fry
* [p5.js Programming Guide (in Japanese) p5.jsプログラミングガイド] (http://www.cutt.co.jp/book/978-4-87783-381-7.html), Kouichi Matsuda, Tetsuo Yutani, Ayana Shiino

## p5.js Resources
* [p5.js reference](http://p5js.org/reference)
* [p5.js forum](http://forum.processing.org/two/)
* [p5.js on GitHub](https://github.com/lmccart/p5.js)
* [p5.js CDN](http://cdnjs.com/libraries/p5.js)
* [Getting Started with p5.js](http://www.amazon.com/Make-Interactive-Graphics-JavaScript-Processing/dp/1457186772) - O'Reilly book
* [Intro to Visual Programming with p5.js](https://www.kadenze.com/courses/introduction-to-programming-for-the-visual-arts-with-p5-js) - online video tutorials (free with signup)

## JS Resources
* [Codecademy: JavaScript](http://www.codecademy.com/tracks/javascript)
* [How to learn JavaScript properly](http://javascriptissexy.com/how-to-learn-javascript-properly/)
* [JavaScript the right way](http://www.jstherightway.org/)
* [Code School](https://www.codeschool.com/paths/javascript)
* [JavaScript garden](http://bonsaiden.github.io/JavaScript-Garden/)
* [A re-introduction to JS by Mozilla](https://developer.mozilla.org/en-US/docs/Web/JavaScript/A_re-introduction_to_JavaScript)
* [JavaScript 101 from JQuery](https://learn.jquery.com/javascript-101/)
* [JavaScript: The Definitive Guide](http://shop.oreilly.com/product/9780596000486.do)
* [Eloquent JavaScript](http://eloquentjavascript.net/contents.html), Marijn Haverbeke
* [Beginning JavaScript](http://www.amazon.com/Beginning-JavaScript-Paul-Wilton/dp/0470525932), Paul Wilton and Jeremy McPeak
* [JavaScript book](http://www.javascriptbook.com/)

## HTML+CSS Resources
* [HTML & CSS book](http://www.htmlandcssbook.com/)
* [Codecademy HTML glossary](https://www.codecademy.com/glossary/html#attributes)
* [Mozilla Intro to HTML](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Introduction)
* [Codecademy CSS glossary](https://www.codecademy.com/glossary/css)
* [Mozilla Getting Started with CSS](https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Getting_started)
* [How to Become a Web Developer: Envato Tuts+](https://code.tutsplus.com/courses/how-to-become-a-web-developer) - register to watch free

## General Programming
* [Udacity - Object Oriented Javascript](https://www.udacity.com/course/object-oriented-javascript--ud015)
* [Lynda](https://www.lynda.com/)
* [Codecademy](http://www.codecademy.com/)
* [Flat Iron School](http://prework.flatironschool.com/web-development/)
* [Programming Terms and Environments Summary](https://itp.nyu.edu/physicalcomputing/lessons/programming/programming-terms-and-programming-environments/)
* [A Brief Introduction to Debugging](http://vimeo.com/channels/debugging) Video Series

## Tools
* [Github student developer pack](https://education.github.com/pack) - includes Digital Ocean $100 credit and more!
* [Basic unix commands](http://www.webmonkey.com/2010/02/learn_enough_unix_for_your_resume/#Basic_Commands)
* Checking code: [JSLint](http://www.jslint.com/) / [JSHint](http://www.jshint.com) / [ESLint](http://eslint.org/) / [StandardJS](http://standardjs.com/)
* Browser debugging: Chrome Developer Tools ([tutorial](https://developer.chrome.com/extensions/tut_debugging)) / Firebug ([tutorial](http://www.developerfusion.com/article/139949/debugging-javascript-with-firebug/))
* Mobile debugging [jsconsole.com](http://jsconsole.com)
* Sharing code snippets (useful for asking questions via email): [gist.github.com](http://gist.github.com)

## Debugging
* [A Brief Intro to Debugging](http://vimeo.com/channels/debugging) Video Series
* [p5.js debugging tutorial](http://p5js.org/tutorials/debugging/)

# p5.js Development Extended [DRAFT MATERIAL]
[THIS IS A ROUGH DRAFT]

This extended guide doesn't assume familiarity with concepts like unit testing, inline documentation, Javascript deployment workflows or specific tools like grunt or mocha. If you are comfortable with these and are looking for a quick start guide, please see [this page](https://github.com/processing/p5.js/wiki/Development).

The development of P5 is collaborative: we encourage you to participate and help us shape it. Here are some ways to contribute:

- **Add documentation to the code.** P5's main documentation is generated automatically based on structured comments written in the code describing classes, functions and their parameters. Browsing the files in the `src` folder and adding documentation where it's missing is a great way to get familiarized with p5. See syntax details [below].
- **Create unit tests.** P5 is tested using a unit testing framework. This means that for each feature there should be a test that asserts whether it does what it's supposed to do. Each time we generate a distribution of p5, all unit tests are run. This allows us to make changes more confidently: if all tests pass, we know we didn't break anything; if some tests fail, we know exactly what did. You can take a look at the existing tests in the `tests` folder. Adding tests to functions that don't have them is also a great way to get started. See how to do this in the [testing section].
- **Fix a bug.** Explain how Issues list is used in this project. 
- **Add a feature.**

Setting up: 
- start from beginning: fork repo and add upstream remote (and link to tutorial).
- explain why distribution needed: p5 runs in browser. browser gets library from server. can’t start running until all files have been transferred —> distribution. p5.js: all files combined into one. p5-min.js: one file w/o unnecessary spaces and line breaks. not readable, but faster download. 
- explain why grunt: javascript is interpreted, not compiled. but because p5 fairly big project still need a series of steps to generate distribution and also do some quality control: syntax checking (and good practices? check what lint does), running tests. repetitive task, so automated. task runner: grunt. to install grunt: package manager.

- specific setup instructions will be the same, but adding details like ‘Open Terminal’. 

Writing code:
- **Code Style.** "All code in any code-base should look like a single person typed it, no matter how many people contributed."
We recommend looking at [idiomatic.js](https://github.com/rwaldron/idiomatic.js/) for a JS style guide. Here is some sample code for quick reference: ///I'd want to be able to take a quick look: have to do a lot of scrolling before getting this on the idiomatic page. Should see what else to include though 
```
var i = 0,
      length = 100;

    for ( ; i < length; i++ ) {
      // statements
    }

    if ( true ) {
      // statements
    } else {
      // statements
    }

```
 
- **Inline Documentation.** Please add inline documentation to your code. This will allow us to generate a complete HTML documentation website automatically. We use [JSDoc](http://usejsdoc.org/); here is some example syntax: 
```
/**
   * Create a new empty PImage object.
   * @param  {Integer} width
   * @param  {Integer} height
   * @return {PImage}
   */
function Book(title, author) {
}
```

Testing:
- explain what the tools are before going over specific steps.
- include test snippet.

**Misc.**

Large Objects - Sometimes large Javascript objects get unruly and the code needs to be split across multiple files.  For this scenario, the style convention should be: p5.[ObjectName].[descriptor].js.  Note, code should be grouped in each file thematically.

For example, the p5.Renderer3D file is split across 3 js files: 
- p5.Renderer3D.js
- p5.Renderer3D.Retained.js
- p5.Renderer3D.Immediate.js
