# HKPictures

[https://github.com/tkfka1/HKPicture](https://github.com/tkfka1/HKPicture)

# HKPictures

## 프로젝트 개요

요즘 빠져있는 Stable Diffusion AI를 사용해서 이것저것 많은 이미지들을 만들다 보니 이 이미지들을 편리하게 **저장및 한눈에 볼 수 있는 사이트**를 개발하고 싶었다.

**인스타그램이나 핀터레스트처럼** 이미지들을 보기 편하게 나열하는것을 목표로 프로젝트를 진행한다.

또한 stable diffusion webui api를 사용하여 이미지를 제작 후 바로 저장이 되는것을 최종 목표로 한다.

## 사용 기술스택

| 이름 | 용도 |
| --- | --- |
| Python | 주 개발 언어 |
| Django | 백엔드 프레임워크 |
| mysql | 배포용 DB |
| sqlite3 | 개발용 DB |
| bootstrap | css 라이브러리 |
| HTML, JS, CSS | 정적 페이지 구성기술 |
| jenkins, k8s | 빠른 개발을위해 자동배포 및 유지보수를 위한 컨테이너 사용 |

### Django를 사용한 이유

많은 부분이 이미 만들어져있어서, 쉽고 빠르게 프로젝트를 만들 수 있다.

- 데이터베이스 대화기능, 어드민 패널, 유저 인증 기능 등등

보안에도 많은 신경을 써서 보안이 가능하며 그 부분을 따로 생각을 많이 할 필요가없다. 

많은 기업들이 사용하고 있어서, 신뢰도가 높다.

Python 이라는 언어를 사용함으로 앞으로 AI의 기능을 통해 이미지의 분류및 여러 AI 관련 알고리즘을 넣을 수 있는 기반을 마련할 수 있다.

## DB

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b54a7760-cf65-4282-825c-43ebf0fbf5f3/Untitled.png)

- 기본적인 장고의 user와 group을 이용해서 user부분을 구성했다.
- **profileapp (프로필)**
닉네임, 프로필이미지, 자기소개가 들어가고 기본장고의 userID와 관계를맺고 있다.
- **projectapp (주제)**
주제의 이미지, 이름, 주제설명, 생성날짜가 들어간다.
- **articleapp (이미지)**
이미지의 제목,이미지,댓글,제작날짜,좋아요가 들어가며 projectID와 userID로 관계를 맺고있다.
- **likeapp (좋아요)**
어떤 이미지를 어떤 사람이 좋아요를 눌렀는지 저장을위해 articleID와 userID로 관계를 맺고 있다.
- **commentapp (댓글)**
좋아요와 같지만 댓글 내용이 있다는점이 차이점이다.

## App

![test.svg](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ccd4540a-782e-43a8-9878-deb94f0809d1/test.svg)

### 기능 구성

**accountapp**

- 로그인, 로그아웃,장고 기본기능활용및 마이페이지 정보수정 등user관련 CRUD

**articleapp**

- 이미지 생성 및 제거, 수정 article관련 CRUD

**projectapp**

- 주제 생성 및 제거, 수정 project관련 CRUD

**commentapp**

- 댓글 생성 및 제거, 수정 comment관련 CRUD

**likeapp**

- 좋아요 생성 및제거, 수정 like관련 CRUD

**profileapp**

- 내 정보의 프로필 관리 기능(프로필이미지, 소개등) CRUD

### 화면 구성

기본 베이스인 header.html, base.html, foorter.html 로 구성이 되어 있고

각종 APP의 templates에도 나누어져서 html 구성이 되어 있음

**회원가입**

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/04373983-9a5a-4f30-82da-3d146e3858d0/Untitled.png)

**이미지**

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/bd51465d-81dd-479c-a0e6-99491e5954a1/Untitled.png)

**주제**

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/33112c47-3724-488d-ab06-67a88154b413/Untitled.png)

**구독중 주제**

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6b8f3ec4-75b7-45cb-90d7-071b0f33a10e/Untitled.png)

**마이페이지**

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/32c4c092-24f8-46f9-8b17-445289c91794/Untitled.png)

**마이페이지-정보수정**

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f63a1325-6e5b-4787-aa12-1d9fd82cab91/Untitled.png)

### 개선점, 후기

문제점 및 개선사항

- **처음 기획**했던 핀터레스트와 비슷한 처음 로그인 화면이 없음
메인 로그인 화면을 구현하고, **Oauth2** 기능을 사용해 소셜 로그인 기능 추가
- **MPA** 방식으로 제작되어 유지보수가 힘듬
**SPA** 방식으로 구현하여 유지보수를 용이하게 하며 많은 사람들이 사용하는 프론트엔드 프레임워크(React, Vue, anguler )를 이용하여 유지보수가 용이한 프로젝트로 발전
- 이미지가 **Django 프로젝트 폴더 내의 media 폴더에 저장**됨
**Cloud서비스 혹은 NAS**를 이용해서 사용할 수 있도록 연결
- 처음 기획했던 AI 그림출력후 바로 업로드 적용이 되지 않음
stabledefusion을 기반으로 한 api를 사용해서 직접 연산 후 적용이 되도록 구현
- **로그인, 회원가입 부분의 UX** 가 떨어짐(회원가입 후 바로 로그인안되는점, 댓글을 전부 작성을 한 후에 로그인이 되지 않았으면 로그인 페이지로 가는점 등)
메인 로그인이 생긴다면 어느정도 해결이 될 부분
- **크기가 다양한 이미지들의 레이아웃 처리**를 고려가 많이 되어있지 않음
크기를 하나 혹은 몇개의 이미지 크기 포멧을 만들고 그것에 맞추어 배치를 하는것을 고려
- 좋아요를 누른것들을 따로 모아서 볼 수 있도록
- 좋아요가 많은것들을 모을 수 있도록
- 최근순으로 뿐만이 아닌 여러 필터를 사용해서 이미지들을 분류하여 볼 수 있도록

향후 지향

- SPA 방식으로 Django DRF를 사용해서 RESTAPI 형식으로 개발을 할 예정
- 프론트엔드 프레임워크(React, Vue, anguler)를 사용하되 앞서 생각한 개선점들을 고려해서 프론트엔드 프레임워크를 정해서 개발
- stabledefusion을 기반으로 한 api를 사용해서 직접 연산 후 적용하기 위해 GPU를 사용하면서 Django를 같이 사용할 지 gpu만 사용해서 따로 api를 보내주는 백엔드를 개발할지 고민을 해보고 결정
