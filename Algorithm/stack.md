# Stack (스택)
```
210804 TIL #2 stack
사용언어 : C언어
```
## ✔️Stack 이란?
먼저 들어간 자료가 나중에 나오는 자료구조. 


**후입선출 FILO(First In Last Out)**

![image](https://user-images.githubusercontent.com/78305431/128198423-37781f5b-d612-45fa-8fea-eb2566409d9e.png)

### ❓ Restricted structure
특정 위치에서만 원소를 넣거나 뺄 수 있는 제한이 걸려있는 자료구조 

```ex) 스택, 큐, 덱 ... ```
***

## ✔️원소의 삽입, 제거, 확인
```
시간복잡도 O(1)
```
원소의 확인은 원칙적으로 상단만 가능하다.
상단이 아닌 나머지 원소들의 확인, 변경이 불가하다. 

- 추가, 제거, 상단 원소 확인 외에는 스택이 제공하는 기능이 아니다.

***
[코드]
```C
// BOJ_10828
#include <stdio.h>
#define SIZE 10000
int arr[SIZE];
int top = 0;

int push(int x)
{
    if (top >= SIZE) return 0;
    arr[top++] = x;
    return 1;
}

int pop()
{
    if (top <= 0) return -1;
    else return arr[--top];
}

int size() {
    return top;
}

int empty() {
    if (top == 0) return 1;
    else return 0;
}

int get_top() {
    if (top >= SIZE || top <= 0)
        return -1;

    return arr[top - 1];
}

int main(void) {
    int n;
    char command[10];

    scanf_s("%d", &n); //주어지는 명령의 수

    while (n > 0) {
        n--;

        scanf_s("%s", command, 10);

        if (strcmp(command, "push") == 0) {
            int num;
            scanf_s("%d", &num);
            int rlt = push(num);

            if (rlt == -1)
                printf("error\n");
        }
        else if (strcmp(command, "pop") == 0) {
            printf("%d\n", pop());
        }
        else if (strcmp(command, "size") == 0) {
            printf("%d\n", size());
        }
        else if (strcmp(command, "empty") == 0) {
            printf("%d\n", empty());
        }
        else if (strcmp(command, "top") == 0) {
            printf("%d\n", get_top());
        }
    }
}
```
***
## ✔️스택의 활용 : 수식의 괄호쌍
문자열을 앞에서부터 읽어 나갈 때, 닫는 괄호는 남아있는 괄호 중에서 가장 최근에 들어오는 여는 괄호와 짝을 지어 없애버리는 명령이라고 생각하면 된다. 

ex ( { ( ) { } } )

1. 여는 괄호부터 스택에 push
2. 닫는 괄호를 만나면 스택의 가장 최근 들어오는 여는 괄호와 비교. 짝이 맞다면 삭제 
3. 남아있는 괄호가 없다면 확인 성공!
4. 남아있는 괄호가 있다면 올바르지 않은 괄호쌍

추가) 2번 

- 스택이 비어있다면 올바르지 않은 괄호쌍 
- 스택의 top이 짝이 맞지 않은 괄호일 경우는 올바르지 않은 괄호쌍
- 스택의 top이 짝이 맞는 괄호일 경우 pop

```C
// BOJ_2504
#include <stdio.h>
#include <string.h>
#define SIZE 100
char arr[SIZE];
int top = -1;

void init() {
    top = -1;
}

int push(char x)
{
    if (top >= SIZE - 1) return -1;
    return arr[++top] = x;

}

int pop()
{
    if (top < 0) return -1;
    else return arr[top--] = '\0';
}

char peek() {
    if (top >= SIZE - 1 || top < 0)
        return -1;

    return arr[top];
}
int empty() {
    if (top == -1) return 1;
    else return 0;
}
int main(void) {
    char input[SIZE];
    int rlt = 0;
    int temp = 1; // 중간 더하기 값
    int error = 0;

    gets(input);

    init();
    for (int i = 0; input[i] != '\0'; i++) {
        if (input[i] == '(') {
            temp *= 2;
            push(input[i]);
        }
        else if (input[i] == '[') {
            temp *= 3;
            push(input[i]);
        }
        else if (input[i] == ')') {
            //쌍이 맞지 않는다면 error 발생시켜 break -> 실행시간 단축
            if (peek() != '(' || empty()) {
                error = 1;
                break;
            }
            if (input[i - 1] == '(')
                rlt += temp;

            pop();

            temp /= 2;
        }
        else if (input[i] == ']') {
            if (peek() != '[' || empty()) {
                error = 1;
                break;
            }

            if (input[i - 1] == '[')
                rlt += temp;

            pop();

            temp /= 3;
        }
    }
    if (empty() && !error) printf("%d\n", rlt);
    else printf("0\n");

    return 0;
}
```