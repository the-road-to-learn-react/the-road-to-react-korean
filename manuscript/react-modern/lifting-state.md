## Lifting State in React
## 리액트 상태 위로 전달하기

Currently, the Search component still has its internal state. While we established a callback handler to pass information up to the App component, we are not using it yet. We need to figure out how to share the Search component's state across multiple components.
현재 Search 컴포넌트는 아직 내부 상태를 가지고 있습니다. App 컴포넌트에게 정보를 전달하기 위한 콜백 핸들러를 만들었지만, 사용하지 않고 있습니다. Search 컴포넌트의 상태를 여러 컴포넌트들과 공유하는 방법을 알아내야 합니다.  

The search term is needed in the App to filter the list before passing it to the List component as props. We'll need to **lift state up** from Search to App component to share the state with more components.
검색 용어는 List 컴포넌트에 프롭으로 전해지기 전에 App에서 리스트를 필터링하기 위해 필요합니다. 더 많은 컴포넌트와 상태를 공유할 수 있도록 Search 에서 App 컴포넌트로 **상태를 위로 전달**해야합니다.

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

We learned about the callback handler previously, because it helps us to keep an open communication channel from Search to App component. The Search component doesn't manage the state anymore, but only passes up the event to the App component after text is entered into the input field. You could also display the `searchTerm` again in the App component or Search component by passing it down as prop.
콜백 핸들러가 Search에서 App으로 가는 의사소통 채널을 유지한다고 배웠습니다. Search 컴포넌트는 입력 필드에 텍스트가 들어오면 더 이상 상태를 관리하지 않고 App 컴포넌트에 이벤트를 넘깁니다. App 컴포넌트나 Search 컴포넌트에서 prop으로 내려 받아 `searchTerm`을 표시할 수도 있었습니다. 

Always manage the state at a component where every component that's interested in it is one that either manages the state (using information directly from state) or a component below the managing component (using information from props). If a component below needs to update the state, pass a callback handler down to it (see Search component). If a component needs to use the state (e.g. displaying it), pass it down as props.
상태의 정보를 직접적으로 이용하여 관리하거나 관리하는 컴포넌트 아래에서 프롭으로 정보를 이용하는 컴포넌트만이 상태에 관여하는 컴포넌트에서 상태를 관리하세요. 아래의 컴포넌트가 상태를 업데이트 해야하면 콜백 핸들러를 내려 보내세요 (Search 컴포넌트의 예를 보세요). 컴포넌트가 상태를 이용해야 한다면 (예. 표시하기), 프롭으로 내려 보내세요.

By managing the search feature state in the App component, we can finally filter the list with the stateful `searchTerm` before passing the `list` to the List component:
App 컴포넌트의 검색 기능 상태를 관리함으로써 비로소 `list`를 List 컴포넌트에 보내기 전에 상태중심의 `searchTerm`을 이용하여 리스트를 필터링할 수 있게 되었습니다.

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

Here, the [JavaScript array's built-in filter function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter) is used to create a new filtered array. The filter function takes a function as an argument, which accesses each item in the array and returns true or false. If the function returns true, meaning the condition is met, the item stays in the newly created array; if the function returns false, it's removed:
자바스크립트 배열의 내장 필터링 함수로 새로운 필터링된 배열을 만들었습니다. 필터링 함수는 함수를 인자로 받아 배열의 각 요소를 접근한 뒤 참 또는 거짓을 리턴합니다. 조건을 만족하여 함수가 참을 리턴하면 요소는 새롭게 생성된 배열에 남고, 거짓을 리턴하면 제거됩니다.

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

The filter function checks whether the `searchTerm` is present in our story item's title, but it's still too opinionated about the letter case. If we search for "react", there is no filtered "React" story in your rendered list. To fix this problem, we have to lower case the story's title and the `searchTerm`.
필터링 함수는 `searchTerm`이 이야기 요소의 제목에 있는지 확인하지만 여전히 대문자/소문자 구분을 하지 못합니다. "react"를 검색하면 렌더링된 리스트에 필터링된 "React" 이야기는 없습니다. 이 문제를 해결하기 위해 이야기의 제목과 `searchTerm`을 소문자로 변경합니다.

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

Now you should be able to search for "eact", "React", or "react" and see one of two displayed stories. You have just added an interactive feature to your application.
이제 "eact", "React", 또는 "react"를 검색하여 두 결과 이야기 중 하나를 볼 수 있습니다. 이제 애플리케이션에 상호작용하는 기능을 추가하였습니다.

The remaining section shows a couple of refactoring steps. We will be using the final refactored version in the end, so it makes sense to understand these steps and keep them. As learned before, we can make the function more concise using a JavaScript arrow function:
남은 장은 리팩토링 단계를 보여줍니다. 마지막에는 최종 리팩토링된 버전을 사용할 것이기 때문에 리팩토링 단계를 이해하고 유지하는 것이 필요합니다. 이전에 배웠듯이, 자바스크립트 화살표 함수로 함수를 더 간략하게 나타낼 수 있습니다. 

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

In addition, we could turn the return statement into an immediate return, because no other task (business logic) happens before the return:
게다가 리턴하기 전에 아무 일 (비즈니스 로직)도 일어나지 않기 때문에, 리턴 문을 즉각 리턴으로 바꿀 수 있습니다.

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

That's all to the refactoring steps of the inlined function for the filter function. There are many variations to it -- and it's not always simple to keep a good balance between readable and conciseness -- however, I feel like keeping it concise whenever possible keeps it most of the time readable as well.
필터링 함수의 인라인 함수 리팩토링이 끝났습니다. 다른 방법도 가능하지만 -- 그리고 읽기 쉬운 코드와 간단한 코드 사이 좋은 균형을 찾는 것이 항상 쉽지는 않지만 -- 가능할 때마다 간단하게 만드는 것이 읽기 좋게 한다고 생각합니다.

Now we can manipulate state in React, using the Search component's callback handler in the App component to update it. The current state is used as a filter for the list. With the callback handler, we used information from the Search component in the App component to update the shared state and indirectly in the List component for the filtered list.
이제 App 컴포넌트에 있는 Search 컴포넌트의 콜백 핸들러로 리액트에서 상태를 관리할 수 있습니다. 현재 상태는 리스트를 필터링하는데 사용합니다. 콜백 핸들러로 Search 컴포넌트에 있는 정보를 App 컴포넌트에서 사용하여 공유하는 상태를 업데이트하고 간접적으로 List 컴포넌트의 필터링된 리스트까지 변경하였습니다.

### Exercises:
### 실습하기
* 마지막 장의 소스 코드를 확인하세요.
* 마지막 장의 변경 사항을 확인하세요.

* Confirm your [source code for the last section](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/Lifting-State-in-React).
 * Confirm the [changes from the last section](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/Callback-Handler-in-JSX...hs/Lifting-State-in-React?expand=1).