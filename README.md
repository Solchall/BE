

## API Document
### 1. 상품 검색
<img width="1623" alt="image" src="https://github.com/Solchall/what2buy-AI/assets/71062967/131886c5-8e2f-43bc-8a8d-a8512207305b">

- Input
  - `apikey`: OpenAI API Key
  - `userNeed`: 사용자가 찾고자 하는 상품 스타일
    - 예시1) 40,000원 이하 스프라이트 블랙 니트를 찾아줘
    - 예시2) 4만원대 브라운 맨투맨 추천해줘. 4개월 동안 판매가 많은순으로 정렬해줘
    - 예시3) 10만원 이하로 베이지 린넨소재 셔츠 찾아줘. 3달내 리뷰순으로 정렬해줘
    - 예시4) y2k 옷 찾아줘
    - 예시5) 뉴진스가 입을 것 같은 옷 알려줘
    - 예시6) 바캉스 갈 때 입을 옷 추천해봐
- Output
  - 상품 리스트
<br>

### 2. 상품 설명
<img width="1618" alt="image" src="https://github.com/Solchall/what2buy-AI/assets/71062967/9e4fb8ba-8efe-418e-a39f-bf236d378f80">

- Input
  - `apikey`: OpenAI API Key
  - `id`: 사용자가 선택한 상품의 ID
- Output
  - 상품 개괄설명
  - 사이즈별 키 / 몸무게
  - 유용한 리뷰 / 평점 낮은 리뷰 요약

<br>

### 3. 질의응답
<img width="539" alt="image" src="https://github.com/Solchall/what2buy-AI/assets/71062967/d7c2f205-3a19-4d37-90ed-751b46446525">

- Input
  - `apikey`: OpenAI API Key
  - `user_question`: 상품에 대한 사용자의 질문
  - `id`: 사용자가 선택한 상품의 ID
- Output
  - 사용자 질문에 대한 응답

<br>


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

<br>

## 👒 Prompt Engineering and LLMs with Langchain

### 1. Beautifulsoup and Selenium

**사용자 입력에 따른 기본 상품 리스트**
* get_ft_list.py
<br>filtering prompt로부터 사용자 입력에 따라 검색된 페이지 url에서 상품 리스트 추출

**사용자 입력에 따른 매거진 상품 리스트**
* get_mg_list.py
<br>magazines prompt로부터 사용자 입력에 따라 검색된 매거진 페이지 url에서 상품 리스트 추출

**상품 아이디**
* get_ids.py
<br>빠른 상품 정보 제공 및 효율성을 위해 상품번호 추출

**상품 개괄 정보**
* get_simple_detail.py
<br>별점, 후기수, 도착 예정일 등 상품에 대한 개괄 정보 추출

**상품 리뷰**
* get_reviews.py
<br>유용한 순, 낮은 평점 순 리뷰를 num개씩 가져와 각 리뷰의 프로필, 사이즈, 별점, 리뷰내용 추출

**사이즈 추천**
* get_size_reco.py
<br>해당 상품의 사이즈 추천 정보 추출

### 2. Prompt

**사용자 입력에 따른 기본 상품 리스트**
* filtering.py
<br>사용자 입력에 부합하는 검색 결과 url 추출 (카테고리 기반)

**사용자 입력에 따른 매거진 상품 리스트**
* magazines.py
<br>좀 더 자유로운 사용자 입력에 부합하는 매거진 검색 결과 url 추출 (에디터 추천 기반)

**리뷰 요약**
* review_summ.py
<br>리뷰 데이터를 가져와 사용자에게 요약되어 보여지도록 prompt engineering

**상품 개괄 정보**
* simple_detail_gpt.py
<br>상품 개괄 정보를 가져와 사용자에게 요약되어 보여지도록 prompt engineering

**사이즈 추천**
* size_reco.py
<br>상품 사이즈 추천 정보를 가져와 사용자에게 요약되어 보여지도록 prompt engineering

**질의응답**
* ask.py
<br>해당 상품의 리뷰 데이터를 기반으로 사용자와 자유롭게 질의응답하는 prompt
