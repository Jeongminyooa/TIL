# Git 기초 - Tag
```
210827 TIL #20 tag 
```
## ✔️ 태그(Tag)란?
무언가 표시를 해두기 위한 태깅 기능을 위한 것으로, 특정 커밋을 태그해 두는 것이다. 특정 커밋을 가리키는 링크라고 생각해도 좋다.

### ❓ commit과 tag의 차이점
커밋의 경우 `checkout`하여 내용을 수정할 수 있으나, 태그는 수정이 불가능하며, 따라서 읽기전용 커밋 같은 개념이다. 저장소의 소스 버전을 간간히 표시하기 위해서는 커밋 메시지 또는 브랜치로해서 표시하는 것보단 태그로 깔끔하게 하는 것이 좋다.

보통 태그는 **소프트웨어의 버전을 릴리즈 할 때 사용**한다. 예를 들어 제품이 1.0이 릴리즈 될 때 태깅을 한번 해 두고 1.1버전을 개발하면서 그 사이에 만들어지는 브랜치들과 커밋들이 존재하는데 이러한 것들은 커밋으로만 관리하다가 1.1버전이 완성되는 커밋에 태깅을 해두는 것이다.

한 번 붙인 태그는 브랜치처럼 위치가 이동하지 않고 고정된다. 

***
## ✔️ 태그 조회하기
`git tag` 명령으로 이미 만들어진 태그가 있는지 확인할 수 있다. (`-l`, `--list`는 옵션)
```
$ git tag
v1.0
v1.1
```
태그가 많은 경우 페이지 단위로 출력하므로 `스페이스나 엔터`를 누르면 다음 페이지가 출력된다. 태그 보기를 종료하려면 `q`를 입력한다.

태그는 문자 순서대로 정렬하여 보여주므로 버전 형식을 잘 따른다면 가장 오래된 버전이 가장 먼저 출력될 것이다. 그러나 검색 패턴을 사용하여 태그를 검색할 수 있으므로 순서는 크게 중요하지 않다.

만약 1.8버전대의 모든 태그를 보고싶다면
```
$ git tag -l "v1.8*"
v1.8.0
v1.8.0-rc0
v1.8.0-rc1
v1.8.0-rc2
v1.8.0-rc3
v1.8.0.1
v1.8.0.2
```

### ❓ 와일드카드를 사용해 tag 확인하기
단순히 모든 tag 목록을 확인하기 위해 `git tag` 명령을 실행 했을 때 `-l` 또는 `--list` 옵션이 적용된 것과 동일한 결과가 출력된다. 하지만 와일드 카드를 사용하여 태그 목록을 검색하는 경우에는 반드시 `-l` 또는 `--list` 옵션을 함께 사용해야 원하는 결과를 얻을 수 있다.

태그와 태깅된 커밋의 SHA-1 체크섬을 같이 보는 경우 `git show-ref --tags`를 사용한다.
```c++
$ git show-ref --tags
bcc8a837055fe720579628d758b7034d6b520f2e refs/tags/1.0
bcc8a837055fe720579628d758b7034d6b520f2e refs/tags/1.0.1
dbee06de85859af59591813d3004e6695b8bb278 refs/tags/1.0.2
4e3da33c59fafe34e237585743e86e24ba81046e refs/tags/1.0.3
```

`git show` 명령어를 사용하면 태그가 붙은 커밋에 대한 정보를 보여준다
```c++
$ git show v1.0
commit dc48b11e0c6c77e2b96e89a18f34d7b0c4f9a9d4 (HEAD -> master, tag: v1.0, origin/master, origin/HEAD)
Author: Dave Methvin <dave.methvin@gmail.com>
Date:   Wed Mar 7 20:09:09 2018 -0500
    squash! Set attributes all at once, src last
```
***

## ✔️ 태그 종류
Git 에서는 일반적으로 `이름 정보만을 갖는 태그(Lightweight tag)`와 보다 `상세한 정보를 포함하는 주석 태그(Annotated tag)`, 이 두 가지 태그를 사용할 수 있다.

- 일반 태그 (Lightweight tag)
    + 이름만 붙일 수 있다.
    + 브랜치와 비슷한데 브랜치처럼 가리키는 지점을 최신 커밋으로 이동시키지 않는다. 단순히 특정 커밋에 대한 포인터일 뿐이다.
- 주석 태그 (Annotated tag)
    + 이름을 붙일 수 있다.
    + Git 데이터베이스에 태그를 만든 사람의 이름, 이메일과 태그를 만든 날짜, 그리고 태그 메시지도 저장한다.
    + GPG(GNU Privacy Guard)로 서명할 수도 있다.

:point_right: 보통 '릴리스 브랜치(Relase branch)' 에서는 주석 태그를 사용하고, 로컬에서 일시적으로 사용하는 '토픽 브랜치(Topic branch)'에서는 이름만 만들어 붙이는 태그를 사용한다.

***
## ✔️ Lightweight 태그 생성하기
Lightweight 태그는 기본적으로 파일에 커밋 체크섬을 저장하는 것 뿐이다. 다른 정보는 저장하지 않는다. 그러므로 태그를 만들 때 `-a`, `-s`, `-m` 옵션을 사용하지 않는다. 

`git tag <tagname>` 형식으로 사용한다.
```
$ git tag v1.0     #태그를 생성합니다.
$ git tag -l "v1.0"   #생성된 태그를 확인
v1.0
```
Lightweight 태그 같은 경우 `git show` 명령어를 실행한다면 별도의 태그 정보를 확인할 수 없다.

***
## ✔️ Annotated 태그 생성하기
정보를 같이 남기고 싶은 경우 Annotated 태그를 사용한다.

`tag` 명령을 실행할 때 `-a` 옵션을 추가한다.
```
$ git tag -a v1.4 -m "my version 1.4"
$ git tag
v0.1
v1.3
v1.4
```
`-m` 옵션으로 태그를 저장할 때 메시지를 함께 저장할 수 있다. 명령을 실행할 때 메시지를 입력하지 않으면 Git은 편집기를 실행시킨다.

***

## ✔️ 특정 커밋에 태그 생성하기
현재 상태를 태깅하는 것이 아닌 과거의 커밋에 대해서도 태깅할 수 있다. 과거의 특정 커밋을 태깅하려면 해당 커밋의 SHA-1 체크섬 값을 알아야 한다.
```
$ git log --pretty=oneline #커밋 체크섬과 메시지만 보여줌
dc48b11e0c6c77e2b96e89a18f34d7b0c4f9a9d4 squash! Set attributes all at once, src last
1f4375a34227f42570d2b72e190e51bcfb1e8597 Ajax: Allow custom attributes when script transport is used
29e76e254059f8c2b695f4e41054260b52a6910d Misc: Update license prolog/epilog to placate Github checker
```
특정 커밋에 태그하기 위해서는 명령의 끝에 커밋 체크섬을 명시한다. 체크섬값을 모두 명시할 필요는 없고 다른 커밋의 체크섬값과 중복되지 않는 선에서 몇 글자만 사용해도 된다.

`git tag -a <tag name> <commit checksum>` 형식으로 사용한다.
```
$ git tag v1.3 1f4375a
$ git show v1.3
commit 1f4375a34227f42570d2b72e190e51bcfb1e8597 (tag: v1.3)
Author: Dave Methvin <dave.methvin@gmail.com>
Date:   Tue Sep 12 12:40:00 2017 -0400
    Ajax: Allow custom attributes when script transport is used
```

***
## ✔️ 태그를 원격 저장소에 Push 하기
`git push` 명령은 자동으로 리모트 서버에 태그를 전송하지 않는다. 태그를 만들었으면 서버에 별도로 `push`해야 한다. `git push origin <tag name>`을 실행한다. 
```
$ git push origin v1.5
Counting objects: 14, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (12/12), done.
Writing objects: 100% (14/14), 2.05 KiB | 0 bytes/s, done.
Total 14 (delta 3), reused 0 (delta 0)
To git@github.com:schacon/simplegit.git
 * [new tag]         v1.5 -> v1.5
 ```

 만약 한 번에 태그를 여러 개 Push 하고 싶으면 `--tags`옵션을 추가하여 `git push` 명령을 실행한다. 이 명령으로 리모트 서버에 없는 태그를 모두 전송할 수 있다.
 ```
 $ git push origin --tags
Counting objects: 1, done.
Writing objects: 100% (1/1), 160 bytes | 0 bytes/s, done.
Total 1 (delta 0), reused 0 (delta 0)
To git@github.com:schacon/simplegit.git
 * [new tag]         v1.4 -> v1.4
 * [new tag]         v1.4-lw -> v1.4-lw
 ```
 이제 누군가 저장소에서 Clone 하거나 Pull을 하면 모든 태그 정보도 함께 전송된다.

 ***
 ## ✔️ 태그를 Checkout하기 
 태그가 특정 버전을 가리키고 있고, 특정 버전의 파일을 체크아웃해서 확인하고 싶다면 다음과 같이 실행한다. 단, 태그를 체크아웃하면 (브랜치를 체크아웃 하는것이 아니라면) 'detatched HEAD(떨어져 나온 HEAD)' 상태가 되며 일부 Git 관련 작업이 브랜치에서 작업하는 것과 다르게 동작할 수 있다.
 ```
 $ git checkout 2.0.0
Note: checking out '2.0.0'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by performing another checkout.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -b with the checkout command again. Example:

  git checkout -b <new-branch>

HEAD is now at 99ada87... Merge pull request #89 from schacon/appendix-final

$ git checkout 2.0-beta-0.1
Previous HEAD position was 99ada87... Merge pull request #89 from schacon/appendix-final
HEAD is now at df3f601... add atlas.json and cover image
```
``detached HEAD''(떨어져나온 HEAD) 상태에서는 작업을 하고 커밋을 만들면, 태그는 그대로 있으나 새로운 커밋이 하나 쌓인 상태가 되고 새 커밋에 도달할 수 있는 방법이 따로 없게 된다. 물론 커밋의 해시 값을 정확히 기억하고 있으면 가능하긴 하다. 특정 태그의 상태에서 새로 작성한 커밋이 버그 픽스와 같이 의미있도록 하려면 반드시 브랜치를 만들어서 작업하는 것이 좋다.
```
$ git checkout -b version2 v2.0.0
Switched to a new branch 'version2'
```
물론 이렇게 브랜치를 만든 후에 version2 브랜치에 커밋하면 브랜치는 업데이트된다. 하지만, v2.0.0 태그는 가리키는 커밋이 변하지 않았으므로 두 내용이 가리키는 커밋이 다르다는 것을 알 수 있다.

---
출처 - https://git-scm.com/book/ko/v2/Git%EC%9D%98-%EA%B8%B0%EC%B4%88-%ED%83%9C%EA%B7%B8

https://dololak.tistory.com/348