
# 클로저(Closure)

> 클로저는 독립적인 변수(지역적으로 사용되지만, 둘러싼 범위 안에서 정의된 변수)를 참조하는 함수들이다. 즉, 이 함수들은 그들이 생성된 환경을 '기억'한다.

- 클로저는 어떤 데이터(문법적 환경)와 그 데이터에 운용되는 함수를 연관시켜주기 때문에 유용하다. 이건 객체가 어떤 데이터(그 객체의 속성)와 하나 이상의 메소드를 연관시킨다는 점에서 객체지향 프로그래밍과 분명히 같은 맥락에 있다. 
- 결론적으로 오직 하나의 메소드를 가지고 있는 객체를 일반적으로 사용하는 모든 곳에 클로저를 사용할 수 있다.
- 이렇게 할 수 있는 상황은 특히 웹에서 일반적이다. 프론트 엔드 자바스크립트에서 우리가 쓰는 많은 코드가 이벤트 기반이다. 우리는 몇 가지 동작을 정의한 다음 사용자에 의한 이벤트 (클릭 혹은 키 누르기 같은)에 연결한다. 우리의 코드는 일반적으로 콜백으로 첨부된다. 이벤트에 응답하여 실행되는 단일 함수다.

## 클로저 예제

```javascript
// 전역 변수 count 를 선언해야 함수가 접근해서 값을 변경
// var count = 0;
  
// function increaseCount() {
//   // 어떻게 해야 count가 1씩 증가하게 될까?
//   // var count = 0;
//   return ++count;
// }

// increaseCount(); // 1
// increaseCount(); // 2
// increaseCount(); // 3
// increaseCount(); // 4

// 클로저 예제
// 외부 함수
var countDownMaker = function(n) {
  var count = n || 10;
  // 내부 함수
  // 함수 정의 없이 함수 값을 바로 반환할 수 있다.
  return function (step) {
    // 어떻게 해야 count가 1씩 증가하게 될까?
    // var count = 0;
    count -= (step || 1);
    return count;
  }
  // 내부 함수를 외부로 내보낸다.
  // return increaseCount;
};

var countUpMaker = function(n) {
  n = n || 10;
  return function(step) {
    n += (step || 1);
    return n;
  };
};

var countDown10  = countDownMaker(); // return function() {}
var countDown20  = countDownMaker(20); // countDownMaker(20)(4)
var countDown45  = countDownMaker(45);
var countDown100 = countDownMaker(100);

countDown10();  // 9
countDown10(4); // 5

var countUp10  = countUpMaker();
var countUp20  = countUpMaker(20);
var countUp45  = countUpMaker(45);
var countUp100 = countUpMaker(100);

countUp45();  // 46
countUp45(2); // 48
```

### JavaScript 클로저는 함수만 반환한다?

- JavaScript는 함수 뿐만 아니라, 모든 데이터 유형을 반환할 수 있다.
- 객체를 반환하는 래퍼 함수를 사용하여 클로저를 활용할 수 있다.
- JavaScript 클로저는 함수이다? -> 외부로 유출된 데이터가 함수 내부의 영역의 기억을 가지고 있다면..!

```javascript
// 카운트를 관리하는 객체
function makeCountManager(init_count) {
  // 관리할 카운트 값을 초기화
  var memoried_count = init_count = init_count || 0;
  return {
    // 카운트 증가 메서드
    increase: function(step) {
      init_count += (step || 1);
      return init_count;
    },
    // 카운트 감소 메서드
    decrease: function(step) {
      init_count -= (step || 1);
      return init_count;
    },
    // 카운트 초기화 메서드
    reset: function(value) {
      init_count = value || memoried_count;
    },
    // 현재 카운트 값을 반환하는 메서드
    getCount: function() {
      return init_count;
    }
  };
}
```
