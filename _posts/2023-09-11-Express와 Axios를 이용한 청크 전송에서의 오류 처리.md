---
title: Express와 Axios를 이용한 청크 전송에서의 오류 처리
date: 2023-09-11 20:00:00 +0900
categories:
  - JavaScript
tags:
  - Express
---

## 소개

청크 전송이라는 용어를 처음 들어본다면, 이것은 데이터를 '덩어리(chunk)'로 나눠 전송하는 방법입니다. Express와 Axios 라이브러리를 사용하면 이러한 청크 전송을 쉽게 구현할 수 있습니다. 그러나 청크 전송 중 오류가 발생하면 어떻게 처리해야 할까요? 이 문제에 대해 자세히 알아보겠습니다.

## 오류 형태: `Transfer-Encoding: chunked`

먼저, `Transfer-Encoding: chunked`는 HTTP 프로토콜에서 데이터를 청크 형태로 보내기 위한 메커니즘입니다. 이것을 사용하면서 오류가 발생할 수 있는 주요 사례는 다음과 같습니다.

1. 클라이언트나 서버가 청크 데이터를 잘못 구성한 경우
2. 네트워크 지연 또는 중단
3. 서버 리소스 부족

## Express에서의 오류 처리 방법

Express에서는 `res.write()`와 `res.end()` 메서드를 사용하여 청크를 보낼 수 있습니다. 만약 중간에 오류가 발생한다면, `res.status(500).send()`를 호출하여 오류를 클라이언트에게 알릴 수 있습니다.

```javascript
app.post('/chunked', (req, res) => {
  try {
    // 청크 데이터 처리
    res.write('청크1');
    res.write('청크2');
  } catch (error) {
    res.status(500).send('Internal Server Error');
  } finally {
    res.end();
  }
});
```

## Axios에서의 오류 처리 방법

Axios를 사용할 때는 `axios.post()` 등의 메서드를 이용합니다. 이 메서드는 Promise를 반환하므로, `.then()`과 `.catch()`를 사용하여 성공과 오류를 각각 처리할 수 있습니다.

```javascript
axios.post('/chunked', data)
  .then(response => {
    // 성공 시 처리
  })
  .catch(error => {
    // 오류 시 처리
  });
```

## 결론

Express와 Axios를 사용하여 청크 전송을 구현할 때, 중간에 오류가 발생하면 적절히 처리하는 것이 중요합니다. Express에서는 `res.status(500).send()`를, Axios에서는 `.catch()`를 사용하여 오류를 핸들링할 수 있습니다. 이를 통해 사용자에게 안정적인 서비스를 제공할 수 있습니다.