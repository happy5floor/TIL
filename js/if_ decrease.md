## 중첩 if문 줄이기

---

if문 안에 if 문이 있는 (_중첩 if문_) 을 줄이는 방법을 알아보자.

```js
const onClickNumber = (event) => {
  if (operator) {
    if (!numTwo) {
      $result.value = "";
    }
    numTwo += event.target.textContent;
  } else {
    numOne += event.target.textContent;
  }
  $result.value += event.target.textContent;
};
```

라는 코드를 통해 예시를 들어보겠다.

## 중첩 if문은 5가지 절차를 걸쳐 줄일 수 있다.

    1. if문 다음에 나오는 공통된 절차를 각 분기점 내부에 넣는다.
    2. 분기점에서 짧은 절차부터 실행하게 if 문을 작성한다.
    3. 짧은 절차가 끝나면 return 문(함수 내부일 때)이나 break 문(for 문 내부일 때)으로 중단한다.
    4. else 문을 제거한다(이때 중첩 하나가 제거된다.)
    5. 다음 중첩된 분기점이 나오면 1~4의 과정을 반복한다.

---

첫번째, onClickNumber() 함수에서 if문과 상관없이 공통적으로 실행되는 부분은 $result.value += event.target.textContent; 이다. 이 부분을 각 분긱점 안에 넣는다.

```js
const onClickNumber = (event) => {
  if (operator) {
    if (!numTwo) {
      $result.value = "";
    }
    numTwo += event.target.textContent;
    `$result.value += event.target.textContent;`;
  } else {
    numOne += event.target.textContent;
    `$result.value += event.target.textContent;`;
  }
};
```

두번째, 분기점에서 어떤 절차가 더 짧은 지 확인한다. opeator에 저장된 값이 없을 때 절차가 더 짧으니 먼저 작성. 이때 조건은 operator에서 !operator로 바뀐다.

```js
const onClickNumber = (event) => {
  if (`!operator`) {
    numOne += event.target.textContent;
    $result.value += event.target.textContent;
  } else {
    if (!numTwo) {
      $result.value = "";
    }
    numTwo += event.target.textContent;
    $result.value += event.target.textContent;
  }
};
```

세번째, 짧은 절차 즉, !operator일 때의 절차가 마무리되면 return문으로 함수를 종료한다.
네번째, return 문 아랫부분은 무조건 operator일 때만 실행되므로 else 문으로 감쌀 필요가 없다.

```js
const onClickNumber = (event) => {
  if (!operator) {
    numOne += event.target.textContent;
    $result.value += event.target.textContent;
    `return;`;
  }
  //이하 코드는 operator에 값이 저장되어 있는 경우에만 실행됨
  if (!numTwo) {
    $result.value = "";
  }
  numTwo += event.target.textContent;
  $result.value += event.target.textContent;
};
```

---

연습용 예제

```js
function test() {
  let result = "";
  if (a) {
    if (!b) {
      result = "C";
    }
  } else {
    result = "a";
  }
  result += "b";
  return result;
}
```

답안

```js
function test() {
  let result = "";
  if (!a) {
    result = "a";
    result += "b";
    return result;
  }
  if (!b) {
    result = "C";
  }
  result += "b";
  return result;
}
```

심화 - else문이 없는 if 문은 else{} 있다고 생각하고 해보기

```js
function test() {
  let result = "";
  if (!a) {
    result = "a";
    result += "b";
    return result;
  }
  if (!b) {
    result = "C";
  } else {
  }
  result += "b";
  return result;
}
```

답안

```js
function test() {
  let result = "";
  if (!a) {
    result = "a";
    result += "b";
    return result;
  }
  if (b) {
    result += "b";
    return result;
  }
  result = "C";
  result += "b";
  return result;
}
```
