Hasta ahora, hemos declarado todo en el contexto "global" (observa que el contexto global es realmente el [objeto window](https://developer.mozilla.org/es/docs/Web/API/Window)).  En jerga p5, nos referimos a esto como "modo global".

```
var x = 100;
var y = 100;

function setup() {
  createCanvas(200,200);
}

function draw() {
  background(0);
  fill(255);
  ellipse(x,y,50,50);
}
```

Aunque esto es conveniente (y amigable) es importante notar que esto puede llevar a problemas y confusiones al momento de agregar otras bibliotecas de JavaScript o al tratar de incluir múltiples bosquejos de p5 en la misma página.  Una metodología más segura y avanzada es crear un bosquejo p5 como un objeto "instance" (instancia). Esto hace que tu bosquejo "viva" bajo una variable en particular. En otras palabras, tendremos un objeto (llamado por ejemplo "myp5") que almacena una referencia a un bosquejo p5.  Todo lo relacionado a ese bosquejo entonces tendrá que ser llamado con la sintaxis punto, i.e. `myp5.background(0);`. Esto recibe el nombre de modo "instance".

La sintaxis para el modo instance es la siguiente (el bosquejo a continuación es idéntico al ejemplo anterior):

```
var s = function( sketch ) {

  var x = 100; 
  var y = 100;

  sketch.setup = function() {
    sketch.createCanvas(200, 200);
  };

  sketch.draw = function() {
    sketch.background(0);
    sketch.fill(255);
    sketch.rect(x,y,50,50);
  };
};

var myp5 = new p5(s);
```

Esto puede ser un poco confuso, así que analícemoslo por partes.

```
var myp5 = new p5(s);
```

Esta parte nos debiera hacer sentido. Estamos creando un nuevo objeto llamado `myp5` (el nombre inventado de nuestra variable).  La llamamos meidante el constructor `new p5()`.  El código para `function p5()` puede ser encontrado en el [código fuente de p5.js](https://github.com/lmccart/p5.js/blob/main/src/core/core.js#L28). Pero no estamos solo creando un bosquejo "en blanco", estamos pasando un arugmento llamado `s` que servirá como la base para el código de ese bosquejo. 

¿Y qué es `s`?

```
var s = function( sketch ) {

};
```

`s` es la semilla de nuestro bosquejo p5. Es una función que toma un argumento, un objeto `sketch` y le añade propiedades a ese `sketch`. Las propiedades son cosas que serán necesarias para el bosquejo p5, funciones como `setup()` y `draw()`.

```
var s = function( sketch ) {
  sketch.setup = function() {
  };
};
```

Esas funciones tienen su propio contexto, aunque además tienen acceso a cualquier cosa declarada alrededor de ellas.

```
var s = function( sketch ) {
  var x = 100; 
  var y = 100;

  sketch.draw = function() {   // draw() es una función interna, una "closure"
    sketch.rect(x,y,50,50);    // draw() usa variables (x,y) declaradas en la función s padre (parent)
  };
};
```

Esto se conoce como [closure](https://developer.mozilla.org/es/docs/Web/JavaScript/Closures), una de las características más poderosas de los lenguajes de programación funcional como JavaScript. 

Puedes pensar en el propósito de s como inicializar todo lo que necesitamos para un bosquejo p5. Un vez que está todo listo, es pasada al constructor `new p5()` y nuestra variable `myp5` se encarga de llevar el registro de todo lo que está acompañando originalmente al argumento `sketch`.  Como `myp5` un objeto instancia de p5 (y por lo tanto hereda todo lo que necesitamos del prototipo p5), todo lo que escribimos en sketch funcionará. 


## Instancia anónima

Como hemos visto en JavaScript, cada vez que pasamos una función a otra función es una oportunidad para declarar esa función de forma anónima. Aquí está la forma en que escribimos lo anterior.
```
var s = function( sketch ) {
   // vacío
};
var myp5 = new p5(s);
```

Y ahora sin una variable separada `s`.

```
var myp5 = new p5( function( sketch ) {
  // vacío
});
```

Ahora rellenada con todos los detalles, se ve así:

```
var myp5 = new p5( function( sketch ) {

  var x = 100; 
  var y = 100;

  sketch.setup = function() {
    sketch.createCanvas(200, 200);
  };

  sketch.draw = function() {
    sketch.background(0);
    sketch.fill(255);
    sketch.rect(x,y,50,50);
  };
});
```

Si crees que esta sintaxis es confusa, felicitaciones, eres un se humano. Sí, involucra escribir menos, pero por claridad, verás todos los ejemplos escritos de la forma más larga.

Una nota final: cuando creas una instancia de p5, puedes especificar un segundo argumento (id de elemento HTML) que actúa como padre (parent) de todos los elementos creados por el bosquejo. Por ejemplo, digamos que tienes:

```
<body>
  <div id = "p5sketch">
  </div>

  <p>HTML adicional</p>
</body>
```

Ahora puedes decir:

```
var myp5 = new p5(s,'p5sketch');
```

Y así todos los elementos serán creados dentro esa div.


## Otras bibliotecas de JavaScript

* [Tutorial para integración con otras bilbiotecas](https://github.com/processing/p5.js/wiki/Integrando-otras-bibliotecas)


## HTML5 Video

p5.js will likely include features for video playback and capture in the future, but it is currently not a capability.  However given that HTML5 supports video and capture (via [WebRTC](http://www.webrtc.org/)) it is fairly easy for us to integrate these features into a p5 sketch.

To embed a video on a web page, it's as easy as creating a video element.

```
<video><source src="file.mov"></video>
```

You can set various properties of the video via attributes.

```
<video loop="true" autoplay="true"><source src="fingers.mov"></video>
```

We could of course type the HMTL directly into index.html, but we can also create it dynamically via p5.

```
video = createHTML('<video id=\'vid\'><source src=\'fingers.mov\'></video>');
video = document.getElementById('vid');  // Grab the dom element itself
video.play();                            // We can call methods on that element like play()
video.setAttribute('loop', true);        // We can also set attributes
video.setAttribute('controls',true);
```

[More about HTML5 audio and video](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Using_HTML5_audio_and_video).

If we want to draw on top of the video we could create a transparent canvas element.  However, in some projects it may be advantageous to copy the pixels of a video into a canvas rather than display the video element itself on the page.  This can be accomplished but first setting the video element's display style to none.

```
video.style.display = 'none';
```

We can then draw the video to the canvas using `drawImage()`.  It should be noted that `drawImage()` is [part of the HTML5 Canvas API](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D).  While used behind the scenes in p5, it's not something we've used directly ourselves.  It's most likely this wiki will become quickly out of date if/when p5 integrates video drawing, but for now we'll have to grab our canvas graphics context and manually draw the video.  The code looks like this:

```
// Video
var video;

// Drawing context
// Temporary as eventually p5 may support drawing video into canvas directly?
var context;

function setup() {
  video = createHTML('<video id=\'vid\'><source src=\'fingers.mov\'></video>');
  video = document.getElementById('vid');
  video.play();

  var canvas = createCanvas(640, 360);
  // need to keep track of the context to draw the video
  context = canvas.elt.getContext('2d');
}

function draw() {
  background(51);
  // Draw video into canvas
  context.drawImage(video,0,0,width,height);
};
```

## Capture with WebRTC

Now that we have recorded video working, we can take a few extra steps and get live capture from a user.  First we make an empty video element.

```
// Make an invisible video DOM element
video = createHTML('<video id=\'vid\'></video>');
video = document.getElementById('vid');
video.setAttribute('autoplay',true);
video.style.display = 'none';
```

Now instead of saying `<source src="file.mov">` we need to assign the video's source to a live capture stream.  To do this, we are going to use [navigator.getUserMedia()](https://developer.mozilla.org/en-US/docs/Web/API/Navigator.getUserMedia).  This navigator object is a property of window that provide additional browser functionality.   It is not consistently available across all browsers, however.  We can get a little bit of cross-browser support by checking to see if it is available and if not, trying a different, analogous method.

```
navigator.getUserMedia = navigator.getUserMedia || 
                         navigator.webkitGetUserMedia || 
                         navigator.mozGetUserMedia || 
                         navigator.msGetUserMedia;
```

`getUserMedia()` takes three arguments.  

The first argument is an object with a video and audio property.  This indicates whether we want to capture from a camera, microphone, or both.  For example: `{ video: true, audio: false }` gives us video stream only.

The second argument is a function that is triggered when getUserMedia() has been successful (note a user has to approve access to capture device).  What we'll do here is take the argument to that function (a media stream) and assign it to our video element, i.e.

```
function(stream) {
  video.src = window.URL.createObjectURL(stream);
}
```

The last argument is a function that is triggered if the user rejects our request to capture. 

```
function(e) {
  console.log('User said no!', e);
} 
```

Putting it all together, it looks like so:

```
// Make an invisible video DOM element
video = createHTML('<video id=\'vid\'></video>');
video = document.getElementById('vid');
video.setAttribute('autoplay',true);
video.style.display = 'none';

// For cross-browser support
navigator.getUserMedia  = navigator.getUserMedia || navigator.webkitGetUserMedia || navigator.mozGetUserMedia || navigator.msGetUserMedia;

// Get a stream of video from the user
navigator.getUserMedia(
  // First argument is an object that tells us if we want audio and/or video
  { video: true, audio: false }, 
  // Second argument is a function that assigns a 'stream' to the video's source
  function(stream) {
    video.src = window.URL.createObjectURL(stream);
  }, 
  // Third argument is the callback if the user rejected
  rejected
);  

var rejected = function(e) {
  // The user rejected capturing
  // We could handle this however we want
  console.log('User said no!', e);
};
```

Notice how we are using an anonymous function for the second argument and a function stored in a variable for the third one.  This is arbitrary and is just meant to demonstrate both possibilities.



