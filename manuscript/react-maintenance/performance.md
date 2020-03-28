# 리액트 유지 관리

리액트 애플리케이션의 크기가 커지면 유지 관리가 중요해집니다. 이러한 만일의 사태에 대비하기 위해 성능 최적화, 타입 안전성, 테스트, 프로젝트 구조에 대해 알아봅니다. 각각은 애플리케이션이 품질을 잃지 않고도 더 많은 기능을 수행할 수 있도록 강화해줄 것입니다.

성능 최적화는 주어진 자원의 효율적인 사용을 보장하여 애플리케이션이 느려지는 것을 방지합니다. 타입스크립트(TypeScript)와 같은 타입을 지정하는 프로그래밍 언어는 피드백 루프 초기에 버그를 감지합니다. 테스팅은 타입을 지정하는 프로그래밍보다 더 명확한 피드백을 제공하며, 어떤 동작이 애플리케이션을 중단시킬 수 있는지 이해할 방법을 제공합니다. 마지막으로 프로젝트 구조는 자산을 폴더와 파일로 체계적으로 관리할 수 있도록 지원하며, 이는 팀 구성원이 서로 다른 영역에서 작업할 경우 특히 더 유용합니다.

## 리액트의 성능 (고급 주제)

이 섹션은 리액트의 성능 향상을 다룹니다. 리액트는 특별히 빠른 편이기 때문에 대부분의 리액트 애플리케이션은 최적화가 필요하지 않습니다. 자바스크립트(JavaScript)나 리액트의 성능을 측정하기 위한 보다 더 정교한 도구들이 존재하지만, 간단한 `console.log()`와 브라우저의 개발 도구로 로그를 출력합니다.

### 첫 렌더링에는 실행하지 마세요.

앞에서 사이드 이펙트에 사용되는 리액트의 useEffect 훅을 다루었습니다. 이 훅은 컴포넌트가 처음 렌더링(마운팅) 될 때와 이후의 모든 재렌더링(업데이트)에 실행됩니다. 훅의 두 번째 인수로 빈 종속성 배열을 주면 첫 번째 렌더링에서만 동작하게 할 수 있습니다. 그러나 반대로 재렌더링에만 동작하도록 지시할 수는 없습니다. 예를 들어, 아래의 사용자 정의 훅을 확인해보세요. 리액트의 useState 훅으로 상태를 관리하고 리액트의 useEffect 훅으로 지역 저장소의 반영구적 상태를 관리합니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const useSemiPersistentState = (key, initialState) => {
  const [value, setValue] = React.useState(
    localStorage.getItem(key) || initialState
  );

  React.useEffect(() => {
# leanpub-start-insert
    console.log('A');
# leanpub-end-insert
    localStorage.setItem(key, value);
  }, [value, key]);

  return [value, setValue];
};
~~~~~~~

개발자 도구를 자세히 보면 이 사용자 정의 훅을 사용하는 컴포넌트의 첫 번째 렌더링 로그를 볼 수 있습니다. 초기 값 이외에는 지역 저장소에 저장할 것이 없기 때문에 컴포넌트의 첫 렌더링에 사이드 이펙트를 실행하는 것은 불필요한 함수 호출이며 컴포넌트의 모든 재렌더링에서만 실행되어야 합니다. 

앞에서 언급했듯이 모든 재렌더링에 실행되는 리액트 훅은 존재하지 않고, 리액트에 어울리는 방식으로 `useEffect` 훅의 함수를 재렌더링에만 호출하도록 지시할 방법도 없습니다. 하지만 리액트의 useRef 훅이 자신의 `ref.current` 속성을 재렌더링 동안에도 그대로 유지하는 것을 이용하여 (상태 업데이트 시 컴포넌트를 재렌더링 하지 않고) 컴포넌트 생애주기의 **지어낸 상태(made up state)**를 유지할 수 있습니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const useSemiPersistentState = (key, initialState) => {
# leanpub-start-insert
  const isMounted = React.useRef(false);
# leanpub-end-insert

  const [value, setValue] = React.useState(
    localStorage.getItem(key) || initialState
  );

  React.useEffect(() => {
# leanpub-start-insert
    if (!isMounted.current) {
      isMounted.current = true;
    } else {
# leanpub-end-insert
      console.log('A');
      localStorage.setItem(key, value);
# leanpub-start-insert
    }
# leanpub-end-insert
  }, [value, key]);

  return [value, setValue];
};
~~~~~~~

재렌더링을 유발하지 않는 강제적인 상태 관리를 위해 `ref`와 그것의 변경 가능한 `current` 속성을 이용합니다. 훅이 컴포넌트에서 처음 불릴 때 (컴포넌트 렌더링) ref의 `current`는 `isMounted`라 부르는 `거짓` 부울 값(boolean)으로 초기화되어 있습니다. 그 결과 `useEffect`의 사이드 이펙트 함수가 불리지 않고 그 안에서 `isMounted`의 부울 값 표시만 `참`으로 전환됩니다. 훅이 다시 실행될 때마다 (컴포넌트 재렌더링) 사이드 이펙트에서 부울 값 표시를 평가하는데, 그것이 `참`이기 때문에 사이트 이펙트 함수가 실행됩니다. 컴포넌트의 생애주기 동안 `isMounted` 부울 값은 `참`으로 유지될 것입니다. 그것은 위의 사용자 정의 훅을 사용하는 첫 렌더링에서만 사이트 이펙트 함수를 부르지 않게 하기 위해 존재했습니다. 

위의 내용은 첫 컴포넌트 렌더링에서 간단한 한 개의 함수 호출을 막는 것에 불과했습니다. 하지만 사이트 이펙트에 값비싼 계산이 있거나 사용자 정의 훅이 애플리케이션에서 자주 사용된다고 생각해보세요. 불필요한 함수 호출을 피하기 위해 이 기술을 적용하는 것이 더 실용적일 것입니다.

**참고: 이 기술은 성능 최적화에서만 사용되는 것이 아니며 컴포넌트 재렌더링에만 동작하는 사이드 이펙트를 만들 때도 유용합니다. 저도 이 기술을 여러 번 사용했지만, 여러 분도 결국 사용하게 될 것이라고 생각합니다.**

### 불필요한 재렌더링을 하지 마세요.

앞에서 우리는 리액트의 재렌더링 메커니즘을 탐구했습니다. App과 List 컴포넌트로 다시 연습해 보겠습니다. 두 컴포넌트 모두에 로깅 구문을 추가합니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

# leanpub-start-insert
  console.log('B:App');
# leanpub-end-insert

  return ( ... );
};

const List = ({ list, onRemoveItem }) =>
# leanpub-start-insert
  console.log('B:List') ||
# leanpub-end-insert
  list.map(item => (
    <Item
      key={item.objectID}
      item={item}
      onRemoveItem={onRemoveItem}
    />
  ));
~~~~~~~

List 컴포넌트는 함수의 본문이 없기 때문에 간단한 로깅 구문을 넣기 위해 코드를 리팩토링 하기보다 `||` 연산자를 사용하였습니다. 이것은 함수 본문이 없는 경우 로깅 구문을 추가할 때 사용할 수 있는 깔끔한 트릭입니다. 연산자의 왼쪽에 있는 `console.log()`가 항상 거짓으로 평가되기 때문에 연산자의 오른쪽에 있는 구문은 항상 실행됩니다.

{title="Code Playground",lang="javascript"}
~~~~~~~
function getTheTruth() {
  if (console.log('B:List')) {
    return true;
  } else {
    return false;
  }
}

console.log(getTheTruth());
// B:List
// false
~~~~~~~

브라우저 개발자 도구의 실제 로그에 집중해봅시다. 위와 유사한 결과를 볼 수 있을 것입니다. 먼저 App 컴포넌트가 렌더링되고, 그 자식 컴포넌트 (예: List 컴포넌트)가 렌더링됩니다.

{title="Visualization",lang="text"}
~~~~~~~
B:App
B:List
B:App
B:App
B:List
~~~~~~~

사이드 이펙트가 첫 렌더링 이후 데이터 가져오기를 유발하기 때문에 List 컴포넌트는 조건부 렌더링에서 로딩 지표로 대체되고 App 컴포넌트만 렌더링됩니다. 데이터가 도착하면 두 컴포넌트 모두 다시 렌더링됩니다.

{title="Visualization",lang="text"}
~~~~~~~
// initial render
B:App
B:List

// data fetching with loading
B:App

// re-rendering with data
B:App
B:List
~~~~~~~

지금까지는 모든 렌더링이 제시간에 이루어졌기 때문에 이러한 동작은 수용 가능했습니다. 이제 한 단계 더 나아가서 SearchForm 컴포넌트의 입력 필드에 입력해보겠습니다. 엘리먼트에 한 문자를 입력할 때마다 변화를 확인할 수 있을 것입니다.

{title="Visualization",lang="text"}
~~~~~~~
B:App
B:List
~~~~~~~

하지만 List 컴포넌트는 재렌더링 되어서는 안 됩니다. 버튼을 통해 검색 기능이 실행된 것이 아니기 때문에 List 컴포넌트에 전달된 `list`는 그대로여야 합니다. 이것이 많은 사람들을 놀라게 하는 리액트의 기본 동작입니다. 

리액트는 기본적으로 부모 컴포넌트가 재렌더링 되면 그 자식 컴포넌트도 재렌더링 됩니다. 자식 컴포넌트의 재렌더링을 막으면 버그가 발생할 수 있고, 리액트의 재렌더링 메커니즘은 아직 충분히 빠르기 때문입니다.

하지만 재렌더링을 막고 싶을 때가 있습니다. 예를 들어, 표에 표시된 대용량 데이터셋은 업데이트에 영향을 받지 않는 이상 재렌더링 되어서는 안됩니다. 컴포넌트의 무엇인가가 바뀌었을 때 동등성 검사를 수행하는 것이 더 효율적입니다. 그러므로 우리는 다음과 같이 리액트의 memo API를 이용하여 prop의 동등성 검사를 할 수 있습니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
# leanpub-start-insert
const List = React.memo(
# leanpub-end-insert
  ({ list, onRemoveItem }) =>
    console.log('B:List') ||
    list.map(item => (
      <Item
        key={item.objectID}
        item={item}
        onRemoveItem={onRemoveItem}
      />
    ))
# leanpub-start-insert
);
# leanpub-end-insert
~~~~~~~

However, the output stays the same when typing into the SearchForm's input field:

하지만 SearchForm의 입력 필드에 입력할 때 출력은 변하지 않습니다.

{title="Visualization",lang="text"}
~~~~~~~
B:App
B:List
~~~~~~~

List 컴포넌트에 전달된 `list`는 같지만 `onRemoveItem` 콜백 핸들러는 다릅니다. App 컴포넌트가 재렌더링 되면 항상 새로운 버전의 콜백 핸들러를 생성합니다. 앞에서 우리는 리액트의 useCallback 훅을 사용하여 (종속성 중 하나가 변경된 경우) 재렌더링에만 함수를 생성하도록 하여 이 동작을 방지했습니다. 

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

# leanpub-start-insert
  const handleRemoveStory = React.useCallback(item => {
# leanpub-end-insert
    dispatchStories({
      type: 'REMOVE_STORY',
      payload: item,
    });
# leanpub-start-insert
  }, []);
# leanpub-end-insert

  ...

  console.log('B:App');

  return (... );
};
~~~~~~~

콜백 핸들러는 함수 시그니처(function signature, 함수와 메서드 입력ㆍ출력을 정의)의 인수로 `item`을 받기 때문에 종속성이 없고 App 컴포넌트가 처음 렌더링될 때 단 한 번만 선언됩니다. 이제 List 컴포넌트에 전달된 prop은 모두 변해서는 안됩니다. SearchForm의 입력 필드를 통해 검색하기 위해 `memo`와 `useCallback` 조합을 시도해 보세요. "B:List" 출력이 사라지고 App 컴포넌트만이 "B:App"을 출력하며 재렌더링 됩니다. 

컴포넌트에 전달된 prop이 모두 변하지 않았더라도 그것의 부모 컴포넌트가 강제로 재렌더링되면 컴포넌트는 다시 렌더링됩니다. 재렌더링 메커니즘이 충분히 빠르기 때문에 이러한 리액트의 기본 동작은 대부분의 경우 잘 작동합니다. 하지만 재렌더링이 리액트 애플리케이션의 성능을 저하시키는 경우, `memo`가 재렌더링 방지를 도와줄 것입니다.

간혹 `memo`만으로는 도움이 되지 않을 때가 있습니다. 콜백 핸들러가 부모 컴포넌트에서 매번 새로 정의되고 컴포넌트에 **변경된** prop으로 전달되면 또다른 재렌더링을 유발합니다. 그런 경우에는 `useCallback`으로 콜백 핸들러가 종속성이 바뀔 때만 변경되도록 할 수 있습니다.

### 값비싼 계산은 한 번만 실행하세요.

가끔 리액트 컴포넌트에 매 렌더링마다 실행되는 성능 집약적인 계산이 (컴포넌트의 함수 시그니처와 return 블록 사이에) 있을 수 있습니다. 이런 시나리오를 위해 일단 현재 애플리케이션에 사용 예시를 생성해야 합니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
# leanpub-start-insert
const getSumComments = stories => {
  console.log('C');

  return stories.data.reduce(
    (result, value) => result + value.num_comments,
    0
  );
};
# leanpub-end-insert

const App = () => {
  ...

# leanpub-start-insert
  const sumComments = getSumComments(stories);
# leanpub-end-insert

  return (
    <div>
# leanpub-start-insert
      <h1>My Hacker Stories with {sumComments} comments.</h1>
# leanpub-end-insert

      ...
    </div>
  );
};
~~~~~~~

함수에 모든 인수들이 전달된다면 함수를 컴포넌트 밖에 두어도 됩니다. 그렇게 하면 함수가 매 렌더링마다 생성되지 않기 때문에 'useCallback' 훅이 불필요해집니다. 그러나 여전히 함수는 댓글 수의 합을 매 렌더링에 계산하기 때문에, 더 값비싼 계산에서는 문제가 될 수 있습니다.

SearchForm 컴포넌트의 입력 필드에 문자가 입력될 때마다 이 계산은 "C"를 출력하며 다시 실행됩니다. 이 경우와 같이 무겁지 않은 계산에 대해서는 괜찮을지 모르지만, 이 계산이 500ms 이상 걸린다고 상상해 보세요. 컴포넌트 내의 모든 것들이 이 계산이 끝나기를 기다려야 하기 때문에 재렌더링에 지연이 발생할 것입니다. 리액트에게 종속성에 변화가 있을 때만 함수를 실행하도록 지시할 수 있습니다. 종속성이 변하지 않으면 함수의 결과가 유지되도록 하는 것입니다. 리액트의 useMemo 훅을 사용하면 됩니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

# leanpub-start-insert
  const sumComments = React.useMemo(() => getSumComments(stories), [
    stories,
  ]);
# leanpub-end-insert

  return ( ... );
};
~~~~~~~

SearchForm에 입력이 들어올 때마다 계산을 실행해서는 안됩니다. 이제 이 계산은 `stories`에 해당하는 종속성 배열이 변하는 경우에만 실행됩니다. 하지만 이것은 컴포넌트 (재)렌더링의 지연을 가져올 수 있는 값비싼 계산에만 사용되어야 합니다.

Now, after we went through these scenarios for `useMemo`, `useCallback`, and `memo`, remember that these shouldn't necessarily be used by default. Apply these performance optimization only if you run into a performance bottlenecks. Most of the time this shouldn't happen, because React's rendering mechanism is pretty efficient by default. Sometimes the check for utilities like `memo` can be more expensive than the re-rendering itself.

이제 `useMemo`, `useCallback`, 그리고 `memo`를 사용하는 시나리오를 모두 검토했으니 이것을 기본적으로 사용할 필요는 없음을 기억하세요. 이러한 성능 최적화는 성능 병목을 마주했을 때만 적용하세요. 대부분의 경우 리액트의 렌더링 메커니즘이 기본적으로 꽤 효율적이기 때문에 사용할 일이 없을 것입니다. 경우에 따라서 재렌더링 자체보다 `memo`와 같은 유틸리티를 확인하는 것이 더 값비싸질 수도 있습니다.

### 읽어보기
* [마지막 섹션의 소스 코드](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/Performance-in-React)를 확인하세요.
* [마지막 섹션의 변경 사항](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/react-modern-final...hs/Performance-in-React?expand=1)을 확인하세요.
* [리액트 memo API](https://reactjs.org/docs/react-api.html#reactmemo)에 대해 더 읽어보세요.
* [리액트 useCallback 훅](https://reactjs.org/docs/hooks-reference.html#usecallback)에 대해 더 읽어보세요.

### 실습하기
* Download *React Developer Tools* as an extension for your browser. Open it for your application in the browser via the browser's developer tools and try its various features. For instance, you can use it to visualize React's component tree and its updating components.
* Does the SearchForm re-render when removing an item from the List with the "Dismiss" button? If it's the case, apply performance optimization techniques to prevent re-rendering.
* Does each Item re-render when removing an item from the List with the "Dismiss" button? If it's the case, apply performance optimization techniques to prevent re-rendering.
* Remove all performance optimizations to keep the application simple. Our current application doesn't suffer from any performance bottlenecks. Try to avoid [premature optimzations](https://en.wikipedia.org/wiki/Program_optimization). Use this section as reference, in case you run into performance problems.

* 브라우저 확장 기능인 **리액트 개발자 도구**를 다운로드 받으세요. 브라우저의 애플리케이션을 위해 브라우저 개발자 도구로 확장 기능을 열고 다양한 기능을 시도해 보세요. 예를 들어, 리액트 컴포넌트 트리와 업데이트 되는 컴포넌트를 시각화 하는데 사용할 수 있습니다.
* List에서 "Dismiss" 버튼을 사용하여 아이템을 제거할 때 SearchForm이 재렌더링 되나요? 만약 그렇다면 재렌더링을 방지하기 위한 성능 최적화 기술을 적용해 보세요.
* List에서 "Dismiss" 버튼을 사용하여 아이템을 제거할 때 각 Item은 재렌더링 되나요? 만약 그렇다면 재렌더링을 방지하기 위한 성능 최적화 기술을 적용해 보세요.
* 애플리케이션을 간단하게 유지하기 위해 모든 성능 최적화를 제거해보세요. 현재 애플리케이션은 성능 병목이 없습니다. [너무 이른 최적화](https://en.wikipedia.org/wiki/Program_optimization)는 피하고 성능 문제가 발생한 경우에만 이 섹션을 참고하세요.