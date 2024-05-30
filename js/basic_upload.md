# 깃허브에 공부한 내용 올리기\_basic

---

**_1. Issue 생성하기_** - Title: 공부 키워드 작성 - Assignees - 본인 등록 - submit new issue

**_2. vs code 에서 branch 생성_**
`- git checkout -b branchname(#이슈번호_이슈이름)`

**_3. 공부한 내용 작성 왼쪽 하단 branch가 main이 아닌 지 확인_**
-local에 저장된 상태

**_4. local에서 원격으로 올리는 작업이 필요_**
-local -> **내 컴퓨터** -원격 -> **web desktop(Github)**

**_5. 소스제어 클릭 후 변경 내용 스테이징_**

**_6. 커밋 메시지 작성_**
`add: 작성내용(한국어 가능)`

**_7. 커밋 후 push를 통해 원격에 올리는 작업 실시_**
`- git push origin #branch이름 `

**_8. GitHub 접속_**
-pull requests
-compare & pull request -이때 base가 main을 향하는 지 꼭 확인
-create pull request

---

## 수정법

---

**_1. 수정내용 작성_**

**_2. 소스제어 클릭 후 변경 내용 스테이징_**

**_3. 커밋 메시지 작성_**
`fix: 수정내용(한국어 가능)`

**_4. 커밋 후 push를 통해 원격에 올리는 작업 실시_**
`- git push origin #branch이름 `

---

\*main branch로 이동 후 자료 가져오기

_-git checkout main_
_-git pull origin main_

ps. git checkout main 후 git pull origin main을 습관화 하자.
