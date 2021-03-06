# π μλ‘ 

### **μ©μ΄ μ λ¦¬**

Production Code : μ€μ  μλΉμ€, λ°°ν¬ν΄μΌ νλ μ½λ

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

### TDDλ?

**TDD = TFD(Test First Development) + λ¦¬ν©ν λ§**

TDD β  λ¨μνμ€νΈ

> TDDλ νλ‘κ·Έλλ° μμ¬κ²°μ κ³Ό νΌλλ°± μ¬μ΄μ κ°κ·Ήμ μμνκ³  μ΄λ₯Ό μ μ΄νλ κΈ°μ μ΄λ€. 
TDDμ μμ΄λ¬λ μ€ νλλ νμ€νΈ κΈ°μ μ΄ μλλΌλ μ μ΄λ€. TDDλ λΆμ κΈ°μ μ΄λ©°, μ€κ³ κΈ°μ μ΄κΈ°λ νλ€.

-μΌνΈ λ°±, Test Driven Development by Example μ€

### **TDDλ₯Ό νλ μ΄μ **

- λλ²κΉ μκ°μ μ€μ¬μ€λ€.
- λμνλ λ¬Έμ μ­ν μ νλ€.
- λ³νμ λν λλ €μμ μ€μ¬μ€λ€.

### TDD μ¬μ΄ν΄

Test fails β Test passes β Refactor β Test fails ...

- μ€ν¨νλ νμ€νΈ κ΅¬ν
- νμ€νΈκ° μ±κ³΅νλλ‘ νλ‘λμ μ½λ κ΅¬ν
- νλ‘λμ μ½λμ νμ€νΈ μ½λλ₯Ό λ¦¬ν©ν λ§

### TDD μμΉ

1. μ€ν¨νλ λ¨μ νμ€νΈλ₯Ό μμ±ν  λκΉμ§ νλ‘λμ μ½λλ₯Ό μμ±νμ§ μλλ€.
2. μ»΄νμΌμ μ€ν¨νμ§ μμΌλ©΄μ μ€νμ΄ μ€ν¨νλ μ λλ‘λ§ λ¨μ νμ€νΈλ₯Ό μμ±νλ€.
3. νμ¬ μ€ν¨νλ νμ€νΈλ₯Ό ν΅κ³Όν  μ λλ‘λ§ μ€μ  μ½λλ₯Ό μμ±νλ€.

# π TDD λ°©λ²

### λλ©μΈ μ§μ, κ°μ²΄ μ€κ³ κ²½νμ΄ μλ κ²½μ°

- μκ΅¬μ¬ν­ λΆμμ ν΅ν΄ λλ΅μ μΈ μ€κ³ - κ°μ²΄ μΆμΆ
- UI, DB λ±κ³Ό μμ‘΄κ΄κ³λ₯Ό κ°μ§μ§ μλ ν΅μ¬ λλ©μΈ μμ­μ μ§μ€ μ€κ³

π **1μ°¨μ μΌλ‘λ λλ©μΈ λ‘μ§μ νμ€νΈ νλ κ²μ μ§μ€**

### λλ©μΈ μ§μ, κ°μ²΄ μ€κ³ κ²½νμ΄ μλ κ²½μ°

**π κ΅¬νν  κΈ°λ₯ λͺ©λ‘ μμ±νκΈ°**

- κ΅¬νν  κΈ°λ₯ λͺ©λ‘μ μμ±ν νμ TDDλ‘ λμ 
- κΈ°λ₯ λͺ©λ‘μ μμ±νλ κ²λ μ°μ΅μ΄ νμνλ€

### κ·Έλλ λ§λ§νλ€λ©΄...

**π μΌλ¨ κ΅¬ν**

- κ΅¬ννλ €λ νλ‘κ·Έλλ°μ **λλ©μΈ μ§μμ μλλ€**
- **κ΅¬νν λͺ¨λ  μ½λλ₯Ό λ²λ¦°λ€**
- κ΅¬νν  κΈ°λ₯ λͺ©λ‘ μμ± λλ κ°λ¨ν λλ©μΈ μ€κ³
- κΈ°λ₯ λͺ©λ‘ μ€ κ°μ₯ λ§λ§ν λμλΆν° TDDλ‘ κ΅¬ν μμ
- λ³΅μ‘λκ° λμμ Έ λ¦¬ν©ν λ§νκΈ° νλ  μνκ° λλ©΄ λ€μ λ²λ¦°λ€
- λ€μ λμ 

μλ¬΄κ²λ μλ μνμμ κ΅¬ννλ κ²λ³΄λ€ λ κ±°μ μ½λλ₯Ό λΆμνκ³  λ¦¬ν©ν λ§νλ κ²μ΄ λ μ΄λ €μ΄ μΌμ΄λ€. SIμμ λΉ¨λ¦¬ λΉ¨λ¦¬ κ°λ°μ λλ΄λ κ²μ λ―Έλμ²λΌ μ¬κΈ°μ§λ§ λΉ¨λ¦¬ κ΅¬νμ λ§μΉλ€κ³  ν΄μ μ’μ κ°λ°μλΌκ³  ν  μ μλ€. μ€νλ € μ μ§λ³΄μλ₯Ό νλ©΄μ κΈ°μ‘΄μ μ°λ κΈ° μ½λλ€μ λ¦¬ν©ν λ§ ν΄λκ°μΌ μ€λ ₯μ μμ μ μλ€.

# π TDDλ‘ μ«μ μΌκ΅¬ κ²μ κ΅¬ν

### μΌλ¨ κ΅¬ν

- μ§κΈκΉμ§ μμ μκ² μ΅μν λ°©λ²μΌλ‘ μΌλ¨ κ΅¬ν
- λͺ¨λ  μ½λλ₯Ό λ²λ¦¬κ³  TDDλ‘ λ€μ κ΅¬ν

### κΈ°λ₯ λͺ©λ‘μ μμ±ν ν νμ€νΈ κ°λ₯ν λΆλΆμ μ°Ύμ TDDλ‘ λμ 

- 1~9μ μ«μ μ€ λλ€μΌλ‘ 3κ°μ μ«μλ₯Ό κ΅¬νλ€
- μ¬μ©μλ‘λΆν° μλ ₯ λ°λ 3κ° μ«μ μμΈ μ²λ¦¬
    - 1~9μ μ«μμΈκ°?
    - μ€λ³΅ κ°μ΄ μλκ°?
    - 3μλ¦¬μΈκ°?
- μμΉμ μ«μ κ°μ΄ κ°μ κ²½μ° - μ€νΈλΌμ΄ν¬
- μμΉλ λ€λ₯Έλ° μ«μ κ°μ΄ κ°μ κ²½μ° - λ³Ό
- μ«μ κ°μ΄ λ€λ₯Έ κ²½μ° - λ«μ±
- μ¬μ©μκ° μλ ₯ν κ°μ λν μ€ν κ²°κ³Όλ₯Ό κ΅¬νλ€

## 1λ¨κ³ - Util μ±κ²©μ κΈ°λ₯μ΄ TDDλ‘ λμ νκΈ° μ’μ

- μ¬μ©μλ‘λΆν° μλ ₯ λ°λ 3κ° μ«μ μμΈ μ²λ¦¬
    - 1~9μ μ«μμΈκ°?
    - μ€λ³΅ κ°μ΄ μλκ°?
    - 3μλ¦¬μΈκ°?

ValidationUtilsTest.java

```java
import org.junit.jupiter.api.DiaplayName;
import org.junit.jupiter.api.Test;

import static org.assertj.core.api.Assertions.assertThat;

public class ValidationUtilsTest {
	@Test
	@DisplayName("μΌκ΅¬_μ«μ_1_9_κ²μ¦") // (1)
	void μΌκ΅¬_μ«μ_1_9_κ²μ¦() {
		boolean result = ValidationUtils.validNo(9); // (2)
		assertThat(result).isTrue();
		
		// μμ λ μ€ λ¦¬ν©ν λ§
		assertThat(ValidationUtils.validNo(9)).isTrue(); // pass : 1 cycle λ
		assertThat(ValidationUtils.validNo(1)).isTrue(); // pass
		assertThat(ValidationUtils.validNo(0)).isFalse(); // (3) fail : 2 cycle λ
		assertThat(ValidationUtils.validNo(10)).isFalse();
	}
}
```

(1) νκΈλ‘ μ μ΄λ λΌ. μν΅μ΄ μ€μνλκΉ.

(2) μΌλ¨ ν΄λμ€λ μμ§λ§ λ¨Όμ  μμ±νλ€. κ±°κΎΈλ‘ μμ±ν΄λκ°λ κ²μ΄λκΉ. μ»΄νμΌλ¬ μ΄μ©ν΄μ(κ°μ¬λ intelliJ μ) μΌλ¨ μμ±λΆν° νλ€.

ValidationUtils.java

```java
public class ValidationUtils {
	public static boolean validNo(int no) {
		if (no <= 9) { // (3)μμ failμ΄ λ¨λ μ½λμ΄λ―λ‘ μμ ν΄μ€λ€.
			return true;
		}
		return false;
	}

	// (3)μ λ¦¬ν©ν λ§ κ²°κ³Ό
	public static boolean validNo(int no) {
		if (no >= 1 && no <= 9) { 
			return true;
		}
		return false;
	}

	// λ¦¬ν©ν λ§ (λΆνμν λΆκΈ°μ²λ¦¬ μ κ±°) : 3 cycle λ
	public static boolean validNo(int no) {
		return no >= 1 && no <= 9;
	}

	// λ¦¬ν©ν λ§ (μμ μ²λ¦¬) : 4 cycle λ
	public static final int MIN_NO = 1;
	public static final int MIN_NO = 9;

	public static boolean validNo(int no) {
		return no >= MIN_NO && no <= MAX_NO;
	}
	
}
```

μ»€λ°μ νλμ νμ€νΈ μ½λμ ν΄λΉ κΈ°λ₯ κ΅¬ν λ° λ¦¬ν©ν λ§κΉμ§ λ§μΉ νμ νλ κ²μ κΆμ₯νλ€. μ»€λ° λ©μμ§λ νμ€νΈ μ½λμ displayNameμ΄ λ  κ²μ΄λ€. λ³΄κΈ°μ λͺννλ©° κΈ°λ₯ λ¨μλ‘ λ¨μ΄μ Έμ μ μ νλ€.

inputκ³Ό outputμ΄ λͺνν UTILμ± λ©μλκ° TDDνκΈ°μ μ’λ€. κ·Έλ¬λ―λ‘ μ΄λ¬ν λ©μλλΆν° TDDνλ κ²μ κΆμ₯νλ€.

## 2λ¨κ³ - νμ€νΈ κ°λ₯ν λΆλΆμ λν΄ TDDλ‘ λμ 

- μμΉμ μ«μ κ°μ΄ κ°μ κ²½μ° - μ€νΈλΌμ΄ν¬
- μμΉλ λ€λ₯Έλ° μ«μ κ°μ΄ κ°μ κ²½μ° - λ³Ό
- μ«μ κ°μ΄ λ€λ₯Έ κ²½μ° - λ«μ±

```java
COM / USER
123, 456 -> nothing
123, 245 -> 1ball
123, 145 -> 1strike

PlayResult result = Baseball.play(Arrays.asList(1, 2, 3), Arrays.asList(4, 5, 6));
/**
λ°°μ΄λ‘ νλ©΄ λλ¬΄ λ³΅μ‘νλ€. νλ νλ μͺΌκ°μ ν΄λ³΄λ μμμ νμ.
*/

---
μμ λ¨μλ‘ μͺΌκ°κΈ°
---
COM / USER
1, 4 -> κ²°κ³Όλ₯Ό μ μ μλ€. μμΉκ°μ λͺ¨λ₯΄λκΉ!

μμΉκ°, μ«μ
1 4 , 1 4 -> strike
1 4 , 2 4 -> ball
1 4 , 2 5 -> nothing

```

BallTest.java

```java
public class BallTest {
	@Test
	void nothing() {
		Ball com = new Ball(1, 4); // λ μλ κ±°λΆν° μμ±ν΄μ£Όμγ
		BallStatus status = com.play(new Ball(2, 5));
		assertThat(status).isEqualTo(BallStatus.NOTHING);
	}

	@Test
	void ball() {
		Ball com = new Ball(1, 4); // λ μλ κ±°λΆν° μμ±ν΄μ£Όμγ
		BallStatus status = com.play(new Ball(2, 4));
		assertThat(status).isEqualTo(BallStatus.BALL);
	}
}

/* BallTestμ μ€λ³΅ μ½λ(Ball com = new Ball(1, 4);) λ¦¬ν©ν λ§*/
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

		/* play() λ¦¬ν©ν λ§ */
		public BallStatus play(Ball ball) {
			if (ball.matchBallNo(ballNo)) {
				return BallStatus.BALL;
			}
			return BallStatus.NOTHING;
		}

		private boolean matchBallNo(int ballNo) {
			return this.ballNo == ballNo;
		}

		/* strike μΆκ° */
		public BallStatus play(Ball ball) {
			if (this.equals(ball)) {
				return BallStatus.STRIKE;
			}
			if (ball.matchBallNo(ballNo)) { // ballμμ NPE κ°λ₯μ± μμΌλ―λ‘ nullμΈμ§ μ²΄ν¬ν΄μ€μΌ ν¨
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

### λμ΄λλ₯Ό λμ¬μ...

```java
COM / USER
123 / 1 4 -> nothing
123 / 1 2 -> ball
123 / 1 1 -> strike

μ΄λ²μ Listμ μ«μλ₯Ό λΉκ΅ν΄λ³΄μ.
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
						// .filter(status -> status != BallStatus.NOTHING) λ¦¬ν©ν λ§1
						// .filter(status -> status.isNotNothing()) λ¦¬ν©ν λ§2
						.filter(BallStatus::isNotNothing)
						.findFirst()
						.orElse(ballStatus.NOTHING);
		}

		(public) PlayResult play(List<Integer> balls) { // public μ§μλ λ¨ private λ©μλμ λ€λ¦ μλ€.
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
	
	// enumλ νλμ ν΄λμ€κ³  κ°μ²΄κΈ° λλ¬Έμ μ΄λ κ² λ©μμ§λ₯Ό λ³΄λΌ μ μλ€.
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
		// if (status == BallStatus.STRIKE) { λ¦¬ν©ν λ§ : λ©μμ§μ λ΄μμ£Όλκ² μ’λ€
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

κ°μ²΄κ° κ°κ³  μλ μν λ°μ΄ν°λ₯Ό getμ ν΅ν΄ μ κ·Όνλ κ² μλ€λ©΄ κ·Έλ κ² νμ§ λ§κ³ , λ©μμ§λ₯Ό λ³΄λ΄μ, μν λ°μ΄ν°λ₯Ό κ°λ κ°μ²΄κ° μΌμ νκ² λ§λ€μ΄λΌ.
κ·Έκ²λ§ ν΄λ TDDν  μΌμ΄ λ§λ€.

[Balls.java](http://balls.java) μ play() λ₯Ό μΈν°νμ΄μ€ν ν  μλ μλμ?
( μλ Playable μ΄λ interface λ₯Ό λ§λ€μ΄λ³΄μλ€. )

μΈν°νμ΄μ€λ₯Ό μΆμΆνλ κ²λ μ’μλ° 'νμν μμ μ' νλ κ² μ€μνλ€. μ κ·Έλ¬λ©΄ μΈν°νμ΄μ€λ₯Ό λ¨λ°νκ² λ  μ μλ€. play νλ μ΄ λ©μλμ λ³κ²½ κ°λ₯μ±μ΄ μλ€κ±°λ λ€λ₯Έ λ°©μμΌλ‘ playνλ κ²°κ³Όκ° μλ€λ©΄ κ΅¬νμ²΄λ₯Ό λ§λλ κ² μλ―Έκ° μκ² μ§λ§ κ·Έλ μ§ μλ€λ©΄ νΉλ³ν μλ―Έλ μμ κ² κ°λ€.

```java
public interface Playable {
		PlayResult play(List<Integer> balls);
}
```

```java
public class Balls implements Playable {
	...
	// μ΄ν λμΌ 
	...
}
```

private λ©μλλ νμ€νΈ μ½λλ₯Ό μμ±ν΄μΌ ν κΉμ? ex. [Balls.java](http://balls.java) μ PlayResult play(List<Integer> balls) λ©μλ

λ°λμ ν  νμλ μμ§λ§ νμΈμ΄ νμνλ€λ©΄ λ§λ€μ΄μΌκ² μ§μ..?

μμΉλ‘ μλ€μ λ©μλμ private μ κ·Όμ νμλ₯Ό μ μ§νκ³  reflectionμ μ΄μ©ν΄μ νμ€νΈμ½λμμ νΈμΆνλ λ°©μμ κ³ μ§νκΈ°λ νλ€. κ·Έλ¬λ λ(κ°μ¬)μ κ²½μ° μ€μ©μ£Όμμμ΄κΈ° λλ¬Έμ ν΄λΉ λ©μλλ₯Ό κ°μ package μμ μλ νμ€νΈ μ½λλΌλ©΄ defaultλ‘ λ°κΎΈκ±°λ publicμΌλ‘ ν΄μ νμ€νΈ μ½λλ₯Ό μμ±νκΈ°λ νλ€.

κ·Έλ¬λ, private λ©μλλ₯Ό κΌ­ νμ€νΈλ₯Ό ν΄λ³΄μμΌ νλ κ²½μ°λΌλ©΄ ***ν΄λΉ λ©μλμ μμΉκ° μ λ§ κ·Έκ³³μ΄ λ§λμ§*** νμΈνλ κ²λ νλμ ν¬μΈνΈκ° λ  μ μλ€. λ§μ½ λ€λ₯Έ ν΄λμ€λ‘ μ?κΈ΄λ€λ©΄ κ·Έ λ©μλλ openλλ κ²μ΄κΈ° λλ¬Έμ(=Balls.javaμμ ν ν΄λμ€μ μλ ν΄λΉ λ©μλλ₯Ό νΈμΆνλκΉ) μ λ§ κ·Έ μμΉμ μλ κ² λ§λμ§ μκ°μ ν΄λ³΄μ. 

κ°μ¬λ private λ©μλλ‘ μ κ·Ήμ μΌλ‘ μͺΌκ°λ κ²μ μΆμ²νλ€. κ·Έλ¬λ κΌ­ λͺ¨λ  private λ©μλλ₯Ό νμ€νΈν  νμλ μλ€κ³  λ³Έλ€. publicμ ν΅ν΄μ λλΆλΆ λ€ νμ€νΈν  μ μκΈ° λλ¬Έμ΄λ€.

(μμΈ μ²λ¦¬λ₯Ό μν)

BallNumber.java

```java
public class BallNumber {
	public final static int MIN_NO = 1;
	public final static int MAX_NO = 9;

	private int no;

	public BallNumber(int no) {
		if (no < MIN_NO || no > MAX_NO) {
			throw new IllegalArgumentException("λ³Ό μ«μλ 1λΆν° 9μ κ°μ΄μ΄μΌ ν©λλ€.");
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
			// this.ballNo = ballNo; λ¦¬ν©ν λ§
			this.ballNo = new BallNumber(ballNo);
		}

		...
		
}
```
