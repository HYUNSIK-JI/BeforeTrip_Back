 # 여행전날

   

   > 여행 전 필수 체크사항 정형화된 사이

   

   ## 프로젝트 소개
   
   - 🗓

     프로젝트 기간

     - 2023.03.01 (수) ~ 2022.03.08(수)

   - 📚 사용한 기술 STACKS

   - <div style="text-align:center">    
     <img src="https://img.shields.io/badge/Python-red?style=flat-square&logo=Python&logoColor=white"/>
     <img src="https://img.shields.io/badge/Docker-blue?style=flat-square&logo=Docker&logoColor=white"/>
     <img src="https://img.shields.io/badge/Mysql-green?style=flat-square&logo=Mysql&logoColor=white"/>
     <img src="https://img.shields.io/badge/Shell-red?style=flat-square&logo=Shell&logoColor=white"/>
     <img src="https://img.shields.io/badge/Django-red?style=flat-square&logo=DJANGO&logoColor=white"/>
     <img src="https://img.shields.io/badge/Nginx-blue?style=flat-square&logo=Nginx&logoColor=white"/>
     <img src="https://img.shields.io/badge/AWS-Black?style=flat-square&logo=AWS&logoColor=blue"/>
     </div>

     


     ### 📌 **BackEnd**

     - DRF(Django REST Framework)를 통한 REST API 구현 및 프론트엔드 통신
     - 배포 주소:https://www.beforetripsback.shop/users/register/
   

   ## 모델 구조, ERD 작성

   

   ![최프-erd2](https://user-images.githubusercontent.com/59475851/225585512-72b8f002-e049-434d-b560-fa05759363f5.jpg)


### ⚛️ 기능 설계

- 회원관리
  - 회원가입
  - 로그인
  - 로그아웃
- 커뮤 니티
  - 여행지 글 후기 작성 / 삭제 / 수정
  - 후기 글 좋아요 / 취소
  - 여행지 댓글 작성 / 삭제 / 수정
- 여행지 정보
  - 국가별 꿀팁 정보 작성 / 삭제 / 수정
  - 게시글 좋아요 / 취소
  - 꿀팁 정보 댓글 작성/ 삭제 / 수정
  - 좋아요 많은 순으로 꿀팁 정보 조회

### API 문서
| 앱 | 이름 | 클래스 이름 | 메소드 | 요청 URL | 상세 내용 | 참고사항 | API 요청 | API 값 |


### ✅ 내가 담당한 기능

> **💻 메인 Role - BackEnd: BackEnd 전체 코드 작성**

- 구현 주요 기능
  - CRUD: 여행지 글 후기 / 댓글 / 좋아요
  - 기존 Django sqlite3 데이터 베이스를 MYSQL로 전환
  - User 모델 와 게시글 모델 M:N 관계 설정 게시글 좋아요 구현
  - 게시글 모델 과 댓글 M : N 관계 설정 댓글 작성 및 조회 구현
  - 게시글 좋아요를 annotate ORM 기능으로 많은 순으로 정렬하여 꿀팁 정보 조회
  - 도커를 활용하여 Nginx, MYSQL, Django 컨테이너 생성 EC2 환경에 도커 설치후 배포 진행

## 개발 이슈

### 1. JWT 로그인 위한 쿠키 설정

### ⁉️ 에러 메세지

쿠키 설정 중 SAME_SITE 라는 속성이 존재 한다.

예전에는 기본 값이 None 이였다고 한다. 

하지만 쿠키 설정이 보안 적인 이유 로 기본 값이 LAX으로 변경 되어 프론트엔드에서 쿠키를 받아 들이지 못하는 이슈가 존재 했다.
![image](https://user-images.githubusercontent.com/59475851/225653671-47619d65-7c45-4dae-9d0b-495493b904a9.png)
![image](https://user-images.githubusercontent.com/59475851/225655594-da2cbf90-6c6c-4083-8f14-baf2de025752.png)
![image](https://user-images.githubusercontent.com/59475851/225653743-0e6ba570-7ae7-4534-b064-b570851ff875.png)


### ⭕️ 해결 방법

1. 쿠키 설정을 커스텀 진행

![image](https://user-images.githubusercontent.com/59475851/225657429-f095e07d-a798-4189-90f5-766a750e8c4b.png)

2. HTTPS 설정

![image](https://user-images.githubusercontent.com/59475851/225658181-42d362c2-aab7-4b4a-aab5-ad93daea58f3.png)


### 2. CORS

### ⁉️ 에러 메세지

![CORS](https://user-images.githubusercontent.com/59475851/225637095-3f46d089-5af7-4223-82eb-499a3f286b2d.PNG)


### ⭕️ 해결 방법

1. Nginx 설정 파일에서 

![CORS3](https://user-images.githubusercontent.com/59475851/225641504-f3d7f164-c910-4d76-8f58-59f4fef0a8ef.PNG)

아래와 같이 헤더에 값을 추가  하면 해결 되었다.



### 3. Mysql 설정이슈

### ⁉️ 에러 메세지

1. 유저 모델이 AbstractBaseUser 의존 -> migrate가 발생 하지 않은 현상 발생

![image](https://user-images.githubusercontent.com/59475851/225665781-efdde7c6-bac8-42cc-a780-6864faad3379.png)

![image](https://user-images.githubusercontent.com/59475851/225665645-90590e9d-361f-47b2-bc48-f0a9af280486.png)


### ⭕️ 해결 방법

![image](https://user-images.githubusercontent.com/59475851/225666059-298e40a9-77be-4092-aeb6-f32847673d9f.png)

![image](https://user-images.githubusercontent.com/59475851/225666243-1c0d2064-8966-4368-a6a9-83b405432daa.png)

위의 사진과 같이 주석 처리하게 되면 migrate로 mysql과 연동 가능하게 되었다. (MYSQL WORKbench)


### 4. 배포 이후 HTTPS을 위한 nginx 설정 이슈

### ⁉️ 에러 메세지

1. nginx 설정 파일인 default.conf 내용 중 HTTPS을 위한 설정 코드

   ssl_certificate /etc/letsencrypt/live/www.beforetripsback.shop/fullchain1.pem;

   ssl_certificate_key /etc/letsencrypt/live/www.beforetripsback.shop/privkey1.pem;

   파일이 존재 하지 않아 nginx 컨테이너가 실행 되지 않는 현상 발생



### ⭕️ 해결 방법

1. HTTPS 을 설정 하기 위해선 기본적으로 Nginx 컨테이너가 무조건 실행 되어야 했다.
2. ssl 설정 부분을 주석 처리하고,  nginx을 실행 시켰다.
3. 이후 Docker hub에는 certbot 공식 image가 존재했고 이를 이용하여 인증서을 발급
4. 발급 받은 인증서를 nginx 컨테이너가 불러오는 디렉터리에 인증서를 복사
5. 하지만 인증서 심볼릭 링크가 존재 하므로 원본 복사는 불가했고, 복사본을 컨테이너에 복사
6. 주석 했던 nginx 설정 부분을 풀고 프록시 서버 부분을 http://example.com 으로 수정
7. nginx 컨테이너 재 실행



### 5.배포 이후 Static 파일 찾아 오지 못하는 현상

### ⁉️ 에러 메세지

1. Static 파일을 읽어 오지 못해 css, js 등 홈페이지 가 깨지는 현상 발생

![static4](https://user-images.githubusercontent.com/59475851/225648023-02112e8b-60cb-474e-aa39-68fa79b2006c.PNG)


### ⭕️ 해결 방법
nginx 설정 파일 코드 추가

![static1](https://user-images.githubusercontent.com/59475851/225648076-a5cdfdbf-6400-49ee-adfc-b452680ba779.PNG)


django settings.py 아래 사진과 같이 코드 추가
![static2](https://user-images.githubusercontent.com/59475851/225648123-678530e4-5214-4580-90ec-1bfa8f5e979a.PNG)
![static3](https://user-images.githubusercontent.com/59475851/225648136-3cbbf8c1-965b-4bf1-81b8-bb701608e6e4.PNG)

도커 컨테이너 설정 추가

![static5](https://user-images.githubusercontent.com/59475851/225649170-35ac4bfe-566b-42c5-9b85-71900d525055.PNG)

## 프로젝트 후기

처음 백엔드 부분을 맡았을땐 막막 하였다. django rest framework 부분도 잘 모르고 

이제껏 쓰지 않았던 기술을 써야 하는 상황 이였기 때문이였다.

익숙하지 않아 힘든 점이 많았지만 야생학습을 통해 새로운 기술을 학습해나가는 역량 또한 길러 나갈 수 있었다.

새로운 기술, 프레임워크 등을 학습하는 부분에 대해 자신감을 얻을수 있었고 백엔드 개발자를 지망하는

지망생으로서 백엔드에서 필수적으로 배워야 할 부분을 배운것 같아 적은 기간이였지만 뿌듯한 프로젝트 였다.
