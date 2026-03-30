---
layout: section
---

# 참조에 의한 객체 복사

객체는 값이 아닌 주소를 저장한다

---
layout: default
hideInToc: true
---

# 원시값 vs 객체의 복사

<div class="grid grid-cols-2 gap-4">

<div>

**원시값 — 값 자체가 복사됨**

```js {monaco}
let a = "Hello!";
let b = a; // 값이 복사됨

b = "Bye!";
console.log(a); // "Hello!" (영향 없음)
```

`a`와 `b`는 완전히 독립적입니다.

</div>

<div>

**객체 — 참조(주소)가 복사됨**

```js {monaco}
let user = { name: "John" };
let admin = user; // 참조가 복사됨

admin.name = "Pete"; // 같은 객체를 수정!
console.log(user.name); // "Pete" ← 영향받음!
```

`user`와 `admin`은 **같은 객체**를 가리킵니다.

</div>

</div>

<v-click>

> 서랍장(객체)은 하나, 열쇠(변수)는 여러 개.
> 어느 열쇠로 열어도 같은 서랍장을 봅니다.

</v-click>

---
layout: default
hideInToc: true
---

# 참조 비교

객체끼리 `==` / `===` 비교는 **같은 객체를 가리키는지** 비교합니다.

```js {monaco}
let a = {};
let b = a;   // 같은 객체 참조

console.log(a == b);  // true
console.log(a === b); // true

let c = {};
let d = {};  // 독립된 빈 객체

console.log(c == d);  // false ← 내용이 같아도 다른 객체!
```

<v-click>

> 객체의 내용이 같은지 비교하려면 `JSON.stringify()` 등을 활용해야 합니다.
> (단순 `==` / `===` 는 주소를 비교합니다)

</v-click>

---
layout: default
hideInToc: true
---

# 객체 복사 — 얕은 복사

독립적인 복사본을 만들려면 **프로퍼티를 직접 복사**해야 합니다.

<div class="grid grid-cols-2 gap-4">

<div>

**for...in 으로 복사**
```js {monaco}
let user = { name: "John", age: 30 };

let clone = {};
for (let key in user) {
  clone[key] = user[key];
}

clone.name = "Pete";
console.log(user.name);  // "John" (독립!)
console.log(clone.name); // "Pete"
```

</div>

<div>

**Object.assign 으로 복사**
```js {monaco}
let user = { name: "John", age: 30 };

// Object.assign(목표, 출처1, 출처2, ...)
let clone = Object.assign({}, user);

// 병합도 가능
Object.assign(user, { canView: true, canEdit: true });
console.log(user);
// { name: "John", age: 30, canView: true, canEdit: true }
```

</div>

</div>

---
layout: default
hideInToc: true
---

# 얕은 복사의 한계 — 중첩 객체

`Object.assign`은 **중첩 객체는 여전히 참조로 복사**합니다.

```js {monaco}
let user = {
  name: "John",
  sizes: { height: 182, width: 50 } // 중첩 객체
};

let clone = Object.assign({}, user);

console.log(user.sizes === clone.sizes); // true ← 같은 객체!

user.sizes.width++;
console.log(clone.sizes.width); // 51 ← 영향받음!
```

<v-click>

**완전히 독립적인 복사 → 깊은 복사(Deep Clone)**

```js {monaco}
// 방법 1: JSON 직렬화 (간단하지만 함수/undefined 등 손실)
let deepClone = JSON.parse(JSON.stringify(user));

// 방법 2: structuredClone (모던 브라우저/Node.js 지원)
let deepClone2 = structuredClone(user);
```

</v-click>

---
layout: default
hideInToc: true
---

# Practice 1 — 참조 vs 복사 예측

아래 코드의 **출력 결과를 먼저 예측**하고, 실행해서 확인해보세요.

```js{monaco-run} {autorun:false, height:'220px'}
// ① 원시값 복사
let x = 10;
let y = x;
y = 20;
console.log(x); // 예측: ?

// ② 객체 참조
let obj1 = { value: 10 };
let obj2 = obj1;
obj2.value = 20;
console.log(obj1.value); // 예측: ?

// ③ 객체 비교
let a = { n: 1 };
let b = { n: 1 };
let c = a;
console.log(a == b);  // 예측: ?
console.log(a == c);  // 예측: ?
```

---
layout: default
hideInToc: true
---

# Practice 2 — Object.assign 활용

`Object.assign`을 활용해 객체를 복사하고 병합해보세요.

```js{monaco-run} {autorun:false, height:'220px'}
let defaults = { theme: "light", language: "ko", fontSize: 14 };
let userSettings = { theme: "dark", fontSize: 16 };

// ① defaults를 복사한 뒤 userSettings로 덮어써서 최종 설정 객체를 만드세요
// 결과: { theme: "dark", language: "ko", fontSize: 16 }
let finalSettings = /* 여기를 완성하세요 */;
console.log(finalSettings);

// ② defaults가 변경되지 않았는지 확인하세요
console.log(defaults.theme); // "light" 여야 합니다
```

---
layout: default
hideInToc: true
---

# Practice 3 — 얕은 복사 vs 깊은 복사

얕은 복사와 깊은 복사의 차이를 직접 확인해보세요.

```js{monaco-run} {autorun:false, height:'220px'}
let original = {
  name: "철수",
  scores: { math: 90, english: 85 }
};

// ① 얕은 복사 (Object.assign)
let shallow = Object.assign({}, original);

// ② 깊은 복사 (structuredClone)
let deep = structuredClone(original);

// 중첩 객체 수정
original.scores.math = 100;

console.log(shallow.scores.math); // 예측: ? (얕은 복사)
console.log(deep.scores.math);    // 예측: ? (깊은 복사)

// 최상위 프로퍼티 수정
original.name = "영희";
console.log(shallow.name); // 예측: ?
console.log(deep.name);    // 예측: ?
```

---
