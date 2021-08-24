# Dynamic Programming (동적 계획법)
```
210824 TIL #18 DP
사용 언어 : JAVA
```
## ✔️ DP란?
여러 개의 하위 문제를 먼저 푼 후 그 결과를 쌓아올려 주어진 문제를 해결하는 알고리즘.

### ❓ 왜 DP가 필요한가?
분할정복 알고리즘에서 나누어진 작은 문제들이 여러번 겹쳐서 같은 문제를 계속 풀게되면 비효율적으로 계산을 하게 된다. 
```java
public static int fib_divide_conquer(int n) {
        if(n == 0) 
            return 0;
        else if(n == 1) 
            return 1;
        else
            return fib_divide_conquer(n - 1) + fib_divide_conquer(n - 2);
    }
```
그러므로 겹치는 문제들은 저장해두었다가 다음 문제를 풀 때 바로 값을 사용함으로써 다시 문제를 풀지 않는다. **시간을 줄이고 효율적인 프로그래밍이 가능한 기법**을 **동적 프로그래밍**이라고 한다.
```java
int fibo(int n) {
    int dp[20];

    dp[0] = dp[1] = 1 // 초기값 설정

    for(int i = 2; i <= n; i++) {
        dp[i] = dp[i-1] + dp[i-2]; // 점화식
    }

    return dp[n];
}
```


***

## ✔️ DP 속성
대표적인 예 ) 피보나치 수열
```
F(n) = F(n-1) + F(n-2)
```

1. Overlapping Subproblem : 부분 문제가 겹친다.

F(n)을 F(n-1)과 F(n-2)의 하위 문제로 나누어 풀 수 있다. 

2. Optimal Substructure : 최적 부분 구조

하위 문제인 F(n-1) + F(n-2)를 쌓아올려 F(n)을 풀 수 있다.

:point_right: DP는 **Optimal Substructure를 만족**하기 때문에 작은 문제로 큰 문제의 정답을 구할 수 있다. 그러므로 **작은 문제의 정답을 메모**해둔다.

***
## ✔️ DP 방식
1. Top-Down
```
큰 문제를 작은 문제로 나눈다.
작은 문제를 풀어서 큰 문제를 해결한다.

ex) 재귀 호출
```

2. Bottom-Up
```
문제를 크기가 작은 문제부터 차례대로 쓴다.
문제의 크기를 조금씩 크게 만들면서 문제를 푼다.
작은 문제를 풀어 큰 문제의 답을 구한다.

ex) dp 배열을 통한 메모
```