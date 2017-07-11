# DOM Script 중급

## 생성 (Creation) & 조작 (Manipulation)

- 노드 생성 (creation)
	- createElement
	- createAttribute
	- createTextNode
    - setAttribute

- 노드 조작 (manipulation)
    - appendChild

### DOM 생성 및 조작 유틸리티 함수들 (Library/FDS.js 네임 스페이스)

- createElement()
- createText()
- appendChild()
- createEl()

```javascript
// DOM 생성 및 조작 API: 유틸리티 함수 (Library/FDS.js 파일)
  
  var createElement = function(name){
    validateError(name, '!string', '요소의 이름을 문자열로 전달해주세요.');
    return document.createElement(name);
  };
  var createText = function(content){
    validateError(content, '!string', '콘텐츠는 문자열이어야 합니다.');
    return document.createTextNode(content);
  };
  var appendChild = function(parent, child) {
    validateElementNode(parent);
    parent.appendChild(child);
    return child;
  };
  var createEl = function(name, content) {
    validateError(name, '!string', '첫번째 인자로 요소의 이름을 설정해주세요.');
    var el = createElement(name);
    if ( content && isType(content, 'string') ) {
      var text = createText(content);
      appendChild(el, text);
    }
    return el;
  };
```

### - 생성 메서드 및 유틸리티 함수 실습

```javascript
  // 동적으로 요소노드를 생성
  // var list = document.createElement('ul');
  // var list_item = document.createElement('li');
  // var headline = document.createElement('h2');
  // var list_link = document.createElement('a');
  // var list_img = document.createElement('img');

  var list      = _.createEl('ul');
  var list_item = _.createEl('li');
  var headline  = _.createEl('h2', '새로운 것은 존재하지 않는다. 아직 내가 못 본 것일 뿐.');
  var list_link = _.createEl('a');
  var list_img  = _.createEl('img');

  // 동적으로 속성노드를 생성 (거의 사용되지 않음)
  // 생성된 <a> 요소에 href 속성을 설정(생성해서)
  var list_link_href = document.createAttribute('href');
  // 생성된 <img> 요소에 src, alt 속성을 설정(생성해서)
  var list_img_src = document.createAttribute('src');
  var list_img_alt = document.createAttribute('alt');

  // 동적으로 생성된 속성노드의 노드 값을 설정
  list_link_href.nodeValue = 'https://github.com/yamoo9';
  list_img_src.nodeValue = 'https://unsplash.it/300/200/?random';
  list_img_alt.nodeValue = 'architecture';

  // 동적으로 텍스트노드 생성
  // var headline_text = document.createTextNode('새로운 것은 존재하지 않는다. 아직 내가 못 본 것일 뿐.');
  // var headline_text = _.createText('새로운 것은 존재하지 않는다. 아직 내가 못 본 것일 뿐.');
```

### - 조작 메서드 및 유틸리티 함수 실습

```javascript
  // 요소노드를 요소노드에 붙이려면?
  // 부모노드.appendChild(자식노드)
  // ul
  //  li
  //    h2
  //    a(href)
  //      img(src, alt)
  // list.appendChild(list_item);
  // list_item.appendChild(headline);
  // list_item.appendChild(list_link);
  // list_link.appendChild(list_img);
  _.appendChild(list, list_item);
  _.appendChild(list_item, headline);
  _.appendChild(list_item, list_link);
  _.appendChild(list_link, list_img);
  console.log('list:', list);

  // 속성노드를 요소노드에 붙이려면?
  list_link.setAttributeNode(list_link_href);
  list_img.setAttributeNode(list_img_alt);
  list_img.setAttributeNode(list_img_src);

  // 텍스트노드를 요소노드에 붙이려면?
  // headline.appendChild(headline_text);
  // _.appendChild(headline, headline_text);
```

## 동적 Navigation Indicator 만들기

### 1. 순환시킬 데이터 객체

```javascript
  var data = [
    {
      index: '1068',
      alt: '푸른 빛 탁자'
    },
    {
      index: '1017',
      alt: '광활한 산맥'
    },
    {
      index: '1067',
      alt: '빛이 스며드는 해안 도시 풍경'
    },
    {
      index: '1060',
      alt: '커피 향기 가득한 매장'
    },
    {
      index: '1042',
      alt: '수 놓은 별 빛이 흐른다'
    },
    {
      index: '1039',
      alt: '녹색 산림 위 폭포수'
    },
    {
      index: '1027',
      alt: '우수에 찬 눈빛의 여인'
    },
    {
      index: '1013',
      alt: '하얀 차량 내부에서 전화 통화 중인 여인'
    },
    {
      index: '977',
      alt: '아름다운 버섯과 빛의 향연'
    },
    {
      index: '859',
      alt: '강렬한 인상을 주는 붉은 벽과 노란 대문'
    },
  ];

  // 새로운 아이템 추가
  data.push({
    index: 1062,
    alt: '청순 Dog~~'
  });
```

### 2. 반복문과 함수를 이용하여 동적으로 controller 영역 만들기

```javascript
  // 동적 생성해야 할 템플릿 코드
  // <li role="presentation">
  //   <a href class="photo-showcase-indicator" role="tab">
  //     <img src="https://unsplash.it/100/100?image=" alt="">
  //   </a>
  // </li>

  var controller = _.selector('.photo-showcase-controller [role=tablist]');

  for ( var i=0, l=data.length; i<l; ++i ) {

    var item = data[i];
    var index = item.index;
    var alt = item.alt;

    var li = _.createEl('li');
    li.setAttribute('role', 'presentation');

    var a = _.createEl('a');
    a.setAttribute('role', 'tab');
    a.setAttribute('href', '');
    a.setAttribute('class', 'photo-showcase-indicator');

    var img = _.createEl('img');
    img.setAttribute('src', 'https://unsplash.it/100/100?image=' + index);
    img.setAttribute('alt', alt);

    _.appendChild(li, a);
    _.appendChild(a, img);
    _.appendChild(controller, li);

    // 클로저 함수 활용 예시
    // 방법 1.
    a.onclick = function(index) {
      return function(){
        console.log(this, index);
        return false;
      };
    }(i);

    // 방법 2.
    // 이벤트 바인딩 (속성 <-> 함수)
    a.onclick = changeShowcaseViewWrapper(i);

    // JavaScript 객체는 속성을 만들기가 너~~~~~무 쉽다.
    // 방법 3.
    // 객체의 속성을 추가하여 메모리하라.
    // a???? <a> 요소노드 === JavaScript 객체
    a.index = i;
    a.onclick = changeShowcaseView;

  }

  // 이벤트 핸들러(함수) 정의
  // 방법 2.
  function changeShowcaseViewWrapper(index) {
    return function changeShowcaseView() {
      // this === 클릭한 <a>
      console.log(this, index);
      // 기본 동작 차단 (구형)
      return false;
    };
  }

  // 방법 3.
  function changeShowcaseView() {
    // this === 클릭한 <a>
    // console.log(this, this.index);
    var source = data[this.index];
    var showcase = _.selector('.photo-showcase img');
    showcase.setAttribute('alt', source.alt);
    var showcase_old_src = showcase.getAttribute('src');

    // 방법 1.
    // .slice(), .indexOf() 를 활용한 예시
    var end_index = showcase_old_src.indexOf('=') + 1;
    var showcase_new_src = showcase_old_src.slice(0, end_index) + source.index;

    // 방법 2.
    // RegExp, replace() 를 활용한 예시
    var showcase_new_src = showcase_old_src.replace(/=.+/, function(){
      return '=' + source.index;
    });

    showcase.setAttribute('src', showcase_new_src);
    // 기본 동작 차단 (구형)
    return false;
  };
```

### - 중간체크! - String.prototype객체의 메서드들 

- .charAt(index)
- .substring(start[, end])
- .substr(start[, length])
- .indexOf(string)
- .slice(start[, end])
- .split(string) => array
- .replace(string|regexp, string|function)

### 3. 접근성 개선

```javascript
    // 문서객체 참조
    var container        = _.selector('.photo-showcase-container');
    var container_active = 'active';
    var indicator_first  = _.selector('li:first-child a', controller);
    var indicator_last   = _.selector('li:last-child a', controller);

    // focus, blur 이벤트 감지
    indicator_first.onfocus = function() {
    // container 요소에 활성화 클래스를 추가한다.
        var container_class = container.getAttribute('class');
        container_class += ' ' + container_active;
        container.setAttribute('class', container_class);
  };

    indicator_last.onblur = function() {
    // container 요소에 활성화 클래스를 제거한다.
        var container_class = container.getAttribute('class');
        container_class = container_class.replace(container_active, '').trim();
        container.setAttribute('class', container_class);
  };
```