You can always just host the HTML and JS files of your p5.js project online and visit the URL where they're located to see them running. However, you might want to integrate/embed a sketch into an existing page or blog. Here are a few ways to do it.

## Using iframes

The simplest solution is to use iframes. An iframe is basically a window into a nested page within a page, sandboxed from the rest of your page. For classes, I have students host their work and turn in a link to running sketches. Then I can embed their sketches or examples I create in iframes on a wordpress blog or class site.

Embed code for the iframe:
```html
<iframe src="http://p5js.org/test/embed.html" width="600px" height="400px"></iframe>
```

and styling for the iframe (this could directly into a wordpress post or in a stylesheet):
```html
<style> iframe{ border: none; } </style>
```

Only trick here is that you need to manually set the size of the iframe, so it works best if things are a standard size.

## Using p5.js-widget

@toolness has created an awesome p5.js widget that can be used to embed code snippets and examples on a page. It is a work in progress. You can see documentation of how to use it here:
https://toolness.github.io/p5.js-widget/

![](http://i.imgur.com/4ecSjpM.png)

## Other options

These are just a few of the best I've tried, there are many tools like these that fit different needs and situations.

#### Ace editor
The examples on the [learn page](http://p5js.org/learn/#examples) use [ace editor](http://ace.c9.io/#nav=about) rather than the render.js script because it's less hacky and has better support for editing (it includes linting, dynamic code highlighting, etc). This one requires a little custom configuration, there is a tutorial to get you started here: http://ace.c9.io/#nav=howto. 

#### CodePen

[CodePen](http://codepen.io/) is a web-based editor with a friendly interface. It has some nice features that let you embed your pens in other sites, text them to a phone for easy mobile access to a link, and fork. It is nice for workshop settings where you don't want people to spend much time getting set up / downloading editors, etc. You will need to link to the [CDN](http://jsdelivr.com/#!p5.js) to include p5.js libraries. The formatting gets a little wonky if you try to magnify it for class demos on screen, but there are "pro" and "professor" modes that I haven't coughed up the $ to try.

#### JSFiddle

[JSFiddle](http://jsfiddle.net) is similar to codepen, slightly different interface but similar features. This can also be [embedded](http://doc.jsfiddle.net/use/embedding.html) on external sites and forked. You will need to link to the [CDN](http://jsdelivr.com/#!p5.js) to include p5.js libraries.