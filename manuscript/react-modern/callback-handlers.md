## JSX의 콜백 핸들러

이제 Search 컴포넌트를 독립적으로 분리하고 App 컴포넌트에 해당 인스턴스를 만들어 인풋 필드와 라벨을 살펴보겠습니다. 이 과정을 통해 Search 컴포넌트와 List 컴포넌트는 서로 형제 컴포넌트가 됩니다. 또한 핸들러와 상태를 Search 컴포넌트로 옮겨서 기능을 그대로 유지해보겠습니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  const stories = [ ... ];

  return (
    <div>
      <h1>My Hacker Stories</h1>

# leanpub-start-insert
      <Search />
# leanpub-end-insert

      <hr />

      <List list={stories} />
    </div>
  );
};

# leanpub-start-insert
const Search = () => {
  const [searchTerm, setSearchTerm] = React.useState('');

  const handleChange = event => {
    setSearchTerm(event.target.value);
  };

  return (
    <div>
      <label htmlFor="search">Search: </label>
      <input id="search" type="text" onChange={handleChange} />

      <p>
        Searching for <strong>{searchTerm}</strong>.
      </p>
    </div>
  );
};
# leanpub-end-insert
~~~~~~~

추출된 Search 컴포넌트는 상태를 다루면서 내용을 표시하지 않고 상태를 보여줍니다. 컴포넌트는 `searchTerm`을 텍스트로 표시하지만, 아직 이 정보를 부모나 형제 컴포넌트와 공유하지는 않습니다. Search 컴포넌트는 검색어를 보여주는 것 외에 아무것도 실행하지 않기 때문에 다른 컴포넌트에는 사용할 수 없습니다.

props는 자연스럽게 아래 방향으로만 전달되므로 자바스크립트 데이터 타입으로서 정보를 컴포넌트 구조에 전달할 방법은 없습니다. 그러나 함수로 **콜백 핸들러**를 사용할 수 있습니다. 선언한 콜백 함수는(A) 다른 곳에서 사용되지만(B) 도입된 위치에서 "다시 호출"됩니다(C).

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  const stories = [ ... ];

# leanpub-start-insert
  // A
  const handleSearch = event => {
    // C
    console.log(event.target.value);
  };
# leanpub-end-insert

  return (
    <div>
      <h1>My Hacker Stories</h1>

# leanpub-start-insert
      <Search onSearch={handleSearch} />
# leanpub-end-insert

      <hr />

      <List list={stories} />
    </div>
  );
};

# leanpub-start-insert
const Search = props => {
# leanpub-end-insert
  const [searchTerm, setSearchTerm] = React.useState('');

  const handleChange = event => {
    setSearchTerm(event.target.value);

# leanpub-start-insert
    // B
    props.onSearch(event);
# leanpub-end-insert
  };

  return ( ... );
};
~~~~~~~

각 코드 블록이 실행하는 작업을 알려주므로 소스 코드에서 주석으로 A, B와 C를 생략하세요. 콜백 핸들러의 개념을 생각해봅시다. 한 컴포넌트(App)에서 다른 컴포넌트(Search)로 함수를 전달하고 두 번째 컴포넌트(Search)에서 그 함수를 사용합니다. 그러나 첫 번째 컴포넌트(App)에서 함수 호출의 실제 콜백을 이용합니다. 이렇게 하면 컴포넌트 구조를 통해 소통할 수 있습니다. 한 컴포넌트에서 사용된 핸들러 함수는 콜백 핸들러가 되어 리액트 props를 통해 컴포넌트로 전해져 내려옵니다. 리액트 props는 항상 컴포넌트 구조를 따라 정보로 전달되며, props에서 함수로 전달된 콜백 핸들러는 컴포넌트 계층을 따라 통신할 때 사용할 수 있습니다.

### 실습하기

* [마지막 장의 소스 코드](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/Callback-Handler-in-JSX)를 확인하세요.
  * [마지막 장의 변경 사항](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/React-State...hs/Callback-Handler-in-JSX?expand=1)을 확인하세요.
* 필요한 만큼 핸들러와 콜백 핸들러의 개념을 다시 살펴보세요.