# 현실 속 리액트 (심화)

지금까지 이 책을 통해 리액트 기초, 리액트 최신 버전 이전의 기능들, 애플리케이션 유지보수를 위한 기술 등을 배웠습니다. 이제 현실 속에서 리액트 애플리케이션을 개발할 차례입니다. 각 장에는 과제가 있습니다. 처음에는 _힌트 보기_ 부분을 건너뛰고 과제를 수행해보세요. 처음엔 꽤 힘들 수 있습니다. 도움이 필요할 때 _힌트 보기_ 부분을 참고하거나 각 장의 안내문을 따라하세요.

## 정렬

**과제:** 여러 아이템을 담은 목록을 다룰 때는 사용자가 효율적으로 데이터를 탐색할 수 있도록 작업 해야 하는 경우가 많습니다. 지금까지 모든 아이템을 각각의 속성들과 함께 나열했습니다. 사용자가 데이터를 더 쉽게 탐색하려면 목록을 제목, 저자, 댓글, 점수로 오름차순 및 내림차순 정렬할 수 있어야 합니다. 오름차순이나 내림차순 한 방향으로만 정렬을 구현해도 괜찮습니다. 반대 반향 정렬 기능은 다음 장에서 구현하게 될 것입니다.

**힌트 보기**

- App이나 List 컴포넌트에 정렬을 위한 상태를 새로 추가합니다.
- 각 속성(예시: `title`, `author`, `points`, `num_comments`)별로 HTML 버튼을 만들고, 이 버튼을 누르면 각 속성으로 새로 추가한 상태값이 설정되도록 합니다.
- 배열 형태의 `목록`을 선택한 속성으로 정렬하는 데 적절한 함수를 실행하기 위해 새로 만든 정렬 상태값을 활용합니다.
- [Lodash](https://lodash.com/)와 같은 유틸리티 라이브러리에 속한 `sortBy`와 같은 함수를 활용하길 추천합니다.

데이터 목록을 하나의 테이블로 생각해봅시다. 하나의 열은 목록의 한 아이템을 나타내고, 해당 열의 각 행은 해당 아이템의 속성을 나타냅니다. 헤더의 이름 등을 통해 사용자에게 각 행에 대한 정보를 제공할 수 있습니다.

{title="src/App.js",lang="javascript"}

```
# leanpub-start-insert
const List = ({ list, onRemoveItem }) => (
  <div>
    <div style={{ display: 'flex' }}>
      <span style={{ width: '40%' }}>Title</span>
      <span style={{ width: '30%' }}>Author</span>
      <span style={{ width: '10%' }}>Comments</span>
      <span style={{ width: '10%' }}>Points</span>
      <span style={{ width: '10%' }}>Actions</span>
    </div>

    {list.map(item => (
# leanpub-end-insert
      <Item
        key={item.objectID}
        item={item}
        onRemoveItem={onRemoveItem}
      />
# leanpub-start-insert
    ))}
  </div>
);
# leanpub-end-insert
```

가장 기본적인 레이아웃을 만들기 위해 인라인 스타일을 추가합니다. 모든 열의 레이아웃을 헤더와 동일하게 맞추기 위해 각 Item 컴포넌트에도 헤더와 동일한 레이아웃을 적용합니다.

{title="src/App.js",lang="javascript"}

```
const Item = ({ item, onRemoveItem }) => (
# leanpub-start-insert
  <div style={{ display: 'flex' }}>
    <span style={{ width: '40%' }}>
# leanpub-end-insert
      <a href={item.url}>{item.title}</a>
    </span>
# leanpub-start-insert
    <span style={{ width: '30%' }}>{item.author}</span>
    <span style={{ width: '10%' }}>{item.num_comments}</span>
    <span style={{ width: '10%' }}>{item.points}</span>
    <span style={{ width: '10%' }}>
# leanpub-end-insert
      <button type="button" onClick={() => onRemoveItem(item)}>
        Dismiss
      </button>
    </span>
  </div>
);
```

다음 코드부터는 스타일 속성들을 표시 하지 않습니다. 스타일 속성은 공간을 많이 차지하고, 중요한 구현 로직을 보기 어렵게 만듭니다. (그래서 CSS 파일로 적절하게 분리했습니다.) 이는 가독성을 위한 위한 것이니 여러분의 코드는 그대로 두길 바랍니다.

정렬에 필요한 새로운 상태를 관리하는 주체는 List 컴포넌트입니다. 상태 관리를 App 컴포넌트에서 할 수도 있지만 List 컴포넌트에서 해도 충분하니 List 컴포넌트에 상태를 추가합니다. 추가한 정렬 상태는 `'NONE'`이라는 초기 값을 갖고, 목록은 API로부터 아이템을 받아온 순서 그대로 나타납니다. 그 다음으로, 정렬에 필요한 key를 인자로 받아 정렬 상태를 설정하는 핸들러 함수를 추가합니다.

{title="src/App.js",lang="javascript"}

```
# leanpub-start-insert
const List = ({ list, onRemoveItem }) => {
  const [sort, setSort] = React.useState('NONE');

  const handleSort = sortKey => {
    setSort(sortKey);
  };

  return (
# leanpub-end-insert
    ...
# leanpub-start-insert
  );
};
# leanpub-end-insert
```

List 컴포넌트의 헤더들을 버튼으로 만들어 각 행/속성으로 정렬 상태값을 설정할 수 있도록 합니다. 핸들러 함수를 인라인으로 추가해 정렬하려는 속성(`sortKey`)을 정렬 상태값에 추가합니다. "Title" 행의 버튼이 클릭되었을 때 `'TITLE'`이 새로운 정렬 상태의 값으로 설정됩니다.

{title="src/App.js",lang="javascript"}

```
const List = ({ list, onRemoveItem }) => {
  ...

  return (
    <div>
      <div>
        <span>
# leanpub-start-insert
          <button type="button" onClick={() => handleSort('TITLE')}>
            Title
          </button>
# leanpub-end-insert
        </span>
        <span>
# leanpub-start-insert
          <button type="button" onClick={() => handleSort('AUTHOR')}>
            Author
          </button>
# leanpub-end-insert
        </span>
        <span>
# leanpub-start-insert
          <button type="button" onClick={() => handleSort('COMMENT')}>
            Comments
          </button>
# leanpub-end-insert
        </span>
        <span>
# leanpub-start-insert
          <button type="button" onClick={() => handleSort('POINT')}>
            Points
          </button>
# leanpub-end-insert
        </span>
        <span>Actions</span>
      </div>

      {list.map(item => ... )}
    </div>
  );
};
```

새로운 기능을 위한 상태 관리를 구현했습니다. 하지만 아직 버튼을 클릭했을 때 어떤 액션이 이루어지지 않습니다. 아직 실제로 정렬이 동작하도록 `list`에 적용하지 않았기 때문입니다.

자바스크립트로 배열을 정렬할 때 생각보다 처리해줘야 하는 작업이 많습니다. 배열을 특정 속성으로 정렬하고자 하는데 각 요소로 string, boolean, number와 같은 기본 데이터 타입이 들어가 있어 엣지 케이스에 부딪힐 수 있기 때문입니다. 이를 방지하기 위해 [Lodash](https://lodash.com/)라는 라이브러리의 다양한 자바스크립트 유틸리티 함수들을 활용합니다 (예시: `sortBy`). 우선, 커맨드 라인에 명령어를 입력해 설치를 시작합니다.

{title="Command Line",lang="text"}

```
npm install lodash
```

둘째로, 파일 상단에 정렬을 위한 유틸리티 함수를 불러옵니다.

{title="src/App.js",lang="javascript"}

```
import React from 'react';
import axios from 'axios';
# leanpub-start-insert
import { sortBy } from 'lodash';
# leanpub-end-insert

...
```

셋째로, 자바스크립트 객체(dictionary라고 불리기도 합니다.)를 만들어 필요한 모든 `sortKey`들을 속성으로, 각 속성에 맞는 정렬 함수를 값으로 추가합니다. 속성으로 설정된 `sortKey`를 기준으로 `list`를 정렬하는 데 필요한 함수를 실행합니다. `sortKey`가 `'NONE'`이면 인자로 들어온 목록을 정렬하지 않은 채 그대로 반환하고 `'POINT'`일 땐 `points` 속성으로 아이템이 정렬된 목록을 반환합니다.

{title="src/App.js",lang="javascript"}

```
# leanpub-start-insert
const SORTS = {
  NONE: list => list,
  TITLE: list => sortBy(list, 'title'),
  AUTHOR: list => sortBy(list, 'author'),
  COMMENT: list => sortBy(list, 'num_comments').reverse(),
  POINT: list => sortBy(list, 'points').reverse(),
};
# leanpub-end-insert

const List = ({ list, onRemoveItem }) => {
  ...
};
```

`정렬 상태값` (`sortKey`)으로 우리는 필요한 정렬 기준을 만들고 얼마든지 필요한 형태로 목록을 정렬할 수 있습니다. Item 컴포넌트를 만들기 전에 목록을 정렬해주기만 하면 됩니다.

{title="src/App.js",lang="javascript"}

```
const List = ({ list, onRemoveItem }) => {
  const [sort, setSort] = React.useState('NONE');

  const handleSort = sortKey => {
    setSort(sortKey);
  };

# leanpub-start-insert
  const sortFunction = SORTS[sort];
  const sortedList = sortFunction(list);
# leanpub-end-insert

  return (
    <div>
      ...

# leanpub-start-insert
      {sortedList.map(item => (
# leanpub-end-insert
        <Item
          key={item.objectID}
          item={item}
          onRemoveItem={onRemoveItem}
        />
      ))}
    </div>
  );
};
```

이제 끝났습니다. 먼저 우리는 상태의 값인 `sortKey`로 dictionary 자료구조에서 필요한 정렬 함수를 찾았습니다. 그리고 이 정렬 함수로 목록을 먼저 정렬한 뒤에 render 함수 안에서 각각의 Item 컴포넌트를 만들었습니다. 한 번 복습해보겠습니다. 최초의 정렬 상태값은 `'NONE'`이었고 이는 정렬을 적용하지 않는다는 뜻입니다.

둘째로 사용자가 선택할 수 있는 HTML 버튼들을 만들었습니다. 그리고 버튼을 눌렀을 때 정렬 상태값이 바뀌도록 했습니다. 마지막으로 정렬 상태값을 활용해 실제 목록을 정렬했습니다.

### 연습문제:

- [마지막 장의 소스 코드](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/Sort)를 확인합니다.
  - [마지막 장에서 변경된 코드](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/react-modern-final...hs/Sort?expand=1)를 확인합니다.
- [Lodash](https://lodash.com/) 자료를 더 읽어봅니다.
- `points`와 `num_comments`와 같이 숫자를 값으로 가진 속성에는 왜 역방향 정렬을 정렬했을까요?
- 사용자가 현재 선택된 정렬 기준이 무엇인지 잘 알 수 있도록 여러분만의 스타일링 기술을 사용해봅니다. 현재 선택된 정렬 기준 버튼에만 다른 색깔을 적용하는 것과 같이 단순한 방법이어도 좋습니다.
