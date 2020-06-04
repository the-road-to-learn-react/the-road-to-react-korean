## SVG 사용

최신 리액트 애플리케이션을 만들기 위해 SVG를 사용하는 것이 좋습니다. 모든 버튼 개체 텍스트를 만드는 대신 예를 들면 여러분들은 아이콘으로 좀 더 가볍게 만들 수 있습니다. 이번에는 리액트 컴포넌트 중 하나인 확장 가능한 그래픽(SVG, scalable vector graphic)을 사용해 보겠습니다. 

이번 장은 SVG 아이콘을 더 멋지고 정확하게 사용할 수 있도록 하는 이전에 다뤘던 "리액트에서의 CSS"를 기반으로 합니다. 다른 스타일링이나 혹은 전혀 꾸미지 않아도 되며 SVG는 꾸미기 없이도 괜찮습니다. 

이 SVG 아이콘은 [플랫아이콘 무료 사이트](https://www.flaticon.com/authors/freepik)에 있습니다. 이 사이트의 많은 SVG는 원작자를 남기면 무료로 사용할 수 있습니다. [이 곳에서](https://www.flaticon.com/free-icon/check_109748) SVG로 아이콘을 다운로드할 수 있으며 프로젝트 *src/check.svg* 파일에 적용하면 됩니다. 이 파일을 다운로드하는 것이 좋으나 더 자세히 알기 위해 SVG 정의를 살펴보면 아래와 같습니다.

{title="Code Playground",lang="html"}
~~~~~~~
<?xml version="1.0" encoding="iso-8859-1"?>
<!-- Generator: Adobe Illustrator 18.0.0, SVG Export Plug-In . SVG Version: 6.00 Build 0)  -->
<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" "http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">
<svg version="1.1" id="Capa_1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px"
   viewBox="0 0 297 297" style="enable-background:new 0 0 297 297;" xml:space="preserve">
  <g>
    <path d="M113.636,272.638c-2.689,0-5.267-1.067-7.168-2.97L2.967,166.123c-3.956-3.957-3.956-10.371-0.001-14.329l54.673-54.703
      c1.9-1.9,4.479-2.97,7.167-2.97c2.689,0,5.268,1.068,7.169,2.969l41.661,41.676L225.023,27.332c1.9-1.901,4.48-2.97,7.168-2.97l0,0
      c2.688,0,5.268,1.068,7.167,2.97l54.675,54.701c3.956,3.957,3.956,10.372,0,14.328L120.803,269.668
      C118.903,271.57,116.325,272.638,113.636,272.638z M24.463,158.958l89.173,89.209l158.9-158.97l-40.346-40.364L120.803,160.264
      c-1.9,1.902-4.478,2.971-7.167,2.971c-2.688,0-5.267-1.068-7.168-2.97l-41.66-41.674L24.463,158.958z"/>
  </g>
</svg>
~~~~~~~

create-react-app을 다시 쓰기 때문에 바로 리액트 컴포넌트로 CSS와 비슷하게 SVG를 가져올 수 있습니다. *src/App.js*에서 SVG를 가져오기 위해 아래 문법을 사용합니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
import React from 'react';
import axios from 'axios';

import './App.css';
# leanpub-start-insert
import { ReactComponent as Check } from './check.svg';
# leanpub-end-insert
~~~~~~~

SVG를 가져와서 로고, 배경 등 다양한 용도로 활용할 수 있습니다. 버튼에 텍스트 대신 'height'와 'width' 속성이 있는 SVG 컴포넌트를 사용할 수 있습니다.

{title="src/App.js",lang="javascript"}
~~~~~~~
const Item = ({ item, onRemoveItem }) => (
  <div className="item">
    <span style={{ width: '40%' }}>
      <a href={item.url}>{item.title}</a>
    </span>
    <span style={{ width: '30%' }}>{item.author}</span>
    <span style={{ width: '10%' }}>{item.num_comments}</span>
    <span style={{ width: '10%' }}>{item.points}</span>
    <span style={{ width: '10%' }}>
      <button
        type="button"
        onClick={() => onRemoveItem(item)}
        className="button button_small"
      >
# leanpub-start-insert
        <Check height="18px" width="18px" />
# leanpub-end-insert
      </button>
    </span>
  </div>
);
~~~~~~~

여러분이 사용하는 스타일링 기법에 상관없이 SVG 아이콘 버튼에 마우스 오버 효과도 줄 수 있습니다. 기본 CSS 기법에서 *src/App.css* 파일에서 아래와 같이 표현할 수 있습니다.

{title="src/App.css",lang="css"}
~~~~~~~
.button:hover > svg > g {
  fill: #ffffff;
  stroke: #ffffff;
}
~~~~~~~

create-react-app 프로젝트에서 별도의 설정 없이 SVG를 쉽게 사용할 수 있습니다. 하지만 여러분이 웹팩 같은 빌드 도구와 함께 리액트 프로젝트를 처음부터 만든다면 여러분이 직접 관리해야 하므로 다릅니다. SVG는 여러분의 애플리케이션을 좀 더 사용하기 쉽게 만들어 주기 때문에 적극적으로 사용하길 권장합니다.

### 실습하기

* 마지막 장의 [소스 코드]를 확인합니다. (https://codesandbox.io/s/github/the-road-to-learn-react/hacker-stories/tree/hs/CSS-in-React-SVG)
* 마지막 장에서 [변경된 코드]를 확인합니다. (https://github.com/the-road-to-learn-react/hacker-stories/compare/hs/CSS-in-React...hs/CSS-in-React-SVG?expand=1)
* [리액트 앱 만들기 속 SVG]에 대해 더 알아보세요. (https://create-react-app.dev/docs/adding-images-fonts-and-files)
* [리액트 속 SVG 배경 패턴]에 대해 더 알아보세요. (https://www.robinwieruch.de/react-svg-patterns)
* 다른 SVG 아이콘을 애플리케이션에 적용해보세요.
