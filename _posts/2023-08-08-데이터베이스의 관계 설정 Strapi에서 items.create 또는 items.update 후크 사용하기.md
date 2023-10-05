---
title: 데이터베이스의 관계 설정 Strapi에서 items.create 또는 items.update 후크 사용하기
date: 2023-08-08 20:00:00 +0900
categories:
  - JavaScript
tags:
  - Strapi
---

## 들어가기 전에

Strapi는 자바스크립트로 만든 헤드리스 CMS(Content Management System)입니다. CMS는 웹 사이트의 내용을 쉽게 관리할 수 있도록 도와주는 도구입니다. 후크(hook)는 어떤 이벤트가 발생했을 때 자동으로 실행되는 코드의 한 부분입니다. 이 글에서는 Strapi의 `items.create` 또는 `items.update` 후크를 사용하여 데이터베이스의 관계를 설정하는 방법을 상세하게 알아보겠습니다.

## 오류 메시지 해결: `ValidationError`

많은 개발자들이 StackOverflow에 질문을 올려 Strapi의 `items.create` 또는 `items.update` 후크에서 `ValidationError` 오류에 대한 해결책을 찾고 있습니다. `ValidationError`는 유효하지 않은 데이터가 입력될 때 나타나는 오류 메시지입니다.

## 관계 설정의 중요성

데이터베이스에서의 관계 설정은 중요한 작업 중 하나입니다. 이 작업을 통해 데이터 간의 연관성을 명확하게 할 수 있고, 이를 통해 효율적인 데이터 관리와 빠른 검색이 가능해집니다.

## 후크를 사용한 관계 설정 방법

1. **후크 파일 찾기**: Strapi의 `api` 폴더 내에서 관련된 모델의 `config` 폴더를 찾아 들어갑니다.
  
2. **후크 코드 작성**: `lifecycles` 객체 내에 `afterCreate` 또는 `afterUpdate` 메서드를 작성합니다. 여기서 실제로 관계를 설정하는 로직을 넣습니다.

    ```javascript
    module.exports = {
      lifecycles: {
        async afterCreate(data) {
          // 관계 설정 로직
        },
        async afterUpdate(data) {
          // 관계 설정 로직
        },
      },
    };
    ```

3. **유효성 검사**: 데이터가 올바른 형식과 값을 가지고 있는지 확인합니다. 만약 데이터가 유효하지 않다면, `ValidationError`가 발생할 것입니다.

4. **테스트**: 변경사항을 저장한 뒤 Strapi를 재시작하고, 데이터를 생성하거나 업데이트하여 관계가 제대로 설정되었는지 확인합니다.

## 마무리

Strapi에서의 `items.create` 또는 `items.update` 후크를 통한 데이터베이스 관계 설정은 복잡한 데이터 관리를 간단하게 해결할 수 있습니다. 이 방법을 통해 `ValidationError` 같은 오류 메시지를 효과적으로 해결할 수 있습니다. 이제 여러분도 Strapi를 더 효율적으로 사용할 수 있을 것입니다.