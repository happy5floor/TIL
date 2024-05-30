## 고차함수(High Order Function)

---

고차함수는 함수를 반환하는 함수, 함수를 만드는 함수를 의미한다.

예시를 통해 알아보고자 한다.

```js
const func = (msg) => {
  return () => {
    console.log(msg);
  };
};
```

func() 함수를 호출하면 함수를 반환한다.
반환된 함수를 다른 변수에 저장할 수도 있고, 변수에 저장된 함수를 다시 호출 할 수도 있다.

```js
const innerFunc1 = func("hello");
const innerFunc2 = func();
innerFunc1();
innerFunc2();
hello;
undefined;
```

---

##### 고차함수를 통해 중복 제거하기 (공부 내용 참고)

---

아래와 같이 계산기를 만드는 부분에서 숫자들의 함수들을 각자 부여했다고 쳐보자.

```js
document.querySelector("#num-0").addEventListener("click", () => {
  if (operator) {
    numTwo += "0";
  } else {
    numOne += "0";
  }
  $result.value += "0";
});
document.querySelector("#num-1").addEventListener("click", () => {
  if (operator) {
    numTwo += "1";
  } else {
    numOne += "1";
  }
  $result.value += "1";
});
```

숫자 0과 1만 해도 중복되는 코드가 생긴다. 이때 중복을 줄이기 위해 onClickNumber 라는 함수를 만들어 보자.

```js
const onClickNumber = (number) => {
  if (operator) {
    numTwo += number;
  } else {
    numOne += number;
  }
  $result.value += number;
};
```

이 함수를 통해

```js
document.querySelector("#num-1").addEventListener("click", onClickNumber("0"));
```

코드를 줄일 수 있다. 허나 이대로 실행하게 되면 우리가 원하는 값을 도출 할 수 없다.

왜그럴까 ?

함수는 항상 return undefined; 를 뱉어낸다. 그래서 onClickNumber("0")는 undefinend가 되고 우리는 원하는 값을 얻을 수 없다.

```js
const onClickNumber = (number) => {
  if (operator) {
    numTwo += number;
  } else {
    numOne += number;
  }
  $result.value += number;
  return () => {};
};
```

위는 return 값을 함수로 바꾸어 주었다 허나, 실행이 되지 않는 건 동일하다.

```js
const onClickNumber = (number) => {
  return () => {
    if (operator) {
      numTwo += number;
    } else {
      numOne += number;
    }
    $result.value += number;
  };
};
```

이 코드를 작성함으로써 우리는 원하는 값을 중복 제거와 함께 구할 수 있을 것이다.

```js
const onClickNumber = (number) => () => {
  if (operator) {
    numTwo += number;
  } else {
    numOne += number;
  }
  $result.value += number;
};
```

**_위 코드는 화살표 함수가 return과 {}가 나란하게 나올 때 제거할 수 있음을 나타낸다._**
