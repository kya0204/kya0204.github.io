---
title: 자바스크립트에서 display none과 display block 사이의 전환 효과 추가하기
date: 2023-08-18 20:00:00 +0900
categories:
  - JavaScript
tags:
  - 자바스크립트전환효과
---

## 문제 상황

자바스크립트에서 웹 페이지의 특정 요소를 보이거나 숨기는 작업은 흔한 일입니다. 이럴 때 `display: none`과 `display: block` 스타일을 자주 사용합니다. 그런데 이 두 스타일 사이에 부드러운 전환 효과를 주고 싶을 때가 있습니다. 이 문제에 대해 자세히 알아봅시다.

## `display:none`과 `display:block`의 기능

`display: none`은 웹 페이지의 특정 요소를 완전히 숨깁니다. 요소가 페이지에서 사라집니다. 반대로 `display: block`은 요소를 화면에 나타나게 합니다. 하지만 이 두 스타일은 전환 효과를 지원하지 않아서, 바로 사라지거나 나타나게 됩니다.

## CSS `transition`을 사용한 해결법

`display` 속성 자체에는 전환 효과를 적용할 수 없습니다. 그래서 다른 방법을 사용해야 합니다. CSS의 `transition` 속성을 이용해서 `opacity`를 조절하면 부드러운 전환 효과를 만들 수 있습니다. 

예를 들어, 자바스크립트 코드는 다음과 같을 수 있습니다.

```javascript
function toggleElement(id) {
  const element = document.getElementById(id);
  element.classList.toggle('hidden');
}
```

CSS 코드는 다음과 같습니다.

```css
.hidden {
  opacity: 0;
  transition: opacity 0.5s ease-out;
}
```

이렇게 하면 `hidden` 클래스가 추가되거나 제거될 때, `opacity` 값이 0에서 1 또는 1에서 0으로 부드럽게 변경됩니다. 이를 통해 `display:none`과 `display:block` 사이에 전환 효과를 추가할 수 있습니다.

## `visibility` 속성을 활용한 또 다른 방법

`visibility: hidden`과 `visibility: visible` 속성도 전환 효과를 추가하는 데 사용할 수 있습니다. `visibility` 속성은 `transition`과 함께 사용할 수 있으므로, 이를 활용할 수 있습니다.

## 결론

`display:none`과 `display:block` 사이에 전환 효과를 추가하려면 `opacity` 또는 `visibility` 속성을 조절하면 됩니다. 이 방법을 통해 사용자 경험을 향상시킬 수 있습니다. 이러한 작업은 웹 페이지의 동적인 요소를 더 자연스럽게 보이게 하고, 사용자의 관심을 끌 수 있습니다.