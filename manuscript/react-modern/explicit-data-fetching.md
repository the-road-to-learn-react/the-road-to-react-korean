## 리액트로 명시적 데이터 가져오기

입력 필드에 글자가 입력될 때마다 모든 데이터를 다시 가져오는 것은 최적의 방법이 아닙니다. 서드 파티 API를 이용하여 데이터를 가져오기 때문에 그 내부 상황은 알 수 없습니다. 하지만 결국은 데이터 대신 오류를 반환하는 [속도 제어](https://en.wikipedia.org/wiki/Rate_limiting)를 초래할 것입니다.

이러한 문제를 해결하기 위해 암시적 데이터 (다시) 가져오기에서 명시적 데이터 (다시) 가져오기로 구현 세부사항을 변경합니다. 즉, 애플리케이션은 확인 버튼이 클릭될 경우에만 데이터를 다시 가져올 것입니다. 먼저, JSX에 확인을 위한 버튼 엘레멘트를 추가하세요.

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
        isFocused
# leanpub-start-insert
        onInputChange={handleSearchInput}
# leanpub-end-insert
      >
        <strong>Search:</strong>
      </InputWithLabel>

# leanpub-start-insert
      <button
        type="button"
        disabled={!searchTerm}
        onClick={handleSearchSubmit}
      >
        Submit
      </button>
# leanpub-end-insert

      ...
    </div>
  );
};
~~~~~~~

입력 및 버튼 핸들러에 컴포넌트의 상태를 업데이트하기 위한 구현 로직을 전달합니다. 입력 필드 핸들러는 여전히 `searchTerm`을 업데이트하고 버튼 핸들러는 **현재** `searchTerm`에서 파생된 `url`과 정적 API URL을 새로운 상태로 설정합니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  const [searchTerm, setSearchTerm] = useSemiPersistentState(
    'search',
    'React'
  );

# leanpub-start-insert
  const [url, setUrl] = React.useState(
    `${API_ENDPOINT}${searchTerm}`
  );
# leanpub-end-insert

  ...

# leanpub-start-insert
  const handleSearchInput = event => {
# leanpub-end-insert
    setSearchTerm(event.target.value);
  };

# leanpub-start-insert
  const handleSearchSubmit = () => {
    setUrl(`${API_ENDPOINT}${searchTerm}`);
  };
# leanpub-end-insert

  ...
};
~~~~~~~

`searchTerm`이 변할 때마다 (즉, 입력 필드의 값이 변할 때마다) 데이터 가져오기 사이드 이펙트를 실행하는 대신 `url`을 사용합니다. `url`은 새로운 버튼을 통해 검색이 확인될 때 사용자가 명시적으로 설정합니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

  const handleFetchStories = React.useCallback(() => {
    dispatchStories({ type: 'STORIES_FETCH_INIT' });

# leanpub-start-insert
    fetch(url)
# leanpub-end-insert
      .then(response => response.json())
      .then(result => {
        dispatchStories({
          type: 'STORIES_FETCH_SUCCESS',
          payload: result.hits,
        });
      })
      .catch(() =>
        dispatchStories({ type: 'STORIES_FETCH_FAILURE' })
      );
# leanpub-start-insert
  }, [url]);
# leanpub-end-insert

  React.useEffect(() => {
    handleFetchStories();
  }, [handleFetchStories]);

  ...
};
~~~~~~~

이전에는 `searchTerm`이 입력 필드의 상태를 업데이트 할 때와 데이터 가져오기 사이드 이펙트를 활성화할 때의 두 가지 경우에 사용되었습니다. 이는 너무 많은 역할을 하고 있는 것으로 볼 수 있습니다. 이제는 전자의 경우에만 `searchTerm`을 사용힙니다. `url`이라는 또 다른 상태가 도입되어 사용자가 확인 버튼을 누를 때만 데이터 가져오기 사이드 이펙트를 유발합니다.

### 실습하기
* [마지막 장의 소스 코드](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/Explicit-Data-Fetching-with-React)를 확인하세요.
  * [마지막 장의 변경 사항](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/Memoized-Handler-in-React...hs/Explicit-Data-Fetching-with-React?expand=1)을 확인하세요.
* `url` 상태 관리에 `useSemiPersistentState` 대신 `useState`가 사용된 이유를 생각해보세요.
* `handleFetchStories` 함수에서 `searchTerm`이 비어 있는 경우를 더 이상 확인하지 않는 이유를 생각해보세요.