## 리액트 Props

우리는 현재 `list` 변수를 애플리케이션의 전역 변수로 사용하고 있습니다. 변수를 App 컴포넌트의 전역 스코프에서 직접 사용하고, List 컴포넌트에서도 똑같이 사용했습니다. 이는 변수를 한 개만 사용한다면 문제가 되지 않지만, 여러 개의 변수를 여러 컴포넌트에서 사용할 때는 효율적이지 못한 방법입니다.

Props를 사용하면 변수에 저장된 데이터를 한 컴포넌트에서 다른 컴포넌트로 전달할 수 있습니다. Props를 사용하기에 앞서, 전역 스코프에 선언한 list를 App 컴포넌트 안에서 호출하고, 필요한 기능에 맞게 이름을 바꿀 것입니다.

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

이제 **리액트 props**를 사용하여 배열을 List 컴포넌트에 전달해봅시다.

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

App 컴포넌트에 변수 `stories`를 생성하고, 이 이름으로 List 컴포넌트에 전달하겠습니다. 그러나 이 props는 List 컴포넌트가 인스턴스화될 때 `list` 속성으로 할당됩니다. List 컴포넌트의 함수 시그니처(function signature)를 통해 `props ` 객체는 `list`으로 접근하게 됩니다.

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

이 작업을 통해 list/stories 변수가 App 컴포넌트에서 다른 값으로 대체되는 것을 방지했습니다. `stories` 는 App 컴포넌트에서 직접 사용되지는 않지만, App의 자식 컴포넌트인 List 컴포넌트에서는 사용되기 때문에 props로 전달했습니다. 이제 첫 번째 함수 시그니쳐의 인수인 `props` 를 통해 stories에 접근할 수 있게 되었습니다.



* [지난 장에서 사용한 소스코드](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/React-Props)를 확인하세요.
  * [지난 장에서 수정된 코드](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/Handler-Function-in-JSX...hs/React-Props?expand=1)도 확인하세요..
* [리액트 컴포넌트에 props를 전달하는 방법](https://www.robinwieruch.de/react-pass-props-to-component)에 대해서 더 알아보세요.