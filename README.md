#4주차

---


##  Vite에서 SWC가 사라진 이유

### 프로젝트 설정 확인

* `vite.config.js` 파일에서 확인 가능

### Oxc와 SWC
* 모두 Rust로 작성되어 매우 빠른 속도를 자랑하는 차세대 자바스크립트/타입스크립트 도구

#### SWC (Speedy Web Compiler)

* Babel 대체 목적
* 트렌스파이링(TS->JS)과 번들링에 특화
* 바벨을 완벽하게 대체 가능. Next.js 등 현대적인 프레임워크에서 기본으로 사용

#### Oxc (Oxidation Compiler)

* ESLint, Prettier, TypeScript 트랜스파일러 등을 모두 대체하려는 고성능 도구 모음
* SWC보다 파싱 속도 약 3배 빠름
* 정적 분석 및 린팅에 매우 강점을 가짐
* ESLint 보다 100배 이상 빠름

---

##  나의 첫 번째 컴포넌트 만들기

### Step 1: 기본 컴포넌트

```jsx
import reactLogo from './assets/react.svg'

export default function App() {
  return (
    <>
      <img className="button-icon" src={reactLogo} alt="" />
    </>
  )
}
```

### 기본 구조

```jsx
function Profile () {
  return (
    <>
    </>
  )
}
```

---

### Step 2: 컴포넌트 분리

#### App.jsx

```jsx
import Profile from "./Profile"

export default function App() {
  return (
    <>
      <Profile />
    </>
  )
}
```

#### Profile.jsx

```jsx
import reactLogo from './assets/react.svg'

export default function Profile () {
  return (
    <>
      <img className="button-icon" src={reactLogo} alt="" />
    </>
  )
}
```

---

##  컴포넌트 생성 및 사용 방법

### 생성

1. 컴포넌트 이름과 동일한 파일 생성
2. `export default` 선언
3. 함수 내부에 로직 작성
4. return 구문의 `( )` 내부에 컴포넌트에서 반환할 구문 작성

### 사용

1. `import`로 불러오기
2. `<변수명 />` 형태로 사용

---

##  컴포넌트 중첩 (Nesting)

### 개념

* 컴포넌트 내부에서 다른 컴포넌트를 호출하는 것
* 내부에 선언하는 것이 아니라 호출하는 것

---

##  React 렌더링 구조

```
컴포넌트들 → App.jsx라는 루트 컴포넌트 → main.jsx → index.html
```

### React에서 컴포넌트와 HTML 태그를 어떻게 렌더링?

* 소문자로 시작하는 태그: HTML 요소
* 대문자로 사작하는 태그: React 컴포넌트

---

##  Default Export와 Named Export

### 차이점

* 두 가지 선언 방식의 차이는 default 키워드의 사용 여부
* 두 가지 방법 모두 한 파일에서 사용할 수도 있음
* 주의할 점은 하나의 파일에는 하나의 default export만 존재할 수 있고, named export는 여러개 존재 가능
* default는 별칭 사용이 가능하지만 named는 불가능

### Default Import

* import 키워드 다음에 다른 이름으로 변수명을 선언할 수 있음
* 이 이름을 로컬 식별자 혹은 변수명이라고 함
* 예를 들어 import Banana from './Button'라고 선언하면, 이 파일안에서는 Banana라는 이름으로 사용할 수 있음
* 변수명은 대문자로 시작해야 함

### Named Export

* export하는 곳과 import하는 곳의 컴포넌트의 이름이 같아야 함
* 모듈에 여러 개의 named 컴포넌트가 있을 경우 전부 혹은 일부만 import해서 사용할 수 있음
---

##  Named Export를 권장하는 이유

* 일관성 유지
* 리팩토링 용이
* 트리 쉐이킹에 유리

---

##  JSX로 마크업 작성하기

### JSX란

* JSX는 JavaScript를 확장한 문법으로, Java Script 파일을 HTML과 비슷한 형태의 마크업을 작성할 수 있도록 해줌
* 컴포넌트를 작성하는 다른 방법도 있지만, JSX의 간결함 때문에 대부분의 React 개발자가 선호


---

##  JSX 규칙 3가지

1. 하나의 루트 엘리먼트로 반환해야 함
2. 모든 태그는 닫아줘야 함
3. 속성(attribute)는 카멜 케이스(camelCase)로 작성

* PascalCase: 컴포넌트 이름 (예: MyComponent)
* camelCase: 속성 및 변수 (예: onClick, className)

---
