## 데이터 유형 (Data Types)

### 1. 분류 (ES5 기준)

#### 원시 데이터 유형(Primitive Data Types)
- undefined: false (변수 값이 할당되지 않음)
- null: false (변수 값이 없음)
- Number : (정수, 실수, 소수) / 0: false
- String : 홑따옴표, 쌍따옴표로 묶인 텍스트 / "": false / " ": true
- Boolean : (true, false) / !!false: false

#### 참조 데이터 유형(Reference Data Types)
- Object
	- Function : 수행을 위한 절차
	- Array : 값의 집합
	- Object : 속성의 집합


### 2. 문자(String) 유형의 데이터
> 따옴표(큰,작은)로 묶인 텍스트

#### * 사용시 유의점
- 따옴표의 시작과 끝이 같은 유형이어야 한다.
- 문자 데이터 유형을 구분짓기 위한 따옴표가 아닌,문자로서의 따옴표의 경우는 이스케이스(Escape) 처리해야 한다.

```javascript
//다음과 같은 HTML 코드를 문자 데이터 유형으로 처리하려면?
<p class="message" title="달리기 기록">나의 하프 마라톤 기록은 50" 23'이다.</p>

//큰 따옴표 사용 시
var message_html = "<p class=\"message\" title=\"달리기 기록\">나의 하프 마라톤 기록은 50\" 23'이다.</p>";

//작은 따옴표 사용 시
var message_html = '<p class="message" title="달리기 기록">나의 하프 마라톤 기록은 50" 23\'이다.</p>';
```

### 3. 데이터 형 변환(자동)

- JavaScript는 동적 데이터 유형 처리 언어이기 때문에 변수를 사용하여 런타임(실시간, 웹 브라우저에서 실행 중인 상황) 중에 값의 유형을 변경할 수 있다.

```javascript
// 변수 선언 시에 문자 유형의 데이터 값을 변수에 할당했지만,
var process_my_work = '논리에 기반한 선별적 디자인 프로세스';

// 웹 브라우저에서 실행 중인 상황에 사용자의 코드에 따라 값의 유형이 바뀔 수 있다. (너무나 쉽게)
process_my_work = false;          // 문자 -> 불리언 으로 변경
process_my_work = function() {};  // 불리언 -> 함수 로 변경
```

#### * 동적 할당 언어인 JavaScript에서 유의할 점

```javascript
var a, b, c;

a = 10;
b = 7;
c = a + b; 17

a = 10;
b = '칠'; // 사용자가 잘못된 유형을 입력한 경우
c = a + b; '10칠' // 의도치 않는 결과를 가져온다.

Single var pattern
var x, y, z;

x = 'X';
y = 'Y';
z = 'Z';

var x = 'X',
    y = 'Y',
    z = 'Z';
```

## 미리 살펴보는 DOM Script

```javascript
//DOM Script 에서 Single var pattern을 사용한 예시
var html = window.document.documentElement,
    head = window.document.head,
    body = window.document.body;

console.log('html:', html);
console.log('head:', head);
console.log('body:', body);
```


### [참조링크 - Mozilla Developer Network](https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide)

# 데이터 구조 및 형

## 데이터 유형
### 원시 유형의 데이터
```javascript
// Number
var num = 291029304;
// String
var str = 'morning food';
// Boolean
var boo = false;
// null
const NULL = null;
// undefined
const UNDEFINED = undefined;
```
### 참조 유형의 데이터
```javascript
// Object
var glass = {}; // new Object()
// Function
var watchGlass = function(){}; // new Function()
// Array
var glasses = []; // new Array()
```

## 데이터 형 변환
### 1. 숫자 데이터 > 문자 데이터
```javascript
console.log('num:', num);
// num: 291029304

// String(숫자데이터)    => "문자데이터"
var convert_num_to_str_case1 = String(num);
console.log('String(num):', convert_num_to_str_case1);
// String(num): 291029304
console.log('타입:: String(num):', typeof convert_num_to_str_case1);
// 타입:: String(num): string

// 숫자데이터 + ''       => "문자데이터"
var convert_num_to_str_case2 = num + '';
console.log('num + \'\':', convert_num_to_str_case2);
// num + '': 291029304
console.log('타입:: num + \'\':', typeof convert_num_to_str_case2);
// 타입:: num + '': string

// 숫자데이터.toString() => "문자데이터"
var convert_num_to_str_case3 = num.toString();
console.log('num.toString():', convert_num_to_str_case3);
// num.toString(): 291029304
console.log('타입:: num.toString():', typeof convert_num_to_str_case3);
// 타입:: num.toString(): string
```

### 2. 문자 데이터(숫자만 포함된 문자) > 숫자 데이터
```javascript
// 1. Number(문자데이터(숫자형)) 함수  e.g) "23412"
console.groupCollapsed('문자 데이터(숫자만 포함한 문자) ➡︎ 숫자 데이터로 변경되는 사례');
console.log('Number(convert_num_to_str_case3):', Number(convert_num_to_str_case3));
// Number(convert_num_to_str_case3): 291029304
console.log('typeof Number(convert_num_to_str_case3):', typeof Number(convert_num_to_str_case3));
// typeof Number(convert_num_to_str_case3): number

// 2. -, *, / => '12343124' - 0 = 12343124
console.log('convert_num_to_str_case3 - 0:', convert_num_to_str_case3 - 0);
// convert_num_to_str_case3 - 0: 291029304
console.log('convert_num_to_str_case3 * 1:', convert_num_to_str_case3 * 1);
// convert_num_to_str_case3 * 1: 291029304
console.log('convert_num_to_str_case3 / 1:', convert_num_to_str_case3 / 1);
// convert_num_to_str_case3 / 1: 291029304

// 3. +문자데이터(숫자형) => 숫자데이터  e.g) +"23412"
console.log('+convert_num_to_str_case3:', +convert_num_to_str_case3);
// +convert_num_to_str_case3: 291029304
```

### 3. 문자 데이터(숫자 + 문자를 포함하는 문자) > 숫자 데이터
```javascript
var news_font_size = '16.6345px';
// JavaScript 내장 함수 parseInt(), parseFloat()

// window.parseInt(단위를포함하는문자, 진수)   <= 단위를 제거하고 정수 값 반환
var convert_news_font_size_to_int = window.parseInt(news_font_size, 10);
console.log('convert_news_font_size_to_int:', convert_news_font_size_to_int);
// convert_news_font_size_to_int: 16

// window.parseFloat(단위를포함하는문자, 진수) <= 단위를 제거하고 실수 값 반환
var convert_news_font_size_to_float = window.parseFloat(news_font_size, 10);
console.log('convert_news_font_size_to_float:', convert_news_font_size_to_float);
// convert_news_font_size_to_float: 16.6345
```

### 4. 데이터 > 불리언 데이터
```javascript

// 1. Boolean(데이터) 함수 => 불리언 데이터로 변경
console.log('Boolean(num):', Boolean(num));
// Boolean(num): true
console.log('Boolean(0):', Boolean(0));
// Boolean(0): false
console.log('Boolean(str):', Boolean(str));
// Boolean(str): true
console.log('Boolean(""):', Boolean(""));
// Boolean(""): false
console.log('Boolean(" "):', Boolean(" "));
// Boolean(" "): true
console.log('Boolean(glass):', Boolean(glass)); 
// Boolean(glass): true
console.log('Boolean(glasses):', Boolean(glasses)); 
// Boolean(glasses): true
console.log('Boolean(watchGlass):', Boolean(watchGlass)); 
// Boolean(watchGlass): true

// 2. !! (부정의 부정 === 긍정) => 불리언 데이터로 변경
console.log('!!num:', !!num);
// !!num: true
console.log('!!0:', !!0);
// !!0: false
console.log('!!str:', !!str);
// !!str: true
console.log('!!"":', !!"");
// !!"": false
console.log('!!" ":', !!" ");
// " ": true
console.log('!!glass:', !!glass);
// !!glass: true
console.log('!!glasses:', !!glasses);
// !!glasses: ture
console.log('!!watchGlass:', !!watchGlass);
// !!watchGlass: true
```

### 5. null, undefined 형 변환
```javascript
// !!
console.log('!!null:', !!null);
// !!null: false
console.log('!!undefined:', !!undefined); 
// !!undefined: false

// !
console.log('!null:', !null);
// !null: true
console.log('!undefined:', !undefined);
// !undefined: true

// + ''
console.log('null + \'\':', null + '');
// null + '': null
console.log('typeof (null + \'\'):', typeof (null + ''));
// typeof (null + ''): string
console.log('undefined + \'\':', undefined + '');
// undefined + '': undefined
console.log('typeof (undefined + \'\'):', typeof (undefined + ''));
// typeof (undefined + ''): string

// String()
console.log('String(null):', String(null));
// String(null): null
console.log('typeof String(null):', typeof String(null));
// typeof String(null): string
console.log('String(undefined):', String(undefined));
// String(undefined): undefined
console.log('typeof String(undefined):', typeof String(undefined));
// typeof String(undefined): string

// null + 숫자
console.log('null + 10:', null + 10);
// null + 10: 10
console.log('undefined + 10:', undefined + 10);
//undefined + 10: NaN

// Number()
console.log('Number(null):', Number(null));
// Number(null): 0
console.log('Number(undefined):', Number(undefined));
// Number(undefined): NaN
```


## 값 복사와 참조

### 값 복사(pass by value)

- 값 복사(pass by value)가 이루어지는 데이터 유형

    - 원시 데이터 유형
    : number, string, boolean, null, undefined

```javascript
// 변수 n1을 선언한 후, 값으로 숫자 리터럴(값) 99를 할당한다.
// 변수 n1을 선언한 후, 숫자 값 99를 변수 n1에 복사한다.
var n1 = 99;
// 변수 k2를 선언한 후, n1 변수에 복사된 숫자 값 99를 복사한다.
var k2 = n1;
console.log('n1:', n1); // 99
console.log('k2:', k2); // 99

console.log('n1 값을 수정한 후 ------------------------');

// 가설: n1, k2에 복사된 숫자 데이터는 같은 값으로 보이나, 서로 다른 값이다.
// 증명: n1의 데이터 값을 변경했을 때, k2는 변화가 없어야 한다.
n1 = n1 * n1;
console.log('n1:', n1); // 9801
console.log('k2:', k2); // 99
```

### 값 참조(pass by reference)

- 값 참조(pass by reference)가 이루어지는 데이터 유형

    - 참조형 데이터 유형
    : 함수, 배열, 객체

```javascript
var playlist = music_list;
console.log('music_list:', music_list);
console.log('playlist:', playlist);

console.log('playlist를 변경하면? music_list는 어떻게 될까?');

// 가설: music_list, playlist에 참조된 데이터는 같은 값이다.
// 증명: music_list 또는 playlist의 데이터 값을 변경했을 때, 값을 동시에 변경된다. (동일한 값이기에)

playlist.push('루키'); // length: 4
music_list.author = 'mike';

console.log('music_list:', music_list);
console.log('playlist:', playlist);
```
