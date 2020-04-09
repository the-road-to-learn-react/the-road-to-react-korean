## 리액트의 서드 파티 라이브러리

이전에는 해커 뉴스 API 요청을 처리하기 위해 브라우저가 제공하는 기본 fetch API를 사용했습니다. 그러나 모든 브라우저, 특히 구형 브라우저는 이 기능을 지원하지 않습니다. 또한 [headless 브라우저 환경](https://en.wikipedia.org/wiki/Headless_browser)에서 애플리케이션 테스트를 시작하면 fetch API에서 문제가 생길 수 있습니다. 구형 브라우저에서 fetch를 사용할 수 있게 [폴리필(Polyfill)](https://en.wikipedia.org/wiki/Polyfill_(programming))을 추가하거나 클라이언트에 동시에 사용 가능한 isomorphic-fetch 등 라이브러리를 도입할 수 있습니다만, 이 개념은 본 학습 목표에서 조금 벗어난 부분입니다.

한 가지 대안으로는 기본 fetch API를 원격 API에 비동기 요청을 수행하는 [axios](https://github.com/axios/axios)처럼 안정적인 라이브러리로 대체하는 방법이 있습니다. 이번 장에서는 기존 웹 API 대신 npm 라이브러리인 axios를 사용합니다. 먼저 커맨드 라인에서 axios를 설치하세요.

{title="Command Line",lang="text"}
~~~~~~~
npm install axios
~~~~~~~

그 다음 App 컴포넌트 파일에서 axios를 불러옵니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
import React from 'react';
# leanpub-start-insert
import axios from 'axios';
# leanpub-end-insert

...
~~~~~~~

사용법은 기본 fetch API와 거의 동일하며, `fetch` 대신 `axios`를 사용합니다. axios는 인수로 URL을 취하고 프로미스(promise)를 반환합니다. axios는 자바스크립트 데이터 객체로 결과를 감싸므로 더는 반환된 응답을 JSON으로 바꿀 필요가 없습니다. 반환된 데이터 구조에 맞게 코드를 수정하세요.

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

이 코드에서는 명시적인 [HTTP GET 요청](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/GET)을 위해 axios의 `axios.get()`을 호출합니다. 브라우저 기본 fetch API를 이용해 기본적으로 사용한 것과 동일한 HTTP 메서드입니다. `axios.post()`와 함께 HTTP POST와 같은 다른 HTTP 메서드도 사용할 수 있습니다.

이 예제에서 axios는 원격 API 요청을 수행하는 강력한 라이브러리임을 알아보았습니다. 요청이 복잡해지거나 또는 구형 브라우저로 작업하거나 테스트할 때는 기본 fetch API를 사용하는 것이 좋습니다.

### 실습하기

* [마지막 장의 소스 코드](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/Third-Party-Libraries-in-React)를 확인하세요.
  * [마지막 장의 변경 사항](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/Explicit-Data-Fetching-with-React...hs/Third-Party-Libraries-in-React?expand=1)을 확인하세요.
* [리액트의 인기 라이브러리](https://www.robinwieruch.de/react-libraries)에 대해 자세히 알아보세요.
* [프레임워크가 중요한 이유](https://www.robinwieruch.de/why-frameworks-matter)에 대해 자세히 알아보세요.
* [axios](https://github.com/axios/axios)에 대해 자세히 알아보세요.