## 리액트 사이드 이펙트

다음으로 Search 컴포넌트에 또 다른 훅의 형태로 기능을 추가하겠습니다. Search 컴포넌트가 가장 최근의 검색 상호작용을 기억하게 하고 브라우저가 재시작할 때 애플리케이션이 그 결과를 열도록 할 것입니다. 

브라우저의 로컬 저장소에 식별자를 동반한 `searchTerm`을 저장합니다. 다음으로, 저장된 값이 존재하면 `searchTerm`의 초기 상태를 설정하는 데 사용하고 그렇지 않으면 초기 상태를 이전처럼 기본값 ("React")으로 둡니다.

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

입력 필드를 사용한 뒤 브라우저의 탭을 새로고침하면 브라우저는 가장 최근의 검색어를 기억해야 합니다. 리액트에서 로컬 저장소를 사용하는 것은 브라우저 API를 이용해 리액트 영역 밖과 상호작용하는 것이기 때문에 사이드 이펙트라고 볼 수 있습니다.

하지만 한 가지 문제가 있습니다. 핸들러 함수는 상태를 업데이트하는데 주력해야 하는데, 이제 사이드 이펙트도 가집니다. `setSearchTem` 함수를 애플리케이션의 다른 위치에서 사용하면 로컬 저장소도 함께 업데이트될지 확신할 수 없기 때문에 구현한 기능을 망가뜨릴 수 있습니다. 사이드 이펙트를 정해진 장소에서 처리하도록 하여 이 문제를 해결해봅시다. **useEffect** 훅을 사용하여 `searchTerm`이 바뀔 때마다 사이드 이펙트를 유발하도록 할 것입니다.

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

useEffect 훅은 두 가지 인수를 받습니다. 첫 번째 인수는 사이드 이펙트가 일어나는 함수입니다. 위의 경우에서 사이드 이펙트는 사용자가 브라우저의 로컬 저장소에 `searchTerm`을 입력하는 것입니다. 두 번째 인수는 변수의 종속성 배열입니다. 하나의 변수가 변하면 사이드 이펙트를 포함하는 함수가 불립니다. 위의 경우에서 함수는 컴포넌트가 처음 렌더링될 때를 시작으로 `searchTerm`이 변할 때마다 불립니다.

useEffect의 종속성 배열이 빈 배열이면, 사이드 이펙트를 포함하는 함수는 컴포넌트가 첫 렌더링될 때 단 한 번만 불립니다. 이렇게 훅으로 리액트 컴포넌트 생명주기에 동참할 수 있습니다. 훅은 컴포넌트가 처음으로 마운트될 때 뿐만 아니라 종속성 중 하나가 업데이트 될 때 유발될 수 있습니다.

Using React `useEffect` instead of managing the side-effect in the handler has made the application more robust. *Whenever* and *wherever* `searchTerm` is updated via `setSearchTerm`, local storage will always be in sync with it.

핸들러 함수에서 사이드 이펙트를 관리하는 대신 `useEffect`를 사용하여 애플리케이션을 더 탄탄하게 만들었습니다. **언제 어디서나** `searchTerm`은 `setSearchTerm`을 통해 업데이트 되고, 로컬 저장소는 항상 그것과 동기화되어 있을 것입니다.

### 읽어보기
* useEffect 훅에 대해 더 읽어보세요 ([0](https://reactjs.org/docs/hooks-effect.html), [1](https://reactjs.org/docs/hooks-reference.html#useeffect)).

### 실습하기
* [마지막 장의 소스 코드](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/React-Side-Effects)를 확인하세요.
* [마지막 장의 변경 사항](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/Props-Handling...hs/React-Side-Effects?expand=1)을 확인하세요.
* useEffect 훅의 첫 번째 인수로 `console.log()` 함수를 주고 종속 배열로 실험해 보세요. 빈 배열을 주었을 때의 로그도 확인해 보세요.