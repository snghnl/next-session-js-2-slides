---
layout: section
---
# 배열 메서드
자주 쓰는 배열 조작 메서드 총정리

---
layout: default
hideInToc: true
---
# splice — 만능 요소 조작

`arr.splice(index, deleteCount, ...items)`

요소 **삭제 + 추가 + 교체** 모두 가능합니다.

```js
// ① 삭제
let arr = ["I", "study", "JavaScript"];
arr.splice(1, 1);
console.log(arr); // ["I", "JavaScript"]
```

<v-click>

```js
// ② 교체
let arr = ["I", "study", "JavaScript", "right", "now"];
arr.splice(0, 3, "Let's", "dance");
console.log(arr); // ["Let's", "dance", "right", "now"]
```

</v-click>

<v-click>

```js
// ③ 삽입 (deleteCount = 0)
let arr = ["I", "study", "JavaScript"];
arr.splice(2, 0, "complex", "language");
console.log(arr); // ["I", "study", "complex", "language", "JavaScript"]
```

> `splice`는 제거된 요소를 배열로 반환합니다.

</v-click>

---
layout: two-cols
hideInToc: true
---
# slice — 배열 복사/추출

`arr.slice(start, end)` — 원본 유지, 새 배열 반환

```js
let arr = ["t", "e", "s", "t"];

arr.slice(1, 3); // ["e", "s"]
arr.slice(-2);   // ["s", "t"]
arr.slice();     // 전체 복사본
```

<v-click>

> `end` 인덱스의 요소는 포함되지 않습니다.
> 음수 인덱스 = 끝에서부터

</v-click>

::right::

<v-click>

# concat — 배열 합치기

`arr.concat(arr2, arr3, ...)` — 새 배열 반환

```js
let arr = [1, 2];

arr.concat([3, 4]);       // [1,2,3,4]
arr.concat([3, 4], [5, 6]); // [1,2,3,4,5,6]
arr.concat([3, 4], 5, 6);   // [1,2,3,4,5,6]
```

</v-click>

<v-click>

> `splice`는 원본 배열을 변경하지만,
> `slice`와 `concat`은 **새 배열을 반환**합니다.

</v-click>

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

<v-click>

| | `for...of` | `forEach` |
|---|---|---|
| 문법 | 간결 | 콜백 전달 |
| `break` | 가능 | 불가능 |
| 반환값 | — | — |
| 주 사용처 | 단순 순회 | 메서드 체이닝 |

</v-click>

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

<v-click>

| 메서드 | 반환값 | 개수 |
|---|---|---|
| `find` | 요소 (또는 `undefined`) | 첫 번째 1개 |
| `findIndex` | 인덱스 (또는 `-1`) | 첫 번째 1개 |
| `filter` | 새 배열 | 조건 만족 전부 |

</v-click>

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
# sort / reverse — 정렬과 뒤집기

**`sort()`** — 기본은 문자열 정렬 → 숫자 정렬 시 함수 필요

```js
let arr = [1, 2, 15];

arr.sort();             // [1, 15, 2] ❌ 문자열 기준 정렬!
arr.sort((a, b) => a - b); // [1, 2, 15] ✅
arr.sort((a, b) => b - a); // [15, 2, 1] (내림차순)
```

<v-click>

**`reverse()`** — 배열 뒤집기 (원본 변경)

```js
let arr = [1, 2, 3, 4, 5];
arr.reverse();
console.log(arr); // [5, 4, 3, 2, 1]
```

</v-click>

<v-click>

> `sort`와 `reverse`는 모두 **원본 배열을 변경**합니다.

</v-click>

---
layout: default
hideInToc: true
---
# split / join — 문자열 ↔ 배열

**`split(구분자)`** — 문자열 → 배열

```js
let str = "철수, 영희, 민준";
let arr = str.split(", ");
console.log(arr); // ["철수", "영희", "민준"]

// 한 글자씩 분리
"hello".split(""); // ["h", "e", "l", "l", "o"]
```

<v-click>

**`join(구분자)`** — 배열 → 문자열

```js
let arr = ["철수", "영희", "민준"];
console.log(arr.join(", ")); // 철수, 영희, 민준
console.log(arr.join(" / ")); // 철수 / 영희 / 민준
```

</v-click>

<v-click>

> `split`과 `join`은 **서로 반대 연산**입니다.

</v-click>

---
layout: default
hideInToc: true
---
# reduce — 배열을 하나의 값으로

`arr.reduce((누산기, 현재값) => ..., 초깃값)`

```js
let arr = [1, 2, 3, 4, 5];

let sum = arr.reduce((acc, cur) => acc + cur, 0);
console.log(sum); // 15
```

<v-click>

**실행 흐름**

| 호출 | `acc` | `cur` | 결과 |
|---|---|---|---|
| 1번째 | `0` | `1` | `1` |
| 2번째 | `1` | `2` | `3` |
| 3번째 | `3` | `3` | `6` |
| 4번째 | `6` | `4` | `10` |
| 5번째 | `10` | `5` | `15` |

</v-click>

<v-click>

> 빈 배열에서 초깃값 없이 호출하면 에러! 항상 초깃값을 명시하세요.

</v-click>

---
layout: default
hideInToc: true
---
# 메서드 한눈에 보기

<div class="text-sm">

| 메서드 | 용도 | 원본 변경 | 반환값 |
|---|---|---|---|
| `splice` | 삭제/삽입/교체 | ✅ | 삭제된 요소 배열 |
| `slice` | 범위 복사 | ❌ | 새 배열 |
| `concat` | 배열 합치기 | ❌ | 새 배열 |
| `forEach` | 순회 | ❌ | `undefined` |
| `find` | 조건 첫 요소 탐색 | ❌ | 요소 / `undefined` |
| `filter` | 조건 전체 탐색 | ❌ | 새 배열 |
| `map` | 요소 변환 | ❌ | 새 배열 |
| `sort` | 정렬 | ✅ | 정렬된 배열 |
| `reverse` | 뒤집기 | ✅ | 뒤집힌 배열 |
| `reduce` | 누산 → 단일값 | ❌ | 최종 누산값 |
| `split` | 문자열→배열 | — | 새 배열 |
| `join` | 배열→문자열 | ❌ | 문자열 |

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
# Practice 1 — splice / slice / concat

```js{monaco-run} {autorun:false}
let fruits = ["사과", "바나나", "오렌지", "포도", "딸기"];

// ① splice: "오렌지"를 "망고"로 교체하세요
// (결과: ["사과", "바나나", "망고", "포도", "딸기"])

// ② slice: 인덱스 1~3 요소를 새 배열로 추출하세요 (3 미포함)
// (결과: ["바나나", "망고"])

// ③ concat: fruits에 ["수박", "참외"]를 합친 새 배열을 만드세요

console.log(fruits);   // splice 결과
// let sliced = ...
// let combined = ...
console.log(sliced);
console.log(combined);
```

---
layout: default
hideInToc: true
---
# Practice 2 — map / filter / find

```js{monaco-run} {autorun:false}
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

---
layout: default
hideInToc: true
---
# Practice 3 — sort / reduce

```js{monaco-run} {autorun:false}
let scores = [88, 45, 92, 61, 77, 33, 95, 50];

// ① sort: 오름차순으로 정렬하세요
// 결과: [33, 45, 50, 61, 77, 88, 92, 95]

// ② reduce: 전체 점수의 합계를 구하세요

// ③ reduce: 평균 점수를 구하세요 (힌트: 합계 / 개수)

// scores.sort(...)
// let total = scores.reduce(...)
// let average = ...

console.log(scores);   // 정렬된 배열
console.log(total);    // 합계
console.log(average);  // 평균
```

---
layout: default
hideInToc: true
---
# Practice 4 — split / join / 메서드 체이닝

```js{monaco-run} {autorun:false}
let csv = "철수,85,영희,92,민준,73";

// ① split으로 csv를 배열로 변환하세요

// ② 변환된 배열에서 이름만(짝수 인덱스) 추출해 새 배열을 만드세요
// 힌트: filter((_, index) => index % 2 === 0)

// ③ 이름 배열을 " / "로 join해서 하나의 문자열로 만드세요
// 결과: "철수 / 영희 / 민준"

// let arr = csv.split(...)
// let names = arr.filter(...)
// let result = names.join(...)

console.log(result); // 철수 / 영희 / 민준
```

---
