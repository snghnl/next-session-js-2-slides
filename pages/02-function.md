---
layout: section
---

# 함수 (Function)

코드를 재사용하는 가장 기본적인 방법

---
layout: default
hideInToc: true
---

# 함수란?

유사한 동작을 하는 코드를 **한 곳에 모아** 언제든 다시 호출할 수 있게 합니다.

```js {monaco}
// 함수 선언 (Function Declaration)
function showMessage() {
  console.log('안녕하세요!');
}

// 함수 호출
showMessage(); // 안녕하세요!
showMessage(); // 안녕하세요! (재사용!)
```

<v-click>

```js {monaco}
// 매개변수가 있는 함수
function greet(name) {
  console.log('안녕하세요, ' + name + '님!');
}

greet('철수'); // 안녕하세요, 철수님!
greet('영희'); // 안녕하세요, 영희님!
```

</v-click>

---
layout: default
hideInToc: true
---

# 지역 변수 vs 외부 변수

<div class="grid grid-cols-2 gap-4">

<div>

**지역 변수 (Local Variable)**
함수 안에서만 존재합니다.

```js {monaco}
function showMessage() {
  let message = "안녕하세요!"; // 지역 변수
  console.log(message);
}

showMessage(); // 안녕하세요!
console.log(message); // ❌ ReferenceError!
```

</div>

<div>

**외부 변수 (Outer Variable)**
함수는 바깥 변수를 읽고 수정할 수 있습니다.

```js {monaco}
let userName = 'John';

function showMessage() {
  userName = "Bob"; // 외부 변수 수정
  console.log('Hello, ' + userName);
}

console.log(userName); // John
showMessage();         // Hello, Bob
console.log(userName); // Bob (변경됨!)
```

</div>

</div>

<v-click>

> **Tip:** 외부 변수를 함부로 수정하면 버그가 생기기 쉽습니다. **매개변수와 지역 변수**를 활용하세요!

</v-click>

---
layout: default
hideInToc: true
---

# 매개변수와 기본값

```js {monaco}
// 매개변수(parameter): 함수 선언 시 괄호 안의 변수
// 인수(argument): 함수 호출 시 전달하는 값
function showMessage(from, text = "메시지 없음") {
  console.log(from + ": " + text);
}

showMessage("Ann", "Hello!");    // Ann: Hello!
showMessage("Ann");              // Ann: 메시지 없음 (기본값 사용)
showMessage("Ann", undefined);   // Ann: 메시지 없음 (기본값 사용)
```

<v-click>

**중요:** 매개변수는 **복사된 값**을 사용합니다 — 원본은 변경되지 않습니다.

```js {monaco}
function addStar(from) {
  from = '*' + from + '*'; // 복사된 값을 변경
  console.log(from);
}

let name = "Ann";
addStar(name);      // *Ann*
console.log(name);  // Ann (원본은 그대로!)
```

</v-click>

---
layout: default
hideInToc: true
---

# 반환 값 (return)

함수가 계산한 결과를 **호출한 곳으로 돌려줍니다**.

```js {monaco}
function sum(a, b) {
  return a + b; // 값을 반환하고 함수 종료
}

let result = sum(3, 5);
console.log(result); // 8
```

<v-click>

**주의사항**

```js {monaco}
// return이 없는 함수도 → undefined 반환
function doNothing() { }
console.log(doNothing()); // undefined

// ⚠️ return 뒤에 줄바꿈 금지!
// return        ← 세미콜론이 자동 삽입되어 undefined 반환!
//   a + b;
```

</v-click>

---
layout: default
hideInToc: true
---

# 함수 이름짓기

함수 이름은 **동사**로 시작하고, 이름만 보고도 동작을 알 수 있어야 합니다.

<div class="grid grid-cols-2 gap-4 mt-4">

<div>

**좋은 접두어 예시**

| 접두어 | 의미 |
|--------|------|
| `show…` | 무언가를 보여줌 |
| `get…` | 값을 반환함 |
| `calc…` | 무언가를 계산함 |
| `create…` | 무언가를 생성함 |
| `check…` | 확인 후 boolean 반환 |

</div>

<div>

**실제 예시**

```js {monaco}
showMessage(..);     // 메시지를 보여줌
getAge(..);          // 나이를 반환함
calcSum(..);         // 합계를 계산함
createForm(..);      // form을 생성해 반환
checkPermission(..); // true/false 반환
```

<v-click>

> **원칙:** 함수 하나는 **동작 하나**만!
> `getAge()`가 나이를 출력까지 하면 안 됩니다.

</v-click>

</div>

</div>

---
layout: default
hideInToc: true
---

# Practice 1 — 기본 함수 만들기

두 수를 받아 **더하고**, **빼고**, **곱하는** 함수 3개를 만들고 호출해보세요.

```js{monaco-run} {autorun:false}
// ① add(a, b): a와 b를 더한 값을 반환
function add(a, b) {
  // 여기를 완성하세요
}

// ② subtract(a, b): a에서 b를 뺀 값을 반환


// ③ multiply(a, b): a와 b를 곱한 값을 반환


// 테스트
console.log(add(3, 5));        // 8
console.log(subtract(10, 4));  // 6
console.log(multiply(3, 7));   // 21
```

---
layout: default
hideInToc: true
---

# Practice 2 — 매개변수와 기본값

이름과 인사말을 받아 출력하는 함수를 만들어보세요.
인사말을 전달하지 않으면 **기본값 "안녕하세요"** 를 사용해야 합니다.

```js{monaco-run} {autorun:false}
// greet(name, greeting): name과 greeting을 조합해 출력
// 예: greet("철수", "반가워요") → "반가워요, 철수님!"
// 예: greet("영희")             → "안녕하세요, 영희님!"

function greet(name, greeting = /* 기본값을 설정하세요 */) {
  // 여기를 완성하세요
}

// 테스트
greet("철수", "반가워요"); // 반가워요, 철수님!
greet("영희");             // 안녕하세요, 영희님!
greet("민준", "좋은 아침이에요"); // 좋은 아침이에요, 민준님!
```

---
layout: default
hideInToc: true
---

# Practice 3 — 함수로 분리하기

아래 코드는 1~100 사이 **소수(prime number)를 출력**합니다.
`isPrime(n)` 함수를 분리해서 코드를 더 읽기 좋게 만들어보세요.

```js{monaco-run} {autorun:false}
// 현재 코드 (함수 분리 전)
// for (let i = 2; i <= 100; i++) {
//   let isPrime = true;
//   for (let j = 2; j < i; j++) {
//     if (i % j === 0) { isPrime = false; break; }
//   }
//   if (isPrime) console.log(i);
// }

// ① isPrime(n): n이 소수면 true, 아니면 false를 반환하는 함수를 만드세요
function isPrime(n) {
  // 여기를 완성하세요
}

// ② 위 함수를 사용해 1~100 사이 소수를 출력하세요
for (let i = 2; i <= 100; i++) {
  // 여기를 완성하세요
}
```
