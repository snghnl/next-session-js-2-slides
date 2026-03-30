---
layout: section
---
# JSON과 메서드
객체를 문자열로, 문자열을 객체로

---
layout: default
hideInToc: true
---
# JSON이란?

**JSON (JavaScript Object Notation)** — 데이터를 교환하기 위한 범용 텍스트 포맷

```js
// 자바스크립트 객체
let user = { name: "John", age: 30 };

// JSON 문자열 (네트워크 전송 가능)
'{"name":"John","age":30}'
```

<v-click>

자바스크립트 객체와 비슷하지만 **규칙이 더 엄격합니다:**

- 키는 반드시 **큰따옴표** `"key"`
- 값의 문자열도 반드시 **큰따옴표** `"value"`
- 함수, `undefined`, `Symbol` 사용 불가

</v-click>

<v-click>

```
JavaScript  →  JSON.stringify()  →  JSON 문자열
JSON 문자열  →  JSON.parse()     →  JavaScript 객체
```

</v-click>

---
layout: default
hideInToc: true
---
# JSON.stringify — 객체 → 문자열

```js
let student = {
  name: "John",
  age: 30,
  isAdmin: false,
  courses: ["html", "css", "js"],
  wife: null
};

let json = JSON.stringify(student);

console.log(typeof json); // string
console.log(json);
// {"name":"John","age":30,"isAdmin":false,"courses":["html","css","js"],"wife":null}
```

<v-click>

**자동으로 무시되는 프로퍼티**

```js
let user = {
  sayHi() { alert("Hello"); }, // 메서드 → 무시
  [Symbol("id")]: 123,          // 심볼 → 무시
  something: undefined          // undefined → 무시
};

console.log(JSON.stringify(user)); // {}
```

</v-click>

---
layout: default
hideInToc: true
---
# JSON.stringify — 가독성 옵션

`JSON.stringify(value, replacer, space)`

**세 번째 인수 `space`** — 들여쓰기 공백 수

```js
let user = {
  name: "John",
  age: 25,
  roles: { isAdmin: false, isEditor: true }
};

console.log(JSON.stringify(user, null, 2));
```

<v-click>

```json
{
  "name": "John",
  "age": 25,
  "roles": {
    "isAdmin": false,
    "isEditor": true
  }
}
```

> 네트워크 전송 시엔 `space` 없이, 디버깅/로깅 시엔 `space: 2` 사용

</v-click>

---
layout: default
hideInToc: true
---
# JSON.parse — 문자열 → 객체

```js
// 서버에서 받은 JSON 문자열
let userData = '{"name":"John","age":35,"isAdmin":false,"friends":[0,1,2,3]}';

let user = JSON.parse(userData);

console.log(user.name);       // John
console.log(user.friends[1]); // 1
```

<v-click>

**흔한 실수 — 잘못된 JSON 형식**

```js
let json = `{
  name: "John",        // ❌ 키에 따옴표 없음
  "surname": 'Smith',  // ❌ 작은따옴표 사용
  "birthday": new Date(2000, 2, 3)  // ❌ new 사용 불가
}`;

JSON.parse(json); // SyntaxError 발생!
```

</v-click>

---
layout: default
hideInToc: true
---
# reviver — 날짜 등 타입 복원

`JSON.parse` 후 날짜 문자열은 그냥 `string`으로 남습니다.

```js
let str = '{"title":"Conference","date":"2017-11-30T12:00:00.000Z"}';

let meetup = JSON.parse(str);
console.log(meetup.date.getDate()); // ❌ Error! (date는 문자열)
```

<v-click>

**reviver 함수로 타입 복원**

```js
let meetup = JSON.parse(str, function(key, value) {
  if (key === "date") return new Date(value);
  return value;
});

console.log(meetup.date.getDate()); // ✅ 30
```

</v-click>

---
layout: default
hideInToc: true
---
# 핵심 정리

<v-click>

- `JSON.stringify(obj)` → 객체를 JSON **문자열**로 변환

</v-click>

<v-click>

- `JSON.parse(str)` → JSON 문자열을 **객체**로 변환

</v-click>

<v-click>

- JSON은 키/값 모두 **큰따옴표** 필수, 함수·심볼·`undefined` 불가

</v-click>

<v-click>

- `stringify(obj, null, 2)` → 들여쓰기로 가독성 향상

</v-click>

<v-click>

- 순환 참조 객체는 stringify 불가 (에러 발생)

</v-click>

<v-click>

```js
// 객체 깊은 복사 트릭
let clone = JSON.parse(JSON.stringify(original));
```

</v-click>

---
layout: section
hideInToc: true
---
# Practice
JSON 실습

---
layout: default
hideInToc: true
---
# Practice 1 — JSON.stringify 기본

<div class="overflow-y-auto max-h-96">

```js{monaco-run} {autorun:false, height:'220px'}
let product = {
  id: 101,
  name: "노트북",
  price: 1500000,
  inStock: true,
  tags: ["전자제품", "컴퓨터"],
  seller: undefined,     // undefined
  getPrice() {           // 메서드
    return this.price;
  }
};

// ① JSON.stringify로 product를 JSON 문자열로 변환하세요
// let json = ???

// ② 들여쓰기 2칸으로 보기 좋게 출력해보세요
// let prettyJson = ???

console.log(json);
console.log("---");
console.log(prettyJson);
// undefined와 메서드는 결과에서 사라집니다!
```

</div>

---
layout: default
hideInToc: true
---
# Practice 2 — JSON.parse와 활용

```js{monaco-run} {autorun:false, height:'220px'}
// 서버에서 받은 JSON 응답이라고 가정합니다
let response = `{
  "status": 200,
  "users": [
    {"id": 1, "name": "철수", "score": 85},
    {"id": 2, "name": "영희", "score": 92},
    {"id": 3, "name": "민준", "score": 73}
  ]
}`;

// ① JSON.parse로 객체로 변환하세요
// let data = ???

// ② users 배열에서 score가 80 이상인 유저의 name만 출력하세요
// (힌트: filter + map)

// ③ 전체 users의 평균 score를 구하세요
// (힌트: reduce)

// 예상 출력:
// 고득점자: ["철수", "영희"]
// 평균 점수: 83.33...
```

---
layout: default
hideInToc: true
---
# Practice 3 — 직렬화 & 역직렬화 왕복

```js{monaco-run} {autorun:false, height:'220px'}
// 객체 → JSON → 객체 왕복 여행

let original = {
  title: "JavaScript 스터디",
  members: ["철수", "영희", "민준"],
  info: {
    level: "beginner",
    sessions: 8
  }
};

// ① original을 JSON 문자열로 변환하세요
// let jsonStr = ???

// ② jsonStr을 다시 객체로 변환하세요
// let restored = ???

// ③ original과 restored가 같은 내용인지 확인하세요
//    (=== 비교 결과와 이유를 주석으로 설명해보세요)
console.log(original === restored);     // ?
console.log(JSON.stringify(original) === JSON.stringify(restored)); // ?

// ④ restored.members에 "지수"를 추가해도 original에 영향이 없음을 확인하세요
restored.members.push("지수");
console.log(original.members);  // ?
console.log(restored.members);  // ?
```

---

---
