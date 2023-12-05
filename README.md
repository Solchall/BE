

## API Document
### 1. 상품 검색
<img width="1623" alt="image" src="https://github.com/Solchall/what2buy-AI/assets/71062967/131886c5-8e2f-43bc-8a8d-a8512207305b">
(설명 추가)


### 2. 상품 설명
<img width="1618" alt="image" src="https://github.com/Solchall/what2buy-AI/assets/71062967/9e4fb8ba-8efe-418e-a39f-bf236d378f80">
(설명 추가)


### 3. 질의응답
<img width="539" alt="image" src="https://github.com/Solchall/what2buy-AI/assets/71062967/d7c2f205-3a19-4d37-90ed-751b46446525">
(설명 추가)


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







## 👒 Prompt Engineering and LLMs with Langchain

### 1. Beautifulsoup and Selenium

**1-1. 사용자 입력에 따른 기본 상품 리스트**
* [x] get_ft_list.py  - filtering prompt로부터 사용자 입력에 따라 검색된 페이지 url에서 상품 리스트 추출

**1-2. 사용자 입력에 따른 매거진 상품 리스트**
* [x] get_mg_list.py  - magazines prompt로부터 사용자 입력에 따라 검색된 매거진 페이지 url에서 상품 리스트 추출

**1-3. 상품 아이디**
* [x] get_ids.py  - 빠른 상품 정보 제공 및 효율성을 위해 상품번호 추출

**1-4. 상품 개괄 정보**
* [x] get_simple_detail.py  - 별점, 후기수, 도착 예정일 등 상품에 대한 개괄 정보 추출

**1-5. 상품 리뷰**
* [x] get_reviews.py  - 유용한 순, 낮은 평점 순 리뷰를 num개씩 가져와 각 리뷰의 프로필, 사이즈, 별점, 리뷰내용 추출

**1-5. 사이 추천**
* [x] get_size_reco.py  - 해당 상품의 사이즈 추천 정보 추출

### 2. Prompt

