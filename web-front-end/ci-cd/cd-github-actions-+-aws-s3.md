---
description: https://ggsno.tistory.com/13 요약
---

# CD :: github actions + AWS S3

#### Github Actions

Github Actions은 Github에서 제공하는 클라우드형 CI/CD 툴이다. 아래는 Github Actions 구성 요소이다.

* Workflow : 하나 이상의 작업을 실행하는 자동화 프로세스. 레포지토리 내의 yaml 파일에 의해 정의된다. 후술할 Event에 의해 트리거되거나 정의된 일정으로 실행될 수 있고 수동으로도 실행 가능하다.
* Event : Workflow 실행을 트리거하는 레포지토리의 특정 활동
* Runner : Workflow를 실행할 서버. GitHub Actions의 Runner는 기본적으로 Node 16 version을 탑재한다.
* Jobs : 하나의 Runner에서 실행되는 Workflow의 일련의 step 모음. step은 하나의 shell script 혹은 후술할 Action을 의미한다.
* Actions : 자주 반복 되는 작업을 수행하는 GitHub Actions 플랫폼용 사용자 지정 응용 프로그램. 설정파일에서 use 키워드와 함께 사용할 수 있다.

***

### AWS S3를 이용한 정적 사이트 배포

* AWS S3 : S3는 Simple Storage Service의 약자로, 파일을 클라우드 스토리지에 저장하고 인터넷상으로 접근할 수 있게 해주는 서비스다. build한 정적인 파일들을 S3를 통해 배포 가능하다.

#### 배포용 S3 Bucket 생성 및 호스팅 설정

[AWS 사이트의 S3 서비스](https://aws.amazon.com/ko/s3/?nc2=type\_a)에 접속해 새로운 bucket을 생성한다

<figure><img src="https://blog.kakaocdn.net/dn/SlUSK/btrLh851co2/Oagzv91nku4Uf6TgbZKf7k/img.png" alt=""><figcaption><p>bucket 생성 창</p></figcaption></figure>

* Bucket name : 아이디처럼 다른 사람들과 중복되지 않게 만들어야 함
* AWS Region : 클라우드 서비스를 제공하는 물리적 서버의 위치. 가까운 곳으로 설정.

<figure><img src="https://blog.kakaocdn.net/dn/b0z2dG/btrLiCeDcv2/URuRMr3Ycc7OzMqGlBZ4a1/img.png" alt=""><figcaption><p>public access block을 체크 해제시 하단에 경고창이 뜬다. 알았다고 체크해주자.</p></figcaption></figure>

* 배포용이기 때문에 public access block을 체크 해제

<figure><img src="https://blog.kakaocdn.net/dn/d3WKXY/btrLukGk3LU/PBeBjQ71wNEl8BxZINKl8k/img.png" alt=""><figcaption><p>만들어둔 bucket의 Permissions탭으로 이동</p></figcaption></figure>

<figure><img src="https://blog.kakaocdn.net/dn/bgNN8Y/btrLu2d5IOE/P12OhkIQZMFGU4DhdYA61K/img.png" alt=""><figcaption><p>bucket policy를 위와 같이 수정</p></figcaption></figure>

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::<bucket-name>/*"
        }
    ]
}
```

Resource속성의 \<bucket-name>을 현재 생성한 bucket의 이름으로 바꿔야 한다.

<figure><img src="https://blog.kakaocdn.net/dn/u9JFF/btrLzDxEdUF/veDogkk5cnvqxhZFUpUZT0/img.png" alt=""><figcaption><p>Properties 탭에서 최하단에 있는 Static website hosting 옵션 진입</p></figcaption></figure>

<figure><img src="https://blog.kakaocdn.net/dn/by9S3C/btrLzEDlkYl/L5HO1qK9KLVlhKmaTAKwn0/img.png" alt=""><figcaption><p>정적 웹사이트 호스팅 Enable체크 후 가장 먼저 보여줄 index 파일의 이름 기입</p></figcaption></figure>

<figure><img src="https://blog.kakaocdn.net/dn/ZrMKq/btrLzlDYIBU/KzFoYYtLLylarOebmLvItk/img.png" alt=""><figcaption><p>Properties 탭의 최하단에 있는 Static website hosting에 추가된 배포 사이트 URL</p></figcaption></figure>

<figure><img src="https://blog.kakaocdn.net/dn/cTNcew/btrLux0b99I/t8T9y7oucBqVT7BN3ExUZ1/img.png" alt=""><figcaption><p>build한 파일들을 Object탭에 업로드</p></figcaption></figure>

\


여기까지가 S3를 이용한 정적사이트 배포이다.

\


여기에 깃허브 액션에서 사용할 access key를 미리 받아두자.

<figure><img src="https://blog.kakaocdn.net/dn/JaXLg/btrLBeEutx6/9TuYqqKXBFvKKvK9x9oKj0/img.png" alt=""><figcaption><p>사이트 우측 상단에 있는 아이디를 클릭하면 Security credentials가 있다</p></figcaption></figure>

<figure><img src="https://blog.kakaocdn.net/dn/KAIEo/btrLvCttSXI/v79RiDYWyH6CkIIoSPOLMk/img.png" alt=""><figcaption><p>Create New Access Key를 클릭해 Access key를 생성하자</p></figcaption></figure>

액세스 키를 만들 때 access id와 secret key를 주는데, 최초 한 번만 보여주고 그 이후로는 절대 볼 수 없으니 따로 파일로 저장하는것을 추천한다.

***

### Github action을 이용한 배포 자동화

깃허브 레포지토리를 생성하고 build할 파일들을 넣은 후 Actions에 들어가보자

<figure><img src="https://blog.kakaocdn.net/dn/Gcaiu/btrLyZVQplw/llSbib5gnY4nJICdEs7TFk/img.png" alt=""><figcaption><p>workflow를 만들어주는 많은 템플릿들이 있다. 우리는 실습을 위해 직접 작성해보자.</p></figcaption></figure>

<figure><img src="https://blog.kakaocdn.net/dn/bqwRWn/btrLu2so2Zg/csyKnnOTsNJfQubRk34cA0/img.png" alt=""><figcaption></figcaption></figure>

line 1 | name : workflow의 이름

line 3 | on : job이 트리거 되는 조건들 ( main 브랜치에 push가 되면 job을 실행해라)

line 8 \~ 23 | jobs의 steps들이 차례대로 실행된다. env에서 사용하는 변수들은 아래에 나올 스크린샷을 참고하자

line 24 | SOURCE\_DIR에는 build될 파일들이 들어가는 디렉토리 이름을 기입한다. vite로 프로젝트를 만들었다면 dist이고 CRA로 만들었다면 build일 것이다.

```
name: deploy

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@main
      - run: npm ci
      - run: npm run build
      - name: deploy to s3 bucket
        uses: jakejarvis/s3-sync-action@master
        with:
          args: --delete
        env:
          AWS_S3_BUCKET: ${{ secrets.AWS_S3_BUCKET }}
          AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
          AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          AWS_REGION: "ap-northeast-2"
          SOURCE_DIR: "dist"
```

\


<figure><img src="https://blog.kakaocdn.net/dn/SGlMg/btrLuw8n17G/DPX9KIkeHaNHmXlASkLJy0/img.png" alt=""><figcaption></figcaption></figure>

AWS에서 발급한 액세스 키 id와 비밀키, bucket의 이름을 선언해주자.

\


이후 해당 레포지토리가 연결된 환경에서 push를 하면 위의 workflow가 실행된다.

<figure><img src="https://blog.kakaocdn.net/dn/zVVod/btrLzkrUdIx/kV1HiWLeJbXxQRQAcDpku1/img.png" alt=""><figcaption><p>push 후 CD가 자동으로 된 모습</p></figcaption></figure>

***

### 오류 상황

<figure><img src="https://blog.kakaocdn.net/dn/Ii043/btrLBxqsqA7/bakcK1JgK0XuKDczUsjgK0/img.png" alt=""><figcaption></figcaption></figure>

yarn으로 dependancy를 다운받으면 yarn.lock만 있는데 package-lock.json이 있어야 정상 작동 한다. 따라서 npm install로 dependancy를 다운받자.

\
