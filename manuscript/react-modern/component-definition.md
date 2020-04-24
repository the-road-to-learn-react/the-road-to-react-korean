## 리액트 컴포넌트 정의 (심화)

다음 리팩터링은 선택사항으로, 자바스크립트/리액트의 다양한 패턴을 설명합니다. 물론 이러한 고급 패턴 없이도 완전한 리액트 애플리케이션을 구축할 수 있습니다. 너무 복잡해 보인다면 권장하지 않습니다.

*src/App.js* 파일에 있는 모든 컴포넌트는 함수형 컴포넌트였습니다. 지금까지는 화살표 함수(arrow functions)보다는 함수 선언식(function statement)을 사용해왔죠. 자바스크립트에는 함수를 선언하는 여러 가지 방법에 대해 알아보겠습니다.

{title="Code Playground",lang="javascript"}
~~~~~~~
// 함수 선언
function () { ... }

// 화살표 함수 선언
const () => { ... }
~~~~~~~

전달하려는 인수가 1개인 경우에는 괄호를 제거할 수 있습니다. 그러나 인수가 여러 개인 경우에는 반드시 괄호가 필요합니다.

{title="Code Playground",lang="javascript"}
~~~~~~~
// 허용
const item => { ... }

// 허용
const (item) => { ... }

// 비허용
const item, index => { ... }

// 비허용
const (item, index) => { ... }
~~~~~~~

화살표 함수를 사용하면 리액트 컴포넌트를 더욱 간결하게 정의할 수 있습니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
# leanpub-start-insert
const App = () => {
# leanpub-end-insert
  return (
    <div>
      ...
    </div>
  );
# leanpub-start-insert
};
# leanpub-end-insert

# leanpub-start-insert
const List = () => {
# leanpub-end-insert
  return list.map(function(item) {
    return (
      <div key={item.objectID}>
        ...
      </div>
    );
  });
# leanpub-start-insert
};
# leanpub-end-insert
~~~~~~~

자바스크립트 배열의 map 메서드에서 사용한 것처럼, 다른 함수에서도 마찬가지로 사용할 수 있습니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const List = () => {
# leanpub-start-insert
  return list.map(item => {
# leanpub-end-insert
    return (
      <div key={item.objectID}>
        <span>
          <a href={item.url}>{item.title}</a>
        </span>
        <span>{item.author}</span>
        <span>{item.num_comments}</span>
        <span>{item.points}</span>
      </div>
    );
  });
};
~~~~~~~

만약 화살표 함수의 내부가 하나의 구문으로 이루어진 경우(화살표 함수에서 반환값만 존재하는 경우), 함수의 **블록(block) 바디**(중괄호)를 제거할 수 있습니다. **간결한(concise) 바디**에서는 암시된 반환문을 포함하므로 반환문을 제거할 수 있습니다.

{title="Code Playground",lang="javascript"}
~~~~~~~
// 블록 바디 사용
count => {
  // perform any task in between

  return count + 1;
}

// 간결한 바디 사용
count =>
  count + 1;
~~~~~~~

이 작업은 App 및 List 컴포넌트에서도 적용할 수 있습니다. 애플리케이션 및 컴포넌트는 JSX만 반환할 뿐, 아무런 작업도 수행하지 않기 때문입니다. map 함수에서 사용하는 화살표 함수도 마찬가지입니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
# leanpub-start-insert
const App = () => (
# leanpub-end-insert
  <div>
    ...
  </div>
# leanpub-start-insert
);
# leanpub-end-insert

# leanpub-start-insert
const List = () =>
  list.map(item => (
# leanpub-end-insert
    <div key={item.objectID}>
      <span>
        <a href={item.url}>{item.title}</a>
      </span>
      <span>{item.author}</span>
      <span>{item.num_comments}</span>
      <span>{item.points}</span>
    </div>
# leanpub-start-insert
  ));
# leanpub-end-insert
~~~~~~~

이제 JSX는 함수 선언, 중괄호, 반환문을 생략했기 때문에 더욱 간결해졌습니다. 그러나 이 과정은 선택 사항일 뿐입니다. 화살표 함수 대신에 일반 함수를 사용해도 되고, 화살표 함수에서 중괄호를 사용해도 됩니다. 혹은 함수 시그니쳐와 반환문 사이에 더 많은 비즈니스 로직을 도입하기 위해 블록 본문이 필요할 수도 있습니다.

{title="Code Playground",lang="javascript"}
~~~~~~~
const App = () => {
  // 여기에서 세부 구현을 작업하세요

  return (
    <div>
      ...
    </div>
  );
};
~~~~~~~

앞으로 화살표 함수에서 블록 바디를 사용하지 않는 경우에 대해서는 빠르게 넘어갈 것이기 때문에 이 리팩터링 개념을 이해하고 넘어가세요. 물론 우리가 어떤 걸 사용할지는 컴포넌트의 요구 사항에 따라 다릅니다.

### 실습하기

* [마지막 장의 소스코드](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/React-Component-Definition)를 확인하세요.
  * [마지막 장의 변경 사항](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/Meet-another-React-Component...hs/React-Component-Definition?expand=1)을 확인하세요.
* [자바스크립트의 화살표 함수](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)에 해대 자세히 알아보세요.
* 화살표 함수에 친숙해지도록 연습해보세요. 블록 바디는 반환문과 같이, 간결한 바디는 반환문 없이 사용해보세요.

