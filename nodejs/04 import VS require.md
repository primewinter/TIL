## import VS require

웹팩에서 Import와 Require을 사용시 발생하는 차이점에 대해 간단히 알아보도록 하겠습니다. 아래와 같이 file1.js를 불러왔을 때, 특정 실제로 사용할 a값을 가져올 수 있으며 나머지값들은 웹팩의 tree shaking으로 인해 빌드에서 제거됩니다. 즉, 불필요한 파일을 제거함으로 코드량을 줄일 뿐만 아니라, 성능적으로도 더 좋습니다.

```
// file1.js
export {
  a: "a",
  b: "b",
  c: "c",
};// file2.js
import { a } from './file1';
console.log(a);
```

하지만, require을 사용하면 동적으로 모듈을 불러올 수 있지만, 불필요한 코드들까지 불러오기 때문에 실제로 어떤 코드가 사용되었는지 명확히 알 수가 없습니다.

```
import React from 'react';
import ReactDOM from 'react-dom';
import ReloadRoot from './components/ReloadRoot';
const render = () => {
  ReactDOM.render(
    <ReloadRoot />,
    document.getElementById('root')
  );
}render();if (module.hot) {
  module.hot.accept('./components/ReloadRoot', () => {
    require('./components/ReloadRoot').default;
    render();
  });
}
```

그렇기 때문에, ES2015에서 이 문제를 해결하기 위해 import를 사용합니다. babel-loader에서는 웹팩의 tree shaking 기능을 유지하기 위해 설정시 modules: false로 하면 됩니다.

출처 : https://medium.com/@shlee1353/webpack-웹팩-import-vs-require-차이점은-무엇일까-17948f6c919e

---

### 모듈 정의하기 (export)

**ES6**

```jsx
// 모듈 전체를 export, 파일내 한번만 사용가능하다.
var module = {};
export default module

// 모든 속성을 export
export *;

// 함수를 직접 export
export function moduleFunc() {};
var property = "some property";
export {property};`
```

**CommonJs**

```jsx
// 모듈 전체를 export
module.exports = module

// 모든 속성을 export
// (아시는 분 알려주세요)

// 함수를 직접 export
exports.moduleFunc = function() {}
```

### 모듈 가져오기 (import)

**ES6**

```jsx
// 모듈 전체를 import
import module
import module as myModule

// 모든 속성 import
import * from module

// 특정 멤버(함수 등)만 import
import {moduleFunc, moduleFunc2} from module
```

**CommonJs**

```jsx
// 모듈 전체를 import
var module = require('./someModule.js')

// 모든 속성 import
// (위의 module 객체에 모든 속성이 담아져 온다.)

// 특정 멤버(함수 등)만 import, 위의 module을 이용한다.
module.moduleFunc
```

출처 : [https://blueshw.github.io/2017/05/16/ES-require-vs-import/](https://blueshw.github.io/2017/05/16/ES-require-vs-import/)
