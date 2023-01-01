---

layout: single
title:  "TIL - TWD HTML:기초"
categories: TIL
tag: [TIL,유데미 - The Web Developer 부트캠프 2023,HTML]
toc: true
toc_sticky: true
author_profile: false
sidebar:
    nav: "docs"

---

# HTML(HyperText Markup Language) 기초

<p data-ke-size="size14"><i>본 내용은 'The Web Developer 부트캠프 2023', 'Mozilla Developer Network'를 참고하여 작성했습니다.</i></p>

## 1. HTML 개요
* HTML을 작성하려면 이미지 요소, 양식 등 많은 HTML요소가 필요하다.
* HTML의 요소는 태그(tag)를 사용하여 표시하며, 다양한 기능을 한다.
* 시작 태그와 종료 태그를 사용하여 범위를 지정한다.
* 태그에는 `<p>`, `<br>`, `<ul>`, `<ol>`, `<li>` 등 다양하게 존재한다.
* 속성은 태그에 부여할 수 있는 작은 정보를 말한다. 속성의 동작을 제어하며 이름-값 쌍으로 나타내며, 구분은 '='로 하여 시작 태그 안에서 작성된다.

```html
<태그 속성="값">Hello</태그>
```

## 2. 제목 요소 [h1](https://developer.mozilla.org/ko/docs/Web/HTML/Element/Heading_Elements)
* 제목(Heading) 6단계의 구획 제목을 나타내는 태그
* 글자 크기를 위해 제목 태그를 사용하면 안 된다.
  * 대신 CSS나 font-size 속성을 사용하면 된다.
* 제목 단계는 항상 h1->h2 순서대로 해야 한다. (올바른 순서가 아니어도 오류는 나지 않는다.)
* 페이지당 하나의 h1만 사용해야 한다. 
  * 여러 개를 써도 오류는 나지 않지만 h1은 단일로 사용하는 것이 모범적인 사례이다.

<style>
![제목](/assets/images/Udemy/01/udemy01_제목.PNG){ display:block; margin:auto;}
</style>

## 3. 단락 요소 [p](https://developer.mozilla.org/ko/docs/Web/HTML/Element/p)
* 하나의 문단(Paragraph)을 나타내는 태그
* 코드 상에서 엔터를 사용한 줄 바꿈은 인식되지 않고 공백으로 인식된다.
* `<P>`요소를 사용해 문단 사이에 여백을 추가하는 것은 좋지 않은 사례이다.
  * 여분의 공간이 필요하다면 [margin](https://developer.mozilla.org/ko/docs/Web/CSS/margin)등의 [CSS](https://developer.mozilla.org/ko/docs/Glossary/CSS)속성을 통해 적용하면 된다.

![단락](/assets/images/Udemy/01/udemy01_단락.PNG)

## 4. HTML 상용구
* HTML5를 사용하고 있다는 표식이라고 생각하면 된다.
* VSCode에서는 !를 입력하고 Tab을 누르면 자동으로 생성된다.
* HTML5요소 중 루트 요소(문서의 최상위 요소)라고 불린다.
* 하나의 head에는 하나의 body가 쌍으로 이루어져 있다.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    
</body>
</html>
```

### 4-1 [head](https://developer.mozilla.org/ko/docs/Web/HTML/Element/head)
* 기계가 식별할 수 있는 문서 정보(메타데이터)를 담는다. 정보로는 문서가 사용할 제목, 스크립트, 스타일 시트 등이 있다.
* Head와 쌍으로 단 하나만 존재한다.

### 4-2 [title](https://developer.mozilla.org/ko/docs/Web/HTML/Element/title)
* 브라우저 탭 상에 표시되는 내용을 수정한다.
  
![Title](/assets/images/Udemy/01/udemy01_Title.PNG)

### 4-3 [body](https://developer.mozilla.org/ko/docs/Web/HTML/Element/body)
* 모든 문서의 내용을 담고 있는 부분이다.
* Head와 쌍으로 단 하나만 존재한다.

## 5. 목록 요소 [ul](https://developer.mozilla.org/ko/docs/Web/HTML/Element/ul), [ol](https://developer.mozilla.org/ko/docs/Web/HTML/Element/ol), [li](https://developer.mozilla.org/ko/docs/Web/HTML/Element/li)
* `<ul>`는 정렬되지 않은 목록을 나타낸다.
* `<ol>`는 정렬된 목록을 나타낸다.
* `<li>`는 목록의 항목을 나타낸다.
  * 반드시 정렬 목록 ol, 비정렬 목록 ul, 메뉴 menu안에 위치해야 한다.

![ulol](/assets/images/Udemy/01/udemy01_ulol태그.PNG)

## 6. 하이퍼링크 [a](https://developer.mozilla.org/ko/docs/Web/HTML/Element/a)
* 웹페이지, 이메일 주소, 파일 혹은 현재 페이지의 다른 위치로 연결할 수가 있다.
* 주로 다른 페이지로 연결될 때 많이 사용한다.
* 속성으로 href은 하이퍼링크가 가리키는 URL로 이동시켜준다.
* VSCode에서 a를 입력하고 Tab을 누르면 자동 생성된다.

```html
<a href="http://www.google.com">Google Website</a>
```

## 7. 이미지 [img](https://developer.mozilla.org/ko/docs/Web/HTML/Element/img)
* HTML 문서에 이미지를 삽입할 수 있게 해준다.
* 닫는 태그가 없다.
* src(source)속성을 사용해야 한다.
* width등을 사용하여 이미지 크기 조절이 가능하다.
  * 사이즈는 HTML보다 CSS로 작성하는 게 더 좋다.
* alt속성은 접근성 면에서 유용하며 이미지가 나오지 않을 시 이미지를 설명해준다.

```html
<img src="이미지 주소와 파일명과 확장자" width ="200px" alt="">
```

![img](/assets/images/Udemy/01/udemy01_img태그.PNG)

## 8. 주석
* 코드를 작성할 때 개발자가 볼 수 있도록 소스의 설명이나 코드의 동작이 반영되지 않게 할 수 있다.
* VSCode에서 'Ctrl'+'/'를 사용하면 된다.

```html
<!-- 주석 내용 -->
```

![주석](/assets/images/Udemy/01/udemy01_주석.PNG)
