---
layout: section
---
# 구조 분해 할당
객체와 배열을 변수로 간결하게 분해하기

---
layout: default
hideInToc: true
---
# 배열 구조 분해

배열 요소를 변수로 한 번에 꺼낼 수 있습니다.

```js
// 기존 방식
let arr = ["Bora", "Lee"];
let firstName = arr[0];
let surname   = arr[1];
```

<v-click>

```js
// 구조 분해 할당
let [firstName, surname] = ["Bora", "Lee"];

console.log(firstName); // Bora
console.log(surname);   // Lee
```

</v-click>

<v-click>

```js
// split과 함께 활용
let [first, last] = "Bora Lee".split(" ");

// 요소 건너뛰기 (쉼표로 생략)
let [name1, , title] = ["Julius", "Caesar", "Consul"];
console.log(title); // Consul
```

</v-click>

---
layout: default
hideInToc: true
---
# 배열 구조 분해 — 나머지 & 기본값

**나머지 요소 `...rest`**

```js
let [name1, name2, ...rest] = ["Julius", "Caesar", "Consul", "of Rome"];

console.log(name1); // Julius
console.log(name2); // Caesar
console.log(rest);  // ["Consul", "of Rome"]
```

<v-click>

**기본값 설정**

```js
let [name = "Guest", role = "User"] = ["철수"];

console.log(name); // 철수 (배열에서 받아온 값)
console.log(role); // User (기본값)
```

</v-click>

<v-click>

**변수 값 교환 트릭**

```js
let a = 1, b = 2;
[a, b] = [b, a];
console.log(a, b); // 2 1
```

</v-click>

---
layout: default
hideInToc: true
---
# 객체 구조 분해

객체 프로퍼티를 변수로 꺼냅니다. **순서는 상관없습니다.**

```js
let options = { title: "Menu", width: 100, height: 200 };

let { title, width, height } = options;

console.log(title);  // Menu
console.log(width);  // 100
console.log(height); // 200
```

<v-click>

**다른 이름의 변수에 할당 (콜론 사용)**

```js
let { width: w, height: h, title } = options;
// width → w, height → h

console.log(w); // 100
console.log(h); // 200
```

</v-click>

---
layout: default
hideInToc: true
---
# 함수 매개변수에서 구조 분해

매개변수가 많을 때 **객체로 받아서 구조 분해**하면 순서 걱정이 없습니다.

```js
// ❌ 순서를 외워야 하는 불편한 방식
function showMenu(title, width, height, items) { ... }
showMenu("My Menu", undefined, undefined, ["Item1"]);
```

<v-click>

```js
// ✅ 구조 분해로 받는 방식
function showMenu({ title = "Untitled", width = 200, height = 100, items = [] }) {
  console.log(`${title} ${width}x${height}`);
  console.log(items);
}

let options = { title: "My Menu", items: ["Item1", "Item2"] };
showMenu(options); // My Menu 200x100
```

</v-click>

<v-click>

**인수 없이도 호출 가능하게 — 기본값 `= {}`**

```js
function showMenu({ title = "Menu", width = 100 } = {}) {
  console.log(title, width);
}

showMenu(); // Menu 100 (에러 없음)
```

</v-click>

---
layout: default
hideInToc: true
---
# 핵심 정리

<v-click>

**배열 구조 분해**
```js
let [a, b, ...rest] = [1, 2, 3, 4];
```

</v-click>

<v-click>

**객체 구조 분해**
```js
let { prop: varName = default, ...rest } = object;
```

</v-click>


<v-click>
<div text="xs"> 

| 기능 | 문법 |
|---|---|
| 기본값 | `let [a = 1] = []` |
| 이름 변경 | `let { a: newName } = obj` |
| 나머지 | `let [a, ...rest] = arr` |
| 중첩 | `let { size: { w } } = obj` |
| 함수 매개변수 | `function fn({ a = 1 } = {})` |
</div>

</v-click>

---
layout: section
hideInToc: true
---
# Practice
구조 분해 할당 실습

---
layout: default
hideInToc: true
---
# Practice 1 — 배열 구조 분해

```js{monaco-run} {autorun:false, height:'220px'}
// ① 아래 배열을 구조 분해해서 변수에 담으세요
let colors = ["빨강", "초록", "파랑", "노랑", "보라"];

// first: "빨강"
// second: "초록"
// rest: ["파랑", "노랑", "보라"]

// let [first, second, ...rest] = ???

console.log(first);  // 빨강
console.log(second); // 초록
console.log(rest);   // ["파랑", "노랑", "보라"]

// ② 두 변수의 값을 교환하세요 (임시 변수 없이!)
let x = 10, y = 20;
// [???, ???] = ???

console.log(x, y); // 20 10
```

---
layout: default
hideInToc: true
---
# Practice 2 — 객체 구조 분해

```js{monaco-run} {autorun:false, height:'220px'}
let user = {
  name: "철수",
  age: 20,
  role: "admin",
  score: 95
};

// ① name, age를 구조 분해로 꺼내세요

// ② role을 "userRole"이라는 변수명으로 꺼내세요

// ③ score를 꺼내되, 없을 경우 기본값 0을 사용하세요
//    또한 "point"라는 변수에 저장하세요 (콜론 + 기본값 조합)

// ④ 나머지 프로퍼티를 rest 객체에 담으세요

console.log(name, age);   // 철수 20
console.log(userRole);    // admin
console.log(point);       // 95
console.log(rest);        // { role: "admin", score: 95 } 또는 나머지
```


---
layout: default
hideInToc: true
---
# Practice 3 — 함수 매개변수 구조 분해

```js{monaco-run} {autorun:false, height: '220px'}
// 아래 함수를 구조 분해 매개변수 방식으로 리팩토링하세요

// ❌ 기존 방식
// function createProfile(name, age, role, isActive) { ... }

// ✅ 구조 분해 방식으로 작성하세요
// - name: 기본값 "익명"
// - age: 기본값 0
// - role: 기본값 "user"
// - isActive: 기본값 true
// - 인수 없이도 호출 가능하도록 = {} 추가

function createProfile(/* 여기를 수정하세요 */) {
  return `[${role}] ${name} (${age}세) - ${isActive ? "활성" : "비활성"}`;
}

console.log(createProfile({ name: "철수", age: 20 }));
// [user] 철수 (20세) - 활성

console.log(createProfile({ name: "영희", role: "admin", isActive: false }));
// [admin] 영희 (0세) - 비활성

console.log(createProfile());
// [user] 익명 (0세) - 활성
```
