## JSX의 핸들러 함수

App 컴포넌트에는 사용하지 않은 입력 필드와 라벨이 그대로 있습니다. JSX 외부의 HTML에서 입력 필드에는 [onchange 핸들러](https://developer.mozilla.org/en-US/docs/Web/API/GlobalEventHandlers/onchange)가 있습니다. 리액트 컴포넌트의 JSX와 함께 onchange 핸들러 사용 방법을 알아보겠습니다. 먼저 App 컴포넌트 본문을 간결하게 만들고 세부 구현 사항을 추가합니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
# leanpub-start-insert
const App = () => {
  // 여기에 코드를 작성하세요.

  return (
# leanpub-end-insert
    <div>
      <h1>My Hacker Stories</h1>

      <label htmlFor="search">Search: </label>
      <input id="search" type="text" />

      <hr />

      <List />
    </div>
# leanpub-start-insert
  );
};
# leanpub-end-insert
~~~~~~~

그다음 입력 필드의 change 이벤트에 대한 함수를 정의하세요. 일반 함수나 화살표 함수를 사용할 수 있습니다. 리액트에서 이 함수를 **(이벤트) 핸들러**라고 합니다. 이제 함수는 입력 필드의 `onChange` 속성(지정된 JSX 속성)으로 전달됩니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
# leanpub-start-insert
  const handleChange = event => {
    console.log(event);
  };
# leanpub-end-insert

  return (
    <div>
      <h1>My Hacker Stories</h1>

      <label htmlFor="search">Search: </label>
# leanpub-start-insert
      <input id="search" type="text" onChange={handleChange} />
# leanpub-end-insert

      <hr />

      <List />
    </div>
  );
};
~~~~~~~

웹 브라우저에서 애플리케이션을 실행합니다. 브라우저의 개발자 도구를 열고 입력 필드에 입력하여 로그가 발생하는지 확인하세요. 이를 자바스크립트 객체가 정의한 **합성 이벤트(synthetic event)**라고 합니다. 이 객체를 통해 입력 필드가 내보내는 값에 접근할 수 있습니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  const handleChange = event => {
# leanpub-start-insert
    console.log(event.target.value);
# leanpub-end-insert
  };

  return ( ... );
};
~~~~~~~

합성 이벤트는 기본적으로 [브라우저의 기본 이벤트](https://developer.mozilla.org/en-US/docs/Web/Events)를 감싸는 형태이며, 기본 브라우저 동작(예: 사용자가 폼 전송 버튼을 클릭한 후의 페이지 새로고침)을 막는 유용한 기능이 더 많이 있습니다. 어떤 때는 이벤트를 사용하기도 하고 어떤 때는 필요하지 않을 때도 있습니다.

다음은 사용자 상호작용에 응답하기 위해 JSX 핸들러 함수에 HTML 요소를 전달하는 방법입니다. 반환 값이 함수일 때를 제외하고는 항상 이런 핸들러에 함수의 반환 값이 아니라 함수를 전달하세요.

{title="Code Playground",lang="javascript"}
~~~~~~~
// 이렇게 하지 마세요.
<input
  id="search"
  type="text"
# leanpub-start-insert
  onChange={handleChange()}
# leanpub-end-insert
/>

// 대신 이렇게 하세요.
<input
  id="search"
  type="text"
# leanpub-start-insert
  onChange={handleChange}
# leanpub-end-insert
/>
~~~~~~~

HTML과 자바스크립트는 JSX에서 잘 동작합니다. HTML의 자바스크립트는 객체를 표시하고 HTML 속성에 자바스크립트 원시 타입을 전달할 수 있습니다((예: `<a>`에 `href`). 그리고 이벤트 처리를 위해 요소의 속성에 함수를 전달할 수 있습니다.

이벤트 핸들러로서 간결한 화살표 함수 사용을 선호하지만, 더 큰 리액트 컴포넌트에서는 컴포넌트 본문 안에 있는 다른 변수 선언과 비교하여 더 명확하게 보이기 때문에 함수 선언문을 사용하기도 합니다.

### 실습하기

* [마지막 장의 소스 코드](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/Handler-Function-in-JSX)를 확인하세요.
  * [마지막 장의 변경 사항](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/React-Component-Definition...hs/Handler-Function-in-JSX?expand=1)를 확인하세요.
* [리액트의 이벤트](https://reactjs.org/docs/events.html)에 대해 자세히 알아보세요.