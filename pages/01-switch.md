---
layout: section
---

# switch문

복수의 조건을 깔끔하게 처리하는 방법

---
layout: default
hideInToc: true
---

# switch문이란?

여러 개의 `if` 조건문을 하나의 깔끔한 구조로 대체할 수 있습니다.

```js {monaco}
switch(x) {
  case 'value1':  // if (x === 'value1')
    // 실행할 코드
    break;

  case 'value2':  // if (x === 'value2')
    // 실행할 코드
    break;

  default:
    // 어떤 case에도 해당하지 않을 때
    break;
}
```

<v-click>

- `case` 값과 변수를 **일치 비교(`===`)** 합니다
- 일치하는 `case`의 코드를 실행하고, `break`를 만나면 멈춥니다
- 어느 `case`도 맞지 않으면 `default`가 실행됩니다

</v-click>

---
layout: default
hideInToc: true
---

# break가 없으면?

`break`가 없으면 **아래 case를 계속 실행**합니다 (Fall-through)

<div class="grid grid-cols-2 gap-4">

<div>

**break 있음 ✅**
```js {monaco}
let a = 4;

switch (a) {
  case 3:
    console.log('3입니다');
    break;
  case 4:
    console.log('4입니다');
    break;  // ← 여기서 멈춤
  case 5:
    console.log('5입니다');
    break;
}
```

</div>

<div>

**break 없음 ⚠️**
```js {monaco}
let a = 4;

switch (a) {
  case 3:
    console.log('3입니다');
  case 4:
    console.log('4입니다'); // ← 실행됨
  case 5:
    console.log('5입니다'); // ← 이것도 실행됨!
  default:
    console.log('default'); // ← 이것도!
}
```

</div>

</div>

<v-click>

> **주의:** `break`를 빠뜨리면 조건에 상관없이 아래 `case`가 줄줄이 실행됩니다!

</v-click>

---
layout: default
hideInToc: true
---

# 여러 case 묶기

같은 코드를 실행해야 하는 `case`는 **한데 묶을 수** 있습니다.

```js {monaco}
let a = 3;

switch (a) {
  case 4:
    console.log('계산이 맞습니다!');
    break;

  case 3: // case 3과 case 5를 묶음
  case 5:
    console.log('계산이 틀립니다!');
    console.log('수학 수업을 다시 들어보는걸 권유 드립니다.');
    break;

  default:
    console.log('계산 결과가 이상하네요.');
}
```

<v-click>

`case 3`에 `break`가 없으므로 `case 5`로 이어지고, 두 case가 **같은 코드 블록을 공유**합니다.

</v-click>

---
layout: default
hideInToc: true
---

# 자료형의 중요성

switch문은 **엄격한 일치 비교(`===`)** 를 사용합니다 — 값과 타입이 모두 같아야 합니다!

```js {monaco}
let arg = "3"; // prompt는 항상 문자열을 반환합니다

switch (arg) {
  case '0':
  case '1':
    console.log('0이나 1을 입력하셨습니다.');
    break;

  case '2':
    console.log('2를 입력하셨습니다.');
    break;

  case 3:         // ← 숫자 3 (문자열 "3"과 다름!)
    console.log('이 코드는 절대 실행되지 않습니다!');
    break;

  default:
    console.log('알 수 없는 값을 입력하셨습니다.');
}
```

<v-click>

`"3" === 3`은 **`false`** — 문자열과 숫자는 다릅니다!

</v-click>

---
layout: default
hideInToc: true
---

# Practice 1 — 요일 출력기

`day` 값에 따라 **한국어 요일 이름**을 출력하는 switch문을 완성해보세요.

```js{monaco-run} {autorun:false, height:'220px'}
let day = 3; // 1~7 사이 값을 바꿔가며 테스트해보세요
             // 1=월, 2=화, 3=수, 4=목, 5=금, 6=토, 7=일

switch (day) {
  // 여기에 case를 작성하세요
  // 예: case 1: console.log("월요일"); break;
}

// 보너스: 6, 7은 "주말입니다!", 1~5는 "평일입니다!" 도 함께 출력해보세요
```

---
layout: default
hideInToc: true
---

# Practice 2 — 계절 판별기

`month` 값(1~12)에 따라 **계절**을 출력해보세요.
여러 case를 묶는 방법을 활용해보세요.

```js{monaco-run} {autorun:false, height:'220px'}
let month = 7; // 이 값을 바꿔가며 테스트해보세요

// 봄: 3, 4, 5월 → "봄입니다 🌸"
// 여름: 6, 7, 8월 → "여름입니다 ☀️"
// 가을: 9, 10, 11월 → "가을입니다 🍂"
// 겨울: 12, 1, 2월 → "겨울입니다 ❄️"
// 그 외: "올바른 월을 입력해주세요"

switch (month) {
  // 여기에 코드를 작성하세요
}
```

---
layout: default
hideInToc: true
---

# Practice 3 — if문을 switch로 바꾸기

아래 `if/else if` 코드를 **switch문으로 변환**해보세요.

<div class="grid grid-cols-2 gap-4">

<div>

**변환 전 (if문)**
```js {monaco}
let fruit = "사과";

if (fruit === "사과") {
  console.log("🍎 사과입니다");
} else if (fruit === "바나나") {
  console.log("🍌 바나나입니다");
} else if (fruit === "포도") {
  console.log("🍇 포도입니다");
} else {
  console.log("🍽️ 모르는 과일입니다");
}
```

</div>

<div>

**변환 후 (switch문)**
```js{monaco-run} {autorun:false, height:'220px'}
let fruit = "사과"; // 값을 바꿔가며 테스트해보세요

switch (fruit) {
  // 여기에 코드를 작성하세요
}
```

</div>

</div>
