# Light Camera, Material 을 이용한 바다 및 튜브 구조 구현

###조원 :  김동해, 이주협, 이호현, 임채하, 하보천

##소스파일
```
var cols, rows;
var scl = 50;
var w = 2000;
var h = 1500;

var flying = 0;

var terrain = [];

let img;

function setup() {
  createCanvas(700, 700, WEBGL);
  cols = w / scl;
  rows = h / scl;
  textSize(30);
  text('word',10,30);

  for (var x = 0; x < cols; x++) {
    terrain[x] = [];
    for (var y = 0; y < rows; y++) {
      terrain[x][y] = 0; //specify a default value for now
    }
  }
  
  img = loadImage('ImageA');
  
  camera = createCamera();
}

function draw() {

  flying -= 0.03;
  var yoff = flying;
  for (var y = 0; y < rows; y++) {
    var xoff = 0;
    for (var x = 0; x < cols; x++) {
      terrain[x][y] = map(noise(xoff, yoff), 0, 1, -100, 100);
      xoff += 0.2;
    }
    yoff += 0.2;
  }

  //background(1000)
  background(100,100,200);
  
  push();
  translate(0, 50);
  rotateX(PI / 2.2);
  fill(10, 20, 150, 230);
  noStroke();
  translate(-w / 2, -h / 2);
  for (var y = 0; y < rows - 1; y++) {
    beginShape(TRIANGLE_STRIP);
    for (var x = 0; x < cols; x++) {
      vertex(x * scl, y * scl, terrain[x][y]);
      vertex(x * scl, (y + 1) * scl, terrain[x][y + 1]);
    }
    endShape();
  }
  pop();
  
  push();
  var xLocation = noise(millis()/ 1000 + 15);
  xLocation = map(xLocation, 0,1,-1000,1000);
  var yLocation = noise(millis()/ 1000 + 30);
  yLocation = map(yLocation, 0,1, -100,300);
  var zLocation = noise(millis()/1000 + 45);
  zLocation = map(zLocation, 0, 1, 300,-2000);
  translate(xLocation,yLocation-150,zLocation+300);
  rotateX(4.8);
  texture(img);
  box(100);
  pop();
  
  push();
  translate(mouseX-350, mouseY-350, 300-mouseY);
  camera.lookAt(20, 20, 0);
  camera.setPosition(sin(frameCount / 60) * 200, 0, 500);
  rotateX(4.3);
  
  normalMaterial();
  ambientMaterial(150,30,30);
  ambientLight(255);
  torus(80, 20, 64, 64);
  pop();
  
}
  
function touchStarted() {
  img = loadImage('ImageB');
}
function touchEnded() {
  img = loadImage('ImageA');
}
```

##설명

##소감
김동해
이주협
이호현
임채하
하보천
