---
layout: section
---

# 함수 표현식 (Function Expression)

함수도 값이다

---
layout: default
hideInToc: true
---

# 함수 선언문 vs 함수 표현식

<div class="grid grid-cols-2 gap-4">

<div>

**함수 선언문 (Function Declaration)**

```js {monaco}
// 독립된 구문으로 존재
function sayHi() {
  console.log("Hello");
}

sayHi(); // Hello
```

</div>

<div>

**함수 표현식 (Function Expression)**

```js {monaco}
// 변수에 함수를 값으로 할당
let sayHi = function() {
  console.log("Hello");
};  // ← 구문 끝이므로 세미콜론 필요!

sayHi(); // Hello
```

</div>

</div>

<v-click>

함수 표현식에서 `function` 뒤에 **이름이 없습니다** — 이를 **익명 함수(anonymous function)** 라고 합니다.

> 함수는 **값**입니다. 숫자나 문자열처럼 변수에 저장하고 전달할 수 있습니다.

</v-click>

---
layout: default
hideInToc: true
---

# 함수를 값처럼 다루기

함수는 값이기 때문에 **복사하고 전달**할 수 있습니다.

```js {monaco}
function sayHi() {   // (1) 함수 선언
  console.log("Hello");
}

let func = sayHi;    // (2) 함수 복사 (괄호 없음! sayHi() 였다면 호출 결과가 저장됨)

func();              // (3) Hello — 복사한 함수 실행
sayHi();             //     Hello — 원본 함수도 실행
```

<v-click>

**주의: 괄호 유무가 완전히 다릅니다!**

```js {monaco}
let a = sayHi;   // sayHi 함수 자체를 a에 저장
let b = sayHi(); // sayHi를 호출한 반환값을 b에 저장
```

</v-click>

---
layout: default
hideInToc: true
---

# 콜백 함수 (Callback Function)

함수를 **다른 함수의 인수로 전달**하고, 나중에 호출되도록 하는 패턴입니다.

```js {monaco}
function ask(question, yes, no) {
  if (confirm(question)) yes();
  else no();
}

function showOk() { console.log("동의하셨습니다."); }
function showCancel() { console.log("취소 버튼을 누르셨습니다."); }

// showOk, showCancel이 콜백 함수
ask("동의하십니까?", showOk, showCancel);
```

<v-click>

**익명 함수로 더 간결하게:**

```js {monaco}
ask(
  "동의하십니까?",
  function() { console.log("동의하셨습니다."); },    // 익명 콜백
  function() { console.log("취소하셨습니다."); }     // 익명 콜백
);
```

</v-click>

---
layout: two-cols
hideInToc: true
---

# 선언문 vs 표현식: 핵심 차이

**함수 선언문** — 호이스팅 O

```js {monaco}
// 선언 전에 호출 가능! (호이스팅)
sayHi("철수"); // Hello, 철수

function sayHi(name) {
  console.log(`Hello, ${name}`);
}
```

스크립트 실행 전 준비단계에서 먼저 생성됩니다.

::right::

**함수 표현식** — 호이스팅 X

```js {monaco}
// 선언 전에 호출하면 에러!
sayHi("철수"); // ❌ ReferenceError

let sayHi = function(name) {
  console.log(`Hello, ${name}`);
};
```

실행 흐름이 해당 줄에 도달해야 생성됩니다.

<v-click>

**언제 표현식을 써야 할까?** 조건에 따라 함수를 다르게 정의해야 할 때:

```js {monaco}
let greet = (hour < 12)
  ? function() { console.log("좋은 아침!"); }
  : function() { console.log("안녕하세요!"); };

greet();
```

</v-click>

---
layout: default
hideInToc: true
---

# Practice 1 — 함수 표현식으로 변환

아래 함수 선언문들을 **함수 표현식**으로 바꿔 작성해보세요.

```js{monaco-run} {autorun:false}
// 변환 전 (함수 선언문)
// function double(n) { return n * 2; }
// function isEven(n) { return n % 2 === 0; }
// function greet(name) { return "안녕, " + name + "!"; }

// 변환 후 (함수 표현식으로 작성하세요)
let double = /* 여기를 완성하세요 */;
let isEven = /* 여기를 완성하세요 */;
let greet  = /* 여기를 완성하세요 */;

// 테스트
console.log(double(5));      // 10
console.log(isEven(4));      // true
console.log(isEven(7));      // false
console.log(greet("철수"));  // 안녕, 철수!
```

---
layout: default
hideInToc: true
---

# Practice 2 — 콜백 함수

`repeat(n, action)` 함수를 만들어보세요.
`n`번 반복하며 매번 `action(i)`를 호출해야 합니다.

```js{monaco-run} {autorun:false}
// repeat(n, action): n번 반복하며 action(i)를 호출 (i는 0부터 시작)
function repeat(n, action) {
  // 여기를 완성하세요
}

// 테스트 ① — 함수 표현식을 콜백으로 전달
repeat(3, function(i) {
  console.log(`${i}번째 반복입니다`);
});
// 0번째 반복입니다
// 1번째 반복입니다
// 2번째 반복입니다

// 테스트 ② — 함수를 변수에 저장 후 전달
let printSquare = function(i) { console.log(i * i); };
repeat(4, printSquare); // 0, 1, 4, 9
```

---
layout: default
hideInToc: true
---

# Practice 3 — 조건부 함수 정의

`score`에 따라 다른 함수를 `getGrade`에 저장하고 호출해보세요.
함수 표현식과 삼항 연산자를 활용해보세요.

```js{monaco-run} {autorun:false}
let score = 75; // 이 값을 바꿔가며 테스트해보세요

// score가 60 이상이면 "합격입니다!", 미만이면 "불합격입니다." 를 출력하는
// 함수를 getGrade에 할당하세요 (함수 표현식 + 삼항 연산자 활용)
let getGrade = /* 여기를 완성하세요 */;

getGrade(); // score에 따라 다른 메시지 출력

// 보너스: 90이상 A, 80이상 B, 70이상 C, 60이상 D, 미만 F 를 출력하도록 수정해보세요
```
