# 메서드 빌려쓰기 - call, apply, bind

> 함수.call(객체, 전달인자)

- call/apply는 매개변수를 함수 내부에서 사용할 this로 만들어 준다.
- arguments를 call은 콤마로 구분하고 apply는 배열로 받는다.
- 즉, call와 apply의 차이는 두번째 인자를 배열로 받느냐 콤마로 받느냐의 차이

. call과 apply는 실행할 함수에 객체와 arguments를 던져서 실행한다. 함수내에서는 this의 선언으로 전달받은 객체의 값을 할당할 수 있다. 다시 한번 말한다. 호출방식은 이다.

```javascript
  var a = {
    x: 1
  };

  var b = function() {
    console.log(this.x);
  };
  
  b.call(a);
  // 결과: 1
```

```javascript

  function Orange() {  
      return this;
  }
  var delmonte = Orange.call(this);

  console.log(delmonte);
  // 콘솔창 결과 : Window 객체

  // -------------------------------------------

  function Banana(){
      this.taste = 'sweet';
  }

  function Apple(){
    this.shape = 'round';
    Banana.call(this);
  }

  var daegu_apple = new Apple;
  
  console.log(daegu_apple);
  // 콘솔창 결과 : Apple {shape: "round", taste: "sweet"}

 ```

# JavaScript 메서드 빌려쓰기 패턴

```javascript
// 새(객체)를 태어나게 하는 생성자 함수
function Bird() {}
// 새(객체)의 날다 라는 능력 -> 생성자함수.prototype
// 새.날다()
Bird.prototype.fly = function() {};
// 생성자 Bird 함수를 통해 새(객체)를 생체
// var my_bird = new Bird(); // Bird {}

// my_bird.fly();
// my_bird.readBook(); [X]

// 사람.걷다()
function Human(){}
Human.prototype.walk = function() {};
// var me = new Human();

// me.walk();
// me.fly(); // [X]

// Function.prototype.call
// 새.날다.call(사람)

// Bird.prototype.fly.call(me); // me.fly()
```


## call 과 apply
 > ### 함수가 this본문 에서 키워드를 사용하는 경우 모든 함수가 상속 하는 call또는을 사용하여 해당 값을 호출의 특정 개체에 바인딩 할 수 있습니다 .applyFunction.prototype

 ## The bind method
 > ### ECMAScript 5가 도입 Function.prototype.bind되었습니다. 호출 f.bind(someObject)은 본문과 범위가 같은 새 함수를 만듭니다. 그러나 원래 this 함수 에서 발생하는 경우 새 함수 bind에서 함수의 사용 방법에 관계없이 첫 번째 인수에 영구적으로 바인딩 됩니다.

```javascript
  function f() {
    return this.a;
  }

  var g = f.bind({a: 'azerty'});
  console.log(g()); // azerty
  // this.a = azerty

  var h = g.bind({a: 'yoo'}); // bind only works once!
  // hard binding 이라서 attach는 한번만 가능하다.
  console.log(h()); // azerty

  var o = {a: 37, f: f, g: g, h: h};
  console.log(o.f(), o.g(), o.h()); 
```
 +  a:37, f:function f() {
    return this.a;
  }, g: f.bind({a: 'azerty'}), h: g.bind({a: 'yoo'})
+ 순서로 해석 되어지므로  o.f() -> 37, o.g() -> azerty, o.h() -> azerty
