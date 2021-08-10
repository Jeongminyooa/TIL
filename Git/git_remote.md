# Git 기초 - 리모트 저장소
```
210811 TIL #9
```
## ✔️ 리모트 저장소란?
인터넷이나 네트워크 어딘가에 있는 저장소

다른 사람과 함께 일한다는 것은 리모트 저장소를 관리하면서 데이터를 push하고 pull 하는 것이다. 리모트 저장소를 관리한다는 것은 저장소를 추가, 삭제하는 것뿐만 아니라 브랜치를 관리하고 추적할지 말지 등을 관리하는 것을 말한다.

## ❓ 원격 저장소? 로컬 시스템?
`remote'' 저장소라고 이름이 붙어있어도 이 원격 저장소가 사실 같은 로컬 시스템에 존재할 수도 있다.` 여기서 remote''라는 이름은 반드시 저장소가 네트워크나 인터넷을 통해 어딘가 멀리 떨어져 있어야만 한다는 것을 의미하지 않는다. 물론 일반적인 원격 저장소와 마찬가지로 push, pull 등의 기능은 동일하게 사용한다.

## ❓ Local&Remote
편의상 로컬 머신에 존재하는 모든 repository는 local이고 Github에 존재하는 모든 repository는 remote라고 한다면 
1. 로컬에서 `git init`을 새로운 git repository 생성
2. 깃허브에서 새로운 repository를 만든 후 `git clone`으로 가져오기.

이렇게 만든 local과 remote는 버전 관리 시스템. 그래서 local과 remote의 작업 내용을 서로 반영하기 위해 `push`와 `pull`
- `push`는 local에서 remote로 commit 이력을 업로드하는 것
- `pull`은 remote에서 local로 commit 이력을 다운로드하는 것

***

## ✔️ 리모트 저장소 확인하기
`git remote` 명령으로 현재 프로젝트에 등록된 리모트 저장소를 확인할 수 있다. 이 명령은 리모트 저장소의 단축 이름을 보여준다. 저장소를 Clone 하면 'origin' 이라는 리모트 저장소가 자동으로 등록되기 때문에 'origin'이라는 이름을 볼 수 있다.
![image](https://user-images.githubusercontent.com/78305431/128897707-7a93f4cd-1ee0-45c8-9628-c9df1d3284d5.png)

`-v` 옵션을 주어 단축 이름과 URL을 함께 볼 수 있다.
![image](https://user-images.githubusercontent.com/78305431/128897906-791129c1-5b85-4ea8-ad85-2d2f8afc4454.png)

리모트 저장소가 여러 개 있다면 이 명령은 등록된 전부를 보여준다. 여러 사람과 함께 작업하는 리모트 저장소가 여러개라면 다른 결과를 가진다.

리모트 저장소가 여러 개 등록되어 있으면 다른 사람이 기여한 내용(Contributions)을 쉽게 가져올 수 있다.

***
## ✔️ 리모트 저장소 추가하기
기존 워킹 디렉토리에 새 리모트 저장소를 쉽게 추가할 수 있는데 `git remote add <단축이름> <url>` 명령을 사용한다.

:point_right: url 대신에 단축이름을 사용할 수 있다. 
***
## ✔️ 리모트 저장소 Pull 하거나 Fetch 하기
```
$ git fetch <remote>
```
이 명령은 로컬에는 없지만, 리모트 저장소에는 있는 데이터를 모두 가져온다. 그러면 리모트 저장소의 모든 브랜치를 로컬에서 접근할 수 있어서 언제든지 `Merge`하거나 내용을 살펴볼 수 있다.

`git fetch` 명령은 리모트 저장소의 데이터를 모두 로컬로 가져오지만, 자동으로 Merge하지 않는다. 수동으로 해야 한다.

## ❓ origin
저장소를 `Clone`하면 명령은 자동으로 리모트 저장소를 `origin`이라는 이름으로 추가한다. 그래서 나중에 `git fetch origin` 명령을 실행하면 `Clone`한 이후 수정된 것을 모두 가져온다.

```
$ git pull
```
리모트 저장소 브랜치에서 데이터를 가져올 뿐만 아니라 자동으로 로컬 브랜치와 `Merge`시킬 수 있다.

:point_right: `git fetch`와 `git merge`를 함께 하는 것!

먼저 `git clone` 명령은 자동으로 로컬의 master 브랜치가 리모트 저장소의 master 브랜치를 추적하도록 한다. 그리고 `git pull` 명령은 Clone한 서버에서 데이터를 가져오고 그 데이터를 자동으로 현재 작업하는 코드와 Merge 시킨다.

***
## ✔️ 리모트 저장소에 Push 하기
```
$ git push origin master
```
프로젝트를 공유하고 싶을 떄 Upstream 저장소에 Push 할 수 있다. 

이 명령은 Colne한 리모트 저장소에 쓰기 권한이 있고, Clone 하고 난 이후 아무도 upstream 저장소에 push하지 않았을 때만 사용할 수 있다. 만약 다른 사람이 push 한 후에 push 하려고 하면 할 수 없다. 먼저 **다른 사람이 작업한 것을 가져와서 Merge 한 후에 push할 수 있다.**

## ❓ Upstream & DownStream
origin과 local을 기준으로 생각하면 origin이 upstream, local이 downstream이 된다. 그 이유는 `push`와 `pull`을 기준으로 생각했을 때 origin으로부터 local로 흐르는 관계가 형성되기 때문이다.
- local에서 origin으로 push
- origin에서 local로 pull

CLI로 push를 해보았다면 `git push -u origin main`이라는 명령어를 입력했을 텐데, 여기서 `-u` 옵션이 `--set-upstream` 옵션의 줄임으로 upstream을 설정한다는 뜻이다. 이 이후에는 `git push` 또는 `git pull`이라고 명령어만 입력해도 자동으로 origin의 main 브랜치로부터 push와 pull을 진행하는 이유가 upstream 옵션을 통해 해당 브랜치에서 upstream과 downstream 관게가 설정됐기 떄문이다.
***
## ✔️ 리모트 저장소 살펴보기
```
$ git remote show <리모트 저장소 이름>
```
리모트 저장소의 구체적인 정보를 확인할 수 있다.
![image](https://user-images.githubusercontent.com/78305431/128912120-6f1652ad-937c-4551-b48d-62cc61aa99ea.png)

:point_right: 리모트 저장소의 URL과 추적하는 브랜치를 출력한다. `git pull` 명령을 실행할 때 masger 브랜치와 Merge할 브랜치가 무엇인지 보여 준다. 
***
## ✔️ 리모트 저장소 이름을 바꾸거나 삭제하기
```
$ git remote rename <변경 전 리모트 저장소 이름> <변경 후 리모트 저장소 이름>
```
로컬에서 관리하던 리모트 저장소의 브랜치 이름도 바뀐다는 점을 생각하자.

```
$ git remote remove <리모트 저장소>
```
서버 정보가 바뀌었을 때, 더는 별도의 미러가 필요하지 않을 때, 더는 기여자가 활동하지 않을 때 필요하다. 해당 리모트 저장소에 관련된 추적 브랜치 정보나 모든 설정 내용도 함께 삭제된다.
***
참고 - https://git-scm.com/book/ko/v2/Git%EC%9D%98-%EA%B8%B0%EC%B4%88-%EB%A6%AC%EB%AA%A8%ED%8A%B8-%EC%A0%80%EC%9E%A5%EC%86%8C

https://pers0n4.io/github-remote-repository-and-upstream/
