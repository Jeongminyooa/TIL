# Markdown 작성법
```
210803 TIL #1
일반 텍스트 기반의 경량 마크업 언어
```

쉽게 쓰고 읽을 수 있으며 HTML로 변환이 가능하다. 특수 기호와 문자를 이용한 매우 간단한 구조의 문법을 사용하여 웹에서도 빠르게 컨텐츠를 작성하고 보다 직관적으로 인식할 수 있다.

💡 README.md도 마크다운 문서이다.

## **1. Header**
- '---' 또는 '===' 사용
```
This is an H1
=============
This is an H2
-------------
```
This is an H1
=============
This is an H2
-------------
***

- '#' 사용
```
# <h1>의 크기를 가진다.
## <h2>의 크기를 가진다.
...
###### <h6>의 크기를 가진다.
```

# h1의 크기를 가진다.
## h2의 크기를 가진다.
...
###### h6의 크기를 가진다.
***
## **2. 인용 (BlockQuote)**
- '>' 블럭 인용 문자
``` 
> This is a first blockqute.
>	> This is a second blockqute.
>	>	> This is a third blockqute.
```
> This is a first blockqute.
>	> This is a second blockqute.
>	>	> This is a third blockqute.


💡 인용문 안에서 다른 마크다운 요소를 포함 할 수 있다.
***

## **3. 목록**
- 순서 있는 목록
```
1. 첫번째
2. 두번째
3. 세번째
```
1. 첫번째
2. 두번째
3. 세번째

💡 자동으로 내림차순으로 정의된다.

- 순서없는 목록(글머리 기호 '*' '+' '-')
```
* 빨강
  * 녹색
    * 파랑

+ 빨강
  + 녹색
    + 파랑

- 빨강
  - 녹색
    - 파랑
```
* 빨강
  * 녹색
    * 파랑

+ 빨강
  + 녹색
    + 파랑

- 빨강
  - 녹색
    - 파랑
***
## **4. 코드**
4개의 공백 또는 하나의 탭으로 들여쓰기를 만드면 들여쓰지 않은 행을 만날때까지 변환이 계속 된다.

- 들여쓰기 
```
This is a normal paragraph:

    This is a code block.
    
end code block.
```
This is a normal paragraph:

    This is a code block.
    
end code block.
*** 

- 코드블럭코드("``")
<pre>
<code>
```
public class BootSpringBootApplication {
  public static void main(String[] args) {
    System.out.println("Hello, Honeymon");
  }
}
```
</code>
</pre>
💡 github에서는 코드 시작점에 사용하는 언어를 선언하면 문법 강조가 가능하다.
<pre>
<code>
```java
코드들..
```
</code>
</pre>

```java
public class BootSpringBootApplication {
  public static void main(String[] args) {
    System.out.println("Hello, Honeymon");
  }
}
```
***
- 'pre' 코드 블럭 사용
```
<pre>
<code>
public class BootSpringBootApplication {
  public static void main(String[] args) {
    System.out.println("Hello, Honeymon");
  }

}
</code>
</pre>
```
***
## **5. 수평선**
```
***
-----
<hr/>
```
***
-----
<hr/>

## **6. 강조 ('*' '-')와 띄어쓰기**
```
*이태릭체*
**볼드체**
***이태릭+볼드체***
~~취소선~~
```
*이태릭체*
**볼드체**
***이태릭+볼드체***
~~취소선~~

- 띄어쓰기
띄어쓰기를 여러번 적용하고 싶다면
```
&nbsp;&nbsp;&nbsp;
```

***

## **7. 링크**
- 참조링크
```
[link keyword][id]

[id]: URL "Optional Title here"

// code
Link: [Google][googlelink]

[googlelink]: https://google.com "Go google"
```
Link: [Google][googlelink]

[googlelink]: https://google.com "Go google"
***

- 외부링크(인라인 링크)
```
사용문법: [Title](link)
적용예: [Google](https://google.com, "google link")
```
Link : [Google](https://google.com, "google link")
***

- 자동 연결
```
일반적인 URL 혹은 이메일주소인 경우 적절한 형식으로 링크를 형성한다.

* 외부링크: <http://example.com/>
* 이메일링크: <address@example.com>
```
* 외부링크: <http://example.com/>
* 이메일링크: <address@example.com>
*** 

- 다른 md파일로 이동

상대 경로를 이용해야 한다.
```
1. 현재 위치인 ETC 파일의 markdown.md 파일에서 상위 README.md로 이동하기

[README.md 이동](../README.md)
```
[README.md 이동](../README.md)

```
2. 현재 위치인 ETC 파일의 markdown.md 파일에서 (../Git/Git과 Github 기초.md)로 이동하기

[Git과 Github 기초 이동](../Git/github_Foundation.md)
```
[Git과 Github 기초 이동](../Git/github_Foundation.md)
***
- 같은 md 파일 안에서 이동

md 파일의 내용이 길 경우, 문서 상단의 목차에서 원하는 영역으로 바로 이동할 수 있도록 할 때 사용한다. 이를 위해서는 각 내용이 **헤더 태그**를 사용해야 한다.
```
[같은 md파일 안에서 이동](#Markdown-작성법)

주의할 점 : 공백은 -으로바꾼다.
이모지, 마침표(.), 콤마(,)생략 
헤더 태그의 레벨(h1~h6)은 신경쓰지 않아도 된다.
```
[같은 md파일 안에서 이동](#Markdown-작성법)
***
## **8. 이미지**

이미지가 프로젝트 내에 존재하면 상대경로, 외부에서 가져오는 이미지는 절대경로
```
![엑박시 보여질 이미지명](이미지주소)

![Alt text](/path/to/img.jpg)
![Alt text](/path/to/img.jpg "Optional title")
```

사이즈 조절 기능은 없기 때문에 `<img width="" height=""></img>`를 이용한다

```java
<img src="/path/to/img.jpg" width="450px" height="300px" title="px(픽셀) 크기 설정" alt="RubberDuck"></img><br/>

<img src="/path/to/img.jpg" width="40%" height="30%" title="px(픽셀) 크기 설정" alt="RubberDuck"></img>
```
***


## **9. 이스케이프 문자**
특수 문자의 기능을 무시한다.

```
\# 출력
```
\# 출력
***
## **10. 줄바꿈**
3칸 이상 띄어쓰기를 하면 줄이 바뀐다.

***
## **11. 이모지**
[더 많은 이모지](https://gist.github.com/Jeongminyooa/66009168b615dd9d5143be8a20e6f40c)

***
## **12. 테이블**
```
<!-- Markdown -->
Title1|Title2
-|-
content1|content2
content3|content4
  
Title1|Title2|Title3
:-|:-:|-:
content1|content2|content3
<!-- Html -->
<figure>
    <table>
        <thead>
            <tr>
                <th>Title1</th>
                <th>Title2</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>content1</td>
                <td>content2</td>
            </tr>
            <tr>
                <td>content3</td>
                <td>content4</td>
            </tr>
        </tbody>
    </table>
</figure>
  
<figure>
    <table>
        <thead>
            <tr>
                <th style='text-align:left;' >Title1</th>
                <th style='text-align:center;' >Title2</th>
                <th style='text-align:right;' >Title3</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td style='text-align:left;' >content1</td>
                <td style='text-align:center;' >content2</td>
                <td style='text-align:right;' >content3</td>
            </tr>
        </tbody>
    </table>
</figure>
```
<!-- Markdown -->
Title1|Title2
-|-
content1|content2
content3|content4
  
Title1|Title2|Title3
:-|:-:|-:
content1|content2|content3
<!-- Html -->
<figure>
    <table>
        <thead>
            <tr>
                <th>Title1</th>
                <th>Title2</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>content1</td>
                <td>content2</td>
            </tr>
            <tr>
                <td>content3</td>
                <td>content4</td>
            </tr>
        </tbody>
    </table>
</figure>
  
<figure>
    <table>
        <thead>
            <tr>
                <th style='text-align:left;' >Title1</th>
                <th style='text-align:center;' >Title2</th>
                <th style='text-align:right;' >Title3</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td style='text-align:left;' >content1</td>
                <td style='text-align:center;' >content2</td>
                <td style='text-align:right;' >content3</td>
            </tr>
        </tbody>
    </table>
</figure>

***
## **13. 글씨색**
```
<span style="color:yellow">노란 글씨입니다.</span>
```
<span style="color:yellow">노란 글씨입니다.</span>
***
## **14. 접기/펼치기**
```
<details markdown="1">
<summary>접기/펼치기</summary>

<!--summary 아래 빈칸 공백 두고 내용을 적는공간-->

</details>
```

참고 - https://gist.github.com/ihoneymon/652be052a0727ad59601
https://github.com/mangdo/TIL/blob/main/ETC/markdown.md#9.-%EB%A7%81%ED%81%AC