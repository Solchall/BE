



## Cloud Run 배포
Google Cloud Run에 Dockerized FastAPI를 배포하기 위해 Dockerfile을 생성해야 한다.

### [Dockerfile](https://github.com/Solchall/what2buy-AI/blob/main/Dockerfile)에 포함된 내용
- Python 버전을 3.11.3으로 설정
- Selenium에 사용되는 [Chrome](https://googlechromelabs.github.io/chrome-for-testing/)과 [ChromeDriver](https://chromedriver.chromium.org/downloads)를 설치하는 명령어 추가
- 필요한 환경 변수 설정
- [requirements.txt](https://github.com/Solchall/what2buy-AI/blob/main/requirements.txt)를 사용해 필요한 패키지 설치

<br>

### 배포 방법
1. Google Cloud에 프로젝트를 생성
2. [gcloud CLI](https://cloud.google.com/sdk/docs/install?hl=ko) 설치
3. 터미널에 `$ gcloud init`를 입력해 gCloud CLI 초기화
4. 소스코드가 있는 폴더에서 터미널을 열고 `$ gloud run deploy`를 입력하여 배포
5. Google Cloud 콘솔에서 `새 버전 수정 및 배포`를 클릭한 후 `컨테이너 > 변수 및 보안 비밀`에 환경변수를 입력

> `새 버전 수정 및 배포`에서 컨테이너의 할당량을 변경할 수 있다. <br>
>  메모리, CPU, 요청 시간 제한, 실행 환경, 인스턴스 최소/최대 개수 등을 조정하여 성능을 향상시킬 수 있다.
