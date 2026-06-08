# Python Data Analysis Projects

잇업 교육기관의 「실전에서 써먹는 파이썬 데이터분석」 강의를 수강하며 수행한 9개의 데이터 분석 프로젝트를 정리한 저장소입니다.

CSV, Excel 파일 기반의 정형 데이터 분석부터 웹 크롤링을 통한 비정형 데이터 수집까지 다양한 데이터 처리 과정을 실습했습니다. 공개 데이터와 웹 데이터를 직접 수집·가공하며 데이터 분석의 전체 흐름을 익혔습니다.

Python을 중심으로 Pandas, BeautifulSoup, Selenium 등 실무에서 자주 활용되는 라이브러리를 사용하여 데이터로부터 의미 있는 인사이트를 도출하는 경험을 쌓았습니다.

---

## 기술 스택

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=Python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat-square&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=flat-square&logo=numpy&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-11557c?style=flat-square&logo=python&logoColor=white)
![Seaborn](https://img.shields.io/badge/Seaborn-4C72B0?style=flat-square&logo=python&logoColor=white)
![Requests](https://img.shields.io/badge/Requests-2CA5E0?style=flat-square&logo=python&logoColor=white)
![BeautifulSoup](https://img.shields.io/badge/BeautifulSoup-59666C?style=flat-square&logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=flat-square&logo=Jupyter&logoColor=white)

---

## 프로젝트 목록

| No | 프로젝트 | 주요 내용 |
|:---:|---|---|
| 1 | 가장 많이 사용된 이름 TOP 10 분석 | 미국 아기 이름 CSV 데이터를 Pandas로 분석하여 이름별 사용 횟수를 합산하고 상위 10개 이름 추출 |
| 2 | 네이버 검색어 입력 및 연관검색어 추출 | Selenium으로 네이버 검색창에 키워드를 입력하고 BeautifulSoup으로 연관검색어 목록 수집 |
| 3 | 베스트셀러 도서 상세정보 추출 | Selenium + BeautifulSoup으로 YES24 베스트셀러 목록에서 도서명, 저자, 출판사, 출판일 정보 수집 |
| 4 | 서울 중구 커피점·카페 상가수 파악 | SQLAlchemy로 MariaDB에 연결하여 SQL 쿼리로 서울 중구 내 커피점·카페 상가 수 조회 |
| 5 | 유튜브 댓글 수집 및 분석 | Selenium + BeautifulSoup으로 유튜브 영상 댓글을 수집하고 Pandas DataFrame으로 저장 |
| 6 | 유튜브 채널 데이터 수집 및 저장 | Selenium + BeautifulSoup으로 유튜브 랭킹 사이트에서 채널 랭킹, 카테고리, 구독자 수, 조회수, 영상 수 수집 |
| 7 | 지하철 데이터 KMeans 클러스터링 | 서울시 지하철 시간대별 승하차 인원 데이터를 활용해 KMeans 클러스터링으로 이용 패턴이 유사한 역 그룹화 |
| 8 | 최근 가입 고객 이름 분석 | SQLAlchemy로 MariaDB에 연결하여 SQL 쿼리로 가장 최근에 가입한 고객 정보 조회 |
| 9 | 평균연봉 상위 10개 사업장 확인 | 국민연금공단 공개 데이터(CSV)를 Pandas로 분석하여 고지금액 기반 평균연봉을 계산하고 상위 10개 사업장 추출 |

---

## 배운 점

| 항목 | 내용 |
|---|---|
| 데이터 전처리 | Pandas를 활용한 데이터 정제, 집계, 정렬 등 전처리 과정 이해 |
| 데이터 시각화 | Matplotlib, Seaborn을 활용한 데이터 시각적 표현 |
| 웹 데이터 수집 | Selenium + BeautifulSoup을 활용한 동적 웹페이지 크롤링 |
| 데이터 분석 과정 | 데이터 수집 → 전처리 → 분석 → 결과 도출의 전체 흐름 습득 |
| 인사이트 도출 | 공개 데이터와 수집 데이터에서 의미 있는 정보를 추출하는 경험 |

---

## 폴더 구조

```
python_data_analysis_projects/
├── data/
│   ├── (실습)서울시 지하철 호선별 역별 시간대별 승하차 인원 정보_2404.xlsx
│   ├── babyNamesUS.csv
│   └── 국민연금공단_국민연금 가입 사업장 내역.csv
├── 가장 많이 사용된 이름 TOP 10분석.ipynb
├── 네이버 검색어 입력및 연관검색어 추출.ipynb
├── 베스트셀러 도서 상세정보 추출.ipynb
├── 서울 중구 커피점, 카페 상가수 파악.ipynb
├── 유튜브 댓글 수집 및 분석.ipynb
├── 유튜브 채널 데이터 수집 및 저장.ipynb
├── 지하철 데이터 Kmeans 클러스터.ipynb
├── 최근 가입 고객 이름 분석하기.ipynb
├── 평균연봉 상위 10개 사업장 확인.ipynb
└── README.md
```
