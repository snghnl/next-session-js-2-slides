---
layout: section
---
# 옵셔널 체이닝 `?.`
존재하지 않는 프로퍼티에 안전하게 접근하기

---
layout: default
hideInToc: true
---
# 왜 필요할까?

중첩 객체에서 없는 프로퍼티에 접근하면 에러가 발생합니다.

```js
let user = {}; // 주소 정보가 없는 사용자

alert(user.address.street);
// TypeError: Cannot read property 'street' of undefined
```

<v-click>

**기존 해결 방법 — `&&` 연산자**

```js
alert( user && user.address && user.address.street );
// undefined (에러 없음, 하지만 코드가 너무 길다!)
```

</v-click>

<v-click>

**더 나은 방법 — 옵셔널 체이닝 `?.`**

```js
alert( user?.address?.street );
// undefined (에러 없음, 훨씬 간결!)
```

</v-click>

---
layout: default
hideInToc: true
---
# 옵셔널 체이닝 동작 원리

`?.` **앞의 값이 `null` 또는 `undefined`이면** 평가를 즉시 멈추고 `undefined`를 반환합니다.

```js
let user = null;

alert( user?.address );        // undefined
alert( user?.address.street ); // undefined
```

<v-click>

> `?.`은 **앞**의 값만 검사합니다. 뒤는 검사하지 않습니다.

```js
let user = {}; // user는 있지만 address가 없음

alert( user?.address?.street ); // undefined ✅
alert( user?.address.street );  // TypeError ❌ (address가 undefined이므로)
```

</v-click>

<v-click>

> **주의:** `?.`를 남용하지 마세요.
> 반드시 존재해야 하는 값에 `?.`를 쓰면 에러를 조기에 발견하지 못합니다.
> **선택적으로 있어도 되는 값**에만 사용하세요.

</v-click>

---
layout: two-cols
hideInToc: true
---
# 단락 평가 (Short-circuit)

`?.` 왼쪽이 `null`/`undefined`이면
오른쪽은 **아예 실행되지 않습니다.**

```js
let user = null;
let x = 0;

user?.sayHi(x++);
// 아무 일도 일어나지 않음

alert(x); // 0 (증가하지 않음!)
```

::right::

<v-click>

**세 가지 사용 형태**

| 형태 | 설명 |
|---|---|
| `obj?.prop` | 프로퍼티 접근 |
| `obj?.[key]` | 대괄호 접근 |
| `obj?.method()` | 메서드 호출 |

```js
// ① 프로퍼티
user?.address

// ② 대괄호
let key = "firstName";
user1?.[key]

// ③ 메서드 호출
user1.admin?.()
user2.admin?.() // 에러 없음
```

</v-click>

---
layout: default
hideInToc: true
---
# `?.[]` 와 `?.()`

**`?.()`** — 메서드가 있을 수도, 없을 수도 있을 때

```js
let user1 = {
  admin() { alert("관리자 계정입니다."); }
};
let user2 = {};

user1.admin?.(); // 관리자 계정입니다.
user2.admin?.(); // 에러 없이 undefined 반환
```

<v-click>

**`?.[]`** — 동적 키로 프로퍼티에 접근할 때

```js
let user1 = { firstName: "Violet" };
let user2 = null;

let key = "firstName";

alert( user1?.[key] ); // Violet
alert( user2?.[key] ); // undefined

// 체이닝도 가능
alert( user1?.[key]?.something?.not?.existing ); // undefined
```

</v-click>

---
layout: default
hideInToc: true
---
# 핵심 정리

<v-click>

- `?.`은 왼쪽이 `null`/`undefined`이면 즉시 멈추고 `undefined` 반환

</v-click>

<v-click>

- 세 가지 형태: `obj?.prop` / `obj?.[key]` / `obj?.method()`

</v-click>

<v-click>

- **단락 평가** — 오른쪽 코드는 실행조차 되지 않음

</v-click>

<v-click>

- **남용 금지** — 선택적으로 있어도 되는 값에만 사용

</v-click>

<v-click>

- `?.` 앞의 변수는 반드시 선언되어 있어야 함

</v-click>

<v-click>

- 할당 연산자 왼쪽에는 사용 불가 (`user?.name = "X"` ❌)

</v-click>

---
layout: section
hideInToc: true
---
# Practice
옵셔널 체이닝 실습

---
layout: default
hideInToc: true
---
# Practice 1 — 안전한 프로퍼티 접근

`?.`를 사용해 에러 없이 값을 출력해보세요.

```js{monaco-run} {autorun:false, height:'220px'}
let users = [
  { name: "철수", address: { city: "서울", street: "강남대로" } },
  { name: "영희" }, // address 없음
  null,             // 사용자 자체가 없음
];

// 각 사용자의 street를 출력하세요.
// address나 사용자가 없으면 "정보 없음"을 출력하세요.
for (let user of users) {
  // let street = ???
  // console.log(user?.name, ":", street ?? "정보 없음");
}

// 예상 출력:
// 철수 : 강남대로
// 영희 : 정보 없음
// (null) : 정보 없음
```

---
layout: default
hideInToc: true
---
# Practice 2 — `?.()` 메서드 호출

메서드가 있을 수도 없을 수도 있는 객체를 안전하게 처리하세요.

```js{monaco-run} {autorun:false, height:'220px'}
let users = [
  {
    name: "철수",
    greet() { return `안녕하세요, ${this.name}입니다!`; }
  },
  {
    name: "영희"
    // greet 메서드 없음
  }
];

for (let user of users) {
  // greet 메서드가 있으면 호출하고, 없으면 "메서드 없음" 출력
  // let message = ???
  // console.log(message ?? "메서드 없음");
}

// 예상 출력:
// 안녕하세요, 철수입니다!
// 메서드 없음
```

---
layout: default
hideInToc: true
---
# Practice 3 — 중첩 객체 탐색

API 응답처럼 불완전한 데이터를 안전하게 처리해보세요.

```js{monaco-run} {autorun:false, height:'220px'}
let response = {
  status: 200,
  data: {
    user: {
      profile: {
        name: "민준",
        social: {
          github: "minjun-dev"
        }
      }
    }
  }
};

// 아래 값들을 옵셔널 체이닝으로 안전하게 접근하세요.
let name    = /* response에서 name 꺼내기 */;
let github  = /* response에서 github 꺼내기 */;
let twitter = /* response에서 twitter 꺼내기 (없는 값) */;

console.log(name);    // 민준
console.log(github);  // minjun-dev
console.log(twitter); // undefined
```

---
