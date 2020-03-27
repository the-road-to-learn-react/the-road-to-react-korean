## 준비사항

이 책을 따라가려면 웹 개발의 기본, 즉 HTML, CSS, 자바스크립트를 사용하는 방법을 숙지해야 합니다. 또한 [APIs](https://www.robinwieruch.de/what-is-an-api-javascript/)를 이해한다면 도움이 될 것입니다.

### 코드 에디터와 터미널

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

코드 에디터에서 애플리케이션을 열어 봅시다. Visual Studio Code의 경우, 터미널에 `code .`를 입력하면 됩니다. *create-react-app*의 버전에 따라 조금씩 다를 수 있으나, 일반적으로는 디렉터리에 아래와 같은 구조가 보일 겁니다.

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

