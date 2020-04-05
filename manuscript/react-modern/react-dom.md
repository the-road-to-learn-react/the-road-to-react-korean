## 리액트 DOM

앞서 컴포넌트 정의 및 인스턴스화에 대해 배웠으므로 App 컴포넌트에도 적용해봅시다. App 컴포넌트는 리액트 세계로의 진입점인 *src/index.js*에서 사용됩니다.

{title="src/index.js",lang="javascript"}
~~~~~~~
import React from 'react';
import ReactDOM from 'react-dom';

import App from './App';

ReactDOM.render(
  <App />,
  document.getElementById('root')
);
~~~~~~~

리액트에 이어 반드시 포함해야 하는 라이브러리는 `react-dom`입니다. 이 라이브러리는  `ReactDOM.render()` 메서드를 통해 HTML의 DOM 노드를 JSX로 바꿔줍니다. 이 과정을 통해 리액트를 HTML로 통합할 수 있게 됩니다. `ReactDOM.render()`에는 두 개의 인자가 필요합니다. 첫 번째 인자는 화면에 표시할 JSX 입니다. App 컴포넌트가 아닌 간단한 JSX여도 됩니다. 반드시 컴포넌트의 인스턴스를 주어야 하는 것은 아닙니다.

{title="Code Playground",lang="javascript"}
~~~~~~~
ReactDOM.render(
  <h1>Hello React World</h1>,
  document.getElementById('root')
);
~~~~~~~

두 번째 인자는 리액트 애플리케이션이 들어갈 HTML상의 위치입니다. 예제에서는 `id`가 `root`인 엘레먼트에 넣으려 하는데, *public/index.html* 파일에 해당 엘레먼트가 있습니다.

### 읽어보기

* *public/index.html*을 열어 리액트 애플리케이션이 삽입될 HTML상의 위치를 찾아보세요.
* HTML을 사용하는 외부 애플리케이션에 어떻게 리액트 애플리케이션을 삽입할 수 있을지 생각해보세요.
* [리액트의 엘레먼트 렌더링](https://reactjs.org/docs/rendering-elements.html)에 대해 더 읽어보세요.