## DOM Script

### 탐색 유틸리티 함수 parent()
- 요소의 부모노드를 찾는다. depth 매개변수를 주어, 바로 위 부모만이 아니라 그 위의 부모, 혹은 그 위의 위의 부모도 찾을 수 있다.

### 탐색 유틸리티 함수 hasChild()
- 자식노드을 가지고 있는 요소들을 찾는다.

```javascript
  var parent = function(node, depth) {
    validateElementNode(node);
    depth = depth || 1;
    do { node = node.parentNode; }
    while(node && --depth);
    return node;
  };
  
  var hasChild = function(node) {
    validateElementNode(node);
    return node.hasChildNodes();
  }
```

### 함수 activeParent()와 반복문
- 부모(몇번째 위의 조상)에게 'active'라는 클래스를 주는 함수
- 유사 배열인 노드 집합(NodeList)를 순환(반복 처리)
- 반복 처리하는 일: 이벤트 연결 <<->> 핸들러(함수)

```javascript
  for ( var link, i=0, l=study_content_links.length; i<l; ++i ) {
    link = study_content_links.item(i);
    link.onclick = activeParent;
  }

  function activeParent(){
    // 이벤트 핸들링 구문에서 this는 이벤트의 주인을 가리킨다.
    // console.log(this);
    // this 객체의 부모 객체를 찾아서 'active' 클래스 속성을 추가
    console.log('this.parentNode:', this.parentNode);
    // HTML DOM 방식에서
    // 요소노드에 className 속성 값을 설정
    // this.parentNode.className = 'active';
    _.parent(this).className = 'active';
    // 브라우저 기본 동작 차단 (Prevent Default Action)
    // 구형 방법
    return false;
  };
```

### 자식노드를 가지지 않는 요소들을 찾아 배열에 수집하는 함수

```javascript
(function(global, $){
  'use strict';

  // <body> 내부의 모든 요소를 수집
  var body = $.tag('body'); // document.body
  var body_children = $.tagAll('*', body);
   console.log('body_children:', body_children);

  // 수집된 요소를 순환 처리한다.
  var will_removed = [];
  for ( var i=body_children.length, child; child=body_children[--i]; ) {
    // 처리 과정에서 <script> 요소는 배제한다.
    var node_name = child.nodeName.toLowerCase();
    if ( node_name === 'script' ) { continue; }
    console.log(node_name);
    // 나머지 요소 중, 자식이 없는 요소를 찾아서
    // 새로운 배열에 수집한다.
    // console.log( node_name, child.hasChildNodes() );
    // if ( !child.hasChildNodes() ) {
    if ( !$.hasChild(child) ) {
      will_removed.push(child);
    }
  }
  will_removed.reverse();
  // console.log('will_removed:', will_removed);

}) (window, window.FDS);
```

### 선택 유틸리티 함수 classAll(), classSingle()
- IE 9+ 뿐만 아니라 IE 8 이하에서도 호환되는 크로스 브라우징 유틸리티 함수
- IE 9 이상의 모던 브라우저 : getElementsByClassName 사용
- IE 8 이하의 구형 브라우저 : 유틸리티 함수 tagAll과 반복문을 사용하여 배열로 수집한다. 정규표현식을 이용하여 클래스명이 두개 이상인 경우를 대비한다.

```javascript
var classAll = function(){
    var _classAll = null;
    if ( 'getElementsByClassNames' in Element.prototype ) {
      _classAll = function(name, context) {
        validateError(name, '!string', '첫번째 전달인자는 문자열을 전달해야 합니다.');
        context = context || document;
        validateElementNodeOrDocument(context);
        return context.getElementsByClassName(name);
      };
    } else {
      _classAll = function(name, context) {
        validateError(name, '!string', '첫번째 전달인자는 문자열이어야 합니다.');
        context = context || document;
        validateElementNodeOrDocument(context);
        var _alls = tagAll('*', context);
        var _matched = [];
        var match = new RegExp('(^|\\s)' + name + '($|\\s)');
        for ( var i=0, l=_alls.length; i<l; ++i ) {
          var _el = _alls.item(i);
          if ( match.test(_el.className) ) { _matched.push(_el); }
        }
        return _matched;
      };
    }
    return _classAll;
  }();
  var classSingle = function(name, context) {
    return classAll(name, context)[0];
  };
  ```

### 선택 유틸리티 함수 queryAll(), query()
- 선택자를 찾아주는 함수

  ```javascript
  var queryAll = function(selector, context){
    validateError(selector, '!string', '첫번째 인자는 CSS 선택자 문자열이어야 합니다.');
    context = context || document;
    validateElementNodeOrDocument(context);
    return context.querySelectorAll(selector);
  };
  var query = function(selector, context){
    return queryAll(selector, context)[0];
  };
  ```
