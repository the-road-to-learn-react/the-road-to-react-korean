## Props 핸들링 (심화)

Props는 컴포넌트 트리 안에서 부모로부터 자식에게 전달됩니다. Props를 사용하여 컴포넌트 A에서 컴포넌트 B에게 데이터를 전달하는 경우가 많고, 때로는 컴포넌트 C를 통해 전달하기도 합니다. Props를 더 편리하게 사용할 수 있는 몇 가지 방법에 대해 알아봅시다.

*메모: 다음 리팩터링은 다른 자바스크립트/리액트 패턴을 학습을 위한 것으로는 권장하지만, 이러한 과정 없이도 온전한 리액트 애플리케이션을 만들 수 있습니다. 소스 코드를 더욱 간결하게 만드는 리액트 고급 테크닉에 대해 고려해보세요.*

리액트 props는 자바스크립트 객체이므로 리액트 컴포넌트에서 `props.list` 또는 `props.onSearch` 에 접근할 수 없습니다. `props`가 객체이기 때문에 몇 가지 자바스크립트 트릭을 적용할 수가 있습니다. 그 예로, 객체 프로퍼티에 접근하는 것이 가능합니다.

{title="Code Playground",lang="javascript"}
~~~~~~~
const user = {
 firstName: 'Robin',
 lastName: 'Wieruch',
};

// 구조 분체(object destructing)를 하지 않은 경우
const firstName = user.firstName;
const lastName = user.lastName;

console.log(firstName + ' ' + lastName);
// "Robin Wieruch"

//구조 분체(object destructing)를 한 경우
const { firstName, lastName } = user;

console.log(firstName + ' ' + lastName);
// "Robin Wieruch"
~~~~~~~

이러한 기능을 [자바스크립트 구조 분해(destructuring)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)라고 합니다. 객체의 여러 속성에 접근해야 한다면 여러 줄 대신 한 줄의 코드를 사용하는 것이 더 간단하고 명료합니다. 이제 Search 컴포넌트의 props에 적용해봅시다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const Search = props => {
# leanpub-start-insert
 const { search, onSearch } = props;
# leanpub-end-insert

 return (
   <div>
     <label htmlFor="search">Search: </label>
     <input
       id="search"
       type="text"
# leanpub-start-insert
       value={search}
       onChange={onSearch}
# leanpub-end-insert
     />
   </div>
 );
};
~~~~~~~

리액트 컴포넌트에서 `props` 객체를 구조 분해함으로써 `props` 객체 없이 프로퍼티를 사용할 수 있습니다. `props` 의 프로퍼티에 접근하기 위해 Search 컴포넌트의 화살표 함수를 간결한(concise) 바디에서 블록(block) 바디로 리팩터링했습니다. 이러한 패턴을 사용하지 않고, 함수 시그니처에서 `props`를 구조 분해한다면 조금 전에 만든 블록 바디를 걷어낼 수 있습니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
# leanpub-start-insert
const Search = ({ search, onSearch }) => (
# leanpub-end-insert
 <div>
   <label htmlFor="search">Search: </label>
   <input
     id="search"
     type="text"
# leanpub-start-insert
     value={search}
     onChange={onSearch}
# leanpub-end-insert
   />
 </div>
);
~~~~~~~

컴포넌트 안에서 `props`를 객체 그 자체로 사용하는 일은 드뭅니다. `props`는 실제 컴포넌트에서 사용되는 정보가 담긴 컨테이너와 같습니다.`props` 객체를 구조 분해해 필요한 정보만 가져올 수 있습니다.

이제 `props` 객체에 자체에 대한 것보다는, 이 객체에서 나오는 정보에 대해 살펴봅시다. 먼저 List 컴포넌트에서 Item 컴포넌트를 새로 뽑아냅니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
# leanpub-start-insert
const List = ({ list }) =>
 list.map(item => <Item key={item.objectID} item={item} />);
# leanpub-end-insert

# leanpub-start-insert
const Item = ({ item }) => (
 <div>
   <span>
     <a href={item.url}>{item.title}</a>
   </span>
   <span>{item.author}</span>
   <span>{item.num_comments}</span>
   <span>{item.points}</span>
 </div>
);
# leanpub-end-insert
~~~~~~~

앞서, 각 컴포넌트의 함수 시그니처에서 `props` 객체를 구조 분해했습니다. Item 컴포넌트에 들어오는 `item` 은 `props`로 보일 수도 있을 겁니다. Item 컴포넌트 안에서 직접 사용하지 않았으니까요. 이러한 문제를 해결하기 위해선 3가지 방법을 사용할 수 있습니다. 첫 번째는 컴포넌트의 함수 시그니처에서 *중첩 구조 분해(nested destructuring)*를 하는 것입니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
// 첫 번째 버전 (최종)
const Item = ({
# leanpub-start-insert
 item: {
   title,
   url,
   author,
   num_comments,
   points,
 },
# leanpub-end-insert
}) => (
 <div>
   <span>
# leanpub-start-insert
     <a href={url}>{title}</a>
# leanpub-end-insert
   </span>
# leanpub-start-insert
   <span>{author}</span>
   <span>{num_comments}</span>
   <span>{points}</span>
# leanpub-end-insert
 </div>
);
~~~~~~~

중첩 구조 분해는 함수 시그니처에서 일어나는 들여쓰기 때문에 많은 혼란을 야기합니다. 가장 읽기 어려운 방법이지만, 특정 상황에서는 유용한 방법이 될 수 있습니다. 이제 두 번째 방법으로 이동합니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
// 두 번째 버전 (1)
const List = ({ list }) =>
 list.map(item => (
   <Item
     key={item.objectID}
# leanpub-start-insert
     title={item.title}
     url={item.url}
     author={item.author}
     num_comments={item.num_comments}
     points={item.points}
# leanpub-end-insert
   />
 ));

# leanpub-start-insert
const Item = ({ title, url, author, num_comments, points }) => (
# leanpub-end-insert
 <div>
   <span>
     <a href={url}>{title}</a>
   </span>
   <span>{author}</span>
   <span>{num_comments}</span>
   <span>{points}</span>
 </div>
);
~~~~~~~

Item 컴포넌트의 함수 시그니처는 간결해졌지만, 모든 프로퍼티가 Item 컴포넌트에서 개별적으로 전달이 되었기 때문에 List 컴포넌트가 복잡해지게 됩니다. 이럴 경우 [자바스크립트의 전개 연산자(spread operator)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)을 통해 개선할 수 있습니다.

{title="Code Playground",lang="javascript"}
~~~~~~~
const person = {
 firstName: 'Robin',
 lastName: 'Wieruch',
};

const details = {
 year: 1988,
 country: 'Germany',
};

const personWithDetails = { ...person, ...details };

console.log(personWithDetails);
// {
//   firstName: "Robin",
//   lastName: "Wieruch",
//   year: 1988,
//   country: "Germany"
// }
~~~~~~~

Props를 통해 List에서 Item 컴포넌트로 프로퍼티를 하나씩 전달하는 대신에, 자바스크립트의 전개 연산자를 사용하여 모든 객체의 키/값의 쌍을 속성/값의 쌍으로 JSX 엘레먼트에 전달할 수 있습니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
// 두 번째 버전 (2)
const List = ({ list }) =>
# leanpub-start-insert
 list.map(item => <Item key={item.objectID} {...item} />);
# leanpub-end-insert

const Item = ({ title, url, author, num_comments, points }) => (
 ...
);
~~~~~~~

그런 다음, [자바스크립트의 나머지 파라미터(Rest parameters)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters)를 사용합니다.

{title="Code Playground",lang="javascript"}
~~~~~~~
const person = {
 firstName: 'Robin',
 lastName: 'Wieruch',
 year: 1988,
};

const { year, ...personWithoutYear } = person;

console.log(personWithoutYear);
// {
//   firstName: "Robin",
//   lastName: "Wieruch"
// }
~~~~~~~

자바스크립트 나머지 연산자는 객체 구조 분해의 마지막 부분입니다. 전개 연산자와 동일한 연산자를 사용하기 때문에 착각할 수 있습니다. 일반적으로 나머지 연산자는 할당하는 부분의 오른쪽에서 사용하고, 전개 연산자는 왼쪽에서 사용합니다.

이제 List 컴포넌트에서 item과 `objectID`를 구분하여 사용할 수 있습니다. `objectID`는 `key`로만 사용될 뿐, Item 컴포넌트 안에서 사용되는 값이 아니기 때문입니다. 나머지 item만 이전처럼 속성/값의 쌍으로 Item 컴포넌트에 확장됩니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
// 두 번째 버전 (3/최종)
const List = ({ list }) =>
# leanpub-start-insert
 list.map(({ objectID, ...item }) => (
   <Item key={objectID} {...item} />
# leanpub-end-insert
 ));
~~~~~~~

이 버전은 매우 간결하지만, 고급 자바스크립트 문법을 사용하게 됩니다. 세 번째 버전에서는 좀 더 읽기 쉬운 방법을 사용해봅시다.

{title="src/App.js",lang="javascript"}
~~~~~~~
// 세 번째 버전 (최종)
const List = ({ list }) =>
 list.map(item => <Item key={item.objectID} item={item} />);

const Item = ({ item }) => (
 <div>
   <span>
     <a href={item.url}>{item.title}</a>
   </span>
   <span>{item.author}</span>
   <span>{item.num_comments}</span>
   <span>{item.points}</span>
 </div>
);
~~~~~~~

개인적으로는 이 방법이 여러 사람들과 리액트 프로젝트에서 협업하기에 가장 좋다고 생각합니다. 두 번째 버전만큼 간결하지는 않지만, 더 읽기 쉽고 Item 컴포넌트에 노출되는 API 영역도 줄일 수 있습니다. 무엇보다 자바스크립트의 기능(전개 연산자, 나머지 연산자)을 과하게 쓰지 않아도 됩니다.

위 세 가지 버전에는 모두 장단점이 있습니다. 컴포넌트를 리팩터링 할 때는 항상 가독성을 신경 쓰세요. 특히 여러 사람으로 구성된 팀에서 작업할 경우에는 공통적으로 사용하는 리액트 코드 스타일을 잊지 마세요.

### 읽어보기

* [지난 장에서 사용한 코드](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/Props-Handling)를 확인하세요.
 * [지난 장에서 수정된 코드](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/React-Controlled-Components...hs/Props-Handling?expand=1)를 확인하세요.
* [자바스크립트의 구조 분해 할당](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)에 대해 읽어보세요.
* 리액트의 `useState` 훅에서 사용한 자바스크립트 배열 구조 분해와 객체 구조 분해의 차이에 대해 생각해보세요.
* [자바스크립트의 전개 연산자](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)에 대해 읽어보세요.
* [자바스크립트의 나머지 파라미터](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters)에 대해 읽어보세요.
* 자바스크립트를 더 잘 이해할 수 있는 부분(전개 연산자, 나머지 파라미터, 구조 분해)들에 대해 알아보고 어떤 것들이 리액트(예: props)와 연관되어있는지 생각해보세요.
* 리액트의 props를 핸들링하는 나만의 방법을 찾아보세요. 아직 결정하지 못했다면 이전 장에서 사용한 버전에 대해서도 생각해보세요.