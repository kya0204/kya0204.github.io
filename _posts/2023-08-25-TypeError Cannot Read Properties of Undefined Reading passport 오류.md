---
title: TypeError Cannot Read Properties of Undefined Reading passport 오류
date: 2023-08-25 20:00:00 +0900
categories:
  - JavaScript
tags:
  - 자바스크립트에러
---

## 해결 방법

### 초기 설정 확인하기

먼저, 모듈이 올바르게 설치되어 있는지 확인합니다. 'passport' 모듈이 없거나 제대로 설치되지 않았을 경우, 이런 문제가 발생할 수 있습니다.

```bash
npm install passport
```

### 코드 분석하기

문제가 발생한 코드 부분을 찾아, 'undefined' 상태인 부분이 있는지 확인합니다. 예를 들어, 아래와 같은 코드에서 문제가 발생할 수 있습니다.

```javascript
app.use(session({
  secret: 'mysecret',
  resave: true,
  saveUninitialized: true
}));
app.use(passport.initialize());
app.use(passport.session());
```

### 올바른 순서로 미들웨어 설정하기

위 코드에서 볼 수 있듯이, `passport.initialize()`와 `passport.session()` 미들웨어는 `session()` 미들웨어 뒤에 위치해야 합니다. 만약 이 순서가 바뀌면 'undefined' 에러가 발생할 수 있습니다.

## 실제 적용 예시

만약 모듈 설치와 코드 분석, 그리고 미들웨어 순서까지 모두 확인했는데도 문제가 해결되지 않는다면, 'passport' 설정 파일을 다시 한 번 체크해보세요. 예를 들어, 아래와 같이 `passport.use()`를 잘못 설정한 경우도 있습니다.

```javascript
passport.use(new LocalStrategy({
  usernameField: 'email',
  passwordField: 'password'
}, function(email, password, done) {
  // 로직
}));
```

이 경우에도 'passport' 객체가 'undefined' 상태일 수 있으므로, 코드를 잘못 작성한 부분이 없는지 확인하세요.

## 결론

'TypeError: Cannot read properties of undefined reading 'passport''는 주로 초기 설정 오류나 코드의 순서 문제, 그리고 객체나 변수의 'undefined' 상태 때문에 발생합니다. 이러한 문제를 해결하기 위해서는 코드의 각 부분을 꼼꼼하게 검토해야 합니다.