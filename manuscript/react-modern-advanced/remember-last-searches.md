## 최근 검색어 저장

**과제:** API 요청을 할 수 있도록 최근 검색어 5개를 저장하고 검색어간 쉽게 이동할 수 있는 버튼을 추가합니다. 버튼을 클릭하면 검색어에 맞는 책 검색 결과를 다시 요청해 받아올 수 있도록 합니다.

**힌트 보기**

- 최근 검색어 저장 기능을 위해 새로운 상태값을 추가하지 마세요. `url` 상태값과 `setUrl` 상태값 업데이트 함수를 재활용해 검색 결과를 불러오는 API 요청을 할 수 있습니다. `urls`에 여러 상태값을 추가하고, 이 때 `setUrls` 함수를 사용합니다. `urls`에 가장 마지막으로 추가된 URL로 데이터를 불러오고 `urls`에 가장 마지막으로 추가된 5개의 URL을 버튼으로 보여줍니다.

먼저 상태값 `url`을 `urls`로, 상태값 업데이트 함수인 `setUrl`을 `setUrls`로 모두 고칩니다. `url` 문자열을 초기 상태값으로 설정하는 대신에 `url` 문자열이 유일한 요소로 들어간 배열을 초기 상태값으로 설정해줍니다.

{title="src/App.js",lang="javascript"}

```
const App = () => {
  ...

# leanpub-start-insert
  const [urls, setUrls] = React.useState([
# leanpub-end-insert
    `${API_ENDPOINT}${searchTerm}`,
# leanpub-start-insert
  ]);
# leanpub-end-insert

  ...
};
```

둘째로, 데이터를 불러올 때 현재 `url` 상태값 대신 `urls` 배열의 마지막 요소 값을 활용합니다. 만약 또 다른 `url`이 `urls` 배열에 추가되면, 이 추가된 마지막 `url` 상태값을 활용합니다.

{title="src/App.js",lang="javascript"}

```
const App = () => {

  ...

  const handleFetchStories = React.useCallback(async () => {
    dispatchStories({ type: 'STORIES_FETCH_INIT' });

    try {
# leanpub-start-insert
      const lastUrl = urls[urls.length - 1];
      const result = await axios.get(lastUrl);
# leanpub-end-insert

      dispatchStories({
        type: 'STORIES_FETCH_SUCCESS',
        payload: result.data.hits,
      });
    } catch {
      dispatchStories({ type: 'STORIES_FETCH_FAILURE' });
    }
# leanpub-start-insert
  }, [urls]);
# leanpub-end-insert

  ...
};
```

셋째로, 상태값 업데이트 함수에서 `url`을 문자열로 저장하는 대신 새 `url`을 기존의 `urls` 배열과 합치도록 합니다.

{title="src/App.js",lang="javascript"}

```
const App = () => {
  ...

  const handleSearchSubmit = event => {
# leanpub-start-insert
    const url = `${API_ENDPOINT}${searchTerm}`;
    setUrls(urls.concat(url));
# leanpub-end-insert

    event.preventDefault();
  };

  ...
};
```

검색할 때마다 새로운 URL이 `urls` 상태에 저장됩니다. 다음으로 최근 검색한 각 검색어의 URL로 연결되는 버튼 5개를 만듭니다. 이 버튼들에 적용할 공통 핸들러 함수를 만들고, 각 버튼에 각각의 `url` 값을 인자로 넘깁니다. 이렇게 하면 각 url에 맞는 인라인 핸들러 함수로 활용할 수 있습니다.

{title="src/App.js",lang="javascript"}

```
# leanpub-start-insert
const getLastSearches = urls => urls.slice(-5);
# leanpub-end-insert

...

const App = () => {
  ...

# leanpub-start-insert
  const handleLastSearch = url => {
    // do something
  };
# leanpub-end-insert

# leanpub-start-insert
  const lastSearches = getLastSearches(urls);
# leanpub-end-insert

  return (
    <div>
      <h1>My Hacker Stories</h1>

      <SearchForm ... />

# leanpub-start-insert
      {lastSearches.map(url => (
        <button
          key={url}
          type="button"
          onClick={() => handleLastSearch(url)}
        >
          {url}
        </button>
      ))}
# leanpub-end-insert

      ...
    </div>
  );
};
```

다음으로, 마지막으로 검색한 URL의 전체 주소가 아니라 검색어만 버튼에 노출될 수 있도록 API의 엔드포인트 주소를 빈 문자열로 바꿉니다.

{title="src/App.js",lang="javascript"}

```
# leanpub-start-insert
const extractSearchTerm = url => url.replace(API_ENDPOINT, '');
# leanpub-end-insert

# leanpub-start-insert
const getLastSearches = urls =>
  urls.slice(-5).map(url => extractSearchTerm(url));
# leanpub-end-insert

...

const App = () => {
  ...

  const lastSearches = getLastSearches(urls);

  return (
    <div>
      ...

      {lastSearches.map(searchTerm => (
        <button
# leanpub-start-insert
          key={searchTerm}
# leanpub-end-insert
          type="button"
# leanpub-start-insert
          onClick={() => handleLastSearch(searchTerm)}
# leanpub-end-insert
        >
# leanpub-start-insert
          {searchTerm}
# leanpub-end-insert
        </button>
      ))}

      ...
    </div>
  );
};
```

이제 `getLastSearches` 함수는 전체 URL 대신 검색어만 반환합니다. 실제 `검색어`가 `url` 대신 인라인 핸들러 함수의 인자로 들어갑니다. `getLastSearches` 함수 안에서 map 메서드를 사용해 `urls` 배열을 돌면서 각 `url`의 검색어를 추출합니다. 이를 좀 더 간결하게 만들면 아래와 같습니다.

{title="src/App.js",lang="javascript"}

```
const getLastSearches = urls =>
# leanpub-start-insert
  urls.slice(-5).map(extractSearchTerm);
# leanpub-end-insert
```

이제 새로운 핸들러 함수를 활용해 모든 버튼에 기능을 추가합니다. 버튼 하나를 클릭하면 새로 검색되어야 합니다. 우리는 지금까지 `urls` 상태값으로 데이터를 불러오고, 이 때 상태값에 가장 마지막으로 추가된 URL이 사용되도록 만들었습니다. 새 `url`이 추가되면 이 값으로 새로운 검색 요청을 할 수 있도록 `urls` 배열에 추가합니다.

{title="src/App.js",lang="javascript"}

```
const App = () => {
  ...

# leanpub-start-insert
  const handleLastSearch = searchTerm => {
    const url = `${API_ENDPOINT}${searchTerm}`;
    setUrls(urls.concat(url));
  };
# leanpub-end-insert

  ...
};
```

방금 만든 핸들러 함수의 구현 로직을 `handleSearchSubmit` 함수의 로직과 비교해보면 공통적으로 수행하고 있는 기능을 찾아볼 수 있습니다. 이 공통적인 기능을 새로운 유틸리티 함수로 따로 만든 뒤 핸들러 함수에서 활용하도록 합니다.

{title="src/App.js",lang="javascript"}

```
# leanpub-start-insert
const getUrl = searchTerm => `${API_ENDPOINT}${searchTerm}`;
# leanpub-end-insert

...

const App = () => {
  ...

  const handleSearchSubmit = event => {
# leanpub-start-insert
    handleSearch(searchTerm);
# leanpub-end-insert

    event.preventDefault();
  };

  const handleLastSearch = searchTerm => {
# leanpub-start-insert
    handleSearch(searchTerm);
# leanpub-end-insert
  };

# leanpub-start-insert
  const handleSearch = searchTerm => {
    const url = getUrl(searchTerm);
    setUrls(urls.concat(url));
  };
# leanpub-end-insert

  ...
};
```

따로 만든 유틸리티 함수는 App 컴포넌트의 다른 곳에서 활용될 수 있습니다. 두 곳에서 공통으로 쓰이는 특정 기능을 별도로 분리했을 때, 해당 기능을 또 다른 곳에서 활용할 수 있을지 항상 생각해보는 것이 좋습니다.

{title="src/App.js",lang="javascript"}

```
const App = () => {
  ...

  // important: still wraps the returned value in []
# leanpub-start-insert
  const [urls, setUrls] = React.useState([getUrl(searchTerm)]);
# leanpub-end-insert

  ...
};
```

지금까지 만든 코드로 원하는 검색 기능이 동작하지만, 동일한 검색어가 두 번 이상 검색되면 문제가 생깁니다. `검색어`가 각 버튼을 구별하는 key 속성으로 사용되고 있기 때문입니다. 검색어 배열에 map 메서드를 실행할 때 검색어와 index를 합친 값이 key 속성으로 들어갈 수 있도록 합니다.

{title="src/App.js",lang="javascript"}

```
const App = () => {
  ...

  return (
    <div>
      ...

# leanpub-start-insert
      {lastSearches.map((searchTerm, index) => (
# leanpub-end-insert
        <button
# leanpub-start-insert
          key={searchTerm + index}
# leanpub-end-insert
          type="button"
          onClick={() => handleLastSearch(searchTerm)}
        >
          {searchTerm}
        </button>
      ))}

      ...
    </div>
  );
};
```

이것도 완벽한 해결 방법은 아닙니다. `index`는 변할 수 있는 값이기 때문입니다(특히 배열에 아이템을 추가할 때 그렇습니다.). 하지만 지금과 같은 상황에서 문제가 생기지는 않습니다. 기능이 동작하긴 하지만 아래 작업을 통해 UX를 개선해보는 것도 좋은 방법입니다.

**추가 과제:**

- (1) 버튼에 현재 검색어를 보여주지 말고, 최근 검색어 5개만 보여줍니다. 힌트: `getLastSearches` 함수를 활용합니다.
- (2) 중복 검색어는 보여주지 않습니다. "React"를 두 번 검색한다고 두 개의 다른 버튼을 만들지 않습니다. 힌트: `getLastSearches` 함수를 활용합니다.
- (3) 버튼 하나를 클릭했을 때 SearchForm 컴포넌트의 검색어 입력창에 버튼에 해당하는 검색어가 나오도록 합니다.

5개의 버튼은 `getLastSearches` 함수로 만들어집니다. 이 함수는 `urls` 배열을 인자로 받아 가장 마지막으로 추가된 5개의 값을 반환합니다. 이 유틸리티 함수를 수정해서 5개가 아닌 6개의 값을 반환하되 가장 마지막에 추가된 값은 삭제되도록 합니다. 이렇게 하면 5개의 _이전_ 검색어들만 버튼에 나타납니다.

{title="src/App.js",lang="javascript"}

```
const getLastSearches = urls =>
  urls
# leanpub-start-insert
    .slice(-6)
    .slice(0, -1)
# leanpub-end-insert
    .map(extractSearchTerm);
```

동일한 검색어를 연속으로 검색했을 때 중복되는 버튼들이 만들어지는데, 원하는 동작은 아닐 것입니다. 동일한 검색어는 하나의 그룹으로 묶어 하나의 버튼으로만 보이도록 만들어 줍시다. 이 작업도 유틸리티 함수에서 처리하도록 합니다. 배열을 5개의 이전 검색어로 분리해주기 전에 이전 검색어의 가장 마지막 값이 새로 들어온 검색어와 같다면 하나의 같은 값으로 처리되도록 합니다.

{title="src/App.js",lang="javascript"}

```
const getLastSearches = urls =>
  urls
# leanpub-start-insert
    .reduce((result, url, index) => {
      const searchTerm = extractSearchTerm(url);

      if (index === 0) {
        return result.concat(searchTerm);
      }

      const previousSearchTerm = result[result.length - 1];

      if (searchTerm === previousSearchTerm) {
        return result;
      } else {
        return result.concat(searchTerm);
      }
    }, [])
# leanpub-end-insert
    .slice(-6)
    .slice(0, -1);
```

reduce 메서드는 처음에 빈 배열인 result를 만들고, urls 배열을 처음 한 바퀴 돌면서 url에서 분리한 `검색어`들을 result 배열에 추가합니다. 이 때 추출된 `검색어` 들은 이전 검색어들과 비교되고, 만약 이전 검색어와 현재 검색어가 다른 경우에만 result 배열에 `검색어`가 추가됩니다. 만약 검색어들이 똑같다면 아무것도 추가하지 않은 채 result를 반환합니다.

마지막으로 최근 검색어 검색 버튼을 클릭하면 SearchForm의 입력창에 새로운 `검색어`가 추가되도록 합니다. SearchForm 컴포넌트를 위한 특정 값을 추출하기 위해 상태값 업데이트 함수를 활용합니다.

{title="src/App.js",lang="javascript"}

```
const App = () => {
  ...

  const handleLastSearch = searchTerm => {
# leanpub-start-insert
    setSearchTerm(searchTerm);
# leanpub-end-insert

    handleSearch(searchTerm);
  };

  ...
};
```

끝으로, 이 장에서 만든 기능들을 하나의 독립적인 컴포넌트으로 만들어 App 컴포넌트가 가볍게 유지될 수 있도록 합니다.

{title="src/App.js",lang="javascript"}

```
const App = () => {
  ...

  const lastSearches = getLastSearches(urls);

  return (
    <div>
      ...

# leanpub-start-insert
      <LastSearches
        lastSearches={lastSearches}
        onLastSearch={handleLastSearch}
      />
# leanpub-end-insert

      ...
    </div>
  );
};

# leanpub-start-insert
const LastSearches = ({ lastSearches, onLastSearch }) => (
  <>
    {lastSearches.map((searchTerm, index) => (
      <button
        key={searchTerm + index}
        type="button"
        onClick={() => onLastSearch(searchTerm)}
      >
        {searchTerm}
      </button>
    ))}
  </>
);
# leanpub-end-insert
```

만들기 쉽지 않은 기능이었습니다. 다양한 React 기초 지식은 물론 자바스크립트 지식이 요구되는 작업이었습니다. 혼자 설명을 읽고 기능을 만들면서 어려움을 느끼지 않았다면 훌륭한 실력을 갖춘 것입니다. 만약 어려움을 느꼈더라도 걱정할 필요 없습니다. 이 문제를 다른 방식으로 해결할 수도 있고, 어쩌면 그 방법이 제가 설명드린 방법보다 더 단순할지도 모릅니다.

### 실습하기

- [마지막 장의 소스 코드](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/Remember-Last-Searches)를 확인합니다.
  - [마지막 장에서 변경된 코드](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/Reverse-Sort...hs/Remember-Last-Searches?expand=1)를 확인합니다.
