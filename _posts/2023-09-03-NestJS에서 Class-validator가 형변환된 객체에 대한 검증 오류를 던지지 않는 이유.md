---
title: NestJS에서 Class-validator가 형변환된 객체에 대한 검증 오류를 던지지 않는 이유
date: 2023-09-03 20:00:00 +0900
categories:
  - JavaScript
tags:
  - NestJS
---

## 문제 상황

질문에서는 NestJS 프레임워크에서 `class-validator`를 사용하면서 발생하는 문제에 대해 언급하고 있습니다. 특히, 원시 타입(`string`, `number` 등)이 클래스 객체로 형변환(cast)되었을 때, `class-validator`가 제대로 동작하지 않는 상황을 지적하고 있습니다.

## 원인과 해결 방법

### 원인: 형변환과 검증 메커니즘

먼저, `class-validator`는 TypeScript 또는 JavaScript 클래스에 정의된 속성에 대해 검증을 수행합니다. 그러나 형변환을 거친 객체는 검증 과정에서 원래의 유형을 잃어버리게 됩니다. 이 때문에 `class-validator`는 형변환된 객체에 대해 제대로 동작하지 않습니다.

### 해결 방법: 명시적 형 선언과 유효성 검사

이 문제를 해결하기 위한 가장 간단한 방법은 객체를 생성할 때 명시적으로 클래스 형을 선언하는 것입니다. 다음은 코드 예시입니다:

```typescript
const myObject = new MyClass({
  ...yourRawObject
});
```

이렇게 하면 `MyClass`에 정의된 검증 규칙이 적용되어, 문제가 해결될 것입니다.

## 기타 고려 사항

### 데이터 바인딩(Data Binding)

데이터 바인딩은 프론트엔드에서 백엔드로 데이터를 전송할 때 자주 사용되는 기술입니다. NestJS에서는 이를 쉽게 구현할 수 있으나, 형변환 문제가 발생할 가능성이 있으므로 주의가 필요합니다.

### Error 이름: ValidationError

`class-validator`에서 유효성 검사 실패 시 발생하는 오류의 이름은 `ValidationError`입니다. 이 오류는 검증이 실패한 필드와 실패 이유를 담고 있으므로, 디버깅에 유용합니다.

## 결론

NestJS와 `class-validator`를 사용하면서 형변환된 객체에 대한 검증 문제가 발생한다면, 객체 생성 시 명시적으로 클래스 형을 선언하여 해결할 수 있습니다. 이 방법을 통해 유효성 검사가 정확히 이루어질 것입니다.