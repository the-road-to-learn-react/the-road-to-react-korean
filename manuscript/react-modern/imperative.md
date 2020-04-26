## 명령형 리액트

리액트는 본질적으로 JSX로 시작하고 훅으로 끝나는 선언형입니다. JSX에서는 리액트에게 **어떻게**가 아니라 **무엇**을 렌더링할지 알려줍니다. 사이드 이펙트 훅 (useEffect)에서는 **어떻게** 달성할지가 아니라 **무엇**을 언제 달성해야 하는지를 표현합니다. 하지만 때때로 다음과 같이 JSX의 렌더링 된 엘레먼트를 명령형으로 접근해야 하는 경우도 있습니다.

* DOM API를 통해 엘레먼트 읽기/쓰기
  * 엘레먼트의 넓이나 높이 측정 (읽기)
  * 입력 필드의 포커스 상태 설정 (쓰기)
* 더 복잡한 애니메이션 구현
  * 전환 설정
  * 전환 조정
* 서드 파티 라이브러리 통합
  * [D3](https://d3js.org/) 은 자주 쓰이는 명령형 차트 라이브러리입니다.

리액트에서 명령형 프로그래밍은 장황하고 직관에 반하는 경우가 많기 때문에 입력 필드의 포커스를 설정하는 작은 예시만 살펴보겠습니다. 선언형 방법에서는 입력 필드의 자동 포커스 속성을 설정하기만 하면 됩니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const InputWithLabel = ({ ... }) => (
  <>
    <label htmlFor={id}>{children}</label>
    &nbsp;
    <input
      id={id}
      type={type}
      value={value}
# leanpub-start-insert
      autoFocus
# leanpub-end-insert
      onChange={onInputChange}
    />
  </>
);
~~~~~~~

위의 코드도 동작하지만, 재사용 가능한 컴포넌트 중 하나가 한 번만 렌더링 되는 경우에만 해당합니다. 예를 들어, App 컴포넌트가 두 InputWithLabel 컴포넌트를 렌더링하면 마지막에 렌더링 된 컴포넌트만 자동 포커스를 받습니다. 하지만 여기에는 재사용 가능한 리액트 컴포넌트가 있어 전용 prop을 전달하고 개발자가 입력 필드의 자동 포커스 여부를 결정하도록 할 수 있습니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

  return (
    <div>
      <h1>My Hacker Stories</h1>

      <InputWithLabel
        id="search"
        value={searchTerm}
# leanpub-start-insert
        isFocused
# leanpub-end-insert
        onInputChange={handleSearch}
      >
        <strong>Search:</strong>
      </InputWithLabel>

      ...
    </div>
  );
};
~~~~~~~

`isFocused`만 속성으로 사용하는 것은 `isFocused={true}`와 동등합니다. 컴포넌트 내에서 이 새로운 prop을 입력 필드의 `autoFocus` 속성에 사용하세요.

{title="src/App.js",lang="javascript"}
~~~~~~~
const InputWithLabel = ({
  id,
  value,
  type = 'text',
  onInputChange,
# leanpub-start-insert
  isFocused,
# leanpub-end-insert
  children,
}) => (
  <>
    <label htmlFor={id}>{children}</label>
    &nbsp;
    <input
      id={id}
      type={type}
      value={value}
# leanpub-start-insert
      autoFocus={isFocused}
# leanpub-end-insert
      onChange={onInputChange}
    />
  </>
);
~~~~~~~

포커스 기능은 작동하지만, 여전히 선언형 구현을 사용하고 있습니다. **어떻게**가 아니라 **무엇**을 해야하는지를 정의하고 있기 때문입니다. 이렇게 선언형 접근법으로도 할 수 있지만, 이 시나리오를 명령형 접근으로 리팩토링 해보겠습니다. 입력 필드가 렌더링되면 그것의 DOM API를 통해 `focus()` 메서드를 프로그래밍적으로 실행합니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const InputWithLabel = ({
  id,
  value,
  type = 'text',
  onInputChange,
  isFocused,
  children,
}) => {
# leanpub-start-insert
  // A
  const inputRef = React.useRef();
# leanpub-end-insert

# leanpub-start-insert
  // C
  React.useEffect(() => {
    if (isFocused && inputRef.current) {
      // D
      inputRef.current.focus();
    }
  }, [isFocused]);
# leanpub-end-insert

  return (
    <>
      <label htmlFor={id}>{children}</label>
      &nbsp;
# leanpub-start-insert
       {/* B */}
# leanpub-end-insert
      <input
# leanpub-start-insert
        ref={inputRef}
# leanpub-end-insert
        id={id}
        type={type}
        value={value}
        onChange={onInputChange}
      />
    </>
  );
};
~~~~~~~

모든 필수적인 단계를 주석으로 표시하고 단계별로 설명합니다.

* (A) **useRef** 훅으로 `ref`를 생성하세요. `ref` 개체는 리액트 컴포넌트의 생명주기 동안 그대로 유지되는 지속적인 값입니다. 여기에는 `ref` 개체와 달리 변경될 수 있는 `current` 속성이 포함되어 있습니다.

* (B) 다음으로, `ref`는 JSX로 미리 지정한 입력 필드의 `ref` 속성으로 전달되고 엘레먼트 인스턴스는 변경 가능한 `current` 속성에 할당됩니다.

* (C) useEffect 훅으로 리액트 생명주기에 들어가 컴포넌트가 렌더링될 때 (또는 그것의 의존성이 변할 때) 입력 필드에 포커스를 수행합니다.

* (D) 마지막으로, `ref`가 입력 필드의 `ref` 속성에 전달되었기 때문에 그것의 `current` 속성으로 엘레먼트에 접근 가능합니다. 사이드 이펙트로 포커스를 프로그래밍적으로 실행하세요. 단, `isFocused`가 설정되고 `current` 속성이 존재할 때에만 해당합니다.

위의 예제를 통해 선언형 프로그래밍에서 명령형 프로그래밍으로 어떻게 이동하는지를 배웠습니다. 이제는 선언형으로 프로그래밍하는 것이 항상 가능하기 때문에 명령형 접근법이 필수적이며, 리액트의 DOM API에 대해 배우기 위해 필요합니다.

### 읽어보기
* [useRef 훅](https://reactjs.org/docs/hooks-reference.html#useref)에 대해 더 읽어보세요. 

### 실습하기
* [마지막 장의 소스 코드](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/Imperative-React)를 확인하세요.
* [마지막 장의 변경 사항](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/React-Component-Composition...hs/Imperative-React?expand=1)을 확인하세요.
