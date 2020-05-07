## 리액트에서 데이터 다시 가져오기

지금까지 App 컴포넌트는 미리 지정된 쿼리 ('react')로 스토리 목록을 한 번만 가져왔습니다. 이후에 사용자는 클라이언트 사이드에서 스토리를 검색할 수 있습니다. 이제 이 기능을 서버 사이드로 옮겨 실제 `searchTerm`을 API 요청의 동적 쿼리로 사용해봅시다.

API에서 검색된 스토리를 받을 것이므로 `searchedStories`를 지웁니다. List 컴포넌트에는 일반적인 스토리만 넘겨줍니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

  return (
    <div>
      ...

      {stories.isLoading ? (
        <p>Loading ...</p>
      ) : (
# leanpub-start-insert
        <List list={stories.data} onRemoveItem={handleRemoveStory} />
# leanpub-end-insert
      )}
    </div>
  );
};
~~~~~~~

하드코딩한 검색어 대신에 컴포넌트 상태에서 실제 `searchTerm`을 가져와 사용합니다. `searchTerm`이 빈 문자열이라면 아무것도 하지 않습니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

  React.useEffect(() => {
# leanpub-start-insert
    if (searchTerm === '') return;
# leanpub-end-insert

    dispatchStories({ type: 'STORIES_FETCH_INIT' });

# leanpub-start-insert
    fetch(`${API_ENDPOINT}${searchTerm}`)
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
  }, []);

  ...
};
~~~~~~~

이제 첫 검색은 검색어를 반영합니다. 이제 데이터 다시 가져오기를 구현하겠습니다. `searchTerm`이 바뀌면 데이터 가져오기를 위한 사이드 이펙트를 다시 실행합니다. 더 일반화된 조건으로 `searchTerm`이 존재하지 않으면 (예: null, 빈 문자열, undefined) 아무것도 하지 않습니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

  React.useEffect(() => {
# leanpub-start-insert
    if (!searchTerm) return;
# leanpub-end-insert

    dispatchStories({ type: 'STORIES_FETCH_INIT' });

    fetch(`${API_ENDPOINT}${searchTerm}`)
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
  }, [searchTerm]);
# leanpub-end-insert

  ...
};
~~~~~~~

검색 기능을 클라이언트 사이드에서 서버 사이드로 변경하였습니다. 클라이언트에서 미리 지정된 스토리 목록을 필터링하는 대신에 `searchTerm`을 이용하여 서버 사이드에서 필터링된 리스트를 가져왔습니다. 서버 사이드 검색은 첫 데이터 가져오기뿐만 아니라 `searchTerm`이 변경될 때의 데이터 가져오기에도 일어납니다. 이 기능은 이제 완전히 서버 사이드에서 이루어집니다.

입력 필드에 글자가 입력될 때마다 데이터를 다시 가져오는 것이 최선은 아니므로, 곧 수정할 예정입니다. 현재 구현 방식은 API에게 부담을 주기 때문에 지나치게 자주 요청을 날리면 오류를 경험할 수도 있습니다.

### 실습하기
* [마지막 장의 소스 코드](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/Data-Re-Fetching-in-React)를 확인하세요.
  * [마지막 장의 변경 사항](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/Data-Fetching-with-React...hs/Data-Re-Fetching-in-React?expand=1)을 확인하세요.