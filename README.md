
# Python 데이터 분석 포트폴리오

데이터 분석, 웹 크롤링, DB 연동, KMeans 클러스터링을 포함한 9개의 Python 데이터 분석 프로젝트 모음

---

## 📋 프로젝트 개요

\| 항목 | 내용 |
| --- | --- |
| 개발 기간 | 2026.04 |
| 프로젝트 유형 | 개인 데이터 분석 포트폴리오 |
| 데이터 출처 |  웹 크롤링, 잇업 데이터(CSV/Excel), MariaDB |
| 분석 도구 | Python, Jupyter Notebook |
| 분석 기법 | 집계·정렬, KMeans 클러스터링, SQL 조회, 웹 자동화 |

---

## 🎯 프로젝트 목적

정형 데이터(CSV, Excel) 분석부터 Selenium 기반 웹 자동화, SQL을 통한 DB 조회, KMeans 클러스터링까지 데이터 분석의<br>전 과정을 구현하는 것을 목표로 했다. 

---

## 📂 데이터 소개

### 데이터 출처

| # | 프로젝트 | 데이터 출처 | 형식 |
|:---:|---|---|:---:|
| 1 | 가장 많이 사용된 이름 TOP 10 분석 | Itup 데이터 | CSV |
| 2 | 평균연봉 상위 10개 사업장 확인 | Itup 데이터 | CSV |
| 3 | 지하철 데이터 KMeans 클러스터링 | Itup 데이터 | Excel |
| 4 | 서울 중구 커피점·카페 상가수 파악 | MariaDB (sgg_upjong_cnt 테이블) | DB |
| 5 | 최근 가입 고객 이름 분석 | MariaDB (customers 테이블) | DB |
| 6 | 베스트셀러 도서 상세정보 추출 | YES24 베스트셀러 크롤링 | HTML |
| 7 | 유튜브 채널 데이터 수집 및 저장 | youtube-rank.com 크롤링 | HTML |
| 8 | 유튜브 댓글 수집 및 분석 | YouTube 영상 크롤링 | HTML |
| 9 | 네이버 검색어 입력 및 연관검색어 추출 | 네이버 검색 자동화 | HTML |


---

## 🔄 분석 과정

### 1. 데이터 수집

- **정형 데이터**: `pd.read_csv()`, `pd.read_excel()`로 로컬 파일 로드
- **웹 크롤링**: Selenium으로 동적 페이지 렌더링 후 BeautifulSoup으로 CSS 셀렉터 기반 HTML 파싱
- **DB 연동**: SQLAlchemy로 MariaDB 연결 후 `pd.read_sql_query()`로 결과를 DataFrame으로 수신

### 2. 데이터 전처리

- **인코딩 처리**: CSV의 `cp949` 인코딩 명시적 지정
- **파생 컬럼 생성**: 국민연금 데이터에서 인당 고지금액 계산 → 역산으로 월 급여 추정 → 연봉 환산
- **텍스트 정제**: 크롤링한 저자명의 구분자(`/`)를 ` / `로 통일

### 3. 데이터 분석

- **집계**: `pivot_table()`로 이름별 출생 수 합산, `sort_values()` + `head()`로 상위 N개 추출
- **SQL 분석**: 집계 함수, 산술 연산(`opn_1 + opn_2 + ... + opn_5up`), 서브쿼리로 DB 조회
- **KMeans 클러스터링**: 승하차 상위 20개 역을 12개 시간대 특성으로 3개 그룹 분류

---

## 📊 주요 분석 결과

| # | 프로젝트 | 결과 |
|:---:|---|---|
| 1 | 이름 TOP 10 | Michael, James, Robert, John, David 순 |
| 2 | 평균연봉 상위 사업장 | 국민연금 요율 역산 기준 상위 10개 사업장 추출 |
| 3 | 지하철 클러스터링 | 20개 역을 이용 패턴 기준 3개 그룹(9개·6개·5개 역)으로 분류 |
| 4 | 서울 중구 카페 상가수 | 총 888개 |
| 5 | 최근 가입 고객 이름 분석 | 가장 최근 가입일(2023-07-12) 고객 1명(박영수) 조회 |
| 6 | YES24 베스트셀러 | 실시간 베스트셀러 도서의 도서명·저자·출판사·출판일 수집 |
| 7 | 유튜브 채널 데이터 수집 | 상위 채널 순위·카테고리·구독자·조회수·영상수 수집 |
| 8 | 유튜브 댓글 수집 | 영상 댓글 수집 및 DataFrame 저장 |
| 9 | 네이버 연관검색어 추출 | '파이썬' 검색 시 연관검색어 자동 추출 |

---

## 💡 인사이트

- **미국 이름 트렌드**: Michael, James, Robert 등 전통적인 영미권 이름이 누적 출생 수 기준 상위권을 독점하며, 시대와 무관하게 지속적으로 사용된 이름임을 확인
- **공개 데이터로 연봉 추정**: 국민연금 보험료율(9%)을 활용하면 연봉을 직접 제공하지 않는 데이터에서도 사업장별 급여 수준을 근사할 수 있음
- **지하철 이용 패턴 다양성**: 승하차 상위 역들도 시간대별 패턴에 따라 명확히 구분되는 그룹이 존재하며, 단순 이용량 순위와는 다른 이용 특성이 있음을 클러스터링으로 확인
- **서울 중구 카페 포화도**: 서울 중구에만 888개의 커피점·카페가 운영 중, 상업 밀집 지역의 높은 카페 포화도를 수치로 확인
- **베스트셀러 트렌드**: 자기계발·투자·수험서가 상위권에 고르게 분포하며, 정기적으로 크롤링 시 시기별 도서 트렌드 변화를 추적할 수 있는 구조
- **글로벌·국내 채널 규모 격차**: 글로벌 1위 MrBeast(4억6600만 구독)와 국내 1위 김프로KIMPRO(1억3000만 구독)의 구독자 수가 약 3.6배 차이로, 플랫폼 내 국내·글로벌 채널 간 규모 차이를 수치로 확인
- **신규 고객 유입 정체**: 가장 최근 가입 고객의 가입일이 2023-07-12로, 이후 신규 가입 이력이 없어 고객 유입이 정체된 상태임을 확인. 지속적인 성장을 위해 신규 고객 유치 전략이 필요함을 시사
- **유튜브 댓글로 드러나는 감정 반응 패턴**: '인사이드 아웃' 영상 댓글을 수집한 결과, 시청자의 감정적 반응이 다양하게 분포함을 확인. 댓글 분석을 통해 콘텐츠가 시청자에게 미치는 감정적 영향력을 파악할 수 있음
- **네이버 연관검색어로 파악하는 검색 의도**: '파이썬' 검색 시 연관검색어 대부분이 독학·기초·자격증·학원 등 학습 목적 키워드로, 실무 개발자보다 입문자 수요가 검색 트렌드를 주도함을 확인. 

---

## 🔑 핵심 구현 내용

### 1. 국민연금 데이터 기반 평균연봉 역산

```python
raw['평균연봉(만원)'] = (raw['당월고지금액'] / raw['가입자수']) / 0.09 / 10000 * 12
```

국민연금 보험료율(9%) 역산으로 별도 연봉 데이터 없이 사업장별 평균 연봉 추정

### 2. 유튜브 댓글 수집 재사용 함수

```
def yt_review(url, content_name, end_key_input):
```

URL, 컨텐츠명, 스크롤 횟수를 파라미터로 받아 다양한 영상에 재사용 가능하도록 함수화

### 3. 지하철 시간대별 KMeans 클러스터링

```python
kmeans = KMeans(n_clusters=3, random_state=30)
kmeans.fit(df_cluster[columns_for_cluster])
```

12개 시간대 특성으로 승하차 상위 20개 역을 3개 그룹으로 분류

### 4. SQL 산술 연산으로 상가 수 합산

```sql
SELECT opn_1 + opn_2 + opn_3 + opn_5 + opn_5up AS total FROM sgg_upjong_cnt
WHERE sido_nm = '서울특별시' AND sgg_nm = '중구' AND upjong_mnm = '커피점/카페'
```

규모별 상가 수 컬럼을 SQL 산술 연산으로 합산하여 총 상가 수 도출

### 5. SQL 서브쿼리로 최근 가입 고객 조회

```sql
SELECT * FROM customers WHERE join_date = (SELECT MAX(join_date) FROM customers)
```

서브쿼리로 최대 가입일을 구한 뒤 해당 고객만 필터링

### 6. 이름별 출생 수 집계

```python
df = raw.pivot_table(index='Name', values='Number', aggfunc='sum')
top10 = df.sort_values(by='Number', ascending=False).head(10)
```

pivot_table로 이름별 누적 출생 수 합산 후 상위 10개 추출

### 7. 베스트셀러 도서 정보 파싱

```python
authors = book_part.select('span.authPub.info_auth')[0].text.strip().replace('/', ' / ')
```

CSS 셀렉터로 도서 요소 추출, 저자명 구분자(`/`)를 ` / `로 정제

### 8. 유튜브 채널 데이터 수집

```python
result.append([ranking, category, youtube_name, subscriber_count, view_count, video_count])
```

채널별 6개 항목을 리스트로 누적 수집 후 DataFrame 변환

### 9. 네이버 연관검색어 자동 추출

```python
input_word_place.send_keys(searching)
```

`send_keys()`로 검색어 자동 입력 후 자동완성 리스트에서 연관검색어 추출

---

## 🛠️ 기술 스택 및 선택 이유

| 기술 | 선택 이유 |
|---|---|
| Python | 데이터 분석 생태계와 라이브러리 지원 |
| Pandas | DataFrame 기반 정형 데이터 집계·정렬·파생 컬럼 처리 |
| Selenium | JavaScript 렌더링이 필요한 동적 웹페이지 자동화 및 스크롤 제어 |
| BeautifulSoup | CSS 셀렉터 기반 HTML 파싱으로 필요한 요소 정밀 추출 |
| SQLAlchemy | Python 환경에서 MariaDB 연결 및 SQL 결과를 DataFrame으로 수신 |
| scikit-learn |  KMeans 클러스터링 구현을 위한 Python 표준 머신러닝 라이브러리 |
| Jupyter Notebook | 단계별 분석 과정과 결과를 함께 기록 |

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=Python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat-square&logo=pandas&logoColor=white)
![Selenium](https://img.shields.io/badge/Selenium-43B02A?style=flat-square&logo=Selenium&logoColor=white)
![BeautifulSoup](https://img.shields.io/badge/BeautifulSoup-59666C?style=flat-square&logo=python&logoColor=white)
![SQLAlchemy](https://img.shields.io/badge/SQLAlchemy-D71F00?style=flat-square&logo=python&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=flat-square&logo=scikit-learn&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=flat-square&logo=Jupyter&logoColor=white)

---

## 🔧 트러블슈팅 / 개선 경험

### Selenium 크롤링 시 동적 로딩 대기 문제

**문제 상황**

유튜브 댓글 수집 시 스크롤 후 즉시 요소를 파싱하면 댓글이 누락되거나 빈 리스트가 반환됨

**원인 분석**

JavaScript로 동적 렌더링되는 페이지는 스크롤 이벤트 이후에도 DOM 업데이트가 완료되기까지 시간이 필요하며, 렌더링이 끝나기 전에 파싱하면 아직 로드되지 않은 요소는 수집되지 않음

**해결 방법**

```python
driver.execute_script("window.scrollTo(0, document.body.scrollHeight);")
time.sleep(2)  # 스크롤 후 렌더링 대기
```

**배운 점**

`time.sleep()`은 단순하지만 동적 페이지에서 렌더링 완료를 보장하는 현실적인 방법임. 대기 시간이 너무 짧으면 요소 누락, 너무 길면 수집 속도 저하로 이어지므로 페이지 응답 특성에 맞게 조정이 필요함


### ChromeDriver 버전 불일치 오류

**문제 상황**

Selenium 실행 시 아래 오류 발생:
```
SessionNotCreatedException: Message: session not created:
This version of ChromeDriver only supports Chrome version XX
```

**원인 분석**

로컬에 설치된 Chrome 브라우저 버전과 수동으로 설치한 ChromeDriver 버전이 일치하지 않아 세션 생성 실패. Chrome은 자동 업데이트되므로 ChromeDriver를 별도로 관리하면 버전 불일치가 반복적으로 발생함

**해결 방법**

```python
import chromedriver_autoinstaller
chromedriver_autoinstaller.install()
```

실행 시점의 Chrome 버전을 자동 감지해 맞는 ChromeDriver를 설치하므로 버전 관리 불필요

**배운 점**

Chrome 자동 업데이트 환경에서는 ChromeDriver를 수동으로 관리하는 것이 비효율적이며, `chromedriver-autoinstaller`로 버전 동기화를 자동화하는 것이 현실적인 해결책임


### KMeans 실행마다 클러스터 결과가 달라지는 문제

**문제 상황**

KMeans 실행 시 같은 코드인데도 실행할 때마다 클러스터 구성이 달라져, 분석 결과를 재현하거나 다른 사람과 공유하기 어려움

**원인 분석**

KMeans는 초기 중심점(centroid)을 랜덤하게 선택하기 때문에 실행마다 출발점이 달라지고, 그 결과 클러스터 구성도 매번 달라질 수 있음

**해결 방법**

```python
kmeans = KMeans(n_clusters=3, random_state=30)
```

`random_state`에 고정값을 지정하면 랜덤 시드가 고정되어 누가, 언제 실행해도 동일한 결과가 보장됨

**배운 점**

분석 결과의 재현성은 코드 공유나 협업 시 필수 조건임. 머신러닝에서 랜덤 요소가 개입되는 알고리즘은 `random_state`를 명시적으로 고정하는 습관이 중요함


### 한글 CSV 파일 인코딩 오류

**문제 상황**

국민연금공단 CSV 파일을 기본 옵션으로 읽을 때 인코딩 오류 발생

**원인 분석**

한국 정부 공공데이터는 UTF-8이 아닌 `cp949(EUC-KR)` 인코딩으로 배포되는 경우가 많음

**해결 방법**

```python
raw = pd.read_csv('./data/국민연금공단_국민연금 가입 사업장 내역.csv', encoding='cp949')
```

**배운 점**

오류 메시지만으로는 인코딩 문제임을 바로 파악하기 어려웠고, `encoding` 파라미터를 명시하지 않으면 pandas가 UTF-8로 읽으려다 실패한다는 것을 확인했다. 이후 한국 공공데이터를 다룰 때는 `cp949`를 우선 시도하는 것이 기본 패턴이 됨

---

## 📈 향후 개선 계획

- [ ] 지하철 클러스터링 결과를 seaborn 히트맵으로 시각화하여 그룹별 시간대 패턴 비교
- [ ] 유튜브 댓글 수집 후 KoNLPy를 통한 키워드 빈도 분석 추가
- [ ] 국민연금 연봉 데이터를 업종별·지역별로 세분화하여 분포 비교 분석
- [ ] Selenium 크롤링에 예외 처리 및 재시도 로직 추가
- [ ] 수집한 데이터를 CSV 또는 DB로 저장하는 파이프라인 구성

---

## 🚀 실행 방법

```bash
# 의존성 설치
pip install pandas selenium beautifulsoup4 sqlalchemy pymysql scikit-learn chromedriver-autoinstaller openpyxl

# Jupyter Notebook 실행
jupyter notebook
```

> DB 연동 프로젝트(서울 중구 커피점 파악, 최근 가입 고객 분석)는 MariaDB 연결 정보를 별도로 설정해야 합니다.

---

## 📁 폴더 구조

```
python_data_analysis_projects/
├── data/
│   ├── babyNamesUS.csv                                               # 미국 아기 이름 통계
│   ├── 국민연금공단_국민연금 가입 사업장 내역.csv                        # 국민연금 사업장 데이터
│   └── (실습)서울시 지하철 호선별 역별 시간대별 승하차 인원 정보_2404.xlsx  # 서울 지하철 데이터 (2024.04)
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

---

## 📎 참고자료

- [공공데이터포털](https://www.data.go.kr) — 국민연금 가입 사업장 내역
- [서울 열린데이터광장](https://data.seoul.go.kr) — 지하철 시간대별 승하차 인원
- [YES24 베스트셀러](https://www.yes24.com/Product/Category/BestSeller)
- [YouTube Rank](https://youtube-rank.com)
