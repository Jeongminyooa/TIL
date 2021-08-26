# Modular Arthmetic (모듈러 연산)
```
210826 TIL #19 모듈러 연산
```
## ✔️ 모듈러 연산
우리가 프로그래밍에서 나머지 연산을 사용할 때에는 `A % C` 로 표현한다. 그러나 일반표기식으로 쓴다면 `A mod C`이다. 

즉, 모듈러 연산은 나머지를 구하는 연산자이다.

계산 중에 너무 큰 값이 만들어질 것 같고 결과값이 모듈러 연산한 나머지를 출력하는 문제라면, 중간에 연산을 하면서 바로 모듈러 연산을 해도 최종적으로 같은 값이 나온다.

![image](https://user-images.githubusercontent.com/78305431/130919216-82038ba3-6165-41b9-9e27-132f93fb9ede.png)

이처럼 모듈러 연산은 다음과 같은 분배법칙이 모두 성립한다.
***

## ✔️ 모듈러 연산 증명
```
(a + b) mod C = ((a mod C) + (b mod C)) mod C
```
 <details markdown="1">
<summary>증명식 보기</summary>

```java
// T와 S는 a와 b를 나눈 나머지
a mod C = T 
b mod C = S

// i와 j는 임의의 정수
a = T + iC
b = S + jC
```

(a + b) mod C

= ((T + iC) + (S + jC)) mod C

= ((T + S) + (i + j)C) mod C
` ==> C mod C = 0이므로 무엇을 곱해도 0 (i + j)C mod C = 0`

= (T + S) mod C

= ((a mod C) + (b mod C)) mod C
</details>

```
(a * b) mod C = ((a mod C) * (b mod C)) mod C
```
 <details markdown="1">
<summary>증명식 보기</summary>

```java
// T와 S는 a와 b를 나눈 나머지
a mod C = T 
b mod C = S

// i와 j는 임의의 정수
a = T + iC
b = S + jC
```

(a * b) mod C

= ((T + iC) * (S + jC)) mod C

= ((TS) * (TjC) * (SiC) * (ijC^2)) mod C
` ==> C mod C = 0 즉, TjC mod C = SiJ mod C = ijC^2 mod C= 0`

= (TS) mod C

= ((a mod C) * (b mod C)) mod C
</details>