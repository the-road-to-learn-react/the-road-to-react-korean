## 컴포넌트의 인스턴스화

다음으로, 리액트의 구성요소를 이해하기 위해 자바스크립트 클래스에 대해 간략하게 설명하겠습니다. 기술적으로는 크게 관련이 없지만, 컴포넌트의 개념을 이해하는 데에 도움이 될 것입니다.

클래스는 일반적으로 객체지향 프로그래밍 언어에서 사용합니다. 자바스크립트는 융통성과 유연성이 뛰어난 프로그래밍 언어로 함수형 프로그래밍과 객체지향 프로그래밍으로 모두 작성할 수 있습니다. 다음 *Developer* 클래스를 통해 자바스크립트의 클래스를 공부해봅시다.

{title="Code Playground",lang="javascript"}
~~~~~~~
class Developer {
  constructor(firstName, lastName) {
    this.firstName = firstName;
    this.lastName = lastName;
  }

  getName() {
    return this.firstName + ' ' + this.lastName;
  }
}
~~~~~~~

클래스에는 인스턴스화 할 수 있는 생성자(constructor)가 있습니다. 생성자는 매개변수를 사용해 클래스 인스턴스에 할당합니다. 또한 클래스는 함수를 정의할 수 있습니다(예: `getName()`). 이런 함수는 클래스와 연관되어 있어 **메서드(methods)** 또는 **클래스 메서드**로 불립니다.

Developer 클래스는 클래스 선언문일 뿐입니다. `new`를 사용하여 클래스를 호출해 클래스 내 여러 개의 인스턴스를 작성할 수 있습니다. 

{title="Code Playground",lang="javascript"}
~~~~~~~
// 클래스 정의
class Developer { ... }

// 클래스 인스턴스 생성
const robin = new Developer('Robin', 'Wieruch');

console.log(robin.getName());
// "Robin Wieruch"

// 새로운 클래스 인스턴스 생성
const dennis = new Developer('Dennis', 'Wieruch');

console.log(dennis.getName());
// "Dennis Wieruch"
~~~~~~~

자바스크립트 클래스가 정의되었다면, 한 개의 클래스는 여러 개의 인스턴스를 생성할 수 있습니다. 이는 컴포넌트 정의는 하나지만 인스턴스는 여러 개를 생성할 수 있는 리액트 컴포넌트와도 유사합니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
// App 컴포넌트 정의부
function App() {
  return (
    <div>
      <h1>My Hacker Stories</h1>

      <label htmlFor="search">Search: </label>
      <input id="search" type="text" />

      <hr />

      {/* List 컴포넌트 인스턴스 생성 */}
      <List />
      {/* List 컴포넌트 인스턴스 추가 */}
      <List />
    </div>
  );
}

// List 컴포넌트 정의부
function List() { ... }
~~~~~~~

**컴포넌트**를 한 번 정의했다면 JSX의 어느 곳에서나 HTML **엘레먼트(element)**처럼 사용할 수 있습니다. 이 엘레먼트는 컴포넌트의 인스턴스를 생성합니다. 컴포넌트를 사용하면 컴포넌트의 **인스턴스**가 만들어지는데, 다른 말로는 컴포넌트의 인스턴스화 라고도 합니다. 자바스크립트 클래스를 정의하고 사용하는 것과 크게 다르지 않습니다.

### 읽어보기

* *컴포넌트 선언*, *인스턴스*, *엘레먼트*라는 용어를 숙지하고 이들의 차이를 이해하세요.
* List 컴포넌트에 여러 개의 인스턴스를 생성해보세요.
* 각 List 컴포넌트가 고유의 `list`를 가지려면 어떻게 해야할지 생각해보세요.