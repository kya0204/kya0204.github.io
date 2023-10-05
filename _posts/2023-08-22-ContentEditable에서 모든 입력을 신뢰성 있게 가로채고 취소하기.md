---
title: ContentEditable에서 모든 입력을 신뢰성 있게 가로채고 취소하기
date: 2023-08-22 20:00:00 +0900
categories:
  - JavaScript
tags:
  - ContentEditable
---

## 문제 상황 파악

StackOverflow에서 나온 문제는 `contenteditable` 속성이 있는 HTML 요소에서 사용자의 모든 입력을 가로채고 취소하는 방법에 관한 것입니다. 이 문제는 웹 개발에서 종종 발생하는 상황 중 하나로, 특별한 처리나 유효성 검사를 해야 할 경우에 매우 중요합니다.

## 이벤트 리스너와 preventDefault()를 활용한 해결 방법

HTML에서 `contenteditable` 속성을 가진 요소에 특정 이벤트가 발생했을 때 그것을 가로채는 가장 기본적인 방법은 자바스크립트의 이벤트 리스너를 사용하는 것입니다. 여기서 `preventDefault()` 메서드는 이벤트의 기본 동작을 취소하는 역할을 합니다.

```javascript
document.querySelector('[contenteditable]').addEventListener('keydown', function(event) {
  event.preventDefault();
});
```

이 코드는 `keydown` 이벤트를 가로채고, 그 이벤트의 기본 동작을 취소합니다. 이로써 `contenteditable` 속성이 있는 요소에 어떠한 키를 눌러도 입력이 되지 않게 됩니다.

## 주의사항과 한계

그러나 위의 코드는 모든 입력을 무조건 취소하므로, 특정 조건 하에서만 입력을 취소하려면 추가적인 로직이 필요합니다. 예를 들어, 특정 키(예: 엔터 키)에 대해서만 동작을 취소하려면 `event.keyCode` 값을 검사해야 합니다.

또한 이 방법은 단순히 키 입력만을 대상으로 하기 때문에, 마우스로 텍스트를 드래그 앤 드롭하는 경우 등은 처리하지 못합니다. 이러한 경우에는 다른 이벤트 리스너를 추가로 등록해야 합니다.

## 결론

`contenteditable`에서 모든 입력을 가로채고 취소하기 위해서는 자바스크립트의 이벤트 리스너와 `preventDefault()` 메서드를 활용할 수 있습니다. 그러나 이 방법은 특정 조건이나 다른 입력 방법에 대한 처리가 추가로 필요할 수 있으므로, 구체적인 요구사항에 맞게 코드를 수정해야 합니다.