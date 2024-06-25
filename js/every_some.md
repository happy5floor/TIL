## every(), some()

---

배열에서 `모든 요소가` 조건에 해당 하는 지 판단하려면 `every()` 메서드를 사용한다.
배열에서 `하나라도` 조건에 해당 하는 지 판단하려면 `some()` 메서드를 사용한다.

```js
const arr = [1, 3, 5, 7];
arr.every((value) => value !== null); // true
```

```js
const arr = [1, 3, 5, 7];
arr.every((value) => value === null); //false
```

이 코드는 요소 1에서부터 1 === null이 false이므로 every()는 false가 되어 반복을 중단한다. 3, 5, 7은 검사할 필요가 없기 때문이다.
일반적인 반복문보다 효율적이다.

some() 메서드는 반대로 요소 중 하나라도 만족하는 지 판단한다. 인덱스 2에서 null이 있으므로 이때 some() 메서드는 true가 되고 7은 검사하지 않는다.

```js
const arr = [1, 3, null, 7];
arr.some((value) => value === null); //true
```
