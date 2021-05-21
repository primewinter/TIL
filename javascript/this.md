# this

## 1 상황에 따라 달라지는 this

this는 함수를 호출할 때 결정된다. 함수를 어떤 방식으로 호출하느냐에 따라 값이 달라진다.

## 1-1 전역 공간에서의 this

전역 공간에서의 this는 **전역 객체**를 가리킨다. 개념상 전역 컨텍스트를 생성하는 주체가 바로 전역 객체이기 때문이다.

전역변수를 선언하면 자바스크립트 엔진은 이를 전역객체(=실행 컨텍스트의 LexicalEnvironment)의 프로퍼티로 할당한다. 

```jsx
var a = 1;
console.log(a); // 1
console.log(window.a); // 1
console.log(this.a); // 1
```

a를 직접 호출할 때도 1이 나오는 이유는, 변수 a에 접근하고자 하면 스코프 체인에서 a를 검색하다가 가장 마지막에 도달하는 전역 스코프인 LE, 즉 전역객체에서 해당 프로퍼티 a를 발견해서 그 값을 반환하기 때문이다.

- **전역변수와 전역객체**

```jsx
var a = 1;
delete window.a; // false
console.log(a, window.a, this.a); // 1 1 1

var b = 2;
delete b; // false
console.log(b, window.b, this.b); // 2 2 2

window.c = 2;
delete window.c; // true
console.log(c, window.c, this.c); // Uncaught ReferenceError : c is not defined

window.d = 4;
delete d;
cosnole.log(d, window.d, this.d); // Uncaught ReferenceError : d is not defined
```

처음부터 전영객체의 프로퍼티로 할당한 경우(c, d)에는 삭제가 되는 반면 전역변수로 선언한 경우(a,b)에는 삭제가 되지 않는다. 즉, 전역변수를 선언하면 자바스크립트 엔진이 이를 자동으로 전역객체의 프로퍼티로 할당하면서 추가적으로 해당 프로퍼티의 configurable 속성(변경 및 삭제 가능성)을 false로 정의하는 것이다.

→ var로 선언한 전역변수와 전역객체의 프로퍼티는 호이스팅 여부 및 configurable 여부에서 차이를 보인다.

## 1-2 메서드로서 호출할 때 그 메서드 내부에서의 this

### 함수 vs 메서드

- **함수** : 그 자체로 독립적인 기능을 수행 (독립성 o)
- **메서드** : 자신을 호출한 대상 객체에 관한 동작을 수행 (독립성 x)

```jsx
// 함수로서의 호출
var func = function(x) {
	console.log(this, x);
};
func(1); // (1) Window { ... } 1

// 메서드로서의 호출
var obj = {
	method: func
};
obj.method(2); // (2) { method: f } 2
```

원래의 익명함수는 그대로인데 이를 변수에 담아 호출한 경우(1)와 obj 객체의 프로퍼티에 할당에서 호출한 경우(2)에 this가 달라진다.

```jsx
// 메서드로서의 호출 - 점 표기법, 대괄호 표기법
var obj = {
	method: function(x) { console.log(this, x); }
};
obj.method(1); // { method: f } 1
obj['method'](2); // { method: f} 2
```

this에는 호출한 주체에 대한 정보가 담긴다. 메서드로서 호출하는 경우 호출 주체는 바로 함수명(프로퍼티명) 앞의 객체이다. 점 표기법의 경우 마지막 점 앞에 명시된 객체가 곧 this가 된다.

```jsx
var obj = {
	methodA: function() { console.log(this); },
	inner: {
			methodB: function() { console.log(this); }
	}
};
obj.methodA(); // { methodA : f, inner: {...} } ( === obj)
obj['methodA'](); // { methodA : f, inner: {...} } ( === obj)

obj.inner.methodB(); // { methodB: f } ( === obj.inner)
obj.inner['methodB'](); // { methodB: f } ( === obj.inner)
obj['inner'].methodB(); // { methodB: f } ( === obj.inner)
obj['inner']['methodB'](); // { methodB: f } ( === obj.inner)
```

## 1-3 함수로서 호출할 때 그 함수 내부에서의 this

### 함수 내부에서의 this

어떤 함수를 함수로서 호출할 경우에는 this가 지정되지 않는다. this에는 호출한 주체에 대한 정보가 담기는데, 함수로서 호출하는 것은 호출 주체를 명시하지 않고 개발자가 코드로 직접 실행한 것이기 때문에 호출 주체의 정보를 알 수 없다.

앞서서 실행 컨텍스트를 활성화할 당시에 this가 지정되지 않은 경우 this는 전역 객체를 바라본다고 했다. 따라서 함수에서의 this는 전역객체를 가리킨다.

### 메서드의 내부함수에서의 this

```jsx
var obj1 = {
	outer: function() {
			console.log(this); // (1)
			var innerFunc = function() {
					console.log(this); // (2), (3)
			};
			innerFunc();
		
			var obj2 = {
					innerMethod: innerFunc
			};
			obj2.innerMethod();
};
obj1.outer();
```

(1) obj1.outer 함수의 실행 컨텍스트가 생성되면서 호이스팅하고, 스코프 체인 정보를 수집하고, this를 바인딩한다. 이 함수는 호출할 때 함수명인 outer앞에 점(.)이 있었으므로 메서드로서 호출한 것이다. 따라서 this에는 마지막 점 앞의 객체는 obj1이 바인딩된다.

(2) innerFunc 함수의 실행 컨텍스트가 생성되면서 호이스팅, 스코프 체인 수집, this바인딩 등을 수행한다. 이 함수를 호출할 때 함수명 앞에는 점(.)이 없었다. 즉, 함수로서 호출한 것이므로 this가 지정되지 않았고, 따라서 자동으로 스코프 체인상의 최상위 객체인 전역객체(Window)가 바인딩 된다.

(3) obj2.innerMethod 함수의 실행 컨텍스트가 생성된다. 이 함수는 호출할 때 함수명인 innerMethod 앞에 점(.)이 있었으므로 메서드로서 호출한 것이다. 따라서 this에는 마지막 점 앞의 객체인 obj2가 바인딩된다.

### 메서드의 내부 함수에서의 this를 우회하는 방법

변수를 검색하면 우선 가장 가까운 스코프의 LE를 찾고 없으면 상위 스코프를 탐색하듯이, this 역시 현재 컨텍스트에 바인딩된 대상이 없으면 직전 컨텍스트의 this를 바라보면 더 자연스러울 지도 모른다. 그러나 호출 주체가 없을 때에는 자동으로 전역객체를 바인딩하는 것은 js의 고유한 특성이므로 주어진 환경에 적응해야 한다. 우회의 방법으로 변수를 활용하여 내부함수에 this를 상속할 수 있다.

```jsx
var obj = {
	outer: function() {
			console.log(this); // (1)
			var innerFunc1 = function () {
					console.log(this); // (2)
			};
			innerFunc1();

			var self = this;
			var innerFunc2 = function () {
					console.log(self); // (3)
			};
			innerFunc2();
	}
};
obj.outer();
```

(1) { outer: f }

(2) Window { ... }

(3) { outer: f }

innerFunc1 내부에서 this는 전역객체를 가리킨다. 한편 outer 스코프에서 self라는 변수에 this를 저장한 상태에서 호출한 innerFunc2의 경우 self에는 객체 obj가 출력된다.

### this를 바인딩하지 않는 함수

ES6에서는 함수 내부에서 this가 전역객체를 바라보는 문제를 보완하고자 this를 바인딩하지 않는 화살표 함수arrow function을 도입했다. 화살표 함수는 실행 컨텍스트를 생성할 때 this 바인딩 과정 자체가 빠지게 되어, 상위 스코프의 this를 그대로 활용할 수 있다.

```jsx
var obj = {
		outer: function() {
				console.log(this); // (1)
				var innerFunc = () => {
						console.log(this); // (2)
				};
				innerFunc();
		}
};
obj.outer();
```

(1) { outer : f }

(2) { outer : f }

## 1-4 콜백 함수 호출 시 그 함수 내부에서의 this

- 콜백 함수 : 함수 A의 제어권을 다른 함수(또는 메서드) B에게 넘겨주는 경우에서 함수A

제어권을 받은 함수에서 콜백 함수에 별도로 this가 될 대상을 지정한 경우에는 그 대상을 참조하게 된다.

```jsx
setTimeout(function () { console.log(this); }, 300); // (1)

[1, 2, 3, 4, 5].forEach(function(x) {
		console.log(this, x); // (2)
});

document.body.innerHTML += '<button id="a">클릭</button>';
document.body.querySelector('#a')
			.addEventListener('click', function(e) {
					console.log(this, e);  // (3)
			});
```

(1) 0.3초 뒤 전역객체 출력 → 콜백 함수 내부에서의 this는 전역객체 참조

(2) 전역객체와 배열의 각 요소가 총 5회 출력 → 콜백 함수 내부에서의 this는 전역객체 참조

(3) click 이벤트가 발생하면 HTML 엘리먼트와 클릭 이벤트에 관한 정보가 담긴 객체 출력 → 콜백 함수를 호출할 때 자신의 this를 상속하도록 정의되어 있다

## 1-5 생성자 함수 내부에서의 this

- 생성자 함수 : 어떵 공통된 성질을 지니는 객체들을 생성하는 데 사용하는 함수 (객체 지향 언어에서는 class라고 부른다)

JS는 함수에 생성자로서의 역할을 함께 부여한다. new 명령어와 함께 함수를 호출하면 해당 함수가 생성자로서 동작한다. 그리고 어떤 함수가 생성자 함수로서 호출된 경우 내부에서의 this는 곧 새로 만들 구체적인 인스턴스 자신이 된다.

생성자 함수를 호출(new 명령어와 함께 함수를 호출)하면 우선 생성자의 prototype 프로퍼티를 참조하는 __proto__라는 프로퍼티가 있는 객체(인스턴스)를 만들고, 미리 준비된 공통 속성 및 개성을 해당 객체(this)에 부여한다. 이렇게 해서 구체적인 인스턴스가 만들어진다.

```jsx
var Cat = function (name, age) {
		this.bark = '야옹';
		this.name = name;
		this.age = age;
};
var choco = new Cat('초코', 7); // this : choco 인스턴스
var nabi = new Cat('나비', 5); // this : nabi 인스턴스
console.log(choco, nabi);

/* 결과
Cat { bark: '야옹', name: '초코', age: 7 }
Cat { bark: '야옹', name: '나비', age: 5 }
*/
```

## 2 명시적으로 this를 바인딩하는 방법

## 2-1 call 메서드

```jsx
Function.prototype.call(thisArg[, arg1[, arg2, ...]]])
/* call 메서드 : 메서드의 호출 주체인 함수를 즉시 실행시키는 명령
* 첫 번째 인자를 this로 바인딩하고, 이후의 인자들을 호출할 함수의 매개변수로 함
*/ 

var func = function (a, b, c) {
		console.log(this, a, b, c);
};

func(1, 2, 3); // Window{ ... } 1 2 3
func.call({ x:1 }, 4, 5, 6); // { x:1 } 4 5 6

var obj = {
		a: 1,
		method: function(x, y) {
				console.log(this.a, x, y);
		}
};

obj.method(2, 3); // 1 2 3
obj.method.call({ a:4 }, 5, 6); // 4 5 6
```

## 2-2 apply 메서드

```jsx
Function.prototype.apply(thisArg[, argsArray])
/* apply 메서드 : call 메서드와 기능적으로 완전히 동일
* 첫 번째 인자를 this로 바인딩
* 두 번째 인자를 배열로 받아 그 배열의 요소들을 호출할 함수의 매개변수로 지정
*/

var func = function(a, b, c) {
		console.log(this, a, b, c);
};
func.apply({ x:1 }, [4, 5, 6]); // { x:1 } 4 5 6

var obj = {
		a: 1,
		method: function(x, y) {
				console.log(this.a, x, y);
		}
};
obj.method.apply({ a:4 }, [5, 6]); // 4 5 6
```
