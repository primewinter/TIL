[popping-journal 프로젝트]

오늘의 목표는 server쪽 구조의 큰 틀을 잡는 것이었다. express-generator를 이용하지 않고 다른 프로젝트들의 폴더구조를 참고해서 만들기로 했다. 오류가 너무 많이 났다. 기본기가 많이 부족하다는 것을 느꼈다.

### 오류1 : npm start 실패

```bash
$ npm start

> server@1.0.0 start
> node app.js

internal/modules/cjs/loader.js:883
  ^

Error: Cannot find module 'C:\dev\js\popping-journal\server\app.js'
    at Function.Module._resolveFilename (internal/modules/cjs/loader.js:880:15)
    at Function.Module._load (internal/modules/cjs/loader.js:725:27)
    at Function.executeUserEntryPoint [as runMain] (internal/modules/run_main.js:72:12)
    at internal/main/run_main_module.js:17:47 {
  code: 'MODULE_NOT_FOUND',
  requireStack: []
}
```

- **원인**

    경로 설정이 잘못되었다. app.js는 server\src 아래에 있었는데 잘못된 경로에서 찾고 있었다.

- **해결**

    package.json 의 "scripts"의 "start"를 다음과 같이 수정하였다. ( "src/" 추가 )

    ```bash
    "start": "node src/app.js"
    ```

### 오류2

```bash
$ npm start

> server@1.0.0 start
> node src/app.js

(node:16108) Warning: To load an ES module, set "type": "module" in the package.json or use the .mjs extension.
(Use `node --trace-warnings ...` to show where the warning was created)
C:\dev\js\popping-journal\server\src\app.js:1
^^^^^^

SyntaxError: Cannot use import statement outside a module
    at wrapSafe (internal/modules/cjs/loader.js:979:16)
    at Module._compile (internal/modules/cjs/loader.js:1027:27)
    at Object.Module._extensions..js (internal/modules/cjs/loader.js:1092:10)
    at Module.load (internal/modules/cjs/loader.js:928:32)
    at Function.Module._load (internal/modules/cjs/loader.js:769:14)
    at Function.executeUserEntryPoint [as runMain] (internal/modules/run_main.js:72:12)
    at internal/main/run_main_module.js:17:47
```

- **원인 (출처 :** [https://www.daleseo.com/js-node-es-modules/](https://www.daleseo.com/js-node-es-modules/) )

    CommonJS를 모듈 시스템을 채택했던 Node.js에서는 import, export와 같은 ES 모듈을 사용하려면 Babel과 같은 트랜스파일러(transpiler)를 사용했어야 했는데, Node.js 버전 13.2부터 ES 모듈 시스템에 대한 정식 지원이 시작됨에 따라 다른 도구 없이 Node.js에서 손쉽게 ES 모듈을 사용할 수 있게 되었다.

    기존에 require("모듈명");로 사용하던 코드가 import "가져올 것의 이름" from "모듈명"; 로 바뀌는데 주의할 점이 있다. Node.js에서 import 키워드로 프로젝트 내부 모듈을 불러올 때는 반드시 확장자까지 포함해서 경로를 명시를 해줘야 한다. 이는 브라우저에서 import가 작동하는 방식과 맞추기 위해서 의도적으로 설계된 부분이라고 한다.

- **해결**

    Node.js에서 ES 모듈을 사용하는 다른 방법은 `package.json` 파일 설정을 통해 전체 파일에 적용하는 것이다. 모든 파일의 확장자를 일일이 바꾸지 않고, 프로젝트 전체에 ES 모듈을 적용하고 싶을 때 적합한 방법이다.

    먼저 프로젝트의 `package.json` 파일을 열고, 최상위에 `type` 항목을 `module`로 설정한다.

    package.json에 "type"을 추가하였다.

    ```jsx
    {
    	...
    	"type": "module"
    }
    ```

### 오류3: import db from "db" vs import db from "db.js"

```bash
$ npm start

> server@1.0.0 start
> node src/app.js

internal/process/esm_loader.js:74
    internalBinding('errors').triggerUncaughtException(
                              ^
Error [ERR_MODULE_NOT_FOUND]: Cannot find module 'C:\dev\js\popping-journal\server\src\db' imported from C:\dev\js\popping-journal\server\src\app.js
    at finalizeResolution (internal/modules/esm/resolve.js:276:11)
    at moduleResolve (internal/modules/esm/resolve.js:699:10)
    at Loader.defaultResolve [as _resolve] (internal/modules/esm/resolve.js:810:11)
    at Loader.resolve (internal/modules/esm/loader.js:86:40)
    at Loader.getModuleJob (internal/modules/esm/loader.js:230:28)
    at ModuleWrap.<anonymous> (internal/modules/esm/module_job.js:56:40)
    at link (internal/modules/esm/module_job.js:55:36) {
  code: 'ERR_MODULE_NOT_FOUND'
}
```

- **원인**

    MDN Web docs에 따르면 from 뒤에는 가져올 대상 모듈. 보통, 모듈을 담은 .js 파일로의 절대 또는 상대 경로를 가리킨다. 번들러에 따라 확장자를 허용하거나, 필요로 할 수도 있으므로 작업 환경을 확인해야 한다. 현재 번들러가 따로 없기 때문에 확장자를 붙여줘야 하는 것으로 추측하고 있다. 아직 정확한 원인은 모르겠다. 아마도 babel이나 webpack, ES6 관련해서 찾아보면 더 정확히 알 수 있을 듯싶다.

- **해결**

    app.js에 import db from "./db"; 를 import db from "./db.js";로 변경

### 오류4: ??

```bash
$ npm start

> server@1.0.0 start
> node src/app.js

internal/process/esm_loader.js:74
    internalBinding('errors').triggerUncaughtException(
                              ^

controllers\index.js
    at finalizeResolution (internal/modules/esm/resolve.js:276:11)
    at moduleResolve (internal/modules/esm/resolve.js:699:10)
    at Loader.defaultResolve [as _resolve] (internal/modules/esm/resolve.js:810:11)
    at Loader.resolve (internal/modules/esm/loader.js:86:40)
    at Loader.getModuleJob (internal/modules/esm/loader.js:230:28)
    at ModuleWrap.<anonymous> (internal/modules/esm/module_job.js:56:40)
    at link (internal/modules/esm/module_job.js:55:36) {
  code: 'ERR_MODULE_NOT_FOUND'
}
```

- 원인
- 해결

    기억이 안나네 ㅠ

### 오류5: ???

```bash
npm start

> node src/app.js

file:///C:/dev/js/popping-journal/server/src/app.js:4
import db from "./db.js";
       ^^
SyntaxError: The requested module './db.js' does not provide an export named 'default'
    at ModuleJob._instantiate (internal/modules/esm/module_job.js:104:21)
    at async ModuleJob.run (internal/modules/esm/module_job.js:149:5)
    at async Loader.import (internal/modules/esm/loader.js:166:24)
    at async Object.loadESM (internal/process/esm_loader.js:68:5)
```

- 원인
- 해결

    db.js 에 export default db; 추가

- 더 찾아볼 것

    다른 프로젝트에서는 export 안 하고도 잘 썼는데 이유가 무엇일까.. babel의 차이일까.

### 오류6: .env 의 값을 찾지 못하고 undefined 출력

```bash
$ npm start

> server@1.0.0 start
> node src/app.js

SERVER created : undefined
(node:14756) UnhandledPromiseRejectionWarning: MongooseError: The `uri` parameter to `openUri()` must be a string, got "undefined". Make sure the first parameter 
to `mongoose.connect()` or `mongoose.createConnection()` is a string.
    at NativeConnection.Connection.openUri (C:\dev\js\popping-journal\server\node_modules\mongoose\lib\connection.js:694:11)
    at C:\dev\js\popping-journal\server\node_modules\mongoose\lib\index.js:351:10
    at C:\dev\js\popping-journal\server\node_modules\mongoose\lib\helpers\promiseOrCallback.js:31:5
    at new Promise (<anonymous>)
    at promiseOrCallback (C:\dev\js\popping-journal\server\node_modules\mongoose\lib\helpers\promiseOrCallback.js:30:10)
    at Mongoose._promiseOrCallback (C:\dev\js\popping-journal\server\node_modules\mongoose\lib\index.js:1149:10)
    at Mongoose.connect (C:\dev\js\popping-journal\server\node_modules\mongoose\lib\index.js:350:20)
    at file:///C:/dev/js/popping-journal/server/src/db.js:6:10
    at ModuleJob.run (internal/modules/esm/module_job.js:152:23)
    at async Loader.import (internal/modules/esm/loader.js:166:24)
    at async Object.loadESM (internal/process/esm_loader.js:68:5)
(Use `node --trace-warnings ...` to show where the warning was created)
(node:14756) UnhandledPromiseRejectionWarning: Unhandled promise rejection. This error originated either by throwing inside of an async function without a catch block, or by rejecting a promise which was not handled with .catch(). To terminate the node process on unhandled promise rejection, use the CLI flag `--unhandled-rejections=strict` (see https://nodejs.org/api/cli.html#cli_unhandled_rejections_mode). (rejection id: 1)
(node:14756) [DEP0018] DeprecationWarning: Unhandled promise rejections are deprecated. In the future, promise rejections that are not handled will terminate the 
Node.js process with a non-zero exit code.
```

- 원인

    dotenv로 설정한 .env파일은 루트 폴더에 위치해야 하는데 src폴더 안에 있어서 .env파일을 찾지 못했다.

- 해결

    .env 파일을 루트 폴더(/server)로 옮겼다.

### 성공!

고생 끝에 겨우 서버가 제대로 돌아가는 것을 확인하였다.

```bash
$ npm start

> server@1.0.0 start
> node src/app.js
💡SERVER created : 3000
✅Connected to DB
(node:14352) DeprecationWarning: collection.ensureIndex is deprecated. Use createIndexes instead.
(Use `node --trace-deprecation ...` to show where the warning was created)
```

### 앞으로 공부해야 할 것들

- **ES 모듈**
- **webpack**
- **babel**
- **오류5 : 다른 소스에서 export default ~; 가 없어도 잘 불러온 이유는 무엇일지...**
