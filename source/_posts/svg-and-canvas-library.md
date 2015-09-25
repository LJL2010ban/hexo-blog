title: 流行的svg/canvas动画库
date: 2015-08-03 13:16:08
categories: [javascript]
tags: [svg,canvas,libray,animation,frent-end]
---

因为需要用到动画，所以收集了一下现在比较流行的一些svg和canvas动画库，收集的不一定很全，主要是一些使用比较多的库。

#SVG
*	[SVG.JS](http://svgjs.com/)

	A lightweight library for manipulating and animating SVG.

	```
		// create svg drawing
        var draw = SVG('drawing')
        // create image
        var image = draw.image('images/shade.jpg')
        image.size(650, 650).y(-150)
        // create text
        var text = draw.text('SVG.JS').move(300, 0)
        text.font({
          family: 'Source Sans Pro'
        , size: 180
        , anchor: 'middle'
        , leading: 1
        })
        // clip image with text
        image.clipWith(text)
	```
*	[Snap.svg](http://snapsvg.io/)
	
	SVG is an excellent way to create interactive, resolution-independent vector graphics that will look great on any size screen. And the Snap.svg JavaScript library makes working with your SVG assets as easy as jQuery makes working with the DOM.
	
	```
	// First lets create our drawing surface out of existing SVG element
// If you want to create new surface just provide dimensions
// like s = Snap(800, 600);
var s = Snap("#svg");
// Lets create big circle in the middle:
var bigCircle = s.circle(150, 150, 100);
// By default its black, lets change its attributes
bigCircle.attr({
    fill: "#bada55",
    stroke: "#000",
    strokeWidth: 5
});
	```
		
*	[Raphael](http://raphaeljs.com/)
	
	Raphaël is a small JavaScript library that should simplify your work with vector graphics on the web. If you want to create your own specific chart or image crop and rotate widget, for example, you can achieve it simply and easily with this library.

	```
	// Creates canvas 320 × 200 at 10, 50
var paper = Raphael(10, 50, 320, 200);
// Creates circle at x = 50, y = 40, with radius 10
var circle = paper.circle(50, 40, 10);
// Sets the fill attribute of the circle to red (#f00)
circle.attr("fill", "#f00");
// Sets the stroke attribute of the circle to white
circle.attr("stroke", "#fff");
	```
*	[bonsai](https://bonsaijs.org/)
	
	A lightweight graphics library with an intuitive graphics API and an SVG renderer.

	```
	//Draw a 100x200 rectangle to the stage at {0,0}:
var r = new Rect(0, 0, 100, 200).addTo(stage);
//Fill it:
r.fill('blue');
//Change your mind... Make it darker:
r.fill(color('green').darker());
//Animate it:
r.animate('400ms', {
  x: 50,
  y: 50,
  width: 200
});
	```
*	[vivus](https://maxwellito.github.io/vivus/)
	
	Vivus is a lightweight JavaScript class (with no dependencies) that allows you to animate SVGs, giving them the appearence of being drawn. 

*	[svgweb](https://code.google.com/p/svgweb/)	

	SVG Web is a JavaScript library which provides SVG support on many browsers, including Internet Explorer, Firefox, and Safari. Using the library plus native SVG support you can instantly target ~95% of the existing installed web base.
	
	
*	[Processing](http://processingjs.org/)
	
	Processing.js is the sister project of the popular Processing visual programming language, designed for the web. Processing.js makes your data visualizations, digital art, interactive animations, educational graphs, video games, etc. work using web standards and without any plug-ins. 
	
	```
	// Global variables
float radius = 50.0;
int X, Y;
int nX, nY;
int delay = 16;
// Setup the Processing Canvas
void setup(){
  size( 200, 200 );
  strokeWeight( 10 );
  frameRate( 15 );
  X = width / 2;
  Y = height / 2;
  nX = X;
  nY = Y;  
}
// Main draw loop
void draw(){  
  radius = radius + sin( frameCount / 4 );  
  // Track circle to new destination
  X+=(nX-X)/delay;
  Y+=(nY-Y)/delay;  
  // Fill canvas grey
  background( 100 );  
  // Set fill-color to blue
  fill( 0, 121, 184 );
  // Set stroke-color white
  stroke(255);  
  // Draw circle
  ellipse( X, Y, radius, radius );                  
}
// Set circle's next destination
void mouseMoved(){
  nX = mouseX;
  nY = mouseY;  
}
	```
*	[Velocity.js](http://julian.com/research/velocity/)	
	
	Velocity is an animation engine with the same API as jQuery's $.animate(). It works with and without jQuery. It's incredibly fast, and it features color animation, transforms, loops, easings, SVG support, and scrolling. It is the best of jQuery and CSS transitions combined.
	
	```
	// Animate width, then animate height.
$("div")
    .velocity({ width: 75 }, 1500)
    .velocity({ height: 0 }, 1250);
	```
*	[jQuery SVG](http://keith-wood.name/svgRef.html)	
	
	A jQuery plugin that lets you interact with an SVG canvas.
	
	```
	var svg = $('#svgintro').svg('get'); 
svg.circle(130, 75, 50, {fill: 'none', stroke: 'red', strokeWidth: 3});
	```

#Canvas

*	[KineticJS](http://kineticjs.com/)
	
	KineticJS is a fast, robust, HTML5 Canvas Library that is no longer maintained.

*	[Fabric](http://fabricjs.com/)

	Fabric.js is a powerful and simple
Javascript HTML5 canvas library
	
	```
	// reference canvas element (with id="c")
var canvasEl = document.getElementById('c');
// get 2d context to draw on (the "bitmap" mentioned earlier)
var ctx = canvasEl.getContext('2d');
// set fill color of context
ctx.fillStyle = 'red';
// create rectangle at a 100,100 point, with 20x20 dimensions
ctx.fillRect(100, 100, 20, 20);
	```
*	[Paper.js](http://paperjs.org/)

	Paper.js is an open source vector graphics scripting framework that runs on top of the HTML5 Canvas. It offers a clean Scene Graph / Document Object Model and a lot of powerful functionality to create and work with vector graphics and bezier curves, all neatly wrapped up in a well designed, consistent and clean programming interface.

	```
	// Create a Paper.js Path to draw a line into it:
	var path = new Path();
	// Give the stroke a color
	path.strokeColor = 'black';
	var start = new Point(100, 100);
	// Move to start and draw a line from there
	path.moveTo(start);
	// Note the plus operator on Point objects.
	// PaperScript does that for us, and much more!
	path.lineTo(start + [ 100, -50 ]);
	```
	
*	[Easel.js](http://www.createjs.com/easeljs)

	A JavaScript library that makes working with the HTML5 Canvas element easy. Useful for creating games, generative art, and other highly graphical experiences.

	```
	//html
	<body onload="init();">
  <canvas id="demoCanvas" width="500" height="300"></canvas>
</body>
	//js
	var stage = new createjs.Stage("demoCanvas");
	//
	var circle = new createjs.Shape();
circle.graphics.beginFill("DeepSkyBlue").drawCircle(0, 0, 50);
circle.x = 100;
circle.y = 100;
stage.addChild(circle);
	//
	stage.update();
	```
	
	
*	[Pixi.js](http://www.pixijs.com/)

	2D webGL renderer with canvas fallback
	
	```
	var renderer = PIXI.autoDetectRenderer(800, 600,{backgroundColor : 0x1099bb});
document.body.appendChild(renderer.view);
// create the root of the scene graph
var stage = new PIXI.Container();
// create a texture from an image path
var texture = PIXI.Texture.fromImage('_assets/basics/bunny.png');
// create a new Sprite using the texture
var bunny = new PIXI.Sprite(texture);
// center the sprite's anchor point
bunny.anchor.x = 0.5;
bunny.anchor.y = 0.5;
// move the sprite to the center of the screen
bunny.position.x = 200;
bunny.position.y = 150;
stage.addChild(bunny);
// start animating
animate();
function animate() {
    requestAnimationFrame(animate);
    // just for fun, let's rotate mr rabbit a little
    bunny.rotation += 0.1;
    // render the container
    renderer.render(stage);
}
	```
*	[three.js](http://threejs.org/)（3D）
	
	Three.js is a library that makes WebGL - 3D in the browser - easy to use. While a simple cube in raw WebGL would turn out hundreds of lines of Javascript and shader code, a Three.js equivalent is only a fraction of that.
	
	```
	var scene = new THREE.Scene();
var camera = new THREE.PerspectiveCamera( 75, window.innerWidth / window.innerHeight, 0.1, 1000 );

var renderer = new THREE.WebGLRenderer();
renderer.setSize( window.innerWidth, window.innerHeight );
document.body.appendChild( renderer.domElement );
	```


	
	







