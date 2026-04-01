---
layout: section
---
# 배열 메서드
자주 쓰는 배열 조작 메서드 총정리

---
layout: default
hideInToc: true
---
# forEach — 요소마다 함수 실행

`arr.forEach(fn)` — 반환값 없음, 순수 반복 용도

```js
["철수", "영희", "민준"].forEach((item, index) => {
  console.log(`${index + 1}번째: ${item}`);
});
// 1번째: 철수
// 2번째: 영희
// 3번째: 민준
```


<div text="sm">

<v-click>

| | `for...of` | `forEach` |
|---|---|---|
| 문법 | 간결 | 콜백 전달 |
| `break` | 가능 | 불가능 |
| 반환값 | — | — |
| 주 사용처 | 단순 순회 | 메서드 체이닝 |

</v-click>

</div>

---
layout: default
hideInToc: true
---
# 탐색 메서드 — indexOf / includes / find

**단순 값 탐색**

```js
let arr = [1, 0, false];

arr.indexOf(0);    // 1 (인덱스 반환, 없으면 -1)
arr.includes(1);   // true (존재 여부만 확인)
```

<v-click>

**객체 배열 탐색 — `find` / `findIndex`**

```js
let users = [
  { id: 1, name: "John" },
  { id: 2, name: "Pete" },
  { id: 3, name: "Mary" }
];

let user = users.find(item => item.id === 2);
console.log(user.name); // Pete

users.findIndex(item => item.id === 2); // 1
```

</v-click>

<v-click>

> `find`는 조건에 맞는 **첫 번째 요소**, `filter`는 **전체**를 반환합니다.

</v-click>

---
layout: default
hideInToc: true
---
# filter — 조건에 맞는 요소 모두 추출

`arr.filter(fn)` — 조건을 만족하는 요소 전체를 새 배열로 반환

```js
let users = [
  { id: 1, name: "John" },
  { id: 2, name: "Pete" },
  { id: 3, name: "Mary" }
];

let result = users.filter(user => user.id < 3);
console.log(result.length); // 2
console.log(result[0].name); // John
```

<div text="sm">

<v-click>

| 메서드 | 반환값 | 개수 |
|---|---|---|
| `find` | 요소 (또는 `undefined`) | 첫 번째 1개 |
| `findIndex` | 인덱스 (또는 `-1`) | 첫 번째 1개 |
| `filter` | 새 배열 | 조건 만족 전부 |

</v-click>

</div>

---
layout: default
hideInToc: true
---
# map — 요소를 변환해 새 배열 만들기

`arr.map(fn)` — 각 요소에 함수 적용 후 새 배열 반환

```js
let lengths = ["Bilbo", "Gandalf", "Nazgul"].map(item => item.length);
console.log(lengths); // [5, 7, 6]
```

<v-click>

```js
let users = [{ name: "철수" }, { name: "영희" }, { name: "민준" }];

let names = users.map(user => user.name);
console.log(names); // ["철수", "영희", "민준"]

let greetings = users.map(user => `안녕, ${user.name}!`);
console.log(greetings); // ["안녕, 철수!", "안녕, 영희!", "안녕, 민준!"]
```

</v-click>

<v-click>

> `forEach`는 반환값이 없고, `map`은 **새 배열을 반환**합니다.
> 배열 변환이 필요하면 항상 `map`을 사용하세요.

</v-click>

---
layout: default
hideInToc: true
---
# 메서드 한눈에 보기

<div class="text-sm">

| 메서드 | 용도 | 원본 변경 | 반환값 |
|---|---|---|---|
| `forEach` | 순회 | ❌ | `undefined` |
| `find` | 조건 첫 요소 탐색 | ❌ | 요소 / `undefined` |
| `filter` | 조건 전체 탐색 | ❌ | 새 배열 |
| `map` | 요소 변환 | ❌ | 새 배열 |

</div>

---
layout: section
hideInToc: true
---
# Practice
배열 메서드 실습

---
layout: default
hideInToc: true
---
# Practice 1 — map / filter / find

```js{monaco-run} {autorun:false, height:'220px'}
let students = [
  { name: "철수", score: 85 },
  { name: "영희", score: 92 },
  { name: "민준", score: 73 },
  { name: "지수", score: 96 },
  { name: "호진", score: 60 },
];

// ① map: 이름만 뽑은 배열을 만드세요
// 결과: ["철수", "영희", "민준", "지수", "호진"]

// ② filter: 점수가 80점 이상인 학생만 필터링하세요

// ③ find: 이름이 "민준"인 학생 객체를 찾으세요

// let names = ...
// let highScorers = ...
// let minjun = ...

console.log(names);
console.log(highScorers);
console.log(minjun);
```
