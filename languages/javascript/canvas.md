## Basics
> canvas is the a rendenring engine which can be used to draw shapes and create animations by pinpointing the (x, y) coords

### Basic Full Screen Setuo
```js
const canvas = document.getElementById("canvas");
const ctx = canvas,getContext("2d");

canvas.width = window.innerWidth;
canvas.height = window.innerHeight;
```

```html
<canvas id="canvas"></canvas>
```

```css
#canvas {
    position: absolute;
    background-color: black;
}
```

### Lines
`ctx.beginPath();` &rarr; starts a new drawing path

`ctx.moveTo(x, y);` &rarr; moves the pen to a position without drawing

`ctx.lineTo(x, y);` &rarr; draws a line to a position from current

`ctx.stroke();` &rarr; draws the outline of the path

`ctx.fill();` &rarr; fills the inside of the path

`ctx.lineWidth = 5;` &rarr; sets line thickness

`ctx.stokeStyle = "color"` &rarr; sets outline color. can also use `"#00FF00"`

`ctx.fillStyle = "color"` &rarr; sets fill color

### Circle
```js
// adds a circle or arc to the current path
ctx.arc(x, y, radius, start angle, end angle, isCounterClockwise);
```

`x, y` → center position of the circle on the canvas
(example: 150, 150 = circle centered at that point)

`radius` → size of the circle from center to edge
(example: 50 = circle radius is 50px)

`startAngle, endAngle` → where the arc starts and stops, measured in radians
(example: 0 to Math.PI * 2 = full circle)

`isCounterClockwise` → direction the arc is drawn
(false = clockwise, true = counter-clockwise)

> **full circle** &rarr; Math.PI * 2 <br>
> **half circle** &rarr; Math.PI <br>
> **quarter** &rarr; Math.PI / 2

### Rectangle
`ctx.fillRect(x, y, w, h);` &rarr; draws a filled rectangle directly (no path needed)
(ctx.fillRect(50, 60, 120, 80))

`ctx.clearRect(x, y, w, h);` &rarr; erases a rectangular area of the canvas
(ctx.clearRect(0, 0, canvas.width, canvas.height))

> `x, y` &rarr; top-left corner of area <br>
> `w, h` &rarr; width and height of area

### Animate
```js
function animate(){
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    ...
    animationID = requestAnimationFrame(animate);
}
animate();
cancelAnimationFrame(animationID);
```

`requestAnimationFrame(callback);` &rarr; asks browser to run your function before next repaint
(animationID = requestAnimationFrame(animate))

`cancelAnimationFrame(id);` &rarr; stops a scheduled animation frame
(cancelAnimationFrame(animationID))

> `callback` &rarr; function to run each frame (example: animate)

### Image
```js
const img = new Image();
img.src = "./name.png";
img.onload = ()=>{
    ctx.drawImage(img, x, y, width, height)
}
```

### Text
```js
ctx.font = "24px Arial"
ctx.fillStyle = "white"
ctx.fillText("Timer!, x, y);
```