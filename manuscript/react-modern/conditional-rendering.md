## 리액트 조건부 렌더링

리액트에서 비동기 데이터를 처리하다 보면, 데이터가 있기도 하고 데이터가 없기도 하는 '조건부 상태'가 생깁니다. 이미 앞에서 다룬 내용이기도 합니다. 초기 상태가 `null`이 아니라 빈 리스트이기 때문입니다. 만약 null이었다면 이 문제는 JSX에서 다뤄야 하겠지요. 그러나 `[]` 이기 때문에, 만약 검색을 위해 빈 배열에 `filter()`를 사용한다면 빈 배열만 남게 됩니다. 이로 인해 List 컴포넌트의 `map()` 함수는 렌더링을 할 수 있는 항목이 아무것도 없게 됩니다.

실제 애플리케이션에서는 비동기 데이터에 대한 조건부 상태가 두 가지 이상이 있습니다. 데이터 로딩이 지연될 때 사용자에게 로딩 인디케이터를 보여주는 것도 생각해야 하기 때문입니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

  const [stories, setStories] = React.useState([]);
# leanpub-start-insert
  const [isLoading, setIsLoading] = React.useState(false);
# leanpub-end-insert

  React.useEffect(() => {
# leanpub-start-insert
    setIsLoading(true);
# leanpub-end-insert

    getAsyncStories().then(result => {
      setStories(result.data.stories);
# leanpub-start-insert
      setIsLoading(false);
# leanpub-end-insert
    });
  }, []);

  ...
};
~~~~~~~

[자바스크립트의 삼항 조건 연산자(ternary operator)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_Operator)로 조건부 상태를 인라인으로 사용함으로써, JSX에서 **조건부 렌더링**을 할 수 있게 됩니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

  return (
    <div>
      ...

      <hr />

# leanpub-start-insert
      {isLoading ? (
        <p>Loading ...</p>
      ) : (
# leanpub-end-insert
        <List
          list={searchedStories}
          onRemoveItem={handleRemoveStory}
        />
# leanpub-start-insert
      )}
# leanpub-end-insert
    </div>
  );
};
~~~~~~~

비동기 데이터는 오류도 처리를 해야 합니다. 현재 시뮬레이션 환경에서는 오류가 발생하지 않더라도, 다른 API에서 데이터를 가져오기 시작하면 오류가 발생할 수 있습니다. 오류를 저장하는 상태를 만들고, promise의 `catch()` 블록에서 처리하도록 합니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

  const [stories, setStories] = React.useState([]);
  const [isLoading, setIsLoading] = React.useState(false);
# leanpub-start-insert
  const [isError, setIsError] = React.useState(false);
# leanpub-end-insert

  React.useEffect(() => {
    setIsLoading(true);

    getAsyncStories()
      .then(result => {
        setStories(result.data.stories);
        setIsLoading(false);
      })
# leanpub-start-insert
      .catch(() => setIsError(true));
# leanpub-end-insert
  }, []);

  ...
};
~~~~~~~

조건부 렌더링에 문제가 생긴 경우, 사용자에게 피드백을 제공해야 합니다. 이번에는 뭔가를 렌더링하거나 아무것도 렌더링하지 않도록 해봅니다. 한쪽이 `null`을 반환하는 삼항 조건 연산자 대신에 논리 연산자인 `&&`를 사용합니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

  return (
    <div>
      ...

      <hr />

# leanpub-start-insert
      {isError && <p>Something went wrong ...</p>}
# leanpub-end-insert

      {isLoading ? (
        <p>Loading ...</p>
      ) : (
        ...
      )}
    </div>
  );
};
~~~~~~~

자바스크립트에서는 `true && 'Hello World'`는 항상 'Hello World'으로 간주합니다. 마찬가지로 `false && 'Hello World'`의 경우 항상 거짓으로 간주합니다. 리액트에서는 이러한 특성을 장점으로 사용할 수 있습니다. 조건이 참이면, 논리 연산자 `&&`의 뒷부분 내용이 출력됩니다. 조건이 거짓이면 리액트는 표현식을 무시하고 이를 건너뜁니다.

조건부 렌더링은 비동기 데이터만을 위한 것이 아닙니다. 조건부 렌더링의 가장 간단한 예시로는 토글 버튼의 부울 상태가 있습니다. 부울 플래그가 참이면 렌더링, 거짓인 경우 렌더링하지 않습니다.

조건부로 JSX를 렌더링하는 건 꽤 강력한 기능입니다. UI를 더 역동적으로 만드는 리액트의 또 다른 도구입니다. 또한, 앞서 다뤘던 내용에도 나왔듯이 비동기 데이터와 같이 복잡한 제어 흐름이 필요할 때 필수적입니다.

### 실습하기

* [[코드샌드박스] 지난 장에서 사용한 코드](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/React-Conditional-Rendering)
  * [[깃허브] 지난 장에서 수정된 코드](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/React-Asynchronous-Data...hs/React-Conditional-Rendering?expand=1)
* [리액트의 조건부 렌더링](https://www.robinwieruch.de/conditional-rendering-react/)에 대해서 더 읽어보세요.

