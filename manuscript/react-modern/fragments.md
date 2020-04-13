## 리액트 Fragments

JSX에서, 특히 Search 컴포넌트를 만들 때 한 가지 주의할 것이 있습니다. 렌더링하기 위해 HTML을 감싸는 요소를 만들어야 한다는 것입니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const Search = ({ search, onSearch }) => (
# leanpub-start-insert
 <div>
# leanpub-end-insert
   <label htmlFor="search">Search: </label>
   <input
     id="search"
     type="text"
     value={search}
     onChange={onSearch}
   />
# leanpub-start-insert
 </div>
# leanpub-end-insert
);
~~~~~~~

보통 리액트 컴포넌트가 반환하는 JSX에는 다른 요소를 감싸는 단 하나의 최상위 요소만 있어야 합니다. 여러 최상위 요소를 나란히 렌더링하려면 대신 배열에 담아야 합니다. 요소의 리스트를 다룰 때는 모든 형제 요소에 리액트의 `key` 속성을 지정해야 합니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const Search = ({ search, onSearch }) => [
 <label key="1" htmlFor="search">
   Search:{' '}
 </label>,
 <input
   key="2"
   id="search"
   type="text"
   value={search}
   onChange={onSearch}
 />,
];
~~~~~~~

이는 JSX에서 여러 최상위 요소를 담는 방법의 하나입니다. 추가적인 key 속성으로 코드가 장황해져서 읽기가 쉽지 않습니다. 또 다른 방법은 **리액트 fragment**를 사용하는 것입니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const Search = ({ search, onSearch }) => (
# leanpub-start-insert
 <>
# leanpub-end-insert
   <label htmlFor="search">Search: </label>
   <input
     id="search"
     type="text"
     value={search}
     onChange={onSearch}
   />
# leanpub-start-insert
 </>
# leanpub-end-insert
);
~~~~~~~

fragment는 추가적인 요소를 렌더링하지 않으면서 다른 요소를 하나의 최상위 요소로 감쌉니다. 이제 브라우저에 입력 필드와 라벨이 있는 두 검색 요소가 표시됩니다. `<div>` 또는 `<span>` 같은 감싸는 요소를 생략하고 싶다면 JSX에서 허용하는 빈 태그로 대체하여 중간 요소 없이 HTML을 렌더링할 수 있습니다.

### 실습하기

* [마지막 장의 소스 코드](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/React-Fragments)를 확인하세요.
 * [마지막 장의 변경 사항](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/React-Custom-Hooks...hs/React-Fragments?expand=1)을 확인하세요.
* [리액트 fragments](https://reactjs.org/docs/fragments.html)에 대해 자세히 알아보세요.