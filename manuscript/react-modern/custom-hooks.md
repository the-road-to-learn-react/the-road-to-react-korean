## 리액트 커스텀 훅(심화)

지금까지 우리는 리액트에서 가장 자주 사용하는 두 가지 훅인 useState와 useEffect를 다루었습니다. useState는 애플리케이션에 상호작용을 구현하기 위해, useEffect는 컴포넌트의 생명주기 메서드를 구현하기 위해 사용됩니다.

이제 리액트에서 사용할 수 있는 더 많은 훅에 대해 알아봅시다. 이 장에서 훅에 대한 모든 내용을 다루지는 않을 겁니다. 그중에서 **React custom Hooks**를 다룹니다. 즉, 여러분만의 훅을 직접 만드는 것입니다.

이미 만들어놓은 두 개의 훅을 사용하여 `useSemiPersistentState`라는 이름의 새로운 커스텀 훅을 만들 것입니다. 상태를 관리하면서 로컬 스토리지와 동기화되기 때문에 이렇게 이름을 지었습니다. 브라우저의 로컬 스토리지를 삭제하면 이 애플리케이션에 대한 데이터가 삭제되므로 영구적이지 않는다는 점을 알아두세요. 먼저 App 컴포넌트에서 커스텀 훅으로 구현과 관련한 모든 정보를 가져옵니다.

{title="src/App.js",lang="javascript"}

~~~~~~~
# leanpub-start-insert
const useSemiPersistentState = () => {
 const [searchTerm, setSearchTerm] = React.useState(
   localStorage.getItem('search') || ''
 );

 React.useEffect(() => {
   localStorage.setItem('search', searchTerm);
 }, [searchTerm]);
};
# leanpub-end-insert

const App = () => {
...
};
~~~~~~~

여기까지는 앞서 App 컴포넌트에서 사용했던 `useState` 및 `useEffect` 함수입니다. 이것들을 사용하기 전에, 이 커스텀 훅에서 필요한 값을 반환해 봅시다.

{title="src/App.js",lang="javascript"}

~~~~~~~
const useSemiPersistentState = () => {
 const [searchTerm, setSearchTerm] = React.useState(
   localStorage.getItem('search') || ''
 );

 React.useEffect(() => {
   localStorage.setItem('search', searchTerm);
 }, [searchTerm]);

# leanpub-start-insert
 return [searchTerm, setSearchTerm];
# leanpub-end-insert
};
~~~~~~~

여기서는 리액트의 내장 훅에 관한 두 가지 규칙을 따르고 있습니다. 첫째, 모든 훅 이름 앞에 "use" 접두사를 붙이는 규칙입니다. 둘째, 반환 값은 배열로 반환되어야 합니다. 이제 배열 구조분해를 통해 App 컴포넌트의 반환 값과 함께 커스텀 훅을 사용할 수 있습니다.

{title="src/App.js",lang="javascript"}

~~~~~~~
const App = () => {
 const stories = [ ... ];

# leanpub-start-insert
 const [searchTerm, setSearchTerm] = useSemiPersistentState();
# leanpub-end-insert

 const handleSearch = event => {
   setSearchTerm(event.target.value);
 };

 const searchedStories = stories.filter(story =>
   story.title.toLowerCase().includes(searchTerm.toLowerCase())
 );

 return (
   ...
 );
};
~~~~~~~

커스텀 훅의 또 다른 목표는 재사용할 수 있어야 합니다. 이 커스텀 훅은 현재 검색에 대한 것이지만, 일반적으로 훅은 상태가 설정되고 로컬 스토리지에서 동기화된 값에 대한 것이어야 합니다. 따라서 이름을 조정하겠습니다.

{title="src/App.js",lang="javascript"}

~~~~~~~
const useSemiPersistentState = () => {
# leanpub-start-insert
 const [value, setValue] = React.useState(
   localStorage.getItem('value') || ''
# leanpub-end-insert
 );

 React.useEffect(() => {
# leanpub-start-insert
   localStorage.setItem('value', value);
 }, [value]);
# leanpub-end-insert

# leanpub-start-insert
 return [value, setValue];
# leanpub-end-insert
};
~~~~~~~

커스텀 훅은 안에서 추상화된 "값"을 처리합니다. App 컴포넌트에서 이 기능을 사용하면 배열 구조분해를 통해 반환된 현재 상태와 상태를 업데이트하는 함수를 도메인과 관련된 이름으로 지정할 수 있습니다(예 :`searchTerm` 및`setSearchTerm`).

이 커스텀 훅에는 여전히 한 가지 문제가 있습니다. 리액트 애플리케이션에서 커스텀 훅을 두 번 이상 사용하면 로컬 스토리지에서 "값"에 할당된 항목을 덮어씌운다는 점입니다. 이 문제를 해결하려면 키와 함께 전달해야 합니다.

{title="src/App.js",lang="javascript"}

~~~~~~~
# leanpub-start-insert
const useSemiPersistentState = key => {
# leanpub-end-insert
 const [value, setValue] = React.useState(
# leanpub-start-insert
   localStorage.getItem(key) || ''
# leanpub-end-insert
 );

 React.useEffect(() => {
# leanpub-start-insert
   localStorage.setItem(key, value);
 }, [value, key]);
# leanpub-end-insert

 return [value, setValue];
};

const App = () => {
 ...

 const [searchTerm, setSearchTerm] = useSemiPersistentState(
# leanpub-start-insert
   'search'
# leanpub-end-insert
 );

 ...
};
~~~~~~~

이때 키가 외부에서 오기 때문에 커스텀 훅은 키가 변경될 수 있음을 염두에 두어야 합니다. 그렇기에 키와 값은 `useEffect`의 종속성 배열에 포함되어야 합니다. 그렇지 않으면 렌더링 간에 키가 변경되었을 때 오래된 키(*stale*라고도 함)로 인해 부작용이 일어날 수 있습니다.

또 다른 개선 사항은 외부에서 가져온 초기 상태를 커스텀 훅에서 초기 상태로 설정하는 것입니다.

{title="src/App.js",lang="javascript"}

~~~~~~~
# leanpub-start-insert
const useSemiPersistentState = (key, initialState) => {
# leanpub-end-insert
 const [value, setValue] = React.useState(
# leanpub-start-insert
   localStorage.getItem(key) || initialState
# leanpub-end-insert
 );

 ...
};

const App = () => {
 ...

 const [searchTerm, setSearchTerm] = useSemiPersistentState(
# leanpub-start-insert
   'search',
   'React'
# leanpub-end-insert
 );

 ...
};
~~~~~~~

이렇게 첫 번째 커스텀 훅을 만들었습니다. 만약 커스텀 훅이 마음에 들지 않다면 변경 내용을 되돌리고 이전처럼 `useState` 및 `useEffect` 훅을 사용해도 됩니다.

그러나 커스텀 훅에 대해 알고 있으면 더 많은 선택지가 제공됩니다. 커스텀 훅은 컴포넌트에서 멀리 떨어져 있어야 하는 중요한 구현 정보를 캡슐화할 수 있습니다. 또한 둘 이상의 리액트 컴포넌트에서 사용될 수 있습니다. 외부 라이브러리로 만들어 오픈 소스로 제공할 수도 있습니다. 자주 사용하는 검색 엔진을 여러분의 애플리케이션에서 사용할 때, 수백 개의 리액트 훅을 구현에 대한 걱정 없이 사용할 수 있는 것처럼요.

### Exercises:

* [마지막 장의 소스 코드](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/React-Custom-Hooks)를 확인하세요.
 * [마지막 장의 변경 사항](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/React-Side-Effects...hs/React-Custom-Hooks?expand=1)을 확인하세요.
* [리액트 훅](https://www.robinwieruch.de/react-hooks)에 대한 자세한 내용을 읽어보세요. 리액트 함수형 컴포넌트의 필수 요소이므로, 정확히 이해하는 게 중요합니다([0](https://reactjs.org/docs/hooks-overview.html), [1](https://reactjs.org/docs/hooks-custom.html)).

