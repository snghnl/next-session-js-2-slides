---
layout: section
---

# 화살표 함수 (Arrow Function)

더 짧고 간결하게

---
layout: default
hideInToc: true
---

# 화살표 함수 기본 문법

함수 표현식을 **훨씬 짧게** 쓸 수 있습니다.

<div class="grid grid-cols-2 gap-4">

<div>

**함수 표현식**
```js {monaco}
let sum = function(a, b) {
  return a + b;
};
```

</div>

<div>

**화살표 함수**
```js {monaco}
let sum = (a, b) => a + b;
```

</div>

</div>

<v-click>

**괄호 규칙**

```js {monaco}
// 인수가 2개 이상 → 괄호 필수
let sum = (a, b) => a + b;

// 인수가 1개 → 괄호 생략 가능
let double = n => n * 2;

// 인수가 없을 때 → 괄호 필수 (생략 불가)
let sayHi = () => console.log("안녕하세요!");
```

</v-click>

---
layout: default
hideInToc: true
---

# 본문이 여러 줄인 화살표 함수

표현식 하나가 아니라 여러 줄이 필요하다면 **중괄호 + return** 을 사용합니다.

<div class="grid grid-cols-2 gap-4">

<div>

**한 줄 — 중괄호 없음, return 자동**
```js {monaco}
let sum = (a, b) => a + b;

console.log(sum(1, 2)); // 3
```

</div>

<div>

**여러 줄 — 중괄호 필요, return 명시**
```js {monaco}
let sum = (a, b) => {
  let result = a + b;
  return result; // 반드시 return 필요!
};

console.log(sum(1, 2)); // 3
```

</div>

</div>

<v-click>

> **주의:** 중괄호를 쓰면 `return` 없이는 `undefined`가 반환됩니다!

```js {monaco}
let broken = (a, b) => { a + b; }; // return 없음!
console.log(broken(1, 2)); // undefined
```

</v-click>

---
layout: default
hideInToc: true
---

# 콜백으로 활용하기

화살표 함수는 **콜백**을 짧게 쓸 때 특히 유용합니다.

```js {monaco}
// 함수 표현식으로 쓴 콜백
[1, 2, 3].forEach(function(n) {
  console.log(n * 2);
});

// 화살표 함수로 쓴 콜백 (훨씬 간결!)
[1, 2, 3].forEach(n => console.log(n * 2));
```

<v-click>

**조건부 함수 정의도 간결해집니다**

```js {monaco}
let hour = 10;

let greet = (hour < 12)
  ? () => console.log("좋은 아침!")
  : () => console.log("안녕하세요!");

greet();
```

</v-click>

---
layout: default
hideInToc: true
---

# Practice 1 — 화살표 함수로 변환

아래 함수들을 **화살표 함수**로 변환해보세요.

```js{monaco-run} {autorun:false}
// 변환 전
// function square(n) { return n * n; }
// function greet(name) { return "안녕, " + name + "!"; }
// function isPositive(n) { return n > 0; }
// function sayHello() { return "Hello!"; }

// 화살표 함수로 변환하세요
let square    = /* ? */;
let greet     = /* ? */;
let isPositive = /* ? */;
let sayHello  = /* ? */;

// 테스트
console.log(square(4));        // 16
console.log(greet("철수"));    // 안녕, 철수!
console.log(isPositive(-3));   // false
console.log(sayHello());       // Hello!
```

---
layout: default
hideInToc: true
---

# Practice 2 — 여러 줄 화살표 함수

`getAbsMax(a, b)` — 두 수 중 **절댓값이 더 큰 수**를 반환하는 함수를 화살표 함수로 작성해보세요.

```js{monaco-run} {autorun:false}
// 중괄호와 return을 사용하는 화살표 함수로 작성하세요
let getAbsMax = (a, b) => {
  // 여기를 완성하세요
  // 힌트: Math.abs(n) 으로 절댓값을 구할 수 있습니다
};

// 테스트
console.log(getAbsMax(3, -7));  // 7  (-7의 절댓값 7이 더 큼)
console.log(getAbsMax(-5, 2));  // 5
console.log(getAbsMax(4, -4));  // 4
```

---
layout: default
hideInToc: true
---

# Practice 3 — 콜백으로 활용

배열 메서드에 **화살표 함수**를 콜백으로 넘겨보세요.

```js{monaco-run} {autorun:false}
let numbers = [3, -1, 4, -1, 5, -9, 2, 6];

// ① filter: 양수만 골라내기 (화살표 함수 사용)
let positives = numbers.filter(/* 여기를 완성하세요 */);
console.log(positives); // [3, 4, 5, 2, 6]

// ② map: 각 요소를 제곱하기 (화살표 함수 사용)
let squared = numbers.map(/* 여기를 완성하세요 */);
console.log(squared); // [9, 1, 16, 1, 25, 81, 4, 36]

// ③ forEach: 절댓값 출력하기 (화살표 함수 사용)
numbers.forEach(/* 여기를 완성하세요 */);
// 3, 1, 4, 1, 5, 9, 2, 6
```
