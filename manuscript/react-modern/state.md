## 리액트 상태

컴포넌트 트리에 정보를 전달할 때 리액트 props를 사용합니다. **리액트 상태**는 애플리케이션을 대화형으로 만들 때 사용합니다. 상태와 상호작용을 하면서 애플리케이션의 모습을 바꿀 수 있습니다.

먼저 상태 관리를 위한 `리액트`의 `useState`라는 유틸리티 함수가 있습니다. `useState` 함수를 훅(hook)이라고 합니다. 리액트에는 상태 관리와 관련된 하나 이상의 **리액트 훅**이 있으며 또 다른 것도 있습니다. 다음 장에서 배우게 됩니다. 지금은 **리액트의 `useState` 훅**을 살펴보겠습니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  const stories = [ ... ];

# leanpub-start-insert
  const [searchTerm, setSearchTerm] = React.useState('');
# leanpub-end-insert

  ...
};
~~~~~~~

리액트의 `useState` 훅은 인수로 *초기 상태*를 사용합니다. 인수에 빈 문자열을 사용하고 함수는 두 개의 값이 있는 배열을 반환합니다. 첫 번째 값(`searchTerm`)은 *현재 상태*를 나타냅니다. 두 번째 값은 *이 상태를 업데이트하는 함수*(`setSearchTerm`)입니다. 이 함수를 *상태 업데이트 함수*라고 부르기도 합니다.

반환된 배열에서 두 값을 나타내는 구문에 익숙하지 않다면 [자바스크립트 배열 구조 분해](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment#Array_destructuring)를 읽어보세요. 배열을 더 간결하게 읽을 수 있습니다. 배열 구조 분해는 간단하게 시각화되는 장점이 있습니다.

{title="Code Playground",lang="javascript"}
~~~~~~~
// 기본 배열 정의
const list = ['a', 'b'];

// 배열 구조 분해가 아닌 방식
const itemOne = list[0];
const itemTwo = list[1];

// 배열 구조 분해
const [firstItem, secondItem] = list;
~~~~~~~

리액트의 경우, 리액트 `useState` 훅은 배열을 반환하는 함수입니다. 다음의 자바스크립트 예시를 비교해봅시다.

{title="Code Playground",lang="javascript"}
~~~~~~~
function getAlphabet() {
  return ['a', 'b'];
}

// 배열 구조 분해가 아닌 방식
const itemOne = getAlphabet()[0];
const itemTwo = getAlphabet()[1];

// 배열 구조 분해
const [firstItem, secondItem] = getAlphabet();
~~~~~~~

배열 구조 분해는 각 항목에 하나씩 차례로 접근하는 축약 버전의 방식입니다. 리액트에서 배열 구조 분해를 하지 않고 표현한다면 가독성이 떨어지게 됩니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  const stories = [ ... ];

  // 배열 구조 분해를 하지 않아 가독성이 떨어지는 방식
  const searchTermState = React.useState('');
  const searchTerm = searchTermState[0];
  const setSearchTerm = searchTermState[1];

  ...
};
~~~~~~~

리액트는 간결한 구문과 구조 분해된 변수에 이름을 붙일 수 있는 것 때문에 배열 구조 분해를 사용합니다. 다음은 배열 구조 분해의 예시 코드입니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  const stories = [ ... ];

# leanpub-start-insert
  const [searchTerm, setSearchTerm] = React.useState('');
# leanpub-end-insert

  ...
};
~~~~~~~

상태를 초기화하고 현재 상태와 상태 업데이트 함수에 접근한 후, 이를 이용하여 현재 상태를 표시하고 App 컴포넌트의 이벤트 핸들러 안에서 상태를 업데이트하세요.

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  const stories = [ ... ];

  const [searchTerm, setSearchTerm] = React.useState('');

  const handleChange = event => {
# leanpub-start-insert
    setSearchTerm(event.target.value);
# leanpub-end-insert
  };

  return (
    <div>
      <h1>My Hacker Stories</h1>

      <label htmlFor="search">Search: </label>
      <input id="search" type="text" onChange={handleChange} />

# leanpub-start-insert
      <p>
        Searching for <strong>{searchTerm}</strong>.
      </p>
# leanpub-end-insert

      <hr />

      <List list={stories} />
    </div>
  );
};
~~~~~~~

사용자가 입력 필드에 입력하면 입력 필드의 이벤트 핸들러가 change 이벤트로 현재 내부 값을 캡처합니다. 핸들러의 로직은 상태 업데이트 함수를 사용하여 새 상태를 설정합니다. 컴포넌트에 새 상태가 설정되면 컴포넌트는 다시 렌더링 되어 컴포넌트 함수가 다시 실행됩니다. 새 상태는 현재 상태가 되고 컴포넌트의 JSX에 표시할 수 있습니다.

### 실습하기

* [마지막 장의 소스 코드](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/React-State)를 확인하세요.
  * [마지막 장의 변경 사항](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/React-Props...hs/React-State?expand=1)을 확인하세요.
* [자바스크립트 배열 구조 분해](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment#Array_destructuring)에 대해 자세히 알아보세요.
* 대화형 리액트 컴포넌트를 만드는 리액트의 useState 훅([0](https://www.robinwieruch.de/react-usestate-hook), [1](https://reactjs.org/docs/hooks-state.html))에 대해 자세히 알아보세요.