## 리액트 메모이제이션 핸들러 (심화)

이전 절에서 핸들러, 콜백 핸들러, 인라인 핸들러에 대해 배웠습니다. 이번 절에는 핸들러와 콜백 핸들러 위에 적용되는 **메모이제이션 핸들러(memoized handler)** 에 대해 알아보겠습니다. 각 알파벳은 해당 코드를 설명합니다. 

 (A) 데이터를 가저오는 로직을 함수로 만들었습니다. (B) `useCallback`으로 전체 함수를 감싸고, (C)  `useEffect` 훅에서 호출합니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

  // A
# leanpub-start-insert
  const handleFetchStories = React.useCallback(() => {
# leanpub-end-insert
    if (!searchTerm) return;

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
  }, [searchTerm]); // E
# leanpub-end-insert

  React.useEffect(() => {
# leanpub-start-insert
    handleFetchStories(); // C
  }, [handleFetchStories]); // D
# leanpub-end-insert

  ...
};
~~~~~~~

동작은 동일하지만 로직만 리팩터링 했습니다. 데이터 가져오기 로직을 익명 함수로 만들지 말고 함수로 만들고 전달했습니다.

이제 왜 리액트 `useCallback` 훅이 필요한지 설명하겠습니다. 이 훅은 메모이제이션 함수로 의존성이 변경될 때마다 생성됩니다. (E) 결과적으로,  `useEffect` 훅이 제 실행되는데 (C) 새로운 함수에 의존하기 때문입니다. (D)

{title="Visualization",lang="javascript"}
~~~~~~~
1. 변경: searchTerm
2. 암시적 변경 : handleFetchStories
3. 실행: 부작용
~~~~~~~

`useCallback` 훅으로 메모이제이션 함수를 만들지 않으면 각 App 컴포넌트와 함께 새로운 `handleFetchStories` 함수가 만들어집니다. `handleFetchStories` 함수는 매번 생성되며, `useEffect` 훅에서 실행되어 데이터를 가져옵니다. 가져온 데이터는 컴포넌트 상태로 저장됩니다. 컴포넌트 상태가 변경될 때 마다 컴포넌트는 리렌더링되어 다시 새로운 `handleFetchStories` 함수를 만듭니다. 데이터를 가져오기 올 때 사이드 이펙트가 생길 수 있어 무한 루프에 빠지게 됩니다.

{title="Visualization",lang="javascript"}
~~~~~~~
1. 정의: handleFetchStories
2. 실행: 부작용
3. 업데이트: 상태
4. 리렌더링: 컴포넌트
5. 재정의: handleFetchStories
6. 실행: 부작용
...
~~~~~~~

`useCallback` 훅은  검색어가 변경 될 때만 함수를 변경합니다.  입력값이 변경될 때마다 데이터를 다시 가져와 목록을 업데이트합니다.

데이터를 가져오는 기능을 `useEffect` 훅에서 꺼내 함수로 만들게 되면 다른 곳에서도 재사용할 수 있습니다. 아직 이 방법을 사용하지 않았지만 `useCallback` 후크를 이해하는 좋은 방법입니다. `searchTerm`이 변경 될 때마다  `handleFetchStories`이 재정의되기 때문에, `searchTerm`이 변경되면 `useEffect` 훅이 실행됩니다.  `useEffect` 훅은   `handleFetchStories`에 의존하기 때문에 사이드 이펙트가 다시 실행됩니다.

### 실습하기

* [[코드샌드박스] 마지막 절의 소스코드](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/Memoized-Handler-in-React)를 확인하세요.
  * [[깃허브] 마지막 절의 소스코드](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/Data-Re-Fetching-in-React...hs/Memoized-Handler-in-React?expand=1)를 확인하세요.
*  [[공식 문서]리액트 useCallback 훅](https://reactjs.org/docs/hooks-reference.html#usecallback)에 대해 읽어보세요.