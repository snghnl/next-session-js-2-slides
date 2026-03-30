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

<div clas="pr-4">

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

</div>

::right::

<div class="pl-4">


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

</div>

---
layout: two-cols-header
hideInToc: true
---
# 배열 반복문

::left::

<div class="pr-4">

**① `for` (인덱스 순회)**

```js
let arr = ["사과", "오렌지", "배"];

for (let i = 0; i < arr.length; i++) {
  alert( arr[i] );
}
```

**② `for...of` (값 순회, 권장)**

```js
let fruits = ["사과", "오렌지", "자두"];

for (let fruit of fruits) {
  alert( fruit );
}
```

</div>

::right::

<div class="pl-4">


**③ `for...in` (배열에 사용 금지 ❌)**

```js
// 숫자가 아닌 키도 순회하고, 10~100배 느림
for (let key in arr) { ... }
```

> 배열에는 반드시 `for` 또는 `for...of`를 사용하세요.


</div>

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

```js{monaco-run} {autorun:false, height:'220px'}
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

```js{monaco-run} {autorun:false, height:'220px'}
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
