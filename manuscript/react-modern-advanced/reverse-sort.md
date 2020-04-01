## 역방향 정렬

**과제:** 잘 동작하는 정렬을 구현했습니다. 하지만 아직 한 방향으로만 정렬됩니다. 버튼을 두 번 클릭하면 역방향으로 정렬되도록 구현하세요. 기본(오름차순) 정렬과 역방향(내림차순) 정렬을 껐다 키는 기능입니다.

**힌트 보기:**

- `sortKey` 상태와 함께, 기본 정렬 상태인지 역방향 정렬 상태인지는 또 다른 상태(예: `isReverse`)로 관리해보세요.
- 이전 정렬 상태를 기준으로 `handleSort` 핸들러에 새로운 상태를 추가합니다.
- SORTS 객체에서 반환한 정렬 함수에, 새로 추가한 `isReverse` 상태에 따라 자바스크립트 배열의 내장 함수인 `reverse()`를 적용해 배열을 정렬합니다.

기존에 만든 정렬은 숫자들을 높은 수부터 작은 수로 역방향 정렬해주는 것과 마찬가지로 문자열도 정렬해줍니다. 이제 정렬이 기본 방향인지 역방향인지 파악할 수 있는 상태를 추가해 좀 더 복잡한 작업을 해봅시다.

{title="src/App.js",lang="javascript"}

```
const List = ({ list, onRemoveItem }) => {
# leanpub-start-insert
  const [sort, setSort] = React.useState({
    sortKey: 'NONE',
    isReverse: false,
  });
# leanpub-end-insert

  ...
};
```

다음으로, 인자로 들어온 sortKey가 기본 방향 정렬인지 역방향 정렬인지 확인 로직을 핸들러 함수에 추가합니다. 만약 인자로 들어온 sortKey가 현재 sortKey 상태값과 같고 현재 역방랼 정렬이 되지 않은 상태라면 isReverse 상태값을 true로 합니다.

{title="src/App.js",lang="javascript"}

```
const List = ({ list, onRemoveItem }) => {
  const [sort, setSort] = React.useState({
    sortKey: 'NONE',
    isReverse: false,
  });

  const handleSort = sortKey => {
# leanpub-start-insert
    const isReverse = sort.sortKey === sortKey && !sort.isReverse;

    setSort({ sortKey: sortKey, isReverse: isReverse });
# leanpub-end-insert
  };

# leanpub-start-insert
  const sortFunction = SORTS[sort.sortKey];
# leanpub-end-insert
  const sortedList = sortFunction(list);

  return (
    ...
  );
};
```

마지막으로, dictionary에서 찾은 정렬 함수를 실행할 때 `isReverse` 상태값에 맞게 자바스크립트에 내장된 reverse 함수를 추가하도록 합니다.

{title="src/App.js",lang="javascript"}

```
const List = ({ list, onRemoveItem }) => {
  const [sort, setSort] = React.useState({
    sortKey: 'NONE',
    isReverse: false,
  });

  const handleSort = sortKey => {
    const isReverse = sort.sortKey === sortKey && !sort.isReverse;

# leanpub-start-insert
    setSort({ sortKey, isReverse });
# leanpub-end-insert
  };

  const sortFunction = SORTS[sort.sortKey];

# leanpub-start-insert
  const sortedList = sort.isReverse
    ? sortFunction(list).reverse()
    : sortFunction(list);
# leanpub-end-insert

  return (
    ...
  );
};
```

이제 역방향 정렬이 동작하도록 만들었습니다. 상태값 업데이트용 함수에 초기 인자로 넣어줄 객체는 만들 때는 **단축 객체 초기자 표기법**을 사용합니다.

{title="src/App.js",lang="javascript"}

```
const firstName = 'Robin';

const user = {
  firstName: firstName,
};

console.log(user);
// { firstName: "Robin" }
```

**단축 객체 초기자 표기법**을 사용하면 객체의 속성 이름과 해당 속성의 값에 할당하려는 변수의 이름이 같을 때, 속성 이름만 써주면 됩니다.

{title="src/App.js",lang="javascript"}

```
const firstName = 'Robin';

const user = {
  firstName,
};

console.log(user);
// { firstName: "Robin" }
```

이에 대한 내용이 더 궁금하다면 [JavaScript Object Initializers](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object_initializer)를 참고하세요.

### 연습문제:

- [마지막 장의 소스 코드](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/Reverse-Sort))를 확인합니다.
  - [마지막 장에서 변경된 코드](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/Sort...hs/Reverse-Sort?expand=1)를 확인합니다.
- App 컴포넌트가 아니라 List 컴포넌트 안에서 정렬 상태값을 관리할 때의 단점이 무엇일지 생각해보세요. 잘 모르겠다면 "Title'로 배열을 정렬한 뒤 다른 책을 검색해보세요. App 컴포넌트에서 정렬 상태값을 관리한다면 어떤 게 달라질까요?
- 사용자가 현재 선택된 정렬 기준과 정렬 방향이 무엇인지 잘 알 수 있도록 여러분만의 스타일링 기술을 사용해봅니다. 각 정렬 버튼 옆에 [위, 아래 화살표 SVG](https://www.flaticon.com/packs/arrow-set-2)를 추가하는 것도 하나의 방법입니다.
