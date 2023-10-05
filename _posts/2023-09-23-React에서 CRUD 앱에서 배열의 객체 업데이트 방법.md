---
title: React에서 CRUD 앱에서 배열의 객체 업데이트 방법
date: 2023-09-23 20:00:00 +0900
categories:
  - JavaScript
tags:
  - 리액트CRUD
---

## Array Method를 사용한 객체 업데이트 방법

React에서 CRUD(Create, Read, Update, Delete) 앱을 개발하다 보면, 배열 안에 있는 객체를 업데이트해야 할 상황이 자주 발생합니다. 이러한 작업을 어떻게 효율적으로 할 수 있는지에 대한 여러 가지 방법이 있습니다. 배열 메소드를 사용하는 것은 그 중 하나입니다. 배열 메소드란 배열을 다루는데 도움을 주는 함수들을 말합니다.

### `map` 함수를 이용한 업데이트

`map` 함수는 배열의 모든 요소에 함수를 적용한 후 새로운 배열을 반환합니다. 예를 들어, 특정 조건에 맞는 객체만 업데이트하고 싶을 때 `map` 함수를 사용할 수 있습니다.

```javascript
const updateObjectInArray = (array, targetId, newValues) => {
  return array.map(obj => {
    if (obj.id === targetId) {
      return { ...obj, ...newValues };
    }
    return obj;
  });
}
```

위 코드에서 `targetId`는 업데이트할 객체의 ID입니다. `newValues`는 업데이트할 새로운 값들을 포함한 객체입니다.

### `splice` 메소드를 이용한 업데이트

`splice` 메소드는 배열의 특정 부분을 제거하거나 새로운 요소를 추가하는 메소드입니다. 이 메소드를 사용하면 원본 배열을 변경할 수 있습니다.

```javascript
const updateObjectInArray = (array, targetId, newValues) => {
  const index = array.findIndex(obj => obj.id === targetId);
  if (index > -1) {
    array.splice(index, 1, { ...array[index], ...newValues });
  }
}
```

이 방법은 원본 배열을 변경하므로 React의 불변성 원칙에 위배될 수 있습니다. 따라서 새로운 배열을 만들어서 사용하는 것이 좋습니다.

## 주의할 점: Error Name

코드 작성 시 주의해야 할 것 중 하나는 에러 이름입니다. 예를 들어, 배열의 인덱스를 찾지 못했을 경우 자주 발생하는 에러는 `TypeError`입니다.

## 결론

배열 안의 객체를 업데이트하는 방법은 여러 가지가 있습니다. 여기서 소개한 `map`과 `splice`는 그 중 두 가지 방법입니다. 상황에 따라 적절한 메소드를 선택하여 사용하면 됩니다. 이렇게 하면 React에서 CRUD 앱을 효율적으로 개발할 수 있습니다.