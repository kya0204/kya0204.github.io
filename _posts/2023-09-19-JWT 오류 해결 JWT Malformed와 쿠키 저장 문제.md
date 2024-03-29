---
title: JWT 오류 해결 JWT Malformed와 쿠키 저장 문제
date: 2023-09-19 20:00:00 +0900
categories:
  - JavaScript
tags:
  - JWT오류
---

## 오류 개요

"JWT Malformed"는 JSON Web Token(JWT)을 사용할 때 자주 발생하는 오류 중 하나입니다. 이 오류는 보통 토큰의 형식이 올바르지 않거나 토큰을 올바르게 해석할 수 없을 때 나타납니다. 본 글에서는 이 오류가 쿠키(cookie)에 JWT를 저장하려고 할 때 왜 발생하는지와 해결 방법에 대해 설명합니다.

## 쿠키와 JWT

쿠키는 웹사이트가 사용자의 브라우저에 저장하는 작은 데이터 조각입니다. JSON Web Token(JWT)는 사용자 인증 정보를 안전하게 전송하기 위한 토큰입니다. 일반적으로, JWT는 쿠키 또는 로컬 스토리지에 저장됩니다. 하지만 쿠키에 저장할 때 "JWT Malformed" 오류가 발생할 수 있습니다.

## 주요 원인

1. **잘못된 토큰 형식**: JWT는 특정 형식을 따라야 합니다. 만약 이 형식이 맞지 않다면 "JWT Malformed" 오류가 발생합니다.
2. **인코딩 문제**: JWT는 Base64로 인코딩되어야 하는데, 이 과정에서 문제가 발생할 수 있습니다.
3. **헤더 정보 오류**: 토큰의 헤더 정보가 잘못되었다면 같은 오류가 나타날 수 있습니다.

## 해결 방법

### 토큰 확인

먼저 JWT 토큰이 올바른지 확인합니다. 올바른 JWT는 세 부분으로 나뉩니다: 헤더(Header), 페이로드(Payload), 그리고 서명(Signature). 각 부분은 점(`.`)으로 구분됩니다.

### 인코딩 확인

Base64 인코딩이 올바르게 이루어졌는지 확인합니다. 잘못된 인코딩은 토큰을 잘못 해석하게 만듭니다.

### 쿠키 설정 검토

쿠키 설정에서 `HttpOnly`와 `Secure` 옵션이 올바르게 설정되어 있는지 확인합니다. 이 설정들은 쿠키가 안전하게 전송되도록 도와줍니다.

## 결론

"JWT Malformed" 오류는 주로 JWT 토큰의 형식 문제나 쿠키 설정 문제로 발생합니다. 이 문제를 해결하기 위해서는 토큰 형식을 확인하고, 인코딩 문제를 검토한 뒤, 쿠키 설정을 올바르게 조정해야 합니다. 이렇게 하면 오류 없이 JWT를 쿠키에 안전하게 저장할 수 있습니다.