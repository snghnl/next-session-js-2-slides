---
theme: default
background: assets/js-thumbnail.png
title: NEXT Session JavaScript 2
info: |
  Presentation slides for JavaScript 2 Session for Korea Univ NEXT 14th members

class: text-center
drawings:
  persist: false
transition: slide-left
comark: true
duration: 120min
addons:
  - slidev-addon-react
fonts:
  local: Prentendard
hideInToc: true
---

<!-- Make Blank for Image-->
<!-- turn off the dark effect on background-->

<style>
.slidev-layout {
  background-image: url('assets/js-thumbnail.png') !important;
}
</style>

---
hideInToc: true
---

# 목차

<Toc columns=2 />

---
hideInToc: true
layout: center
class: text-center
---

# 1세션 복습

지난 시간에 배운 내용을 직접 코드로 확인해 봅시다

---
hideInToc: true
---

## 1세션 핵심 요약

<div class="grid grid-cols-3 gap-3 mt-2 text-sm">

<div>

**📄 Hello, world! & 코드 구조**
- `<script>` 태그로 JS 삽입
- 문(Statement)은 `;` 으로 구분
- `//` 한 줄, `/* */` 여러 줄 주석

</div>

<div>

**📦 변수와 상수**
- `let` — 재할당 가능
- `const` — 재할당 불가
- camelCase 명명 관례

</div>

<div>

**🔢 자료형**
- `number`, `string`, `boolean`
- `null` / `undefined`
- `typeof` 로 타입 확인
- 백틱 `` ` `` 으로 `${표현식}` 삽입

</div>

<div>

**💬 alert / prompt / confirm**
- `alert` — 메시지 표시
- `prompt` — 문자열 입력 (취소 → `null`)
- `confirm` — true / false 반환

</div>

<div>

**➗ 연산자**
- `+` `-` `*` `/` `%` `**`
- `==` 느슨한 비교 vs `===` 엄격한 비교
- `+=` `++` 복합·증감 할당

</div>

<div>

**🔀 조건문**
- `if / else if / else`
- falsy: `0` `""` `null` `undefined` `NaN`
- 삼항 연산자 `조건 ? 참 : 거짓`

</div>

<div>

**⚡ 논리 연산자**
- `||` — 첫 번째 truthy 반환
- `&&` — 첫 번째 falsy 반환
- `!` — Boolean 역전 / `!!` 형 변환

</div>

<div>

**🔁 반복문**
- `for (init; cond; step)`
- `while` / `do..while`
- `break` 종료 / `continue` 건너뜀

</div>

</div>

---
hideInToc: true
---

## 복습 — Hello, world!

콘솔에 **자기 이름**과 **가장 좋아하는 프로그래밍 언어**를 각각 출력해보세요.

```js{monaco-run} {autorun:false}
// 힌트: console.log()를 두 번 사용해보세요
// 예시: "이름: 홍길동" / "좋아하는 언어: JavaScript"

```

---
hideInToc: true
---

## 복습 — 코드 구조

아래 코드에는 **세미콜론 함정**이 숨어있습니다.
코드를 실행해 에러를 확인하고, **올바르게 고쳐보세요**.

```js{monaco-run} {autorun:false}
// ⚠️ 아래 코드를 그대로 실행해보고, 에러가 왜 발생하는지 생각해보세요
// 그리고 세미콜론을 추가해 올바르게 수정해보세요
console.log("코드 구조 복습")
[1, 2, 3].forEach(n => console.log(n))
```

---
hideInToc: true
---

## 복습 — 변수와 상수

`a`와 `b` 두 변수의 값을 **서로 교환(swap)** 해보세요.
세 번째 임시 변수 `temp`를 활용하세요.

```js{monaco-run} {autorun:false}
let a = "사과";
let b = "바나나";

// 여기에 swap 코드를 작성하세요


console.log(a); // "바나나" 가 출력되어야 합니다
console.log(b); // "사과" 가 출력되어야 합니다
```

---
hideInToc: true
---

## 복습 — 자료형

아래 각 값의 `typeof` 결과를 **주석으로 먼저 예측**한 뒤, 실행해서 확인해보세요.
그리고 마지막 줄은 **템플릿 리터럴**로 완성해보세요.

```js{monaco-run} {autorun:false}
console.log(typeof 42);          // 예측: ?
console.log(typeof "hello");     // 예측: ?
console.log(typeof true);        // 예측: ?
console.log(typeof null);        // 예측: ? ← 함정!
console.log(typeof undefined);   // 예측: ?
console.log(typeof {});          // 예측: ?

// 이름과 나이 변수를 백틱으로 연결해 "저는 OO이고 나이는 OO살입니다." 출력
let name = "여러분";
let age = 20;
console.log(/* 여기를 완성하세요 */);
```

---
hideInToc: true
---

## 복습 — alert / prompt / confirm

`prompt`로 **좋아하는 음식**을 입력받고,
`confirm`으로 **"정말로 좋아하나요?"** 를 물어본 뒤,
결과에 따라 다른 `alert` 메시지를 띄워보세요.

```js{monaco-run} {autorun:false}
// 힌트:
// 1. prompt로 음식 입력받기
// 2. confirm으로 확인받기
// 3. if/else로 분기해서 alert 출력

```

---
hideInToc: true
---

## 복습 — 연산자

아래 각 줄의 **출력 결과를 주석으로 먼저 예측**하고, 실행해서 맞춰보세요.
틀린 게 있다면 왜 그런지 생각해보세요.

```js{monaco-run} {autorun:false}
console.log(2 + 3 * 4);          // 예측: ?
console.log("5" + 3);            // 예측: ?
console.log("5" - 3);            // 예측: ?
console.log(+"42" + +"8");       // 예측: ?
console.log(10 % 3);             // 예측: ?
console.log(2 ** 8);             // 예측: ?
console.log("5" == 5);           // 예측: ?
console.log("5" === 5);          // 예측: ?
```

---
hideInToc: true
---

## 복습 — 조건문

`score` 변수를 바꿔가며 **학점 계산기**를 완성해보세요.

| 점수 | 학점 |
|------|------|
| 90 이상 | A |
| 80 이상 | B |
| 70 이상 | C |
| 60 이상 | D |
| 60 미만 | F |

```js{monaco-run} {autorun:false}
let score = 85; // 이 값을 바꿔가며 테스트해보세요

// if / else if / else 로 학점을 출력하는 코드를 작성하세요

```

---
hideInToc: true
---

## 복습 — 논리 연산자

아래 조건을 **`&&`, `||`, `!`** 를 활용해 구현해보세요.

```js{monaco-run} {autorun:false}
let isLoggedIn = true;
let isAdmin = false;
let userName = ""; // 빈 문자열로 테스트 — 나중에 "철수"로 바꿔보세요

// ① 로그인 상태이고 관리자인 경우만 "관리자 패널 접근 허용" 출력
if (/* 조건을 완성하세요 */) {
  console.log("관리자 패널 접근 허용");
} else {
  console.log("접근 거부");
}

// ② userName이 비어있으면 "익명" 으로 표시 (|| 활용)
let displayName = /* 여기를 완성하세요 */;
console.log("표시 이름:", displayName);
```

---
hideInToc: true
---

## 복습 — 반복문

**구구단 한 단**을 출력하는 코드를 작성해보세요.
`dan` 값을 바꾸면 해당 단의 구구단이 출력되어야 합니다.

```js{monaco-run} {autorun:false}
let dan = 3; // 이 값을 바꿔가며 테스트해보세요

// for 반복문으로 dan단의 구구단을 출력하세요
// 예시 출력: "3 x 1 = 3", "3 x 2 = 6", ...

```

---
