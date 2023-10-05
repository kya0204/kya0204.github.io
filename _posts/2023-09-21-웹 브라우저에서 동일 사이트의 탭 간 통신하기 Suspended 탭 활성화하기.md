---
title: 웹 브라우저에서 동일 사이트의 탭 간 통신하기 Suspended 탭 활성화하기
date: 2023-09-21 20:00:00 +0900
categories:
  - JavaScript
tags:
  - Suspended탭
---

## 문제 상황: Suspended 상태의 탭 활성화하기

웹 브라우저에서 여러 탭을 열어 사용할 때, 일부 탭은 활성 상태가 아니면 'Suspended'(일시 중지) 상태로 전환됩니다. 이런 상황에서 한 탭이 다른 탭을 '깨워야' 할 필요가 있을 수 있습니다. 예를 들어, 동일한 웹사이트에 있는 두 탭이 있고, 하나의 탭에서 발생한 이벤트가 다른 탭에도 반영되어야 한다면 어떻게 해야 할까요? 이 문제에 대한 해결책을 탐구해 봅시다.

## 원리 이해하기: 브라우저의 탭 관리

웹 브라우저는 시스템 자원을 효율적으로 사용하기 위해 비활성 탭을 'Suspended' 상태로 만듭니다. 이 상태는 탭이 사용자에게 보이지 않을 때나, 사용자가 탭을 일정 시간 동안 사용하지 않았을 때 자동으로 발생합니다.

## 기술적 해결방안: Web Workers와 Local Storage 이용하기

### Web Workers

'Web Workers'는 백그라운드에서 실행되는 스크립트로, 메인 스레드와는 독립적으로 작동합니다. 이를 활용하여 다른 탭과 정보를 주고받을 수 있습니다.

### Local Storage

'Local Storage'는 웹 브라우저에서 제공하는 데이터 저장 공간입니다. 이를 이용하여 한 탭이 다른 탭에게 신호를 보낼 수 있습니다.

### 코드 예시: `BroadcastChannel` API

이 문제를 해결하는 한 가지 방법은 `BroadcastChannel` API를 사용하는 것입니다. `BroadcastChannel`을 사용하면 동일 출처(Origin)에 있는 다른 탭과 메시지를 주고받을 수 있습니다.

```javascript
// 채널 생성
const channel = new BroadcastChannel('wakeUpChannel');

// 메시지 받기
channel.onmessage = function(event) {
  if (event.data === 'wakeUp') {
    // 탭을 깨우는 로직
  }
};

// 메시지 보내기
channel.postMessage('wakeUp');
```

## 정리: Suspended 탭도 안심하고 사용하세요!

웹 브라우저의 탭 관리 기능은 사용자에게 편의를 제공하면서도, 때로는 원치 않는 동작을 유발할 수 있습니다. 그러나 이러한 문제도 적절한 기술과 코드를 활용하면 해결할 수 있습니다. 이를 통해 더 나은 사용자 경험을 제공할 수 있으므로, 활용 가능한 다양한 방법을 알아두는 것이 좋습니다.