## 여러 페이지 데이터 받기

검색을 고도화하는 방법은 다양합니다. 해커 뉴스 API로 인기 기사를 검색하는 기능을 구현해 더 완성도 높고 기능적인 검색 엔진을 만들어 봅시다. [해커 뉴스 API](https://hn.algolia.com/api)의 데이터 구조를 자세히 살펴보면서 조회수 외 정보들을 어떻게 전달해주는지 확인해보세요.

구체적으로 살펴보면 여러 페이지로 분리된 목록을 반환한다는 걸 알 수 있습니다. 페이지 속성은 각 페이지의 목록을 받아올 때 사용되고, 첫 응답에서는 값이 `0`입니다. API로 다음 페이지 데이터를 요청할 때 동일한 검색어만 넘겨도 됩니다.

지금부터는 해커 뉴스의 데이터 구조에서 여러 페이지 데이터를 불러오기 위해 어떻게 구현해야 하는지에 대한 내용을 다룹니다. 만약 다른 애플리케이션에서 목록을 **여러 페이지로 처리**된 경우를 많이 봤다면 마음 속에 떠오르는 화면이 있을 것입니다. 1부터 10까지의 번호로 된 버튼이 일렬로 나란히 있고, 현재 선택된 페이지는 1-[3]-10과 같이 하이라이트 처리되었으며 이 중 한 버튼을 클릭하면 해당 버튼에 해당하는 하위 데이터들을 불러와 보여주겠죠.

하지만 우리는 이와는 다른 **무한 페이지** 기능을 구현할 것입니다. 버튼을 클릭했을 때 해당 페이지의 데이터 목록만 보여주는 게 아니라 _여러 페이지로 구성된 모든 데이터를 하나의 목록_ 으로 보여주되 _하나_ 의 버튼으로 다음 페이지 데이터를 받아올 것입니다. 추가되는 모든 _다음 페이지 목록_ 은 _기존 목록_ 끝에 합쳐지는 방식입니다.

**과제:** 목록의 첫 페이지만 불러오는 대신, 각 페이지의 데이터를 연속적으로 불러오며 확장시키는 기능을 구현합니다. 버튼을 클릭했을 때 무한하게 페이지를 불러올 수 있도록 만드세요.

**힌트 보기:**

- `API_ENDPOINT`에 불러올 페이지에 해당하는 인자를 추가합니다.
- 데이터를 불러온 뒤에 `result` 상태값에 `page` 값을 저장합니다.
- 검색할 때마다 데이터의 첫 페이지(`0`) 데이터를 요청해 불러옵니다.
- 새 HTML 버튼을 만들고 이 버튼을 누를 때마다 다음 페이지(`page + 1`) 데이터를 요청해 불러옵니다.

먼저, API 주소 변수에 문자를 추가해 다음 페이지 데이터를 요청할 때 사용합니다. 아래와 같이 하나의 API 주소 변수를 여러 변수로 분리합니다.

{title="src/App.js",lang="javascript"}

```
const API_ENDPOINT = 'https://hn.algolia.com/api/v1/search?query=';

const getUrl = searchTerm => `${API_ENDPOINT}${searchTerm}`;
```

분리된 API 주소 변수들을 파라미터와 함께 다시 조합해 사용합니다.

{title="src/App.js",lang="javascript"}

```
# leanpub-start-insert
const API_BASE = 'https://hn.algolia.com/api/v1';
const API_SEARCH = '/search';
const PARAM_SEARCH = 'query=';
# leanpub-end-insert

// careful: notice the ? in between
# leanpub-start-insert
const getUrl = searchTerm =>
  `${API_BASE}${API_SEARCH}?${PARAM_SEARCH}${searchTerm}`;
# leanpub-end-insert
```

다행히 API 엔드포인트를 매번 직접 만들 필요는 없습니다. `getUrl` 함수를 만들어 검색어 부분만 바뀌게 만들었기 때문입니다. 하지만 직접 만들어주어야 하는 때도 있습니다.

{title="src/App.js",lang="javascript"}

```
const extractSearchTerm = url => url.replace(API_ENDPOINT, '');
```

이번에 할 작업에서는 API 엔드포인트의 베이스 주소를 제거해주는 것만으로는 검색어를 추출하기 쉽지 않습니다. API 엔드포인트에 추가되는 파라미터가 많을 수록 URL은 점점 더 복잡해집니다. 아래의 X에서 Y와 같은 식으로 파라미터가 추가됩니다.

{title="src/App.js",lang="javascript"}

```
// X
https://hn.algolia.com/api/v1/search?query=react

// Y
https://hn.algolia.com/api/v1/search?query=react&page=0
```

이럴 땐 `?`와 `&` 사이에 있는 모든 문자열을 추출하여 검색어를 추출하는 방법이 더 좋습니다. `query`라는 파라미터가 `?` 바로 뒤에 나오고 `page`와 같은 다른 파라미터들은 그 뒤에 나오고 있다는 걸 확인해보세요.

{title="src/App.js",lang="javascript"}

```
# leanpub-start-insert
const extractSearchTerm = url =>
  url
    .substring(url.lastIndexOf('?') + 1, url.lastIndexOf('&'));
# leanpub-end-insert
```

key로 들어간 문자( `query=`) 역시 제거되어야 온전한 값(`searchTerm`)을 추출할 수 있습니다:

{title="src/App.js",lang="javascript"}

```
const extractSearchTerm = url =>
  url
    .substring(url.lastIndexOf('?') + 1, url.lastIndexOf('&'));
# leanpub-start-insert
    .replace(PARAM_SEARCH, '');
# leanpub-end-insert
```

검색어만 남을 때까지 필요없는 문자열을 계속 제거합니다.

{title="src/App.js",lang="javascript"}

```
// url
https://hn.algolia.com/api/v1/search?query=react&page=0

// url after  substring
query=react

// url after replace
react
```

해커 뉴스 API로부터 반환한 결과값으로 `page` 데이터를 전달받습니다.

{title="src/App.js",lang="javascript"}

```
const App = () => {
  ...

  const handleFetchStories = React.useCallback(async () => {
    dispatchStories({ type: 'STORIES_FETCH_INIT' });

    try {
      const lastUrl = urls[urls.length - 1];
      const result = await axios.get(lastUrl);

      dispatchStories({
        type: 'STORIES_FETCH_SUCCESS',
# leanpub-start-insert
        payload: {
          list: result.data.hits,
          page: result.data.page,
        },
# leanpub-end-insert
      });
    } catch {
      dispatchStories({ type: 'STORIES_FETCH_FAILURE' });
    }
  }, [urls]);

  ...
};
```

다음 페이지 데이터를 요청할 때 사용하기 위해 이 값을 store에 저장합니다.

{title="src/App.js",lang="javascript"}

```
const storiesReducer = (state, action) => {
  switch (action.type) {
    case 'STORIES_FETCH_INIT':
      ...
    case 'STORIES_FETCH_SUCCESS':
      return {
        ...state,
        isLoading: false,
        isError: false,
# leanpub-start-insert
        data: action.payload.list,
        page: action.payload.page,
# leanpub-end-insert
      };
    case 'STORIES_FETCH_FAILURE':
      ...
    case 'REMOVE_STORY':
      ...
    default:
      throw new Error();
  }
};

const App = () => {
  ...

  const [stories, dispatchStories] = React.useReducer(
    storiesReducer,
# leanpub-start-insert
    { data: [], page: 0, isLoading: false, isError: false }
# leanpub-end-insert
  );

  ...
};
```

새로운 `page` 파라미터를 API 엔드포인트에 추가합니다. URL에서 검색어를 추출할 때 만들었던 변수와 함수를 활용합니다.

{title="src/App.js",lang="javascript"}

```
const API_BASE = 'https://hn.algolia.com/api/v1';
const API_SEARCH = '/search';
const PARAM_SEARCH = 'query=';
# leanpub-start-insert
const PARAM_PAGE = 'page=';
# leanpub-end-insert

// careful: notice the ? and & in between
# leanpub-start-insert
const getUrl = (searchTerm, page) =>
  `${API_BASE}${API_SEARCH}?${PARAM_SEARCH}${searchTerm}&${PARAM_PAGE}${page}`;
# leanpub-end-insert
```

다음으로 `page`를 인자로 넣어 `getUrl` 함수를 실행합니다. 가장 첫 검색과 마지막 검색은 가장 첫 페이지(`0`)를 불러오기에 첫 페이지 숫자를 함수에 인자로 넘겨 첫 페이지 데이터를 불러옵니다.

{title="src/App.js",lang="javascript"}

```
const App = () => {
  ...

# leanpub-start-insert
  const [urls, setUrls] = React.useState([getUrl(searchTerm, 0)]);
# leanpub-end-insert

  ...

  const handleSearchSubmit = event => {
# leanpub-start-insert
    handleSearch(searchTerm, 0);
# leanpub-end-insert

    event.preventDefault();
  };

  const handleLastSearch = searchTerm => {
    setSearchTerm(searchTerm);

# leanpub-start-insert
    handleSearch(searchTerm, 0);
# leanpub-end-insert
  };

# leanpub-start-insert
  const handleSearch = (searchTerm, page) => {
    const url = getUrl(searchTerm, page);
# leanpub-end-insert
    setUrls(urls.concat(url));
  };

  ...
};
```

버튼을 클릭했을 때 다음 페이지 데이터를 불러오도록 새로운 핸들러의 `page` 인자에 숫자를 더해줍니다.

{title="src/App.js",lang="javascript"}

```
const App = () => {
  ...

# leanpub-start-insert
  const handleMore = () => {
    const lastUrl = urls[urls.length - 1];
    const searchTerm = extractSearchTerm(lastUrl);
    handleSearch(searchTerm, stories.page + 1);
  };
# leanpub-end-insert

  ...

  return (
    <div>
      ...

      {stories.isLoading ? (
        <p>Loading ...</p>
      ) : (
        <List list={stories.data} onRemoveItem={handleRemoveStory} />
      )}

# leanpub-start-insert
      <button type="button" onClick={handleMore}>
        More
      </button>
# leanpub-end-insert
    </div>
  );
};
```

동적으로 변하는 `page` 인자로 데이터를 불러오도록 구현했습니다. 가장 처음과 마지막 검색은 항상 첫 페이지 데이터를 불러오고 "더보기" 버튼은 다음 페이지 데이터를 불러옵니다. 하지만 이 기능에는 큰 버그가 있습니다. 새로 데이터를 불러왔을 때 이전 데이터에 추가되는 게 아니라 이전 데이터를 완전히 대체해버린다는 점입니다.

reducer에서 현재의 `data`가 새로운 `data`를 대체하도록 하지 말고, 여러 페이지의 목록이 합쳐지도록 만들어 이 문제를 해결합시다.

{title="src/App.js",lang="javascript"}

```
const storiesReducer = (state, action) => {
  switch (action.type) {
    case 'STORIES_FETCH_INIT':
      ...
    case 'STORIES_FETCH_SUCCESS':
      return {
        ...state,
        isLoading: false,
        isError: false,
# leanpub-start-insert
        data:
          action.payload.page === 0
            ? action.payload.list
            : state.data.concat(action.payload.list),
# leanpub-end-insert
        page: action.payload.page,
      };
    case 'STORIES_FETCH_FAILURE':
      ...
    case 'REMOVE_STORY':
      ...
    default:
      throw new Error();
  }
};
```

버튼을 새로 눌러 데이터를 불러올 때마다 목록이 길어집니다. 하지만 목록이 길어질 때 화면이 깜빡거리는 사용성 문제가 여전히 남아있습니다. 이는 데이터를 요청할 때 로딩 처리를 하면서 목록이 잠시 사라졌다가 요청이 끝났을 때 다시 나오기 때문입니다.

처음에 비어있던 목록이 한 번 채워지고 나면, 요청이 끝나지 않았을 때만 "더보기" 버튼 부분이 로딩 처리되도록 해주어야 합니다. 이렇게 조건에 따라 다르게 보여주는 방식은 UI 리팩토링 기법으로, 한 목록을 여러 페이지로 나누어 보여줄 때 자주 사용합니다.

{title="src/App.js",lang="javascript"}

```
const App = () => {
  ...

  return (
    <div>
      ...

# leanpub-start-insert
      <List list={stories.data} onRemoveItem={handleRemoveStory} />
# leanpub-end-insert

      {stories.isLoading ? (
        <p>Loading ...</p>
      ) : (
# leanpub-start-insert
        <button type="button" onClick={handleMore}>
          More
        </button>
# leanpub-end-insert
      )}
    </div>
  );
};
```

이제 인기있는 기사 데이터를 계속해서 불러올 수 있습니다. 외부 API를 활용할 때는 항상 해당 API로 작업 가능한 범위를 알아두는 것이 좋습니다. 외부 API는 각기 다른 데이터 구조로 되어있어 특징도 다릅니다. (번역자: 마지막 문장은... 의미를 잘 모르겠어서 skip 합니다.)

### 실습하기

- [마지막 장의 소스 코드](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/Paginated-Fetch)를 확인합니다.
  - [마지막 장에서 변경된 코드](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/Remember-Last-Searches...hs/Paginated-Fetch?expand=1)를 확인합니다.
- [해커 뉴스 API 문서](https://hn.algolia.com/api)를 다시 확인해보세요. API 엔드포인트에 파라미터를 추가해 한 페이지보다 많은 데이터를 불러올 수 있나요?
- 이 장의 앞 부분에서 여러 페이지 처리 기능과 무한 페이지 로딩 처리에 대해 이야기한 부분을 다시 읽어보세요. 1-[3]-10과 같이, 각 버튼을 눌렀을 때 해당 버튼에 해당하는 페이지만 나타나는 일반적인 페이지 처리 방식을 어떻게 구현할 건가요?
- "더보기" 버튼을 넣는 대신 무한 스크롤이 가능하게 만든다면 어떻게 구현할 건가요? 다음 페이지 데이터를 불러오기 위해 명시적으로 버튼을 클릭하게 하지 않고, 브라우저의 창이 화면에 나타난 목록의 끝으로 내려왔을 때 다음 페이지 데이터를 불러오는 식으로 무한 스크롤을 구현할 수 있습니다.
