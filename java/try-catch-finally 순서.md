## try catch finally 동작 순서
finally always executes. If there is a return in try, the rest of try and catch don't execute, then finally executes (from innermost to outermost), then the function exits.

```jsx
try {
	a();
} catch {
	b();
} finally {
	c();
}
```

### 정상 작동 시

a() → c()

### 에러 발생 시

a() → b() → c();

```jsx
try {
	a();
	return;
} catch {
	b();
} finally {
	c();
}
```

### 정상 작동 시

a() → c() → return

### 에러 발생 시

a() → b() → c();
