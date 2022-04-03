# Light Camera, Material 을 이용한 바다 및 튜브 구조 구현

### 조원 :  김동해, 20191129 이주협, 20191131 이호현, 20191137 하보천, 20211110 임채하 

## 소스파일
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

## 설명

## 최종 결과
<video width="

https://user-images.githubusercontent.com/50916731/161411325-a7874df7-1e4b-4522-bb3f-a5e827140a3c.mp4

100%" height="100%" controls="controls">
  <source src="/Processing/source/LightMaterialCamera.mp4" type="video/mp4">
</video>

## 소감
김동해 : 이 과제를 어떻게 시작하여 해결해야 할지 너무 막막했습니다. 하지만 훌륭하신 팀원 분들께서 어떻게 해결해야 할지 솔루션을 제공해주셨고, 질문에 친절히 대답해주셨습니다. 팀원분들의 아이디어를 보고 저렇게 생각할 수 있구나 매우 감탄하였습니다. 지금 만들어진 작품은 훌륭하신 팀장님과 팀원분들의 지혜와 열정, 협력이 아니었다면, 절대 만들어질 수 없었을 것입니다. 앞으로도 열심히 하여 성장하는 제 자신을 발견하고 싶습니다. 존경하는 심재창교수님, 그리고 컴퓨터그래픽스 파이팅! 

이주협 : 수업만으로는 100% 이해했다고 보긴 어려웠지만 팀원들과 서로 모르는 부분은 설명받고 해주다보나 자연스럽게 학습도 되고 동기들 얼굴도 보고 좋은 기회였습니다. 다양한 프로그래밍 언어가 있고 코드를 한줄한줄 이해할 때 마다 쾌감을 느끼며 한차례 성장한 기분을 받을 수 있었고 즐거웠습니다 사랑합니다 교수님

이호현 : 코로나 시기에 수업을 들으면서 다른 학생들과 소통할 기회가 없었는데 이번 팀프로젝트를 통해서 팀원분들과 얘기를 나누어 보고  또 코드를 어떻게 창의적으로 바꿀 수 있을지 다같이 생각해보면서 제가 부족했던 부분을 많이 깨우치게 되었고 더욱 노력해야겠다는 열정이 생겼습니다! 프로젝트를 하는동안 좋은 팀원분들덕에 즐겁게 할 수 있었습니다. 항상 재밌게 수업을 가르쳐주시는 심재창 교수님께 감사합니다!

하보천 : 대부분의 수업이 비대면 수업인만큼 팀프로젝트는 가뭄에 단비같은 기회였습니다. 팀원들과 모여 가지각색의 아이디어를 공유했습니다. 좋은 아이디어가 너무 많아 모두 구현하지 못한게 아쉬울 따름이었습니다. 이를 통해 깨달은 점이 있습니다. 아이디어를 생각해내는 생각하는 힘, 그리고 그걸 실현해내는 구현력의 중요성이 그것입니다. 아무리 좋은 아이디어가 있어도 구현하지 못한다면, 아무리 구현력이 좋아도 실현할 아이디어가 없다면 아무일도 벌어지지 않을 것입니다. 앞으로 더욱더 학업에 매진하여 이 두 요소를 잘 키우겠습니다. 이런 좋은 기회를 제공해주신 교수님 항상 감사드리고 존경합니다!

임채하 : 3차원 지형에 Camera, Light, Material을 포함하여 어떻게 변형하여야 보는 사람도 즐거운 코드가 될 수 있을지에 대해 팀원들과 함께 고민하는 시간과 명령어를 보다 잘 활용하기 위해 레퍼런스를 보고 코드를 변형해보는 시간, 유튜브 영상 매체를 통해 학습하고 다른 사람의 코드를 검색해보는 시간 하나하나가 모두 값지고 즐거웠습니다. 타학과이기도하고 처음보는 학우들과의 과제가 염려되기도 했지만 친절하게 다가와주고 도와주어서 즐겁게 토론하고 문제를 해결해 나갈 수 있었습니다. 더해서 컴퓨터 그래픽스 과목에 대한 공부가 더 필요함 또한 느낄 수 있었습니다. 일주일 정도 밖에 안되는 시간이었지만 많은 것을 보고 느끼고 배울 수 있었고 즐거운 시간을 갖게해주신 심재창교수님과 팀원분들 감사합니다!
