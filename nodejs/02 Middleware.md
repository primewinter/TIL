### 1. 익스프레스 구조도 & 미들웨어 요청 흐름
![express](https://user-images.githubusercontent.com/57691894/111481011-e5b99400-8775-11eb-9d77-da7cb582a58f.jpg)

### 2. 미들웨어
### 2.1 morgan
  - 요청에 대한 정보를 콘솔에 기록

  ```jsx
  ...
  var logger = require('morgan');
  ...
  app.use(logger('dev'));
  ...
  ```

  **logger의 인자**

  **- dev** : 개발에서 주로 쓰인다

     GET / 200 51.267 ms - 1539 (HTTP요청(GET) 주소(/) HTTP상태코드(200) 응답속도(51.267ms) - 응답바이트(1539))

  **- short** : 개발에서 주로 쓰인다

    ::1 - GET / HTTP/1.1 304 - - 1028.771 ms

  **- common** : 배포 시 주로 쓰인다

    ::1 - - [16/Mar/2021:14:27:45 +0000] "GET / HTTP/1.1" 304 -

  **- combined** : 배포 시 주로 쓰인다

    ::1 - - [16/Mar/2021:14:28:25 +0000] "GET / HTTP/1.1" 304 - "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.82 Safari/537.36"
    
    
    
    
### 2.2 body-parser

요청의 본문을 해석해주는 미들웨어. 보통 폼 데이터나 ajax 요청의 데이터 처리

```jsx
...
var bodyParser = require('body-parser');
...
app.use(bodyParser.json());
app.use(bodyParser.urlencoded({extended: false}));
...
```

URL-encoded : 보통 폼 전송이 사용하는 방식. urlencoded 메서드에는 { extended: false }라는 옵션이 들어 있다. 

- **{ extended: *false* }** 노드의 querystring모듈을 사용하여 쿼리스트링을 해석
- **{ extended: *true*}**  qs모듈을 사용하여 쿼리스트링을 해석한다.

    ##### ❗ qs 모듈은 내장 모듈이 아니라 npm패키지이며, querystring 모듈의 기능을 조금더 확장한 모듈이다.

JSON 형식으로 { name: 'Mike', age: '13 years-old' }를 본문으로 보내면 req.body에 그대로 들어간다.

URL-encoded 형식으로 name=mike&age=13years-old를 본문으로 보낸다면 req.body에  { name: 'Mike', age: '13 years-old' }가 들어간다.

JSON과 URL-encoded 형식의 본문 외에도 Raw, Text 형식의 본문을 추가로 해석할 수 있다.

Raw는 본문이 버퍼 데이터일 때, Text 본문이 텍스트 데이터일 때 해석하는 미들웨어
app.use(bodyParser.raw());
app.use(bodyParser.text());

multipart/form-data로 전송한 데이터는 해석하지 못한다.



### 2.3 cookie-parser

요청에 포함된 쿠키를 해석

```jsx
...
var cookieParser = require('cookie-parser');
...
app.use(cookieParser());
...
```

해석된 쿠키들은 req.cookies 객체에 들어간다. ex) req.cookies = { *key : value* }

```jsx
app.use(cookieParser('secret code')); // 첫 번째 인자로 문자열을 넣는다.
```

쿠키들은 제공한 문자열로 서명된 쿠키가 된다. 서명된 쿠키는 클라이언트에서 수정했을 때 에러가 발생하므로 클라이언트에서 쿠키로 위험한 행동을 하는 것을 방지할 수 있다.



### 2.4 static

정적인 파일들을 제공한다. 익스프레스 4 버전에서 내장되어 있던 미들웨어였으나 4.16.0 버전에서는 body-parser의 일부도 내장되면서 유일한 내장 미들웨어가 아니다. 따로 설치할 필요가 없다.

```jsx
...
app.use(express.static(path.join(__dirname, 'public'))); // 정적 파일들이 담긴 폴더를 인자로 넣는다.
...
```

또는,

```jsx
app.use('/img', express.static(path.join(__dirname, 'public'))); // 정적 파일을 제공할 주소를 지정할 수도 있다.
```

static 미들웨어는 요청에 부합하는 정적 파일을 발견한 경우 응답으로 해당 파일을 전송한다. 이 경우 응답을 보냈으므로 다음에 나오는 라우터가 실행되지 않는다. 만약 파일을 찾지 못했다면 요청을 라우터로 넘긴다.

이렇게 자체적으로 정적 파일 라우터 기능을 수행하므로 최대한 위쪽에 배치하는 것이 좋다. 그래야 서버가 쓸데없는 미들웨어 작업을 하는 것을 막을 수 있다. 서비스에 따라 쿠키 같은 것이 정적 파일을 제공하는 데 영향을 끼칠 수도 있기 때문에 자신의 서비스에 맞춰 맞는 위치를 선택해야 한다.
