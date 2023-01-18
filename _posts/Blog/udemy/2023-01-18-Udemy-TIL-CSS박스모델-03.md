---

layout: single
title:  "TIL - TWD CSS:박스모델"
categories: TIL
tag: [TIL,유데미 - The Web Developer 부트캠프 2023,CSS]
toc: true
toc_sticky: true
author_profile: false
sidebar:
    nav: "docs"

---

# CSS(Cascading Style Sheets) 박스모델

<p data-ke-size="size14"><i>본 내용은 'The Web Developer 부트캠프 2023', 'Mozilla Developer Network'를 참고하여 작성했습니다.</i></p>

## 1. [박스모델: 가로와 세로](https://developer.mozilla.org/ko/docs/Web/CSS/width)


```css
div {
    width: 200px;
    height: 300px;
    background-color: aqua;
}
```

![cssbox](/assets/images/Udemy/06/udemy06_cssbox.PNG)

![cssbox2](/assets/images/Udemy/06/udemy06_cssbox2.PNG)

## 2. [박스모델: 테두리와 모깍기](https://developer.mozilla.org/ko/docs/Web/CSS/border)

```css
#one {
    background-color: pink;
    border-width: 5px;
    /* 테두리 사이즈 */
    border-color: black;
    /* 테두리 색상 */
    border-style: solid;
    /* 실선 테두리 */
    box-sizing: border-box;
    /*테두리 기준으로 box 크기 결정*/
}
```

![cssbox3](/assets/images/Udemy/06/udemy06_cssbox3.PNG)

### 테두리 한 번에 작성하는 방법

```css
#two {
    background-color: purple;
    border: 4px solid black;
    /* 너비 | 스타일 | 색 */
    border-left-style: dotted;
    /* 테두리 스타일 왼쪽 적용 */
    border-radius: 50%;
    /* 테두리 둥글게 반영 크기 */
}
```

![cssbox4](/assets/images/Udemy/06/udemy06_cssbox4.PNG)

## 2. [박스 모델:패딩](https://developer.mozilla.org/ko/docs/Web/CSS/padding)

* 개발자 도구 초록박스 -> padding 값  
   ![cssbutton](/assets/images/Udemy/06/udemy06_toolbox.PNG)
* padding은 content와 border 사이의 공간
* 시계 방향으로 한 번에 작성이 가능하다.

```css
#b1 {
    /* padding 상하좌우 반영 크기 */
    padding: 20px;
}

#b2 {
    /* padding 상하,좌우 반영 크기 */
    padding: 10px 20px;
}

#b3 {
    /* padding 상,좌우,하 반영 크기 */
    padding: 20px 30px 40px;
}
    /* padding 상,우,하,좌 반영 크기 */
#b4 {
    padding: 10px 20px 30px 40px;
}
```

![cssbutton](/assets/images/Udemy/06/udemy06_cssbutton.PNG)


## 3. [박스 모델:여백](https://developer.mozilla.org/ko/docs/Web/CSS/margin)

* 개발자 도구 주황박스 -> margin(여백) 값   
    ![cssbutton](/assets/images/Udemy/06/udemy06_toolbox.PNG)   
* content 바깥쪽 여백 간격
* padding과 똑같이 4가지 방법으로 작성이 가능하다.
* body는 기본적으로 8px의 margin을 가지고 시작한다.

```css
#b1 {
    /* padding 상하좌우 반영 크기 */
    padding: 20px;
    /* margin 상하좌우 반영 크기 */
    margin: 20px;
    /* margin 왼쪽만 반영 크기 */
    margin-left: 100px;
}

#b2 {
    /* padding 상하,좌우 반영 크기 */
    padding: 10px 20px;
    /* margin 상하,좌우 반영 크기 */
    margin: 10px 20px;
}

#b3 {
    /* padding 상,좌우,하 반영 크기 */
    padding: 20px 30px 40px;
    /* margin 상,좌우,하 반영 크기 */
    margin: 20px 30px 40px;

}

#b4 {
    /* padding 상,우,하,좌 반영 크기 */
    padding: 10px 20px 30px 40px;
    /* margin 상,우,하,좌 반영 크기 */
    margin: 10px 20px 30px 40px;
}
```

![cssbutton2](/assets/images/Udemy/06/udemy06_cssbutton2.PNG)


## 4. [디스플레이 속성](https://developer.mozilla.org/en-US/docs/Web/CSS/display)

* inline
  * width와 height를 속성으로 지정해도 무시된다.
    * content의 크기에 따라 크기가 결정된다.
  * margin은 위 아래에는 적용 되지 않는다.
  * padding은 좌, 우는 공간과 시각적 모두 적용 되지만 위, 아래는 시각적으로는 보이지만 공간을 차지 하지는 않는다.

* block
  * 기본적으로 width값이 100% 반영된다.
  * width, height, margin, padding 속성이 모두 반영이 된다.

* inline-block
  * 줄바꿈이 이루어지지 않는다.
  * block처럼 width와 height를 지정 할 수 있다.
  * 만약 width와 height를 지정하지 않을 경우, inline과 같이 content만큼 영역이 잡힌다.
  * 대표적으로 span, button, input, select 태그 등에 사용한다.

```css
#one {
    background-color: palevioletred;
    border: 2px solid black;
    width: 300px;
    padding: 25px;
    margin: 25px;
}

#two {
    background-color: palevioletred;
    border: 2px solid black;
    width: 300px;
    padding: 25px;
    margin: 25px;
    display: block;
}

#three {
    background-color: palegreen;
    border: 2px solid black;
    width: 200px;
    padding: 25px;
    display: inline-block;
}
```

![display](/assets/images/Udemy/06/udemy06_display.PNG)

## 5. [CSS UNITS](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Values_and_units)(단위)

* %
  * 부모 요소, 폰트 크기 등 다양한 기준을 비율로 값을 결정한다.
  * 일반적으로 너비나 높이 지정에 가장 많이 사용된다.

* em
  * 부묘 요소와 똑같은 크기가 된다.
    * ex) 2em은 부모 요소보다 2배 크게 된다.
  * 단계적으로 중첩된다.

* rem
  * root em은 html의 글씨 크기에 따라 비례한다.
  * 보통 예측하기 편해서 em보다 많이 사용한다.

```css
#em {
    font-size: 15px;
}

#rem {
    font-size: 15px;
}

#em ul {
    font-size: 1.5em;
    padding: 2em 2em;
    background-color: aquamarine;
    color: violet;
}

#rem ul {
    font-size: 1.5rem;
    padding: 2rem 2rem;
    background-color: aquamarine;
    color: violet;
}
```

![em,rem](/assets/images/Udemy/06/udemy06_em,rem.PNG)
