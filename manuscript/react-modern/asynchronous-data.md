## 리액트 비동기 데이터

애플리케이션에 두 가지 상호 작용이 있습니다. 목록을 검색하는 것과 목록에서 항목을 삭제하는 것입니다. 첫 번째는 목록에 적용된 상태(`searchTerm`)를 통한 유동적인 상호 작용입니다. 두 번째는 목록에서 항목을 되돌릴 수 없게 삭제하는 상호 작용입니다.

서드 파티 API로부터 데이터를 가져와서 표시하기 전에 컴포넌트를 렌더링해야 할 때가 있습니다. 이번에는 애플리케이션에서 이런 종류의 비동기 데이터를 다룹니다. 실제 애플리케이션에서는 실제 원격 API에서 비동기 데이터를 가져옵니다. 우선 간단하게 프로미스를 반환하는(요청이 성공하면 데이터를 반환하는) 함수로 시작합니다. 요청이 처리된 객체는 이전 스토리 목록을 가지고 있습니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const initialStories = [ ... ];

# leanpub-start-insert
const getAsyncStories = () =>
  Promise.resolve({ data: { stories: initialStories } });
# leanpub-end-insert
~~~~~~~

App 컴포넌트에서 `initialStories`를 사용하는 대신 초기 상태로 빈 배열을 사용하세요. 빈 목록에 스토리를 비동기적으로 가져오는 것을 실습하려고 합니다. 새로운 `useEffect` 훅에서 함수를 호출하고 반환된 프로미스를 처리하세요. 훅의 두 번째 인자에 사용된 빈 의존성 배열로 인해 컴포넌트가 처음 렌더링 될 때만 실행됩니다.

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

애플리케이션을 시작할 때 데이터를 비동기적으로 받아야 하지만 데이터가 바로 렌더링 되므로 동기적으로 받는 것처럼 보입니다. API에 대한 모든 네트워크 요청은 지연될 수 있기 때문에 약간 현실적인 지연을 발생 시켜 보겠습니다. 먼저 간단히 작성했던 프로미스 부분을 지우세요.

{title="src/App.js",lang="javascript"}
~~~~~~~
const getAsyncStories = () =>
# leanpub-start-insert
  new Promise(resolve =>
    resolve({ data: { stories: initialStories } })
  );
# leanpub-end-insert
~~~~~~~

그리고 몇 초 늦춰서 프로미스를 이행합니다.

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

애플리케이션을 다시 시작하면 목록이 지연되어 렌더링 됩니다. 스토리의 초기 상태는 빈 배열입니다. App 컴포넌트가 렌더링 되고 나서 부수적 효과로 훅이 한 번 실행되고 비동기 데이터를 가져옵니다. 프로미스 이행이 완료되고 컴포넌트의 상태에 데이터를 설정한 후, 컴포넌트는 다시 렌더링 되어 비동기적으로 로드된 스토리 목록을 표시합니다.

### 실습하기

* [마지막 장의 소스 코드](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/React-Asynchronous-Data)를 확인하세요.
  * [마지막 장의 변경 사항](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/Inline-Handler-in-JSX...hs/React-Asynchronous-Data?expand=1)을 확인하세요.
* [자바스크립트 프로미스](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)에 대해 자세히 알아보세요.