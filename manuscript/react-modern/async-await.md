## 리액트에서의 Async와 Await(심화)

리액트에서 비동기 데이터를 자주 사용하므로 프로미스(promise) 처리를 대신할 수 있는 구문인 async와 await를 알면 좋습니다. 오류 처리 없이 `handleFetchStories` 함수를 리팩토링하는 방법은 다음과 같습니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

# leanpub-start-insert
  const handleFetchStories = React.useCallback(async () => {
# leanpub-end-insert
    dispatchStories({ type: 'STORIES_FETCH_INIT' });

# leanpub-start-insert
    const result = await axios.get(url);
# leanpub-end-insert

# leanpub-start-insert
    dispatchStories({
      type: 'STORIES_FETCH_SUCCESS',
      payload: result.data.hits,
    });
# leanpub-end-insert
  }, [url]);

  ...
};
~~~~~~~

async와 await를 사용하려면 함수에 `async` 키워드를 붙입니다. `await` 키워드를 사용하면 모든 것을 동기 코드처럼 읽을 수 있습니다. `await` 키워드 이후의 동작은 프로미스가 처리될 때까지 실행되지 않고 기다립니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

  const handleFetchStories = React.useCallback(async () => {
    dispatchStories({ type: 'STORIES_FETCH_INIT' });

# leanpub-start-insert
    try {
# leanpub-end-insert
      const result = await axios.get(url);

      dispatchStories({
        type: 'STORIES_FETCH_SUCCESS',
        payload: result.data.hits,
      });
# leanpub-start-insert
    } catch {
      dispatchStories({ type: 'STORIES_FETCH_FAILURE' });
    }
# leanpub-end-insert
  }, [url]);

  ...
};
~~~~~~~

`try`와 `catch` 블록은 이전처럼 오류 처리를 하는 것에 도움이 됩니다. `try` 블록에 문제가 생기면 코드는 `catch` 블록으로 넘어가서 에러를 처리합니다. `then`과 `catch` 블록, 그리고 `try`와 `catch` 블록을 이용한 async와 await 구문 모두 자바스크립트와 리액트에서 비동기 데이터를 관리하는 데에 사용할 수 있습니다.

### 실습하기

* [마지막 장의 소스 코드](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/Async-Await-in-React)를 확인하세요.
  * [마지막 장의 변경 사항](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/Third-Party-Libraries-in-React...hs/Async-Await-in-React?expand=1)을 확인하세요.
* [리액트에서 데이터 불러오기](https://www.robinwieruch.de/react-hooks-fetch-data)에 대해 자세히 알아보세요.
* [자바스크립트의 async와 await](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function)에 대해 자세히 알아보세요.