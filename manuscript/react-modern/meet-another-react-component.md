## 컴포넌트 분리

지금까지는 App 컴포넌트만을 사용하여 애플리케이션을 만들었습니다. 이전 장에서는 리스트를 렌더링하기 위해 필요한 모든 것들을 App 컴포넌트에서 처리했습니다. 계속해서 기능을 추가하고 개발하다보면 App 컴포넌트의 점점 규모가 커질 겁니다. 드디어 이 컴포넌트를 작은 컴포넌트 덩어리로 분리 작업을 시작할 때입니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const list = [ ... ];

function App() { ... }

# leanpub-start-insert
function List() {
  return list.map(function(item) {
    return (
      <div key={item.objectID}>
        <span>
          <a href={item.url}>{item.title}</a>
        </span>
        <span>{item.author}</span>
        <span>{item.num_comments}</span>
        <span>{item.points}</span>
      </div>
    );
  });
}
# leanpub-end-insert
~~~~~~~

반환된 JSX의 가장 바깥 부분이 자바스크립트로 시작하기 때문에 컴포넌트가 이상하게 보일 수 있습니다. HTML 요소로 감싸는 방법도 있지만, 우선은 이전에 하던 방식대로 계속하겠습니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
function List() {
# leanpub-start-insert
  return (
    <div>
      {list.map(function(item) {
# leanpub-end-insert
        return (... );
# leanpub-start-insert
      })}
    </div>
  );
# leanpub-end-insert
}
~~~~~~~

이제 새로운 List 컴포넌트를 App 컴포넌트 안에서 사용할 수 있게 됩니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
function App() {
  return (
    <div>
      <h1>My Hacker Stories</h1>

      <label htmlFor="search">Search: </label>
      <input id="search" type="text" />

      <hr />

# leanpub-start-insert
      <List />
# leanpub-end-insert
    </div>
  );
}
~~~~~~~

이렇게 우리의 첫번째 리액트 컴포넌트를 만들었습니다! 이 예제를 통해 컴포넌트가 어떻게 중요한 작업들을 캡슐화하여 대규모 리액트 애플리케이션에서 동작하는지 확인할 수 있었습니다.

대규모 리액트 애플리케이션들은 **컴포넌트 계층 구조**(**컴포넌트 트리**로도 불림)를 가집니다. 일반적으로 컴포넌트 트리의 가장 높은 곳에는 **최상위 컴포넌트**(예: App)가 하나 있습니다. App은 List의 **부모 컴포넌트**이며, List는 App의 **자식 컴포넌트**가 됩니다. 컴포넌트 트리에서 App은 **루트 컴포넌트**이며, 다른 컴포넌트를 렌더링하지 않는 컴포넌트는 **리프 컴포넌트**(예: List)입니다. App은 List와 마찬가지로 여러 자식 컴포넌트를 가질 수 있습니다. 만약 App에 다른 자식 컴포넌트를 추가한다면, 추가된 자식 컴포넌트는 List의 **형제 컴포넌트**가 됩니다.

### 읽어보기

* [지난 장에서 사용한 코드](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/Meet-another-React-Component)를 확인하세요.
  * [지난 장에서 수정된 코드](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/Lists-in-React...hs/Meet-another-React-Component?expand=1)도 확인하세요.
* 종이 위에 컴포넌트들(App 컴포넌트와 List 컴포넌트)을 컴포넌트 트리로 그려보세요. 다른 컴포넌트(예: App 컴포넌트에 있는 input 영역과 label을 Search 컴포넌트로 구성)를 추가하여 컴포넌트 트리를 확장해보세요. 독립 컴포넌트로 사용할 수 있는 다른 부분도 함께 찾아보세요.
* 만약 Search 컴포넌트가 App 컴포넌트 안에서 사용된다면, Search 컴포넌트는 List 컴포넌트의 형제, 부모, 자식 컴포넌트 중 어떤 것에 해당될까요?
* 만약 `list` 변수를 지금처럼 전역 변수로 사용한다면 어떤 문제가 발생할지 생각해보세요. 이러한 문제를 다루는 방법은 다음 장에서 다루겠습니다.