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
