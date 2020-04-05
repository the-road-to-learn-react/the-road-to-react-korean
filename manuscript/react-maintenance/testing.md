## 유닛 테스트에서 통합 테스트까지

소스 코드를 테스팅하는 것은 개발의 필수적인 과정이고, 개발을 진지하게 생각하는 사람이라면 반드시 익혀야 할 스킬입니다. 코드의 질과 성능을 확인하는 것은 코드를 실제로 배포하기 전에 거쳐야 할 과정입니다. 여기에서는 [테스팅 피라미드](https://martinfowler.com/articles/practical-test-pyramid.html)를 기준 삼아 이야기하도록 하겠습니다.

테스팅 피라미드는 종단간 테스트, 통합 테스트, 그리고 유닛 테스트를 포함합니다. 유닛 테스트는 함수나 컴포넌트처럼 짧고, 따로 분리 가능 코드를 테스트할 때 사용합니다. 통합 테스트는 이러한 유닛들이 함께 잘 작동하는지 확인하기 위해 사용합니다. 마지막으로 종단간 테스트는 웹 어플리케이션에서의 로그인 플로우와 같이, 실제 일어날 법한 시나리오를 모방합니다. 유닛 테스트는 쉽고 빠르게 작성하고 유지할 수 있지만, 종단간 테스트는 정반대입니다.

유닛 테스트는 여러 함수와 컴포넌트를 모두 테스트해야 하니, 많은 수가 필요합니다. 그 다음에는, 가장 중요한 함수와 컴포넌트들이 함께 잘 작동하는지 확인하기 위해 통합 테스트를 사용합니다. 마지막으로 우리는 몇 가지 중요한 시나리오를 모방해 보기 위해 몇 개의 종단간 테스트를 작성할 필요가 있을 수도 있습니다. 이 학습 경험에서는 **유닛 테스트와 통합 테스트**를 다룰 예정이고, 이에 더불어 컴포넌트에 특화된 테스팅 기술인 **스냅샷 테스트**에 대해서도 배울 예정입니다. **종단간 테스트**는 exercise에 포함되어 있습니다.

이미 [테스팅 라이브러리들](https://www.robinwieruch.de/react-testing-tutorial)이 많이 존재하기 때문에, 리액트 초심자들은 사용할 라이브러리를 고르는 데 어려움을 겪을 수도 있습니다. 우리는 이 튜토리얼에서 너무 강한 의견을 피력하는 것을 피하기 위해, 페이스북에서 개발한 [Jest](https://jestjs.io/)를 테스팅 프레임워크로 활용하겠습니다. 다른 리액트 테스팅 라이브러리들 또한 Jest를 기반으로 개발된 것이 많기 때문에, 입문용으로는 더욱 좋습니다.

### 유닛 테스트와 통합 테스트

유닛 테스트와 통합 테스트의 차이를 구분하기 어려운 경우도 여럿 있습니다. 예를 들어, Item 컴포넌트를 담고 있는 List 컴포넌트를 테스팅하고자 한다면, 이는 통합 테스트라고 볼 수도 있겠지만, 밀접하게 연관된 두 개의 컴포넌트 사이의 유닛 테스트일 수도 있겠죠. 이 섹션에서는 유닛 테스트에서 시작해서, 통합 테스트를 향해 나아가 보도록 하겠습니다. 그 과정에서 마주하는 모든 것들은 이 양 극단 사이의 스펙트럼입니다.

*src/App.test.js* 에 간단한 테스트 양식을 적는 것으로 시작해보도록 하겠습니다.

{title="src/App.test.js",lang="javascript"}
~~~~~~~
describe('something truthy', () => {
  it('true to be true', () => {
    expect(true).toBe(true);
  });
});
~~~~~~~

다행히도 create-react-app에는 Jest가 미리 설치되어 있기 때문에, 커맨드 라인에서 create-react-app의 테스트 스크립트를 실행하여 테스팅을 진행할 수 있습니다. 아래 명령어를 실행하면, 모든 테스트 케이스의 테스트 결과가 커맨드 라인에 출력됩니다.

{title="Command Line",lang="text"}
~~~~~~~
npm test
~~~~~~~

테스트 스크립트를 실행하면, Jest는 파일명이 *test.js*로 끝나는 모든 파일을 확인합니다. 성공적으로 통과한 테스트는 초록색으로 표시되고, 실패한 테스트들은 빨간색으로 표시됩니다.

{title="src/App.test.js",lang="javascript"}
~~~~~~~
describe('something truthy', () => {
  it('true to be true', () => {
    expect(true).toBe(false);
  });
});
~~~~~~~

Jest의 테스트는 기본적인 상위 구조인 **테스트 스위트** (`describe`)로 이루어져 있고, 각각의 스위트는 **테스트 케이스** (`it`)의 집합으로 구성되며, 각각의 테스트 케이스는 다시 여러 **단언** (`expect`)으로 나뉩니다. 테스트 실행 시 빨간색이나 초록색으로 결과를 표시합니다.

{title="src/App.test.js",lang="javascript"}
~~~~~~~
// test suite
describe('truthy and falsy', () => {
  // test case
  it('true to be true', () => {
    // test assertion
    expect(true).toBe(true);
  });

  // test case
  it('false to be false', () => {
    // test assertion
    expect(false).toBe(false);
  });
});
~~~~~~~

"it" 블록은 한 개의 테스트 케이스를 나타냅니다. "it"문을 쓸 때는 테스트 성공 혹은 실패를 나타낼 설명을 함께 작성해주어야 합니다. 한 컴포넌트에 대한 테스트 케이스가 여러 개 있다면, "describe" 블록을 사용하여 이 케이스들을 하나의 테스트 스위트로 엮을 수 있습니다. 이 두 가지 블록들은 테스트 케이스를 정리하고, 가독성을 높이기 위해 사용합니다. 한 가지 유의할 점은, 자바스크립트 커뮤니티에서는 `it`을 단일 테스트 케이스 함수로 사용하지만, Jest에서는 `test` 함수에 대한 대체 명령어로 사용한다는 것입니다.

{title="src/App.test.js",lang="javascript"}
~~~~~~~
describe('something truthy', () => {
# leanpub-start-insert
  test('true to be true', () => {
# leanpub-end-insert
    expect(true).toBe(false);
  });
});
~~~~~~~

Jest에서 리액트 컴포넌트를 활용하려면, 컴포넌트를 테스트 환경에서 렌더링하기 위한 라이브러리를 별도로 설치해야 합니다.

{title="Command Line",lang="text"}
~~~~~~~
npm install react-test-renderer --save-dev
~~~~~~~

컴포넌트를 테스팅하려면 먼저 *src/App.js* 파일에서 작성한 컴포넌트들을 export해주어야 합니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
...

export default App;

# leanpub-start-insert
export { SearchForm, InputWithLabel, List, Item };
# leanpub-end-insert
~~~~~~~

방금 설치한 유틸리티 라이브러리와 함께 *src/App.test.js* 파일에 컴포넌트를 import해 줍니다.

{title="src/App.test.js",lang="javascript"}
~~~~~~~
# leanpub-start-insert
import React from 'react';
import renderer from 'react-test-renderer';

import App, { Item, List, SearchForm, InputWithLabel } from './App';
# leanpub-end-insert
~~~~~~~

Item 컴포넌트의 첫 번째 컴포넌트 테스트를 작성합니다. 이 테스트 케이스는 유틸리티 라이브러리를 사용하여, 특정 `item`을 기반으로 컴포넌트를 렌더링 합니다.

{title="src/App.test.js",lang="javascript"}
~~~~~~~
import React from 'react';
import renderer from 'react-test-renderer';

import App, { Item, List, SearchForm, InputWithLabel } from './App';

# leanpub-start-insert
describe('Item', () => {
  const item = {
    title: 'React',
    url: 'https://reactjs.org/',
    author: 'Jordan Walke',
    num_comments: 3,
    points: 4,
    objectID: 0,
  };

  it('renders all properties', () => {
    const component = renderer.create(<Item item={item} />);

    expect(component.root.findByType('a').props.href).toEqual(
      'https://reactjs.org/'
    );
  });
});
# leanpub-end-insert
~~~~~~~

컴포넌트 혹은 element의 속성에 대한 정보는 `props`를 통해 확인할 수 있습니다. 이 테스트 단언에서 우리는 `a` 태그를 찾고, 해당 태그의 `href` 속성을 추출한 후 일치 여부를 확인합니다. 테스트 결과가 초록색이면, `a` 태그의 `href` 속성이 `item`의 `url` prop과 일치한다는 것을 확인할 수 있습니다. 같은 테스트 케이스 안에서, 다른 속성을 확인하기 위해 테스트 단언을 여러 개 추가할 수도 있습니다.

{title="src/App.test.js",lang="javascript"}
~~~~~~~
describe('Item', () => {
  const item = {
    title: 'React',
    url: 'https://reactjs.org/',
    author: 'Jordan Walke',
    num_comments: 3,
    points: 4,
    objectID: 0,
  };

  it('renders all properties', () => {
    const component = renderer.create(<Item item={item} />);

    expect(component.root.findByType('a').props.href).toEqual(
      'https://reactjs.org/'
    );

# leanpub-start-insert
    expect(
      component.root.findAllByType('span')[1].props.children
    ).toEqual('Jordan Walke');
# leanpub-end-insert
  });
});
~~~~~~~

이 컴포넌트에는 `span` 객체가 여러 개 있기 때문에, 테스트를 위해서 우리는 모든 `span` 객체를 찾은 후, 두 번째 항목을 선택하여 (숫자를 0부터 세고 있기 때문에 인덱스는 `1`입니다.) 리액트 `children` 속성을 item의 `author` 속성과 비교합니다. 다만, 이 테스트는 엄밀한 테스트는 아닙니다. `span` 객체의 순서가 바뀌면 이 테스트는 실패합니다. 이와 같은 오류를 방지하기 위해, 단언을 다음과 같이 바꿀 수 있습니다.

{title="src/App.test.js",lang="javascript"}
~~~~~~~
describe('Item', () => {
  const item = { ... };

  it('renders all properties', () => {
    ...

# leanpub-start-insert
    expect(
      component.root.findAllByProps({ children: 'Jordan Walke' })
        .length
    ).toEqual(1);
# leanpub-end-insert
  });
});
~~~~~~~

이 수정된 테스트 단언은 앞선 단언보다 덜 구체적입니다. 이 경우에는 item의 `author` 속성을 가지고 있는 객체가 존재하는지만 확인합니다. Item의 나머지 속성들을 직접 확인해보고자 한다면, 이 방식을 사용하면 됩니다. 아닐 경우에는 이후 예제를 위해 남겨 두세요.

우리는 Item 컴포넌트가 텍스트나 HTML 속성(`href`)을 잘 렌더링하는지는 확인했지만, 콜백 핸들러를 확인하지는 않았습니다. 다음에 보이는 테스트 케이스는 `button` 객체의 `onClick` 속성을 모방함으로서 클릭 이벤트를 실행하고, 단언을 제시합니다.

{title="src/App.test.js",lang="javascript"}
~~~~~~~
describe('Item', () => {
  const item = { ... };

  it('renders all properties', () => {
    ...
  });

# leanpub-start-insert
  it('calls onRemoveItem on button click', () => {
    const handleRemoveItem = jest.fn();

    const component = renderer.create(
      <Item item={item} onRemoveItem={handleRemoveItem} />
    );

    component.root.findByType('button').props.onClick();

    expect(handleRemoveItem).toHaveBeenCalledTimes(1);
    expect(handleRemoveItem).toHaveBeenCalledWith(item);

    expect(component.root.findAllByType(Item).length).toEqual(1);
  });
# leanpub-end-insert
});
~~~~~~~

Jest는 Item 컴포넌트에 테스트 전용 함수를 prop으로 전달할 수 있게 해 줍니다. 이와 같은 테스트 전용 함수들은 **spy**, **stub**, 혹은 **mock** 이라고 불리고, 서로 각기 다른 테스트 시나리오에서 사용됩니다. `jest.fn()` 함수는 실제 함수의 복제품인 *mock*을 리턴하고, 함수가 언제 호출되었는지를 참고할 수 있게 해 줍니다. 이 덕분에 우리는 Jest에서 함수가 호출된 횟수를 측정해 주는 `toHaveBeenCalledTimes`나, 함수 호출 시 사용된 변수가 무엇인지 알려주는 `toHaveBeenCalledWith`와 같은 단언들을 사용할 수 있습니다.

앞에서 우리는 Item 컴포넌트의 입력(`item`)과 출력(`onRemoveItem`) 기능을 모두 확인했고, 유닛 테스트가 완료되었습니다. 이 입출력 결과는 따로 테스팅한 함수형 컴포넌트의 입력(변수)와 출력(JSX)과는 별개의 개념입니다. 마지막으로, 공유된 setup 함수를 제공하여 테스트 스위트 코드의 가독성을 조금 더 높일 수 있습니다.

{title="src/App.test.js",lang="javascript"}
~~~~~~~
describe('Item', () => {
  const item = { ... };
# leanpub-start-insert
  const handleRemoveItem = jest.fn();
# leanpub-end-insert

# leanpub-start-insert
  let component;
# leanpub-end-insert

# leanpub-start-insert
  beforeEach(() => {
    component = renderer.create(
      <Item item={item} onRemoveItem={handleRemoveItem} />
    );
  });
# leanpub-end-insert

  it('renders all properties', () => {
    expect(component.root.findByType('a').props.href).toEqual(
      'https://reactjs.org/'
    );

    ...
  });

  it('calls onRemoveItem on button click', () => {
    component.root.findByType('button').props.onClick();

    ...
  });
});
~~~~~~~

테스트 내에서 공유된 setup 함수(혹은 teardown 함수)는 중복 코드를 제거해 주는 역할을 합니다. 각각의 테스트 케이스에 대해 컴포넌트를 렌더링해야 한다는 점이 일치하고, props 또한 같기 때문에 setup 함수 하나로 코드를 공유할 수 있습니다. 이 다음부터는 List 컴포넌트로 넘어가겠습니다.

{title="src/App.test.js",lang="javascript"}
~~~~~~~
...

describe('Item', () => {
  ...
});

# leanpub-start-insert
describe('List', () => {
  const list = [
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

  it('renders two items', () => {
    const component = renderer.create(<List list={list} />);

    expect(component.root.findAllByType(Item).length).toEqual(2);
  });
});
# leanpub-end-insert
~~~~~~~

이 테스트는 단순히 리스트 내의 두 항목에 의해 Item 컴포넌트 두 개가 만들어졌는지 확인합니다. 이 다음에는 콜백 핸들러 함수(`onRemoveItem`)가 각각의 Item 컴포넌트에서 불리는지 확인해야 하는데, 앞서 Item 컴포넌트에서와 비슷한 방식으로 확인하면 됩니다. 그럼 이 테스트는 유닛 테스트일까요, 아니면 통합 테스트일까요?

이 질문을 염두에 두고, 다음은 InputWithLabel 컴포넌트의 SearchForm으로 넘어가겠습니다.

{title="src/App.test.js",lang="javascript"}
~~~~~~~
# leanpub-start-insert
describe('SearchForm', () => {
  const searchFormProps = {
    searchTerm: 'React',
    onSearchInput: jest.fn(),
    onSearchSubmit: jest.fn(),
  };

  let component;

  beforeEach(() => {
    component = renderer.create(<SearchForm {...searchFormProps} />);
  });

  it('renders the input field with its value', () => {
    const value = component.root.findByType(InputWithLabel).props
      .value;

    expect(value).toEqual('React');
  });
});
# leanpub-end-insert
~~~~~~~

이 테스트에서는 InputWithLabel 컴포넌트가 SearchForm 컴포넌트에서 올바른 prop을 전달받는지를 확인합니다. 다르게 말한다면, 이 테스트는 InputWithLabel 컴포넌트의 인터페이스(props)만 테스트하기 때문에 테스트가 InputWithLabel 컴포넌트가 렌더링되기 전에 끝난다는 뜻입니다. 그럼에도 불구하고 인터페이스를 그대로 유지하면서도 InputWithLabel 컴포넌트의 구조가 바뀔 수 있기 때문에 이 테스트는 여전히 유닛 테스트라고 할 수 있습니다. 이미 모든 컴포넌트들이 렌더링되어 있기 때문에, InputWithLabel의 input 필드로 입력값을 받는 방식으로 테스트를 수정할 수도 있습니다.

{title="src/App.test.js",lang="javascript"}
~~~~~~~
describe('SearchForm', () => {
  ...

  it('renders the input field with its value', () => {
# leanpub-start-insert
    const value = component.root.findByType('input').props.value;
# leanpub-end-insert

    expect(value).toEqual('React');
  });
});
~~~~~~~

이것은 우리의 첫 번째 통합 테스트입니다. SearchForm 컴포넌트와 InputWithLabel 컴포넌트는 List와 Item 컴포넌트처럼 관계가 밀접하지는 않은데요,  InputWithLabel 컴포넌트는 재사용성이 높기 때문에 여러 다른 컴포넌트에서도 사용할 수 있지만, Item 컴포넌트는 List 컴포넌트 내에서만 사용할 수 있기 때문입니다.

{title="src/App.test.js",lang="javascript"}
~~~~~~~
describe('SearchForm', () => {
  const searchFormProps = {
    searchTerm: 'React',
    onSearchInput: jest.fn(),
    onSearchSubmit: jest.fn(),
  };

  ...

# leanpub-start-insert
  it('changes the input field', () => {
    const pseudoEvent = { target: 'Redux' };

    component.root.findByType('input').props.onChange(pseudoEvent);

    expect(searchFormProps.onSearchInput).toHaveBeenCalledTimes(1);
    expect(searchFormProps.onSearchInput).toHaveBeenCalledWith(
      pseudoEvent
    );
  });

  it('submits the form', () => {
    const pseudoEvent = {};

    component.root.findByType('form').props.onSubmit(pseudoEvent);

    expect(searchFormProps.onSearchSubmit).toHaveBeenCalledTimes(1);
    expect(searchFormProps.onSearchSubmit).toHaveBeenCalledWith(
      pseudoEvent
    );
  });
# leanpub-end-insert
});
~~~~~~~

Item 컴포넌트에서 했던 것처럼, 앞선 두 개의 테스트는 컴포넌트의 콜백 핸들러를 확인합니다. 모든 입력(함수가 아닌 props)과 출력 (콜백 핸들러 함수) props는 SearchForm 컴포넌트의 인터페이스에서 잘 작동하는지, 그리고 InputWithLabel 컴포넌트와의 관계에서 잘 통합되는지 테스트를 거치게 됩니다.

버튼이 비활성화된 경우 등의 엣지 케이스를 확인해볼 수도 있습니다. 테스트 컴포넌트 내의 `update()` 함수를 사용하면 컴포넌트에 새로운 props를 제공할 수 있습니다.

{title="src/App.test.js",lang="javascript"}
~~~~~~~
describe('SearchForm', () => {
  const searchFormProps = {
    searchTerm: 'React',
    onSearchInput: jest.fn(),
    onSearchSubmit: jest.fn(),
  };

  let component;

  beforeEach(() => {
    component = renderer.create(<SearchForm {...searchFormProps} />);
  });

  ...

# leanpub-start-insert
  it('disables the button and prevents submit', () => {
    component.update(
      <SearchForm {...searchFormProps} searchTerm="" />
    );

    expect(
      component.root.findByType('button').props.disabled
    ).toBeTruthy();
  });
# leanpub-end-insert
});
~~~~~~~

이 다음에는 한 단계 위의 컴포넌트를 다루겠습니다. App 컴포넌트는 리스트 데이터를 불러와서 List 컴포넌트에 제공해 줍니다. App 컴포넌트를 불러온 후, 아래와 같이 테스트를 작성합니다.

{title="src/App.test.js",lang="javascript"}
~~~~~~~
# leanpub-start-insert
describe('App', () => {
  it('succeeds fetching data with a list', () => {
    const list = [
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

    const component = renderer.create(<App />);

    expect(component.root.findByType(List).props.list).toEqual(list);
  });
});
# leanpub-end-insert
~~~~~~~

실제 App 컴포넌트에서 우리는 외부 라이브러리(axios)를 활용하여 외부 API에 요청을 보냅니다. 이 API 요청은 우리가 테스트에서 예측할 수 없는 데이터를 반환하므로, 여기에서는 이 요청을 모방(mock)해야 합니다. Jest에는 이와 같이 라이브러리와 라이브러리 내 함수들을 모방할 수 있는 방법들을 제공합니다. 이 경우에서 우리는 axios에서 데이터를 반환하는 역할을 하는 `get()` 함수를 모방하고자 합니다.

{title="src/App.test.js",lang="javascript"}
~~~~~~~
import React from 'react';
import renderer from 'react-test-renderer';
# leanpub-start-insert
import axios from 'axios';
# leanpub-end-insert

# leanpub-start-insert
jest.mock('axios');
# leanpub-end-insert

...

describe('App', () => {
  it('succeeds fetching data with a list', () => {
    const list = [ ... ];

# leanpub-start-insert
    const promise = Promise.resolve({
      data: {
        hits: list,
      },
    });
# leanpub-end-insert

# leanpub-start-insert
    axios.get.mockImplementationOnce(() => promise);
# leanpub-end-insert

    const component = renderer.create(<App />);

    expect(component.root.findByType(List).props.list).toEqual(list);
  });
});
~~~~~~~

이 테스트는 순차적으로 진행되지만, 데이터는 비동기적으로 반환됩니다. 이 컴포넌트는 state가 달라지면 다시 렌더링되어야 하는데, 이는 유틸리티 라이브러리와 async/await를 활용하여 해결할 수 있습니다.

{title="src/App.test.js",lang="javascript"}
~~~~~~~
describe('App', () => {
# leanpub-start-insert
  it('succeeds fetching data with a list', async () => {
# leanpub-end-insert
    const list = [ ... ];

    const promise = Promise.resolve({
      data: {
        hits: list,
      },
    });

    axios.get.mockImplementationOnce(() => promise);

# leanpub-start-insert
    let component;

    await renderer.act(async () => {
      component = renderer.create(<App />);
    });
# leanpub-end-insert

    expect(component.root.findByType(List).props.list).toEqual(list);
  });
});
~~~~~~~

App 컴포넌트를 렌더링하는 대신, 우리는 데이터를 반환하는 함수를 모방함으로서 외부 API가 반환할 응답을 모방합니다. 데이터가 성공적으로 반환되는 경우에 대해서, 우리는 테스트로 하여금 우리의 컴포넌트가 비동기적으로 업데이트되는 컴포넌트라고 인지하게 만듭니다. API 호출에 실패하는 경우에 대해서도 비슷한 방식으로 확인할 수 있습니다.

{title="src/App.test.js",lang="javascript"}
~~~~~~~
describe('App', () => {
  it('succeeds fetching data with a list', async () => {
    ...
  });

# leanpub-start-insert
  it('fails fetching data with a list', async () => {
    const promise = Promise.reject();

    axios.get.mockImplementationOnce(() => promise);

    let component;

    await renderer.act(async () => {
      component = renderer.create(<App />);
    });

    expect(component.root.findByType('p').props.children).toEqual(
      'Something went wrong ...'
    );
  });
# leanpub-end-insert
});
~~~~~~~

이제 외부 API를 활용하여 데이터를 호출하고, 통합하는 부분이 완료되었습니다. 여기에서 우리는 단순한 유닛 테스트에서 더 나아가서, 여러 컴포넌트를 동시에 테스팅하고, 외부 라이브러리나 API와 엮여 있는 부분을 테스팅할 수 있는 방법도 배웠습니다.

### 스냅샷 테스팅

이에 더불어, Jest는 렌더링 완료된 컴포넌트의 **스냅샷**을 찍을 수 있게 해 주는데요, 이는 이후의 스냅샷과 비교하여 변화를 감지하는 역할을 합니다. 원하는 결과에 따라서 이와 같은 변화를 허용할 수도, 거부할 수도 있습니다. 이 방식은 유닛 테스트와 통합 테스트와도 함께 사용될 수 있는데요, 여러 관리 비용을 지불하지 않고도 출력 값 자체만을 비교할 수 있는 방법을 제공하기 때문입니다. 실제로 어떻게 작동하는지 확인하려면 Item 컴포넌트의 테스트 스위트에 새로운 스냅샷 테스트를 추가하면 됩니다.

{title="src/App.test.js",lang="javascript"}
~~~~~~~
describe('Item', () => {
  ...

  beforeEach(() => {
    component = renderer.create(
      <Item item={item} onRemoveItem={handleRemoveItem} />
    );
  });

  ...

# leanpub-start-insert
  test('renders snapshot', () => {
    let tree = component.toJSON();
    expect(tree).toMatchSnapshot();
  });
# leanpub-end-insert
});
~~~~~~~

테스트를 다시 돌려 보고, 성공하는지, 실패하는지를 확인해 보세요. *src/App.js* 에서 Item 컴포넌트의 HTML 구조를 바꾸는 등 변화를 줘서 출력값을 바꾼다면, 스냅샷 테스트는 실패합니다. 이 다음에는, 스냅샷을 업데이트할 지, Item 컴포넌트를 확인할 지 결정할 수 있습니다.

Jest는 이후 스냅샷 테스트와의 비교를 위해 스냅샷을 한 폴더 안에 저장합니다. 사용자들은 버전 관리(git 등)을 위해 여러 팀 간에 이와 같은 스냅샷들을 공유할 수도 있습니다. 스냅샷 테스트를 처음 실행하면, 프로젝트 폴더 안에 스냅샷 파일이 생성됩니다. 테스트를 다시 실행하면 이 스냅샷은 직전 테스트 결과와 일치하는지 여부를 확인하게 됩니다. 이와 같은 절차를 통해 DOM이 유지되는 것을 보장할 수 있습니다.

### 실습하기:

* [마지막 장의 소스 코드](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/react-testing)를 확인하세요.
  * [마지막 장의 변경 사항](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/react-modern-final...hs/react-testing?expand=1)을 확인하세요.
* 모든 컴포넌트에 대해 스냅샷 테스트를 하나씩 작성하세요.
* [리액트 컴포넌트 테스트](https://www.robinwieruch.de/react-testing-tutorial)에 대해 더 알아봅니다.
  * 유닛 테스트, 통합 테스트, 스냅샷 테스트에 더 알아보기 위해 [Jest](https://jestjs.io/) 와 [Jest for React](https://www.robinwieruch.de/react-testing-jest/)를 활용할 수 있습니다.
* [리액트 종단간 테스트](https://www.robinwieruch.de/react-testing-cypress)에 대해 더 알아봅니다.
* 다음에 나올 내용을 학습하면서, 계속 테스트 결과를 초록색으로 유지하고, 필요하다고 느낄 때마다 새 테스트를 작성해 줍시다.