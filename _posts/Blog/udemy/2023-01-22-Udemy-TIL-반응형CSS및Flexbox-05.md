---

layout: single
title:  "TIL - TWD 반응형 CSS 및 Flexbox"
categories: TIL
tag: [TIL,유데미 - The Web Developer 부트캠프 2023,CSS]
toc: true
toc_sticky: true
author_profile: false
sidebar:
    nav: "docs"

---

# 반응형 CSS 및 Flexbox

<p data-ke-size="size14"><i>본 내용은 'The Web Developer 부트캠프 2023', 'Mozilla Developer Network'를 참고하여 작성했습니다.</i></p>

## 1. [flex](https://developer.mozilla.org/ko/docs/Web/CSS/flex)
* flex CSS 속성은 하나의 플렉스 아이템이 자신의 컨테이너가 차지하는 공간에 맞추기 위해 크기를 키우거나 줄이는 방법을 설정하는 속성
* `display:flex`를 추가하면 된다.

## 2. [Flexbox](https://developer.mozilla.org/ko/docs/Learn/CSS/CSS_layout/Flexbox)
* CSS의 display 속성 중 하나로, 컨테이너들의 레이아웃, 정렬, 비율, 공간 등을 설정 하는 데에 유연하게 조정할 수 있다.
* flexbox는 부모 요소인 flex container과 자식 요소인 flex item으로 구분된다.
* default값은 flex item 배치 처럼 좌-우 방향으로 진행한다.
* 주축(main axis)와 교차축(cross axis)를 활용하여 배치를 조정한다.

![flexbox](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Flexbox/flex_terms.png)

### 1) [flex-direction](https://developer.mozilla.org/ko/docs/Web/CSS/flex-direction)

* 컨테이너 내의 아이템을 배치할 때 주축 및 방향(정방향, 역방향)을 결정한다.
* default값은 좌-우 이다.
* row, row-reverse, column, column-reverse 등이 있다.

### 2) [flex-wrap](https://developer.mozilla.org/ko/docs/Web/CSS/flex-wrap)

* `flex-item` 요소들이 강제로 한줄에 배치되게 할 것인지, 또는 가능한 영역 내에서 벗어나지 않고 여러행으로 나누어 표현 할 것인지 결정하는 속성
* wrap은 여러 행에 걸쳐서 배치된다. default값은 위-아래 이다.
* wrap, nowrap, wrap-reverse 등이 있다.

### 3) [flex-basis](https://developer.mozilla.org/ko/docs/Web/CSS/flex-basis)

* 요소가 배치되기 전에 요소의 최초 크기를 결정한다.

### 4) [felx-grow](https://developer.mozilla.org/ko/docs/Web/CSS/flex-grow)

* `flex-item`이 `flex-container`에 남은 공간이 있을 때 그 공간을 차지할 비율을 정한다.
* 보통 `flex-shrink`, `flex-basis`와 함께 사용한다.

### 5) [flex-shrink](https://developer.mozilla.org/ko/docs/Web/CSS/flex-shrink) 

* `flex-item`의 크기가 `flex-container` 요소의 크기보다 클 때 `flex-shrink` 속성을 사용하는데, 설정된 숫자값에 따라 `flex-container` 요소 내부에서 `flex-item` 요소의 크기가 축소된다.
* 만일 하나의 요소가 `flex-shrink: 0;`이라면 혼자만 줄어들지 않는다.

### 6) [flex 속기법](https://developer.mozilla.org/ko/docs/Web/CSS/flex)

* flex에서 한줄로 basis, grow, shrink를 사용할 수 있다.
* px나 em 단위는 basis 뿐이다.

```css
/* One value, unitless number: flex-grow */
flex: 2;

/* One value, length or percentage: flex-basis */
flex: 10em;
flex: 30%;

/* Two values: flex-grow | flex-basis */
flex: 1 30px;

/* Two values: flex-grow | flex-shrink */
flex: 2 2;

/* Three values: flex-grow | flex-shrink | flex-basis */
flex: 2 2 10%;
```
## 3. justify

### 1) [justify-content](https://developer.mozilla.org/en-US/docs/Web/CSS/justify-content)

* 주축을 기준으로 Grid가 움직이면서 항목 사이 및 주위 공간 정렬 방식을 결정한다.
* start, center, end, space-between, space-around, space-evenly, baseline 등이 있다.

### 2) [justify-items](https://developer.mozilla.org/en-US/docs/Web/CSS/justify-items)

* 주축을 기준으로 Grid가 움직이지 않은 상태에서 항목 사이 및 주위 공간 정렬 방식을 결정한다.
* stretch, center, start, end, baseline 등이 있다.

## 4. arlign

### 1) [align-content](https://developer.mozilla.org/ko/docs/Web/CSS/align-content)

* 행이 1줄이면 의미가 없으며, 2줄 이상이면 교차축을 기준으로 전체 정렬 방식을 결정한다. -> `flex-wrap: warp` 또는 `flex-wrap: wrap-reverse`가 적용되야 한다.
* start, center, end, space-between, space-around, baseline 등이 있다.

### 2) [align-items](https://developer.mozilla.org/en-US/docs/Web/CSS/align-items)

* 한 행의 교차축을 기준으로 항목 사이 및 주위 공간 정렬 방식을 결정한다.
* stretch, center, start, end, baseline 등이 있다.

### 3) [align-self](https://developer.mozilla.org/en-US/docs/Web/CSS/align-self)

* `align-items`와 개념은 비슷하며, 개별요소를 옮길 때 사용한다.

> baseline
> * 텍스트의 기준선에 맞춰 정렬한다.
> * 요소마다 높이가 다르다면 유용

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="WNKMWEW" data-preview="true" data-editable="true" data-user="ycm0926" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/ycm0926/pen/WNKMWEW">
  Untitled</a> by Changmin Yang (<a href="https://codepen.io/ycm0926">@ycm0926</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

## 5. [Media_Queries](https://developer.mozilla.org/ko/docs/Web/CSS/Media_Queries/Using_media_queries#%ea%b5%ac%eb%ac%b8)

* CSS의 문법 중 하나이며, 미디어 쿼리는 다양한 기기 특성과 파라메터의 존재 여부에 따라 사이트, 혹은 앱을 조정할 수 있다. 일반적으로 <u>반응형 디자인을 사용할 때 많이 사용한다.</u>
* 사용 방법은 `@-규칙` 이라고 불리는 [`@media`](https://developer.mozilla.org/ko/docs/Web/CSS/@media)로 사용하며, 다른 프로그래밍 언어의 if 조건문과 비슷한 개념이다.

> [@-규칙](https://developer.mozilla.org/ko/docs/Web/CSS/At-rule) 
> * @-규칙은 스타일 규칙을 가져올 수 있는 규칙이며, 다른 프로그래밍 언어 모듈과 비슷한? 개념인 것 같다.  
> * 예륻 들어, @import url("fineprint.css") 이면 다른 스타일 시트에서 스타일 규칙을 가져올 수 있다.

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="VwBxbZy" data-preview="true" data-editable="true" data-user="ycm0926" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/ycm0926/pen/VwBxbZy">
  Untitled</a> by Changmin Yang (<a href="https://codepen.io/ycm0926">@ycm0926</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>