```javascript
// 생성자 함수 Dog
function Dog() {};

// 생성자 함수 Dog로 poodle과 beagle라는 객체를 만듬
var poodle = new Dog();
var beagle = new Dog();

// Dog 생성자 함수의 프로토타입에 jump라는 속성을 부여
// 공통 속성
Dog.prototype.jump = true;

poodle.jump = true;
beagle.jump = true;

// 생성자 함수 Dog의 this에 poodle과 beagle이라는 인스턴스가 들어옴
// 개별 속성
function Dog (i, j) {
    this.name = i;
    this.age = j;
}

var poodle = new Dog("nana", 3);
poodle.name = "nana";
poodle.age = 3;

var beagle = new Dog("dodo", 8);
beagle.name = "dodo";
beagle.age = 8;
```
