# SCSS_Study
SCSS 공부

< _main.scss_ 참조 >

## 중첩

```scss
  .container {
    h1 {
      background-color: orange;
      color: $color;
      font-size: 60px;
    }
  }
```
## 상위(부모) 선택자 참조

```scss
  .btn {
    position: absolute;
    &.active {                  
        color: red;
    }
  }
  .list {
     li {
         &:last-child {
             margin-right: 0;
         }
     }
  }
  .fs {
    &-small {font-size : 12px;}
    &-medium { font-size : 14px;}
    &-large {font-size : 16px;}
  }
```
## 중첩된 속성

```scss
  .box {
  font: {
      weight: bold;
      size: 10px;
      family: sans-serif;
    };
    margin: {
        top: 10px;
        left: 20px;
    };
    padding: {
        top: 10px;
        bottom: 40px;
        left: 20px;
        right: 30px;
    };
  }
```
## 변수

```scss
  $size: 200px;          // 전역 변수

  .container {
      position: fixed;
      top : $size;
      .item {
          $size: 100px;      // 지역 변수
          width: $size;
          height: $size;
          transform: translateX($size);
      }
  }
```
## 산술 연산

```scss
  div {
    width: 20px + 20px;
    height: 40px - 10px;
    font-size: 10px * 2;
    margin: (30px /2);                  // 나누기는 가로로 묶어준다.
    padding: 20px % 7;
  }
```
## 재활용 @Mixin

```scss
  @mixin box($size : 100px, $color: tomato) {
  width: $size;
  height: $size;
  background-color: $color;
  }
  .container {
    @include box(200px);
    .item {
        @include box(100px,green);
    }
  }
  .box {
    @include box($color: yellow);
  }
```

## 반복문 For

```scss
  @for $i from 1 through 10 {
    .box:nth-child(#{$i}) {
        width: 100px * $i;
    }
  }
```
## 함수

```scss
   @mixin center {
    display: flex;
    justify-content: center;
    align-items: center;
  }

  @function ratio($size, $ratio) {
    @return $size * $ratio
  }

  .box {
    $width : 100px;
    width: $width;
    height: ratio($width, 9/16);
    @include center;
  }
```
## 색상 내장 함수
- mix($color1, $color2), lighten($color, 10%), darken($color, 10%)
- saturate($color, 30%) 색상 채도 증가, desaturate
- grayscale($color) 회색으로 만들어준다.
- rgba($color, 10%) 불투명하게 만들어준다.

## 가져오기

```scss
  @import "./sub.scss", "./sub2.scss";
```
## 반복문 @each

```scss
  $list : orange, royalblue, yellow;
  $map: (
      o : orange,
      r : royalblue,
      y : yellow

  );
  @each $c in $list {
      .box {
          color: $c;
      }
  }
  @each $K in $map{
      .box2-#{$K} {
          color: $K;
      }
  }
```
## 재활용 @content

```scss
   @mixin top-left {
    position: absolute;
    top: 0;
    left: 0;
    @content;
  }
  .container {
    width: 100px;
    height: 100px;
    @include top-left;
  }
  .box {
    width: 200px;
    height: 300px;
    @include top-left {
        bottom: 0;
        right: 0;
        margin: auto;
    }
  }
```

