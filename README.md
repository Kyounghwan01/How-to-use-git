# How-to-use-git
코드 공유 시스템 git의 작동 원리와 사용법

[TOC]




## Getting Started
프로젝트내 작업을 효율적으로 versioning 하기 위해 사용함



## 사용예제
terminal에서 git 타이핑시 설치하라는 정보가 없으면 끝.

```
git
```
## git 작동 원리

> git add 실행시 : 내부적으로 index, object 파일 생성된다 

## git init
> 버전관리를 위한 초기설정, init시 해당 파일에서 ls-al을 하면 .git(해당파일 버전관리에 대한 모든 정보)파일이 생성되어 있다.
```
git init
```

## git config --global user.email youremail@email-address
> 깃 처음 이용하기 전 해당 파일에 대해 작성자가 누군지 명시한다. 
```
git config --global user.email noh5524@gmail.com
```

## git add
> 해당 파일을 버전관리 시작하겠다. add 명령어 이전, 파일이 변경된 부분에 대해서는 버전관리 되지 않는다. 

> 프로젝트에 정말 중요한 파일과 당장 업데이트하지 않아도 되는 파일이 있는데, 전자와 후자의 파일을 분리하여 관리하고 싶을 때 해당 <br>명령어를 사용한다. 

> 해당 파일이 재 수정되면 다시 git add (파일 이름) 해야 함.

```
git add . 
git add f1.txt
```
## git commit
> add된 파일을 버전관리 실행한다.
```
git commit -a : add없이 방금 수정한 파일을 바로 commit 시켜준다
git commit -m : 커밋창 없이 바로 실행
git commit -am “11” : 바로 올린다. (add 명령어를 한번 이상 실시한 파일만 사용 가능)
```

## git statue
> git 저장소의 상태를 관찰한다

> 모든 정보가 commit되면 아무 정보도 나오지 않는다. git add를 하지 않는 비관리된 파일(untracked file), 관리 되는 파일이나 아직 add 하지 않은 보여준다. 

```
git statue
```

## git log
> 저장소에 바뀐 내역을 보여 준다 .
```
git log 

commit edb62babe8ba47c9500a640a88a04329589ea1e1 (HEAD -> master)
Author: kyounghwan <osc9245@naver.com>
Date:   Tue Apr 2 12:52:38 2019 +0900

    5

commit ed76de3a174013806a4eb30913ad07fda3c4d755
Author: kyounghwan <osc9245@naver.com>
Date:   Mon Apr 1 21:04:34 2019 +0900

    4
```

> commit 옆 주소는 커밋 주소이며, git log 주소 입력시 이 커밋 주소 이전의 커밋 메세지를 다 불러온다.<br>
커밋 메세지 사이 정보를 가져오고 싶을 때는 아래와 같이 입력하면 된다.
```
git diff 주소..주소
```
## git log -p
> 커밋 내용을 불러오되 커밋으로 인해 바뀐 부분까지 불러오고 싶을때 
```
git log -p 

commit ce70f1461d923988a589da5f9d61117d6c85a226 (HEAD -> master)
Author: kyounghwan <osc9245@naver.com>
Date:   Tue Apr 2 13:48:37 2019 +0900

    6

diff --git a/f1.txt b/f1.txt
index d9f32b3..659e266 100644
--- a/f1.txt
+++ b/f1.txt
@@ -1,2 +1,2 @@
-f1.txt : 5
+f1.txt source : 5
 
```

## git diff
> 바로 이전 수정한 작업을 보여준다. 커밋 이전의 파일만 나옴(git add시 git diff 하면 정보 안나옴)

## git reset vs revert
> 과거로 돌아가 commit을 취소한다(.git 파일 백업하고 실시할 것)<br>
주의 : 원격저장소에 코드 공유한 경우 절대 reset 명령어 실행하면 안된다. 내 컴퓨터에 버전 관리할때만 실행

> git revert : 커밋을 취소하면서 새로운 버전을 생성한다. 

## branch 
### branch 쓰는 이유 
> 여러 클라이언트의 요구사항이 달라지므로 하나의 파일을 분개하는 경우 사용
### command
```
Git branch exp (exp 브랜치를 만든다). —> 새로운 브랜치를 만들면 이전 master 브랜치 복사한다. 
Git checkout exp : exp브런치를 사용한다.
Git log —branches —decorate —graph : 각 브런치 별 가진 commit를 본다
Git log —branches —decorate —graph —online
Git log -p master..exp : master에는 없고 exp에는 있는 것 소스코드까지 나옴(master가 exp의 파일 다 가지고있으면 아무것도 안나옴)
Git diff master..exp : 있고 없고의 차이점을 알려준다 (소스코드 안의 차이 보여줌)

Git 병합
exp를 master로 병합 -> master로 이동후 git merge exp

Branch 삭제
Git branch -d exp
```
```
commit 27dd7510e7d3b05de3b876a48734cf7904af3cad (HEAD -> exp)
Author: kyounghwan <osc9245@naver.com>
Date:   Tue Apr 2 17:53:49 2019 +0900

    4

commit 6161968e05f3d1bb99860d520defa3e7220ca4f1
Author: kyounghwan <osc9245@naver.com>
Date:   Tue Apr 2 17:50:48 2019 +0900

    3

commit 1864c7604f1f4545fdadb55a6794a7b19e97017a (master)
Author: kyounghwan <osc9245@naver.com>
Date:   Tue Apr 2 17:46:04 2019 +0900

    2

commit 02186538a07c0f5fee511046e9b9661d54ffe41c
Author: kyounghwan <osc9245@naver.com>
Date:   Tue Apr 2 17:45:22 2019 +0900

    1
```
> Head : 현재 내가 접속한 branch 이름 (master브런치는 2번 commit이 가장 최신이다, exp브런치는 4번 commit이 최신이다)

## git 시간 조작

git log를 통해 commit의 정보를 확인하고 선택적으로 날짜를 임의적으로 바꾼다

직접수정 : rebase 명령어로 바꿈 

   1. 바꾸고자 하는 commit날짜의 이전 날짜를 기준으로 명령어 넣는다

      ```js
      git rebase -i edaba97bce2ad33494381d45d29caa70b8191b1e
      ```

   2. pick을 edit으로 바꾼다
   
   3. Amend 방식으로 날짜를 바꿈 
   
      ```
      git commit --amend --no-edit --date "바꿀날짜 "
      ```
   4. push
      ```
      git push --set-upstream origin master
      ```





## 업데이트 내역

* 0.2.1
    * 수정: 문서 업데이트 (모듈 코드 동일)
* 0.2.0
    * 수정: `setDefaultXYZ()` 메서드 제거
    * 추가: `init()` 메서드 추가
* 0.1.1
    * 버그 수정: `baz()` 메서드 호출 시 부팅되지 않는 현상 (@컨트리뷰터 감사합니다!)
* 0.1.0
    * 첫 출시
    * 수정: `foo()` 메서드 네이밍을 `bar()`로 수정
* 0.0.1
    * 초기 md 파일 세팅

## 기여 방법

1. (<https://github.com/Kyounghwan01/How-to-use-git.git>)을 포크합니다.
2. (`git checkout -b feature/fooBar`) 명령어로 새 브랜치를 만드세요.
3. (`git commit -am 'Add some fooBar'`) 명령어로 커밋하세요.
4. (`git push origin feature/fooBar`) 명령어로 브랜치에 푸시하세요. 
5. 풀리퀘스트를 보내주세요.

## 정보

노경환  – noh5524@gmail.com

## repository

* 생활코딩(지옥에서 온 GIT)


