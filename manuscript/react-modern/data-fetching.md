## 리액트에서 데이터 가져오기

현재 데이터는 실제 사용하는 데이터가 아니라 임시 데이터입니다. 이번 장에서는 외부 API에서 데이터를 가져올 때 필요한 비동기 리액트 및 고급 상태 관리에 대해 알아봅니다. 믿을만하고 유익한 [해커 뉴스 API](https://hn.algolia.com/api)를 사용하여 인기 있는 기술 관련 기사들을 가져와 봅시다.

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

먼저, `API_ENDPOINT` (A)는 특정 쿼리(검색 주제)에 대한 인기 있는 기술 관련 기사들을 가져오는 데에 사용됩니다. 이 경우 리액트 (B)에 대한 기사를 가져옵니다. 둘째, 네이티브 브라우저의 [fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)를 사용하여 요청을 보냅니다 (B). Fetch API의 경우 응답을 JSON으로 변환해야합니다 (C). 마지막으로 반환된 결괏값은 각각 다른 데이터 구조를 따르며 (D), 이들을 컴포넌트의 상태에 payload로 전달됩니다.

이전 코드에서 우리는 [자바스크립트 템플릿 리터럴](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals)로 문자 보간기능을 사용했습니다. 이 기능이 자바스크립트에 등장하기 전까지는 문자열에 + 연산자를 사용했습니다.

{title="Code Playground",lang="javascript"}

~~~~~~~
const greeting = 'Hello';

// + 연산자
const welcome = greeting + ' React';
console.log(welcome);
// Hello React

// 템플릿 리터럴
const anotherWelcome = `${greeting} React`;
console.log(anotherWelcome);
// Hello React
~~~~~~~

브라우저를 열어 해커 뉴스 API에서 가져온 초기 쿼리와 관련된 기사를 확인하세요. 샘플 기사와 똑같은 데이터 구조를 사용했으므로 아무것도 변경할 필요가 없습니다. 또한 검색 기능으로 기사들을 가져온 후 필터링을 할 수도 있습니다. 다음 장에서 이 기능을 구현해 볼 것입니다. App 컴포넌트의 경우, 데이터 가져오기를 구현하는 부분은 많지 않았으나, 리액트에서 비동기 데이터를 상태로 관리하는 방법에 필요한 개념을 모두 학습했습니다.

### 실습하기

* [지난 장에서 사용한 코드](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/Data-Fetching-with-React)를 확인하세요.
  * [지난 장에서 수정된 코드](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/React-Impossible-States...hs/Data-Fetching-with-React?expand=1)를 확인하세요.
* [해커 뉴스(Hacker News)](https://news.ycombinator.com/)에서 제공하는 [API](https://hn.algolia.com/api)에 대해 읽어보세요.
* 원격 API에 연결하기 위한 [네이티브 브라우저 fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)에 대해서도 알아보세요.
* [자바스크립트 템플릿 리터럴](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals)에 대해 읽어보세요.

