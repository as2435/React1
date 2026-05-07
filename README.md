# 202230209 김태율

# 10주차(05.06)
## 이벤트 핸들러에서 Prop 사용
* ToolBar.jsx
``` jsx
import ButtonCom from "./ButtonCom"

export default function ToolBar() {
    return(
        <>
            <ButtonCom message="버튼1 클릭">
                버튼1
            </ButtonCom>
            <ButtonCom message="버튼2 클릭">
                버튼2
            </ButtonCom>
        </>
    )
}
```
* ButtonCom.jsx
``` jsx
export default function ButtonCom({message, children}) {
    function handleClick() {
        alert(message)
    }

    return(
        <button onClick={handleClick}>
            {children}
        </button>
    )
}
```
### 이벤트 핸들러를 Prop으로 전달하기
* 지금까지는 handleClick 이라는 하나의 이벤트 핸들러만 사용
    > 버튼의 이름과 출력되는 문자열은 다르지만 하나의 로직에 의해서 출력됨
* 각각의 버튼이 2가지 이상의 기능을 수행해야 한다면 이벤트 핸들러도 2개 이상이 필요하게 됨
* 구현하는 방법
  1. 조건문을 사용하여 분기하면 쉽게 구현가능
  2. 필요한 만큼 Button 컴포넌트를 만들 수 있음

다음과 같은 방법을 사용하면 관리도 쉽고 재사용도 편리한 컴포넌트를 만들 수 있음

1. 버튼 컴포넌트는 출력만 담당
2. 이벤트 핸들러는 별도의 파일에 모듈의 형태로 모아서 관리
3. 부모 컴포넌트에서 Button 컴포넌트를 호출할 때 이벤트 핸들러를 함께 전달
---
### [실습]
* ToolBar.jsx
```jsx
import ButtonCom from "./ButtonCom";
import { handlePlay, hadleStop } from "./hadle.jsx";
import sampleVideo from "../../assets/sample.mp4";

export default function ToolBar() {
  return (
    <>
      <nav>
        <ButtonCom message="videoPlayer" handle={handlePlay}>
          Play
        </ButtonCom>
        &nbsp;
        <ButtonCom message="videoPlayer" handle={hadleStop}>
          Stop
        </ButtonCom>
      </nav>
      <br />
      <section>
        <video id="videoPlayer" src={sampleVideo} controls width="350"></video>
      </section>
    </>
  );
}
```
* hadle.jsx
```jsx
import ButtonCom from "./ButtonCom";
export function handleClick({ message }) {
  alert(message);
}

export function handlePlay({ message }) {
  const videoSource = document.getElementById(message);
  if (videoSource) videoSource.play();
}
export function hadleStop({ message }) {
  const videoSource = document.getElementById(message);
  if (videoSource) videoSource.play();
}
```
**Note**
#### document.getElementById(id)
* HTML 문서에서 고유한 id 속성을 가진 요소를 찾아 JavaScript 객체로 반환하는 메서드
* id 값을 따옴표로 감싸 매개변수로 전달하며 요소가 없으면 null 반환
* 주로 HTML의 내용 변경, 스타일 수정 등 DOM 조작에 사용됨


# 9주차(04.29)

### UI를 트리 구조로 이해하기
브라우저와 모바일 플랫폼처럼 React도 React 앱을 구성하는 컴포넌트 간의 관계를 관리하고, 모델링하기 위해 트리 구조를 사용  
트리는 React 앱에서 데이터가 흐르는 방식과 렌더링 및 앱 크기를 최적화하는 방법을 이해하는 데 유용한 도구  

컴포넌트의 중요한 특징은 다른 컴포넌트들을 중첩해서 또다른 컴포넌트를 구성하는 것  
컴포넌트를 중첩하면 부모 컴포넌트와 자식 컴포넌트의 개념이 생김
이때 각 부모 컴포넌트도 또 다른 컴포넌트의 자식이 될 수 있음. 다만 자식 컴포넌트의 자식이 될 수는 없음  
React 앱을 렌더링할 때, 이 관계를 Render 트리라고 하는 트리로 모델링할 수 있음  

- 트리는 노드로 구성되어 있으며, 각 노드는 컴포넌트를 나타냄  
- React Render 트리에서 루트 노드는 앱의 Root 컴포넌트  
- DOM 트리와는 달리 Render 트리는 HTML 태그 없이 React 컴포넌트로만 구성

---

## JSX에 스타일 적용하기

### 일반 CSS
- style.css 파일을 만들어서 필요한 스타일을 정의한 후 사용할 컴포넌트에서 import
- 속성의 이름 `class` => `className` 사용
- 컴포넌트 단위로 관리하기 어렵고, 전역 스코프(global)의 클래스 이름과 충돌 가능성이 있기 때문에 주의

---

### 인라인 스타일

* HTML 에서도 인라인 스타일은 유지보수의 어려움 등의 단점이 있어 자주 사용X
* 조건부 스타일에만 제한적으로 사용
* kebab-case가 아닌 camelCase를 사용해야 함

---

### CSS-in-JS

* 자바스크립트 코드 내에서 CSS를 직접 작성, 컴포넌트 단위로 스타일을 관리하는 방법
* 라이브러리 사용 (styled-components, emotion, JSS 등)
* 스타일이 컴포넌트 내에 바인딩 되기 때문에 관리와 유지보수 용이
* props를 기반으로 한 동적(조건부) 스타일링 적용에 매우 편리
* 고유한 클래스명을 자동으로 생성하여 스타일의 충돌 방지

---

###  CSS 프레임워크

* 일반적으로 프론트엔드 개발에 많이 사용
* Tailwind CSS(클래스 단위), Bootstrap(컴포넌트 단위), bulma 등 유명한 CSS 프레임워크들이 있음
* React에서 추천하는 Tailwind CSS는 클래스를 조합하여 스타일을 작성
* 빠른 개발과 디자인의 일관성을 유지할 수 있다는 장점
* 클래스를 조합하는 과정에서 클래스 선언이 길어지기 때문에 문서의 가독성이 떨어질 수 있음

---

### CSS Module

* CSS Module은 클래스명을 `_클래스이름_해쉬값`의 형태로 자동 변환하여, 고유한 이름의 로컬 스코프(Local Scope)를 제공하는 기술
* 스타일의 충돌방지, 유지보수에도 유리
* 컴포넌트 단위로 스타일링 한다는 것이 가장 큰 특징, 컴포넌트의 재사용에도 유리하게 작용

---

### 사용 방법

#### 파일명
* `ButtonCom.module.css`형태

#### CSS 작성
* css의 내용은 일반 css의 작성법을 따름
* class 선택자로 스타일 선언
* Tag 선택자를 사용하는 것은 특별한 경우 아니면 권장하지 않음
* Tag 선택자는 CSS Module 빌드 시에 고유한 이름을 할당 받지 않고 전역으로 사용되기 때문

#### 클래스에 적용
* import의 변수명은 관행적으로 style을 사용
* JSX에서는 class 키워드 대신 className 사용
* class 이름은 객체를 사용할 때처럼 [변수명].[클래스 명]의 형태로 작성
* class 이름 전체를 중괄호로 감싸줌


#### 여러 클래스 적용

```jsx
<nav className={`${style.navBar} ${style.active}`}></nav>
```

---
* ButtonCom.jsx
```jsx
import style from "./ButtonCom.module.css"

export default function ButtonCom() {
    return(
        <>
            <h1 className={style.title}>ButtonCom 컴포넌트</h1>
            <nav className={style.navBar}>
                <button className={style.myButton}>버튼1</button>
                <button className={style.myButton}>버튼2</button>
            </nav>
        </>
    )
}
```
* ButtonCom.module.css
``` css
.title {
    font-size: 30px;
    color: blue;
}

.navBar {
    padding: 10px;
    background-color: #ccc;
    border: #000 1px solid;
}

.myButton {
    margin-right: 10px;
    background-color: green;
    border-radius: 25px;
}
```
---

### 이벤트와 상호작용

* 화면을 구성하는 요소 중 사용자의 입력에 반응해 업데이트 되는 요소가 있음
* 예를 들어 이미지 갤러리에서 특정 이미지를 클릭하면 해당 이미지는 활성 상태가 됨
* 사용자의 클릭과 같은 특정 입력을 이벤트라고 하고, 이벤트가 발생했을 때 반응하는 로직을 이벤트 핸들러라고 함

#### 응답하기
* React에서는 JSX 이벤트 핸들러를 추가할 수 있음
* 이벤트 핸들러는 클릭, 마우스 호버(hover), 폼 입력의 포커스 등 사용자와의 상호작용에 따라 유발되는 사용자 정의 함수
* <button>과 같은 내장 컴포넌트는 onClick과 같은 내장 브라우저 이벤트만 지원
* 반면 사용자 정의 컴포넌트의 경우, 이벤트 핸들러 속성에 원하는 애플리케이션별 이름을 지정할 수도 있음
---
* ButtonCom.jsx
``` jsx
import style from "./ButtonCom.module.css"

function handleClick() {
    alert("버튼 클릭")
}

export default function ButtonCom() {
    return(
        <>
            <h1 className={style.title}>ButtonCom 컴포넌트</h1>
            <nav className={style.navBar}>
                <button onClick={handleClick} className={style.myButton}>버튼1</button>
                <button onClick={handleClick} className={style.myButton}>버튼2</button>
            </nav>
        </>
    )
}
```
* 이벤트 핸들러의 이름은 handle로 시작하고 이벤트명을 뒤에 붙이는 것이 관례

#### 이벤트 핸들러 인라인 스타일 정의
* 이벤트 핸들러는 별도의 함수로 정의하는 것이 일반적이지만 JSX 내에 인라인으로 정의할 수 도 있음

  `<button onClick={() => {alert("버튼 클릭");}} >`
* 하지만 인라인 스타일의 정의는 함수가 아주 짧을 때만 예외적으로 사용할 것을 권장
* 가독성이 떨어지고, 재사용 및 모듈화에도 불편함

---

# 7주차(04.15)

---

## 데이터 전달과 렌더링

### 배열의 항목들 필터링

* heroes 데이터를 수정하면 더욱 강력한 구조화 가능
* JavaScript의 filter() 함수를 사용하여 해당하는 배우의 정보만을 반환 가능

HeroesData
```jsx
export const heroes = [
    {
        id: 0,
        casting: "스파이더맨",
        name: "피터 파커",
        power: 4
    },
    {
        id: 1,
        casting: "아이언맨",
        name: "토니 스타크",
        power: 5
    },
    {
        id: 2,
        casting: "배트맨",
        name: "브루스 웨인",
        power: 3
    },
    {
        id: 3,
        casting: "슈퍼맨",
        name: "클라크 켄트",
        power: 5
    },
    {
        id: 4,
        casting: "헐크",
        name: "로버트 브루스 배너",
        power: 4
    }
];
```

MovieHeroes
```jsx
import { heroes } from "./HeroesData";

export default function MovieHeroes() {

    const filterTests = heroes.filter(hero =>
        hero.name === "클라크 켄트"
    );

    const listHeroes = filterTests.map(hero => 
        <li>
            <p>
                {hero.name}의 배역은 {hero.casting} 입니다
            </p>
        </li>
    );

    return(
        <section>
            <h1>영화 속 영웅들</h1>
            <ul>{listHeroes}</ul>
        </section>
    )
}
```

---

#### power 값으로 필터링

```jsx
import { heroes } from "./HeroesData";

export default function MovieHeroes() {

    const filterTests = heroes.filter(hero =>
        hero.power === 5
    );

    const listHeroes = filterTests.map(hero => 
        <li>
            <p>
                {hero.name}의 배역은 {hero.casting} 입니다
            </p>
        </li>
    );

    return(
        <section>
            <h1>영화 속 영웅들</h1>
            <ul>{listHeroes}</ul>
        </section>
    )
}
```
---

### 엄격한 비교 연산자

* `===`는 `==`보다 더 엄격한 비교 연산자
* 타입 변환 없이 값과 타입을 함께 비교

---

### 화살표 함수

* 화살표 함수는 묵시적으로 `=>` 바로 뒤에 있는 식을 반환하기 때문에 `return`문이 필요 없음
* 그러나 `=>` 뒤에 `{}` 중괄호가 오는 경우에는 return을 명시적으로 작성해야 함
* => {}를 표현하는 화살표 함수를 "block body"를 가지고 있다고 함
* 이 함수를 사용하면 한 줄 이상의 코드를 작성할 수 있지만, return 문을 반드시 작성해야 함
* 일반적으로 원데이터는 복수형(heroes)를 사용하고, 임시저장소는 원데이터의 단수형(hero)를 사용

---

### key prop 사용 이유

```text
Each child in a list should have a unique "key" prop.
```

이 경고는 목록(배열)의 각 자식 요소가 고유한 'key' prop을 가져야 하는데 그렇게 설정되지 않아서 발생함

* 배열의 각 항복은 다른 목록들과 명확히 구분되는 고유한 문자열 혹은 숫자를 key로 지정해야 함
* 이것을 key prop라고 함

---

### 프래그먼트와 key prop
각 항목이 하나가 아닌 여러 개의 DOM 노드를 렌더링해야 하는 경우, 반환해야 하는 태그가 여러개 있을 경우
* 프래그먼트 `<>...</>`구문을 사용하거나, `<div>`태그 등으로 묶어서 하나로 노드로 만들어 반환해야 함
* 그러나 프래그먼트 구문으로는 key를 전달할 수 없음
* 이런 경우 `<div>` 등의 태그로 그룹화하거나, React에서 제공하는 <Fragment>컴포넌트를 사용해야함

---

### 컴포넌트를 순수하게 유지하기
순수 함수란
* 같은 입력 값을 넣으면 항상 같은 결과를 반환하는 함수
* 외부의 상태를 변경하지 않는, 즉 사이드 이펙트(side effect)가 없는 함수를 의미

---
### 의도하지 (않은) 결과 사이드 이펙트

```jsx
/* eslint-disable */
let guest = 0;

function Cup() {
    guest = guest + 1;
    return <h2>Tea cup for guest #{guest}</h2>
}

export default function TeaSet() {
    return(
        <>
            <Cup />
            <Cup />
            <Cup />
        </>
    )
}
```
```jsx
function Cup({guest}) {
    return <h2>Tea cup for guest #{guest}</h2>
}

export default function TeaSet() {
    return(
        <>
            <Cup guest={1}/>
            <Cup guest={2}/>
            <Cup guest={3}/>
        </>
    )
}
```
### 지역 변경(local mutation)

* 잘못된 예제의 문제점은 컴포넌트가 외부에 있는 기존 변수를 렌더링 중에 변경했다는 것
* 이런 사이드 이펙트를 "변경(Mutation)"라고 부르기도 함
* 순수 함수는 함수 스코프 외부의 변수나 호출 전에 생성된 객체를 변경하지 않음
* 그러나, 렌더링하는 동안에 생성된 변수와 객체를 변경하는 것은 문제가 되지 않음
```jsx
function Cup({ guest }) {
  return <h2>Tea cup for guest #{guest}</h2>;
}

export default function TeaGathering() {
  const cups = [];
  for (let i = 1; i <= 12; i++) {
    cups.push(<Cup key={i} guest={i} />);
  }
  return cups;
}
```


# 6주차(04.08)

---

## 데이터 전달과 렌더링

### 조건부 렌더링

* 컴포넌트는 조건에 따라 다른 항목을 표시해야 하는 경우가 많음
* React는 if문, 삼항 연산자와 같은 자바스크립트 문법을 사용하여 조건부로 JSX를 렌더링 할 수 있음

---

### isPacked가 true면 체크 표시 출력

* PackingList

```jsx
import Items from "./Items"

export default function PackingList() {
    return(
        <section>
            <h1>여행 짐 리스트</h1>
            <ul>
                <Items 
                    isPacked={false}
                    name="여분 옷"
                />
                <Items 
                    isPacked={false}
                    name="책"
                />
                <Items 
                    isPacked={true}
                    name="노트북"
                />
            </ul>
        </section>
    )
}
```
* Items

``` jsx
export default function Items({name, isPacked}) {
    if(isPacked) {
        return <li>{name}✅</li>
    }
    return <li>{name}</li>
}
```
조건문에 동일한 코드 `return <li>{name}</li>`가 중복됨

유지보수 어려워짐

---

## 삼항 연산자를 사용하여 중복 코드 제거

### 1번
```jsx
export default function Items({name, isPacked}) {
    return <li>{name} {isPacked ? "✅" : ""}</li>
}
```
### 2번
```jsx
export default function Items({name, isPacked}) {
    return <li>{isPacked ? name + "✅" : name}</li>
}
```
---
### `<del>` 태그 추가

```jsx
export default function Items({name, isPacked}) {
    return(
        <li>
            {isPacked ? (<del>{name + "✅"}</del>) : (name)}
        </li>
    )
}
```
---
### 논리 연산자 AND (&&) 사용
```jsx
export default function Items({name, isPacked}) {
    return(
        <li>
            {name} {isPacked && "✅"}
        </li>
    )
}
```
* JavaScript &&표현식은 왼쪽이 true면 오른쪽의 값을 반환, 조건이 false면 전체 표현식이 false가 됨
* React는 false를 null 또는 undefined처럼 JSX 트리의 "구멍"으로 간주하고 그자리에 아무것도 렌더링하지 않음
* && 왼쪽에 숫자를 두면 안됨
* JavaScript는 조건을 테스트하기 위해 표현식 왼쪽을 자동으로 부울(bool)로 변환. 왼쪽이 숫자 0이면 전체 식이(0)을 얻게 되고, React는 0을 렌더링
---
### 변수에 조건부 JSX 할당
```jsx
export default function Items({name, isPacked}) {
    let itemContent = name;

    if(isPacked) {
        itemContent = <del>{name + "✅"}</del>
    }

    return(
        <li>
            {itemContent}
        </li>
    )
}
```
* let 변수는 재할당 가능
* 조건에 따라 JSX를 변수에 담아서 사용
---
## 리스트 렌더링
여러 데이터를 동일한 형태로 출력할 때 사용

배열과 map() 함수를 활용하여 렌더링

### 배열을 이용한 렌더링
```jsx
const heroes = [
    "스파이더맨: 피터 파커",
    "아이언맨: 토니 스타크",
    "배트맨: 브루스 웨인",
    "슈퍼맨: 클라크 켄트",
    "헐크: 로버트 브루스 배너"
];

export default function MovieHeroes() {
    const listHeroes = heroes.map(hero => <li>{hero}</li>);

    return(
        <section>
            <h1>영화 속 영웅들</h1>
            <ul>
                {listHeroes}
            </ul>
        </section>
    )
}
```
---

# 5주차(04.01)

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

# 4주차(03.25)

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
