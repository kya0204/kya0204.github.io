---
title: TypeScript에서 ES5 라이브러리 사용하기
date: 2023-09-15 20:00:00 +0900
categories:
  - JavaScript
tags:
  - TypeScript라이브러리
---
# TypeScript에서 ES5 라이브러리 사용하기

## 문제 개요

많은 프로젝트에서 TypeScript와 Webpack을 사용하는 경우가 증가하고 있습니다. 그러나 가끔은 이전 버전인 ES5로 작성된 라이브러리를 사용해야 할 때가 있습니다. 이럴 때 어떻게 이 라이브러리를 임포트할 수 있는지에 대한 문제를 다룹니다.

## 오류명: `TypeError: Cannot read property 'X' of undefined`

최초의 문제는 오류 메시지 `TypeError: Cannot read property 'X' of undefined`가 발생하는 것입니다. 이 오류는 ES5 라이브러리가 올바르게 로드되지 않았을 때 발생합니다.

## 해결 방법 1: Webpack 설정

Webpack을 사용하는 경우, `webpack.config.js` 파일에서 설정을 조정해야 합니다. `externals` 옵션을 사용하여 라이브러리가 전역 변수로 접근 가능하도록 설정할 수 있습니다.

```javascript
// webpack.config.js
module.exports = {
  // ...
  externals: {
    'legacy-library': 'LegacyLibrary'
  }
};
```

## 해결 방법 2: TypeScript 설정

`tsconfig.json` 파일에서 `compilerOptions` 섹션을 수정합니다. `allowJs`를 `true`로 설정하여 JavaScript 파일을 TypeScript 프로젝트에서 사용할 수 있도록 합니다.

```json
{
  "compilerOptions": {
    "allowJs": true,
    // ...
  }
}
```

## 해결 방법 3: 라이브러리 임포트

ES5 라이브러리를 임포트할 때, `require` 문법을 사용합니다. 이 방법은 CommonJS 스타일의 임포트 방식입니다.

```typescript
const legacyLibrary = require('legacy-library');
```

## 주의사항

이런 방법을 사용하면 TypeScript의 타입 체킹 기능을 완전히 활용할 수 없을 수 있습니다. 필요한 경우, DefinitelyTyped과 같은 타입 선언 라이브러리를 사용해 보세요.

## 요약

ES5 라이브러리를 TypeScript 프로젝트에 통합하는 것은 복잡할 수 있습니다. Webpack 설정, TypeScript 설정, 그리고 올바른 임포트 방법을 사용하여 이 문제를 해결할 수 있습니다. 이렇게 하면 이전에 작성된 라이브러리도 새로운 프로젝트에서 활용할 수 있습니다.