
# 변수와 상수

## 변수 (Variable)

### 1. 정의
> 물건을 보관했다가 필요할 때 다시 꺼내 사용하는 일종의 창고

> 데이터를 저장하고 읽고 쓸 수 있는 장소

> 어플리케이션에서 값에 상징적인 이름으로 변수를 사용한다. 변수명은 식별자(identifier)라고 불리며 특정 규칙을 따른다.

### 2. 변수 선언

#### 1) 초기 값은 할당되지 않는다.

```javascript
var lunch;
// undefined
```

#### 2) 선언된 변수에 값을 할당

> var 변수_이름 = 값;

- '=' : 할당(대입) 연산자 (할당하는 역할을 수행하는 연산자)

```javascript
lunch = 김밥;
// 김밥 이라는 이름의 변수를 찾는다.
// 선언된 변수가 없으면 참조 오류(Reference Error) 발생
// Uncaught ReferenceError: 김밥 is not defined

lunch = "김밥";
lunch = '김밥';
// 김밥 이라는 문자열 데이터를 찾는다.

lunch = kimbab;
lunch = 'kimbab';
// 아래 영문의 경우도 마찬가지

var 변수_이름 = 값;
var 변수_이름 = 다른_변수_이름;
// 변수를 선언함과 동시에 값을 할당하는 구문
// 다른 변수에 할당된 값을 선언하는 변수에도 할당

var dinner = '치맥'; 
// 점심에 먹은 것을 저녁에도 먹고 싶지 않을 때
var dinner = lunch;
// 점심에 먹은 것을 저녁에도 먹고 싶을 때
```

#### 3) 변수 이름 작성 규칙
- 이름은 알아보기 쉽게, 이해하기 쉽게 명시적으로 지어야 한다.
- 이름은 직관적으로 그것이 무엇을 말하며, 무엇을 행할 수 있는지 알게 지어야 한다.

#### \* 이름 작성 시 주의할 점

\- 공백으로 이름이 구분되게 지어서는 안된다.
```javascript
var my name = 'soyeon1128'; [X]
```

\- 이름을 지을 때 첫 글자가 숫자여서는 안된다.
```javascript
var 101Team = 'IoI'; [X]
var 10px = 'Tem Pixel'; [X]
```

\- 이름 지을 때 사용할 수 있는 특수문자는 정해져 있다.
```javascript
// '_', '$' 을 제외한 다른 특수문자는 사용할 수 없다.
var Team-101 = 'IoI'; [X]
var @design-people = '디자인 피플'; [X]
```

\- 대소문자를 구분하는 JavaScript에서는 이름을 지을 때 관례가 있다.
어긴다고 해서 문법에 오류가 발생하지는 않지만, 오래 전부터 내려오는 관습이 있다.

\- 변수 이름은 _을 사용하여 이름을 구분한다.
* 패턴(Pattern): 사용 빈도가 높음
* Single var pattern : var 변수 선언 키워드를 한 번만 사용하여 변수를 정의하는 패턴
```javascript
var my_name, is_visible, has_children, remote_control;
```

\- 함수 이름은 카멜 케이스(camelCase) 표기법을 사용한다.
```javascript
getName(), setAge(), showMeTheMoney(), blackSheepWall()
```

\- 함수 이름의 첫글자가 대문자인 경우는 특별한 함수일 가능성이 높다.
```javascript
Navigation(), Tabs(), Carousel(), Component(), Vue(), ...
```

### 3. 변수 범위 (Scope)
- 어떤 함수의 바깥에 변수를 선언하면, 현재 문서의 다른 코드에 해당 변수를 사용할 수 있기에 전역 변수라고 합니다. 만약 함수 내부에 변수를 선언하면, 오직 그 함수 내에서만 사용할 수 있기에 지역 변수라고 부릅니다.


#### 1) 전역 변수(Global Variable)
> 모든 구역(Block)에서 접근(Access)이 가능한 변수, 전역 객체의 속성
- 클라이언트 환경(Front-End)
- 전역 객체(Global Object): Window 객체

```javascript
var type_of_my_phone = 'iPhone';
console.log('전역 변수:', type_of_my_phone); 'iphone'
```

#### 2) 지역 변수(Local Variable)
> 특정한 구역(Block)에서만 접근이 가능한 변수

```javascript
//Block 문
{
  var type_of_my_phone = 'Apple Device';
  console.log('블록 내부 변수:', type_of_my_phone); 'Apple Device'
}

console.log('전역 변수는 블록 내부의 변수에 영향을 받았나?:', type_of_my_phone); 'Apple Device' ?
```

### 4. 호이스팅 (Hoisting)
- 변수가 끌어올려 진다.

```javascript
var somthing; undefined

console.log('is exist variable `somthing`?:', somthing);

var somthing = '썸씽';
```

## 상수(Constant)
- 상수는 변수와 유사하나, 읽기 전용(Read Only)이다.
- 한 번 선언된 상수는 재 선언될 수 없다. 뿐만 아니라 다른 값을 할당하는 것도 불가능하다.
- 관례적으로 대문자로만 구성된 이름을 사용하여 변수와 구분 짓는다. (강제성 없음)

```javascript
const IS_ROTATION_EARTH = true; // 대문자로 구성된 상수
const is_rotation_earth = true; // 소문자로 구성된 상수

console.log('IS_ROTATION_EARTH:', IS_ROTATION_EARTH);
console.log('is_rotation_earth:', is_rotation_earth);
```
