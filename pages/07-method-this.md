---
layout: section
---
# 메서드와 `this`
객체에 행동을 부여하는 방법

---
layout: default
hideInToc: true
---
# 메서드란?

객체 프로퍼티에 저장된 함수를 **메서드(method)** 라고 합니다.

```js
let user = {
  name: "John",
  age: 30
};
```

<v-click>

실제 사용자처럼 객체도 **행동**을 할 수 있어야 합니다.
→ 로그인, 로그아웃, 인사하기 등

</v-click>

<v-click>

```js
// 함수를 프로퍼티에 할당하면 → 메서드!
user.sayHi = function() {
  alert("안녕하세요!");
};

user.sayHi(); // 안녕하세요!
```

</v-click>

---
layout: two-cols
hideInToc: true
---
# 메서드 선언 방법

**① 프로퍼티에 직접 할당**

```js
let user = {};

user.sayHi = function() {
  alert("안녕하세요!");
};
```

<v-click>

**② 선언된 함수를 등록**

```js
function sayHi() {
  alert("안녕하세요!");
}

user.sayHi = sayHi;
```

</v-click>

::right::

<v-click>

**③ 단축 구문 (권장)**

```js
let user = {
  // "sayHi: function()"과 동일
  sayHi() {
    alert("안녕하세요!");
  }
};

user.sayHi();
```

> `function` 키워드를 생략해 더 간결하게 작성할 수 있습니다.

</v-click>

---
layout: default
hideInToc: true
---
# 메서드와 `this`

메서드는 객체에 저장된 정보에 접근해야 할 때가 많습니다.

**`this`** = 메서드를 호출한 객체를 가리키는 키워드

```js
let user = {
  name: "John",
  age: 30,

  sayHi() {
    alert(this.name); // 'this'는 현재 객체(user)를 나타냄
  }
};

user.sayHi(); // John
```

<v-click>

> `this`를 쓰지 않고 `user.name`으로 직접 참조할 수도 있지만,
> 객체가 다른 변수에 복사되거나 `null`이 되면 **에러**가 발생합니다.

</v-click>

---
layout: default
hideInToc: true
---
# `this` 없이 쓰면 생기는 문제

```js
let user = {
  name: "John",

  sayHi() {
    alert(user.name); // ❌ this 대신 user를 직접 참조
  }
};

let admin = user;
user = null; // user를 null로 덮어씀

admin.sayHi(); // Error: Cannot read properties of null
```

<v-click>

```js
let user = {
  name: "John",

  sayHi() {
    alert(this.name); // ✅ this를 사용하면 안전
  }
};

let admin = user;
user = null;

admin.sayHi(); // John — 정상 동작!
```

</v-click>

---
layout: default
hideInToc: true
---
# 자유로운 `this`

자바스크립트의 `this`는 **런타임에 결정**됩니다.
같은 함수라도 어떤 객체에서 호출하느냐에 따라 `this`가 달라집니다.

```js
let user  = { name: "John" };
let admin = { name: "Admin" };

function sayHi() {
  alert(this.name);
}

user.f  = sayHi;
admin.f = sayHi;

user.f();  // John   (this == user)
admin.f(); // Admin  (this == admin)
```

<v-click>

> **규칙:** `obj.f()`를 호출하면 `this`는 `obj`입니다.

</v-click>

<v-click>

> **주의:** 객체 없이 `sayHi()`만 호출하면 엄격 모드에서 `this`는 `undefined`입니다.

</v-click>

---
layout: default
hideInToc: true
---
# 화살표 함수와 `this`

화살표 함수는 **자신만의 `this`를 가지지 않습니다.**
외부 함수의 `this`를 그대로 가져옵니다.

```js
let user = {
  firstName: "보라",

  sayHi() {
    // 화살표 함수는 외부 sayHi()의 this를 사용
    let arrow = () => alert(this.firstName);
    arrow();
  }
};

user.sayHi(); // 보라
```

<v-click>

| | 일반 함수 | 화살표 함수 |
|---|---|---|
| `this` | 호출한 객체 | 외부 컨텍스트의 `this` |
| 용도 | 메서드 | 콜백, 내부 함수 |

</v-click>

---
layout: default
hideInToc: true
---
# 핵심 정리

<v-click>

- 객체 프로퍼티에 저장된 함수 → **메서드**

</v-click>

<v-click>

- 메서드 내부에서 `this` → **메서드를 호출한 객체**

</v-click>

<v-click>

- `this`는 **런타임에 결정** — 함수가 어디서 정의됐는지가 아니라 **어떻게 호출됐는지**가 중요

</v-click>

<v-click>

- 화살표 함수는 `this`가 없음 → 외부 컨텍스트의 `this`를 사용

</v-click>

<v-click>

```js
let user = {
  name: "철수",
  greet() {
    return `안녕, 나는 ${this.name}이야!`;
  }
};
console.log(user.greet()); // 안녕, 나는 철수이야!
```

</v-click>

---
layout: section
hideInToc: true
---
# Practice
메서드와 `this` 실습

---
layout: default
hideInToc: true
---
# Practice 1 — 메서드 추가하기

아래 `counter` 객체에 메서드를 추가해보세요.

```js{monaco-run} {autorun:false}
let counter = {
  count: 0,

  // ① increment: count를 1 증가시키는 메서드를 작성하세요
  // increment() { ... }

  // ② decrement: count를 1 감소시키는 메서드를 작성하세요
  // decrement() { ... }

  // ③ reset: count를 0으로 초기화하는 메서드를 작성하세요
  // reset() { ... }
};

counter.increment();
counter.increment();
counter.increment();
counter.decrement();
console.log(counter.count); // 2

counter.reset();
console.log(counter.count); // 0
```

---
layout: default
hideInToc: true
---
# Practice 2 — `this` 활용하기

`calculator` 객체를 완성하세요. 모든 메서드는 `this`를 사용해야 합니다.

```js{monaco-run} {autorun:false}
let calculator = {
  result: 0,

  // add(n): result에 n을 더하고 this를 반환
  // subtract(n): result에서 n을 빼고 this를 반환
  // multiply(n): result에 n을 곱하고 this를 반환
  // getResult(): result를 반환
};

// 메서드 체이닝으로 연속 계산
let answer = calculator
  .add(10)
  .multiply(3)
  .subtract(5)
  .getResult();

console.log(answer); // 25
```

---
layout: default
hideInToc: true
---
# Practice 3 — 화살표 함수 vs 일반 함수

아래 코드를 실행해보고, 왜 그런 결과가 나오는지 이해해보세요.

```js{monaco-run} {autorun:false}
let team = {
  name: "NEXT",
  members: ["철수", "영희", "민준"],

  // ① 일반 함수 메서드
  greetNormal: function() {
    return this.name; // this는?
  },

  // ② 화살표 함수 메서드
  greetArrow: () => {
    return this; // this는?
  },

  // ③ 메서드 안에서 화살표 함수 콜백
  listMembers() {
    return this.members.map(m => `[${this.name}] ${m}`);
  }
};

console.log(team.greetNormal()); // ?
console.log(team.greetArrow());  // ?
console.log(team.listMembers()); // ?
```

---
