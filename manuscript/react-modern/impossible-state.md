## 불가능한 상태

`useState` 훅 때문에 함께 있는 것처럼 보이는 App 컴포넌트의 단일 상태들이 실제로는 서로 연결이 끊긴 것을 확인하였을 것입니다. 기술적으로는 비동기 데이터와 관련된 모든 상태는 실제 데이터인 스토리뿐만 아니라 로딩 및 오류 상태도 포함하여 함께 존재합니다.

하나의 리액트 컴포넌트에 여러 개의 `useState` 훅이 있는 것은 아무 문제가 없습니다. 그러나 여러 상태 업데이트 함수들이 연이어 보이면 주의해야 합니다. 이러한 조건부 상태는 **불가능한 상태**와 UI에서의 원치 않는 동작으로 이어질 수 있습니다. 오류 처리를 시뮬레이션하기 위해 유사 데이터 가져오기 함수를 아래와 같이 변경해보세요.

{title="src/App.js",lang="javascript"}
~~~~~~~
const getAsyncStories = () =>
  new Promise((resolve, reject) => setTimeout(reject, 2000));
~~~~~~~

비동기 데이터에 오류가 발생할 때 불가능한 상태가 나타납니다. 오류를 나타내는 상태는 설정되지만, 로딩 인디케이터의 상태는 취소되지 않는 경우입니다. UI에서는 오류 메시지만 보여주고 로딩 인디케이터를 숨기는 것이 더 적합하지만, 무한 로딩 인디케이터와 오류 메시지를 함께 보여주게 됩니다. 이렇듯 불가능한 상태는 발견하기 쉽지 않아 UI에서 버그를 일으키는 것으로 악명이 높습니다.

다행히 여러 개의 `useState`와 `useReducer` 훅에서 하나의 `useReducer` 훅으로 함께 존재하는 상태들을 이동시킴으로써 버그가 날 확률을 줄일 수 있습니다. 다음의 `useReducer` 훅을 사용합니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

  const [stories, dispatchStories] = React.useReducer(
    storiesReducer,
    []
  );
  const [isLoading, setIsLoading] = React.useState(false);
  const [isError, setIsError] = React.useState(false);

  ...
};
~~~~~~~

통합 상태 관리 및 더욱 복잡한 상태 개체를 위해 하나의 `useReducer` 훅으로 통합합니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

  const [stories, dispatchStories] = React.useReducer(
    storiesReducer,
# leanpub-start-insert
    { data: [], isLoading: false, isError: false }
# leanpub-end-insert
  );

  ...
};
~~~~~~~

비동기 데이터 가져오기와 관련된 모든 항목은 상태 전환에 새로운 디스패치 함수를 사용해야 합니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

  const [stories, dispatchStories] = React.useReducer(
    storiesReducer,
    { data: [], isLoading: false, isError: false }
  );

  React.useEffect(() => {
# leanpub-start-insert
    dispatchStories({ type: 'STORIES_FETCH_INIT' });
# leanpub-end-insert

    getAsyncStories()
      .then(result => {
        dispatchStories({
# leanpub-start-insert
          type: 'STORIES_FETCH_SUCCESS',
# leanpub-end-insert
          payload: result.data.stories,
        });
      })
      .catch(() =>
# leanpub-start-insert
        dispatchStories({ type: 'STORIES_FETCH_FAILURE' })
# leanpub-end-insert
      );
  }, []);

  ...
};
~~~~~~~

새로운 상태 전환 유형을 도입했으므로 `storiesReducer` 리듀서 함수에서 처리해줍니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const storiesReducer = (state, action) => {
  switch (action.type) {
# leanpub-start-insert
    case 'STORIES_FETCH_INIT':
      return {
        ...state,
        isLoading: true,
        isError: false,
      };
    case 'STORIES_FETCH_SUCCESS':
      return {
        ...state,
        isLoading: false,
        isError: false,
        data: action.payload,
      };
    case 'STORIES_FETCH_FAILURE':
      return {
        ...state,
        isLoading: false,
        isError: true,
      };
    case 'REMOVE_STORY':
      return {
        ...state,
        data: state.data.filter(
          story => action.payload.objectID !== story.objectID
        ),
      };
# leanpub-end-insert
    default:
      throw new Error();
  }
};
~~~~~~~

모든 상태 전환에서 자바스크립트의 전개 연산자를 통해 **현재 상태** 개체의 모든 키/값 쌍과 덮어쓸 새로운 속성이 포함된 **새로운 상태** 개체를 반환합니다. 예를 들어, `STORIES_FETCH_FAILURE`은 `isLoading`을 거짓으로 재설정하고 `isError` 부울 플래그는 참으로 바꾸지만 다른 모든 상태 (예: `stories`)는 그대로 유지합니다. 오류가 나면 로딩 상태는 그만두어야 하므로 이러한 방식으로 앞에서 소개된 버그를 처리합니다.

`REMOVE_STORY` 액션이 어떻게 변했는지도 관찰해보세요. 그것은 더 이상 단순한 `state`만이 아니라 `state.data`에도 작동합니다. 상태는 단순한 스토리 목록이 아니라 데이터, 로딩 및 오류 상태를 가진 복잡한 개체입니다. 이 문제 역시 나머지 코드에서 해결해야 합니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

  const [stories, dispatchStories] = React.useReducer(
    storiesReducer,
    { data: [], isLoading: false, isError: false }
  );

  ...

# leanpub-start-insert
  const searchedStories = stories.data.filter(story =>
# leanpub-end-insert
    story.title.toLowerCase().includes(searchTerm.toLowerCase())
  );

  return (
    <div>
      ...

# leanpub-start-insert
      {stories.isError && <p>Something went wrong ...</p>}
# leanpub-end-insert

# leanpub-start-insert
      {stories.isLoading ? (
# leanpub-end-insert
        <p>Loading ...</p>
      ) : (
        <List
          list={searchedStories}
          onRemoveItem={handleRemoveStory}
        />
      )}
    </div>
  );
};
~~~~~~~

오류가 있는 데이터 가져오기 함수를 다시 사용하여 모든 것이 예상대로 작동하는지 확인합니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const getAsyncStories = () =>
  new Promise((resolve, reject) => setTimeout(reject, 2000));
~~~~~~~

여러 `useState` 훅을 사용하는 신뢰할 수 없는 상태 전환을 useReducer 훅을 사용한 예측 가능한 상태 전환으로 변경했습니다. 리듀서가 관리하는 상태 개체는 로딩, 오류 상태 등 스토리와 관련된 모든 것뿐만 아니라 스토리 목록에서 스토리를 제거하는 등의 구현 세부사항도 포함합니다. 여전히 중요한 부울 플래그를 빠뜨릴 수 있기 때문에 불가능한 상태를 완전히 제거하지는 못했지만, 보다 예측 가능한 상태 관리를 향해 한 걸음 더 다가갔습니다.

### 읽어보기
* 자바스크립트와 리액트의 리듀서에 관한 이전의 튜토리얼 링크를 훑어보세요.
* [언제 useState 또는 useReducer를 사용해야하는지](https://www.robinwieruch.de/react-usereducer-vs-usestate)에 대해 더 읽어보세요. 

### 실습하기
* [마지막 장의 소스 코드](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/React-Impossible-States)를 확인하세요.
  * [마지막 장의 변경 사항](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/React-Advanced-State...hs/React-Impossible-States?expand=1)을 확인하세요.