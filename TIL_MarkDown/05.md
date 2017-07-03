
# 리터럴

## 배열 리터럴

- 배열 객체 <- 생성자를 통해 객체를 생성
- 생성자란? (일반적으로 JavaScript 에서 앞 글자가 대문자인 함수)
    - Number(), String(), Boolean(), Function(), Array(), Object()
- 객체 생성을 위한 문법
    - var 생성된_객체를_참조할_변수 = new 생성자()
    - `생성된_객체를_참조할_변수` 에는 `생성된 객체`가 참조됨.
    - 추상적인 (설계) -> 실존하는 실체(객체)
    - 와플빵 틀(붕어빵 틀) -> 와플빵(붕어빵)
    - Carousel        -> Carousel {}

```javascript
// JavaScript 에서 객체를 생성하는 정식 구문

// 숫자 생성자 함수를 통해 숫자 객체를 생성하는 방법
var minimum = new Number(10);
// Number {}
// console.log(minimum);
minimum = 10; // 숫자 리터럴 (마치 숫자 객체인 것처럼 처리)

// 문자 생성자 함수를 통해 문자 객체를 생성하는 방법
var school_msg = new String('오늘 인터넷은 잘 터지나?');
// String {}
console.log('school_msg.valueOf():', school_msg.valueOf());
// school_msg.valueOf(): 오늘 인터넷은 잘 터지나?

// 불리언 생성자 함수를 통해 불리언 객체를 생성하는 방법
var is_hungry = new Boolean(true); // Boolean {}
console.log('is_hungry.valueOf():', is_hungry.valueOf());
// is_hungry.valueOf(): true

// 함수 생성자 함수를 통해 함수 객체를 생성하는 방법
var eatRunch = new Function('console.log("와구 와구 먹는다.")');
// Function {}
// function(){}

// 배열 생성자 함수를 통해 배열 객체를 생성하는 방법
var favorite_collection = new Array('국자', '밥숟가락');
// Array {}
// ['국자', '밥숟가락'] 배열 리터럴

// 객체 생성자 함수를 통해 객체 객체를 생성하는 방법
var audi = new Object();
// Object {}
// {}
```

- 변수는 하나의 데이터만 담을 수 있다.
- 그렇기 때문에 다른 데이터가 담기면 이전 데이터는 메모리에서 소멸된다.
- 자바스크립트 메모리 관리는 '가비지 콜렉터'가 한다.

### 배열을 활용하는 예시
- 데이터 중, 배열은 다수의 데이터를 담을 수 있다.
- 변수 하나에 다수의 데이터를 담을 수 있는 배열을 담으면 데이터 관리에 용이하다.
```javascript
// convert_num_to_str_case1 === String(909)
// convert_num_to_str_case2 === 808 + ''
// convert_num_to_str_case3 === (707).toString()

// var convert_string_from_number = new Array();
var convert_string_from_number = [];

convert_string_from_number[0] = String(909);
convert_string_from_number[1] = 808 + '';
convert_string_from_number[2] = (707).toString();

console.log('convert_string_from_number.length:', convert_string_from_number.length);
// convert_string_from_number.length: 3

// 위와 같은 방법 (인덱스 숫자를 사용하는) 말고, 아래와 같이 배열 객체의 메서드(능력)를 사용하길!
console.group('Array 객체의 push() 메서드 사용');
convert_string_from_number.push('1001');
console.log("convert_string_from_number.push('1001');");
// convert_string_from_number.push('1001');
convert_string_from_number.push('9003');
console.log("convert_string_from_number.push('9003');");
// convert_string_from_number.push('9003');
console.groupEnd('Array 객체의 push() 메서드 사용');

console.log('convert_string_from_number.length:', convert_string_from_number.length);
// convert_string_from_number.length: 5
```


### 연관형 배열과 length
- 배열 객체
- 연관형 배열 표기법
- Array['key'] = value;
```javascript
console.groupCollapsed('연관형 배열과 length');

// 배열 리터럴을 사용하여 변수 music_list에 배열 객체를 참조
var music_list = [];

// 인덱스를 사용하여 원소을 추가(Add Item)
music_list[0] = '데칼코마니';
music_list[1] = '러시안 룰렛';
music_list[2] = '나야 나';

console.log('music_list.length:', music_list.length); // 3

// 문자 key 값을 사용하여 새로운 원소를 추가
music_list['author']   = 'yamoo9';
music_list['maker']    = 'YG';
music_list['location'] = 'Seoul';

console.log("music_list['author']   = 'yamoo9'");
console.log("music_list['maker']    = 'YG'");
console.log("music_list['location'] = 'Seoul'");

console.log('music_list.length:', music_list.length); // 6[X], 3[O]

console.dir(music_list);
```

## 객체 리터럴
### 함수 객체 (Function Object)
: 함수 선언문과 함수 표현식. 호이스팅(Hoisting)

- 함수 호이스트 현상
    함수 선언문은 영역의 최상위로 몸체가 모두 이동한다.
    함수 표현식은 `var 함수이름;` 만 영역의 최상위로 이동한다.

```javascript
// 아래 함수를 실행했을 때,
// 호이스트 현상이 발생하여 doIt()의 경우는 실행되나,
// sendMail() 함수의 경우는 오류가 발생한다.

// doIt();
// sendMail();

// 0. 함수 생성자를 통해 함수 객체를 생성
// 아래와 같은 방법은 사용하지 않는 것이 좋다.
var myFn = new Function('console.log("create function object from function constructor.")');

// 1. 함수 선언문: 함수 이름 선언
// function doIt(){} 몸체가 모두 영역 최상위로 끌어올려진다.
function doIt(){
  console.log('do it!');
}

// 2. 함수 표현식: 변수에 함수 표현식(함수 리터럴)을 할당
// var sendMail; 구문만 영역 최상위로 끌어올려진다.
var sendMail = function() {
  console.log('Send Mail to you');
};
```

### 기본 객체 (Plain Object)
`속성(key): 값(value)` 쌍(Pair)으로 구성된 집합체(데이터 덩어리)
```javascript
var init_style_of_body = {
  // 속성(key): 값(value)
  'margin'      : 0,
  'font-size'   : '14px',
  lineHeight    : 1.5,
  letterSpacing : 0.04 + 'em',
  color         : '#313233'
};

// 변수
var legs = 4;

// 객체의 속성(객체가 소유한 변수)
var animal = {};

// animal 객체의 legs 속성에 숫자 값 4를 복사
animal.legs = 4;

// legs 변수에 복사된 숫자 값 4를 animal 객체의 legs 속성에 복사
animal.legs = legs;
```

### 객체 속성 제거
```javascript
// delete 객체.속성; // true
delete loreo.wheels; // true

// 전역객체인 window 객체의 속성은 제거할 수 없다.
// 전역을 오염시키는 행위는 안티 패턴이다.
// 전역에 변수를 선언하는 행위를 최소화한다.
```

### 객체의 리터럴 속성을 출력하는 방법
: 값 복사 / 참조
```javascript
var circle = 8;
var brand_makers = ['KIA', 'Hyundai', 'Samsung', 'Google'];
var getMaker = function(brand_index) {
  return brand_makers[brand_index];
};

var loreo = {
  engine: 'V8',
  wheels: circle,
  showMaker: getMaker
};
```

