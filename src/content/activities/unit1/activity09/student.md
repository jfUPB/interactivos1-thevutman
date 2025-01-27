``` js
let x, y;
let xSpeed, ySpeed;
let radius = 20;
let angle = 0;
let amplitude = 50;

function setup() {
  createCanvas(400, 400);
  x = random(radius, width - radius);
  y = random(radius, height - radius);
  xSpeed = random(2, 5);
  ySpeed = random(2, 5);
}

function draw() {
  background(30);
  fill(200, 100, 255); 
  noStroke();
  
  let wave = sin(angle) * amplitude;

  let size = radius + cos(angle) * 10;

  ellipse(x, y + wave, size * 2);

  x += xSpeed;
  y += ySpeed;

  angle += 0.1;

  if (x - size <= 0 || x + size >= width) {
    xSpeed *= -1;
  }
  if (y - size <= 0 || y + size >= height) {
    ySpeed *= -1;
  }
}
```
!image(../../../assets/actividad9.png)