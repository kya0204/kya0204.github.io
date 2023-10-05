---
title: Sequelize에서 ID와 동일한 기본값 설정하기
date: 2023-09-20 20:00:00 +0900
categories:
  - JavaScript
tags:
  - Sequelize
---

## 문제 개요

Node.js의 Sequelize 라이브러리를 사용하면서 테이블의 특정 열에 대해 기본값을 설정하려는 경우가 있습니다. 특히 해당 열의 기본값을 동적으로 생성된 ID와 동일하게 하려는 상황에 직면할 수 있습니다. 이 문제에는 몇 가지 해결 방법이 있으며, 그 중 가장 효과적인 방법을 소개하겠습니다.

## 해결책 1: `beforeCreate` 훅 사용하기

`beforeCreate`는 모델 인스턴스가 데이터베이스에 저장되기 전에 실행되는 함수입니다. 이 훅을 사용하면 새로 생성되는 레코드의 ID를 얻어 해당 레코드의 다른 열에 할당할 수 있습니다.

```javascript
const Model = sequelize.define('Model', {
  id: {
    type: Sequelize.INTEGER,
    primaryKey: true,
    autoIncrement: true
  },
  anotherColumn: {
    type: Sequelize.INTEGER,
    defaultValue: null
  }
});

Model.beforeCreate((instance, options) => {
  instance.anotherColumn = instance.id;
});
```

## 해결책 2: 데이터베이스 트리거 사용하기

데이터베이스 트리거는 특정 이벤트가 발생했을 때 자동으로 실행되는 함수입니다. 예를 들어, 새 레코드가 생성될 때 해당 레코드의 ID를 가져와 다른 열에 할당할 수 있습니다.

```sql
CREATE TRIGGER set_another_column
AFTER INSERT ON Model
FOR EACH ROW
BEGIN
  UPDATE Model SET anotherColumn = NEW.id WHERE id = NEW.id;
END;
```

## 정리

`beforeCreate` 훅과 데이터베이스 트리거 두 가지 방법 모두 장단점이 있습니다. `beforeCreate` 훅은 코드 상에서 간편하게 구현할 수 있으나, 복잡한 로직이 필요한 경우에는 데이터베이스 트리거가 더 효율적일 수 있습니다. 어떤 방법을 선택할지는 프로젝트의 요구사항과 개발 환경에 따라 달라질 수 있으니, 상황에 맞게 선택하는 것이 중요합니다.