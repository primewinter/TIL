## CORS (Cross-Origin Resource Sharing)

클라이언트와 서버의 도메인이 일치하지 않을 시 보안상의 이유로 HTTP 요청을 제한한다. 이 문제를 해결하기 위해서는 응답 헤더에 **Access-Control-Allow-Origin**이라는 헤더를 넣어주어야 한다. 이 헤더의 의미는 웹 브라우저에서 해당 정보를 읽는 것이 허용된 출처라는 것을 설명해주는 것이다.

- **서버에 cors 모듈 설치**

```bash
npm i cors
```

```jsx
const express = require('express');
const cors = require('cors');
...
const router = express.Router();

router.use(cors());
...
```

해당 파일에 속한 모든 라우터에 cors 미들웨어가 적용된다.

### cors 적용한 **Response Headers**
```xml
Access-Control-Allow-Origin: *  → 모든 클라이언트의 요청을 허용한다는 뜻
Connection: keep-alive
Content-Length: 246
Content-Type: application/json; charset=utf-8
```

- **도메인 제한**

```jsx
...
router.use(async (req, res, next) => {
	const domain = await Domain.find({
		where: { host: url.parse(req.get('origin')).host },
	});
	if(domain) {
		cors({ origin: req.get('origin') })(req, res, next);
	} else {
		next();
	}
});
...
```

먼저 도메인 모델로 클라이언트의 도메인(req.get('origin'))과 호스트가 일치하는 것이 있는지 검사한다. http나 https 같은 프로토콜을 떼어낼 때는 url.parse 메소드를 이용한다.

일치하는 것이 있다면 cors를 허용해서 다음 이들웨어로 보내고, 일치하는 것이 없다면 cors 없이 next를 호출한다. 

cors 미들웨어에 옵션 인자를 주어서 origin 속성에 허용할 도메인만 따로 적어주면 된다. *처럼 모든 도메인을 허용하는 대신 기입한 도메인만 허용한다.


### 도메인 제한 후 **Response Headers**

```xml
Access-Control-Allow-Origin: http://localhost:8003
Connection: keep-alive
Content-Length: 246
Content-Type: application/json; charset=utf-8
```
