
# 반복문

## while

- break/continue

  - break 는 멈춘다.
  - continue 현재 실행되는 부분만 점핑해서 넘어간다.
  - 문 내부의 명령 순서에 따라 결과가 달라질 수 있다.

```javascript
// 초기 값
var k = 9;

// 조건 확인
// 조건 값이 참이면 {} 실행
while ( k > 0 ) {
  // break 또는 continue를 설정할 조건
  // 9, 7, 5, 3, 1
  // if ( k < 6 ) {
  //   break;
  // }
  // 값 변경
  // 조건이 거짓이 되는 순간이 와서
  // 논리 오류에 빠져 무한 반복되지 않는다.
  k = k - 2;
  if ( k === 5 ) {
    continue;
  }
  console.log('k:', k);
}
// 콘솔에 찍히는 값 : 7, 3, 1, -1
```

```javascript
var math = Math;
var count = 0;

while( isType(math, 'math') ) {
  console.log('count:', count);
  console.log('Math is 수학 객체');
  // 0, 1, 2, 3, 4
  if ( count++ >= 4 ) {
    // math = new Error(); // Error {} 생성
    break;
  }
  // count = count + 1;
  // count += 1;
  // count++;
  // ++count;
}
```


## do...while

> do 문장 while (조건문);


```javascript
var data_collection = [ null, {}, 9, '집합', false, [], function(){} ];
var n = data_collection.length;

// data_collection 아이템을 역방향 순환하되,
// 아이템 유형이 함수이면 반복을 중지한다.
// 단, 아이템 유형이 함수일지라도 1회는 아이템 유형 값을 반드시 출력하라.
do {
  console.log( type(data_collection[--n]) );
} while( !isType(data_collection[n], 'function') );
```

### while문: data.js 데이터 순환 필터링

```javascript
// classUsingArray
  // school을 다닌 적이 없는 사람을 제외한 사람들을 필터링하라.

var len = classUsingArray.length;      // 10
var classmate, filteredClassmate = []; // undefined

// while ( --len > -1 ) {
while ( len-- ) {
  classmate = classUsingArray[len];
  if ( !isType( classmate.school, 'null' ) ) {
    filteredClassmate.push(classmate);
  }
}

console.log('filteredClassmate:', filteredClassmate);
```


## for

> for(초기선언; 값비교검증; 값변화) { 검증 결과가 참일 때, 반복 수행 }

```javascript
for ( var k = 9; k > 0; --k ) {
  if ( k === 5 ) {
    continue;
  }
  console.log('k:', k);
}
```

### for문: data.js classUsingArray 순환처리 필터링

```javascript
// for문(정상적인 방법)
for ( var classmate, i=0, l=classUsingArray.length, filteredClassmate = []; i<l; ++i ) {
  classmate = classUsingArray[i];
  if ( !isType(classmate.school, 'null') ) {
    filteredClassmate.push(classmate);
  }
}
console.log('filteredClassmate:', filteredClassmate);

// for문(변칙적인 방법)
var len = classUsingArray.length,
    filteredClassmate = [],
    classmate;

for ( ; (classmate = classUsingArray[--len]); ) {
  if ( !isType( classmate.school, 'null' ) ) {
    filteredClassmate.push(classmate);
  }
}
console.log('filteredClassmate:', filteredClassmate);
```


## for...in

> for (variable in object) { statements }

- 객체는 배열과 달리 length 속성이 존재하지 않는다. 따라서 객체를 순환하려면 for...in 문을 사용한다.
- 배열 또한 for...in문을 사용할 수 있으나, 속도가 느려 for문을 사용하는 것이 좋다.

```javascript
// '속성' in 객체
console.log('"age" in han:', "age" in han);
console.log('"grooming" in han:', "grooming" in han);
```

### han 객체 순환 처리

- 객체의 속성을 순환하여 처리하기

```javascript
var han = classUsingObject.한진아;
// console.log('han:', han);

for ( var prop in han ) {
  // 객체 자신이 소유한 속성인지를 판단하여
  // 자신의 속성일 경우만 출력하라.
  if ( han.hasOwnProperty(prop) ) {
    // han 객체의 속성 prop을 순환하여 처리한다.
    console.log('han 객체의 속성:', prop);
    // han.age === han['age']
    // 순환 과정에서 속성 이름을 알 수 없기에,
    // 변수를 사용한 객체 속성 접근법을 사용해야 한다.
    // han[prop]
    console.log('han 객체의 값:', han[prop]);
  }
}
```

### classUsingObject 객체 순환 처리

```javascript
// console.log('type(classUsingObject):', type(classUsingObject));

for ( var member in classUsingObject ) {
  if ( classUsingObject.hasOwnProperty(member) ) {
    var value = classUsingObject[member];
    console.log('member:', member);
    // console.log('value:', value);
  }
}
```

### 객체 상속과 for...in

```javascript
// 객체(부모)
var parent = {
  name: '김훈남',
  age: 67,
  job: '농부',
  drive: function(mobil) {
    mobil = mobil || '경운기';
    return this.job + '인 ' + this.name + '씨가 ' + mobil + '을(를) 타고 드라이브 합니다.';
  }
};

// 객체(자식) <- 부모객체의 능력을 상속(Inheritance)
var child = Object.create(parent);
// 자식 객체에 속성을 추가 (부모 객체에는 없는 속성)
child.game_console = 'Sony Playstation 4';
child.friends = ['토니', '미키', '와사비'];
```

### 객체.hasOwnProperty()

```javascript
// hasOwnProperty()를 사용하지 않았을 경우

for ( var prop in child ) {
  console.log(prop);
}

// hasOwnProperty()를 사용한 경우

for ( var prop in child ) {
  if ( child.hasOwnProperty(prop) ) {
    console.log(prop);
  }
}
```