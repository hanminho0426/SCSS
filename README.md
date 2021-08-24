# SCSS
<a href="https://www.sassmeister.com">SCSS 연습 사이트</a>
- CSS는 주석으로 "/**/"만 가능하지만, SCSS는 "/* */"와 // 모두 사용가능하다.

```scss
.container{
  h1{
    color: royalblue;
    /*background-color: salmon;*/
    //font-size: 60px;
  }
}
```

## 중첩(Nesting)
```html
<!--html-->
<div class ="container">
  <ul>
    <li>
      <div class="name">Git</div>
      <div class="age">40</div>
    </li>
  </ul>
</div>
```
- CSS는 상위 선택자를 반복 작성해주어야 하기 때문에 많은 시간이 들 수 있다.  
```css
/*css*/
.container > ul li {
  font-size: 30px;
}
.container > ul li name {
  color: royalblue;
}
.container > ul li age {
  color: orange;
}
```
- SCSS의 중첩을 사용하면 CSS의 시간을 줄일 수 있다. 
```scss
//scss
.container {
  > ul{
      li{
        font-size: 30px;
        .name{
          color: royalblue;
        }
        .age
          color: orange;
      }
  }
}
```

## 상위선택자 참조 &
- &는 자신이 포함된 그 영역에 상위 선택자를 참조한다.
```scss
// scss
.btn {
  position: absolute;
  &.active { //.btn을 역할을 &가 대신한다.
    color: red;
  }
}

.list {
  li {
    &:last-child { //li의 역할을 &가 대신한다.
      margin-right:0;
    }
  }
}
```
```css
/* css */
.btn {
  position: absolute;
}
.btn.active {
  color: red;
}

.list li:last-child {
  margin-right: 0;
}
```
```scss
//scss
.fs {
  &-small { font-size: 12px; }
  &-medium { font-size: 14px; }
  &-large { font-size: 16px; }
}
```
```css
/* css */
.fs-small {
  font-size:12px;
}
.fs-medium {
  font-size:14px;
}
.fs-large {
  font-size:16px;
}
```
## 중첩된 속성
- 선택자 끝에 : 블록이 끝난 뒤에 ;를 붙이게 되면 "선택자-"와 같은 네임스페이스가 된다.
- 네임스페이스 : 이름을 통해 구분 가능한 범위를 만들어내는 것으로 일종의 유효범위를 지정하는 방법을 말한다.
```scss
// scss
.box {
  font: {
    weight: bold; //font-weight
    size: 10px;
    family: sans-serif;
  };
  margin: {
    top: 10px; //margin-top
    left: 20px;
  };
  padding: {
    top: 10px; //padding-top
    bottom: 40px;
    left: 20px;
    right: 30px;
  }
}
```
```css
/* css */
.box {
  font-weight: bold;
  font-size: 10px;
  font-family: sans-serif;
  margin-top: 10px;
  margin-left:20px;
  padding-top: 10px;
  padding-bottom: 40px;
  padding-left: 20px;
  padding-right: 30px;
}
```

## 변수(Variables)
- $를 통해 자바스크립트처럼 변수를 만들어 반복적 사용이 가능하다.
- 최상단에 변수를 지정할 경우 전역변수로 쓸수있고, {}안에 변수를 지정하면 그 안에서만 사용이 가능하다.
- 재할당이 가능하다. 재할당이 된 이후부터의 범위는 모두 재할당 값이 된다.
```scss
// scss
$size= 100px; //전역변수: 전체범위

.container {
  &small = 100px; //{}안에서만 사용가능한 변수
  position: fixed;
  top: $size; //100px

  .item {
    &small = 200px; //재할당
    width: $size; //200px
    height: $size; //200px
    transform: translateX($size); //200px
  }
  .box {
    width: $size; // 200px
  }
}
```
```css
/* css */
.container {
  position: fixed;
  top: 100px; 
}
.container .item {
  width: 200px;
  height: 200px;
  transform: translateX(200px);
}
```

## 산술 연산
- 나누기 연산자는 단축 속성으로 해석될 수 있기 때문에 
 ()안에 넣어서 사용하거나, $변수를 지정해서 사용 또는 다른 연산과 같이 사용해야한다.

```scss
// scss
div{
  $size= 30px;
  width: 20px + 20px; //40px
  height: 40px  - 10px; //30px
  font-size: 10px * 2; //20px
  //margin: (30px / 2); //15px
  margin: $size/2;
  //margin: (15px + 15px)/2;
  padding: 20px % 7; //6px
}
span {
  font-size: 10px;
  line-height: 10px;
  font: 10px / 10px; 
  font-family: serif;
  //단축속성  size / line-height font-family으로 단축해 사용가능
}
```
```css
/* css */
div{
  width: 40px;
  height: 30px;
  font-size: 20px;
  margin: 15px;
  padding: 6px;
}
```
- 산술연산을 할 때는 기본적인 단위가 동일해야 한다.
- clac() 사용하면 다른 단위도 출력이 가능한 구조가 된다.
```scss
div {
  width: 100% - 200px; //%와 px는 단위가 다르기 때문에 사용 안된다.
  height: clac(100% - 200px);//clac를 통해 출력가능해진다.
}
```
## 재활용(Mixins)
```html
<!-- html -->
<div class ="container">
  <div class="item">
    Mixin!
  </div>
</div>
```
```css
/* css */
.container {
  width: 200px;
  height: 200px;
  background-color: orange;
  display:  flex;
  justify-content: center;
  align-items: center;
}

.container .item {
  width: 100px;
  height: 100px;
  background-color: royalblue;
  display: flex;
  justify-content: center;
  align-items: center;
}

```
- @mixin을 이용해 만들어진 구조는  @include 키워드를 통해 재활용해 이용할 수 있다.
```scss
// scss
@mixin center {
  display: flex;
  justify-content: center;
  align-items: center;
}
.container {
  @include center;
  .item {
    @include center;
  }
}
.box {
  @include center;
}
```
- @mixin은 인수를 제공한다.
- @mixin을 매개변수를 가지는 하나의 함수처럼 사용 가능하다.
- 변수의 뒤에 ":값" 넣으면 기본값이 되어진다.
- , 쉼표를 통해 여러가지 변수를 늘려서 사용할 수 있다. 
- 키워드 인수: 인수를 사용할때 인수 앞에 매개 변수의 이름을 지정하는 것 그 매개변수를 키워드라고 한다.
```scss
// scss
@mixin box($size: 80pm, $color: tomato) { //매개변수: 값 -> 기본값 // , 쉼표를 통해 여러가지 변수를 늘려서 사용할 수 있다
  width: $size;
  height: $size;
  background-color: $color;
}
.container {
  @include box(200px, red); //인수
  .item {
    @include box($color:green); //키워드 인수 
  }
}
.box {
  @include box(100px);
}
.bottom {
   @include box; //기본값을 사용하는 @mixin은 ()를 넣지 않는다.
}
```
```css
/* css */
.container {
  width: 200px;
  height: 200px;
  background-color: red;
}
.container .item {
  width: 80px;
  height: 80px;
  background-color: green;
}
.box {
  width: 100px;
  height: 100px;
  background-color: tomato;
}
.bottom {
  width: 80px;
  height: 80px;
  background-color: tomato;
}

```
## 반복문
```js
//js
//  시작      종료   반복
for(let i= 0; i < 10; i+= 1>){ console.log(`loop-${i}`)
} 
// "loop-1 ~9 까지 반복됨"
```
- CSS는 Zero-based 개념이 아니기 때문에 JS와 다르게 1부터 숫자가 매겨진다.
- from 처음시작 / through 끝
- JS보관법 ${ } , SCSS보관법 #{ }
- 선택자에 이용할 경우 보관법을 사용하고 숫자가 매겨지는 곳은 사용하지 않는다.

```scss
//scss
//     몇번부터시작  몇번까지에서 끝
@for $i from 1 through 10 .box:nth-child(#{$i})/*번호매기기*/ {
  .box {
    width: 100px * $i; //10번이 반복, 100씩 증가
  }
}
```

## 함수
```scss
//scss
// 수직 수평 코드
@mixin center {
  display: flex;
  justify-content: center;
  align-items: center;
}

//JS와 다른게 앞에 @를 붙인다. 
@function ratio($size, $ratio) {
  @return $size * $ratio
}

.box {
  $width: 100px;
  width: $width;
  height: ratio($width, 1/2); //100px * 1/2
 // height: ratio($width, 9/16); //16:9 비율 계산
  @include center; 
}
```
```css
/* css */
.box {
  width: 100px;
  height: 50px;
  display: flex;
  justify-content: center;
  align-items: center;
}
```

## 색상 내장 함수
- 버튼을 만들 때 유용한 함수
- mix(색상,색상) 2개의 지정한 색상을 섞어서, 새로운 색상을 만들어낸다. 2개의 인수를 필요로 한다.
- lighten(색상,퍼센트) 색상을 퍼센트만큼 밝아지게 한다.
- darken(색상, 퍼센트) 색상을 퍼센트만큼 어둡게 해준다.
- saturate(색상,퍼센트)
색상을 퍼센트만큼 채도를 높여준다.
- desaturate(색상,퍼센트) 색상을 퍼센트만큼 채도를 낮추어 준다.
- grayscale(색상) 색상을 회색으로 바꾸어 준다.
- invert(색상) 색상을 반전시켜준다.
- rgba(색상, 값) 색상의 투명도를 준다.
```html
<!-- html -->
<div class="box"></div>
<div class="box built-in"></div>
```
```scss
// scss
.box {
  $color: royalblue;
  width: 200px;
  height: 100px;
  margin:20px;
  border-radius: 10px;
  background-color:  $color;
  &.hover {
    background-color: darken($color, 10%);
  }

  &.built-in {
    //background-color: mix($color, red); //새로운 색을 만들어낸다.
    // background-color: lighten($color, 10%)
    background-color:
    saturate($color, 10%);
  }
}
```
## 가져오기 
- JS는 @import "./파일.js";
- SCSS는 @import "./파일"; 확장자를 따로 명시하지 않아도 된다.
- SCSS는 @import "./파일",(쉼표)"./파일" 를 통해 또 새로운 파일을 연결할 수 있다.
 ```scss
 @import "./sub", "./sub2";
 ```

### 리팩토링(Refactoring)
- '결과의 변경없이 코드의 구조를 재조정함'을 뜻한다.

### 데이터의 종류
```scss
// scss
$number: 1; // .5, 100px, 1em
$string: bold; // relative, "../imges/a.png"
$color: red; //blue, #FFFF00, rgba(0,0,0,.1) //문자 데이터가 아닌 색상데이터로 해석된다.
$boolean: true; // false
$null: null;
$list: orange, royalblue, yellow; //쉼표로 구분해서 순서대로 나열한 것 마치 배열 데이터와 유사하게 생겼다.
$map: (
  o: orange,
  r: royalblue,
  y: yellow
); // 객체데이터와 유사하다. 키와 키값의 형태이고 JS는 {}지만 SCSS는 ()사용한다.

.box {
  width: 100px; //숫자데이터
  color: red; //색상데이터
  position: relative; //문자데이터
}
```

### @each
- list
```scss
// scss
$list: orange, royalblue, yellow;

// @로 시작하는 each키워드를 통해서  "$list"라는  변수에 있는 해당 데이터를 
// 반복적으로 "$c"라는 이름의 변수에 담아서 {}사이에서 처리하겠다는 의미
@each $c in $list {
  .box {
    color: $c;
  }
} 

```
```css
/* css */
.box {
  color: orange;
}
.box {
  color: royalblue;
}
.box {
  color: yellow;
}
```
- map
```scss
// scss
$map: (
  o: orange,
  r: royalblue,
  y: yellow
);
//    키  밸류
@each $k, $v in $map {
  .box-#{$k} {
    color: $v;
  }
} 
```

```css
.box-0 {
  color: orange;
}

.box-r {
  color: royalblue;
}

.box-y {
  color: yellow;
}
```

### @content
```scss
@mixin left-top {
  position: absolute;
  top: 0;
  left: 0;
  @content;
}
.container {
  width: 100px;
  height: 100px;
  @include left-top;
}

.box {
  width: 200px;
  height: 300px;
  @include left-top { //{}안에 있는 내용을 @mixin안의 새로운 내용에 추가하는 역할
    bottom: 0;
    right: 0;
    margin: auto;
  }
}
```

```css
.container {
  width: 100px;
  height: 100px;
  position: absolute;
  top: 0;
  left: 0;
}

.box {
  width: 200px;
  height: 300px;
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  margin: auto;
}
```
### SCSS의 단점 
- 트리 쉐이킹(Tree Shaking) 트리 쉐이킹이란 단일 번들을 최적화할 때   
사용되는 필요하지 않은 코드를 제거하는 기술을 말한다.
