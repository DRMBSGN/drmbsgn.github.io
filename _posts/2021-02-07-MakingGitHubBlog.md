---
title: "[공부]GitHub 블로그 만들기"
categories:
  - etc
tags:
  - GitHub_Blog
  - Jekyll
last_modified_at: 2021-02-07T00:00:00-05:00
---
DeepLearning 관련 포스팅을 찾아볼 때 Github 블로그가 항상 눈에 띄였다.

GitHub가 코드들의 버전관리를 유용하게 해주는 플랫폼인건 알고 있어,

내가 여기서 블로그를 만들기 전까지는,

대충 네이버블로그와 같이 GitHub에서 저런 편집기를 제공해주는구나~ 하고 쉽게 생각했다.

실상은 그게 아니었지만 말이다.

먼저 시작하기 앞서, 필자는 웹이라고는 1도 모르는 전자공학도임을 밝힌다.

프로그래밍 실력도 필요할 때 마다 문법을 찾아보는 무지랭이의 수준이다.

그러니 전문지식을 가진자는 조용히 뒤로 가기 버튼을 누르기를 권장한다. :(

무지랭이와 함께 험난한 Github블로그 모험을 떠나볼 준비가 되었는가!!

자 그럼 시작해보자

__목차__
- [Github란?](#github--)
- [GitHub 설치](#github---)
- [GitPage 란?](#gitpage---)
- [Jekyll Theme 사용하기](#jekyll-theme-----)
- [루비 활용하기](#-------)
- [블로그 작성 팁](#--------)
  * [포스트 올려보기](#--------)
  * [마크다운 소소한 팁](#----------)
  * [Theme 수정하기](#theme-----)


<br/>
<br/>

## Github란?

+ __Github__ : Git을 사용하는 프로젝트를 지원하는 웹호스팅 서비스, Git을 업로드할 수 있는 웹사이트, 개발자들의 버전제어 및 공동 작업을 위한 플랫폼

+ __Git__ : 분산 소스 버전 관리 시스템, 서버를 분산시켜 구축할 수 있게 하는 소프트웨어

먼저 깃허브는 공과 계열 전공자라면 다들 어디선가 한번쯤 들어봤을 것이다.

소프트웨어 개발자들이 자신의 소스코드를 공유하거나 관리를 할 때 사용하는 서비스이며,  
 Git을 사용하여 자신의 프로그램 버전 업데이트, 버그 처리를 손쉽게 할 수 있다.

아니면 Git에 올라와 있는 오픈 소스들을 쉽게 가져올 수도 있다.

리눅스나 MacOS의 운영체제를 사용하는 사람은 이 Git이 왜 좋은지 경험적으로 알 수 있다.

Git을 설치한뒤 그냥 터미널 창에다가 명령어 몇줄만 쓱쓱 치더라도 Git에 접근이 가능하다!

Git 서버에 있는 저장소를 __원격 저장소__ 라고 부르고, 내 컴퓨터에 연동 된 디렉토리, 폴더, 저장소를 __로컬 저장소__ 라고 부른다.

우리는 원격저장소에 있는 파일들을 모두 복사해와서 로컬 저장소에서 작업을 할 수 있고,

이 코드들이 어느정도 완성된다면, 다른 사람들이 볼 수 있도록 나중에 원격저장소에 업로드할 수 있다.



개발자들이 코드들을 수정하고, 정리해서 업로드를 하면서 완성된 하나의 버전을 만들어낼 수 있다.

이 버전들은 시간이 지남에 따라 계속 수정이 될 것이고, 수정 시점마다  version 1, version 2 , .. 가 생성이 되며 하나씩 쌓여갈 것이다.

<br/>

<p>
<img src="/assets/images/MakingGitHubBlog/snapshots_1.png" width="600">
</p>

<br/>

Git은 이 버전이 하나씩 생성이 될 때 마다 그 버전일 때 파일의 내용을 나타내는 __스냅샷__ 이라는 파일을 만들어낸다.

처음에 버전1일때 스냅샷파일을 rev1라고 해보자.

그 이후에 개발자가 또 파일과 디렉토리를 수정해서 그걸 반영하면, 버전 2가 되는 것이고,  스냅샷 파일  rev2가 생성이 된다.

이렇게 Git은 수정할 때 마다 버전이 저장되고, 이때 스냅샷을 통째로 저장한다.

<br/>

<p>
<img src="/assets/images/MakingGitHubBlog/snapshots_2.png" width="400">
</p>

<br/>

만약 이렇게 계속해서 쌓아간다면, 1k였던 데이터들은 불어나서 버전 6까지 나왔다면 6k가 되어버릴 것이다.

그래서 Git은 적정시점에 버전 1부터 버전 6까지 되는 스냅샷 파일을 정리해주며, 이를 Garbage Collection이라고 부른다.

보통 가장 최근에 수정된 파일이 최종적인 파일이므로 이 경우, 버전 6 스냅샷은 원본 파일 그대로 놔둔뒤, 버전 5,4,3,2,1에 대한 스냅샷의 용량을 줄여버린다.

버전 6과 5의 차이, 버전 5와 4의 차이, 버전 4와 3의 차이 .. 등 5개의 "델타" 스냅샷을 저장하는 것이다.

<br/>
<p>
<img src="/assets/images/MakingGitHubBlog/snapshots_3.png" width="400">
</p>
<br/>

그렇게 하면, 우리는 적은 용량에 과거 버전부터 최근 버전에 해당하는 파일까지 모두 데이터베이스에 저장할 수 있게 된다.

만약 버전 6을 불러오고 싶다면 rev 6을 그대로 불러오면 되는거고, 버전 3을 불러오고 싶다면 (rev6 + delta(6-5) + delta(5-4) )의 파일들을 합쳐서 rev4를 반환할 수 있다.

우리가 저장소에서 데이터를 삭제하고, 코드를 삭제하더라도, Git의 입장에서 모든 행동은 데이터 추가이다.

우리 입장에서 삭제는 Git 데이터베이스에서의 삭제가 아니다.

<br/>

Git은 파일을 총 3가지 상태로 관리한다. 이해하기 쉽게 약간의 의역을 덧붙였다.

- Modified : 개발자가 해당 파일을 수정했으며, 아직 로컬 데이터 베이스에 안전하게 저장을 하지 않은 상태이다.   
파일 수정은 했지만, 아직 업로드 할까? 말까? 저장하기 전에 더 수정해야한다!인 불완전한 상태라고 보면 된다.

- Staged : 개발자가 확실하게 수정한 상태이다.   
이건 어느정도 된 것 같아! 로컬 데이터 베이스에 이 파일을 저장할 것이라고 __표시만__ 해 놓은 상태라고 보면 된다.

- Committed : 데이터가 로컬 데이터베이스에 안전하게 저장되었다를 의미한다.

<br/>

여기서 중요한 것. __Staged__ 상태였던 (확실하게 저장하기 위해 대기시켜놓은) 데이터들을 확실하게 저장하는 과정을 __Commit__ 이라고 부른다.   
(물론 파일을 수정하는 것 말고도 파일 저장, 파일 지우기도 Commit이라고 한다.)

__Commit__ 을 하면, 그  __흔적__ 이 데이터베이스에 무조건 남게 된다.  

우리가 만약에 저장소에 있는 파일 A가 필요없다, 삭제하겠다는 결심을 했다고 해보자.

우리는 폴더안에 있는 파일 A를 삭제한다면, 파일은 Modified 상태가 된다.

그리고 확신을 했기 때문에 이 파일을 Staged 상태로 바꿀 수 있다.

그리고 나서 그걸 Commit을 했다고 해보자.

이제 저장소에다가 프로젝트의 최신 버전 파일들을 보여달라! 하면 이 파일이 없어진 상태를 보여 줄 것이다.

다만, GitHub는 버전 관리 시스템이기 때문에 그 전 버전일 때 파일 목록을 보여달라고 할 때 삭제 전 파일을 반환해줘야 한다.

즉, 파일 A를 삭제하라고 했어도, __무조건 그 파일은 데이터베이스에 남아있게 된다.__

그렇기 때문에 아무렇게나 파일을 업로드 하고 Commit하고, 어 잘못됐네?  지워야겠네~ 하다가는

쓸 데 없는 파일들이 쌓여가서 데이터베이스 용량만 낭비하게 될거다.

우리는 신중해질 필요가 있다.

위와 같은 상황을 방지하기 위해 Git은 저장소에 반영을 하기까지 일련의 단계와 저장공간을 둔다.

자세하게 살펴보자.

<br/>
<p>
<img src="/assets/images/MakingGitHubBlog/status.png" width="400">
</p>
<br/>

<br/>

저장 공간

- working directory : 우리가 작업하는 공간을 의미한다.

- staging area: 저장소에 반영할 내용들을 쌓아가는 공간이다.

- .git directory (Respository): `git init` 을 실행하면 폴더 내에 .git이라는 폴더가 새로 생성되는데, 여기 내에는 프로젝트의 메타데이터들, 객체 데이터베이스. 각 버전에 대한 스냅샷들이 모두 저장이 되어 있다. 다른 컴퓨터에 있는 저장소들을 `git clone`하여 복사해 가져와 이 git 폴더를 생성할 수도 있다. 어쨌든 프로젝트의 내용이 들어있는 데이터 베이스이고,  내 컴퓨터인 로컬 저장소에 있는 데이터베이스라고 보면 된다.

<br/>

단계

+ Checkout the project: 우리는 git directory로 부터 프로젝트의 특정 버전을 복사하여 데이터들을 수정할 수 있다. 데이터들은 Working directory로 복사가되며, 우리는 이 작업공간에서 마음껏 개발하면 된다. 어떻게 수정을 하더라도, 프로젝트의 데이터베이스에는 흔적이 남지 않게 된다.

+ Stage Fixes : 우리는 수정을 완료하고나서 __Commit__ 할 데이터 정보를 __Staging Area__ 에 저장해야 한다. 이 정보를 저장하는 과정을 Stage Fixes라고 한다. 수정한 데이터 중 일부만을 픽스할 수도 있다.
이때 이 데이터들을 `.git` 폴더 내(git 저장소)에 저장하는데, 이를 Blob이라고 부른다.
그리고 Staging Area에는 이 파일을 식별할 수 있는 이름인 체크섬이 저장된다
<br/>

  * 체크섬은  SHA-1 해시이다. SHA-1라는 함수에 파일 내용 입력으로 하면 160비트(16진수 40자의 코드)를 생성할 수 있다. 그러면 이 코드가 바로 체크섬이 되고, 파일의 새로운 이름이 된다.
<br/>
  * 예시 : `24b9ac65552f25448a19200a07e97304c29c0889`
<br/>
  * 실제로, 하나의 폴더(tree 개체) 내에 많은 파일이 들어가 있을 수록 성능 저하가 발생하는데, 이를 방지하기 위하여 체크섬의 앞 두글자는 폴더(tree 개체)의 이름으로, 나머지는 파일(blob 개체)의 이름으로 사용된다.
  <br/>

  * 수정했지만 Staging area에 정보가없는 데이터는 __modified__ 상태이고, 수정되고 Staging area에 있는 데이터는 __staged__ 상태라고 보면 된다.

  <br/>

+ Commit : __Staging Area__ 에 저장된 정보(tree, blob 개체)들을 바탕으로 __하나의 버전__ 을 만든다.  즉, Git 디렉토리에 영구적으로 정보를 남기게 되는 거이다. 이때 _1) 루트 디렉토리 와 하위 디렉토리의 트리개체_ 를 _2)체크섬_ 과 함께 저장한다. 이 것이 __스냅샷__ 이다.  그리고  저자, 이전 커밋에 대한 포인터, 커밋 메시지를 저장하는 __커밋개체__ 는 Staging area에 있는 데이터의 스냅샷을 포인팅 하게 생성된다.
<br/>
  * Commit하는 건 버전을 남기는 것이기 때문에 명령어를 실행할 때 마다 메시지를 추가해 줘야한다.
  <br/>
  * Commit은 전의 어떤 Commit을 기준으로 바뀐 지 나타내기 위하여, 이전 커밋 포인터를 가지고 있다.

<br/>
Git에는 브랜치라는게 존재한다.

프로젝트에 있는 디렉토리와 파일들을 모두 복사해와서 독립적으로 개발을 할 수 있는 환경이 바로 브랜치이다.

여러 개의 branch들을 생성하며, 각각의 브랜치들에서 코드들을 수정해보고, 테스트할 수 있다.

그리고, 코드가 안정화가 되면, 중심 브랜치인 master branch(저장소를 생성할 때 맨처음에 만들어지는 브랜치.)에 이 branch를 합쳐 달라고 요청을 보낼 수 있다.

병렬적으로 여러 버전을 관리할 수 있는 branch를 통해, 개발자들은 버전의 유지보수를 하면서 새로운 기능 추가 및 버그 수정을 할 수 있다.

각각의 브랜치는 특정한 하나의 커밋을 가리키고 있다.

같은 것을 가리킬 수도, 수정함에 따라 다른 것을 가리킬 수도 있다.

지금 작업중인 브랜치는 HEAD라는 포인터가 가리키게 되고, `git checkout`을 통해 다른 브랜치에서 작업을 할 수도 있다.

이때 HEAD 포인터는 다른 브랜치를 가리키게 된다. 실제 브랜치 파일은 SHA-1 해시(16진수 40자의 코드)에 불과하다.

<br/>

+  __(원격 저장소) -> (내 폴더, 로컬 저장소, 로컬 브랜치)__  

원하는 저장소의 코드들을 다운받고 연동할 수 있다.  
이때 이 폴더가 바로 로컬 저장소가 된다.  
( `git init` : 새로운 Git 저장소를 만드는 명령어다.  저장소로 사용할 폴더에 초기화 작업을 진행.  
  `git clone [url]` : 기존 Git 저장소를 불러와 폴더와 연동하는 명령어이다.  
  새로운 디렉토리를 만들고 초기화 한 뒤, 해당 주소에 있는 원격 저장소와 연동한다.  
  즉, 안에 있는 파일들을 모두 로컬 저장소에 다운로드.  )  

<br/>

+   __(원격 저장소) -> (로컬 저장소, 로컬 브랜치)__  
만약 GitHub저장소에서 업데이트된 파일들이 있다면, 그 내용만을 내 저장소에 반영할 수 있다.  `git pull`

<br/>

+  __(로컬 저장소, 로컬 브랜치) <- (작업 공간)__  
 변경할 내용들을 로컬 저장소(.git 폴더)에 저장하는 작업을 `commit` 이라고 하는 데 이 작업을 하기 전, 선행되어야 하게 있다.  
 바로 *staging area* 라는 가상의 영역에 내가 저장공간에서 변경할 내용 중 어떤 내용만을 이 버전에 저장할 지 정보를 담는 것이다.  
 이 곳에 변경할 파일 정보를 올릴 수 있다 (`git add [파일이름]` 또는 `git add .` 를 통하여 tree와 blob을 저장한다 ).   
 지금까지 add된 내용은 `git status` 를 통해 확인할 수 있다.   
 `git commit -m [메시지]` 명령어를 사용하여 지금까지 *staging area* 에 올린 내용을 스냅샷으로 하는 커밋 개체를 생성할 수 있다.   
 그러면 내가 작업중인 브랜치는 이 커밋 개체를 가리키게 된다.

<br/>

+   __(원격 저장소) <- (로컬 저장소, 로컬 브랜치)__  
`commit` 을 하더라도, 내 로컬 저장소(로컬  branch)에만 적용이 될 뿐, 실제 원격 저장소(master branch)에 반영되지 않는다.   
즉, 원격 저장소의 Master branch에 내 branch에 적용된 내용을 똑같이 반영하는 작업을 해야하는데, 이를 `push` 라고 한다.

<br/>

+   __(원격 저장소) <- (로컬 저장소, 로컬 브랜치)__
특정 브렌치에서 타 브렌치에  `pull request`를 할 수 있다.   
풀요청을 해서 수정된 내용을 제안하고, 다른 사람의 리뷰를 요청하며, 타 브렌치가 그 브렌치와 합쳐지도록 요구한다.  
( pull request에 대한 건 일단 패스하도록 한다.)

<br/>


## GitHub 설치

참고로 Git은 Windows라면  [Git for Windows 설치 사이트](http://git-scm.com/download/win) 에서 다운받으면 설치 가능하고,

리눅스나 Mac이면 터미널에 몇몇 명령만 쓰면 바로 다운로드 가능하다. [Git 설치 참고 사이트](https://git-scm.com/book/ko/v2/%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0-Git-%EC%84%A4%EC%B9%98)

Github에서 회원가입을 하고 repository(저장소)를 만들어보자!

<br/>
<p>
<img src="/assets/images/MakingGitHubBlog/join.png" width="400">
</p>
<small> - 회원가입 창 </small>

<br/>

<p>
<img src="/assets/images/MakingGitHubBlog/join1.png" width="400">
</p>
<small>- 왼쪽 상단에는 저장소 새로 만들기 버튼이 있다. </small>

<br/>

GitHub블로그를 만들 때 우리는 Fork 기능을 사용할 예정이므로 일단 저렇게 원격저장소를 만들 수 있다는 것만 참고하자.

<br/>

Git Bash를 이용하여 작업공간으로 사용할 폴더를 만들고 이동한 뒤 Git directory로 설정하는 방법은 아래와 같다.

아직 Fork를 하기 전이니 이것도 참고만 하자.

```
$mkdir workspace
$cd workspace
$git init
```

이미 GitHub에 자기의 저장소를 만들었다면, git init 대신 `$git clone [url]` 를 사용하여 초기화 할 수 있다.

<br/>
<br/>

## GitPage 란?

GitHub page는 Github 저장소의 내용을 웹페이지로 만들어주는 서비스이다.  
블로그를 위한 저장소를 만든 뒤, Setting 메뉴에서 스크롤을 내려보면 아래와 같은 화면을 확인할 수 있다

<br/>

<p>
<img src="/assets/images/MakingGitHubBlog/page.png" width="400">
</p>

<br/>

내가 만든 저장소에 html을 넣으면 이 html에 맞게 웹페이지를 만들 수 있다.  

우리는 웹에 대한 지식이 부족하니, 다른 사람들이 만들어 놓은 테마들을 가져와 저장소에 저장하고, 블로그 웹 호스팅을 진행할 예정이다.

바로 Jekyll Theme를 사용해서 말이다.

<br/>

## Jekyll Theme 사용하기

<http://jekyllthemes.org/>  에 방문하면 여러가지 테마들을 발견할 수 있다.  
마음에 드는 테마를 골라보자.

__Chirpy__ 가 마음에 들어 클릭했다고 해보자. 그러면 아래와 같은 화면이 표시될 것이다.

 홈페이지에 들어가보자.

<br/>
<p>
<img src="/assets/images/MakingGitHubBlog/jekyll.png" width="400">
</p>

<br/>

그러면 이 테마에 대한 리소스들이 들어있는 저장소에 접속할 수 있다.

<br/>
<p>
<img src="/assets/images/MakingGitHubBlog/jekyll1.png" width="700">
</p>

<br/>

fork를 누르면 해당 테마의 내용들을 내 저장소로 그대로 복제해서 가져올 수 있다.

(일반적으로 다른 사람의 Github 저장소에서 내가 어떤 부분을 수정하거나 추가기능을 넣고 싶을 때 내 저장소로 복제해오는 작업을 Fork라고 한다. 여기에서는 테마를 가져오기위해 사용한다. pull request를 하지 않는 이상, 나는 이 forked 저장소에서 독립적으로 commit, push, pull을 계속 할 수 있다. )

<br/>

<p>
<img src="/assets/images/MakingGitHubBlog/jekyll2.png" width="700">
</p>

<br/>

블로그 주소를 설정해주기 위해 저장소의 이름을 바꿔보자.

일반적으로 뭐시기.github.io를 많이 사용해서 나도 저렇게 지정했다.

<br/>
<p>
<img src="/assets/images/MakingGitHubBlog/jekyll3.png" width="700">
</p>

<br/>
<p>
<img src="/assets/images/MakingGitHubBlog/jekyll4.png" width="700">
</p>

<br/>
저장소에 보면 _config 파일이 있는데, 여기에서 기본적인 블로그 설정이 가능하다.

<br/>
<p>
<img src="/assets/images/MakingGitHubBlog/jekyll5.png" width="700">
</p>

<br/>
위에있는 연필 표시를 클릭해서 내용을 기입하면 된다.

언어, 블로그 이름, 블로그 설명, base url, 주소, 작성자, 트위터, github이름, 로고(저장소에 넣고, 경로를 적어주면 적용된다. 나중에 필요할 때 그 외 셋팅들은 자잘하게 수정해주면 된다.)

블로그가 제대로 호스팅 됐는지 확인하기 위해서는 Setting 탭으로 들어가 GitHub pages를 확인해주면 된다.

 (스크롤을 내리다보면 발견할 수 있다.) 여기서 무언가 문제가 생긴다면 초록색 표시가 아닌 빨간색 표시가 나타나게 된다.

<br/>
<p>
<img src="/assets/images/MakingGitHubBlog/page.png" width="700">
</p>
<br/>

좀 더 쉽게 블로그를 편집하기 위해 로컬 저장소를 만들어보자.

<br/>

위에서 Git은 설치 완료했을 거라 생각한다. Git CMD를 켜서 다음의 명령어를 실행해보자.

원하는 위치에 작업공간을 만들고, 그 위치에서 블로그를 위한 원격저장소와 로컬 저장소를 연결한다.

```
$mkdir workspace
$cd workspace
$git clone [저장소 url]
```

이러면 블로그 셋팅은 50퍼센트 완료됐다.

<br/>

## 루비 활용하기

다만 이 상태로 블로그를 운영한다면 다소 비효율적으로 작업하게 된다.

원격저장소(Github홈페이지)에서 계속 포스트를 수정, 삭제하고, 테마를 편집하고 한다면, Commit이 많이 발생하게 된다.

한번에 우리가 소스코드를 수정하면 문제가 발생하지 않겠지만, 실제 웹페이지에 빌드가 될 때 내가 원하지 않는 형태로 나오는게 빈번하다.

즉, 우리는 이 자잘한 버그를 고치기 위해 Commit을 계속 하기 때문에 버전관리가 상당히 버거워지게된다. 또 데이터베이스도 낭비된다.

위에서 언급했듯, 확실하지 않은 코드들에 대해 Commit을 남발하는 건 좋지 않은 습관이다.

우리는 내 컴퓨터에서 "웹에 괜찮게 나오네!"를 확인 한 뒤 로컬 저장소에 적용하고, 또 이 내용을 원격 저장소에 올리고자 한다.

따로 설명은 안했지만, jekyll 테마는 루비언어로 작성된 프로젝트이다.

이 테마에서 제공하는  jekyll serve 명령어를 통해서 로컬 컴퓨터에서 블로그를 확인해볼 수 있다.

우리가 임의로 호스팅한 127.0.0.1:4000 주소에서 내 작업공간에서 수정한 내용을 바로바로 웹으로 볼 수 있다.

로컬 컴퓨터에서 호스팅을 해서 이 웹사이트 주소로 확인해 볼 수 있는 형태이다.

<br/>

<p>
<img src="/assets/images/MakingGitHubBlog/ruby.png" width="700">
</p>

<br/>


서버에 업로드할 내용이 확정되면,  git을 사용하여 로컬 저장소의 staging area에 추가.. 로컬 저장소에 Commit.. 원격 저장소로 push.. 를 진행한다.

원격 저장소에 반영된 순간, 실제 블로그에 변경사항이 적용된다.

아래는 작업공간에서는 포스팅이 완료됐지만 아직 push를 하지 않아 실제 블로그에서는 반영되지 않은 모습을 보여준다.

<br/>

<p>
<img src="/assets/images/MakingGitHubBlog/ruby1.png" width="700">
</p>



<br/>

Jekyll에 대한 자세한 내용은 다음을 참고하자.

<https://jekyllrb-ko.github.io/docs/ruby-101/>

<br/>

이 jekyll serve, gem install 등의 명령어들은 루비 프롬프트에서 실행 가능하다.

윈도우를 위한 루비 커맨드 프롬프트는 다음 사이트에서 설치가능하다.

설치 중간에 User UTF-8 as default external encoding에 체크를 하자.

<https://rubyinstaller.org/>

<br/>

설치된 루비 커맨드 프롬프트에서 `cd` 명령을 통해 로컬 저장소로 이동한 다음 명령어들을 실행해준다.

`gem install jekyll bundler`

이렇게 하면 지킬과 번들러 잼을 설치할 수 있다.

참고로 Ruby에서 Bundler는 프로젝트에 있는 Gemfile이라는 파일에 있는 젬(패키지)를 설치할때 도움이 되는 잼(패키지)이다.

<br/>

`bundle install`

현재 디렉토리에 있는 Gemfile를 토대로 필요한 Gem을 설치할 수 있다.

<br/>

`jekyll serve`

그리고 나서 위 명령어를 통해 사이트 빌드가 가능하다.

만약 빨간색 오류들이 뜬다면 오류를 잘 읽어보고, 더 필요한 잼들이 있는지 확인한다. 그리고  jekyll serve될 때까지 관련 잼 설치를 계속한다. gem install 뭐시기를 계속 반복해주면 된다.

인코딩 에러시 `chcp 65001` 를 사용해보자.

<br/>

<p>
<img src="/assets/images/MakingGitHubBlog/jekyll6.png" width="700">
</p>

<br/>


## 블로그 작성 팁

*테마에 따라 약간씩 다를 수 있다! READ_ME를 자세히 읽어보도록 하자*

<br/>

### 포스트 올려보기
-  _post 폴더에  markdown 문서를 넣으면 블로그 빌드시 자동으로 html 파일이 만들어진다.

- 어떻게 작성하는지 보려면, 디렉토리를 살펴보자! docs 폴더의 _post 폴더에 예시 마크다운 문서들이 널려있다.

- 마크다운 문법 참고
<https://cizz3007.github.io/%EB%A7%88%ED%81%AC%EB%8B%A4%EC%9A%B4/%EB%AC%B8%EB%B2%95/markdown/2018/04/08/markdown/>

- markdown을 쉽게 수정하기 위해서 atom 에디터를 사용할 수 있다. ( markdown preview plus를 설치하면 마크다운이 적용되는 것을 한눈에 파악할 수 있다.)

- markdown 저장시 자동으로 바뀌는 문제는 관련 플러그인 markdown-format을 꺼놓으면 해결된다.

- 포스팅에 숫자를 넣기 위해 Latex사용하는 방법은 다음과 같다. _layouts/post.html에 아래 내용을 <article> 태그 앞쪽에 넣어주면 된다.

```
  <script type="text/javascript" async
      src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
  </script>
```

-  로컬로 호스팅한 블로그(로컬 저장소)에서 반영이 안된다면, 루비 프롬프트를 확인해보자. 아마 Error 뭐시기 저시기 떠있을 것이다.

- 로컬에서 충분히 확인했으면, 실제 블로그에 반영해봐야한다.  Github 원격 저장소에 변경 사항을 올리는 것이다. 다음을 git CMD에서 실행한다.

```
  $ git add . (Staging area로 전체 수정된 파일들을 올린다. )
  $ git commit -m "메시지"  (로컬 저장소에 Staging area에 있는 파일들의 변경사항을 저장한다.)
  $ git push  (로컬 저장소의 변경사항을 원격 저장소에도 반영한다. 즉, 내 컴퓨터에서 작업한 포스트들이 Github page에 반영된다.)
```

<br/>

### 마크다운 소소한 팁

- markdown 이미지 추가시 가운데 정렬은 html 태그를 사용해서만 가능하다.

```
<p align="center">
<img src="/assets/images/cognitive1.png" width="200">
</p>
```

- 파워포인트는 구글 Docs에 올린 뒤 웹으로 내보내기를 누르면 된다. 아래에 src = 뒤의 주소에 자신의 ppt 주소를 넣는다.

```
<div class="responsive-wrap">
<!-- this is the embed code provided by Google -->
<iframe src="https://docs.google.com/presentation/d/e/2PACX-1vSRH89qSk92S2BnbPFfraSjRkFEVdf7lFmz3YSMjMkmMACr2-nAGQL7cJCzdtCDnPFaD3Bpd4Sxhzgn/embed?start=false&loop=false&delayms=3000" frameborder="0" width="1280" height="749" allowfullscreen="true" mozallowfullscreen="true" webkitallowfullscreen="true"></iframe>
<!-- Google embed ends -->
</div>
```

- 마크다운 작성 시 강제 줄바꾸기는 html 태그를 추가해서 가능하다.

```
<br/>
```


- Markdown 문서 작성시 직접 목차를 만들지 않아도 된다!

<https://ecotrust-canada.github.io/markdown-toc/>

<br/>

### Theme 수정하기

*_data 폴더의 theme.yml 파일을 수정해보자!*

- 카테고리 수정은 이 파일의 navigation_pages에서 가능하다.  
내 블로그는 예제파일에 있는 categories.md, posts.md를 그대로 가져와 사용했다.

<p>
<img src="/assets/images/MakingGitHubBlog/theme2.png" width="400">
</p>

<br/>
- 폰트는 두 단계를 거쳐서 수정이 가능하다.

  +  google_fonts에 원하는 구글 폰트의 이름, 크기, 굵기를 적는다.   
  예를 들어 내가 원하는 폰트가 'Noto Serif KR', serif' 라면 위의 사진처럼 변경해주는 것이다.
    <br/>
      <p>
      <img src="/assets/images/MakingGitHubBlog/theme1.png" width="400">
      </p>

  + 그 다음 _sass 폴더에서 변수가 저장되어있는 _variables를 수정해보자..  base-font-family가 폰트 이름에 대한 변수인 것으로 추정되므로 위와 같이 변경해준다.
  <br/>
    <p>
    <img src="/assets/images/MakingGitHubBlog/theme3.png" width="400">
    </p>
  + _variables에서 폰트 크기, 메뉴 열리는 시간 등 테마의 여러부분을 커스터마이징할 수 있다.

<br/>

참고 자료

<https://git-scm.com/book/ko/v2/Appendix-C%3A-Git-%EB%AA%85%EB%A0%B9%EC%96%B4-%EA%B3%B5%EC%9C%A0%ED%95%98%EA%B3%A0-%EC%97%85%EB%8D%B0%EC%9D%B4%ED%8A%B8%ED%95%98%EA%B8%B0>
