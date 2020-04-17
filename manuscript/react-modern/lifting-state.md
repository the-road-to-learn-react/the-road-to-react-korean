## 리액트 상태 끌어올리기

현재 Search 컴포넌트는 아직 자신의 내부 상태를 가지고 있습니다. App 컴포넌트에 정보를 전달하기 위한 콜백 핸들러를 만들었지만, 아직 사용하지 않았습니다. Search 컴포넌트의 상태를 여러 컴포넌트와 공유하는 방법을 찾아야 합니다.  

App 컴포넌트에서 리스트를 필터링하여 List 컴포넌트의 props로 전달하는 데 검색어가 필요합니다. 더 많은 컴포넌트와 상태를 공유할 수 있도록 Search에서 App 컴포넌트로 **상태를 끌어올려야** 합니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
 const stories = [ ... ];

# leanpub-start-insert
 const [searchTerm, setSearchTerm] = React.useState('');
# leanpub-end-insert

 const handleSearch = event => {
# leanpub-start-insert
   setSearchTerm(event.target.value);
# leanpub-end-insert
 };

 return (
   <div>
     <h1>My Hacker Stories</h1>

     <Search onSearch={handleSearch} />

     <hr />

     <List list={stories} />
   </div>
 );
};

const Search = props => (
 <div>
   <label htmlFor="search">Search: </label>
# leanpub-start-insert
   <input id="search" type="text" onChange={props.onSearch} />
# leanpub-end-insert
 </div>
);
~~~~~~~

Search에서 App 컴포넌트로의 열린 의사소통 채널을 유지하는 데 도움이 되는 콜백 핸들러를 배웠습니다. Search 컴포넌트는 이제 상태를 관리하지 않고 입력 필드에 글자가 입력되면 App 컴포넌트에 이벤트를 전달합니다. `searchTerm`을 App 컴포넌트에서 보여주거나 Search 컴포넌트에 prop으로 전달하여 다시 보여줄 수도 있습니다. 

항상 연관된 모든 컴포넌트가 상태를 관리하는 컴포넌트 (상태에서 직접 정보를 사용)이거나 그 아래에서 props를 통해서 가져온 정보를 사용하는 컴포넌트일 때만 상태를 관리하세요. 아래의 컴포넌트가 상태를 업데이트해야 하면 콜백 핸들러를 내려보내세요. (Search 컴포넌트의 예를 확인하세요) 컴포넌트가 상태를 이용해야 한다면 (예. 보여주기), props로 내려보내세요.

App 컴포넌트 검색 기능의 상태를 관리함으로써 비로소 `list`를 List 컴포넌트에 보내기 전에 상태를 가지는 `searchTerm`으로 필터링할 수 있게 되었습니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
 const stories = [ ... ];

 const [searchTerm, setSearchTerm] = React.useState('');

 const handleSearch = event => {
   setSearchTerm(event.target.value);
 };

# leanpub-start-insert
 const searchedStories = stories.filter(function(story) {
   return story.title.includes(searchTerm);
 });
# leanpub-end-insert

 return (
   <div>
     <h1>My Hacker Stories</h1>

     <Search onSearch={handleSearch} />

     <hr />

# leanpub-start-insert
     <List list={searchedStories} />
# leanpub-end-insert
   </div>
 );
};
~~~~~~~

[자바스크립트 배열의 내장 필터링 함수](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)로 필터링된 배열을 생성했습니다. 필터링 함수는 배열의 각 요소에 접근한 뒤 참 또는 거짓을 반환하는 함수를 인자로 받습니다. 조건을 만족하여 함수가 참을 반환하면 요소는 새롭게 생성된 배열에 남고, 거짓을 반환하면 제거됩니다.

{title="Code Playground",lang="javascript"}
~~~~~~~
const words = [
 'spray',
 'limit',
 'elite',
 'exuberant',
 'destruction',
 'present'
];

const filteredWords = words.filter(function(word) {
 return word.length > 6;
});

console.log(filteredWords);
// ["exuberant", "destruction", "present"]
~~~~~~~

필터링 함수는 `searchTerm`이 이야기 항목의 제목에 있는지 확인하지만 여전히 대, 소문자 구분을 하지 못합니다. "react"를 검색하면 렌더링된 리스트에 필터링된 "React" 이야기는 없습니다. 이 문제를 해결하기 위해 이야기의 제목과 `searchTerm`을 소문자로 변경해야 합니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
 ...

 const searchedStories = stories.filter(function(story) {
# leanpub-start-insert
   return story.title
     .toLowerCase()
     .includes(searchTerm.toLowerCase());
# leanpub-end-insert
 });

 ...
};
~~~~~~~

이제 "eact", "React", 또는 "react"를 검색하여 나온 두 이야기 중 하나를 볼 수 있습니다. 이로써 애플리케이션에 상호작용하는 기능이 추가하였습니다.

남은 장은 리팩토링 단계를 보여줍니다. 결국은 최종적으로 리팩토링된 버전을 사용할 것이기 때문에 리팩토링 단계를 이해하고 유지해야 합니다. 이전에 배웠듯이, 자바스크립트 화살표 함수로 함수를 더 간결하게 나타낼 수 있습니다. 

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
 ...

# leanpub-start-insert
 const searchedStories = stories.filter(story => {
# leanpub-end-insert
   return story.title
     .toLowerCase()
     .includes(searchTerm.toLowerCase());
 });

 ...
};
~~~~~~~

게다가 반환하기 전에 아무 일 (비즈니스 로직)도 일어나지 않기 때문에, return 구문을 즉시 return하는 것으로 바꿀 수 있습니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
 ...

# leanpub-start-insert
 const searchedStories = stories.filter(story =>
   story.title.toLowerCase().includes(searchTerm.toLowerCase())
 );
# leanpub-end-insert

 ...
};
~~~~~~~

필터링 함수의 인라인 함수 리팩토링이 끝났습니다. 물론 다른 리팩토링 방법도 존재하고, 읽기 쉬운 코드와 간결한 코드 사이 좋은 균형을 찾는 것이 항상 쉽지는 않지만 가능할 때마다 코드를 간결하게 만드는 것이 대부분의 경우 읽기 좋게 만듭니다.

이제 App 컴포넌트에 있는 Search 컴포넌트의 콜백 핸들러로 상태를 업데이트하는 방식으로 리액트에서 상태를 관리할 수 있습니다. 현재 상태는 리스트를 필터링하는데 사용합니다. 콜백 핸들러로 Search 컴포넌트에 있는 정보를 App 컴포넌트에서 사용하여 공유 상태를 업데이트하고 간접적으로 List 컴포넌트의 필터링된 리스트까지 변경하였습니다.

### 실습하기
* [마지막 장의 소스 코드](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/Lifting-State-in-React)를 확인하세요.
* [마지막 장의 변경 사항](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/Callback-Handler-in-JSX...hs/Lifting-State-in-React?expand=1)을 확인하세요.