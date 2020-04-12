## 재사용이 가능한 리액트 컴포넌트

Search 컴포넌트를 좀 더 자세히 살펴봅시다. 라벨의 엘리먼트에는 "Search:"라는 텍스트가 있습니다. id/htmlFor 속성에는`search `라는 값을 갖는` search`식별자가 있습니다. 그리고  `onSearch`라는 콜백 함수도 있습니다. 이 컴포넌트들은 `search`와 밀접하게 관련되어 있어 다른 애플리케이션과 `search`를 하지 않는 작업에서는 재사용이 어렵습니다. 그뿐만 아니라 id/htmlFor 조합이 중복되어 있어 사용자가 두 라벨 중 하나를 클릭하면 포커스를 잃어버립니다. 때문에 Search 컴포넌트가 양쪽에서 렌더링 되면 버그를 일으킬 위험이 있습니다.

Search 컴포넌트가 실질적으로 "검색"기능을 갖고 있지 않기 때문에, search 도메인 속성들을 다른 애플리케이션에서도 재사용이 가능하도록 하는 것이 어렵지 않습니다. 추가적인 `id`와 `label` prop을 Search 컴포넌트로 넘겨줍니다. 그리고 실제 값과 콜백 함수 핸들러의 이름을 조금 더 추상적인 이름으로 바꾸고 컴포넌트의 이름도 함께 바꿔줍니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const App = () => {
 ...

 return (
   <div>
     <h1>My Hacker Stories</h1>

# leanpub-start-insert
     <InputWithLabel
       id="search"
       label="Search"
# leanpub-end-insert
       value={searchTerm}
# leanpub-start-insert
       onInputChange={handleSearch}
# leanpub-end-insert
     />

     ...
   </div>
 );
};

# leanpub-start-insert
const InputWithLabel = ({ id, label, value, onInputChange }) => (
# leanpub-end-insert
 <>
# leanpub-start-insert
   <label htmlFor={id}>{label}</label>
   &nbsp;
# leanpub-end-insert
   <input
# leanpub-start-insert
     id={id}
# leanpub-end-insert
     type="text"
     value={value}
# leanpub-start-insert
     onChange={onInputChange}
# leanpub-end-insert
   />
 </>
);
~~~~~~~

아직 완전하게 재사용이 가능하진 않습니다. 만약 숫자(`number`)나 전화번호(`tel`) 같은 데이터에 대한 입력 필드를 원하면, 외부에서도 입력 필드의 `type`속성에 접근할 수 있도록 해야 합니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const InputWithLabel = ({
 id,
 label,
 value,
# leanpub-start-insert
 type = 'text',
# leanpub-end-insert
 onInputChange,
}) => (
 <>
   <label htmlFor={id}>{label}</label>
   &nbsp;
   <input
     id={id}
# leanpub-start-insert
     type={type}
# leanpub-end-insert
     value={value}
     onChange={onInputChange}
   />
 </>
);
~~~~~~~

App 컴포넌트의 `type`  prop은 InputWithLabel 컴포넌트로 전달되지 않기 때문에 외부에서 명시되지 않아도 됩니다. 함수 서명의 [기본 매개변수](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Default_parameters)가 입력 필드를 대신합니다.

몇 개의 수정으로 Search 컴포넌트를 재사용성이 높은 컴포넌트로 만들었습니다.  내부 구현의 세부사항을 이름을 일반화했고, 새로운 컴포넌트에게 외부에서 필요한 모든 정보를 제공하는 큰 API를 주었습니다.

### 읽어보기:

* [지난 장의 소스코드](https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/Reusable-React-Component) 확인하기
 * [지난 장과 달라진 점](https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/React-Fragments...hs/Reusable-React-Component?expand=1) 확인하기
* [재사용이 가능한 컴포넌트]()에 대해 더 읽어보기
* 이제 "Search:" 텍스트에 ":"를 쓰기 전에 어떻게 처리를 해야 할까요? `label="Search` 를 prop으로 InputWithLabel 컴포넌트에게 전달할지 InputWithLabel 컴포넌트에서`<label htmlFor={id}>{label}:</label>`를 사용하고 하드코딩을 할까요? 이 내용은 나중에 살펴 보도록 하겠습니다.