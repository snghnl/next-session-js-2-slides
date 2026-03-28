---
layout: section
---

# 객체 (Object)

데이터를 묶어서 다루는 방법

---
layout: default
hideInToc: true
---

# 객체란?

여러 데이터를 **키-값 쌍**으로 묶어 저장하는 자료구조입니다.

```js {monaco}
// 객체 리터럴로 생성
let user = {
  name: "John",   // 키: "name", 값: "John"
  age: 30,        // 키: "age",  값: 30
};

// 점 표기법으로 접근
console.log(user.name); // John
console.log(user.age);  // 30

// 프로퍼티 추가 / 삭제
user.isAdmin = true;   // 추가
delete user.age;       // 삭제

console.log(user); // { name: "John", isAdmin: true }
```

<v-click>

> `const`로 선언해도 프로퍼티는 수정할 수 있습니다. `const`는 변수 재할당만 막습니다.

</v-click>

---
layout: default
hideInToc: true
---

# 점 표기법 vs 대괄호 표기법

<div class="grid grid-cols-2 gap-4">

<div>

**점 표기법** — 단순한 키에 사용

```js {monaco}
let user = { name: "John", age: 30 };

console.log(user.name); // John
user.age = 31;
```

공백이나 특수문자가 있으면 사용 불가!

</div>

<div>

**대괄호 표기법** — 어떤 키든 사용 가능

```js {monaco}
let user = { "likes birds": true };

// 공백 있는 키
console.log(user["likes birds"]); // true

// 변수로 동적 접근
let key = "name";
console.log(user[key]);  // John
console.log(user.key);   // undefined ❌
```

</div>

</div>

<v-click>

**계산된 프로퍼티** — 변수로 키를 동적으로 설정:

```js {monaco}
let fruit = "apple";
let bag = { [fruit]: 5 }; // { apple: 5 }
console.log(bag.apple);   // 5
```

</v-click>

---
layout: default
hideInToc: true
---

# 단축 프로퍼티

변수 이름과 프로퍼티 이름이 같을 때 **생략**할 수 있습니다.

<div class="grid grid-cols-2 gap-4">

<div>

**일반 방식**
```js {monaco}
function makeUser(name, age) {
  return {
    name: name,
    age: age,
  };
}

let user = makeUser("John", 30);
console.log(user.name); // John
```

</div>

<div>

**단축 프로퍼티**
```js {monaco}
function makeUser(name, age) {
  return {
    name,  // name: name 과 동일
    age,   // age: age 와 동일
  };
}

let user = makeUser("John", 30);
console.log(user.name); // John
```

</div>

</div>

---
layout: default
hideInToc: true
---

# `in` 연산자와 `for...in` 반복문

**`in` — 프로퍼티 존재 여부 확인**

```js {monaco}
let user = { name: "John", age: 30 };

console.log("age" in user);    // true
console.log("height" in user); // false

// undefined 비교보다 in이 더 안전!
let obj = { test: undefined };
console.log(obj.test === undefined); // true (프로퍼티가 없는 것처럼 보임)
console.log("test" in obj);          // true (실제로는 존재!)
```

<v-click>

**`for...in` — 모든 프로퍼티 순회**

```js {monaco}
let user = { name: "John", age: 30, isAdmin: true };

for (let key in user) {
  console.log(key + ": " + user[key]);
}
// name: John
// age: 30
// isAdmin: true
```

</v-click>

---
layout: default
hideInToc: true
---

# Practice 1 — 객체 만들고 다루기

`book` 객체를 만들고 프로퍼티를 추가/삭제/조회해보세요.

```js{monaco-run} {autorun:false}
// ① title: "자바스크립트", author: "존도우", pages: 300 으로 book 객체를 만드세요
let book = /* 여기를 완성하세요 */;

// ② 점 표기법으로 title과 author를 출력하세요
console.log(/* ? */); // 자바스크립트
console.log(/* ? */); // 존도우

// ③ isRead: false 프로퍼티를 추가하세요

// ④ pages 프로퍼티를 삭제하세요

// ⑤ "isRead" 키가 존재하는지 in 연산자로 확인하세요
console.log(/* ? */); // true

console.log(book); // 최종 객체 확인
```

---
layout: default
hideInToc: true
---

# Practice 2 — 대괄호 표기법과 단축 프로퍼티

동적으로 프로퍼티에 접근하고, 단축 프로퍼티로 객체를 만들어보세요.

```js{monaco-run} {autorun:false}
// ① 아래 함수를 단축 프로퍼티를 사용해 완성하세요
function createPerson(name, age, job) {
  return {
    // 여기를 완성하세요 (단축 프로퍼티 사용)
  };
}

let person = createPerson("철수", 25, "개발자");
console.log(person); // { name: "철수", age: 25, job: "개발자" }

// ② 변수 key를 사용해 person의 프로퍼티에 동적으로 접근하세요
let keys = ["name", "age", "job"];
for (let key of keys) {
  console.log(key + ": " + /* 대괄호 표기법으로 접근 */);
}
```

---
layout: default
hideInToc: true
---

# Practice 3 — for...in 활용

`for...in`으로 객체를 순회하며 여러 작업을 해보세요.

```js{monaco-run} {autorun:false}
let scores = {
  수학: 85,
  영어: 92,
  과학: 78,
  국어: 88,
};

// ① for...in으로 모든 과목과 점수를 출력하세요
// 예: "수학: 85점"

// ② 총점과 평균을 구하세요
let total = 0;
// 여기를 완성하세요

console.log("총점:", total);
console.log("평균:", total / Object.keys(scores).length);

// ③ 90점 이상인 과목만 출력하세요
```
