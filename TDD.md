# 📘 서론

### **용어 정리**

Production Code : 실제 서비스, 배포해야 하는 코드

```java
public class Calculator {
	int add(int i, int j) {
		return i + j;
	}
	int subtract(int i, int j) {
		return i - j;
	}
	int multiply(int i, int j) {
		return i * j;
	}
	int divide(int i, int j) {
		return i / j;
	}
}
```

Test Code 

```java
public static void main(String[] args) {
	Calculator cal = new Calculator();
	System.out.println(cal.add(3, 4));
	System.out.println(cal.subtract(5, 4));
	System.out.println(cal.muliply(2, 6));
	System.out.println(cal.divide(8, 4));
}
```

### TDD란?

**TDD = TFD(Test First Development) + 리팩토링**

TDD ≠ 단위테스트

> TDD란 프로그래밍 의사결정과 피드백 사이의 간극을 의식하고 이를 제어하는 기술이다. 
TDD의 아이러니 중 하나는 테스트 기술이 아니라는 점이다. TDD는 분석 기술이며, 설계 기술이기도 하다.

-켄트 백, Test Driven Development by Example 중

### **TDD를 하는 이유**

- 디버깅 시간을 줄여준다.
- 동작하는 문서 역할을 한다.
- 변화에 대한 두려움을 줄여준다.

### TDD 사이클

Test fails → Test passes → Refactor → Test fails ...

- 실패하는 테스트 구현
- 테스트가 성공하도록 프로덕션 코드 구현
- 프로덕션 코드와 테스트 코드를 리팩토링

### TDD 원칙

1. 실패하는 단위 테스트를 작성할 때까지 프로덕션 코드를 작성하지 않는다.
2. 컴파일은 실패하지 않으면서 실행이 실패하는 정도로만 단위 테스트를 작성한다.
3. 현재 실패하는 테스트를 통과할 정도로만 실제 코드를 작성한다.

# 📘 TDD 방법

### 도메인 지식, 객체 설계 경험이 있는 경우

- 요구사항 분석을 통해 대략적인 설계 - 객체 추출
- UI, DB 등과 의존관계를 가지지 않는 핵심 도메인 영역을 집중 설계

👉 **1차적으로는 도메인 로직을 테스트 하는 것에 집중**

### 도메인 지식, 객체 설계 경험이 없는 경우

**👉 구현할 기능 목록 작성하기**

- 구현할 기능 목록을 작성한 후에 TDD로 도전
- 기능 목록을 작성하는 것도 연습이 필요하다

### 그래도 막막하다면...

**👉 일단 구현**

- 구현하려는 프로그래밍의 **도메인 지식을 쌓는다**
- **구현한 모든 코드를 버린다**
- 구현할 기능 목록 작성 또는 간단한 도메인 설계
- 기능 목록 중 가장 만만한 녀석부터 TDD로 구현 시작
- 복잡도가 높아져 리팩토링하기 힘든 상태가 되면 다시 버린다
- 다시 도전

아무것도 없는 상태에서 구현하는 것보다 레거시 코드를 분석하고 리팩토링하는 것이 더 어려운 일이다. SI에서 빨리 빨리 개발을 끝내는 것을 미덕처럼 여기지만 빨리 구현을 마친다고 해서 좋은 개발자라고 할 수 없다. 오히려 유지보수를 하면서 기존의 쓰레기 코드들을 리팩토링 해나가야 실력을 쌓을 수 있다.

# 📘 TDD로 숫자 야구 게임 구현

### 일단 구현

- 지금까지 자신에게 익숙한 방법으로 일단 구현
- 모든 코드를 버리고 TDD로 다시 구현

### 기능 목록을 작성한 후 테스트 가능한 부분을 찾아 TDD로 도전

- 1~9의 숫자 중 랜덤으로 3개의 숫자를 구한다
- 사용자로부터 입력 받는 3개 숫자 예외 처리
    - 1~9의 숫자인가?
    - 중복 값이 있는가?
    - 3자리인가?
- 위치와 숫자 값이 같은 경우 - 스트라이크
- 위치는 다른데 숫자 값이 같은 경우 - 볼
- 숫자 값이 다른 경우 - 낫싱
- 사용자가 입력한 값에 대한 실행 결과를 구한다

## 1단계 - Util 성격의 기능이 TDD로 도전하기 좋음

- 사용자로부터 입력 받는 3개 숫자 예외 처리
    - 1~9의 숫자인가?
    - 중복 값이 있는가?
    - 3자리인가?

ValidationUtilsTest.java

```java
import org.junit.jupiter.api.DiaplayName;
import org.junit.jupiter.api.Test;

import static org.assertj.core.api.Assertions.assertThat;

public class ValidationUtilsTest {
	@Test
	@DisplayName("야구_숫자_1_9_검증") // (1)
	void 야구_숫자_1_9_검증() {
		boolean result = ValidationUtils.validNo(9); // (2)
		assertThat(result).isTrue();
		
		// 위의 두 줄 리팩토링
		assertThat(ValidationUtils.validNo(9)).isTrue(); // pass : 1 cycle 끝
		assertThat(ValidationUtils.validNo(1)).isTrue(); // pass
		assertThat(ValidationUtils.validNo(0)).isFalse(); // (3) fail : 2 cycle 끝
		assertThat(ValidationUtils.validNo(10)).isFalse();
	}
}
```

(1) 한글로 적어도 돼. 소통이 중요하니까.

(2) 일단 클래스는 없지만 먼저 작성한다. 거꾸로 작성해나가는 것이니까. 컴파일러 이용해서(강사는 intelliJ 씀) 일단 생성부터 했다.

ValidationUtils.java

```java
public class ValidationUtils {
	public static boolean validNo(int no) {
		if (no <= 9) { // (3)에서 fail이 뜨는 코드이므로 수정해준다.
			return true;
		}
		return false;
	}

	// (3)의 리팩토링 결과
	public static boolean validNo(int no) {
		if (no >= 1 && no <= 9) { 
			return true;
		}
		return false;
	}

	// 리팩토링 (불필요한 분기처리 제거) : 3 cycle 끝
	public static boolean validNo(int no) {
		return no >= 1 && no <= 9;
	}

	// 리팩토링 (상수 처리) : 4 cycle 끝
	public static final int MIN_NO = 1;
	public static final int MIN_NO = 9;

	public static boolean validNo(int no) {
		return no >= MIN_NO && no <= MAX_NO;
	}
	
}
```

커밋은 하나의 테스트 코드와 해당 기능 구현 및 리팩토링까지 마친 후에 하는 것을 권장한다. 커밋 메시지는 테스트 코드의 displayName이 될 것이다. 보기에 명확하며 기능 단위로 떨어져서 적절하다.

input과 output이 명확한 UTIL성 메소드가 TDD하기에 좋다. 그러므로 이러한 메소드부터 TDD하는 것을 권장한다.

## 2단계 - 테스트 가능한 부분에 대해 TDD로 도전

- 위치와 숫자 값이 같은 경우 - 스트라이크
- 위치는 다른데 숫자 값이 같은 경우 - 볼
- 숫자 값이 다른 경우 - 낫싱

```java
COM / USER
123, 456 -> nothing
123, 245 -> 1ball
123, 145 -> 1strike

PlayResult result = Baseball.play(Arrays.asList(1, 2, 3), Arrays.asList(4, 5, 6));
/**
배열로 하면 너무 복잡하다. 하나 하나 쪼개서 해보는 작업을 하자.
*/

---
작은 단위로 쪼개기
---
COM / USER
1, 4 -> 결과를 알 수 없다. 위치값을 모르니까!

위치값, 숫자
1 4 , 1 4 -> strike
1 4 , 2 4 -> ball
1 4 , 2 5 -> nothing

```

BallTest.java

```java
public class BallTest {
	@Test
	void nothing() {
		Ball com = new Ball(1, 4); // 또 없는 거부터 생성해주자ㅋ
		BallStatus status = com.play(new Ball(2, 5));
		assertThat(status).isEqualTo(BallStatus.NOTHING);
	}

	@Test
	void ball() {
		Ball com = new Ball(1, 4); // 또 없는 거부터 생성해주자ㅋ
		BallStatus status = com.play(new Ball(2, 4));
		assertThat(status).isEqualTo(BallStatus.BALL);
	}
}

/* BallTest의 중복 코드(Ball com = new Ball(1, 4);) 리팩토링*/
public class BallTest {
	private Ball com;

	@BeforeEach
	void setUp() {
		com = new Ball(1, 4);
	}
	
	@Test
	void nothing() {
		BallStatus status = com.play(new Ball(2, 5));
		assertThat(status).isEqualTo(BallStatus.NOTHING);
	}

	@Test
	void ball() {
		BallStatus status = com.play(new Ball(2, 4));
		assertThat(status).isEqualTo(BallStatus.BALL);
	}

	@Test
	void strike() {
		BallStatus status = com.play(new Ball(1, 4));
		assertThat(status).isEqualTo(BallStatus.STRIKE);
	}
}
```

BallStatus.java

```java
public enum BallStatus {
		STRIKE, BALL, NOTHING
}
```

Ball.java

```java
public class Ball {
		private final int position;
		private final int ballNo;

		public Ball(int position, int ballNo) {
			this.position = position;
			this.ballNo = ballNo;
		}

		public BallStatus play(Ball ball) {
			if (ballNo == ball.ballNo) {
				return BallStatus.BALL;
			}
			return BallStatus.NOTHING;
		}

		/* play() 리팩토링 */
		public BallStatus play(Ball ball) {
			if (ball.matchBallNo(ballNo)) {
				return BallStatus.BALL;
			}
			return BallStatus.NOTHING;
		}

		private boolean matchBallNo(int ballNo) {
			return this.ballNo == ballNo;
		}

		/* strike 추가 */
		public BallStatus play(Ball ball) {
			if (this.equals(ball)) {
				return BallStatus.STRIKE;
			}
			if (ball.matchBallNo(ballNo)) { // ball에서 NPE 가능성 있으므로 null인지 체크해줘야 함
				return BallStatus.BALL;
			}
			return BallStatus.NOTHING;
		}

		@Override
		public boolean equals(Object o) {
			if (this == o) return true;
			return false;
		}
		
}
```

### 난이도를 높여서...

```java
COM / USER
123 / 1 4 -> nothing
123 / 1 2 -> ball
123 / 1 1 -> strike

이번엔 List와 숫자를 비교해보자.
Ball -> Balls
BallTest -> BallsTest
```

BallsTest.java

```java
public class BallsTest {
		@Test
		void nothing() {
			Balls answers = new Balls(Arrays.asList(1, 2, 3));
			BallStatus status = answers.paly(new Ball(1, 4));
			assertThat(status).isEqualTo(BallStatus.NOTHING);
		}

		@Test
		void ball() {
			Balls answers = new Balls(Arrays.asList(1, 2, 3));
			BallStatus status = answers.paly(new Ball(1, 2));
			assertThat(status).isEqualTo(BallStatus.BALL);
		}

		@Test
		void strike() {
			Balls answers = new Balls(Arrays.asList(1, 2, 3));
			BallStatus status = answers.paly(new Ball(1, 1));
			assertThat(status).isEqualTo(BallStatus.STRIKE);
		}

		@Test
		void play_nothing() {
			Balls answers = new Balls(Arrays.asList(1, 2, 3));
			PlayResult result = answers.play(Arrays.asList(4, 5, 6));
			assertThat(result.getStrike()).isEqualTo(0);
			assertThat(result.getBall()).isEqualTo(0);
		}

		@Test
		void play_1strike_1ball() {
			Balls answers = new Balls(Arrays.asList(1, 2, 3));
			PlayResult result = answers.play(Arrays.asList(1, 4, 2));
			assertThat(result.getStrike()).isEqualTo(1);
			assertThat(result.getBall()).isEqualTo(1);
		}

		@Test
		void play_3strike() {
			Balls answers = new Balls(Arrays.asList(1, 2, 3));
			PlayResult result = answers.play(Arrays.asList(1, 2, 3));
			assertThat(result.getStrike()).isEqualTo(3);
			assertThat(result.getBall()).isEqualTo(0);
			assertThat(result.isGameEnd()).isTrue();
		}
}
```

Balls.java

```java
public class Balls {
		private final List<Ball> answers;

		public Balls(List<Integer> answers) {
			this.balls = mapBall(answers);
		}

		private static List<Ball> mapBall(List<Integer> answers) {
			List<Ball> balls = new ArrayList<>();
			for (int i=0; i < 3 ; i++) {
				balls.add(new Ball(i + 1, answers.get(i)));
			}
			return balls;
		}

		public BallStatus play(Ball userBall) {
			return balls.stream()
						.map(answer -> answer.play(userBall))
						// .filter(status -> status != BallStatus.NOTHING) 리팩토링1
						// .filter(status -> status.isNotNothing()) 리팩토링2
						.filter(BallStatus::isNotNothing)
						.findFirst()
						.orElse(ballStatus.NOTHING);
		}

		(public) PlayResult play(List<Integer> balls) { // public 지워도 됨 private 메소드와 다름 없다.
			Balls userBalls = new Balls(balls);
			PlayResult result = new PlayResult();
			for (Ball answer: answers) {
				BallStatus status = userBalls.play(answer);
				result.report(status);
			}
			return result;
		}
}
```

BallStatus.java

```java
public enum BallStatus {
	BALL, STRIKE, NOTHING;
	
	// enum도 하나의 클래스고 객체기 때문에 이렇게 메시지를 보낼 수 있다.
	public boolean isNotNothing() {
		return this != NOTHING;
	}

	public boolean isStrike() {
		return this == STRIKE;
	}

	public boolean isBall() {
		return this == BALL;
	}
}
```

PlayResult.java

```java
public class PlayResult {
	private int strike = 0;
	private int ball = 0;

	public int getStrike() {
		return this.strike;
	}

	public int getBall() {
		return this.ball;
	}
	
	public void report(BallStatus status) {
		// if (status == BallStatus.STRIKE) { 리팩토링 : 메시지에 담아주는게 좋다
		if (status.isStrike()) {
			return this.strike += 1;
		}
		if (status.isBall()) {
			return this.ball += 1;
		}
	}

	public boolean isGameEnd() {
		return strike == 3;
	}
}
```

객체가 갖고 있는 상태 데이터를 get을 통해 접근하는 게 있다면 그렇게 하지 말고, 메시지를 보내서, 상태 데이터를 갖는 객체가 일을 하게 만들어라.
그것만 해도 TDD할 일이 많다.

[Balls.java](http://balls.java) 의 play() 를 인터페이스화 할 수는 없나요?
( 아래 Playable 이란 interface 를 만들어보았다. )

인터페이스를 추출하는 것도 좋은데 '필요한 시점에' 하는 게 중요하다. 안 그러면 인터페이스를 남발하게 될 수 있다. play 하는 이 메소드에 변경 가능성이 있다거나 다른 방식으로 play하는 결과가 있다면 구현체를 만드는 게 의미가 있겠지만 그렇지 않다면 특별한 의미는 없을 것 같다.

```java
public interface Playable {
		PlayResult play(List<Integer> balls);
}
```

```java
public class Balls implements Playable {
	...
	// 이하 동일 
	...
}
```

private 메소드도 테스트 코드를 작성해야 할까요? ex. [Balls.java](http://balls.java) 의 PlayResult play(List<Integer> balls) 메소드

반드시 할 필요는 없지만 확인이 필요하다면 만들어야겠지요..?

원칙론자들은 메소드의 private 접근제한자를 유지하고 reflection을 이용해서 테스트코드에서 호출하는 방식을 고집하기도 한다. 그러나 나(강사)의 경우 실용주의자이기 때문에 해당 메소드를 같은 package 안에 있는 테스트 코드라면 default로 바꾸거나 public으로 해서 테스트 코드를 작성하기도 한다.

그러나, private 메소드를 꼭 테스트를 해보아야 하는 경우라면 ***해당 메소드의 위치가 정말 그곳이 맞는지*** 확인하는 것도 하나의 포인트가 될 수 있다. 만약 다른 클래스로 옮긴다면 그 메소드는 open되는 것이기 때문에(=Balls.java에서 타 클래스에 있는 해당 메소드를 호출하니까) 정말 그 위치에 있는 게 맞는지 생각을 해보자. 

강사는 private 메소드로 적극적으로 쪼개는 것을 추천한다. 그러나 꼭 모든 private 메소드를 테스트할 필요는 없다고 본다. public을 통해서 대부분 다 테스트할 수 있기 때문이다.

(예외 처리를 위한)

BallNumber.java

```java
public class BallNumber {
	public final static int MIN_NO = 1;
	public final static int MAX_NO = 9;

	private int no;

	public BallNumber(int no) {
		if (no < MIN_NO || no > MAX_NO) {
			throw new IllegalArgumentException("볼 숫자는 1부터 9의 값이어야 합니다.");
		}
		this.no = no;
	}
}
```

Ball.java

```java
public class Ball {
		private final int position;
		private final int ballNo;

		public Ball(int position, int ballNo) {
			this.position = position;
			// this.ballNo = ballNo; 리팩토링
			this.ballNo = new BallNumber(ballNo);
		}

		...
		
}
```
