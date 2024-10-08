### 7~8강에서 다룰만한 것들

#### classList

---

`태그.classList.contains("클래스");`
해당 클래스가 들어 있다면 true, 들어있지 않다면 false 가 반환된다.

```js
태그.classList.add("클래스"); // 추가가
태그.classList.replace("기존클래스", "수정클래스"); // 수정
태그.classList.remove("클래스"); //제거
```

#### reduce

---

```js
    배열.reduce((누적값, 현재값) => {
        return 새로운누적값;
    }, 초기값);`
```

초기값이 없으면 배열의 첫 번째 요소가 초기값이 된다.

```js
    const sum = [1, 2, 3, 4, 5].reduce((a, c) => {
        return a + c
    }, 0);

    <계산표>
    // a(누적값): 0 c(현재값): 1 a+c(반환값): 1
    // a(누적값): 1 c(현재값): 2 a+c(반환값): 3
    // a(누적값): 3 c(현재값): 3 a+c(반환값): 6
    // a(누적값): 6 c(현재값): 4 a+c(반환값): 10
    // a(누적값): 10 c(현재값): 5 a+c(반환값): 15
    console.log(sum);
    15
```

초기값 X

```js
    const sum = [1, 2, 3, 4, 5].reduce((a, c) => {
        return a + c
    });

    <계산표>
    // a(누적값): 1 c(현재값): 2 a+c(반환값): 3
    // a(누적값): 3 c(현재값): 3 a+c(반환값): 6
    // a(누적값): 6 c(현재값): 4 a+c(반환값): 10
    // a(누적값): 10 c(현재값): 5 a+c(반환값): 15
    console.log(sum);
    15
```

객체를 만들 수도 있다.

```js
[1, 2, 3, 4, 5].reduce((a, c) => {
  a[c] = c * 10;
  return a;
}, {});
```

| 단계 | 누산기(a)                      | 현재 요소(c) | 수행 작업      | 결과 누산기(a)                        |
| ---- | ------------------------------ | ------------ | -------------- | ------------------------------------- |
| 1    | {}                             | 1            | a[1] = 1 \* 10 | { 1: 10 }                             |
| 2    | { 1: 10 }                      | 2            | a[2] = 2 \* 10 | { 1: 10, 2: 20 }                      |
| 3    | { 1: 10, 2: 20 }               | 3            | a[3] = 3 \* 10 | { 1: 10, 2: 20, 3: 30 }               |
| 4    | { 1: 10, 2: 20, 3: 30 }        | 4            | a[4] = 4 \* 10 | { 1: 10, 2: 20, 3: 30, 4: 40 }        |
| 5    | { 1: 10, 2: 20, 3: 30, 4: 40 } | 5            | a[5] = 5 \* 10 | { 1: 10, 2: 20, 3: 30, 4: 40, 5: 50 } |

1. 초기 배열: [1, 2, 3, 4, 5]이라는 배열이 있다.
2. reduce 함수: 이 배열에 대해 reduce 메서드를 사용한다. reduce 메서드는 배열의 각 요소에 대해 콜백 함수를 실행하여 단일 결과값을 생성한다.
3. 콜백 함수의 매개변수:
   - a: 누산기(accumulator). 이전 콜백 함수 호출에서 반환된 값이 전달됩니다. 여기서는 객체를 누산기로 사용합니다.
   - c: 현재 배열 요소(current element)입니다.
4. 콜백 함수의 내용:
   - a[c] = c _ 10;: 객체 a의 키 c에 값 c _ 10을 할당합니다. 예를 들어, 배열의 첫 번째 요소 1에 대해 a[1] = 1 \* 10;이 됩니다.
   - return a;: 수정된 객체 a를 반환하여 다음 콜백 함수 호출에 사용합니다.
5. 초기값: {}. 빈 객체가 초기값으로 제공됩니다. 이 객체가 누산기로 사용됩니다.
