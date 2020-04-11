## 리액트 컴포넌트 구성

HTML 엘리먼트와 동일한 방식으로 React 안에서 엘리먼트를 사용하는 방법을 알아 봅시다.

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
        onInputChange={handleSearch}
# leanpub-start-insert
      >
        Search
      </InputWithLabel>
# leanpub-end-insert

      ...
    </div>
  );
};
~~~~~~~

`label`의 prop 을 사용하는 대신 컴포넌트의 엘리먼트 태그 사이에 "Search :"라는 텍스트를 삽입했습니다. InputWithLabel 컴포넌트에서 **리액트의 children** prop를 통해 정보에 접근 할 수 있습니다. `label`의 prop를 사용하는 대신 children prop을 사용하여 원하는 곳에서 전달된 모든 것을 렌더링하십시오.

{title="src/App.js",lang="javascript"}
~~~~~~~
const InputWithLabel = ({
  id,
  value,
  type = 'text',
  onInputChange,
# leanpub-start-insert
  children,
# leanpub-end-insert
}) => (
  <>
# leanpub-start-insert
    <label htmlFor={id}>{children}</label>
# leanpub-end-insert
    &nbsp;
    <input
      id={id}
      type={type}
      value={value}
      onChange={onInputChange}
    />
  </>
);
~~~~~~~

이제 리액트 컴포넌트의 엘리먼트는 기본 HTML과 유사하게 작동합니다. 컴포넌트의 엘리먼트 사이에 전달되는 모든 것은 컴포넌트의 하위 요소로 접근하여 어딘가에 렌더링 할 수 있습니다. 때때로 리액트 컴포넌트를 사용할 때, 컴포넌트 내부에 렌더링할 항목을 외부로부터 더 자유롭게 만들기를 원합니다.

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
        onInputChange={handleSearch}
      >
# leanpub-start-insert
        <strong>Search:</strong>
# leanpub-end-insert
      </InputWithLabel>

      ...
    </div>
  );
};
~~~~~~~

이 리액트 기능으로 리액트 컴포넌트를 서로 구성 할 수 있습니다. 우리는 자바스크립트 문자열과 HTML <strong>요소로 싸인 문자열과 함께 사용 했지만 여기서 끝나지 않습니다. 리액트 children를 통해 컴포넌를 전달할 수도 있습니다.

### 실습하기:

* [마지막 장의 소스 코드를 확인하세요](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/React-Component-Composition).
  * Confirm the [마지막 장의 변경 사항을 확인하세요](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/Reusable-React-Component...hs/React-Component-Composition?expand=1).
* 리액트 컴포넌트 구성 ([0](https://www.robinwieruch.de/react-component-composition), [1](https://reactjs.org/docs/composition-vs-inheritance.html))에 대해 자세히 알아보세요.
* InputWithLabel 컴포넌트에 간단한 문자열을 렌더링하는 `children`컴포넌트를 만드십시오.
