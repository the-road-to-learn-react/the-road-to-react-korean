## 리액트 상태 관리 (심화)

어플리케이션의 모든 상태 관리는 리액트의 useState 훅을 많이 사용합니다. 보다 정교한 상태 관리는 리액트의 **useReducer** 훅을 통해 이루어집니다. 자바스크립트의 리듀서(reducer) 개념에 대해서는 많은 의논이 있기 때문에 여기서는 다루지 않습니다. 이번 절의 마지막에 있는 연습 문제가 많은 도움이 될 것입니다.

우리는 `stories`의 상태 관리를 `useState` 훅에서 `useReducer` 훅으로 옮길 것입니다. 먼저, 컴포넌트 외부에 reducer를 생성하세요. 이 리듀서는 항상 `state`와 `action`을 받습니다. 이 두 인자를 기반으로 리듀서는 항상 새로운 상태를 반환합니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
# leanpub-start-insert
const storiesReducer = (state, action) => {
  if (action.type === 'SET_STORIES') {
    return action.payload;
  } else {
    throw new Error();
  }
};
# leanpub-end-insert
~~~~~~~

리듀서의 `action`은 `타입(type)`과 관련 있습니다. 리듀서의 조건과 타입이 일치할 경우 동작이 수행되며 조건이 일치하지 않을 경우 오류를 반환합니다. `storiesReducer`는 하나의 `타입을 포함한 후 현재 상태를 사용하여 새 상태를 계산하지 않고 들어오는 action의` 데이터를 전달합니다. `새로운 상태는 단순히` 전달된 데이터에 불과합니다.

앱 컴포넌트 안에서 `stories`를 관리하려면 `useState`를 `useReducer`로 교환합니다. 새로운 훅은 리듀서의 초기 상태를 인자로 받고 두 요소가 있는 배열을 반환합니다. 첫 요소는 현재 상태이며, 두 번째 요소는 상태를 업데이트하는 함수입니다. *디스패치 함수(dispatch function)* 라고 합니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

# leanpub-start-insert
  const [stories, dispatchStories] = React.useReducer(
    storiesReducer,
    []
  );
# leanpub-end-insert

  ...
};
~~~~~~~

`useState`에서 반환된 `setStories`함수 대신 새 디스패치 기능을 사용할 수 있습니다. `useState`에 명시적으로 상태를 업데이트하는 대신 `useReducer`의 상태 업데이트 기능은 리듀서에 디스패치를 통해 action을 보냅니다. action은 타입과 지정된 데이터와 함께 제공됩니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

  React.useEffect(() => {
    setIsLoading(true);

    getAsyncStories()
      .then(result => {
# leanpub-start-insert
        dispatchStories({
          type: 'SET_STORIES',
          payload: result.data.stories,
        });
# leanpub-end-insert
        setIsLoading(false);
      })
      .catch(() => setIsError(true));
  }, []);

  ...

  const handleRemoveStory = item => {
    const newStories = stories.filter(
      story => item.objectID !== story.objectID
    );

# leanpub-start-insert
    dispatchStories({
      type: 'SET_STORIES',
      payload: newStories,
    });
# leanpub-end-insert
  };

  ...
};
~~~~~~~

리듀서와 리액트의 `useReducer` 훅이 이제 스토리의 상태를 관리하지만 애플리케이션은 브라우저에서 동일하게 나타납니다. 상태 전환 처리 후, 리듀서를 최소 버전으로 가져오십시오.

`handleRemoveStory`핸들러는 새 스토리를 계산합니다. 이 로직을 리듀서로 옮기고 action으로 리듀서를 관리하는 것이 유효합니다. 이는 명령형에서 선언형 프로그래밍으로 변경하는 예입니다. *어떻게 해야 하는지* 직접 말하는 대신 리듀서에 *무엇을 해야 하는지* 말하고 있습니다. 다른 많은 것들도 리듀서 안에 숨겨져 있습니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

  const handleRemoveStory = item => {
# leanpub-start-insert
    dispatchStories({
      type: 'REMOVE_STORY',
      payload: item,
    });
# leanpub-end-insert
  };

  ...
};
~~~~~~~

이제 리듀서는 상태 변경을 처리해야합니다. 조건에 따라 리듀서는 스토리를 제거하기 위한 구현 사항을 가지게 됩니다. 이는 현재 상태에서 스토리를 제거하고 필터링 된 스토리의 새 목록을 리턴하는데 필요한 모든 정보 (항목 ID)를 제공합니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const storiesReducer = (state, action) => {
  if (action.type === 'SET_STORIES') {
    return action.payload;
# leanpub-start-insert
  } else if (action.type === 'REMOVE_STORY') {
    return state.filter(
      story => action.payload.objectID !== story.objectID
    );
  } else {
# leanpub-end-insert
    throw new Error();
  }
};
~~~~~~~

리듀서에 많은 상태 변경을 추가할 경우 if else 문을 사용하면 복잡해집니다. switch 문으로 리팩토링하면 읽기 쉽습니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const storiesReducer = (state, action) => {
# leanpub-start-insert
  switch (action.type) {
    case 'SET_STORIES':
      return action.payload;
    case 'REMOVE_STORY':
      return state.filter(
        story => action.payload.objectID !== story.objectID
      );
    default:
      throw new Error();
  }
# leanpub-end-insert
};
~~~~~~~

우리가 다룬 것은 자바스크립트에서 최소 버전의 리듀서 개념입니다. 두 가지 상태 변경을 다루고 현재 상태와 동작을 새로운 상태로 계산하는 방법을 보여 주며 일부 비즈니스 로직 (스토리 제거)을 사용합니다. 이제 비동기적으로 도착하는 데이터의 상태로 스토리 목록을 설정하고 하나의 상태 관리 리듀서와 관련된 `useReducer`훅을 사용하여 스토리 목록에서 스토리를 제거 할 수 있습니다.

자바스크립트에서 리듀서 개념과 리액트의 useReducer 훅 사용법을 완전히 이해하려면 연습 링크를 확인하세요.

### 실습하기


* [마지막 장의 소스 코드](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/React-Advanced-State)를 확인하세요..
  * [마지막 장의 변경 사항](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/React-Conditional-Rendering...hs/React-Advanced-State?expand=1)을 확인하세요.
* [자바스크립트 Reducer](https://www.robinwieruch.de/javascript-reducer)에 대해 자세히 알아보세요.
* 리액트 Reducer와 useReducer ([0](https://www.robinwieruch.de/react-usereducer-hook), [1](https://reactjs.org/docs/hooks-reference.html#usereducer))에 대해 자세히 알아보세요.