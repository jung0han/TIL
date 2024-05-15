## 8.1 리액트 컴포넌트의 타입

리액트 내장 타입 중에는 역할이 명확한 것도 있지만 역할이 비슷해 보이는 타입도 있기 때문에 어떤 것을 사용할 지 헷갈릴 수 있다.

### 1. 클래스 컴포넌트 타입

React.Component와 React.PureComponent는 props와 상태를 제네릭으로 받는다.

### 2. 함수 컴포넌트 타입

함수 표현식을 사용하여 함수 컴포넌트를 선언할 때 가장 많이 볼 수 있는 형태는 React.FC 또는 React.VFC로 타입을 지정하는 것이다. React.VFC는 @type/react 16.9.4버전에서 추가되었으며 React.VFC는 children props를 허용하지 않는다. 그러나 react v18부터 React.VFC가 삭제되고 React.FC에서 children이 사라졌으므로 React.FC 또는 props 타입, 반환 타입을 직접 지정해줘야 한다.

### 3. Children props 타입 지정

가장 보편적인 children 타입은 ReactNode | undefined이며 ReactNode는 ReactElement 외에도 boolean, number 등 여러 타입을 포함하고 있으므로 구체적으로 타이핑하는 용도에는 적합하지 않다. 예를 들어 특정 문자열만 허용하기 위해서는 children에 대해 추가로 타이핑 해줘야 한다.

### 4. render 메서드와 함수 컴포넌트의 반환 타입



### 5. ReactElement, ReactNode, JSX.Element 활용하기

### 6. 사용 예시

### 7. 리액트에서 기본 HTML 요소 타입 활용하기

## 8.2 타입스크립트로 리액트 컴포넌트 만들기

### 1. JSX로 구현된 Select 컴포넌트

### 2. JSDocs로 일부 타입 지정하기

### 3. props 인터페이스 적용하기

### 4. 리액트 이벤트

### 5. 훅에 타입 추가하기

### 6. 제네릭 컴포넌트 만들기

### 7. HTMLAttributes, ReactProps 적용하기

### 8. styled-components를 활용한 스타일 정의

### 9. 공변성과 반공변성

## 8.3 정리