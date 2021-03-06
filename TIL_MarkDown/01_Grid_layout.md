# Grid Layout

## Toggle Grid Module (토글 그리드 모듈)

### 1. 바디 전체에 position: relative
```css
.show-grid {
  position: relative;
}
```

### 2. 바디의 가상요소박스에 position: absolute
```css
.show-grid::before,
.show-grid::after {
  content: '';
  position: absolute;
  top: 0;
  height: 100vh;
}
```

### 3. 행 만들기
```css
.show-grid::before {
  z-index: 10000;
  left: 0;
  width: 100%;
  background: linear-gradient(180deg, transparent 20px, #0cf 20px);
  background-size: 1px 21px;
}
```
+ body의 before 가상요소박스에 position: absolute, top: 0, left: 0 값을 준다.
+ background: linear-gradient로 0 ~ 20px 영역은 transparent(투명)값을, 20px 이후는 색상값을 준다. 
+ background-size: 1px 21px 값을 주어, 색상이 들어간 1px(21px - 20px = 1px) 영역이 반복되면서 1px 너비의 행이 만들어 진다.

### 4. 열 만들기
```css
.show-grid::after {
  z-index: 10010;
  left: 50%;
  width: 1080px;
  background: linear-gradient(90deg, transparent 10px, rgba(251, 137, 137, 0.35) 10px, rgba(251, 137, 137, 0.35) 80px, transparent 80px);
  background-size: 90px 1px;
  transform: translateX(-50%);
```
- absolute 상태에서 left: 50%, translateX(-50%) 값을 주어 중앙으로 정렬한다.
- width 값을 container 전체 너비와 같은 값으로 준다.
- background: linear-gradient 값으로 다음과 같이 준다. 0 ~ 10px 영역은 컬럼의 margin-left로 transparent(투명)값을 준다. 10px ~ 80px 영역은 컬럼 영역으로 색상값을 준다. 80px 이상의 영역은 컬럼의 margin-right로 transparent(투명)값을 준다.
- background-size: 90px 1px 값을 주어 0 ~ 90px(투명 - 색 - 투명) 영역이 반복되어 컬럼이 만들어 진다.
- rgba 함수에서 0.35의 투명도 값을 주어 행이 겹쳐 보이도록 한다.
- 컬럼의 z-index 값을 행보다 높은 값을 부여하여 행 위에 렌더링 되도록 한다.

---

## Nesting Row Module (중첩 행 모듈)

```css
.row{
  &.is-nesting {
    & > :first-child { margin-left: 0; }
    & > :last-child { margin-right: 0; }
  }
}
```
- row 요소에 .is-nesting 클래스를 부여한다.
- 부모요소 박스와 자식요소 박스의 마진이 중첩되어 원하는 값이 나오지 않기 때문이다.
- 첫번째 자식요소의 margin-left와 마지막 자식요소의 margin-rigth에 0값을 부여하여 중복되는 부분을 제거한다.

---

## 페이지 총 폭의 길이를 구하는 함수
- 70px * 12 + 20px * 12
- ($column-width + $gutter-width) * $columns
```css
$page-width: ($column-width + $gutter-width) * $columns;
```

---

## 컬럼 개수에 따른 폭(width) 구하는 공식
- 컬럼_폭 × 컬럼_개수 + 거터_폭(합) * (컬럼_개수 - 1)
- calc( 70px * $i + (10px * 2) * ($i - 1) )
```javascript
@function column-width($n) {
  @return $column-width * $n + $gutter-width * ($n - 1);
}
```

---

## 옵셋 개수에 따른 마진(margin-left) 구하는 공식
- 컬럼_폭 × 컬럼_개수 + (컬럼_폭 + 거터_절반_폭)
```javascript
@function offset-width($n) {
  @return column-width($n) + ($gutter-width + $half-gutter-width);
}
```