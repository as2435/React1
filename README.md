# 4주차

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

# 5주차

---
## JSX로 마크업 작성하기

### 태그 (Tag)
- HTML과 같은 마크업에서 요소를 표시하는 기호
- 예: `<div>`, `<li>`

### 엘리먼트 (Element)
- DOM의 구성 단위 (DOM 노드)
- 구조: 여는 태그 + 내용 + 닫는 태그
- 예:
 ```
   <p>엘리먼트 설명</p>
 ```

### 어트리뷰트 (Attribute)

* 태그의 행동을 제어하거나, 엘리먼트에 추가적인 정보 제공
* `<img>` 태그의 src같은 정적 속성 같은 것
* 예:
  ```
  <img src="image.png" />
  ```

### 프로퍼티 (Property)

* DOM 객체 내부의 동적 속성
* JavaScript로 제어 가능
* 예:

  * 사용자가 input에 입력 → value 프로퍼티 변경
  * HTML의 value 어트리뷰트는 그대로 유지

---

## JSX에서 자바스크립트 사용하기

### 사용 방법 4가지

1. 문자열 전달 (따옴표)
2. `{}`로 변수 사용
3. `{}`로 함수 호출
4. `{}`로 객체 사용

### 변수 사용

```jsx
export default function UseJsx () {
    const name = "React"

    return (
        <>
            <h1>Hello, {name}</h1>
        </>
    )
}
```

### 함수 사용

```jsx
export default function UseJsx () {
    const name = "React"

    function formatDate(date){
        return new Intl.DateTimeFormat(
            "en-US", { weekday: "long" }
        ).format(date);
    }

    return (
        <>
            <h1>Hello, {name}</h1>
            <p>Today is {formatDate(new Date())}</p>
        </>
    )
}
```

---

## 데이터 전달과 렌더링

### 개요

* React 컴포넌트는 props를 이용해 서로 통신
* 부모 컴포넌트는 자식 컴포넌트에게 props를 통해 데이터를 전달
* props는 HTML의 속성과 비슷해 보이지만 객체, 배열, 함수를 포함한 모든 JavaScript 값을 전달 가능

### Props의 데이터 전달

* Props는 부모 컴포넌트가 자식 컴포넌트에게 전달되는 데이터 꾸러미라고 할 수 있음
* React에서는 props를 통해 JSX 태그에 정보를 전달
* `<img>`태그에 전달할 수 있는 props는 HTML 표준으로 이미 정의되어 있음

### 컴포넌트에 props 전달하기

#### 부모 컴포넌트
- 자식 컴포넌트를 자신의 구조 안에 포함 (import 및 호출)
- 자식에게 props를 통해 데이터 전달

#### 자식 컴포넌트
- 부모로부터 전달받은 props를 이용해 UI 생성
- 생성된 결과를 반환
- 독립적으로 재사용 가능

#### Props의 특징

- 일방통행  

- 읽기 전용  

- 다양한 타입  

### Props의 기본값 지정

* 부모 컴포넌트로부터 전달받은 prop이 없을 때는 기본값을 지정해줄 수 있음  
* 기본값을 지정할 때는 변수 뒤에 = 과 함께 기본값을 넣어줌  
* 이 기본값은 prop이 없거나(undefined)로 전달될 때 사용됨
* {null} 또는 {0}으로 전달된다면, 기본값은 사용되지 않음

### JSX spread 문법으로 props 전달하기

* 모든 props를 한 번에 자식 컴포넌트에 전달하는 방법은 자바스크립트의 spread 문법을 이용
* 자바스크립트에서 spread 문법은 객체를 펼치는 문법
* `<User {...props} />` 는 `<User name={props.name} age={props.age} />`과 동일

#### 이 방법은 주로 다음과 같은 경우에 사용

* 전달받은 props 그대로 넘겨줄 때 (Props Forwarding): 부모 컴포넌트가 받은 props를 중간 단계 컴포넌트가 그대로 자식에게 전달할 때 유용

기본 HTML 속성 확장할 때: 버튼 등을 만들 때 onClick, type, disabled 같은 표준 HTML 속성들을 한꺼번에 전달 가능

전달하고자 하는 props의 수가 너무 많을 때: props의 수가 많아서 가독성이 떨어질 때 간결하게 작성 가능

---
