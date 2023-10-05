---
title: TypeScript와 Webpack 환경에서 ES5 기반 레거시 자바스크립트 라이브러리 임포트 문제 해결하기
date: 2023-09-09 20:00:00 +0900
categories:
  - JavaScript
tags:
  - 타입스크립트임포트
---

## 문제 상황: `Cannot find name 'MyLibrary'`

웹 개발을 하다 보면 새로운 기술과 오래된 기술을 함께 사용해야 하는 경우가 많습니다. TypeScript와 Webpack을 사용하면서 ES5(ECMAScript 5) 기반의 레거시(오래된) 자바스크립트 라이브러리를 임포트하는 데 문제가 발생했다고 가정해봅시다. 그럴 때 나타나는 에러 메시지는 대체로 `Cannot find name 'MyLibrary'` 와 같은 형태입니다.

## 기초 개념 이해하기: TypeScript, Webpack, ES5

- **TypeScript**: 자바스크립트에 타입을 추가한 언어로, 코드의 안정성을 높입니다.
- **Webpack**: 여러 개의 파일과 의존성을 하나의 번들로 만들어주는 모듈 번들러입니다.
- **ES5**: ECMAScript의 5번째 버전으로, 오래된 자바스크립트 코드가 이 기준에 많이 부합합니다.

## 해결 방법 1: `declare` 키워드 사용하기

`declare` 키워드를 사용하면 TypeScript에게 해당 변수가 전역 범위에 존재함을 알려줄 수 있습니다.

```typescript
declare var MyLibrary: any;
```

이렇게 하면 TypeScript는 `MyLibrary` 변수가 어디에든 존재할 수 있다고 인식하고, 에러를 던지지 않습니다.

## 해결 방법 2: 외부 모듈로 처리하기

Webpack을 사용하는 경우, 다음과 같이 `externals` 옵션을 설정하여 레거시 라이브러리를 외부 모듈로 처리할 수 있습니다.

```javascript
// webpack.config.js
module.exports = {
  externals: {
    MyLibrary: 'MyLibrary'
  }
};
```

이 설정은 Webpack에게 `MyLibrary`는 외부에서 불러올 것이라고 알려줍니다.

## 해결 방법 3: `shim` 사용하기

`shim`이라는 기술을 사용하여 레거시 코드와 현재 코드를 이어줄 수 있습니다. `shim`은 오래된 라이브러리가 현재의 모듈 시스템에 맞게 동작할 수 있도록 중간에서 조정해주는 코드 조각입니다.

```javascript
// shim.js
window.MyLibrary = require('path/to/legacy/library');
```

이 파일을 프로젝트의 진입점(entry point) 파일에서 불러오면, 레거시 라이브러리를 현재의 모듈 시스템과 호환성 있게 만들 수 있습니다.

## 마무리

TypeScript와 Webpack 환경에서 ES5 기반의 레거시 자바스크립트 라이브러리를 사용하려면 여러 가지 방법이 있습니다. `declare` 키워드 사용, `externals` 설정, 또는 `shim`을 사용하는 방법 등을 통해 이 문제를 해결할 수 있습니다. 선택한 방법에 따라 설정이 달라질 수 있으므로, 프로젝트의 요구 사항에 맞는 방법을 선택하는 것이 중요합니다.