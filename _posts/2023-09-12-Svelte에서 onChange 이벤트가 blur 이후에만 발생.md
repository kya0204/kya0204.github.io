---
title: Svelte에서 onChange 이벤트가 blur 이후에만 발생
date: 2023-09-12 20:00:00 +0900
categories:
  - JavaScript
tags:
  - 스벨트onChange
---

## 문제 상황: `onChange` 이벤트가 'blur' 이후에만 발생

Svelte에서 입력 요소(input element)에 `onChange` 핸들러를 사용할 때 문제가 발생할 수 있습니다. 일반적으로 이 핸들러는 사용자가 입력을 변경할 때마다 호출되어야 합니다. 그러나 Stack Overflow의 질문에서 확인할 수 있듯이, `onChange` 이벤트가 입력 요소에서 포커스(focus)를 잃은 이후('blur' 이벤트 발생 후)에만 실행됩니다.

## 원인: DOM의 `change` 이벤트와 Svelte의 `onChange` 차이

Svelte의 `onChange`는 실제 DOM의 `change` 이벤트를 기반으로 합니다. DOM에서 `change` 이벤트는 사용자가 입력 값을 변경하고, 그 입력 요소에서 포커스를 잃을 때 발생합니다. 따라서, Svelte의 `onChange`도 마찬가지로 작동하게 됩니다.

## 해결 방안: `input` 이벤트 사용

실시간으로 사용자의 입력을 추적하고 싶다면, `input` 이벤트를 사용해야 합니다. 이 이벤트는 사용자가 입력 값을 변경할 때마다 즉시 발생합니다. Svelte에서는 다음과 같이 사용할 수 있습니다.

```svelte
<script>
  let value = '';
  function handleInput(event) {
    value = event.target.value;
  }
</script>

<input type="text" on:input={handleInput} value={value} />
```

위의 코드에서 `handleInput` 함수는 사용자가 입력을 변경할 때마다 호출됩니다.

## 요약: 올바른 이벤트 핸들러 선택이 중요

입력 요소에서 실시간으로 변경을 감지하려면 `input` 이벤트를 사용하세요. 반면에 사용자가 입력을 완료하고 다른 요소로 이동할 때만 변경을 감지하려면 `onChange` 또는 DOM의 `change` 이벤트를 사용하세요. 이렇게 하면 예상대로 이벤트 핸들러가 작동할 것입니다.