# Github Profile 관리하기
```
210815 TIL #13 깃허브 프로필 세팅
```
마크다운 파일을 이용해 깃허브 프로필을 꾸며보자.

## 1. Repository 만들기
자신의 github 계정 이름과 똑같은 이름의 repository를 만들어 준다.
![image](https://user-images.githubusercontent.com/78305431/129457379-3b213403-58d3-4c70-aa99-984fe35f37af.png)

고양이가 열심히 설명을 해주고 있다. 대충 깃허브 프로필을 README 파일을 통해 꾸밀 수 있다는 것!

> 그러므로 ✔️**Add a README file** 을 체크해주어야 한다

***

## 2. README 파일 수정하기
이제 만든 레포에서 README.md를 취향에 맞게 수정하면 된다! 보통은 `짧은 소개, 사용해본 기술 스택, contact 등`의 정보를 넣는다.

> markdown 작성 시 미리볼 수 없기 때문에 미리보기 제공 서비스에서 한번 작성하고 복붙하기를 추천 https://dillinger.io/

***

## ✔️배지와 아이콘
:point_right: 출처 - [shileds.io 사용방법 참고](https://efficientuser.com/2019/09/12/add-some-cool-badges-in-your-github-repo/)
![image](https://user-images.githubusercontent.com/78305431/129457511-c23fa270-77ea-41c2-9405-8c86552efc02.png)

이렇게 배지로 자신의 스택을 보기 좋게 정리할 수 있다. 슬프게도 나는 아직 쓸 줄 아는 언어가 몇 없고 프로젝트 경험조차 부족하다. 그러나 이제부터 스택을 쌓아가면 되는 일이기에 배지와 아이콘 사용법을 익혀두어야 한다!

> 사실 처음 배지 기능에 대해 알았을 때 대체 어떻게 해야 하는지 감이 안 잡혔다. 그러므로 정말 정말 상세하게 적어놓도록 하겠다.
***

## ✔️배지 활용하기

먼저 Badge를 사용하기 위해서는 [배지](https://shields.io/)에 접속해야한다. 일단 들어가면 모두 영어로 되어 있는데 당황하지 않아도 된다.
![image](https://user-images.githubusercontent.com/78305431/130580421-abfe0aed-b47e-4db5-8cd2-deb55923eb70.png)

메인 페이지에서 만약 원하는 기능의 뱃지가 있다면 그대로 복사해서 사용하면 된다. 

스크롤을 밑으로 내리면 뱃지를 어떻게 사용하는지에 대한 설명이 나온다.

![image](https://user-images.githubusercontent.com/78305431/130578896-350f1180-f890-44a4-8060-c7b692fc9c4f.png)

- **LABEL** : 배지 라벨(왼쪽)
- **MESSAGE** : 배지 설명(오른쪽)
- **COLOR** : 배지 색상

[자세한 코드]
```
- 기본 형태
https://img.shields.io/badge/<LABEL>-<MESSAGE>-<COLOR>

- 마크다운에서 사용 (뱃지 링크 연결)
[![뱃지_이름](https://img.shields.io/badge/<LABEL>-<MESSAGE>-<COLOR>)](뱃지 클릭 시 입력할 링크)

- 마크다운에서 사용 (뱃지 링크 미연결)
![뱃지_이름](https://img.shields.io/badge/<LABEL>-<MESSAGE>-<COLOR>)

- HTML로 사용 (스타일 추가)
<img src="https://img.shields.io/badge/쓰고자하는_텍스트-컬러코드?style=flat-square&logo=simpleicons에서_아이콘이름&logoColor=white"/></a>&nbsp
```

## ✔️배지 예제로 알아보기
ex) `https://img.shields.io/badge/label-message-green` 라면 뱃지의 라벨(왼쪽 부분)에는 `badge`가 입력되고, 메시지(오른쪽 부분) 에는 `message`가 출력될 것이며, 색상은 `green`으로 하겠다는 것이다.

`![Badge ex1](https://img.shields.io/badge/label-message-green)`

:point_right: ![Badge ex1](https://img.shields.io/badge/label-message-green)

***

ex 2) `https://img.shields.io/badge/label-green` 라면 뱃지의 라벨에는 `badge`가 입력되고, 색상은 `green`으로 하겠다는 것이다.

`![Badge ex1](https://img.shields.io/badge/label-green)`

:point_right: ![Badge ex1](https://img.shields.io/badge/label-green)

> message 여부에 따라 color는 다른 영역에 적용된다.
***
## ✔️배지에 스타일 적용하기
뱃지에는 스타일도 적용할 수 있다. Shields.io에 자세하게 설명이 나와 있다.
![image](https://user-images.githubusercontent.com/78305431/130598280-29551383-9912-4d13-adff-54c18a37decb.png)

원하는 스타일 태그를 자신의 뱃지 코드 뒤에 이어 붙여주면 된다.
```
![Badge ex1](https://img.shields.io/badge/label-green?style=flat?style=flat-square)
```
:point_right: ![Badge ex1](https://img.shields.io/badge/label-green?style=flat-square)

***
## ✔️아이콘
아이콘은 배지를 꾸며주고 이미지를 통해 좀 더 명확하게 구분하도록 한다.

예를 들어, 똑같은 Java 스택을 나타내더라도 ![Java Badge](https://img.shields.io/badge/Java-007396?style=flat-square&logo=Java&logoColor=white)와 ![Java Badge](https://img.shields.io/badge/Java-007396) 는 명확하게 다르다. 

아이콘도 뱃지 코드 뒤에 `logo=원하는_로고_이름` 형식으로 작성해주면 되는데 로고는 [아이콘](https://simpleicons.org/) 에서 사용할 수 있다.





***
테크블로그나 인스타그램 링크

`<a href="링크걸_주소"><img src="https://img.shields.io/badge/쓰고자하는_텍스트-컬러코드?style=flat-square&logo=simpleicons에서_아이콘이름&logoColor=white&link=내링크"/></a>&nbsp`

참고 - https://velog.io/@woo0_hooo/Github-github-profile-%EA%B0%84%EC%A7%80%EB%82%98%EA%B2%8C-%EA%BE%B8%EB%AF%B8%EA%B8%B0