## 리액트 컴포넌트 기초

우리의 첫 리액트 컴포넌트는 *src/App.js* 파일입니다. 대부분은 아래 코드와 비슷하게 생겼을 겁니다. 아래의 코드가 여러분의 코드와 조금씩 다를 수 있음을 주의하세요. create-react-app 키트가 조금씩 컴포넌트의 구조를 바꿀 수도 있기 때문입니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
import React from 'react';
import logo from './logo.svg';
import './App.css';

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>
          Edit <code>src/App.js</code> and save to reload.
        </p>
        <a
          className="App-link"
          Href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer"
        >
          Learn React
        </a>
      </header>
    </div>
  );
}

export default App;
~~~~~~~

이 파일은 달리 명시되지 않는 한, 우리 프로젝트에서 기본적인 컴포넌트로 사용합니다. 이제 컴포넌트에서 요소들을 조금씩 제거하면서 더 가벼운 버전의 create-react-app을 만들어봅시다.

{title="src/App.js",lang="javascript"}
~~~~~~~
# leanpub-start-insert
import React from 'react';

function App() {
  return (
    <div>
      <h1>Hello World</h1>
    </div>
  );
}

export default App;
# leanpub-end-insert
~~~~~~~

이 리액트 컴포넌트는 App 컴포넌트라는 자바스크립트 함수입니다. 일반적으로 **함수 컴포넌트**라고 불리며, 이외의 다른 종류의 컴포넌트는 뒤에서 다시 다룰 예정입니다(나중에 **컴포넌트 종류**를 참조하세요). 또한, App 컴포넌트는 별도의 매개변수를 받지 않습니다(나중에 **props**를 참조하세요). 마지막으로 App 컴포넌트는 JSX라고 하는 HTML과 유사한 코드를 반환합니다(나중에 **JSX**를 참조하세요).

함수 컴포넌트에도 자바스크립트 함수처럼 구현 세부 사항이 있습니다. 이제 실제로 개발을 하면서 하나씩 살펴봅시다.

{title="src/App.js",lang="javascript"}
~~~~~~~
import React from 'react';

function App() {
# leanpub-start-insert
  // 이 사이에 변수를 만들어봅시다.
# leanpub-end-insert

  return (
    <div>
      <h1>Hello World</h1>
    </div>
  );
}

export default App;
~~~~~~~

함수 본문(body)에서 정의된 변수는 함수가 실행될 때마다 매번 재정의될 것입니다. 자바스크립트 함수처럼요.

{title="src/App.js",lang="javascript"}
~~~~~~~
import React from 'react';

function App() {
# leanpub-start-insert
  const title = 'React';
# leanpub-end-insert

  return (
    <div>
      <h1>Hello World</h1>
    </div>
  );
}

export default App;
~~~~~~~

현재 App 컴포넌트 안에는 이 변수에 사용되는 요소(예: 함수 시그니처에서 나오는 매개변수)가 없기 때문에, 우리는 App 컴포넌트 밖에서 변수를 정의할 수 있습니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
import React from 'react';

# leanpub-start-insert
const title = 'React';
# leanpub-end-insert

function App() {
  return (
    <div>
      <h1>Hello World</h1>
    </div>
  );
}

export default App;
~~~~~~~

이제 변수를 사용하는 방법을 살펴봅시다.

### 읽어보기

* [지난 장에서 사용한 코드](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/Meet-the-React-Component)를 확인하세요.
* 자바스크립트(혹은 리액트)의 `const`, `let` 또는 `var` 를 사용하여 변수를 정의하는 게 익숙하지 않다면,  [이들의 차이점](https://www.robinwieruch.de/const-let-var)에 대해 읽어보세요.
  * [const](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const)
  * [let](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let)
* App 컴포넌트가 HTML로 반환되었을 때, `title` 변수를 표시할 방법을 생각해보세요. 다음 장에서 이 변수를 사용합니다.