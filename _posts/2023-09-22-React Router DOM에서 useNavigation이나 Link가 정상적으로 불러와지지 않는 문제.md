---
title: React Router DOM에서 useNavigation이나 Link가 정상적으로 불러와지지 않는 문제
date: 2023-09-22 20:00:00 +0900
categories:
  - JavaScript
tags:
  - useNavigation
---

## 문제 상황

Stackoverflow에서 많은 개발자들이 `React Router DOM` 라이브러리에서 `useNavigation`이나 `Link` 컴포넌트를 정상적으로 불러오지 못하는 문제에 대해 얘기하고 있습니다. 이 문제로 인해 애플리케이션의 네비게이션이 제대로 작동하지 않거나 오류가 발생합니다.

## 오류 메시지

```ModuleNotFoundError: Can't resolve 'react-router-dom/useNavigation'```

## 해결 방법

### 패키지 버전 확인

가장 먼저 할 일은 패키지의 버전을 확인하는 것입니다. `React Router DOM`의 특정 버전에서는 `useNavigation`이 없을 수 있습니다. 패키지의 최신 버전을 사용하고 있는지 확인해 보세요.

### 올바른 Import 문법 사용

```javascript
// 잘못된 방법
import { useNavigation } from 'react-router-dom/useNavigation';
// 올바른 방법
import { useNavigation } from 'react-router-dom';
```

### 의존성 재설치

의존성 문제가 있는 경우, `node_modules` 폴더를 삭제한 다음 `npm install` 또는 `yarn install` 명령어를 실행하여 모든 패키지를 다시 설치할 수 있습니다.

### 커스텀 훅 사용

`useNavigation`이 없는 경우, 자체적인 네비게이션 로직을 구현할 수 있습니다. 예를 들어, `useHistory`와 같은 다른 훅을 사용하여 동일한 기능을 구현할 수 있습니다.

## 주의 사항

다양한 해결 방법이 있지만, 애플리케이션의 전반적인 구조와 사용하는 다른 라이브러리에 따라 가장 적합한 방법이 다를 수 있습니다. 따라서, 문제를 해결하기 위해 다양한 방법을 시도해 보는 것이 중요합니다.

## 마치며

이 문제는 여러 가지 원인과 해결 방법이 있을 수 있으므로, 가장 적합한 해결책을 찾기 위해 여러 가지를 시도해 보는 것이 좋습니다. 문제의 원인을 정확히 파악하고 적절한 방법으로 해결하면, 애플리케이션의 네비게이션 기능을 원활하게 사용할 수 있습니다.