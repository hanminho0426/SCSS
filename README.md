# SCSS
<a href="https://sassmeister.com">SCSS 연습 사이트</a>
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
.container ul li {
  font-size: 30px;
}
.container ul li name {
  color: royalblue;
}
.container ul li age {
  color: orange;
}
```
- SCSS의 중첩을 사용하면 CSS의 시간을 줄일 수 있다. 
```scss
//scss
.container {
  ul{
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