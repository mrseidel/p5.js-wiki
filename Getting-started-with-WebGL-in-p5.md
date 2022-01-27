The following tutorial was inspired by the introduction to P3D in Processing 2.0+, which can be found here:
https://processing.org/tutorials/p3d/

# Introducing WebGL in p5.js

In p5.js, there are two render modes: P2D (default renderer) and WEBGL.  Both render modes utilize the html canvas element, however by enabling the WEBGL "context" on the canvas, we can now draw in both 2D and 3D.  To enable WEBGL, simply specify as the third parameter in the createCanvas() function.

```javascript
function setup() {
  createCanvas(200, 200, WEBGL);
}
```

# 3D coordinate system

If you've been coding in p5.js for a while you probably know the Cartesian coordinate 0,0 (x,y) is located in the top left corner of our drawing canvas. In WEBGL mode we introduce a third dimension:  Z.  So how do we handle the z-coordinate? I'm glad you asked! The z-dimension is the axis that points toward you from the screen. A helpful mnemonic device for remembering which way the axes point in p5.js (WEBGL), is the "left-handed" rule. Point your left index finger to the right, and your middle finger downward, and your thumb will automatically point toward you. The direction your fingers are pointing are exactly mapped to the axes. The 0,0,0 (x,y,z) point is located in the middle of the canvas.

Let’s look at a quick example:

```javascript
function setup() {
  createCanvas(windowWidth, windowHeight, WEBGL);
}

function draw(){
  background(255);
  box();
}
```

This should draw a box in the center of your canvas.

# Translate, Rotate

We feel that centering objects by default makes more sense as a starting point for thinking about 3D space, and is especially fast if you want to draw a couple of geometric primitives, but if you prefer to move the origin back to the top left corner similar to 2D mode, simply apply a negative width and height translation:

```javascript
function draw(){
  background(255);
  translate(-width/2,-height/2,0); //moves our drawing origin to the top left corner
  box();
}
```

Calling translate(x,y,z), applies a transformation to the Model Matrix.  This is a technical way of saying, we are moving the origin coordinate for our drawing.  If we write the following code:

```javascript
box();
translate(100,100,-100);
box();
```
This code draws a box, then translates our model matrix 100 units to the right, 100 units down, and 100 units away from the viewer, and finally draws another box at the new translated origin.  There are two important things to note here.  First, translate() always applies to draw functions called afterward.  Second, you may have noticed we use the generic term, “units,” instead of “pixels”.  The reason for this is because the actual distance of translation largely depends on our virtual camera view.  Model Matrix + View Matrix (i.e. camera) creates the perceived translation distance.  In the next section we’ll discuss the virtual camera in greater detail but before we do that, let’s talk about rotation.  Another type of model matrix transformation in 3D is rotate().  There are 4 different rotation functions in WEBGL mode:

```javascript
rotate(angle, [x,y,z]);
rotateX(angle);
rotateY(angle);
rotateZ(angle);
```
A helpful way to remember which function to use for rotation is, “rotate around the ____ axis”
Therefore, If we want to do a barrel roll around the X axis, we’d write:

```javascript
rotateX(radians(45));
```
All rotation functions take a numerical parameter in radians.  

# Camera and view
In WEBGL mode, there are currently 3 camera functions.  

```javascript
camera(x,y,z)
perspective(fovy, aspect, near, far)
ortho(left, right, bottom, top, near, far)
```

The default camera view in WEBGL mode is perspective with a 60 degree field of view.  This is created when you initialize WEBGL mode in createCanvas().  To override the default camera options, simply call perspective() or ortho().  In a perspective view, objects closer to the viewer in the z-plane appear larger than those farther away.  In orthographic view (ortho()), objects of the same dimensions appear to be the same size even if they are farther away on the z-plane.  For example:

```javascript
function setup(){
  createCanvas(500,500,WEBGL);
  ortho(-width, width, height, -height/2, 0.1, 100);
}
function draw(){
  box(30);
  translate(100,100,-100);
  rotate(PI/4, [1,1,0]);
  box(30);
}
``` 
For more information on the camera in 3D, check out the excellent P3D tutorial here: https://processing.org/tutorials/p3d/

At the time of this writing, only one camera is supported per canvas.  However, this may change in the future.

# 3D Primitives Shapes

There are 7 different 3D geometry primitives in p5.js.  

```javascript
box()
plane()
sphere()
ellipsoid()
cone()
cylinder()
torus() 
```

Each of these primitives take only size parameters, not position.  For example:

```javascript
box(10,20,30); //draws a box of width: 10, height: 20, and depth: 30
cone(40, 100, 100);//draws a cone with radius: 40, height: 100, and a detail of 100
```

You may be saying, “Hey now, what’s this detail you speak of?!”  In webgl mode, the user can specify how smooth the curves and lines should be drawn.  Larger detail numbers create smoother curves, however at the expense of the graphics renderer.  Generally, leaving the default detail is sufficient when drawing primitives:

```javascript
cone(40,100);//draws a cone with radius: 40, height: 100, and a default detail: 24
``` 

One important difference between drawing primitives in 3d and drawing primitives in 2d is that 3d primitives take size parameters, but not position.  To reposition 3D primitives, simply call translate(x,y,z); as per the Translation section above.

# Custom shapes & 2D drawing in WEBGL
In the introduction, we mentioned that WEBGL mode supports both 2D and 3D drawing.  While WEBGL is optimized for 3D, you don’t necessarily have to always draw in 3D.  For 2D drawing, there are the point(), line(), triangle() and quad() functions.  For example,

```javascript
for(let i = 0; i < 500; i+=100){
  push();
  fill(i * 0.1, 100, 100);

  //line
  translate(0, 100, 0);
  line(-100, 0, i, 100, 0, i);

  //triangles
  translate(0, 100, 0);
  triangle(
    0, sin( i + frameCount * 0.1) * 10, i, 
    60, 60, i, 
    -60, 60, i);

  //quad
  translate(0, 200, 0);
  quad(
    -100, i, 0,
    100, i, 0,
    -100, 100, i,
    100, 100, i
    );
  pop();
}
```

If we look more closely at the quad() function, you’ll notice there are 12 parameters- 4 groups of 3 (x,y,z).  Even though we are drawing a 2-dimensional shape, we still need to use the z-coordinate for each vertex.

Another way of drawing custom shapes in WEBGL mode is to use beginShape() and endShape().  This works exactly the same in 2d mode as it does in WEBGL, except in WEBGL, vertices receive x, y, and z as location coordinates.

```javascript
beginShape();
vertex(100,23,-100);
vertex(200,23,-50);
vertex(150, 45,-100);
endShape();
```

# Textures
At the time of this writing, p5.js supports video, image, and offscreen 2d renderers as textures in WEBGL mode.  A texture is like a “skin” that wraps around a 3D geometry.  For example, if you want a static image to “texture” a box, you would write something like this:

```javascript
let img;
function preload(){
  img = loadImage(“path/to/img.jpg”);
}
function setup(){
  createCanvas(500,500,WEBGL);
}
function draw(){
  background(255);
  texture(img);
  box(45);
}
```
Loading images for texturing inside the preload() method is generally a best practice, but it is especially helpful when working with video since video files are generally larger than static images and can take therefore extra time to load.

To texture a beginShape() graphic you will need to pass in u,v coordinates. These coordinates map to the texture being applied. With textureMode(NORMAL) we tell p5 to normalize these values between 0 and 1. See the [textureMode() reference](https://p5js.org/reference/#/p5/textureMode) for more info.

Below is an example:

```javascript
let img;
function setup() {
  createCanvas(windowWidth, windowHeight, WEBGL);
  img = loadImage("path/to/img.jpg");
  textureMode(NORMAL);
}

function draw() {
  background(200);
  texture(img)

  // Assuming img has 100 pixels width and height
  beginShape();
  vertex(0, 0, 0, 0, 0);
  vertex(100, 0, 0, 1, 0);
  vertex(100, 100, 0, 1, 1);
  vertex(0, 100, 0, 0, 1);
  endShape(CLOSE);
}
```


# Text
To work with text in webgl mode, you have two options: use the 2d p5.js API to render to an offscreen image, or use the native webgl `text()` method. There are advantages & disadvantages to both which are discussed below:

## Offscreen Renderer
You can draw your text to an offscreen renderer first, and then use it as a texture.

Advantages:
- You can use the same fonts available to the 2d p5.js API, including the browser's built-in fonts (eg, 'mono', 'sans', etc...).
- You can use `stroke()` to draw an outline around the glyphs.
- The performance may be better, especially if you are able to render your text only once in `setup()` and reuse that texture in your `draw()` function.

Disadvantages:
- The fidelity of the text may not be as high as with the `text()` method due to pixellation when zooming or inaccuracies in anti-aliasing when tilting the text image.

Here is an example of using an offscreen renderer to draw text:
```javascript
let pg;
function setup(){
  createCanvas(100, 100, WEBGL);
  pg = createGraphics(256,256);
}
function draw(){
  background(0);
  pg.background(255);
  pg.text('hello world!', 50, 50);
  //pass graphics as texture
  texture(pg);
  plane(100);
}
```

## webgl `text()`
The webgl version of the `text()` method works very similarly to the 2d version. However there are a few differences:

Disadvantages:
- You can only use use opentype/truetype fonts loaded in your [`preload()`](https://p5js.org/reference/#/p5/preload) function using the [`loadFont()`](https://p5js.org/reference/#/p5/loadFont) method. You must either place those font files in a location accessible from your sketch, or use a [CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)-compatible webl URL.
- [`stroke()`](https://p5js.org/reference/#/p5/) is not currently supported.

Advantages:
- The fidelity of the rendered text should be better, especially when zooming & tilting.
- The performance may be better, especially if the text changes regularly and you are unable to cache the offscreen image used in the previous method.

Here is an example of loading an opentype font and using it to draw text with the webgl `text()` method:
```javascript
let myFont;
function preload() {
  myFont = loadFont('assets/AvenirNextLTPro-Demi.otf');
}

function setup() {
  fill('#ED225D');
  textFont(myFont);
  textSize(36);
  text('p5*js', 10, 50);
}
```

# Lights and Materials
The last big inclusion in WEBGL mode is lights.  Lighting is a simple but powerful way to provide depth and realism to p5.js sketches.  At the time of this writing there are 3 types of light functions in p5.js:

```javascript
ambientLight();
directionalLight();
pointLight();
```

```javascript
ambientLight(255,0,0); //even red light across our objects
box(25);
```
ambientLight() is the simplest of the three functions, and it provides even (omnidirectional) ambient lighting to objects drawn afterward.  It takes a p5.Color or r,g,b numerical values as parameters.

```javascript
directionalLight(r, g, b, x, y, z):
```

```javascript
let dirY = (mouseY / height - 0.5) *2;
let dirX = (mouseX / width - 0.5) *2;
directionalLight(250, 250, 250, dirX, -dirY, 0.25);
ambientMaterial(250);
sphere(50, 64);
```
directionalLight rays shine in a given direction, but they do not have a specific point of origin, and therefore cannot be positioned closer or farther away from a geometry.  The directionalLight vector can also be considered the angle in which light hits the geometry.  Therefore, a negative y-value will light a given geometry from below.

pointLight():
On the other hand, pointLight takes a color and a location as parameters.  The major difference between directionalLight and pointLight is pointLight shines from a specific point of origin, and therefore reflects differently when it is farther vs. nearer the object.

In the real world, light reflects off objects differently, depending on their angle of reflection as well as the object's’ material.  At the time of this writing there are four types of materials in p5.js:

```javascript
normalMaterial()
ambientMaterial()
specularMaterial()
```

`normalMaterial()` does not take any parameters, it automatically maps a geometry’s normal vectors to RGB colors.  For more information on geometry normals, we find [this Wikipedia entry](https://en.wikipedia.org/wiki/Normal_(geometry)) to be pretty helpful.

(At one time, there was also a `basicMaterial()` which fills the following geometry with a color, but is not affected by any of the light functions(). However, due to it being the same as `fill()`, it was removed and the function `fill()` can be used with `WEBGL` for the "basic material" functionality.)

`ambientMaterial()` is like `fill()`, however the total color is affected by light functions that precede it.  

`specularMaterial()` is the most “realistic” of the four materials.   Specular material is a technical way of describing a material that reflects light in a single direction.  This effect is often perceived in the real world as being glassy, water-like, or perhaps in the above example, a billiards ball.
For example:

```javascript
pointLight(255, 255, 255, mouseX, mouseY, 0);
specularMaterial(250, 0, 0);
sphere(50, 64);
```
  


