---

layout: single
title:  "TIL - TWD HTML:폼과 테이블"
categories: TIL
tag: [TIL,유데미 - The Web Developer 부트캠프 2023,HTML]
toc: true
toc_sticky: true
author_profile: false
sidebar:
    nav: "docs"

---

# HTML 폼(FORMS)과 테이블(TABLE)

<p data-ke-size="size14"><i>본 내용은 'The Web Developer 부트캠프 2023', 'Mozilla Developer Network'를 참고하여 작성했습니다.</i></p>

## 1. HTML: [테이블(TABLE)](https://developer.mozilla.org/ko/docs/Web/HTML/Element/table)

*  행과 열로 이루어진 표

### 테이블 태그 [td](https://developer.mozilla.org/ko/docs/Web/HTML/Element/td), [tr](https://developer.mozilla.org/ko/docs/Web/HTML/Element/tr), [th](https://developer.mozilla.org/ko/docs/Web/HTML/Element/th)

* td(table data)는 데이터를 포함하는 표의 셀을 만드는 역할
* tr(table row)은 테이블의 행 셀을 만드는 역할
* th(table head)은 테이블의 제목을 만드는 역할

### 테이블 시맨틱 태그 [thead](https://developer.mozilla.org/ko/docs/Web/HTML/Element/thead), [tbody](https://developer.mozilla.org/ko/docs/Web/HTML/Element/tbody), [tfoot](https://developer.mozilla.org/ko/docs/Web/HTML/Element/tfoot)

  * `<thead>` 테이블의 머리말 그룹태그
  * `<tbody>` 테이블의 본문 부분의 그룹태그
  * `<tfoot>` 테이블의 꼬리말 부분의 그룹태그

![테이블](/assets/images/Udemy/03/udemy03_테이블.PNG)


### 테이블 colspan, rowspan

* colsapn 테이블의 열을 합치기 위해 사용한다.
* rowspan 테이블의 행을 합치기 위해 사용한다.

![테이블](/assets/images/Udemy/03/udemy03_테이블span.PNG)

## 2. HTML:[폼(FORMS)](https://developer.mozilla.org/ko/docs/Web/HTML/Element/form)

* 정보를 제출하기 위한 대화형 컨트롤을 포함하는 문서 구획 즉, 입력 양식 전체를 감싸서 제출한다.
* 예를 들어 텍스트 입력란이나 비밀번호 입력란 같은 껍데기나 컨테이너에 가깝다.
* 폼 태그의 속성으로는 name, action, method, target 등이 있다.
  * action: 전송할 서버 쪽 script 파일을 지정 (전송되는 서버 url 또는 html 링크)
  * name: form의 이름이며, 서버로 제출된 폼 데이터를 참조하기 위해 사용
  * target: action에서 지정한 script 파일을 현재 창이 아닌 다른 위치에 열도록 지정
  * method: 폼을 서버에 전송하는 방식 선택 (GET 또는 POST)
* 폼이 제출 되었을 때, action 속성을 통해 데이터를 보낼 위치와 시간을 지정한다.
* action으로 예를 들면, 어떠한 검색을 하면 action 통해 HTTP 요청으로 데이터를 전송하여 서버에 작업이 들어오고 대량의 데이터 베이스를 검색해서 이미지 및 모든 게시물을 찾아 웹 페이지로 조합한 다음 HTTP 응답으로 요청한 페이지를 전달한다.

>HTML5에서는 더 이상 `<form>` 요소에 반드시 action 속성을 명시할 필요가 없도록 변경되었다.

### [input](https://developer.mozilla.org/ko/docs/Web/HTML/Element/Input)

*  `<input>`은 웹 기반 양식에서 사용자의 데이터를 받을 수 있는 대화형 컨트롤을 생성한다.
*  `<input>` 요소의 동작 방식은 type 특성에 따라 현격히 달라지므로 type 속성이 가장 중요하다.
*  중요한 속성 중 하나인 placeholder 속성은 입력란의 임시텍스트를 지정하여 입력하기 전에 보이는 글이다.
*  닫는 태그가 없으며, Enter로 form 제출이 가능하다.
  
### [label](https://developer.mozilla.org/ko/docs/Web/HTML/Element/label)

* `<label>`은 사용자 인터페이스 항목의 설명을 나타낸다.
* for 속성을 사용해서 `<label>` 을 `<input>` 요소와 연결해준다.
* `<label>` 을 `<input>` 요소와 연결하면 몇 가지 이점이 있다.
  * 1. label 텍스트는 텍스트 입력과 시각적으로 관련이 있을 뿐만 아니라 화면리더기(screenreader) 는 폼 입력(form input)에서 label을 읽어서 보조기술(assistive technology) 사용자가 입력해야하는 텍스트가 무엇인지 더 쉽게 이해할 수 있어서 프로그래밍 적으로도 관련이 있다.
  * 2. 관련 label 을 클릭해서 input 자체에 초점을 맞추거나 활성화를 시킬 수 있다. (활성되어서)늘어난 누를 수 있는 영역(hit area)은 터치스크린 사용자를 포함해 입력하려 하는 모든 사람에게 이점을 준다.
* `<label>` 을 `<input>` 요소와 연관시키려면, `<input>` 에 **<u>id속성</u>**을 넣어야 한다.
* 한 페이지에 한 개의 요소만 지정된 id를 지녀야 한다. 즉, 사용한 id요소는 똑같은 이름으로 재사용하면 안 된다.
* `<label>` 안에 `<input>` 요소를 넣어 작성이 가능하지만 중첩하지 않는 게 표준이고 스타일을 각각 할 수 없어 잘 사용하지 않는다.

![label](/assets/images/Udemy/03/udemy03_label.PNG)

(Enter a Username, Enter a Password, Enter a Username 클릭하면 연결된 iuput으로 이동한다.)

### [butten](https://developer.mozilla.org/ko/docs/Web/HTML/Element/button)

* `<button>`은 form안에 butten이 있다면 기본값으로 해당 form을 제출해준다.
* type="butten"을 넣어주면 폼 안에서도 폼 제출이 아닌 평범한 butten으로 동작한다.
* `<input>` 속성에 butten을 넣어도 똑같은 기능을 하지만 value 속성을 넣어야 이름을 변경하는 등의 조금의 불편함이 있다.

![button](/assets/images/Udemy/03/udemy03_button.PNG)

![button2](/assets/images/Udemy/03/udemy03_button2.PNG)
(폼 안의 button을 누르면 form의 action속성으로 /tacos라는 목적지 url로 이동한 결과.)

### [name](https://developer.mozilla.org/ko/docs/Web/HTML/Element/Input#htmlattrdefname)

* `<input name="">`은 input 양식 컨트롤의 이름이다. 이름/값 짝(name/value pair)의 일부로서 양식과 함께 전송된다.
* 즉, 데이터를 서버로 전송할 때 사용되는 name이다.
* 보통 이 값은 공백이 없고 짧다.

![name](/assets/images/Udemy/03/udemy03_name.PNG)

![name2](/assets/images/Udemy/03/udemy03_name2.PNG)

> 아래는 name을 실제 유튜브에서 사용되는 검색 name(search_query)으로 설정하면 바로 youtube검색을 실행시켜준다.

![input](/assets/images/Udemy/03/udemy03_input.PNG)

![input](/assets/images/Udemy/03/udemy03_input2.PNG)

### [checkbox](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/checkbox), [radio](https://developer.mozilla.org/ko/docs/Web/HTML/Element/Input/radio), [select](https://developer.mozilla.org/ko/docs/Web/HTML/Element/select)

**checkbox**
* `<input type="checkbox">`는 공식 정부 문서 양식에서 볼 수 있는 것처럼 활성화될 때 체크(체크)되는 상자로 기본적으로 렌더링된다.
* checked를 통해 미리 체크가 가능하다.


**radio**
* `<input type="radio">`는 보통 서로 관련된 옵션을 나타내는 라디오 버튼 콜렉션, 라디오 그룹 에 사용된다.
* id로 연결하여 임의의 그룹 내에서는 동시에 하나의 라디오 버튼만 사용할 수 있다.

**select**
* `<select>`은 옵션 메뉴를 제공하는 컨트롤을 나타낸다.
* `<option>` 태그의 selected 속성은 페이지가 로드될 때 옵션 중에서 미리 선택되어지는 옵션을 명시한다.
* <option> 요소는 <select>, <optgroup>, <datalist> 요소의 항목을 정의한다.
* <option>을 사용해 팝업 메뉴 등 목록에서 하나의 항목을 나타낼 수 있다.

![rcs](/assets/images/Udemy/03/udemy03_r,c,s.PNG)

### [range](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/range), [textarea](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea)

**range**
* `<input type="range">`를 통해 사용자는 정확한 값이 아닌 슬라이더 또는 다이얼 컨트롤을 사용할 수 있다.
* 속성으로 min, max, step 등을 사용할 수 있다.
* `<input type="number">`에도 사용이 가능하다.

**textarea**
* `<textarea>`는 여러 줄의 일반 텍스트 편집 컨트롤을 나타내며 사용자가 상당한 양의 자유 형식 텍스트를 입력할 수 있도록 하려는 경우에 유용하다.
* rows, cols 속성을 이용하여 크기 조절이 가능하다.

![range](/assets/images/Udemy/03/udemy03_range.PNG)

## 3. HTML5 폼의 유효성 검사

### [required](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/required)

* `<input>`의 required속성은 사용자가 소유 양식을 제출하기 전에 주어진 조건을 만족해야 제출되게 해준다.
* required는 text, search, url, tel, email, password 등 유형이 있다.
* [pattern](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/pattern)속성에 정규표현식을 활용해서 복잡한 조건으로 제한이 가능하다.
* 아래의 이미지는 required속성의 text와 range의 유형이다.

![required](/assets/images/Udemy/03/udemy03_required.PNG)

![required](/assets/images/Udemy/03/udemy03_required2.PNG)
