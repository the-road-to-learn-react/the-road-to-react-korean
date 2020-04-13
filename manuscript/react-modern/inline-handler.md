## JSX의 인라인 핸들러

지금까지 살펴본 stories 리스트는 상태를 갖지 않은 변수였습니다. 검색 기능을 이용해 렌더링 된 리스트를 필터링할 수는 있지만, 필터를 제거하면 리스트 자체는 온전한 상태로 남아있습니다. 필터는 단지 외부 기능을 이용해 일시적인 변화를 만들어낼 뿐이며 실제 리스트를 조작할 수는 없습니다.

리스트를 조작할 수 있도록 리액트의 useState 훅을 사용해 봅시다. 리스트를 초기 상태로 사용하여 리스트가 상태를 갖도록 만들면 됩니다. 훅은 현재 상태(`stories`)와 상태를 업데이트하는 함수(`setStories`)를 반환합니다. 아직 직접 만든 `useSemiPersistentState` 훅을 사용하지는 않을 것입니다. 매번 브라우저를 열 때마다 캐시된 상태의 리스트가 아니라 항상 초기 상태의 리스트를 보고 싶기 때문입니다.

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

이 애플리케이션은 이전 코드와 동일하게 동작합니다. `useState` 훅에서 반환된 `stories`가 동일하게 `searchedStories`로 필터링 되어 List 컴포넌트에 출력됩니다. 이제 리스트에서 아이템을 삭제하면서 리스트를 조작해봅시다.

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

App 컴포넌트의 콜백 핸들러는 삭제할 아이템을 인수로 하여 필터 조건을 충족하지 않는 모든 아이템을 삭제하면서 stories를 필터링합니다. 그다음 반환된 stories는 새로운 상태로 설정되고 List 컴포넌트는 해당 함수를 자식 컴포넌트에 전달합니다. List 컴포넌트가 새로운 상태 정보를 사용하기 위해서가 아니라 단지 자식에게 전달하기 위함입니다.

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

마침내 List로부터 전달받은 함수에 `item`을 넘겨주기 위해 Item 컴포넌트에 또 다른 핸들러를 정의해 사용합니다. button 엘레먼트는 실제로 이벤트를 발생시키기 위해 사용되었습니다.

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

사실 App 컴포넌트의 콜백 핸들러에서는 아이템의 `objectID` 값만 필요했기 때문에 이 값만 전달해줄 수도 있었습니다. 하지만 핸들러가 이후에 다른 곳에서 어떤 정보가 필요할지 확신할 수 없습니다. 아이템을 삭제하기 위해 식별자 이외의 다른 정보를 더 필요할지도 모르기 때문입니다.`onRemoveItem` 핸들러를 호출할 때 아이템의 식별자가 아니라 아이템 자체를 전달해야 합니다.

리액트의 useState 훅을 이용해 stories 리스트가 상태를 갖도록 만들었습니다. 그러고 나서 검색 결과로 필터링 된 stories를 List 컴포넌트에 props로 전달했으며 콜백 핸들러(`handleRemoveStory`)와 Item 컴포넌트에서 사용될 핸들러(`handleRemoveItem`)를 구현했습니다. 핸들러는 그저 함수이기 때문에 이 상황에서 아무것도 반환하지 않습니다. 그러므로 코드의 완성도를 위해 함수 블록 부분을 걷어내 봅시다.

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

이러한 변경사항은 함수 컴포넌트에서 핸들러의 수가 많아질수록 소스 코드의 가독성을 떨어트립니다. 가끔 함수 컴포넌트에 존재하는 화살표 함수 핸들러를 다시 일반적인 함수 선언문으로 리팩토링할 때도 있습니다. 단지 컴포넌트를 더욱 확장 가능하게 만들기 위해서 말이죠.

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

이번 절에서는 이전에 배운 props, 핸들러, 콜백 핸들러, 그리고 state 개념을 적용해보았습니다. 이제부터는 JSX 안에서 함수를 바로 실행할 수 있게 해주는 **인라인 핸들러**에 관해 알아보겠습니다. Item 컴포넌트에서 전달받은 함수를 인라인 핸들러로 사용하는 방법은 두 가지가 존재합니다. 첫 번째 방법은 자바스크립트의 bind 메서드를 사용하는 방법입니다.

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

함수에 [자바스크립트의 bind 메서드](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_objects/Function/bind)를 사용하면 함수를 실행할 때 전달해야 하는 인자를 직접 바인딩 할 수 있습니다. bind 메서드는 바인드된 인자를 가진 새로운 함수를 반환합니다.

더욱 널리 사용되는 두 번째 방법은 화살표 함수를 사용해 래핑하는 방법입니다. 화살표 함수를 사용하면 아래 코드처럼 `item`과 같은 인자를 슬쩍 넘겨줄 수 있습니다.

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

이 방법은 신속한 해결방안입니다. 가끔 함수 시그니처와 반환(return)문 사이에 놓인 적절한 핸들러를 정의하기 위해 함수 컴포넌트의 간결한 함수 본문을 다시 함수 블록으로 리팩토링하는 것을 원치 않기 때문입니다. 이 방법은 다른 방법보다 더 간결하지만, 자바스크립트의 로직이 JSX 안에 감춰질 수 있기 때문에 디버깅하기가 더 어려울 수 있습니다. 만약 래핑한 화살표 함수가 여러 줄의 구현 로직을 캡슐화한다면 간결한 본문 대신 함수 블록을 사용해 더욱 장황하게 코드를 작성해야 할 수도 있습니다. 이러한 상황은 지양해야 합니다.

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

인라인 핸들러와 일반 핸들러를 포함해 총 세 가지 버전의 핸들러는 모두 용인되는 방식입니다. 인라인 핸들러는 구현 내용을 JSX 안에 작성하고 그 외의 핸들러는 함수 컴포넌트의 블록 본문에 작성한다는 차이점이 있을 뿐입니다.

### 실습하기

* [[코드샌드박스] 이전 절의 소스 코드](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/Inline-Handler-in-JSX)를 읽어보세요.
  * [[깃허브] 이전 절의 소스 코드](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/Imperative-React...hs/Inline-Handler-in-JSX?expand=1)를 확인하세요.
* 핸들러, 콜백 핸들러, 인라인 핸들러에 관한 내용을 복습하세요.