## 리액트 리스트

지금까지 JSX에서 몇 가지 기본 변수를 렌더링했습니다. 다음으로 리스트 목록을 렌더링해 봅시다. 우선 샘플 데이터로 만들어본 후, 외부 API에서 데이터를 가져오는 실습을 진행할 예정입니다. 먼저 배열을 변수로 정의합니다. 이전과 마찬가지로 컴포넌트 외부 또는 내부에서 변수를 정의할 수 있습니다. 아래 예제에서는 컴포넌트 외부에서 정의합니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
import React from 'react';

# leanpub-start-insert
const list = [
  {
    title: 'React',
    url: 'https://reactjs.org/',
    author: 'Jordan Walke',
    num_comments: 3,
    points: 4,
    objectID: 0,
  },
  {
    title: 'Redux',
    url: 'https://redux.js.org/',
    author: 'Dan Abramov, Andrew Clark',
    num_comments: 2,
    points: 5,
    objectID: 1,
  },
];
# leanpub-end-insert

function App() { ... }

export default App;
~~~~~~~

위 코드를 보면 `...`라는 표시가 보일 겁니다. App 컴포넌트의 전체 코드를 적지 않음으로써 예제 코드의 길이를 줄일 수 있고, 코드에서 중요한 부분(`list`변수가 App 컴포넌트 외부에 선언된 것)을 강조할 수 있습니다. 이전 예제에 한 번 등장했던 코드는 앞으로 `...`를 사용하여 대체할 예정입니다. 만약 이해가 잘 안 간다면, 매 장의 마지막 부분에 있는 CodeSandbox 링크를 통해서 전체 코드를 확인하세요.

리스트에 있는 아이템은 각각 제목, url, 저자, 식별자(`objectID`), 인기도를 나타내는 포인트, 댓글 수를 가집니다. 이제 JSX로 리스트를 동적으로 렌더링해 봅시다.

{title="src/App.js",lang="javascript"}
~~~~~~~
function App() {
  return (
    <div>
# leanpub-start-insert
      <h1>My Hacker Stories</h1>
# leanpub-end-insert

      <label htmlFor="search">Search: </label>
      <input id="search" type="text" />

# leanpub-start-insert
      <hr />
# leanpub-end-insert

# leanpub-start-insert
      {/* 여기에서 리스트가 렌더링 됩니다 */}
# leanpub-end-insert
    </div>
  );
}
~~~~~~~

[자바스크립트 배열 map 메서드](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)을 사용하면 리스트에 있는 각 아이템에 접근하고 이들을 새로운 리스트로 반환할 수 있습니다.

{title="Code Playground",lang="javascript"}
~~~~~~~
const numbers = [1, 4, 9, 16];

const newNumbers = numbers.map(function(number) {
  return number * 2;
});

console.log(newNumbers);
// [2, 8, 18, 32]
~~~~~~~

여기서는 하나의 자바스크립트 타입을 다른 타입으로 변환하는 일은 하지 않을 겁니다. 대신에, 리스트의 각 아이템을 렌더링하는 JSX fragment으로 반환합니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
function App() {
  return (
    <div>
      ...

      <hr />

# leanpub-start-insert
      {list.map(function(item) {
        return <div>{item.title}</div>;
      })}
# leanpub-end-insert
    </div>
  );
}
~~~~~~~

리액트에서 처음으로 "아하"를 외쳤던 순간이 바로 여기에 있습니다. 별도의 HTML 템플릿 구문 없이, 자바스크립트만을 사용하여 자바스크립트 객체 목록을 HTML 요소에 매핑을 할 수가 있습니다. 그저 HTML 안의 자바스크립트일 뿐입니다.

이제 리액트는 각 아이템을 표시할 수 있습니다. 여기서 조금 더 정교하게 처리할 수 있도록 코드를 개선해봅시다. 각 아이템 요소에 키 속성을 할당함으로써, 리스트가 변경되었을 경우(예: 재정렬)에도 수정된 아이템을 식별할 수 있게 됩니다. 다행히도 현재 리스트의 아이템들에는 `objectID`라는 식별자가 존재합니다. 

{title="src/App.js",lang="javascript"}
~~~~~~~
function App() {
  return (
    <div>
      ...

      <hr />

      {list.map(function(item) {
# leanpub-start-insert
        return (
          <div key={item.objectID}>
# leanpub-end-insert
            {item.title}
# leanpub-start-insert
          </div>
        );
# leanpub-end-insert
      })}
    </div>
  );
}
~~~~~~~

안정적인 식별자를 키 속성으로 사용해야 하므로 아이템에 배열 인덱스를 사용하지 않습니다. 예를 들어 리스트에서 아이템들의 순서를 바꿀 경우, 각 아이템을 식별하기가 어려워집니다.

{title="Code Playground",lang="javascript"}
~~~~~~~
// don't do this
{list.map(function(item, index) {
  return (
    <div key={index}>
      ...
    </div>
  );
})}
~~~~~~~

지금까지는 각 아이템의 제목만 표시했습니다. 이제 아이템의 다른 속성들도 표시해봅시다.

{title="src/App.js",lang="javascript"}
~~~~~~~
function App() {
  return (
    <div>
      ...

      <hr />

# leanpub-start-insert
      {list.map(function(item) {
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
      })}
# leanpub-end-insert
    </div>
  );
}
~~~~~~~

JSX에서는 map 함수를 인라인 형태로 간결하게 사용할 수 있습니다. map 함수를 통해 각 아이템과 아이템이 가진 값에 접근할 수 있습니다. 각 아이템이 갖는 `url` 값에 따라 동적으로 앵커 태그의 `href` 속성을 생성할 수 있습니다. JSX의 자바스크립트를 사용하여 아이템을 표시할 뿐만 아니라, HTML 속성을 동적으로 할당할 수도 있습니다.

### 읽어보기

* [지난 장에서 사용한 코드](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/Lists-in-React)를 확인하세요.
  * [지난 장에서 수정된 코드](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/React-JSX...hs/Lists-in-React?expand=1)를 확인하세요.
* 왜 리액트에서 키 속성을 필요로 하는지 확인하세요([0](https://dev.to/jtonzing/the-significance-of-react-keys---a-visual-explanation--56l7), [1](https://www.robinwieruch.de/react-list-key), [2](https://reactjs.org/docs/lists-and-keys.html)). 아직 구현에 대해 이해하지 못하더라도 걱정하지 말고, 동적 리스트를 생성할 때 어떤 문제가 발생하는지에만 집중하세요.
* [자바스크립트 배열 메서드](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/)를 복습해보세요. 특히 map, filter, reduce를 중점으로 보면 좋습니다. 이들은 네이티브 자바스크립트에서도 사용할 수 있습니다.
* JSX 대신에 `null`을 반환하면 어떤 일이 일어날까요?
* 몇 가지 아이템을 더 추가하여 예제 리스트를 보다 현실적으로 만들어보세요.
* 예제에서 사용한 방법 외에도 다른 방식으로 JSX에서 자바스크립트를 사용해보세요.

