## 리액트 컴포넌트 제어

**제어 가능한 컴포넌트**는 리액트 컴포넌트가 아닌 HTML 엘리먼트입니다. 이 장에서 검색 컴포넌트와 입력 필드를 제어하는 방법에 대해 알아 보겠습니다.

리액트 애플리케이션에서 컴포넌트를 제어하는 이유에 대한 시나리오를 살펴 보겠습니다. 여러분은 `searchTerm`에 초기 상태를 제공하고 변경 사항을 적용한 후의 오류를 브라우저상에서 발견 할 수 있습니까?

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
 const stories = [ ... ];

# leanpub-start-insert
 const [searchTerm, setSearchTerm] = React.useState('React');
# leanpub-end-insert

 ...
};
~~~~~~~

초기 상태에 따라 목록이 필터링 되었지만 입력 필드에 초기 `searchTerm`가 표시되지 않습니다. 우리는 입력 필드가 초기 상태에 따라 실제 `searchTerm`에 반영되기를 원합니다. 하지만 이곳에서는 필터링 된 목록에만 반영됩니다.

입력 필드가 있는 검색 컴포넌트를 제어 가능한 컴포넌트로 변환해야합니다. 현재까지는 입력 필드가 `searchTerm`에 대해 아무것도 모릅니다. 변경 사항을 알려주기 위해서 이벤트 변경을 사용합니다. 입력 필드에 `value(값)` 속성이 있는 것을 확인 하세요.

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
 const stories = [ ... ];

 const [searchTerm, setSearchTerm] = React.useState('React');

 ...

 return (
   <div>
     <h1>My Hacker Stories</h1>

# leanpub-start-insert
     <Search search={searchTerm} onSearch={handleSearch} />
# leanpub-end-insert

     ...
   </div>
 );
};

const Search = props => (
 <div>
   <label htmlFor="search">Search: </label>
   <input
     id="search"
     type="text"
# leanpub-start-insert
     value={props.search}
# leanpub-end-insert
     onChange={props.onSearch}
   />
 </div>
);
~~~~~~~

이제 입력 필드는 `searchTerm`을 사용하여 리액트의 상태 초기 값을 보여줍니다. 또한 `searchTerm`을 변경할 때 입력 필드가 리액트의 상태 값 (props를 통한)을 사용하도록합니다. 이전에는 입력 필드가 HTML만으로 자체 내부 상태를 관리했습니다.

이 장에서는 컴포넌트의 제어 방법에 대해 배웠고 이전 장까지는 **단방향 데이터 흐름**에 대해 배웠습니다.

{title="Visualization",lang="javascript"}
~~~~~~~
UI -> Side-Effect -> State -> UI -> ...
~~~~~~~

리액 애플리케이션 및 해당 컴포넌트는 초기 상태로 시작하며 다른 컴포넌트에 props로 전달 될 수 있습니다. UI로 처음 렌더링됩니다. API에서 사용자 입력 또는 데이터로드와 같은 현상이 발생하면 변경 사항이 리액트의 상태로 감지됩니다. 상태가 변경되면 수정 된 상태 또는 수정 된 props의 영향을받는 모든 컴포넌트가 다시 렌더링됩니다 (컴포넌트의 함수가 다시 실행 됨).

이전 장에서는 리액트의 **컴포넌트 라이프사이클**에 대해서도 배웠습니다. 처음에는 모든 컴포넌트가 컴포넌트 계층의 맨 위에서 맨 아래로 인스턴스화됩니다. 여기에는 초기 값 (예 : 초기 상태)으로 인스턴스화 된 모든 훅 (예 : `useState`)이 포함됩니다. 거기에서 UI는 사용자 상호 작용과 같은 사이트 이펙트를 기다립니다. 상태가 변경되면 (예 : `useState`에서 상태 업데이터 기능을 통해 현재 상태가 변경됨) 수정 된 상태 / props의 영향을받는 모든 구성 요소가 다시 렌더링됩니다.

컴포넌트의 함수를 실행할 때마다 훅에서 *최신 값* (예 : 현재 상태)을 취하고 다시 초기화하지 않습니다 (예 : 초기 상태). `useState` 훅 함수가 초기 값으로 다시 초기화된다고 가정 할 수 있기 때문에 이상하게 보일 수 있지만 그렇지 않습니다. 컴포넌트가 처음 렌더링 될 때 훅이 한 번만 초기화 된 후 리액트가 가장 최근 값으로 감지합니다.

### 실습하기

* [마지막 장의 소스 코드를 확인하세요.](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/React-Controlled-Components)
 * [마지막 장의 변경 사항을 확인하세요.](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/Lifting-State-in-React...hs/React-Controlled-Components?expand=1)
* [리액트 컴포넌트 제어 방법](https://www.robinwieruch.de/react-controlled-components/)에 대해 자세히 알아보세요.
* 리액트 컴포넌트에서 `console.log()`를 사용하여 입력 필드가 변경 될 때마다 변경 사항이 어떻게 렌더링되는지 확인하세요.