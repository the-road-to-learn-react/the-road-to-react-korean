# 리액트 기초 다지기

첫 장에서는 리액트의 기본적인 내용에 대해 배우고, 첫 번째 리액트 프로젝트를 만듭니다. 그런 다음 실제 웹 애플리케이션과 같은 기능을 구현함으로써 리액트의 새로운 측면을 살펴보겠습니다. 이 과정이 끝날 무렵이면 우리는 클라이언트 및 서버사이드 검색, 원격 데이터 가져오기 및 고급 상태 관리와 같은 기능을 갖춘 리액트 애플리케이션을 갖게 될 것입니다.

## 리액트 시작하기

최근 몇 년 사이에 단일 페이지 애플리케이션([SPA, Single Page Application](https://en.wikipedia.org/wiki/Single-page_application))이 주목을 받고 있습니다. Angular, Ember, Knockout, Backbone과 같은 프레임워크를 사용함으로써 자바스크립트(Vanilla JavaScript, 타 라이브러리나 프레임워크 사용 없이 순수한 자바스크립트로 개발하는 것을 말함)와 제이쿼리(jQuery)를 사용하지 않고도 최신 웹 애플리케이션을 구축할 수 있게 되었습니다. SPA 프레임워크 중 하나인 리액트는 페이스북이 만든 라이브러리로, 2013년에 공개되었습니다. 이들은 모두 자바스크립트로 웹 애플리케이션을 만드는 데에 사용됩니다.

잠시 SPA가 존재하기 이전의 시간으로 돌아가 봅시다. 과거에는 웹 사이트와 웹 애플리케이션이 서버에서 렌더링 되었습니다. 사용자는 브라우저에서 URL에 접속하여 웹 서버에서 하나의 HTML 파일과 모든 관련 HTML, CSS 및 자바스크립트 파일을 요청합니다. 약간의 네트워크 지연을 겪고 나면, 사용자는 브라우저(클라이언트)에서 렌더링 된 HTML을 보고 상호작용을 시작합니다. 추가적인 페이지 전환(다른 URL을 방문하는 것)은 이 과정을 다시 불러일으킵니다. 과거에는 본질적으로 중요한 모든 작업이 서버에서 수행되었던 반면, 클라이언트는 단지 한 페이지씩 렌더링을 함으로써 최소한의 역할만 수행했습니다. HTML과 CSS가 애플리케이션의 구조를 만들고, 약간의 자바스크립트가 상호작용(예: 토글, 드롭다운) 또는 고급 스타일링(예: 툴팁 배치)을 가능하게 했습니다. 이런 종류의 작업에 널리 사용되는 자바스크립트 라이브러리는 jQuery 였습니다.

이와는 반대로, 최신 버전의 자바스크립트는 초점을 서버에서 클라이언트로 옮겼습니다. 극단적으로 이야기하자면, 사용자는 URL을 방문해서 최소한의 HTML 파일과 하나의 자바스크립트 파일만 요청합니다. 약간의 네트워크 지연을 겪고 나면, 사용자는 브라우저에서 자바스크립트에 의해 렌더링 된 HTML을 보고 상호작용을 시작합니다. 추가적인 페이지 전환을 할 때마다 웹 서버에 더 많은 파일을 요청하지는 않지만, 처음에 요청했던 자바스크립트를 사용하여 새로운 페이지를 렌더링할 수 있습니다. 또한, 사용자에 의한 모든 추가적인 작업도 클라이언트에서 처리됩니다. 이러한 최신 버전에서는 서버가 주로 최소한의 HTML 파일에 연결된 자바스크립트만을 제공합니다. HTML 파일은 연결된 모든 자바스크립트를 클라이언트 측에서 실행하여 애플리케이션에서 이루어질 상호작용을 위한 HTML 및 자바스크립트를 렌더링합니다.

여러 SPA 프레임워크 중에서도 리액트는 이를 가능하게 합니다. 기본적으로 SPA는 전체 애플리케이션을 만들기 위해 폴더와 파일로 깔끔하게 정리된 하나의 자바스크립트이며,  SPA 프레임워크는 이를 설계하기 위한 모든 도구를 제공합니다. 이러한 자바스크립트 중심의 애플리케이션은 사용자가 웹 애플리케이션의 URL을 방문하면 네트워크를 통해 브라우저로 한 번만 전달됩니다. 여기서부터 리액트 또는 다른 SPA 프레임워크가 브라우저의 모든 것을 렌더링하고 사용자의 작업을 처리합니다.

리액트의 등장으로 컴포넌트의 개념이 대중화되기 시작했습니다. 모든 컴포넌트는 HTML, CSS, 자바스크립트와 유사하게 정의됩니다. 컴포넌트가 한 번 정의되면, 계층구조로 사용하여 전체 애플리케이션을 구성할 수 있습니다. 리액트는 라이브러리로서 컴포넌트에 중점을 두고 있지만, 주변 생태계에서 이를 좀 더 유연한 프레임워크로 만들고 있습니다. 리액트는 간결한 API, 놀라운 생태계, 훌륭한 커뮤니티를 갖추고 있습니다. 리액트의 세계로 온 걸 환영합니다!

### 읽어보기

* [왜 나는 앵귤러에서 리액트로 옮겼는가](https://www.robinwieruch.de/reasons-why-i-moved-from-angular-to-react/)
* [프레임워크 학습 방법](https://www.robinwieruch.de/how-to-learn-framework/)
* [리액트를 배우는 방법](https://www.robinwieruch.de/learn-react-js)
* [프레임워크가 중요한 이유](https://www.robinwieruch.de/why-frameworks-matter).
* [리액트에 필요한 자바스크립트 기초](https://www.robinwieruch.de/javascript-fundamentals-react-requirements) - 리액트에 대해 너무 걱정하지 말고, 리액트에 사용되는 여러 자바스크립트 기능을 스스로 학습해보세요.

## 준비사항

이 책을 따라가려면 웹 개발의 기본, 즉 HTML, CSS, 자바스크립트를 사용하는 방법을 숙지해야 합니다. 또한 [APIs](https://www.robinwieruch.de/what-is-an-api-javascript/)를 이해한다면 도움이 될 것입니다.

###  코드 에디터와 터미널

웹 개발 환경을 갖춰 봅시다. 텍스트 에디터(예: Sublime Text)나 커맨드 라인(Command line, 터미널(terminal)이라고도 함)(예: iTerm), 또는 IDE(Integrated Development Environment, 통합 개발 환경)(예: Visual Studio Code)가 필요합니다. 자세한 방법은 [개발 환경 설정 가이드](https://www.robinwieruch.de/developer-setup/)를 참고하길 바랍니다. 초보자에게는 Visual Studio Code(VS Code)를 추천합니다. VS Code는 커맨드 라인을 갖춘 고급 편집기를 제공하며, 웹 개발자들 사이에서도 널리 사용됩니다.

이번 실습에서는 *커맨드 라인(command line)*을 사용할 것입니다. *커맨드 라인 도구(command line tool)*, *터미널(terminal)*, *통합 터미널(integrated terminal)*과 같은 용어로도 불립니다. *에디터*, *텍스트 에디터*, *IDE(Integrated Development Environment, 통합 개발 환경)*와도 동일하며, 어떤 도구를 선택해도 비슷합니다.

추가적으로, 이 책의 예제를 실습하면서 프로젝트를 GitHub으로 관리하는 것을 추천합니다. 어떻게 사용하는지는 [짧은 가이드](https://www.robinwieruch.de/git-essential-commands/)를 참고하세요. GitHub은 뛰어난 버전 관리 기능을 제공하여 어떤 변화가 일어났는지를 추적할 수 있습니다. 또한 나중에 다른 사람들과 코드를 공유하기에도 좋습니다.

로컬 환경에서 코드 에디터/터미널 또는 IDE를 설정하고 싶지 않다면 온라인 코드 에디터인 [CodeSandbox](https://codesandbox.io/)를 사용할 수 있습니다. CodeSandbox는 온라인으로 코드를 공유하는 데에 유용한 도구이지만, 로컬 환경에 설정하는 것이 웹 애플리케이션을 만드는 다양한 방법을 배우기에는 더 좋습니다. 또한 전문적으로 애플리케이션을 개발하려면 로컬 설정이 필요합니다.

### Node와 NPM

시작하기 전에, [node(노드)와 npm](https://nodejs.org/en/)을 설치해야 합니다. 둘 다 앞으로 필요한 라이브러리(노드 패키지)를 관리하는 데 사용됩니다. 이러한 노드 패키지는 라이브러리가 될 수도 있고, 전체 프레임워크일 수도 있습니다. 여기서는 npm(node package manager, 노드 패키지 관리자 명령어)을 통해 외부 노드 패키지를 설치합니다.

`node --version`을 사용하여 현재 노드 및 npm 버전을 확인할 수 있습니다. 화면에 버전이 표시되지 않으면 노드 및 npm을 설치해야 합니다.

{title="Command Line",lang="text"}
~~~~~~~
node --version
*vXX.YY.ZZ
npm --version
*vXX.YY.ZZ
~~~~~~~

노드와 npm을 이미 설치한 경우, 최신 버전인지 확인하세요. npm을 처음 사용하거나 다시 설치할 경우, [npm crash course](https://www.robinwieruch.de/npm-crash-course)를 통해 속도를 높일 수 있습니다.

## 리액트 프로젝트 설정하기

이 책에서는 [create-react-app](https://github.com/facebook/create-react-app)를 사용하여 애플리케이션을 부트스트래핑합니다. 부트스트래핑(bootstrapping)이라는 뜻은 애플리케이션을 최초 생성하여 브라우저에서 실행하는 과정을 말합니다.  *create-react-app*은 2016년 페이스북이 제안한 리액트 제로 구성 설치 스타터 킷(Zero-Configuration Setup Starter Kit)입니다. 트위터에서 진행한 한 [조사](https://twitter.com/dan_abramov/status/806985854099062785)에 따르면 96% 이상의 리액트 개발자들이 입문자의 경우 create-react-app 사용을 권장하고 있습니다. create-react-app은 리액트 개발 도구와 환경 설정이 이미 세팅되어 있기 때문에, 우리는 오롯이 애플리케이션 구현에만 신경 쓰면 됩니다.

노드와 npm을 설치한 후 터미널을 사용하여 프로젝트 폴더에 다음 명령어를 입력하세요. 이 프로젝트를 *hacker stories*라고 하겠습니다. 물론 다른 이름을 사용해도 괜찮습니다.

{title="Command Line",lang="text"}
~~~~~~~
npx create-react-app hacker-stories
~~~~~~~

설치가 완료되면 생성된 폴더 안으로 들어갑니다.

{title="Command Line",lang="text"}
~~~~~~~
cd hacker-stories
~~~~~~~

코드 에디터에서 애플리케이션을 열어 봅시다. Visual Studio Code의 경우, 터미널에 `code .`를 입력하면 됩니다. 디렉터리에 아래와 같은 *create-react-app* 구조가 보일 것입니다.

{title="Project Structure",lang="text"}
~~~~~~~
hacker-stories/
--node_modules/
--public/
--src/
----App.css
----App.js
----App.test.js
----index.css
----index.js
----logo.svg
--.gitignore
--package-lock.json
--package.json
--README.md
~~~~~~~

각 파일과 폴더 단위가 무엇을 지칭하는지 알아보겠습니다.

* **README.md:** *.md* 확장자는 마크다운(markdown) 파일입니다. 일반 텍스트와 함께 간단한 마크업 언어로 작성합니다. 대부분 프로젝트에는 *README.md* 파일에 프로젝트 설명 및 설치 방법 등 안내 사항을 작성합니다. 깃허브 리퍼지토리 페이지의 첫 화면에 *README.md* 파일을 보았을 겁니다. *create-react-app* 을 설치한 후 바로 깃허브에 프로젝트를 올린다면 *README.md* 파일 내용은 [create-react-app 공식 깃허브 리퍼지토리](https://github.com/facebookincubator/create-react-app)와 내용이 동일할 것입니다.
* **node_modules/:** 이 폴더에는 npm으로 설치되었던 모든 노드 패키지를 포함합니다. 이미 create-react-app으로 리액트 애플리케이션을 부트스트래핑 했기 때문에 여러 모듈이 설치되어 있습니다. 이 폴더는 절대로 건드리지 말아야 합니다. `npm` 명령어를 사용해 패키지를 설치 또는 제거합니다.
* **package.json:** 노드 패키지 의존성 및 기타 프로젝트 구성 목록을 포함합니다.
* **package-lock.json:** 프로젝트에 사용하는 모든 노드 패키지 버전을 표시합니다. 이 파일 또한 건드리지 않습니다.
* **.gitignore:** git을 사용할 때, 원격 git 리퍼지토리에 제외시킬 모든 파일과 폴더 목록이 나열되어 있습니다. 예를 들어 *node_module*은 로컬에만 있어야 합니다. 의존성 폴더 전체를 올리지 않고도 공유된 *package.json* 파일만으로 의존성 패키지를 설치할 수 있습니다.
* **public/:** *public/index.html* 와 같이 배포를 위해 필요한 파일을 말합니다. 앱이 개발 중이거나 다른 곳에서 호스팅 된 도메인에 있을 때, 인덱스 파일은 *localhost:3000*에 표시됩니다. 프로젝트를 빌드할 때, *src/* 폴더 내 모든 코드는 몇 개의 파일로 묶여 *public* 폴더에 배치됩니다. 기본적으로 *index.html*와 *src/*에 있는 모든 자바스크립트를 처리합니다.

우리가 필요한 모든 파일은 *src/* 폴더에 들어있습니다. 제일 중요한 파일은 *src/App.js* 파일로, 리액트 컴포넌트를 생성하는 역할을 합니다. 지금은 이 파일이 전체 애플리케이션을 이루고 있지만, 나중에 리액트 컴포넌트를 여러 파일로 분절하여 나눠 관리할 수 있습니다.

이외에 테스트를 위한 *src/App.test.js* 파일과 리액트의 진입점인 *src/index.js* 파일이 보일 겁니다. 다음 장에서 두 파일에 대해 알게 될 것입니다. 또한 애플리케이션과 컴포넌트 스타일을 지정하는 *src/index.css* 및 *src/App.css* 파일이 있습니다. 현재는 기본 스타일만 적용되어 있으며, 나중에 수정할 수 있습니다.

리액트 프로젝트의 폴더와 파일 구조에 대해 알게 되었으니, 명령어를 통해 프로젝트를 시작해봅시다. 모든 프로젝트별 명령은 *package.json*의 *scripts* 속성에서 찾을 수 있습니다. 아래와 비슷한 형태일 것입니다.

{title="package.json",lang="javascript"}
~~~~~~~
{
  ...
  },
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
  },
  ...
}
~~~~~~~

이러한 스크립트는 IDE의 내장 터미널이나  `npm run <script>` 명령어를 통해 실행됩니다. `start` 나 `test` 스크립트에서 `run`은 생략할 수 있습니다. 아래와 같이 명령어를 실행합니다.

{title="Command Line",lang="text"}
~~~~~~~
# http://localhost:3000 에서 애플리케이션 실행
npm start

# 테스트 실행
npm test

# 배포를 위한 애플리케이션 빌드
npm run build
~~~~~~~

이전 npm 스크립트 중에는 `eject`도 있었으나, 여기서는 다루지 않습니다. 한 번 eject를 수행하게 되면 이전 상태로 되돌아 갈 수 없기 때문입니다. 이 명령어는 create-react-app의 설정이 만족스럽지 않아 직접 설정을 바꾸고 싶을 때 사용합니다. 여기서 우리는 모든 기본 설정값을 유지합니다.

### 읽어보기

* [create-react-app 공식 문서](https://github.com/facebook/create-react-app) 또는 [시작 가이드](https://create-react-app.dev/docs/getting-started)
  * [create-ract-app에서 지원하는 JavaScript 기능](https://create-react-app.dev/docs/supported-browsers-features)
* [create-react-app의 폴더 구조](https://create-react-app.dev/docs/folder-structure)
	* 리액트 프로젝트의 폴더와 파일을 하나씩 살펴보세요.
* [create-react-app의 스크립트](https://create-react-app.dev/docs/available-scripts)
	* `npm start`을 실행해 브라우저에서 애플리케이션을 확인합니다.
		* `Control + C`를 눌러 터미널에서 명령어 실행을 중지시킵니다.
	* `npm test`를 실행합니다.
	* `npm run build` 스크립트를 실행해 *build/* 폴더에 어떤 파일이 추가되었는지 확인합니다(이 폴더는 나중에 직접 삭제할 수도 있습니다). 빌드된 폴더는 나중에 [앱을 배포할 때](https://www.robinwieruch.de/deploy-applications-digital-ocean/)에도 사용할 수 있습니다.
* 코드를 수정하면 브라우저에서 적용이 잘 되었는지 확인하도록 합니다.

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
  // do something in between
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

`npm start`  명령어를 실행해 애플리케이션을 시작합니다. 브라우저를 열고 렌더링된 변수가 “Hello React”로 표시되었는지 확인합니다.

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

`htmlFor`, `id`, 그리고 `type` 와 같이 3가지 HTML 속성을 정의했습니다. `id`와 `type`은 기존 HTML에서 익숙하게 봐온 반면, `htmlFor`는 생소할 겁니다. `htmlFor`는 HTML의 `for` 속성을 나타냅니다. 이렇게 JSX로 몇몇 HTML 속성을 나타낼 수 있습니다. 전체 목록은 리액트 공식 문서 중 [‘지원하는 HTML 속성’](https://reactjs.org/docs/dom-elements.html#all-supported-html-attributes) 장에서 확인할 수 있으며, 이러한 HTML 속성은 카멜 케이스(camelCase) 표기법을 따릅니다.  `class` 대신에 `className` , `onclick` 대신에 `onClick`을 사용하는 것과 같이 더 많은 JSX 속성을 확인해보세요.

HTML 입력 필드 구현에 대한 내용은 뒤에서 다시 다룹니다. 지금은 JSX의 JavaScript로 돌아가겠습니다. 앞서 우리는 문자열을 App 컴포넌트에 표시하기 위해 string 타입의 변수를 정의했습니다. 이 작업은 자바스크립트 개체에도 동일하게 적용될 수 있습니다.

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
* [리액트 공식 문서 JSX](https://reactjs.org/docs/introducing-jsx.html).
* 여러 가지 변수와 복잡한 데이터 타입을 정의해보고 JSX로 렌더링해보세요.
* 자바스크립트 배열을 JSX로 렌더링해보세요. 너무 복잡한 것 같아도 걱정하지 마세요. 다음 장에서 배울 겁니다.

## Lists in React

So far we've rendered a few primitive variables in JSX; next we'll render a list of items. We'll experiment with sample data at first, then we'll apply that to fetch data from a remote API. First, let's define the array as a variable. As before, we can define a variable outside or inside the component. The following defines it outside:

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

I used a `...` here as a placeholder, to keep my code snippet small (without App component implementation details) and focused on the essential parts (the `list` variable outside of the App component). I will use the `...` throughout the rest of this learning experience as placeholder for code blocks that I have established previous exercises. If you get lost, you can always verify your code using the CodeSandbox links I provide at the end of most sections.

Each item in the list has a title, a url, an author, an identifier (`objectID`), points -- which indicate the popularity of an item -- and a count of comments. Next, we'll render the list within our JSX dynamically:

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
      {/* render the list here */}
# leanpub-end-insert
    </div>
  );
}
~~~~~~~

You can use the [built-in JavaScript map method for arrays](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) to iterate over each item of the list and return a new version of each:

{title="Code Playground",lang="javascript"}
~~~~~~~
const numbers = [1, 4, 9, 16];

const newNumbers = numbers.map(function(number) {
  return number * 2;
});

console.log(newNumbers);
// [2, 8, 18, 32]
~~~~~~~

We won't map from one JavaScript data type to another in our case. Instead, we return a JSX fragment that renders each item of the list:

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

Actually, one of my first React "Aha" moments was using barebones JavaScript to map a list of JavaScript objects to HTML elements without any other HTML templating syntax. It's just JavaScript in HTML.

React will display each item now, but you can still improve your code so React handles advanced dynamic lists more gracefully. By assigning a key attribute to each list item's element, React can identify modified items if the list changes (e.g. re-ordering). Fortunately, our list items come with an identifier:

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

We avoid using the index of the item in the array to make sure the key attribute is a stable identifier. If the list changes its order, for example, React will not be able to identify the items properly:

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

So far, only the title is displayed for each item. Let's experiment with displaying more of the item's properties:

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

The map function is inlined concisely in your JSX. Within the map function, we have access to each item and its properties. The `url` property of each item is used as dynamic `href` attribute for the anchor tag. Not only can JavaScript in JSX be used to display items, but also to assign HTML attributes dynamically.

### Exercises:

* Confirm your [source code for the last section](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/Lists-in-React).
  * Confirm the [changes from the last section](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/React-JSX...hs/Lists-in-React?expand=1).
* Read more about why React's key attribute is needed ([0](https://dev.to/jtonzing/the-significance-of-react-keys---a-visual-explanation--56l7), [1](https://www.robinwieruch.de/react-list-key), [2](https://reactjs.org/docs/lists-and-keys.html)). Don't worry if you don't understand the implementation yet, just focus on what problem it causes for dynamic lists.
* Recap the [standard built-in array methods](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/) -- especially *map*, *filter*, and *reduce* -- which are available in native JavaScript.
* What happens if your return `null` instead of the JSX?
* Extend the list with some more items to make the example more realistic.
* Practice using different JavaScript expressions in JSX.

## Meet another React Component

So far we've only been using the App component to create our applications. We used the App component in the last section to express everything needed to render our list in JSX, and it should scale with your needs and eventually handle more complex tasks. To help with this, we'll split some of its responsibilities into a standalone List component:

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

Optional: If this component looks odd, because the outermost part of the returned JSX starts with JavaScript. We could use it with a wrapping HTML element as well, but we'll continue with the previous version.

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

Now the new List component can be used in the App component:

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

You've just created your first React component! With this example, we can see how components that encapsulate meaningful tasks can work for larger React applications.

Larger React applications have **component hierarchies** (also called **component trees**). There is usually one uppermost **entry point component** (e.g. App) that spans a tree of components below it. The App is the **parent component** of the List, so the List is a **child component** of the App. In a component tree, the App is the **root component**, and the components that don't render any other components are called **leaf components** (e.g. List). The App can have multiple children, as can the List. If the App has another child component, the additional child component is called a **sibling component** of the List.

### Exercises:

* Confirm your [source code for the last section](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/Meet-another-React-Component).
  * Confirm the [changes from the last section](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/Lists-in-React...hs/Meet-another-React-Component?expand=1).
* Draw your components -- the App component and List component -- as a component tree on a sheet of paper. Extend this component tree with other possible components (e.g. extracted Search component for the input field and label in the App component). Try to figure out which other parts can be extracted as standalone components.
* If a Search component is used in the App component, would the Search component be a sibling, parent, or child component for the List component?
* Ask yourself what problems could arise if we keep treating the `list` variable as global variable. We will cover how to handle these problems in the upcoming sections.

## React Component Instantiation

Next, I'll briefly explain JavaScript classes, to help clarify React components. Technically they are not related, but it is a fitting analogy for you to understand the concept of a component.

Classes are most often used in object-oriented programming languages. JavaScript, always flexible in its programming paradigms, allows functional programming and object-oriented programming to co-exist side-by-side. To recap JavaScript classes for object-oriented programming, consider the following *Developer* class:

{title="Code Playground",lang="javascript"}
~~~~~~~
class Developer {
  constructor(firstName, lastName) {
    this.firstName = firstName;
    this.lastName = lastName;
  }

  getName() {
    return this.firstName + ' ' + this.lastName;
  }
}
~~~~~~~

Each class has a constructor that takes arguments and assigns them to the class instance. A class can also define functions that are associated with a subject (e.g. `getName`), called **methods** or **class methods**.

Defining the Developer class once is just one part; instantiating it is the other. The class definition is the blueprint of its capabilities, and usage occurs when an instance is created with the `new` statement.

{title="Code Playground",lang="javascript"}
~~~~~~~
// class definition
class Developer { ... }

// class instantiation
const robin = new Developer('Robin', 'Wieruch');

console.log(robin.getName());
// "Robin Wieruch"

// another class instantiation
const dennis = new Developer('Dennis', 'Wieruch');

console.log(dennis.getName());
// "Dennis Wieruch"
~~~~~~~

If a JavaScript class definition exists, one can create *multiple* instances of it. It is similar to a React component, which has only *one* component definition, but can have *multiple* instances:

{title="src/App.js",lang="javascript"}
~~~~~~~
// definition of App component
function App() {
  return (
    <div>
      <h1>My Hacker Stories</h1>

      <label htmlFor="search">Search: </label>
      <input id="search" type="text" />

      <hr />

      {/* creating an instance of List component */}
      <List />
      {/* creating another instance of List component */}
      <List />
    </div>
  );
}

// definition of List component
function List() { ... }
~~~~~~~

Once we've defined a **component**, we can use it like an HTML **element** anywhere in our JSX. The element produces an **instance** of your component, or in other words, the component gets instantiated. It's not much different from a JavaScript class definition and usage.

### Exercises:

* Familiarize yourself with the terms *component declaration*, *instance*, and *element*.
* Experiment by creating multiple instances of a List component.
* Think about how it could be possible to give each List component its own `list`.

## React DOM

Now that we've learned about component definitions and their instantiation, we can move to the App component's instantiation. It has been in our application from the start, in the *src/index.js* file:

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

Next to React, there is another imported library called `react-dom`, in which a `ReactDOM.render()` function uses an HTML node to replace it with JSX. The process integrates React into HTML. `ReactDOM.render()` expects two arguments; the first is to render the JSX. It creates an instance of your App component, though it can also pass simple JSX without any component instantiation.

{title="Code Playground",lang="javascript"}
~~~~~~~
ReactDOM.render(
  <h1>Hello React World</h1>,
  document.getElementById('root')
);
~~~~~~~

The second argument specifies where the React application enters your HTML. It expects an element with an `id='root'`, found in the *public/index.html* file. This is a basic HTML file.

### Exercises:

* Open the *public/index.html* to see where the React application enters your HTML.
* Consider how we can include a React application in an external web application that uses HTML.
* Read more about [rendering elements in React](https://reactjs.org/docs/rendering-elements.html).

## React Component Definition (Advanced)

The following refactorings are optional recommendations to explain the different JavaScript/React patterns. You can build complete React applications without these advanced patterns, so don't be discouraged if they seem too complicated.

All components in the *src/App.js* file are function component. JavaScript has multiple ways to declare functions. So far, we have used the function statement, though arrow functions can be used more concisely:

{title="Code Playground",lang="javascript"}
~~~~~~~
// function declaration
function () { ... }

// arrow function declaration
const () => { ... }
~~~~~~~

You can remove the parentheses in an arrow function expression if it has only one argument, but multiple arguments require parentheses:

{title="Code Playground",lang="javascript"}
~~~~~~~
// allowed
const item => { ... }

// allowed
const (item) => { ... }

// not allowed
const item, index => { ... }

// allowed
const (item, index) => { ... }
~~~~~~~

Defining React function components with arrow functions makes them more concise:

{title="src/App.js",lang="javascript"}
~~~~~~~
# leanpub-start-insert
const App = () => {
# leanpub-end-insert
  return (
    <div>
      ...
    </div>
  );
# leanpub-start-insert
};
# leanpub-end-insert

# leanpub-start-insert
const List = () => {
# leanpub-end-insert
  return list.map(function(item) {
    return (
      <div key={item.objectID}>
        ...
      </div>
    );
  });
# leanpub-start-insert
};
# leanpub-end-insert
~~~~~~~

This holds also true for other functions, like the one we used in our JavaScript array's map method:

{title="src/App.js",lang="javascript"}
~~~~~~~
const List = () => {
# leanpub-start-insert
  return list.map(item => {
# leanpub-end-insert
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
};
~~~~~~~

If an arrow function doesn't do *anything* in between, but only returns *something*, -- in other words, if an arrow function doesn't perform any task, but only returns information --, you can remove the **block body** (curly braces) of the function. In a **concise body**, an **implicit return statement** is attached, so you can remove the return statement:

{title="Code Playground",lang="javascript"}
~~~~~~~
// with block body
count => {
  // perform any task in between

  return count + 1;
}

// with concise body
count =>
  count + 1;
~~~~~~~

This can be done for the App and List component as well, because they only return JSX and don't perform any task in between. Again it also applies for the arrow function that's used in the map function:

{title="src/App.js",lang="javascript"}
~~~~~~~
# leanpub-start-insert
const App = () => (
# leanpub-end-insert
  <div>
    ...
  </div>
# leanpub-start-insert
);
# leanpub-end-insert

# leanpub-start-insert
const List = () =>
  list.map(item => (
# leanpub-end-insert
    <div key={item.objectID}>
      <span>
        <a href={item.url}>{item.title}</a>
      </span>
      <span>{item.author}</span>
      <span>{item.num_comments}</span>
      <span>{item.points}</span>
    </div>
# leanpub-start-insert
  ));
# leanpub-end-insert
~~~~~~~

Our JSX is more concise now, as it omits the function statement, the curly braces, and the return statement. However, remember this is an optional step, and that it's acceptable to use normal functions instead of arrow functions and block bodies with curly braces for arrow functions over implicit returns. Sometimes block bodies will be necessary to introduce more business logic between function signature and return statement:

{title="Code Playground",lang="javascript"}
~~~~~~~
const App = () => {
  // perform any task in between

  return (
    <div>
      ...
    </div>
  );
};
~~~~~~~

Be sure to understand this refactoring concept, because we'll move quickly from arrow function components with and without block bodies as we go. Which one we use will depend on the requirements of the component.

### Exercises:

* Confirm your [source code for the last section](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/React-Component-Definition).
  * Confirm the [changes from the last section](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/Meet-another-React-Component...hs/React-Component-Definition?expand=1).
* Read more about [JavaScript arrow functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions).
* Familiarize yourself with arrow functions with block body and return, and concise body without return.

## Handler Function in JSX

The App component still has the input field and label, which we haven't used. In HTML outside of JSX, input fields have an [onchange handler](https://developer.mozilla.org/en-US/docs/Web/API/GlobalEventHandlers/onchange). We're going to discover how to use onchange handlers with a React component's JSX. First, refactor the App component form a concise to block body so we can add implementation details.

{title="src/App.js",lang="javascript"}
~~~~~~~
# leanpub-start-insert
const App = () => {
  // do something in between

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

Next, define a function -- which can be normal or arrow -- for the change event of the input field. In React, this function is called an **(event) handler**. Now the function can be passed to the `onChange` attribute (JSX named attribute) of the input field.

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

After opening your application in a web browser, open the browser's developer tools to see logging occur after you type into the input field. This is called a **synthetic event** defined by a JavaScript object. Through this object, we can access the emitted value of the input field:

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

The synthetic event is essentially a wrapper around the [browser's native event](https://developer.mozilla.org/en-US/docs/Web/Events), with more functions that are useful to prevent native browser behavior (e.g. refreshing a page after the user clicks a form's submit button). Sometimes you will use the event, sometimes you won't need it.

This is how we give HTML elements in JSX handler functions to respond to user interaction. Always pass functions to these handlers, not the return value of the function, except when the return value is a function:

{title="Code Playground",lang="javascript"}
~~~~~~~
// don't do this
<input
  id="search"
  type="text"
# leanpub-start-insert
  onChange={handleChange()}
# leanpub-end-insert
/>

// do this instead
<input
  id="search"
  type="text"
# leanpub-start-insert
  onChange={handleChange}
# leanpub-end-insert
/>
~~~~~~~

HTML and JavaScript work well together in JSX. JavaScript in HTML can display objects, can pass JavaScript primitives to HTML attributes (e.g. `href` to `<a>`), and can pass functions to an element's attributes for handling events.

I prefer using arrow functions because of their concision as event handlers, however, in a larger React component I see myself using the function statements too, because it gives them more visibility in contrast to other variable declarations within a component's body.

### Exercises:

* Confirm your [source code for the last section](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/Handler-Function-in-JSX).
  * Confirm the [changes from the last section](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/React-Component-Definition...hs/Handler-Function-in-JSX?expand=1).
* Read more about [React's events](https://reactjs.org/docs/events.html).

## React Props

We are currently using the `list` variable as a global variable in the current application. We used it directly from the global scope in the App component, and again in the List component. This could work if you only had one variable, but it doesn't scale with multiple variables across multiple components from many different files.

Using so called props, we can pass variables as information from one component to another component. Before using props, we'll move the list from the global scope into the App component and rename it to its actual domain:

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
# leanpub-start-insert
  const stories = [
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

  const handleChange = event => { ... };

  return ( ... );
};
~~~~~~~

Next, we'll use **React props** to pass the array to the List component:

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  const stories = [ ... ];

  const handleChange = event => { ... };

  return (
    <div>
      <h1>My Hacker Stories</h1>

      <label htmlFor="search">Search: </label>
      <input id="search" type="text" onChange={handleChange} />

      <hr />

# leanpub-start-insert
      <List list={stories} />
# leanpub-end-insert
    </div>
  );
};
~~~~~~~

The variable is called `stories` in the App component, and we pass it under this name to the List component. In the List component's instantiation, however, it is assigned to the `list` attribute. We access it as `list` from the `props` object in the List component's function signature:

{title="src/App.js",lang="javascript"}
~~~~~~~
# leanpub-start-insert
const List = props =>
  props.list.map(item => (
# leanpub-end-insert
    <div key={item.objectID}>
      <span>
        <a href={item.url}>{item.title}</a>
      </span>
      <span>{item.author}</span>
      <span>{item.num_comments}</span>
      <span>{item.points}</span>
    </div>
  ));
~~~~~~~

Using this operation, we've prevented the list/stories variable from polluting the global scope in the App component. Since `stories` is not used in the App component directly, but in one of its child components, we passed them as props to the List component. There, we can access it through the first function signature's argument, called `props`.

* Confirm your [source code for the last section](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/React-Props).
  * Confirm the [changes from the last section](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/Handler-Function-in-JSX...hs/React-Props?expand=1).
* Read more about [how to pass props to React components](https://www.robinwieruch.de/react-pass-props-to-component).

## React State

React Props are used to pass information down the component tree; **React state** is used to make applications interactive. We'll be able to change the application's appearance by interacting with it.

First, there is a utility function called `useState` that we take from `React` for managing state. The `useState` function is called a hook. There is more than one **React hook** -- related to state management but also other things in React -- and you will learn about them throughout the next sections. For now, let's focus on **React's `useState` hook**:

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

React's `useState` hook takes an *initial state* as an argument. We'll use an empty string, and the function will return an array with two values. The first value (`searchTerm`) represents the *current state*; the second value is a *function to update this state* (`setSearchTerm`). I will sometimes refer to this function as *state updater function*.

If you are not familiar with the syntax of the two values from the returned array, consider reading about [JavaScript array destructuring](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment#Array_destructuring). It is used to read from an array more concisely. This is array destructuring and its benefits visualized in a nutshell:

{title="Code Playground",lang="javascript"}
~~~~~~~
// basic array definition
const list = ['a', 'b'];

// no array destructuring
const itemOne = list[0];
const itemTwo = list[1];

// array destructuring
const [firstItem, secondItem] = list;
~~~~~~~

In the case of React, the React `useState` hook is a function which returns an array. Take again the following JavaScript example as comparison:

{title="Code Playground",lang="javascript"}
~~~~~~~
function getAlphabet() {
  return ['a', 'b'];
}

// no array destructuring
const itemOne = getAlphabet()[0];
const itemTwo = getAlphabet()[1];

// array destructuring
const [firstItem, secondItem] = getAlphabet();
~~~~~~~

Array destructuring is just a shorthand version of accessing each item one by one. If you express it without the array destructuring in React, it becomes less readable:

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  const stories = [ ... ];

  // less readable version without array destructuring
  const searchTermState = React.useState('');
  const searchTerm = searchTermState[0];
  const setSearchTerm = searchTermState[1];

  ...
};
~~~~~~~

The React team chose array destructuring because of its concise syntax and ability to name destructured variables. The following code snippet is an example of array destructuring:

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

After we initialize the state and have access to the current state and the state updater function, use them to display the current state and update it within the App component's event handler:

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

When the user types into the input field, the input field's change event is captured by the handler with its current internal value. The handler's logic uses the state updater function to set the new state. After the new state is set in a component, the component renders again, meaning the component function runs again. The new state becomes the current state and can be displayed in the component's JSX.

### Exercises:

* Confirm your [source code for the last section](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/React-State).
  * Confirm the [changes from the last section](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/React-Props...hs/React-State?expand=1).
* Read more about [JavaScript array destructuring](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment#Array_destructuring).
* Read more about React's useState Hook ([0](https://www.robinwieruch.de/react-usestate-hook), [1](https://reactjs.org/docs/hooks-state.html)), as it makes your React components interactive.

## Callback Handlers in JSX

Next we'll focus on the input field and label, by separating a standalone Search component and creating an instance of it in the App component. Through this process, the Search component becomes a sibling of the List component, and vice versa. We'll also move the handler and the state into the Search component to keep our functionality intact.

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  const stories = [ ... ];

  return (
    <div>
      <h1>My Hacker Stories</h1>

# leanpub-start-insert
      <Search />
# leanpub-end-insert

      <hr />

      <List list={stories} />
    </div>
  );
};

# leanpub-start-insert
const Search = () => {
  const [searchTerm, setSearchTerm] = React.useState('');

  const handleChange = event => {
    setSearchTerm(event.target.value);
  };

  return (
    <div>
      <label htmlFor="search">Search: </label>
      <input id="search" type="text" onChange={handleChange} />

      <p>
        Searching for <strong>{searchTerm}</strong>.
      </p>
    </div>
  );
};
# leanpub-end-insert
~~~~~~~

We have an extracted Search component that handles state and shows state without revealing its content. The component displays the `searchTerm` as text but doesn't share this information with its parent or sibling components yet. Since Search component does nothing except show the search term, it becomes useless for the other components.

There is no way to pass information as JavaScript data types up the component tree, since props are naturally only passed downwards. However, we can introduce a **callback handler** as a function: A callback function gets introduced (A), is used elsewhere (B), but "calls back" to the place it was introduced (C).

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  const stories = [ ... ];

# leanpub-start-insert
  // A
  const handleSearch = event => {
    // C
    console.log(event.target.value);
  };
# leanpub-end-insert

  return (
    <div>
      <h1>My Hacker Stories</h1>

# leanpub-start-insert
      <Search onSearch={handleSearch} />
# leanpub-end-insert

      <hr />

      <List list={stories} />
    </div>
  );
};

# leanpub-start-insert
const Search = props => {
# leanpub-end-insert
  const [searchTerm, setSearchTerm] = React.useState('');

  const handleChange = event => {
    setSearchTerm(event.target.value);

# leanpub-start-insert
    // B
    props.onSearch(event);
# leanpub-end-insert
  };

  return ( ... );
};
~~~~~~~

Use comments in your source code to omit A, B, and C, as these are reminders which task each block of code is to perform. Consider the concept of the callback handler: We pass a function from one component (App) to another component (Search); we use it in the second component (Search); but use the actual callback of the function call in the first component (App). This way, we can communicate up the component tree. A handler function used in one component becomes a callback handler, which is passed down to components via React props. React props are always passed down as information the component tree, and callback handlers passed as functions in props can be used to communicate up the component hierarchy.

### Exercises:

* Confirm your [source code for the last section](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/Callback-Handler-in-JSX).
  * Confirm the [changes from the last section](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/React-State...hs/Callback-Handler-in-JSX?expand=1).
* Revisit the concepts of handler and callback handler as many times as you need.

## Lifting State in React

Currently, the Search component still has its internal state. While we established a callback handler to pass information up to the App component, we are not using it yet. We need to figure out how to share the Search component's state across multiple components.

The search term is needed in the App to filter the list before passing it to the List component as props. We'll need to **lift state up** from Search to App component to share the state with more components.

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

Always manage the state at a component where every component that's interested in it is one that either manages the state (using information directly from state) or a component below the managing component (using information from props). If a component below needs to update the state, pass a callback handler down to it (see Search component). If a component needs to use the state (e.g. displaying it), pass it down as props.

By managing the search feature state in the App component, we can finally filter the list with the stateful `searchTerm` before passing the `list` to the List component:

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

The remaining section shows a couple of refactoring steps. We will be using the final refactored version in the end, so it makes sense to understand these steps and keep them. As learned before, we can make the function more concise using a JavaScript arrow function:

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

Now we can manipulate state in React, using the Search component's callback handler in the App component to update it. The current state is used as a filter for the list. With the callback handler, we used information from the Search component in the App component to update the shared state and indirectly in the List component for the filtered list.

### Exercises:

* Confirm your [source code for the last section](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/Lifting-State-in-React).
 * Confirm the [changes from the last section](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/Callback-Handler-in-JSX...hs/Lifting-State-in-React?expand=1).

## React Controlled Components

**Controlled components** are not necessary React components, but HTML elements. Here, we'll learn how to turn the Search component and its input field into a controlled component.

Let's go through a scenario that shows  why we should follow the concept of controlled components throughout our React application. After applying the following change -- giving the `searchTerm` an initial state -- can you spot the mistake in your browser?

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
 const stories = [ ... ];

# leanpub-start-insert
 const [searchTerm, setSearchTerm] = React.useState('React');
# leanpub-end-insert

 ...
};
~~~~~~~

While the list has been filtered according to the initial search, the input field doesn't show the initial `searchTerm`. We want the input field to reflect the actual `searchTerm` used from the initial state; but it's only reflected through the filtered list.

We need to convert the Search component with its input field into a controlled component. So far, the input field doesn't know anything about the `searchTerm`. It only uses the change event to inform us of a change. Actually, the input field has a `value` attribute.

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
 const stories = [ ... ];

 const [searchTerm, setSearchTerm] = React.useState('React');

 ...

 return (
   <div>
     <h1>My Hacker Stories</h1>

# leanpub-start-insert
     <Search search={searchTerm} onSearch={handleSearch} />
# leanpub-end-insert

     ...
   </div>
 );
};

const Search = props => (
 <div>
   <label htmlFor="search">Search: </label>
   <input
     id="search"
     type="text"
# leanpub-start-insert
     value={props.search}
# leanpub-end-insert
     onChange={props.onSearch}
   />
 </div>
);
~~~~~~~

Now the input field starts with the correct initial value, using the `searchTerm` from the React state. Also, when we change the `searchTerm`, we force the input field to use the value from React's state (via props). Before, the input field managed its own internal state natively with just HTML.

We learned about controlled components in this section, and, taking all the previous sections as learning steps into consideration, discovered another concept called **unidirectional data flow**:

{title="Visualization",lang="javascript"}
~~~~~~~
UI -> Side-Effect -> State -> UI -> ...
~~~~~~~

A React application and its components start with an initial state, which may be passed down as props to other components. It's rendered for the first time as a UI. Once a side-effect occurs, like user input or data loading from a remote API, the change is captured in React's state. Once state has been changed, all the components affected by the modified state or the implicitly modified props are re-rendered (the component functions runs again).

In the previous sections, we also learned about React's **component lifecycle**. At first, all components are instantiated from the top to the bottom of the component hierarchy. This includes all hooks (e.g. `useState`) that are instantiated with their initial values (e.g. initial state). From there, the UI awaits side-effects like user interactions. Once state is changed (e.g. current state changed via state updater function from `useState`), all components affected by modified state/props render again.

Every run through a component's function takes the *recent value* (e.g. current state) from the hooks and *doesn't* reinitialize them again (e.g. initial state). This might seem odd, as one could assume the `useState` hooks function re-initializes again with its initial value, but it doesn't. Hooks initialize only once when the component renders for the first time, after which React tracks them internally with their most recent values.

### Exercises:

* Confirm your [source code for the last section](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/React-Controlled-Components).
 * Confirm the [changes from the last section](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/Lifting-State-in-React...hs/React-Controlled-Components?expand=1).
* Read more about [controlled components in React](https://www.robinwieruch.de/react-controlled-components/).
* Experiment with `console.log()` in your React components and observe how your changes render, both initially and after the input field changes.

## Props Handling (Advanced)

Props are passed from parent to child down the component tree. Since we use props to transport information from component A to component B frequently, and sometimes via component C, it is useful to know a few tricks to make this more convenient.

*Note: The following refactorings are recommended for you to learn different JavaScript/React patterns, though you can still build complete React applications without them. Consider this advanced React techniques that will make your source code more concise.*

React props are a JavaScript object, else we couldn't access `props.list` or `props.onSearch` in React components. Since `props` is an object, we can apply a couple JavaScript tricks to it. For instance, accessing its properties:

{title="Code Playground",lang="javascript"}
~~~~~~~
const user = {
 firstName: 'Robin',
 lastName: 'Wieruch',
};

// without object destructuring
const firstName = user.firstName;
const lastName = user.lastName;

console.log(firstName + ' ' + lastName);
// "Robin Wieruch"

// with object destructuring
const { firstName, lastName } = user;

console.log(firstName + ' ' + lastName);
// "Robin Wieruch"
~~~~~~~

This JavaScript feature is called [object destructuring in JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment). If we need to access multiple properties of an object, using one line of code instead of multiple lines is simpler and more elegant. Let's transfer this knowledge to React props in our Search component:

{title="src/App.js",lang="javascript"}
~~~~~~~
const Search = props => {
# leanpub-start-insert
 const { search, onSearch } = props;
# leanpub-end-insert

 return (
   <div>
     <label htmlFor="search">Search: </label>
     <input
       id="search"
       type="text"
# leanpub-start-insert
       value={search}
       onChange={onSearch}
# leanpub-end-insert
     />
   </div>
 );
};
~~~~~~~

That's a basic destructuring of the `props` object in a React component, so that its properties can be used in the component without the `props` object. We refactored the Search component's arrow function from concise body into block body to access the properties of `props`. This would happen quite often if we followed this pattern, and it wouldn't make things easier for us. We can take it a step further by destructuring the `props` right away in the function signature, omitting the block body again:

{title="src/App.js",lang="javascript"}
~~~~~~~
# leanpub-start-insert
const Search = ({ search, onSearch }) => (
# leanpub-end-insert
 <div>
   <label htmlFor="search">Search: </label>
   <input
     id="search"
     type="text"
# leanpub-start-insert
     value={search}
     onChange={onSearch}
# leanpub-end-insert
   />
 </div>
);
~~~~~~~

React's `props` are rarely used in components by themselves; rather, all the information that comes with the `props` object used as a container that's actually used in the component. By destructuring the `props` object right away in the function signature, we can conveniently access all information without dealing with its container.

Let's check out another scenario where its less about the `props` object, and more about an object that comes from it. The same lesson is applicable for the `props` object. First, we will extract a new Item component from the List component:

{title="src/App.js",lang="javascript"}
~~~~~~~
# leanpub-start-insert
const List = ({ list }) =>
 list.map(item => <Item key={item.objectID} item={item} />);
# leanpub-end-insert

# leanpub-start-insert
const Item = ({ item }) => (
 <div>
   <span>
     <a href={item.url}>{item.title}</a>
   </span>
   <span>{item.author}</span>
   <span>{item.num_comments}</span>
   <span>{item.points}</span>
 </div>
);
# leanpub-end-insert
~~~~~~~

We applied previous lesson by destructuring the `props` object in the function signature of each component. The incoming `item` of the Item component could be seen the same as the `props`, because it's never directly used in the Item component. There are three potential ways to handle this problem. The first is to perform a *nested destructuring* in the component's function signature:

{title="src/App.js",lang="javascript"}
~~~~~~~
// version 1 (final)
const Item = ({
# leanpub-start-insert
 item: {
   title,
   url,
   author,
   num_comments,
   points,
 },
# leanpub-end-insert
}) => (
 <div>
   <span>
# leanpub-start-insert
     <a href={url}>{title}</a>
# leanpub-end-insert
   </span>
# leanpub-start-insert
   <span>{author}</span>
   <span>{num_comments}</span>
   <span>{points}</span>
# leanpub-end-insert
 </div>
);
~~~~~~~

Nested destructuring introduces lots of clutter through indentations in the function signature. While it's not the most readable option, it can be useful in specific scenarios. On to the second way:

{title="src/App.js",lang="javascript"}
~~~~~~~
// version 2 (I)
const List = ({ list }) =>
 list.map(item => (
   <Item
     key={item.objectID}
# leanpub-start-insert
     title={item.title}
     url={item.url}
     author={item.author}
     num_comments={item.num_comments}
     points={item.points}
# leanpub-end-insert
   />
 ));

# leanpub-start-insert
const Item = ({ title, url, author, num_comments, points }) => (
# leanpub-end-insert
 <div>
   <span>
     <a href={url}>{title}</a>
   </span>
   <span>{author}</span>
   <span>{num_comments}</span>
   <span>{points}</span>
 </div>
);
~~~~~~~

Even though the Item component's function signature is more concise, the clutter ended up in the List component instead, because every property is passed to the Item component individually. We can improve this technique using [JavaScript's spread operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax):

{title="Code Playground",lang="javascript"}
~~~~~~~
const person = {
 firstName: 'Robin',
 lastName: 'Wieruch',
};

const details = {
 year: 1988,
 country: 'Germany',
};

const personWithDetails = { ...person, ...details };

console.log(personWithDetails);
// {
//   firstName: "Robin",
//   lastName: "Wieruch",
//   year: 1988,
//   country: "Germany"
// }
~~~~~~~

Instead of passing each property one at a time via props from List to Item component, we could use JavaScript's spread operator to pass all the object's key/value pairs as attribute/value pairs to the JSX element:

{title="src/App.js",lang="javascript"}
~~~~~~~
// version 2 (II)
const List = ({ list }) =>
# leanpub-start-insert
 list.map(item => <Item key={item.objectID} {...item} />);
# leanpub-end-insert

const Item = ({ title, url, author, num_comments, points }) => (
 ...
);
~~~~~~~

Then, we'll use [JavaScript's rest parameters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters):

{title="Code Playground",lang="javascript"}
~~~~~~~
const person = {
 firstName: 'Robin',
 lastName: 'Wieruch',
 year: 1988,
};

const { year, ...personWithoutYear } = person;

console.log(personWithoutYear);
// {
//   firstName: "Robin",
//   lastName: "Wieruch"
// }
~~~~~~~

The JavaScript rest operator is the last part of an object destructuring. It shouldn't be mistaken with the spread operator even though it has the same syntax. Usually, the rest operator happens on the right side of an assignment, with the spread operator on the left.

Now it can be used in our List component to separate the `objectID` from the item, because the `objectID` is only used as `key` and isn't used (so far) in the Item component. Only the remaining (rest) item gets spread as attribute/value pairs into the Item component (as before):

{title="src/App.js",lang="javascript"}
~~~~~~~
// version 2 (III/final)
const List = ({ list }) =>
# leanpub-start-insert
 list.map(({ objectID, ...item }) => (
   <Item key={objectID} {...item} />
# leanpub-end-insert
 ));
~~~~~~~

While this version is very concise, it comes with  advanced JavaScript features that may be unknown to some. The third way of handling this situation is to keep it the same as before:

{title="src/App.js",lang="javascript"}
~~~~~~~
// version 3 (final)
const List = ({ list }) =>
 list.map(item => <Item key={item.objectID} item={item} />);

const Item = ({ item }) => (
 <div>
   <span>
     <a href={item.url}>{item.title}</a>
   </span>
   <span>{item.author}</span>
   <span>{item.num_comments}</span>
   <span>{item.points}</span>
 </div>
);
~~~~~~~

In my opinion, this is the best technique to use when working with other people on a React project. It's not as concise as version 2, but it's more readable, gives the Item component a smaller API surface, and doesn't add too many advanced JavaScript features (spread operator, rest operator).

All these versions have their pros and cons. When refactoring a component, always aim for readability, especially when working in a team of people, and make sure make sure they're using a common React code style.

### Exercises:

* Confirm your [source code for the last section](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/Props-Handling).
 * Confirm the [changes from the last section](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/React-Controlled-Components...hs/Props-Handling?expand=1).
* Read more about [JavaScript's destructuring assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment).
* Think about the difference between  JavaScript array destructuring -- which we used for React's `useState` hook -- and object destructuring.
* Read more about [JavaScript's spread operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax).
* Read more about [JavaScript's rest parameters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters).
* Get a good sense about JavaScript (e.g. spread operator, rest parameters, destructuring) and what's related to React (e.g. props) from the last lessons.
* Continue to use your favorite way to handle React's props. If you're still undecided, consider the version used in the previous section.

## React Side-Effects

Next we'll add a feature to our Search component in the form of another React hook. We'll make the Search component remember the most recent search interaction, so the application opens it in the browser whenever it restarts.

First, use the local storage of the browser to store the `searchTerm` accompanied by an identifier. Next, use the stored value, if there a value exists, to set the initial state of the `searchTerm`. Otherwise, the initial state defaults to our initial state (here "React") as before:

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
 ...

 const [searchTerm, setSearchTerm] = React.useState(
# leanpub-start-insert
   localStorage.getItem('search') || 'React'
# leanpub-end-insert
 );

 const handleSearch = event => {
   setSearchTerm(event.target.value);

# leanpub-start-insert
   localStorage.setItem('search', event.target.value);
# leanpub-end-insert
 };

 ...
);
~~~~~~~

When using the input field and refreshing the browser tab, the browser should remember the latest search term. Using the local storage in React can be seen as a **side-effect** because we interact outside of React's domain by using the browser's API.

There is one flaw, though. The handler function should mostly be concerned about updating the state, but now it has a side-effect. If we use the `setSearchTerm` function elsewhere in our application, we will break the feature we implemented because we can't be sure the local storage will also get updated. Let's fix this by handling the side-effect at a dedicated place. We'll use **React's useEffect Hook** to trigger the side-effect each time the `searchTerm` changes:

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
 ...

 const [searchTerm, setSearchTerm] = React.useState(
   localStorage.getItem('search') || 'React'
 );

# leanpub-start-insert
 React.useEffect(() => {
   localStorage.setItem('search', searchTerm);
 }, [searchTerm]);
# leanpub-end-insert

# leanpub-start-insert
 const handleSearch = event => {
   setSearchTerm(event.target.value);
 };
# leanpub-end-insert

 ...
);
~~~~~~~

React's useEffect Hook takes two arguments: The first argument is a function where the side-effect occurs. In our case, the side-effect is when the user types the `searchTerm` into the browser's local storage. The second argument is a dependency array of variables. If one variable changes, the function for the side-effect is called. In our case, the function is called every time the `searchTerm` changes; it's called initially when the component renders for the first time.

If the dependency array of React's useEffect is an empty array, the function for the side-effect is only called once, after the component renders for the first time. The hook lets us opt into React's component lifecycle. It can be triggered when the component is first mounted, but also one of its dependencies are updated.

Using React `useEffect` instead of managing the side-effect in the handler has made the application more robust. *Whenever* and *wherever* `searchTerm` is updated via `setSearchTerm`, local storage will always be in sync with it.

### Exercises:

* Confirm your [source code for the last section](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/React-Side-Effects).
 * Confirm the [changes from the last section](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/Props-Handling...hs/React-Side-Effects?expand=1).
* Read more about React's useEffect Hook ([0](https://reactjs.org/docs/hooks-effect.html), [1](https://reactjs.org/docs/hooks-reference.html#useeffect)).
* Give the first argument's function a `console.log()` and experiment with React's useEffect Hook's dependency array. Check the logs for an empty dependency array too.

## React Custom Hooks (Advanced)

Thus far we've covered the two most popular hooks in React: useState and useEffect. useState is used to make your application interactive; useEffect is used to opt into the lifecycle of your components.

We'll eventually cover more hooks that come with React -- in this volume and in other resources -- though we won't cover all of them here. Next we'll tackle **React custom Hooks**; that is, building a hook yourself.

We will use the two hooks we already possess to create a new custom hook called `useSemiPersistentState`, named as such because it manages state yet synchronizes with the local storage. It's not fully persistent because clearing the local storage of the browser deletes relevant data for this application. Start by extracting all relevant implementation details from the App component into this new custom hook:

{title="src/App.js",lang="javascript"}
~~~~~~~
# leanpub-start-insert
const useSemiPersistentState = () => {
 const [searchTerm, setSearchTerm] = React.useState(
   localStorage.getItem('search') || ''
 );

 React.useEffect(() => {
   localStorage.setItem('search', searchTerm);
 }, [searchTerm]);
};
# leanpub-end-insert

const App = () => {
...
};
~~~~~~~

So far, it's just a function around our previously in the App component used `useState` and `useEffect` hooks. Before we can use it, let's return the values that are needed in our App component from this custom hook:

{title="src/App.js",lang="javascript"}
~~~~~~~
const useSemiPersistentState = () => {
 const [searchTerm, setSearchTerm] = React.useState(
   localStorage.getItem('search') || ''
 );

 React.useEffect(() => {
   localStorage.setItem('search', searchTerm);
 }, [searchTerm]);

# leanpub-start-insert
 return [searchTerm, setSearchTerm];
# leanpub-end-insert
};
~~~~~~~

We are following two conventions of React's built-in hooks here. First, the naming convention which puts the "use" prefix in front of every hook name; second, the returned values are returned as an array. Now we can use the custom hook with its returned values in the App component with the usual array destructuring:

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
 const stories = [ ... ];

# leanpub-start-insert
 const [searchTerm, setSearchTerm] = useSemiPersistentState();
# leanpub-end-insert

 const handleSearch = event => {
   setSearchTerm(event.target.value);
 };

 const searchedStories = stories.filter(story =>
   story.title.toLowerCase().includes(searchTerm.toLowerCase())
 );

 return (
   ...
 );
};
~~~~~~~

Another goal of a custom hook should be reusability. All of this custom hook's internals are about the search domain, but the hook should be for a value that's set in state and synchronized in local storage. Let's adjust the naming therefore:

{title="src/App.js",lang="javascript"}
~~~~~~~
const useSemiPersistentState = () => {
# leanpub-start-insert
 const [value, setValue] = React.useState(
   localStorage.getItem('value') || ''
# leanpub-end-insert
 );

 React.useEffect(() => {
# leanpub-start-insert
   localStorage.setItem('value', value);
 }, [value]);
# leanpub-end-insert

# leanpub-start-insert
 return [value, setValue];
# leanpub-end-insert
};
~~~~~~~

We handle an abstracted "value" within the custom hook. Using it in the App component, we can name the returned current state and state updater function anything domain-related (e.g. `searchTerm` and `setSearchTerm`) with array destructuring.

There is still one problem with this custom hook. Using the custom hook more than once in a React application leads to an overwrite of the "value"-allocated item in the local storage. To fix this, pass in a key:

{title="src/App.js",lang="javascript"}
~~~~~~~
# leanpub-start-insert
const useSemiPersistentState = key => {
# leanpub-end-insert
 const [value, setValue] = React.useState(
# leanpub-start-insert
   localStorage.getItem(key) || ''
# leanpub-end-insert
 );

 React.useEffect(() => {
# leanpub-start-insert
   localStorage.setItem(key, value);
 }, [value, key]);
# leanpub-end-insert

 return [value, setValue];
};

const App = () => {
 ...

 const [searchTerm, setSearchTerm] = useSemiPersistentState(
# leanpub-start-insert
   'search'
# leanpub-end-insert
 );

 ...
};
~~~~~~~

Since the key comes from outside, the custom hook assumes that it could change, so it needs to be included in the dependency array of the `useEffect` hook. Without it, the side-effect may run with an outdated key (also called *stale*) if the key changed between renders.

Another improvement is to give the custom hook the initial state we had from the outside:

{title="src/App.js",lang="javascript"}
~~~~~~~
# leanpub-start-insert
const useSemiPersistentState = (key, initialState) => {
# leanpub-end-insert
 const [value, setValue] = React.useState(
# leanpub-start-insert
   localStorage.getItem(key) || initialState
# leanpub-end-insert
 );

 ...
};

const App = () => {
 ...

 const [searchTerm, setSearchTerm] = useSemiPersistentState(
# leanpub-start-insert
   'search',
   'React'
# leanpub-end-insert
 );

 ...
};
~~~~~~~

You've just created your first custom hook. If you're not comfortable with custom hooks, you can revert the changes and use the `useState` and `useEffect` hook as before, in the App component.

However, knowing more about custom hooks gives you lots of new options. A custom hook can encapsulate non-trivial implementation details that should be kept away from a component; can be used in more than one React component; and can even be open-sourced as an external library. Using your favorite search engine, you'll notice there are hundreds of React hooks that could be used in your application without worry over implementation details.

### Exercises:

* Confirm your [source code for the last section](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/React-Custom-Hooks).
 * Confirm the [changes from the last section](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/React-Side-Effects...hs/React-Custom-Hooks?expand=1).
* Read more about [React Hooks](https://www.robinwieruch.de/react-hooks) to get a good understanding of them. They are the bread and butter in React function components, so it's important to really understand them ([0](https://reactjs.org/docs/hooks-overview.html), [1](https://reactjs.org/docs/hooks-custom.html)).

## React Fragments

One caveat with JSX, especially when we create a dedicated Search component, is that we must introduce a wrapping HTML element to render it:

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

Normally the JSX returned by a React component needs only one wrapping top-level element. To render multiple top-level elements side-by-side, we have to wrap them into an array instead. Since we're working with a list of elements, we have to give every sibling element React's `key` attribute:

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

This is one way to have multiple top-level elements in your JSX. It doesn't turn out very readable, though, as it becomes verbose with the additional key attribute. Another solution is to use a **React fragment**:

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

A fragment wraps other elements into a single top-level element without adding to the rendered output. Both Search elements should be visible in your browser now, with input field and label. So if you prefer to omit the wrapping `<div>` or `<span>` elements, substitute them with an empty tag that is allowed in JSX, and doesn't introduce intermediate elements in our rendered HTML.

### Exercises:

* Confirm your [source code for the last section](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/React-Fragments).
 * Confirm the [changes from the last section](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/React-Custom-Hooks...hs/React-Fragments?expand=1).
* Read more about [React fragments](https://reactjs.org/docs/fragments.html).

## Reusable React Component

Have a closer look at the Search component. The label element has the text "Search: "; the id/htmlFor attributes have the `search` identifier; the value is called `search`; and the callback handler is called `onSearch`. The component is very much tied to the search feature, which makes it less reusable for the rest of the application and non search-related tasks. It also risks introducing bugs if two of these Search components are rendered side by side, because the htmlFor/id combination is duplicated, breaking the focus when one of the labels is clicked by the user.

Since the Search component doesn't have any actual "search" functionality, it takes little effort to generalize other search domain properties to make the component reusable for the rest of the application. Let's pass an additional `id` and `label` prop to the Search component, rename the actual value and callback handler to something more abstract, and rename the component accordingly:

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
 ...

 return (
   <div>
     <h1>My Hacker Stories</h1>

# leanpub-start-insert
     <InputWithLabel
       id="search"
       label="Search"
# leanpub-end-insert
       value={searchTerm}
# leanpub-start-insert
       onInputChange={handleSearch}
# leanpub-end-insert
     />

     ...
   </div>
 );
};

# leanpub-start-insert
const InputWithLabel = ({ id, label, value, onInputChange }) => (
# leanpub-end-insert
 <>
# leanpub-start-insert
   <label htmlFor={id}>{label}</label>
   &nbsp;
# leanpub-end-insert
   <input
# leanpub-start-insert
     id={id}
# leanpub-end-insert
     type="text"
     value={value}
# leanpub-start-insert
     onChange={onInputChange}
# leanpub-end-insert
   />
 </>
);
~~~~~~~

It's not fully reusable yet. If we want an input field for data like a number (`number`) or phone number (`tel`), the `type` attribute of the input field needs to be accessible from the outside too:

{title="src/App.js",lang="javascript"}
~~~~~~~
const InputWithLabel = ({
 id,
 label,
 value,
# leanpub-start-insert
 type = 'text',
# leanpub-end-insert
 onInputChange,
}) => (
 <>
   <label htmlFor={id}>{label}</label>
   &nbsp;
   <input
     id={id}
# leanpub-start-insert
     type={type}
# leanpub-end-insert
     value={value}
     onChange={onInputChange}
   />
 </>
);
~~~~~~~

From the App component, no `type` prop is passed to the InputWithLabel component, so it is not specified from the outside. The [default parameter](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Default_parameters) from the function signature takes over for the input field.

With just a few changes we turned a specialized Search component into a more reusable component. We generalized the naming of the internal implementation details and gave the new component a larger API surface to provide all the necessary information from the outside. We aren't using the component elsewhere, but we increased its ability to handle the task if we do.

### Exercises:

* Confirm your [source code for the last section](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/Reusable-React-Component).
 * Confirm the [changes from the last section](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/React-Fragments...hs/Reusable-React-Component?expand=1).
* Read more about [Reusable React Components](https://www.robinwieruch.de/react-reusable-components).
* Before we used the text "Search:" with a ":". How would you deal with it now? Would you pass it with `label="Search:"` as prop to the InputWithLabel component or hardcode it after the `<label htmlFor={id}>{label}:</label>` usage in the InputWithLabel component? We will see how to cope with this later.

## React Component Composition

Now we'll discover how to use a React element in the same fashion as an HTML element, with an opening and closing tag:

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

  return (
    <div>
      <h1>My Hacker Stories</h1>

      <InputWithLabel
        id="search"
        value={searchTerm}
        onInputChange={handleSearch}
# leanpub-start-insert
      >
        Search
      </InputWithLabel>
# leanpub-end-insert

      ...
    </div>
  );
};
~~~~~~~

Instead of using the `label` prop from before, we inserted the text "Search:" between the component's element's tags. In the InputWithLabel component, you have access to this information via **React's children** prop. Instead of using the`label` prop, use the children`prop to render everything that has been passed down from above where you want it:

{title="src/App.js",lang="javascript"}
~~~~~~~
const InputWithLabel = ({
  id,
  value,
  type = 'text',
  onInputChange,
# leanpub-start-insert
  children,
# leanpub-end-insert
}) => (
  <>
# leanpub-start-insert
    <label htmlFor={id}>{children}</label>
# leanpub-end-insert
    &nbsp;
    <input
      id={id}
      type={type}
      value={value}
      onChange={onInputChange}
    />
  </>
);
~~~~~~~

Now the React component's elements behave similar to native HTML. Everything that's passed between a component's elements can be accessed as children`in the component and be rendered somewhere. Sometimes when using a React component, you want to have more freedom from the outside what to render in the inside of a component:

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

  return (
    <div>
      <h1>My Hacker Stories</h1>

      <InputWithLabel
        id="search"
        value={searchTerm}
        onInputChange={handleSearch}
      >
# leanpub-start-insert
        <strong>Search:</strong>
# leanpub-end-insert
      </InputWithLabel>

      ...
    </div>
  );
};
~~~~~~~

With this React feature, we can compose React components into each other. We've used it with a JavaScript string and with a string wrapped in an HTML `<strong>` element, but it doesn't end here. You can pass components via React children as well.

### Exercises:

* Confirm your [source code for the last section](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/React-Component-Composition).
  * Confirm the [changes from the last section](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/Reusable-React-Component...hs/React-Component-Composition?expand=1).
* Read more about React Component Composition ([0](https://www.robinwieruch.de/react-component-composition), [1](https://reactjs.org/docs/composition-vs-inheritance.html)).
* Create a simple text component that renders a string and passes it as `children` to the InputWithLabel component.

## Imperative React

React is inherently declarative, starting with JSX and ending with hooks. In JSX, we tell React *what* to render and not *how* to render it. In a React side-effect Hook (useEffect), we express when to achieve *what* instead of *how* to achieve it. Sometimes, however, we'll want to access the rendered elements of JSX imperatively, in cases such as these:

* read/write access to elements via the DOM API:
  * measure (read) an element's width or height
  * setting (write) an input field's focus state
* implementation of more complex animations:
  * setting transitions
  * orchestrating transitions
* integration of third-party libraries:
  * [D3](https://d3js.org/) is a popular imperative chart library

Because imperative programming in React is often verbose and counterintuitive, we'll walk only through a small example for setting the focus of an input field imperatively. For the declarative way, simply set the input field's autofocus attribute:

{title="src/App.js",lang="javascript"}
~~~~~~~
const InputWithLabel = ({ ... }) => (
  <>
    <label htmlFor={id}>{children}</label>
    &nbsp;
    <input
      id={id}
      type={type}
      value={value}
# leanpub-start-insert
      autoFocus
# leanpub-end-insert
      onChange={onInputChange}
    />
  </>
);
~~~~~~~

This works, but only if one of the reusable components is rendered once. For instance, if the App component renders two InputWithLabel components, only the last rendered component receives the auto-focus on its render. However, since we have a reusable React component here, we can pass a dedicated prop and let the developer decide whether its input field should have an autofocus or not:

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

  return (
    <div>
      <h1>My Hacker Stories</h1>

      <InputWithLabel
        id="search"
        value={searchTerm}
# leanpub-start-insert
        isFocused
# leanpub-end-insert
        onInputChange={handleSearch}
      >
        <strong>Search:</strong>
      </InputWithLabel>

      ...
    </div>
  );
};
~~~~~~~

Using just `isFocused` as an attribute is equivalent to `isFocused={true}`. Within the component, use the new prop for the input field's `autoFocus` attribute:

{title="src/App.js",lang="javascript"}
~~~~~~~
const InputWithLabel = ({
  id,
  value,
  type = 'text',
  onInputChange,
# leanpub-start-insert
  isFocused,
# leanpub-end-insert
  children,
}) => (
  <>
    <label htmlFor={id}>{children}</label>
    &nbsp;
    <input
      id={id}
      type={type}
      value={value}
# leanpub-start-insert
      autoFocus={isFocused}
# leanpub-end-insert
      onChange={onInputChange}
    />
  </>
);
~~~~~~~

The feature works, yet it's still a declarative implementation. We are telling React *what* to do and not *how* to do it. Even though it's possible to do it with the declarative approach, let's refactor this scenario to an imperative approach. We want to execute the `focus()` method programmatically via the input field's DOM API once it has been rendered:

{title="src/App.js",lang="javascript"}
~~~~~~~
const InputWithLabel = ({
  id,
  value,
  type = 'text',
  onInputChange,
  isFocused,
  children,
}) => {
# leanpub-start-insert
  // A
  const inputRef = React.useRef();
# leanpub-end-insert

# leanpub-start-insert
  // C
  React.useEffect(() => {
    if (isFocused && inputRef.current) {
      // D
      inputRef.current.focus();
    }
  }, [isFocused]);
# leanpub-end-insert

  return (
    <>
      <label htmlFor={id}>{children}</label>
      &nbsp;
# leanpub-start-insert
       {/* B */}
# leanpub-end-insert
      <input
# leanpub-start-insert
        ref={inputRef}
# leanpub-end-insert
        id={id}
        type={type}
        value={value}
        onChange={onInputChange}
      />
    </>
  );
};
~~~~~~~

All the essential steps are marked with comments that are explained step by step:

* (A) First, create a `ref` with **React's useRef hook**. This `ref` object is a persistent value which stays intact over the lifetime of a React component. It comes with a property called `current`, which, in contrast to the `ref` object, can be changed.
* (B) Second, the `ref` is passed to the input field's JSX-reserved `ref` attribute and the element instance is assigned to the changeable `current` property.
* (C) Third, opt into React's lifecycle with React's useEffect Hook, performing the focus on the input field when the component renders (or its dependencies change).
* (D) And fourth, since the `ref` is passed to the input field's `ref` attribute, its `current` property gives access to the element. Execute its focus programmatically as a side-effect, but only if `isFocused` is set and the `current` property is existent.

This was an example of how to move from declarative to imperative programming in React. It's now always possible to go the declarative way, so the imperative approach is necessary. This lesson is for the sake of learning about the DOM API in React.

### Exercises:

* Confirm your [source code for the last section](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/Imperative-React).
  * Confirm the [changes from the last section](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/React-Component-Composition...hs/Imperative-React?expand=1).
* Read more about [React's useRef Hook](https://reactjs.org/docs/hooks-reference.html#useref).

## Inline Handler in JSX

The list of stories we have so far is only an unstateful variable. We can filter the rendered list with the search feature, but the list itself stays intact if we remove the filter. The filter is just a temporary change through a third party, but we can't manipulate the real list yet.

To gain control over the list, make it stateful by using it as initial state in React's useState Hook. The returned values are the current state (`stories`) and the state updater function (`setStories`). We aren't using the custom `useSemiPersistentState` hook yet, because we don't want to open the browser with the cached list each time. Instead, we always want to start with the initial list.

{title="src/App.js",lang="javascript"}
~~~~~~~
# leanpub-start-insert
const initialStories = [
  {
    title: 'React',
    ...
  },
  {
    title: 'Redux',
    ...
  },
];
# leanpub-end-insert

const useSemiPersistentState = (key, initialState) => { ... };

const App = () => {
  const [searchTerm, setSearchTerm] = ...

# leanpub-start-insert
  const [stories, setStories] = React.useState(initialStories);
# leanpub-end-insert

  ...
};
~~~~~~~

The application behaves the same because the `stories`, now returned from `useState`, are still filtered into `searchedStories` and displayed in the List. Next we'll manipulate the list by removing an item from it:

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

  const [stories, setStories] = React.useState(initialStories);

# leanpub-start-insert
  const handleRemoveStory = item => {
    const newStories = stories.filter(
      story => item.objectID !== story.objectID
    );

    setStories(newStories);
  };
# leanpub-end-insert

  ...

  return (
    <div>
      <h1>My Hacker Stories</h1>

      ...

      <hr />

# leanpub-start-insert
      <List list={searchedStories} onRemoveItem={handleRemoveStory} />
# leanpub-end-insert
    </div>
  );
};
~~~~~~~

The callback handler in the App component receives an item to be removed as an argument, and filters the current stories based on this information by removing all items that don't meet its condition(s). The returned stories are then set as new state, and the List component passes the function to its child component. It's not using this new information; it's just passing it on:

{title="src/App.js",lang="javascript"}
~~~~~~~
# leanpub-start-insert
const List = ({ list, onRemoveItem }) =>
# leanpub-end-insert
  list.map(item => (
    <Item
      key={item.objectID}
      item={item}
# leanpub-start-insert
      onRemoveItem={onRemoveItem}
# leanpub-end-insert
    />
  ));
~~~~~~~

Finally, we can use the incoming function in another handler in the Item component to pass the `item` to it. A button element is used to trigger the actual event:

{title="src/App.js",lang="javascript"}
~~~~~~~
# leanpub-start-insert
const Item = ({ item, onRemoveItem }) => {
  const handleRemoveItem = () => {
    onRemoveItem(item);
  };
# leanpub-end-insert

  return (
    <div>
      <span>
        <a href={item.url}>{item.title}</a>
      </span>
      <span>{item.author}</span>
      <span>{item.num_comments}</span>
      <span>{item.points}</span>
# leanpub-start-insert
      <span>
        <button type="button" onClick={handleRemoveItem}>
          Dismiss
        </button>
      </span>
# leanpub-end-insert
    </div>
  );
};
~~~~~~~

We could have passed only the item's `objectID`, since that's all we need  in the App component's callback handler, but we aren't sure what  information the handler might need later. It may need more than an identifier to remove an item. If we call the handler `onRemoveItem`, it should be the item being passed, not just its identifier.

We have made the list of stories stateful with React's useState Hook; passed the still searched stories down as props to the List component; and implemented a callback handler (`handleRemoveStory`) and handler (`handleRemoveItem`) to be used in their respective components. Since a handler is just a function, and in this case it doesn't return anything, we could remove the block body for it for the sake of completeness.

{title="src/App.js",lang="javascript"}
~~~~~~~
const Item = ({ item, onRemoveItem }) => {
# leanpub-start-insert
  const handleRemoveItem = () =>
    onRemoveItem(item);
# leanpub-end-insert

  ...
};
~~~~~~~

This change makes our source code less readable as we accumulate handlers in the function component. Sometimes I refactor handlers in a function component from an arrow function back to a normal function statement, just to make the component more explorable:

{title="src/App.js",lang="javascript"}
~~~~~~~
const Item = ({ item, onRemoveItem }) => {
# leanpub-start-insert
  function handleRemoveItem() {
    onRemoveItem(item);
  }
# leanpub-end-insert

  ...
};
~~~~~~~

In this section we applied props, handlers, callback handlers, and state. That are all lessons learned from before. Now we'll tackle **inline handlers**, which allow us to execute the function right in the JSX. There are two solutions using the incoming function in the Item component as an inline handler. First, using JavaScript's bind method:

{title="src/App.js",lang="javascript"}
~~~~~~~
const Item = ({ item, onRemoveItem }) => (
  <div>
    <span>
      <a href={item.url}>{item.title}</a>
    </span>
    <span>{item.author}</span>
    <span>{item.num_comments}</span>
    <span>{item.points}</span>
    <span>
# leanpub-start-insert
      <button type="button" onClick={onRemoveItem.bind(null, item)}>
# leanpub-end-insert
        Dismiss
      </button>
    </span>
  </div>
);
~~~~~~~

Using [JavaScript's bind method](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_objects/Function/bind) on a function allows us to bind arguments directly to that function that should be used when executing it. The bind method returns a new function with the bound argument attached.

The second and more popular solution is to use a wrapping arrow function, which allows us to sneak in arguments like `item`:

{title="src/App.js",lang="javascript"}
~~~~~~~
const Item = ({ item, onRemoveItem }) => (
  <div>
    <span>
      <a href={item.url}>{item.title}</a>
    </span>
    <span>{item.author}</span>
    <span>{item.num_comments}</span>
    <span>{item.points}</span>
    <span>
# leanpub-start-insert
      <button type="button" onClick={() => onRemoveItem(item)}>
# leanpub-end-insert
        Dismiss
      </button>
    </span>
  </div>
);
~~~~~~~

This is a quick solution, because sometimes we don't want to refactor a function component's concise function body back to a block body to define an appropriate handler between function signature and return statement. While this way is more concise than the others, it can also be more difficult to debug because JavaScript logic may be hidden in JSX. It becomes even more verbose if the wrapping arrow function encapsulates more than one line of implementation logic, by using a block body instead of a concise body. This should be avoided:

{title="Code Playground",lang="javascript"}
~~~~~~~
const Item = ({ item, onRemoveItem }) => (
  <div>
    ...
    <span>
      <button
        type="button"
        onClick={() => {
          // do something else

          // note: avoid using complex logic in JSX

          onRemoveItem(item);
        }}
      >
        Dismiss
      </button>
    </span>
  </div>
);
~~~~~~~

All three handler versions, two of which are inline and the normal handler, are acceptable. The non-inlined handler moves the implementation details into the function component's block body; the inline handler move the implementation details into the JSX.

### Exercises:

* Confirm your [source code for the last section](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/Inline-Handler-in-JSX).
  * Confirm the [changes from the last section](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/Imperative-React...hs/Inline-Handler-in-JSX?expand=1).
* Review handlers, callback handlers, and inline handlers.

## React Asynchronous Data

We have two interactions in our application: searching the list, and removing items from the list. The first interaction is a fluctuant interference through a third-party state (`searchTerm`) applied on the list; the second interaction is a non-reversible deletion of an item from the list.

Sometimes we must render a component before we can fetch data from a third-party API and display it. In the following, we will simulate this kind of asynchronous data in the application. In a live application, this asynchronous data gets fetched from a real remote API. We start off with a function that returns a promise -- data, once it resolves -- in its shorthand version. The resolved object holds the previous list of stories:

{title="src/App.js",lang="javascript"}
~~~~~~~
const initialStories = [ ... ];

# leanpub-start-insert
const getAsyncStories = () =>
  Promise.resolve({ data: { stories: initialStories } });
# leanpub-end-insert
~~~~~~~

In the App component, instead of using the `initialStories`, use an empty array for the initial state. We want to start off with an empty list of stories, and simulate fetching these stories asynchronously. In a new `useEffect` hook, call the function and resolve the returned promise. Due to the empty dependency array, the side-effect only runs once the component renders for the first time:

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

# leanpub-start-insert
  const [stories, setStories] = React.useState([]);
# leanpub-end-insert

# leanpub-start-insert
  React.useEffect(() => {
    getAsyncStories().then(result => {
      setStories(result.data.stories);
    });
  }, []);
# leanpub-end-insert

  ...
};
~~~~~~~

Even though the data should arrive asynchronously when we start the application, it appears to arrive synchronously, because it's rendered immediately. Let's change this by giving it a bit of a realistic delay, because every network request to an API would come with a delay. First, remove the shorthand version for the promise:

{title="src/App.js",lang="javascript"}
~~~~~~~
const getAsyncStories = () =>
# leanpub-start-insert
  new Promise(resolve =>
    resolve({ data: { stories: initialStories } })
  );
# leanpub-end-insert
~~~~~~~

And second, when resolving the promise, delay it for a few seconds:

{title="src/App.js",lang="javascript"}
~~~~~~~
const getAsyncStories = () =>
  new Promise(resolve =>
# leanpub-start-insert
    setTimeout(
      () => resolve({ data: { stories: initialStories } }),
      2000
    )
# leanpub-end-insert
  );
~~~~~~~

Once you start the application again, you should see a delayed rendering of the list. The initial state for the stories is an empty array. After the App component rendered, the side-effect hook runs once to fetch the asynchronous data. After resolving the promise and setting the data in the component's state, the component renders again and displays the list of asynchronously loaded stories.

### Exercises:

* Confirm your [source code for the last section](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/React-Asynchronous-Data).
  * Confirm the [changes from the last section](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/Inline-Handler-in-JSX...hs/React-Asynchronous-Data?expand=1).
* Read more about [JavaScript Promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise).

## React Conditional Rendering

Handling asynchronous data in React leaves us with conditional states: with data and without data. This case is already covered, though, because our initial state is an empty list rather than `null`. If it was null, we'd have to handle this issue in our JSX. However, since it's `[]`, we `filter()` over an empty array for the search feature, which leaves us with an empty array. This leads to rendering nothing in the List component's `map()` function.

In a real world application, there are more than two conditional states for asynchronous data, though. Consider showing users a loading indicator when data loading is delayed:

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

  const [stories, setStories] = React.useState([]);
# leanpub-start-insert
  const [isLoading, setIsLoading] = React.useState(false);
# leanpub-end-insert

  React.useEffect(() => {
# leanpub-start-insert
    setIsLoading(true);
# leanpub-end-insert

    getAsyncStories().then(result => {
      setStories(result.data.stories);
# leanpub-start-insert
      setIsLoading(false);
# leanpub-end-insert
    });
  }, []);

  ...
};
~~~~~~~

With [JavaScript's ternary operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_Operator), we can inline this conditional state as a **conditional rendering** in JSX:

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

  return (
    <div>
      ...

      <hr />

# leanpub-start-insert
      {isLoading ? (
        <p>Loading ...</p>
      ) : (
# leanpub-end-insert
        <List
          list={searchedStories}
          onRemoveItem={handleRemoveStory}
        />
# leanpub-start-insert
      )}
# leanpub-end-insert
    </div>
  );
};
~~~~~~~

Asynchronous data comes with error handling, too. It doesn't happen in our simulated environment, but there could be errors if we start fetching data from another third-party API. Introduce another state for error handling and solve it in the promise's `catch()` block when resolving the promise:

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

  const [stories, setStories] = React.useState([]);
  const [isLoading, setIsLoading] = React.useState(false);
# leanpub-start-insert
  const [isError, setIsError] = React.useState(false);
# leanpub-end-insert

  React.useEffect(() => {
    setIsLoading(true);

    getAsyncStories()
      .then(result => {
        setStories(result.data.stories);
        setIsLoading(false);
      })
# leanpub-start-insert
      .catch(() => setIsError(true));
# leanpub-end-insert
  }, []);

  ...
};
~~~~~~~

Next, give the user feedback in case something went wrong with another conditional rendering. This time, it's either rendering something or nothing. So instead of having a ternary operator where one side returns `null`, use the logical `&&` operator as shorthand:

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

  return (
    <div>
      ...

      <hr />

# leanpub-start-insert
      {isError && <p>Something went wrong ...</p>}
# leanpub-end-insert

      {isLoading ? (
        <p>Loading ...</p>
      ) : (
        ...
      )}
    </div>
  );
};
~~~~~~~

In JavaScript, a `true && 'Hello World'` always evaluates to 'Hello World'. A `false && 'Hello World'` always evaluates to false. In React, we can use this behaviour to our advantage. If the condition is true, the expression after the logical `&&` operator will be the output. If the condition is false, React ignores it and skips the expression.

Conditional rendering is not just for asynchronous data though. The simplest example of conditional rendering is a boolean flag state that's toggled with a button. If the boolean flag is true, render something, if it is false, don't render anything.

This feature can be quite powerful, because it gives you the ability to conditionally render JSX. It's yet another tool in React to make your UI more dynamic. And as we've discovered, it's often necessary for more complex control flows like asynchronous data.

### Exercises:

* Confirm your [source code for the last section](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/React-Conditional-Rendering).
  * Confirm the [changes from the last section](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/React-Asynchronous-Data...hs/React-Conditional-Rendering?expand=1).
* Read more about [conditional rendering in React](https://www.robinwieruch.de/conditional-rendering-react/).

## React Advanced State

All state management in this application makes heavy use of React's useState Hook. More sophisticated state management gives you **React's useReducer Hook**, though. Since the concept of reducers in JavaScript splits the community in half, we won't cover it extensively here, but the exercises at the end of this section should give you plenty of practice.

We'll move the `stories` state management from the `useState` hook to a new `useReducer` hook. First, introduce a reducer function outside of your components. A reducer function always receives `state` and `action`. Based on these two arguments, a reducer always returns a new state:

{title="src/App.js",lang="javascript"}
~~~~~~~
# leanpub-start-insert
const storiesReducer = (state, action) => {
  if (action.type === 'SET_STORIES') {
    return action.payload;
  } else {
    throw new Error();
  }
};
# leanpub-end-insert
~~~~~~~

A reducer `action` is often associated with a `type`. If this type matches a condition in the reducer, do something. If it isn't covered by the reducer, throw an error to remind yourself the implementation isn't covered. The `storiesReducer` function covers one `type, and then returns the `payload` of the incoming action without using the current state to compute the new state. The new state is simply the `payload`.

In the App component, exchange `useState` for `useReducer` for managing the `stories`. The new hook receives a reducer function and an initial state as arguments and returns an array with two items. The first item is the *current state*; the second item is the *state updater function* (also called *dispatch function*):

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

# leanpub-start-insert
  const [stories, dispatchStories] = React.useReducer(
    storiesReducer,
    []
  );
# leanpub-end-insert

  ...
};
~~~~~~~

The new dispatch function can be used instead of the `setStories` function, which was returned from `useState`. Instead of setting state explicitly with the state updater function from `useState`, the `useReducer` state updater function dispatches an action for the reducer. The action comes with a `type` and an optional payload:

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

  React.useEffect(() => {
    setIsLoading(true);

    getAsyncStories()
      .then(result => {
# leanpub-start-insert
        dispatchStories({
          type: 'SET_STORIES',
          payload: result.data.stories,
        });
# leanpub-end-insert
        setIsLoading(false);
      })
      .catch(() => setIsError(true));
  }, []);

  ...

  const handleRemoveStory = item => {
    const newStories = stories.filter(
      story => item.objectID !== story.objectID
    );

# leanpub-start-insert
    dispatchStories({
      type: 'SET_STORIES',
      payload: newStories,
    });
# leanpub-end-insert
  };

  ...
};
~~~~~~~

The application appears the same in the browser, though a reducer and React's `useReducer` hook are managing the state for the stories now. Let's bring the concept of a reducer to a minimal version by handling more than one state transition.

So far, the `handleRemoveStory` handler computes the new stories. It's valid to move this logic into the reducer function and manage the reducer with an action, which is another case for moving from imperative to declarative programming. Instead of doing it ourselves by saying *how it should be done*, we are telling the reducer *what to do*. Everything else is hidden in the reducer.

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

  const handleRemoveStory = item => {
# leanpub-start-insert
    dispatchStories({
      type: 'REMOVE_STORY',
      payload: item,
    });
# leanpub-end-insert
  };

  ...
};
~~~~~~~

Now the reducer function has to cover this new case in a new conditional state transition. If the condition for removing a story is met, the reducer has all the implementation details needed to remove the story. The action gives all the necessary information, an item's identifier`, to remove the story from the current state and return a new list of filtered stories as state.

{title="src/App.js",lang="javascript"}
~~~~~~~
const storiesReducer = (state, action) => {
  if (action.type === 'SET_STORIES') {
    return action.payload;
# leanpub-start-insert
  } else if (action.type === 'REMOVE_STORY') {
    return state.filter(
      story => action.payload.objectID !== story.objectID
    );
  } else {
# leanpub-end-insert
    throw new Error();
  }
};
~~~~~~~

All these if else statements will eventually clutter when adding more state transitions into one reducer function. Refactoring it to a switch statement for all the state transitions makes it more readable:

{title="src/App.js",lang="javascript"}
~~~~~~~
const storiesReducer = (state, action) => {
# leanpub-start-insert
  switch (action.type) {
    case 'SET_STORIES':
      return action.payload;
    case 'REMOVE_STORY':
      return state.filter(
        story => action.payload.objectID !== story.objectID
      );
    default:
      throw new Error();
  }
# leanpub-end-insert
};
~~~~~~~

What we've covered is a minimal version of a reducer in JavaScript. It covers two state transitions, shows how to compute current state and action into a new state, and uses some business logic (removal of a story). Now we can set a list of stories as state for the asynchronously arriving data, and remove a story from the list of stories, with just one state managing reducer and its associated `useReducer` hook.

To fully grasp the concept of reducers in JavaScript and the usage of React's useReducer Hook, visit the linked resources in the exercises.

### Exercises:

* Confirm your [source code for the last section](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/React-Advanced-State).
  * Confirm the [changes from the last section](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/React-Conditional-Rendering...hs/React-Advanced-State?expand=1).
* Read more about [reducers in JavaScript](https://www.robinwieruch.de/javascript-reducer).
* Read more about reducers and useReducer in React ([0](https://www.robinwieruch.de/react-usereducer-hook), [1](https://reactjs.org/docs/hooks-reference.html#usereducer)).

## React Impossible States

Perhaps you've noticed a disconnect between the single states in the App component, which seem to belong together because of the `useState` hooks. Technically, all the states related to the asynchronous data belong together, which doesn't only include the stories as actual data, but also their loading and error states.

There is nothing wrong with multiple `useState` hooks in one React component. Be wary once you see multiple state updater functions in a row, however. These conditional states can lead to **impossible states**, and undesired behavior in the UI. Try changing your pseudo data fetching function to the following to simulate the error handling:

{title="src/App.js",lang="javascript"}
~~~~~~~
const getAsyncStories = () =>
  new Promise((resolve, reject) => setTimeout(reject, 2000));
~~~~~~~

The impossible state happens when an error occurs for the asynchronous data. The state for the error is set, but the state for the loading indicator isn't revoked. In the UI, this would lead to an infinite loading indicator and an error message, though it may be better to show the error message only and hide the loading indicator. Impossible states are not easy to spot, which makes them infamous for causing bugs in the UI.

Fortunately, we can improve our chances by moving states that belong together from multiple `useState` and `useReducer` hooks into a single `useReducer` hook. Take the following `useState` hooks:

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

  const [stories, dispatchStories] = React.useReducer(
    storiesReducer,
    []
  );
  const [isLoading, setIsLoading] = React.useState(false);
  const [isError, setIsError] = React.useState(false);

  ...
};
~~~~~~~

Merge them into one `useReducer` hook for a unified state management and a more complex state object:

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

  const [stories, dispatchStories] = React.useReducer(
    storiesReducer,
# leanpub-start-insert
    { data: [], isLoading: false, isError: false }
# leanpub-end-insert
  );

  ...
};
~~~~~~~

Everything related to asynchronous data fetching must use the new dispatch function for state transitions:

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

  const [stories, dispatchStories] = React.useReducer(
    storiesReducer,
    { data: [], isLoading: false, isError: false }
  );

  React.useEffect(() => {
# leanpub-start-insert
    dispatchStories({ type: 'STORIES_FETCH_INIT' });
# leanpub-end-insert

    getAsyncStories()
      .then(result => {
        dispatchStories({
# leanpub-start-insert
          type: 'STORIES_FETCH_SUCCESS',
# leanpub-end-insert
          payload: result.data.stories,
        });
      })
      .catch(() =>
# leanpub-start-insert
        dispatchStories({ type: 'STORIES_FETCH_FAILURE' })
# leanpub-end-insert
      );
  }, []);

  ...
};
~~~~~~~

Since we introduced new types for state transitions, we must handle them in the `storiesReducer` reducer function:

{title="src/App.js",lang="javascript"}
~~~~~~~
const storiesReducer = (state, action) => {
  switch (action.type) {
# leanpub-start-insert
    case 'STORIES_FETCH_INIT':
      return {
        ...state,
        isLoading: true,
        isError: false,
      };
    case 'STORIES_FETCH_SUCCESS':
      return {
        ...state,
        isLoading: false,
        isError: false,
        data: action.payload,
      };
    case 'STORIES_FETCH_FAILURE':
      return {
        ...state,
        isLoading: false,
        isError: true,
      };
    case 'REMOVE_STORY':
      return {
        ...state,
        data: state.data.filter(
          story => action.payload.objectID !== story.objectID
        ),
      };
# leanpub-end-insert
    default:
      throw new Error();
  }
};
~~~~~~~

For every state transition, we return a *new state* object which contains all the key/value pairs from the *current state* object (via JavaScript's spread operator) and the new overwriting properties. For instance, `STORIES_FETCH_FAILURE` resets the `isLoading`, but sets the `isError` boolean flags yet keeps all the other state instact (e.g. `stories`). That's how we get around the bug introduced earlier, since an error should remove the loading state.

Observe how the `REMOVE_STORY` action changed as well. It operates on the `state.data` , not longer just the plain `state`. The state is a complex object with data, loading and error states rather than just a list of stories. This has to be solved in the remaining code too:

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

  const [stories, dispatchStories] = React.useReducer(
    storiesReducer,
    { data: [], isLoading: false, isError: false }
  );

  ...

# leanpub-start-insert
  const searchedStories = stories.data.filter(story =>
# leanpub-end-insert
    story.title.toLowerCase().includes(searchTerm.toLowerCase())
  );

  return (
    <div>
      ...

# leanpub-start-insert
      {stories.isError && <p>Something went wrong ...</p>}
# leanpub-end-insert

# leanpub-start-insert
      {stories.isLoading ? (
# leanpub-end-insert
        <p>Loading ...</p>
      ) : (
        <List
          list={searchedStories}
          onRemoveItem={handleRemoveStory}
        />
      )}
    </div>
  );
};
~~~~~~~

Try to use the erroneous data fetching function again and check whether everything works as expected now:

{title="src/App.js",lang="javascript"}
~~~~~~~
const getAsyncStories = () =>
  new Promise((resolve, reject) => setTimeout(reject, 2000));
~~~~~~~

We moved from unreliable state transitions with multiple `useState` hooks to predictable state transitions with React's useReducer Hook. The state object managed by the reducer encapsulates everything related to the stories, including loading and error state, but also implementation details like removing a story from the list of stories. We didn't get fully rid of impossible states, because it's still possible to leave out a crucial boolean flag like before, but we moved one step closer towards more predictable state management.

### Exercises:

* Confirm your [source code for the last section](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/React-Impossible-States).
  * Confirm the [changes from the last section](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/React-Advanced-State...hs/React-Impossible-States?expand=1).
* Read over the previously linked tutorials about reducers in JavaScript and React.
* Read more about [when to use useState or useReducer in React](https://www.robinwieruch.de/react-usereducer-vs-usestate).

## Data Fetching with React

We are currently fetching data, but it's still pseudo data coming from a promise we set up ourselves. The lessons up to now about asynchronous React and advanced state management were preparing us to fetch data from a real third-party API. We will use the reliable and informative [Hacker News API](https://hn.algolia.com/api) to request popular tech stories.

Instead of using the `initialStories` array and `getAsyncStories` function (you can remove these), we will fetch the data directly from the API:

{title="src/App.js",lang="javascript"}
~~~~~~~
// A
# leanpub-start-insert
const API_ENDPOINT = 'https://hn.algolia.com/api/v1/search?query=';
# leanpub-end-insert

const App = () => {
  ...

  React.useEffect(() => {
    dispatchStories({ type: 'STORIES_FETCH_INIT' });

# leanpub-start-insert
    fetch(`${API_ENDPOINT}react`) // B
      .then(response => response.json()) // C
# leanpub-end-insert
      .then(result => {
        dispatchStories({
          type: 'STORIES_FETCH_SUCCESS',
# leanpub-start-insert
          payload: result.hits, // D
# leanpub-end-insert
        });
      })
      .catch(() =>
        dispatchStories({ type: 'STORIES_FETCH_FAILURE' })
      );
  }, []);

  ...
};
~~~~~~~

First, the `API_ENDPOINT` (A) is used to fetch popular tech stories for a certain query (a search topic). In this case, we fetch stories about React (B). Second, the native browser's [fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) is used to make this request (B). For the fetch API, the response needs to be translated into JSON (C). Finally, the returned result follows a different data structure (D), which we send as payload to our component's state.

In the previous code example we used [JavaScript's Template Literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals) for a string interpolation. When this feature wasn't available in JavaScript, we'd have used the + operator on strings instead:

{title="Code Playground",lang="javascript"}
~~~~~~~
const greeting = 'Hello';

// + operator
const welcome = greeting + ' React';
console.log(welcome);
// Hello React

// template literals
const anotherWelcome = `${greeting} React`;
console.log(anotherWelcome);
// Hello React
~~~~~~~

Check your browser to see stories related to the initial query fetched from the Hacker News API. Since we used the same data structure for a story for the sample stories, we didn't need to change anything, and it's still possible to filter the stories after fetching them with the search feature. We will change this behavior in one of the next sections. For the App component, there wasn't much data fetching to implement here, though it's all part of learning how to manage asynchronous data as state in React.

### Exercises:

* Confirm your [source code for the last section](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/Data-Fetching-with-React).
  * Confirm the [changes from the last section](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/React-Impossible-States...hs/Data-Fetching-with-React?expand=1).
* Read through [Hacker News](https://news.ycombinator.com/) and its [API](https://hn.algolia.com/api).
* Read more about [the browser native fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) for connecting to remote APIs.
* Read more about [JavaScript's Template Literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals).

## Data Re-Fetching in React

So far, the App component fetches a list of stories once with a predefined query ('react'). After that, users can search for stories on the client-side. Now we'll move this feature from client-side to server-side searching, using the actual `searchTerm` as a dynamic query for the API request.

First, remove`searchedStories`, because we will receive the stories searched from the API. Pass only the regular stories to the List component:

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

  return (
    <div>
      ...

      {stories.isLoading ? (
        <p>Loading ...</p>
      ) : (
# leanpub-start-insert
        <List list={stories.data} onRemoveItem={handleRemoveStory} />
# leanpub-end-insert
      )}
    </div>
  );
};
~~~~~~~

And second, instead of using a hardcoded search term like before, use the actual `searchTerm` from the component's state. If `searchTerm` is an empty string, do nothing:

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

  React.useEffect(() => {
# leanpub-start-insert
    if (searchTerm === '') return;
# leanpub-end-insert

    dispatchStories({ type: 'STORIES_FETCH_INIT' });

# leanpub-start-insert
    fetch(`${API_ENDPOINT}${searchTerm}`)
# leanpub-end-insert
      .then(response => response.json())
      .then(result => {
        dispatchStories({
          type: 'STORIES_FETCH_SUCCESS',
          payload: result.hits,
        });
      })
      .catch(() =>
        dispatchStories({ type: 'STORIES_FETCH_FAILURE' })
      );
  }, []);

  ...
};
~~~~~~~

The initial search respects the search term now, so we'll implement data refetching. If the `searchTerm` changes, run the side-effect for the data fetching again. If `searchTerm` is not present (e.g. null, empty string, undefined), do nothing (as a more generalized condition):

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

  React.useEffect(() => {
# leanpub-start-insert
    if (!searchTerm) return;
# leanpub-end-insert

    dispatchStories({ type: 'STORIES_FETCH_INIT' });

    fetch(`${API_ENDPOINT}${searchTerm}`)
      .then(response => response.json())
      .then(result => {
        dispatchStories({
          type: 'STORIES_FETCH_SUCCESS',
          payload: result.hits,
        });
      })
      .catch(() =>
        dispatchStories({ type: 'STORIES_FETCH_FAILURE' })
      );
# leanpub-start-insert
  }, [searchTerm]);
# leanpub-end-insert

  ...
};
~~~~~~~

We changed the feature from a client-side to server-side search. Instead of filtering a predefined list of stories on the client, the `searchTerm` is used to fetch a server-side filtered list. The server-side search happens for the initial data fetching, but also for data fetching if the `searchTerm` changes. The feature is fully server-side now.

Re-fetching data each time someone types into the input field isn't optimal, so we'll correct that soon. Because this implementation stresses the API, you might experience errors if you use requests too often.

### Exercises:

* Confirm your [source code for the last section](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/Data-Re-Fetching-in-React).
  * Confirm the [changes from the last section](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/Data-Fetching-with-React...hs/Data-Re-Fetching-in-React?expand=1).

## Memoized Handler in React (Advanced)

The previous sections have taught you about handlers, callback handlers, and inline handlers. Now we'll introduce a **memoized handler**, which can be applied on top of handlers and callback handlers. For the sake of learning, we will move all the data fetching logic into a standalone function outside the side-effect (A); wrap it into a `useCallback` hook (B); and then invoke it in the `useEffect` hook (C):

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

  // A
# leanpub-start-insert
  const handleFetchStories = React.useCallback(() => {
# leanpub-end-insert
    if (!searchTerm) return;

    dispatchStories({ type: 'STORIES_FETCH_INIT' });

    fetch(`${API_ENDPOINT}${searchTerm}`)
      .then(response => response.json())
      .then(result => {
        dispatchStories({
          type: 'STORIES_FETCH_SUCCESS',
          payload: result.hits,
        });
      })
      .catch(() =>
        dispatchStories({ type: 'STORIES_FETCH_FAILURE' })
      );
# leanpub-start-insert
  }, [searchTerm]); // E
# leanpub-end-insert

  React.useEffect(() => {
# leanpub-start-insert
    handleFetchStories(); // C
  }, [handleFetchStories]); // D
# leanpub-end-insert

  ...
};
~~~~~~~

The application behaves the same; only the implementation logic has been refactored. Instead of using the data fetching logic anonymously in a side-effect, we made it available as a function for the application.

Let's explore  why React's `useCallback` Hook is needed here. This hook creates a memoized function every time its dependency array (E) changes. As a result, the `useEffect` hook runs again (C) because it depends on the new function (D):

{title="Visualization",lang="javascript"}
~~~~~~~
1. change: searchTerm
2. implicit change: handleFetchStories
3. run: side-effect
~~~~~~~

If we didn't create a memoized function with React's `useCallback` Hook, a new `handleFetchStories` function would be created with each App component is rendered. The `handleFetchStories` function would be created each time, and would be executed in the `useEffect` hook to fetch data. The fetched data is then stored as state in the component. Because the state of the component changed, the component re-renders and creates a new `handleFetchStories` function. The side-effect would be triggered to fetch data, and we'd be stuck in an endless loop:

{title="Visualization",lang="javascript"}
~~~~~~~
1. define: handleFetchStories
2. run: side-effect
3. update: state
4. re-render: component
5. re-define: handleFetchStories
6. run: side-effect
...
~~~~~~~

The `useCallback` hook changes the function only when the search term changes. That's when we want to trigger a re-fetch of the data, because the input field has new input and we want to see the new data displayed in our list.

By moving the data fetching function outside the `useEffect` hook, it becomes reusable for other parts of the application. We won't use it just yet, but it is a way to understand the `useCallback` hook. Now the `useEffect` hook runs implicitly when the `searchTerm` changes, because the `handleFetchStories` is re-defined each time the `searchTerm` changes. Since the `useEffect` hook depends on the `handleFetchStories`, the side-effect for data fetching runs again.

### Exercises:

* Confirm your [source code for the last section](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/Memoized-Handler-in-React).
  * Confirm the [changes from the last section](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/Data-Re-Fetching-in-React...hs/Memoized-Handler-in-React?expand=1).
* Read more about [React's useCallback Hook](https://reactjs.org/docs/hooks-reference.html#usecallback).

## Explicit Data Fetching with React

Re-fetching all data each time someone types in the input field isn't optimal. Since we're using a third-party API to fetch the data, its internals are out of our reach. Eventually, we will incur [rate limiting](https://en.wikipedia.org/wiki/Rate_limiting), which returns an error instead of data.

To solve this problem, change the implementation details from implicit to explicit data (re-)fetching. In other words, the application will refetch data only if someone clicks a confirmation button. First, add a button element for the confirmation to the JSX:

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

  return (
    <div>
      <h1>My Hacker Stories</h1>

      <InputWithLabel
        id="search"
        value={searchTerm}
        isFocused
# leanpub-start-insert
        onInputChange={handleSearchInput}
# leanpub-end-insert
      >
        <strong>Search:</strong>
      </InputWithLabel>

# leanpub-start-insert
      <button
        type="button"
        disabled={!searchTerm}
        onClick={handleSearchSubmit}
      >
        Submit
      </button>
# leanpub-end-insert

      ...
    </div>
  );
};
~~~~~~~

Second, the handler, input, and button handler receive implementation logic to update the component's state. The input field handler still updates the `searchTerm`; the button handler sets the `url` derived from the *current* `searchTerm` and the static API URL as a new state:

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  const [searchTerm, setSearchTerm] = useSemiPersistentState(
    'search',
    'React'
  );

# leanpub-start-insert
  const [url, setUrl] = React.useState(
    `${API_ENDPOINT}${searchTerm}`
  );
# leanpub-end-insert

  ...

# leanpub-start-insert
  const handleSearchInput = event => {
# leanpub-end-insert
    setSearchTerm(event.target.value);
  };

# leanpub-start-insert
  const handleSearchSubmit = () => {
    setUrl(`${API_ENDPOINT}${searchTerm}`);
  };
# leanpub-end-insert

  ...
};
~~~~~~~

Third, instead of running the data fetching side-effect on every `searchTerm` change -- which would happen each time the input field's value changes -- the `url` is used. The `url` is set explicitly by the user when the search is confirmed via our new button:

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

  const handleFetchStories = React.useCallback(() => {
    dispatchStories({ type: 'STORIES_FETCH_INIT' });

# leanpub-start-insert
    fetch(url)
# leanpub-end-insert
      .then(response => response.json())
      .then(result => {
        dispatchStories({
          type: 'STORIES_FETCH_SUCCESS',
          payload: result.hits,
        });
      })
      .catch(() =>
        dispatchStories({ type: 'STORIES_FETCH_FAILURE' })
      );
# leanpub-start-insert
  }, [url]);
# leanpub-end-insert

  React.useEffect(() => {
    handleFetchStories();
  }, [handleFetchStories]);

  ...
};
~~~~~~~

Before the `searchTerm` was used for two cases: updating the input field's state and activating the side-effect for fetching data. Too many responsibilities one may would have said. Now it's only used for the former. A second state called `url` got introduced for triggering the side-effect for fetching data which only happens when a user clicks the confirmation button.

### Exercises:

* Confirm your [source code for the last section](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/Explicit-Data-Fetching-with-React).
  * Confirm the [changes from the last section](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/Memoized-Handler-in-React...hs/Explicit-Data-Fetching-with-React?expand=1).
* Why is `useState` instead of `useSemiPersistentState` used for the `url` state management?
* Why is there no check for an empty `searchTerm` in the `handleFetchStories` function anymore?

## Third-Party Libraries in React

We previously introduced the native fetch API to complete requests to the Hacker News API, which the browser provides. Not all browsers support this, however, especially the older ones. Also, once you start testing your application in a [headless browser environment](https://en.wikipedia.org/wiki/Headless_browser), issues can arise with the fetch API. There are a couple of ways to make fetch work in older browsers ([polyfills](https://en.wikipedia.org/wiki/Polyfill_(programming))) and in tests (isomorphic fetch), but these concepts are a bit off-task for the purpose of this learning experience.

One alternative is to substitute the native fetch API with a stable library like [axios](https://github.com/axios/axios), which performs asynchronous requests to remote APIs. In this section, we will discover how to substitute a library--a native API of the browser in this case--with another library from the npm registry. First, install axios on the command line:

{title="Command Line",lang="text"}
~~~~~~~
npm install axios
~~~~~~~

Second, import axios in your App component's file:

{title="src/App.js",lang="javascript"}
~~~~~~~
import React from 'react';
# leanpub-start-insert
import axios from 'axios';
# leanpub-end-insert

...
~~~~~~~

You can use `axios` instead of `fetch`, and its usage looks almost identical to the native fetch API. It takes the URL as an argument and returns a promise. You don't have to transform the returned response to JSON anymore, since axios wraps the result into a data object in JavaScript. Just make sure to adapt your code to the returned data structure:

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

  const handleFetchStories = React.useCallback(() => {
    dispatchStories({ type: 'STORIES_FETCH_INIT' });

# leanpub-start-insert
    axios
      .get(url)
# leanpub-end-insert
      .then(result => {
        dispatchStories({
          type: 'STORIES_FETCH_SUCCESS',
# leanpub-start-insert
          payload: result.data.hits,
# leanpub-end-insert
        });
      })
      .catch(() =>
        dispatchStories({ type: 'STORIES_FETCH_FAILURE' })
      );
  }, [url]);

  ...
};
~~~~~~~

In this code, we call axios `axios.get()` for an explicit [HTTP GET request](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/GET), which is the same HTTP method we used by default with the browser's native fetch API. You can use other HTTP methods such as HTTP POST with `axios.post()`as well.

We can see with these examples that axios is a powerful library for performing requests to remote APIs. I recommend over the native fetch API when requests become complex, working with older browser, or for testing.

### Exercises:

* Confirm your [source code for the last section](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/Third-Party-Libraries-in-React).
  * Confirm the [changes from the last section](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/Explicit-Data-Fetching-with-React...hs/Third-Party-Libraries-in-React?expand=1).
* Read more about [popular libraries in React](https://www.robinwieruch.de/react-libraries).
* Read more about [why frameworks matter](https://www.robinwieruch.de/why-frameworks-matter).
* Read more about [axios](https://github.com/axios/axios).

## Async/Await in React (Advanced)

You'll work with asynchronous data often in React, so it's good to know alternative syntax for handling promises: async/await. The following refactoring of the `handleFetchStories` function without error handling shows how:

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

# leanpub-start-insert
  const handleFetchStories = React.useCallback(async () => {
# leanpub-end-insert
    dispatchStories({ type: 'STORIES_FETCH_INIT' });

# leanpub-start-insert
    const result = await axios.get(url);
# leanpub-end-insert

# leanpub-start-insert
    dispatchStories({
      type: 'STORIES_FETCH_SUCCESS',
      payload: result.data.hits,
    });
# leanpub-end-insert
  }, [url]);

  ...
};
~~~~~~~

To use async/await, our function requires the `async` keyword. Once you start using the `await` keyword, everything reads like synchronous code. Actions after the `await` keyword are not executed until promise resolves, meaning the code will wait.

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

  const handleFetchStories = React.useCallback(async () => {
    dispatchStories({ type: 'STORIES_FETCH_INIT' });

# leanpub-start-insert
    try {
# leanpub-end-insert
      const result = await axios.get(url);

      dispatchStories({
        type: 'STORIES_FETCH_SUCCESS',
        payload: result.data.hits,
      });
# leanpub-start-insert
    } catch {
      dispatchStories({ type: 'STORIES_FETCH_FAILURE' });
    }
# leanpub-end-insert
  }, [url]);

  ...
};
~~~~~~~

To include error handling as before, the `try` and `catch` blocks are there to help. If something goes wrong in the `try` block,  the code will jump into the `catch` block to handle the error. `then`/`catch` blocks and async/await with `try`/`catch` blocks are both valid for handling asynchronous data in JavaScript and React.

### Exercises:

* Confirm your [source code for the last section](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/Async-Await-in-React).
  * Confirm the [changes from the last section](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/Third-Party-Libraries-in-React...hs/Async-Await-in-React?expand=1).
* Read more about [data fetching in React](https://www.robinwieruch.de/react-hooks-fetch-data).
* Read more about [async/await in JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function).

## Forms in React

Earlier we introduced a new button to fetch data explicitly with a button click. We'll advance its use with a proper HTML form, which encapsulates the button and input field for the search term with its label.

Forms aren't much different in React's JSX than in HTML. We'll implement it in two refactoring steps with some HTML/JavaScript. First, wrap the input field and button into an HTML form element:

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

  return (
    <div>
      <h1>My Hacker Stories</h1>

# leanpub-start-insert
      <form onSubmit={handleSearchSubmit}>
# leanpub-end-insert
        <InputWithLabel
          id="search"
          value={searchTerm}
          isFocused
          onInputChange={handleSearchInput}
        >
          <strong>Search:</strong>
        </InputWithLabel>

# leanpub-start-insert
        <button type="submit" disabled={!searchTerm}>
# leanpub-end-insert
          Submit
        </button>
# leanpub-start-insert
      </form>
# leanpub-end-insert

      <hr />

      ...
    </div>
  );
};
~~~~~~~

Instead of passing the `handleSearchSubmit` handler to the button, it's used in the new form element. The button receives a new `type` attribute called `submit`, which indicates that the form element handles the click and not the button.

Since the handler is used for the form event, it executes `preventDefault` in React's synthetic event. This prevents the HTML form's native behavior, which leads to a browser reload.

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

# leanpub-start-insert
  const handleSearchSubmit = event => {
# leanpub-end-insert
    setUrl(`${API_ENDPOINT}${searchTerm}`);

# leanpub-start-insert
    event.preventDefault();
# leanpub-end-insert
  };

  ...
};
~~~~~~~

Now we can execute the search feature with the keyboard's `Enter` key. In the next two steps, we will only separate the component into its standalone SearchForm component:

{title="src/App.js",lang="javascript"}
~~~~~~~
# leanpub-start-insert
const SearchForm = ({
  searchTerm,
  onSearchInput,
  onSearchSubmit,
}) => (
  <form onSubmit={onSearchSubmit}>
    <InputWithLabel
      id="search"
      value={searchTerm}
      isFocused
      onInputChange={onSearchInput}
    >
      <strong>Search:</strong>
    </InputWithLabel>

    <button type="submit" disabled={!searchTerm}>
      Submit
    </button>
  </form>
);
# leanpub-end-insert
~~~~~~~

The new component is used by the App component. The App component still manages the state for the form, because the state is used in the App component to fetch data passed as props (`stories.data`) to the List component:

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
  ...

  return (
    <div>
      <h1>My Hacker Stories</h1>

# leanpub-start-insert
      <SearchForm
        searchTerm={searchTerm}
        onSearchInput={handleSearchInput}
        onSearchSubmit={handleSearchSubmit}
      />
# leanpub-end-insert

      <hr />

      {stories.isError && <p>Something went wrong ...</p>}

      {stories.isLoading ? (
        <p>Loading ...</p>
      ) : (
        <List list={stories.data} onRemoveItem={handleRemoveStory} />
      )}
    </div>
  );
};
~~~~~~~

Forms aren't much different in React than HTML. When we have input fields and a button to submit data from them, we can give our HTML more structure by wrapping it into a form element with a `onSubmit` handler. The button that executes the submission needs only the "submit" `type`.

### Exercises:

* Confirm your [source code for the last section](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/Forms-in-React).
  * Confirm the [changes from the last section](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/Async-Await-in-React...hs/Forms-in-React?expand=1).
* Try the code without `preventDefault`.
* Read more about [preventDefault for Events in React](https://www.robinwieruch.de/react-preventdefault).
* Read more about [React Component Composition](https://www.robinwieruch.de/react-component-composition).