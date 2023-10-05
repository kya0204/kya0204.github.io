---
title: State doesn't update while script is still running 문제 해결하기
date: 2023-09-17 20:00:00 +0900
categories:
  - JavaScript
tags:
  - 자바스크립트에러
---

## 원인과 해결방법

### 스레드 블로킹과 자바스크립트 이벤트 루프

자바스크립트는 단일 스레드 언어입니다. 단일 스레드란 하나의 작업만을 수행할 수 있는 구조를 말합니다. 따라서 긴 작업을 처리하는 동안 다른 작업들은 대기해야 합니다. 이런 현상을 '스레드 블로킹'이라고 합니다.

### 비동기 프로그래밍

이 문제의 해결책은 비동기 프로그래밍입니다. 비동기란 여러 작업이 동시에 일어나도록 하는 것입니다. 자바스크립트에서는 `setTimeout`, `Promise`, `async/await` 같은 특수한 문법을 사용하여 비동기 처리를 할 수 있습니다.

### 상태 업데이트와 비동기

React에서 상태를 업데이트할 때, 비동기적으로 처리해야 스크립트 실행 중에도 UI가 업데이트됩니다. 예를 들어 `setState` 함수 내에서 비동기 로직을 사용하면, 작업이 진행되는 동안에도 UI가 업데이트될 수 있습니다.

```javascript
const [count, setCount] = useState(0);
const heavyProcess = () => {
  // Heavy logic here
};

const handleClick = () => {
  setCount(prevCount => prevCount + 1);
  setTimeout(() => {
    heavyProcess();
  }, 0);
};
```

이 예제에서 `setTimeout`은 `heavyProcess` 함수를 비동기적으로 처리하도록 해주므로, `setCount` 함수가 상태를 업데이트할 수 있습니다.

## 정리

React와 자바스크립트에서 긴 작업을 처리할 때는 비동기 프로그래밍을 활용해야 합니다. 그렇게 하면 사용자 경험이 향상되고, 원활한 상태 업데이트가 가능합니다. `setTimeout`, `Promise`, `async/await` 등 다양한 비동기 처리 방법을 적용하여 이 문제를 해결할 수 있습니다.