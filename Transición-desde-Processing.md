### Resumen de diferencias

El lenguaje p5.js es muy similar al lenguaje Processing, con unas pocas diferencias:

+ Como puedes pensar en tu bosquejo como más que solo el lienzo para dibujar, `size()` (tamaño) ha sido reemplazado por `createCanvas()` (crear lienzo), para sugerir la posibilidad de crear otros elementos.
+ `frameRate(num)` define la tasa de cuadros, pero la variable `frameRate`ha sido removida. Para obtener la actual tasa de cuadros, llama a la función `frameRate()` sin argumentos.
+ JavaScript no siempre carga todo de forma síncrona, existen algunas opciones para lidiar con esto:
     + Todos los métodos de carga (load) poseen un argumento opcional de callback (llamada). Esto es, una función que es llamada luego de que el archivo ha sido cargado. 
     + De forma alternativa, puedes ubicar todas las llamadas de carga (load) en un método `preload()` (precarga) que ocurre antes de `setup()` (configuración). Si existe un método preload, setup espera hasta que todo esté cargado, ver este [ejemplo con imagen](http://p5js.org/es/examples/image-alpha-mask.html).
+ La variable `mousePressed` ha sido reemplazada por `mouseIsPressed`.
+ Además de los eventos de ratón (mouse), existen eventos de toque (touch), cuya correspondencia es la siguiente:
     + `mouseX` ~ `touchX`
     + `mouseY` ~ `touchY`
     + `mousePressed()` ~ `touchStarted()`
     + `mouseDragged()` ~ `touchMoved()`
     + `mouseReleased()` ~ `touchEnded()`
     + Existe un arreglo `touches[]` (toques) que contiene una serie de objetos con propiedades x e y correspondientes a las posiciones de cada dedo.
+ `push/popMatrix()`, y `push/popStyle()` han sido reemplazados con `push()` y `pop()`, el equivalente de llamar tanto a los métodos de matriz (matrix) y estilo (style) de forma conjunta.
+ Por defecto, todo está en el espacio de nombres global, y puedes crear tus bosquejos como lo haces en Processing. Sin embargo, existe algo que llamamos modo instancia (instance mode) para crear un bosquejo p5 que se comporta bien con el resto del código corriendo en tu página. Revisa este  [ejemplo del modo instancia](http://p5js.org/es/examples/instance-mode-instantiation.html) y este [tutorial de modo global vs instancia](https://github.com/processing/p5.js/wiki/Modos-Global-e-Instance).
+ En el modo global, la variable p5 y los nombres de funciones no están disponibles fuera de `setup()`, `draw()`, `mousePressed()`, etc. (Excepto en el caso donde están ubicadas dentro de funciones que son llamadas por uno de estos métodos.) Esto significa que que cuando se declaran variables antes de `setup()`, necesitarás asignarles valores dentro de `setup()` si quieres usar estas funciones de p5. Por ejemplo:

  ```javascript
  var n;
  function setup() {
    createCanvas(100, 100);
    n = random(100);
  }
  ```

+ No todas las características de Processing están implementadas en p5.js, ¡pero estamos trabajando en eso! En este momento no existe un equivalente de PShape. El modelo de cámara en p5js sigue siendo muy básico, con solo una posición del ojo y sin un eje de dirección de "hacia donde mirar". Revisa la [referencia](http://p5js.org/es-reference/) para buscar documentación al día sobre las funciones.
 
### Notas sobre JavaScript
+ Las variables no tienen un tipo. Usa var en vez de float, int, double, long, char, String, Array, etc. No necesitas especificar valores de retorno o tipos de parámetros de las funciones.
+ Una var puede ser cualquier cosa -- cualquiera de los tipos mencionados, pero también funciones.
+ Los arreglos son construidos de forma muy simple (no se necesita ArrayList de Processing) e incluyen muchas características, revisa este [ejemplo de arreglo](http://p5js.org/es/examples/arrays-array.html) y más sobre arreglos de JavaScript [aquí](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/Array)
+ JavaScript usa algo llamado prototype (prototipo) para construir algo similar a los objetos a partir de clases de Java. Revisa este [ejemplo de objetos](http://p5js.org/es/examples/objects-objects.html) y más sobre objetos JavaScript [aquí](https://developer.mozilla.org/es/docs/Web/JavaScript/Guide/Trabajando_con_objectos).

### Ejemplos de conversión

#### Bosquejo básico

Esta es la configuración básica de un bosquejo en Processing y uno en p5.js. Observa que p5.js también requiere un archivo HTML en blanco que enlaza la biblioteca p5.js y tu archivo de bosquejo (sketch) en el encabezado(header (ver [Empezar](http://p5js.org/es/get-started/)).

```java
void setup() {
  // contenidos de setup()
}

void draw() {
  // contenidos de draw()
}
```


```javascript
function setup() {
  // contenidos de setup()
}

function draw() {
  // contenidos de draw()
}
```

#### Convertir un bosquejo de Processing a p5.js

Aquí se presentan dos ejemplos de bosquejos que han sido convertidos de Processing a p5.js. Los cambios hechos son señalados en los comentarios, todas las otras líneas quedan igual.

```javascript
/**
 * Este ejemplo puede ser encontrado en la sección de ejemplos de Processing
 * que está incluida en el ambiente de desarrollo de Processing.
 * Processing > Examples > Basics > Form > Bezier
 * Adaptado por Evelyn Eastmond
 */

function setup() {           // **cambio** void setup() a function setup()
  createCanvas(640, 360);    // **cambio** size() a createCanvas()
  stroke(255);               // stroke() queda igual
  noFill();                  // noFill() queda igual
}

function draw() {                         // **cambio** void draw() a function draw()
  background(0);                          // background() queda igual
  for (var i = 0; i < 200; i += 20) {     // **cambio** int i a var i
    bezier(mouseX-(i/2.0), 40+i, 410, 20, 440, 300, 240-(i/16.0), 300+(i/8.0)); // bezier() queda igual
  }
}

```

```javascript

/**
 * Este ejemplo puede ser encontrado en la sección de ejemplos de Processing
 * que está incluida en el ambiente de desarrollo de Processing.
 * Processing > Examples > Topics > Interaction > Follow3
 * Adaptado por Evelyn Eastmond
 */

var x = new Array(20);  // **cambio** float[] x = new float[20] a new Array(20)
var y = new Array(20);  // **cambio** float[] y = new float[20] a new Array(20)
var segLength = 18;                                 // **cambio** float to var

function setup() {                          // **cambio** void setup() a function setup()
  createCanvas(640, 360);                   // **cambio** size() a createCanvas()
  strokeWeight(9);                          // strokeWeight() queda igual
  stroke(255, 100);                         // stroke() queda igual
  for(var i=0; i<x.length; i++) {         // inicializa el arreglo
    x[i]=0;
    y[i]=0;
  }
}

function draw() {                           // **cambio** void draw() a function draw()
  background(0);                            // background() is the same
  drawSegment(0, mouseX, mouseY);           // functions calls, mouseX and mouseY are the same
  for(var i=0; i<x.length-1; i++) {         // **cambio** int i a var i
    drawSegment(i+1, x[i], y[i]);           // function calls are the same
  }
}

function drawSegment(i, xin, yin) {         // **cambio** void drawSegment() a function drawSegment(), quita las declaraciones de tipo de dato
  var dx = xin - x[i];                      // **cambio** float a var
  var dy = yin - y[i];                      // **cambio** float a var
  var angle = atan2(dy, dx);                // **cambio** float a var, atan2() queda igual
  x[i] = xin - cos(angle) * segLength;      // cos() queda igual
  y[i] = yin - sin(angle) * segLength;      // sin() queda igual
  segment(x[i], y[i], angle);               // las llamadas a funciones quedan igual
}

function segment(x, y, a) {                 // **cambio** void segment() a function segment(), quita las declaraciones de tipo de dato
  push();                            		// pushMatrix() a push()
  translate(x, y);                          // translate() queda igual
  rotate(a);                                // rotate() queda igual
  line(0, 0, segLength, 0);                 // line() queda igual
  pop();                              		// popMatrix() a pop()
}
```

#### Convertir un bosquejo de p5.js a Processing

Aquí se presentan dos ejemplos de bosquejos que han sido convertidos de  p5.js a Processing. Los cambios hechos son señalados en los comentarios, todas las otras líneas quedan igual.

```java
/**
 * Este ejemplo puede ser encontrado en la sección de ejemplos de Processing
 * que está incluida en el ambiente de desarrollo de Processing.
 * Processing > Examples > Basics > Form > Bezier
 */

void setup() {                         // **cambio** function setup() a void setup()
  size(640, 360);                      // **cambio** createCanvas() a size()
  stroke(255);
  noFill();
}

void draw() {                          // **cambio** function draw() a void draw()
  background(0);
  for (int i = 0; i < 200; i += 20) {  // **cambio** var i a int i
    bezier(mouseX-(i/2.0), 40+i, 410, 20, 440, 300, 240-(i/16.0), 300+(i/8.0));
  }
}
```

```java
/**
 * Este ejemplo puede ser encontrado en la sección de ejemplos de Processing
 * que está incluida en el ambiente de desarrollo de Processing.
 * Processing > Examples > Topics > Interaction > Follow3
 * Basado en código de Keith Peters. 
 */

float[] x = new float[20];                       // **cambio** arreglo de 0s a float[] x = new float[20]
float[] y = new float[20];                       // **cambio** arreglo de 0s a float[] x = new float[20]
float segLength = 18;                            // **cambio** var a float

void setup() {                                   // **cambio** function setup() a void setup() 
  size(640, 360);                                // **cambio** createCanvas() a size()
  strokeWeight(9);
  stroke(255, 100);
}

void draw() {                                    // **cambio** function draw() a void draw()
  background(0);
  dragSegment(0, mouseX, mouseY);
  for(int i=0; i<x.length-1; i++) {              // **cambio** int i a var i
    dragSegment(i+1, x[i], y[i]);
  }
}

void dragSegment(int i, float xin, float yin) {  // **cambio** function drawSegment() a void drawSegment(). agregar declaraciones de tipo de dato.
  float dx = xin - x[i];                         // **cambio** var a float
  float dy = yin - y[i];                         // **cambio** var a float
  float angle = atan2(dy, dx);                   // **cambio** var a float
  x[i] = xin - cos(angle) * segLength;
  y[i] = yin - sin(angle) * segLength;
  segment(x[i], y[i], angle);
}

void segment(float x, float y, float a) {        // **cambio** function segment() a void segment(). agregar declaraciones de tipo de dato.
  pushMatrix();
  translate(x, y);
  rotate(a);
  line(0, 0, segLength, 0);
  popMatrix();
}
```

#### Sobre las variables

En p5.js, todas las variables (sean números, strings, arreglos, funciones, objetos, ¡lo que sea!) son declaradsa usando el símbollo "var". En Processing, tienes que especificar el tipo de datos de la variable.

Por ejemplo, en vez de:

```javascript
boolean button = false;
```

escribirías
```javascript
var button = false;
```

o 

en vez de:

```javascript
float x = 100.3;
```

escribirías
```javascript
var x = 100.3;
```

Aquí hay un resument de los tipos de datos soportados en Processing (esta tabla fue tomada de [Getting Started with Processing](http://shop.oreilly.com/product/0636920000570.do)).

Nombre | Descripción | Rango de valores
--- | --- | ---
int | Números enteros (sin decimales) | -2,147,483,648 a 2,147,483,647
float | Números de punto flotante | -3.40282347E+38 a 3.40282347E+38
boolean | Valor lógico | true o false (verdadero o falso)
char | Caracter único | A-z, 0-9, y símbolos
String | Secuencia de caracteres | Cualquier letra, palabra, frase, entre otros
PImage | Imagen PNG, JPG, o GIF | N/A
PFont | Tipografía VLW; usa la herramienta Create Font | N/A
PShape | Archivo SVG | N/A



### What next?

+ Check out the [p5.js reference](http://p5js.org/reference/) for up to date documentation.
+ Play with the examples and demos on the [tutorials page](http://p5js.org/tutorials).