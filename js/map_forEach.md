## forEach()

---

for문을 사용하지 않고도 배열에서 제공하는 메서드로 반복문 역할을 수행할 수 있는데 대표적인 매서드로 forEach()가 있다. forEach()는 인수로 함수를 받는다.

`배열.forEach(함수);`

```js
    const arr = [1, 5, 4, 2];
    arr.forEach((number, index) => {
        console.log(number, index);
    });
    1 0
    5 1
    4 2
    2 3
```

forEach()는 인수로 받은 함수를 배열 요소에 각각 적용한다. 이때 요소 순서대로 함수를 적용하므로 반복문 역할을 하게 된다. 인수로 받은 함수의 매개변수로는 요소(number)와 요소의 인덱스(index)가 들어 있다.

(number, index) => {} 처럼 다른 매서드에 인수로 넣었을 때 실행되는 함수를 _콜백 함수(callback function)_ 라고 한다.

#### 콜백 함수의 기본 개념

---

콜백 함수는 어떤 함수에 인수로 전달되어, 그 함수가 특정 작업을 마친 후에 호출하는 함수이다. 다시 말해, 콜백 함수는 다른 함수의 실행을 "콜백"하여 호출되는 함수이다.

```js
function processUserInput(callback) {
  const name = prompt("Please enter your name.");
  callback(name);
}

function greet(name) {
  console.log("Hello " + name);
}

processUserInput(greet);
```

위 코드에서 processUserInput 함수는 callback이라는 인수를 받는다. callback 인수는 함수로 기대되며, processUserInput 함수 내부에서 callback 함수를 호출한다. 이 예제에서는 greet 함수가 processUserInput 함수에 인수로 전달되어 콜백 함수로서 호출된다.

---

## map()

---

map()은 배열 요소들을 일대일로 짝지어서 다른 값으로 변환해 `새로운 배열을 반환하는 매서드`이다.
map()도 forEach()처럼 콜백 함수를 인수로 받지만, `새로운 배열을 반환한다는 점`이 다르다.

`배열.map(<콜백 함수>);`

```js
const numbers = [];
for (let n = 1; n <= 5; n++) {
  numbers.push(n);
}
numbers; // (5) [1, 2, 3, 4, 5]
```

위 for문을 배열의 매서드만 사용해서 같은 결과를 얻을 수 있다.

```js
const numbers = Array(5)
  .fill(1)
  .map((v, i) => i + 1); // *fill() -> undefinded로 채워진다.
numbers; // (5) [1, 2, 3, 4, 5]
```

map()은 항상 새로운 배열을 반환하므로 반환한 배열을 변수에 저장해야 한다.

```js
const array = [1, 3, 5, 7];
const newArray = array.map((v, i) => {
  return v * 2;
});
console.log(array); // [1, 3, 5, 7]
console.log(newArray); // [2, 6, 10 ,14]
```

newArray 변수에는 map() 매서드의 결과물인 [2, 6, 10, 14]가 담긴다. `이때 원본 배열인 array는 수정되지 않는다.`
