## 리액트의 폼

앞서 클릭을 통해 데이터를 명시적으로 가져오는 새로운 버튼에 대해 알아보았습니다. 이번에는 라벨이 있는 검색어 입력 필드와 버튼을 캡슐화하는 적절한 HTML 폼으로 발전 시켜 보겠습니다.

리액트 JSX에서의 폼은 HTML과 크게 다르지 않습니다. HTML과 자바스크립트로 두 단계의 리팩토링을 하겠습니다. 먼저 입력 필드와 버튼을 HTML 폼 요소로 감싸세요.

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

  return (
    <div>
      <h1>My Hacker Stories</h1>

# leanpub-start-insert
      <form onSubmit={handleSearchSubmit}>
# leanpub-end-insert
        <InputWithLabel
          id="search"
          value={searchTerm}
          isFocused
          onInputChange={handleSearchInput}
        >
          <strong>Search:</strong>
        </InputWithLabel>

# leanpub-start-insert
        <button type="submit" disabled={!searchTerm}>
# leanpub-end-insert
          Submit
        </button>
# leanpub-start-insert
      </form>
# leanpub-end-insert

      <hr />

      ...
    </div>
  );
};
~~~~~~~

`handleSearchSubmit` 핸들러를 버튼에 전달하지 않고 새로운 폼 요소에 사용합니다. 버튼은 `submit`이라는 새 `type` 속성을 받는데, 이는 폼 요소가 버튼이 아닌 클릭을 처리한다는 것을 나타냅니다.

핸들러는 폼 이벤트에 사용되므로 리액트의 합성 이벤트(synthetic event)에서 `preventDefault`를 실행합니다. 이렇게 해서 브라우저를 다시 로드하는 HTML 폼의 기본 동작을 막을 수 있습니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

# leanpub-start-insert
  const handleSearchSubmit = event => {
# leanpub-end-insert
    setUrl(`${API_ENDPOINT}${searchTerm}`);

# leanpub-start-insert
    event.preventDefault();
# leanpub-end-insert
  };

  ...
};
~~~~~~~

이제 키보드의 `Enter` 키를 이용하여 검색 기능을 실행할 수 있습니다. 다음 두 단계에서는 컴포넌트를 독립적인 SearchForm 컴포넌트로 분리합니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
# leanpub-start-insert
const SearchForm = ({
  searchTerm,
  onSearchInput,
  onSearchSubmit,
}) => (
  <form onSubmit={onSearchSubmit}>
    <InputWithLabel
      id="search"
      value={searchTerm}
      isFocused
      onInputChange={onSearchInput}
    >
      <strong>Search:</strong>
    </InputWithLabel>

    <button type="submit" disabled={!searchTerm}>
      Submit
    </button>
  </form>
);
# leanpub-end-insert
~~~~~~~

새로운 컴포넌트는 App 컴포넌트에서 사용합니다. List 컴포넌트에 props(`stories.data`)로 전달된 데이터를 가져오기 위해 App 컴포넌트에서 상태를 이용하므로 App 컴포넌트는 폼의 상태를 계속해서 관리합니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

  return (
    <div>
      <h1>My Hacker Stories</h1>

# leanpub-start-insert
      <SearchForm
        searchTerm={searchTerm}
        onSearchInput={handleSearchInput}
        onSearchSubmit={handleSearchSubmit}
      />
# leanpub-end-insert

      <hr />

      {stories.isError && <p>Something went wrong ...</p>}

      {stories.isLoading ? (
        <p>Loading ...</p>
      ) : (
        <List list={stories.data} onRemoveItem={handleRemoveStory} />
      )}
    </div>
  );
};
~~~~~~~

리액트에서의 폼은 HTML과 비슷합니다. 입력 필드와 데이터를 전송하는 버튼이 있다면 `onSubmit` 핸들러가 있는 폼 요소로 HTML을 감싸서 구조를 만들 수 있습니다. 데이터 전송을 실행하는 버튼에 "submit" `type`만 있으면 됩니다.

### 실습하기

* [마지막 장의 소스 코드](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/Forms-in-React)를 확인하세요.
  * [마지막 장의 변경 사항](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/Async-Await-in-React...hs/Forms-in-React?expand=1)을 확인하세요.
* `preventDefault`를 사용하지 않고 코드를 작성해보세요.
* [리액트 이벤트의 preventDefault](https://www.robinwieruch.de/react-preventdefault)에 대해 자세히 알아보세요.
* [리액트 컴포넌트 구성](https://www.robinwieruch.de/react-component-composition)에 대해 자세히 알아보세요.