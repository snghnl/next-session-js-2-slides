---
layout: section
---
# 배열 (Array)
순서가 있는 데이터를 저장하는 자료구조

---
layout: default
hideInToc: true
---
# 배열이란?

객체는 순서를 고려하지 않는 자료구조입니다.
**순서가 있는 컬렉션**이 필요할 때 → **배열** 사용!

```js
// 빈 배열 만들기
let arr = [];

// 초기값 포함
let fruits = ["사과", "오렌지", "자두"];
```

<v-click>

**인덱스로 접근** (0부터 시작)

```js
alert( fruits[0] ); // 사과
alert( fruits[1] ); // 오렌지
alert( fruits[2] ); // 자두

alert( fruits.length ); // 3
```

</v-click>

<v-click>

> 배열 요소의 자료형엔 제약이 없습니다. 숫자, 문자열, 객체, 함수 모두 가능!

</v-click>

---
layout: two-cols
hideInToc: true
---
# push / pop — 배열 끝

**`push`** — 끝에 요소 추가

```js
let fruits = ["사과", "오렌지"];

fruits.push("배");

alert( fruits );
// 사과,오렌지,배
```

<v-click>

**`pop`** — 끝 요소 제거 & 반환

```js
let fruits = ["사과", "오렌지", "배"];

alert( fruits.pop() ); // 배
alert( fruits );       // 사과,오렌지
```

</v-click>

::right::

<v-click>

# shift / unshift — 배열 앞

**`unshift`** — 앞에 요소 추가

```js
let fruits = ["오렌지", "배"];

fruits.unshift("사과");

alert( fruits );
// 사과,오렌지,배
```

</v-click>

<v-click>

**`shift`** — 앞 요소 제거 & 반환

```js
let fruits = ["사과", "오렌지", "배"];

alert( fruits.shift() ); // 사과
alert( fruits );          // 오렌지,배
```

</v-click>

---
layout: default
hideInToc: true
---
# 성능 차이 — push/pop vs shift/unshift

| 메서드 | 위치 | 속도 | 이유 |
|---|---|---|---|
| `push` / `pop` | 끝 | **빠름** | 인덱스 변경 없음 |
| `shift` / `unshift` | 앞 | **느림** | 모든 요소 인덱스 재정렬 |

<v-click>

**`shift` 내부 동작 (느린 이유)**

```
["사과", "오렌지", "배"]
   0       1        2

shift() 실행 후:
① 인덱스 0 제거
② 나머지 전부 한 칸씩 앞으로 이동 (1→0, 2→1)
③ length 갱신
```

</v-click>

<v-click>

> 배열의 앞을 자주 다뤄야 한다면 `shift`/`unshift`보다 다른 자료구조를 검토해보세요.

</v-click>

---
layout: default
hideInToc: true
---
# 배열 반복문

**① `for` (인덱스 순회)**

```js
let arr = ["사과", "오렌지", "배"];

for (let i = 0; i < arr.length; i++) {
  alert( arr[i] );
}
```

<v-click>

**② `for...of` (값 순회, 권장)**

```js
let fruits = ["사과", "오렌지", "자두"];

for (let fruit of fruits) {
  alert( fruit );
}
```

</v-click>

<v-click>

**③ `for...in` (배열에 사용 금지 ❌)**

```js
// 숫자가 아닌 키도 순회하고, 10~100배 느림
for (let key in arr) { ... }
```

> 배열에는 반드시 `for` 또는 `for...of`를 사용하세요.

</v-click>

---
layout: default
hideInToc: true
---
# `length` 프로퍼티

`length` = 가장 큰 인덱스 + 1 (요소 개수가 아님!)

```js
let fruits = [];
fruits[123] = "사과";

alert( fruits.length ); // 124 (요소는 1개지만!)
```

<v-click>

**`length`는 쓰기도 가능합니다**

```js
let arr = [1, 2, 3, 4, 5];

arr.length = 2;  // 뒤를 잘라냄
alert( arr );    // 1,2

arr.length = 5;  // 되돌리려 해도...
alert( arr[3] ); // undefined (복구 불가!)
```

</v-click>

<v-click>

> **배열 비우기:** `arr.length = 0;`

</v-click>

---
layout: default
hideInToc: true
---
# 핵심 정리

<v-click>

- 배열 선언: `let arr = []` (대괄호 방식 권장)

</v-click>

<v-click>

- 인덱스는 **0부터** 시작, `arr[0]`으로 접근

</v-click>

<v-click>

- 끝 조작: `push()` / `pop()` → **빠름**

</v-click>

<v-click>

- 앞 조작: `unshift()` / `shift()` → **느림** (인덱스 재정렬)

</v-click>

<v-click>

- 반복: `for` 또는 `for...of` 사용, `for...in`은 배열에 금지

</v-click>

<v-click>

- `length`를 줄이면 배열이 잘리고 **복구 불가**

</v-click>

---
layout: section
hideInToc: true
---
# Practice
배열 실습

---
layout: default
hideInToc: true
---
# Practice 1 — 배열 기본 조작

아래 코드를 완성해보세요.

```js{monaco-run} {autorun:false}
let stack = [];

// ① "첫번째", "두번째", "세번째"를 순서대로 push 하세요
// ② 마지막 요소를 pop해서 변수 last에 저장하세요
// ③ 앞에 "제로"를 unshift로 추가하세요

let last; // pop 결과를 저장

console.log(last);   // 세번째
console.log(stack);  // ["제로", "첫번째", "두번째"]
console.log(stack.length); // 3
```

---
layout: default
hideInToc: true
---
# Practice 2 — `for...of`로 배열 처리

과일 배열을 순회하며 각 요소를 가공해보세요.

```js{monaco-run} {autorun:false}
let fruits = ["사과", "오렌지", "바나나", "포도", "딸기"];

// ① for...of를 사용해 모든 과일을 "🍎 사과" 형식으로 출력하세요
// (앞에 이모지 대신 인덱스 번호를 써도 됩니다: "1. 사과")

// ② "바나나"가 포함되어 있는지 확인하고 있으면 "있음!", 없으면 "없음"을 출력하세요

// 예상 출력:
// 1. 사과
// 2. 오렌지
// 3. 바나나
// 4. 포도
// 5. 딸기
// 바나나: 있음!
```

---
layout: default
hideInToc: true
---
# Practice 3 — 배열로 스택 구현하기

`push` / `pop`을 사용해 간단한 "실행 취소(Undo)" 기능을 구현해보세요.

```js{monaco-run} {autorun:false}
let history = []; // 작업 이력 스택

function doAction(action) {
  // action을 history에 추가하세요
}

function undo() {
  // 마지막 작업을 history에서 꺼내 반환하세요
  // history가 비어있으면 "취소할 작업 없음"을 반환하세요
}

doAction("글자 입력: 안");
doAction("글자 입력: 녕");
doAction("글자 입력: 하");

console.log(undo()); // 글자 입력: 하
console.log(undo()); // 글자 입력: 녕
console.log(undo()); // 글자 입력: 안
console.log(undo()); // 취소할 작업 없음
```

---
