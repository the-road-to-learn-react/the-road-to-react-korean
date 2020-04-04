## 리액트 JSX

앞서 App 컴포넌트가 반환하는 결괏값이 HTML과 유사하다고 했습니다. 이런 형태의 결괏값을 JSX라고 하며, HTML와 자바스크립트가 결합된 문법입니다. 이제 변수가 어떻게 표시되는지 살펴봅시다.

{title="src/App.js",lang="javascript"}
~~~~~~~
import React from 'react';

const title = 'React';

function App() {
  return (
    <div>
# leanpub-start-insert
      <h1>Hello {title}</h1>
# leanpub-end-insert
    </div>
  );
}

export default App;
~~~~~~~

`npm start`  명령어를 실행해 애플리케이션을 시작합니다. 브라우저를 열고 렌더링된 변수가 "Hello React"로 표시되었는지 확인합니다.

이제 JSX에서 거의 동일하게 표현되는 HTML에 초점을 맞춰 보겠습니다. 라벨이 있는 입력 필드는 다음과 같이 정의할 수 있습니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
import React from 'react';

const title = 'React';

function App() {
  return (
    <div>
      <h1>Hello {title}</h1>

# leanpub-start-insert
      <label htmlFor="search">Search: </label>
      <input id="search" type="text" />
# leanpub-end-insert
    </div>
  );
}

export default App;
~~~~~~~

`htmlFor`, `id`, 그리고 `type` 와 같이 3가지 HTML 속성을 정의했습니다. `id`와 `type`은 기존 HTML에서 익숙하게 봐온 반면, `htmlFor`는 생소할 겁니다. `htmlFor`는 HTML의 `for` 속성을 나타냅니다. 이렇게 JSX로 몇몇 HTML 속성을 나타낼 수 있습니다. 전체 목록은 리액트 공식 문서 중 [지원하는 HTML 속성](https://reactjs.org/docs/dom-elements.html#all-supported-html-attributes) 장에서 확인할 수 있으며, 이러한 HTML 속성은 카멜 케이스(camelCase) 표기법을 따릅니다.  `class` 대신에 `className` , `onclick` 대신에 `onClick`을 사용하는 것과 같이 더 많은 JSX 속성을 확인해보세요.

HTML 입력 필드 구현에 대한 내용은 뒤에서 다시 다룹니다. 지금은 JSX의 자바스크립트로 돌아가겠습니다. 앞서 우리는 문자열을 App 컴포넌트에 표시하기 위해 string 타입의 변수를 정의했습니다. 이 작업은 자바스크립트 개체에도 동일하게 적용될 수 있습니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
import React from 'react';

# leanpub-start-insert
const welcome = {
  greeting: 'Hey',
  title: 'React',
};
# leanpub-end-insert

function App() {
  return (
    <div>
      <h1>
# leanpub-start-insert
        {welcome.greeting} {welcome.title}
# leanpub-end-insert
      </h1>

      <label htmlFor="search">Search: </label>
      <input id="search" type="text" />
    </div>
  );
}

export default App;
~~~~~~~

JSX에서 중괄호(`{}`) 안에 들어있는 건 모두 자바스크립트 문법임을 기억해두세요(예: 함수 표현)

{title="src/App.js",lang="javascript"}
~~~~~~~
import React from 'react';

# leanpub-start-insert
function getTitle(title) {
  return title;
}
# leanpub-end-insert

function App() {
  return (
    <div>
# leanpub-start-insert
      <h1>Hello {getTitle('React')}</h1>
# leanpub-end-insert

      <label htmlFor="search">Search: </label>
      <input id="search" type="text" />
    </div>
  );
}

export default App;
~~~~~~~

JSX는 리액트에서 처음으로 만들어졌지만, 이제는 여러 최신 라이브러리와 프레임워크에서도 많이 사용하게 되었습니다. 이것이 리액트의 가장 큰 장점이기도 합니다. (중괄호를 제외한) 추가적인 템플릿 문법 없이 HTML에서 자바스크립트를 사용할 수 있기 때문이죠.

### 읽어보기

* [지난 장에서 사용한 코드](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/React-JSX)를 확인하세요.
  * [지난 장에서 수정된 코드](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/Meet-the-React-Component...hs/React-JSX?expand=1)도 확인하세요.
* [리액트 공식 문서 JSX](https://reactjs.org/docs/introducing-jsx.html)를 읽어보세요.
* 여러 가지 변수와 복잡한 데이터 타입을 정의해보고 JSX로 렌더링해보세요.
* 자바스크립트 배열을 JSX로 렌더링해보세요. 너무 복잡한 것 같아도 걱정하지 마세요. 다음 장에서 배울 겁니다.