## React Side-Effects
## 리액트 사이드 이펙트

Next we'll add a feature to our Search component in the form of another React hook. We'll make the Search component remember the most recent search interaction, so the application opens it in the browser whenever it restarts.
다음으로 Search 컴포넌트에 또 다른 훅의 형태로 기능을 추가하겠습니다. Search 컴포넌트가 가장 최근의 검색 상호작용을 기억하게 하여 브라우저가 재시작할 때 애플리케이션이 그 결과를 열도록 할 것입니다. 

First, use the local storage of the browser to store the `searchTerm` accompanied by an identifier. Next, use the stored value, if there a value exists, to set the initial state of the `searchTerm`. Otherwise, the initial state defaults to our initial state (here "React") as before:
먼저 브라우저의 로컬 저장소에 `searchTerm`과 그 표시자를 저장합니다. 다음으로, 저장된 값이 존재하면 `searchTerm`의 초기 상태를 설정하는데 사용하고 그렇지 않으면 초기 상태를 이전처럼 기본값으로 둡니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
 ...

 const [searchTerm, setSearchTerm] = React.useState(
# leanpub-start-insert
   localStorage.getItem('search') || 'React'
# leanpub-end-insert
 );

 const handleSearch = event => {
   setSearchTerm(event.target.value);

# leanpub-start-insert
   localStorage.setItem('search', event.target.value);
# leanpub-end-insert
 };

 ...
);
~~~~~~~

When using the input field and refreshing the browser tab, the browser should remember the latest search term. Using the local storage in React can be seen as a **side-effect** because we interact outside of React's domain by using the browser's API.
입력 필드를 사용하고 브라우저의 탭을 새로고침하면 브라우저는 가장 최근의 검색 용어를 기억해야합니다. 리액트에서 로컬 저장소를 사용하는 것은 브라우저 API를 이용해 리액트 영역 밖과 상호작용하는 것이기 때문에 사이드 이펙트라고 볼 수 있습니다.

There is one flaw, though. The handler function should mostly be concerned about updating the state, but now it has a side-effect. If we use the `setSearchTerm` function elsewhere in our application, we will break the feature we implemented because we can't be sure the local storage will also get updated. Let's fix this by handling the side-effect at a dedicated place. We'll use **React's useEffect Hook** to trigger the side-effect each time the `searchTerm` changes:
하지만 한 가지 문제가 있습니다. 핸들러 함수는 상태를 업데이트 하는데 주력해야 하는데, 이제 사이드 이펙트도 가지고 있습니다. `setSearchTem` 함수를 애플리케이션의 다른 위치에서 사용하면 로컬 저장소도 업데이트될지 확신할 수 없기 때문에 기능을 망가뜨릴 수 있습니다. 사이드 이펙트를 정해진 장소해서 처리하도록 하여 이 문제를 고쳐봅시다. **useEffect** 훅을 사용하여 `searchTerm`이 바뀔 때마다 사이드 이펙트를 유발하도록 할 것입니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
 ...

 const [searchTerm, setSearchTerm] = React.useState(
   localStorage.getItem('search') || 'React'
 );

# leanpub-start-insert
 React.useEffect(() => {
   localStorage.setItem('search', searchTerm);
 }, [searchTerm]);
# leanpub-end-insert

# leanpub-start-insert
 const handleSearch = event => {
   setSearchTerm(event.target.value);
 };
# leanpub-end-insert

 ...
);
~~~~~~~

React's useEffect Hook takes two arguments: The first argument is a function where the side-effect occurs. In our case, the side-effect is when the user types the `searchTerm` into the browser's local storage. The second argument is a dependency array of variables. If one variable changes, the function for the side-effect is called. In our case, the function is called every time the `searchTerm` changes; it's called initially when the component renders for the first time.
useEffect 훅은 두 가지 인자를 받습니다. 첫 번째 인자는 사이드 이펙트가 일어나는 함수입니다. 위의 경우에서 사이드 이펙트는 사용자가 브라우저의 로컬 저장소에 `searchTerm`을 입력하는 것입니다. 두 번째 인자는 변수의 종속 배열입니다. 하나의 변수가 변하면 사이드 이펙트를 위한 함수가 불립니다. 위의 경우에서 함수는 컴포넌트가 처음 렌더링될 때를 시작으로 `searchTerm`이 변할 때마다 불립니다.

If the dependency array of React's useEffect is an empty array, the function for the side-effect is only called once, after the component renders for the first time. The hook lets us opt into React's component lifecycle. It can be triggered when the component is first mounted, but also one of its dependencies are updated.
useEffect의 종속 배열이 빈 배열이면, 사이드 이펙트를 위한 함수는 컴포넌트가 첫 렌더링될 때 단 한 번만 불립니다. 훅으로 리액트 컴포넌트 라이프 사이클에 맞춰갈 수 있습니다. 훅은 컴포넌트가 처음으로 마운트될 때 유발될 때 뿐만 아니라 종속성 중 하나가 업데이트 될 때 유발될 수 있습니다.

Using React `useEffect` instead of managing the side-effect in the handler has made the application more robust. *Whenever* and *wherever* `searchTerm` is updated via `setSearchTerm`, local storage will always be in sync with it.
핸들러 함수에서 사이드 이펙트를 관리하는 것보다 `useEffect`를 사용하는 것이 애플리케이션을 더 정확하게 만들어 줍니다. **언제 어디서나** `searchTerm`은 `setSearchTerm`을 통해 업데이트 되고, 로컬 저장소는 항상 그것과 동기화되어 있을 것입니다.

### Exercises:
### 읽어보기
* useEffect 훅에 대해 더 읽어보세요 ([0], [1]).

### 실습하기
* 마지막 장의 소스 코드를 확인하세요.
* 마지막 장의 변경 사항을 확인하세요.
* useEffect 훅의 첫 번째 인자로 `console.log()` 함수를 주고 종속 배열로 실험해 보세요. 빈 배열을 주었을 때의 로그도 확인해 보세요.

* Confirm your [source code for the last section](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/React-Side-Effects).
 * Confirm the [changes from the last section](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/Props-Handling...hs/React-Side-Effects?expand=1).
* Read more about React's useEffect Hook ([0](https://reactjs.org/docs/hooks-effect.html), [1](https://reactjs.org/docs/hooks-reference.html#useeffect)).
* Give the first argument's function a `console.log()` and experiment with React's useEffect Hook's dependency array. Check the logs for an empty dependency array too.