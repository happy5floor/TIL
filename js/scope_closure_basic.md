## 스코프

---

모든 변수는 스코프(scope, 범위)가 있다. `var`는 `함수 스코프`, `let`은 `블록 스코프`를 가진다.

```js
function b() {
    var a = 1;
}
console.log(a);

Uncaught ReferenceError: a is not defined
```

a는 함수b() 안에 선언된 변수라서 함수 바깥에서는 접근할 수 없다. `함수를 경계로 접근 가능 여부가 달라지는 것`을 함수 스코프(함수만 신경 씀)라고 한다. 함수 스코프를 다르게 말하면 `함수가 끝날 때 함수 내부의 변수도 같이 사라진다`고 할 수 있다.

```js
if(ture){
    var a= 1;
}
a;

< 1
```

var는 함수 스코프라 if문 안에 있어도 if문 바깥에서 접근 할 수 있다.

```js
if(ture){
    let a= 1;
}
a;

Uncaught ReferenceError: a is not defined
```

var과 달리 let(const 포함)은 블록스코프(블록을 신경 씀)라서 그렇다. 여기서 블록은 if문, for문, while문, 함수에서 볼 수 있는 `중괄호({})`를 의미한다. 블록 스코프를 다르게 말하면 `블록이 끝날 때 내부의 변수도 같이 사라진다`라고 볼 수 있다.

```js
for (var i=0; i<5; i++){}
i;
< 5
```

for문이 끝났을 때 i가 5가 되어 있다는 점을 주목해보자(아래에서 다시 설명). (var -> let 에러발생)

## 클로저

---

`클로저`는 간단히 말해 `외부 값에 접근하는 함수`이다.

```js
const a = 1;
const func1 = () => {
  console.log(a);
};

const func2 = (msg) => {
  return () => {
    console.log(msg);
  };
};
```

func1은 외부에 있는 변수 a를 func2는 반환값인 익명함수가 자신의 외부에 있는 msg 매개변수를 사용중 따라서, 둘 다 클로저라고 할 수 있다.

```js
const func = () => {
  console.log(a);
};
if (true) {
  const a = 1;
  func();
}
```

위에 코드는 1이 출력될 것 같지만, Uncaught ReferenceError: a is not defined 에러가 발생한다.
const는 블록 스코프이므로 if 문 바깥에서 변수 a에 접근할 수 없다. func() 함수도 if 문 바깥에 있으므로 변수 a에 접근 할 수 없다.

이처럼 함수가 선언된 위치에 따라 접근할 수 있는 값이 달라지는 현상을 "함수는 `정적 스코프를 따른다.`"라고 표현한다. 선언된 위치에 따라 접근할 수 있는 값이 달라진다면 `동적 스코프`를 따르게 되는데 `자바스크립트는 정적 스코프를 따른다.`

---

## let과 var 사용한 결과가 다른 이유

```js
const number = [1, 3, 5, 7];
for (var i = 0; i < number.length; i++) {
  `setTimeout(() => {
        console.log(number[i]);
    }, 1000 * (i + 1))`;
}
```

setTimeout()의 콜백함수(` `로 표시)는 외부 변수 i에 접근하는 `클로저`이다. 이때 1000 _ (i + 1)과 console.log(number[i])가 같은 시점에 실행된다고 착각할 수 있지만 setTimeout() 인수인 1000 _ (i + 1)은 반복문을 돌 때 실행되고, 클로저는 지정한 시간 뒤에 호출된다. 그러나 반복문은 매우 빠른 속도로 돌아 클로저가 실행 될 때는 i 는 이미 4(number.length 도 4)가 되어 있다.

<--! for 문은 동기 -> for문 안에 있는 것은 비동기이기 때문에 안에 있는 것이 실행될 때는 이미 i가 4이 되어있다. 그래서 실행 결과가 undefended 4 가 되는 것이다. (비동기 동기는 따로 다시 다루어보겠다.) -->

- i가 0일 때 setTimeout(콜백, 1000) 실행
- i가 1일 때 setTimeout(콜백, 2000) 실행
- i가 2일 때 setTimeout(콜백, 3000) 실행
- i가 3일 때 setTimeout(콜백, 4000) 실행
- i가 4일 때 4 < number.length는 false이므로 반복문 끝
- 1초 후 콜백 함수 실행 (i는 4)
- 2초 후 콜백 함수 실행 (i는 4)
- 3초 후 콜백 함수 실행 (i는 4)
- 4초 후 콜백 함수 실행 (i는 4)

따라서 클로저가 실행될 때는 `이미 i는 4가 되어` i를 출력하면 4가 되고 number의 인덱스는 3까지 밖에 없으므로 number[4]는 undefined가 된다.

`let을 사용하면 어떻게 될까?` 위 코드에서 var를 let으로 바꾸게 되면 for문에 사용한 let은 반복문을 돌 때마다 새로운 블록을 생성하고 블록별로 i 변수의 값을 고정시킨다. 이것도 블록 스코프의 특성이라고 보면 된다.

- i가 0일 때 블록0 생성, setTimeout(콜백, 1000) 실행, 블록 0의 i는 0
- i가 1일 때 블록1 생성, setTimeout(콜백, 2000) 실행, 블록 1의 i는 1
- i가 2일 때 블록2 생성, setTimeout(콜백, 3000) 실행, 블록 2의 i는 2
- i가 3일 때 블록3 생성, setTimeout(콜백, 4000) 실행, 블록 0의 i는 3
- i가 4일 때 4 < number.length는 false이므로 반복문 끝
- 1초 후 콜백 함수 실행 (블록 0의 i는 0)
- 2초 후 콜백 함수 실행 (블록 1의 i는 1)
- 3초 후 콜백 함수 실행 (블록 2의 i는 2)
- 4초 후 콜백 함수 실행 (블록 0의 i는 3)

그럼 위 코드를 `var를 사용해서는 실행 할 수 없을까?` var는 함수 스코프이므로 함수마다 값이 고정되는 것을 이용해 `클로저가 i 변수 대신 고정된 값을 가리키게 하면 된다`.

```js
const number = [1, 3, 5, 7];
function helper(j) {
  return () => {
    console.log(number[j], j);
  };
}
for (var i = 0; i < number.length; i++) {
  setTimeout(helper(i), 1000 * (i + 1));
}
```

helper() 함수는 매개변수로 j를 갖는다. `j는 i 변수의 값을 고정하는 역할`을 한다. 함수 스코프가 하나 더 생겼으므로 i의 값이 j에 저장되면서 고정되는 것이다. setTimeout()의 클로저는 이제 i 대신 j를 가르키고 있다.

- i가 0일 때 setTimeout(helper(0), 1000) 실행, 실행 j는 0
- i가 1일 때 setTimeout(helper(1), 2000) 실행, 실행 j는 1
- i가 2일 때 setTimeout(helper(2), 3000) 실행, 실행 j는 2
- i가 3일 때 setTimeout(helper(3), 4000) 실행, 실행 j는 3
- i가 4일 때 4 < number.length는 false이므로 반복문 끝
- 1초 후 콜백 함수 실행 (실행 j는 0)
- 2초 후 콜백 함수 실행 (실행 j는 1)
- 3초 후 콜백 함수 실행 (실행 j는 2)
- 4초 후 콜백 함수 실행 (실행 j는 3)

---

#### forEach()로 해결

forEach()의 콜백 함수마다 고정된 i 값을 갖고 있어서 가능한 방식.

```js
const number = [1, 3, 5, 7];
number.forEach((num, i) => {
  setTimeout(() => {
    console.log(num, i);
  }, 1000 * (i + 1));
});
```

#### switch문에서 스코프

---

```js
const type = "a";
switch (type) {
    case "a":
        let name = "손기훈";
        break;
    case "b":
        let name = "kihun";
        break;
}
Uncaught SyntaxError: Identifier 'name' has already been declared
```

같은 블록스코프 안에 같은 이름의 변수를 선언하기 때문에 에러가 발생, 블록 스코프는 현재 switch하나 밖에 없어 각자 블록 스코프를 생성해주면 해결된다.

```js
const type = "a";
switch (type) {
  case "a": {
    let name = "손기훈";
    break;
  }
  case "b": {
    let name = "kihun";
    break;
  }
}
```
