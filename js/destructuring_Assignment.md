## 구조 분해 할당

---

`구조 분해 할당(Destructuring Assignment)`은 JavaScript에서 배열이나 객체의 속성을 분해하여 변수에 쉽게 할당할 수 있는 문법이다.

#### 배열 구조 분해 할당

```js
// 배열 구조 분해 할당 예제
const numbers = [1, 2, 3, 4];

// 기존 방식
const first = numbers[0];
const second = numbers[1];

console.log(first, second); // 출력: 1 2

// 구조 분해 할당 방식
const [one, two, three, four] = numbers;

console.log(one, two, three, four); // 출력: 1 2 3 4

// 기본값 할당
const [a = 10, b = 5] = [];

console.log(a, b); // 출력: 10 5

const [a = 10, b = 5] = [1];

console.log(a, b); // 출력: 1 5
```

`배열의 일부 요소만 할당 할 수도 있다.`

```js
const [one, , three] = numbers; // 빈칸으로 두고 싶은 곳은 , ,로 표기

console.log(one, three); // 출력: 1 3
```

---

#### 객체 구조 분해 할당

```js
// 객체 구조 분해 할당 예제
const person = {
  name: "John",
  age: 30,
  city: "New York",
};

// 기존 방식
const name = person.name;
const age = person.age;

console.log(name, age); // 출력: John 30

// 구조 분해 할당 방식
const { name, age, city } = person;
// const name = person.name 과 같은 의미
console.log(name, age, city); // 출력: John 30 New York

//기본값 할당
const { name, age, country = "USA" } = person;

console.log(name, age, country); // 출력: John 30 USA
```

`변수의 이름을 바꿀 수도 있다.`

```js
const { name: personName, age: personAge } = person;

console.log(personName, personAge); // 출력: John 30
```

이 코드는 다음과 같은 과정을 거친다

1. `person` 객체에서 `name` 속성의 값을 `personName`이라는 새로운 변수에 할당합니다.
2. `person` 객체에서 `age` 속성의 값을 `personAge`라는 새로운 변수에 할당합니다.

이렇게 하면 `personName` 변수에는 `'John'`, `personAge` 변수에는 `30`이 할당됩니다. 원래의 `person` 객체의 `name`과 `age` 속성 이름은 변경되지 않으며, 새로운 변수 이름을 사용할 수 있게 된다.

즉, `person.name`은 `'John'`이고, 이 값이 `personName`에 할당되는 것입니다. 전체 코드를 실행해보면 다음과 같은 결과를 확인할 수 있다.

#### 중첩 구조 분해 할당

```js
const person = {
  name: "John",
  age: 30,
  address: {
    city: "New York",
    zip: 10001,
  },
};

const {
  name,
  address: { city, zip },
} = person;

console.log(name, city, zip); // 출력: John New York 10001
```

---

새로운 변수뿐만 아니라 이미 선언된 변수에도 구조분해 할당이 가능하다.

```js
let a = 5;
let b = 3;
[b, a] = [a, b];
```

위 예제는 a와 b값을 서로 바꾸는 코드이다. a와 b를 [a, b] 배열로 만든 뒤에 구조 분해 할당을 해 첫 번째 요소는 b에 두 번째 요소는 a에 대입한 것이다.
