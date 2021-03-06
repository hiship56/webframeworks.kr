---
layout : tutorials
title : 돔 조작
category : tutorials
subcategory : tips
summary : 이 문서는 http://callmenick.com/post/basics-javascript-dom-manipulation 를 번역한 내용입니다.
permalink : /tutorials/translate/javascript-dom-manipulation
tags : javascript dom
author : apple77y
---

몇 가지 간단한 자바스크립트 돔 조작 설명을 할 것이다. 주로 돔 요소의 생성, 삽입, 삭제, 수정, 스타일, 접근 관계와 같은 유용한 내용을 다룬다.

``` javascript
var el = document.createElement('div');
document.body.appendChild(el);
el.className = 'container';
el.style.marginTop = '30px';
```

여기 나열된 자바스크립트 돔 조작 메소드는 모질라 개발 사이트에 잘 정리되어있다. 이건 한 페이지에서 그냥 간단하게 살펴볼 수 있는 설명서 정도로 보면 된다. 각각의 항목들은 공식 레퍼런스 페이지로 이동하면 더 자세히 볼 수 있다.

## 1) 돔 요소를 생성 ([MDN Reference](https://developer.mozilla.org/en-US/docs/Web/API/Document/createElement))
HTML 문서 안에서 HTML 요소나 HTMLUnknownElement를 생성한다.

``` javascript
var element = document.createElement(tagName);
```
- `element`는 element의 객체로 생성 되었다.
- `tagName`은 element가 어떤 타입으로 생성될 지 정해주는 문자 값이다. 만들어진 element의 nodeName은 `tagName`의 값으로 초기화 될 것이다. 이 값으로 예약어(html:a와 같은)를 사용해서는 안 된다.

## 2) 돔에 새로운 요소를 추가 ([MDN Reference](https://developer.mozilla.org/en-US/docs/Web/API/Node/appendChild))
상위 노드의 하위 리스트 제일 마지막에 하나의 노드를 추가한다. 만약 노드가 이미 존재한다면, 그것은 현재 상위 노드에서 제거되고 새운 상위 노드에 추가 된다.

``` javascript
var child = element.appendChild(child);
```

- `element`는 상위 요소다.
- `child`은 `element`의 아래에 추가될 노드다.

## 3) HTML 요소의 스타일을 변경 ([MDN Reference](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/style))
`HTMLElement.style` 속성은 element의 style 속성을 나타내는 객체다. 하나의 요소에 적용된 모든 CSS 속성 값을 알아보기 위해서는 `window.getComputedStyle()`을 사용하면 된다.

``` javascript
element.style.color = "#ff3300";
element.style.marginTop = "30px";
element.style.paddingBottom = "30px";
```

## 4) HTML 요소를 접근하는 방법 ([MDN Reference](https://developer.mozilla.org/en-US/docs/Web/API/Element/innerHTML))
`innerHTML`은 element 자손의 HTML 구문을 가져오거나 설정할 때 사용한다.

``` javascript
// get the HTML of "element"
var content = element.innerHTML;

// set the HTML of "otherElement"
otherElement.innerHTML = content;
```

## 5) Class 이름에 접근하는 방법 ([MDN Reference](https://developer.mozilla.org/en-US/docs/Web/API/Element/innerHTML))
`className`은 element의 class 속성에 접근할 수 있다.

``` javascript
// get the class name of "element"
var cName = element.className;

// set the class name of "otherElement"
otherElement.className = cName;
```

## 6) ID에 접근하는 방법 ([MDN Reference](https://developer.mozilla.org/en-US/docs/Web/API/Element/id))
Gets or sets the element’s identifier (attribute id).
요소의 식별자(id 속성)에 접근하는 방법

``` javascript
// get the id of "element"
var idStr = element.id;

// set the id of "otherElement"
otherElement.id = idStr;
```

## 7) 돔 요소에 접근하는 방법
돔 요소에 접근하는 방법은 다양하다.

### 7a) ID를 통해 접근하는 방법 ([MDN Reference](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelectorAll))
요소의 ID로 참조 값이 반환된다.

``` javascript
element = document.getElementById(id);
```

### 7b) Class 이름으로 접근 ([MDN Reference](https://developer.mozilla.org/en-US/docs/Web/API/document.getElementsByClassName))
클래스 네임이 동일한 하위 요소들이 담긴 배열이 반환된다. IE8 이하 버전에서는 지원되지 않으므로 사용에 주의해야 한다.

``` javascript
elements = document.getElementsByClassName(names); // or:
elements = rootElement.getElementsByClassName(names);
```

- `elements`는 `HTMLCollection`의 기초 요소다.
- `names`은 클래스 이름이 모인 리스트 중에 맞는 값이 있는지 찾기 위한 텍스트다. 클래스 이름은 공백으로 구분된다.
- `getElementsByClassName`은 document 뿐만 아니라 다른 요소들도 부를 수 있다. 불린 요소는 탐색의 최상단 값으로 활용될 수 있다.

### 7c) Tag 이름으로 접근하는 방법 ([MDN Reference](https://developer.mozilla.org/en-US/docs/Web/API/document/getElementsByTagName))
입력한 태그 이름을 갖는 HTMLCollection 요소들이 반환된다. 최상단 노드를 포함한 모든 document가 탐색된다.

``` javascript
var elements = document.getElementsByTagName(name);
```

- 요소들은 트리 구조에서 순서대로 탐색 된 live HTMLCollection이다. (아래 노트 참고)
- `name`은 요소들의 이름을 의미하는 텍스트다. `"*"` 문자를 넣게 되면 모든 요소를 탐색할 수 있다.

### 7d) 첫 번째 요소에 접근하는 방법 ([MDN Reference](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelector))
셀렉터 그룹과 매칭이 되는 첫 번째 요소를 반환한다. (깊이 우선 전위 순회 사용) IE8 이상 지원된다.

``` javascript
element = document.querySelector(selectors);
```

- `element` 는 요소의 객체 값이다.
- `selectors`는 콤마로 구분된 한 개 이상의 CSS 선택자들이 포함된 텍스트 값이다.

이 예제에서는 "myclass"라는 클래스를 가진 첫 번째 요소가 반환될 것이다.

``` javascript
var el = document.querySelector(".myclass");
```

### 7e) 다수의 선택자로 접근하는 방법 ([MDN Reference](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelectorAll))
document 내의 요소 중에서 다수의 선택자와 매칭이 되는 요소들이 포함된 리스트가 반환된다. (깊이 우선 전위 순회 사용) 그 반환되는 객체는 `NodeList`이다. IE8 이상 지원된다.

``` javascript
elementList = document.querySelectorAll(selectors);
```

- `elementList`은 요소 객체 중 non-live NodeList이다.
- `selectors`는 콤마로 구분된 하나 혹 하나 이상의 CSS 선택자들이 포함된 텍스트 값이다.

이 예제는 document 중 class에 "note" 혹은 "alert"를 가지고 있는 모든 div 요소를 리스트로 반환한다.

``` javascript
var matches = document.querySelectorAll("div.note, div.alert");
```

## 8) 관계
돔 요소의 관계, 다른 요소와의 관계를 활용해 요소에 접근하는 방법

### 8a) 주어진 요소의 하위 요소 ([MDN Reference](https://developer.mozilla.org/en-US/docs/Web/API/Node/childNodes))
`childNodes`은 주어진 요소의 하위 요소들을 하나의 콜랙션으로 반환한다.

``` javascript
var ndList = elementNodeReference.childNodes;
```

### 8b) 주어진 요소의 다음 형제 ([MDN Reference](https://developer.mozilla.org/en-US/docs/Web/API/Node/nextSibling))
상위 요소의 하위 요소 중에 바로 다음 노드를 반환한다. 만약 주어진 요소가 리스트의 마지막 순번이었다면 null을 반환한다.

``` javascript
nextNode = node.nextSibling
```

### 8c) 주어진 요소의 하위 요소들 ([MDN Reference](https://developer.mozilla.org/en-US/docs/Web/API/ParentNode/children))
`ParentNode.children`은 주어진 객체의 하위 요소 중에서 live HTMLCollection을 반환하는 읽기 전용 속성이다. 반환되는 값은 텍스트가 아닌 객체가 모인 집합이다. 이 노드 객체에서 데이터 값을 알아내려면, 그것들의 속성을 사용해야 한다. (예를 들어, 이름 값을 알기 위한 elementNodeReference.children[1].nodeName)

``` javascript
var elList = elementNodeReference.children;
```

### 8d) 바로 다음 특정 요소 ([MDN Reference](https://developer.mozilla.org/en-US/docs/Web/API/NonDocumentTypeChildNode/nextElementSibling))
`ChildNode.nextElementSibling`은 상위 요소의 하위 요소 중에서 특정 하나의 요소를 반환하는 읽기 전용 속성이다. 만약 요소가 마지막 순번이었다면 null을 반환한다.

``` javascript
var nextNode = elementNodeReference.nextElementSibling;
```