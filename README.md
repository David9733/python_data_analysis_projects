# Python 데이터 분석 포트폴리오

데이터 분석, 웹 크롤링, DB 연동, KMeans 클러스터링을 포함한 9개의 Python 데이터 분석 프로젝트 모음

---

## 📋 프로젝트 개요

| 항목 | 내용 |
| --- | --- |
| 개발 기간 | 2026.04 |
| 프로젝트 유형 | 개인 데이터 분석 포트폴리오 |
| 데이터 출처 |  웹 크롤링, 잇업 데이터(CSV/Excel), MariaDB |
| 분석 도구 | Python, Jupyter Notebook |
| 분석 기법 | 집계·정렬, KMeans 클러스터링, SQL 조회, 웹 자동화 |

---

## 🎯 프로젝트 목적

정형 데이터(CSV, Excel) 분석부터 Selenium 기반 웹 자동화, SQL을 통한 DB 조회, KMeans 클러스터링까지 데이터 분석의 전 과정을 구현하는 것을 목표로 했다. 

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
| 3 | 서울 중구 카페 상가수 | 총 888개 |
| 4 | 지하철 클러스터링 | 20개 역을 이용 패턴 기준 3개 그룹(9개·6개·5개 역)으로 분류 |
| 5 | YES24 베스트셀러 | 실시간 베스트셀러의 도서명·저자·출판사·출판일 수집 |
| 6 | 유튜브 댓글 수집 |  댓글 수집 및 DataFrame 저장 |

---

## 💡 인사이트

- **미국 이름 트렌드**: Michael, James, Robert 등 전통적인 영미권 이름이 누적 출생 수 기준 상위권을 독점하며, 시대와 무관하게 지속적으로 사용된 이름임을 확인
- **공개 데이터로 연봉 추정**: 국민연금 보험료율(9%)을 활용하면 연봉을 직접 제공하지 않는 공개 데이터에서도 사업장별 급여 수준을 근사할 수 있음
- **서울 중구 카페 포화도**: 서울 중구에만 888개의 커피점·카페가 운영 중, 상업 밀집 지역의 높은 카페 포화도를 수치로 확인
- **지하철 이용 패턴 다양성**: 승하차 상위 역들도 시간대별 패턴에 따라 명확히 구분되는 그룹이 존재하며, 단순 이용량 순위와는 다른 이용 특성이 있음을 클러스터링으로 확인

---

## 🔑 핵심 구현 내용

### 1. 국민연금 데이터 기반 평균연봉 역산

```python
raw['인당고지금액'] = raw['당월고지금액'] / raw['가입자수']
raw['평균월급여(만원)'] = raw['인당고지금액'] / 0.09 / 10000
raw['평균연봉(만원)'] = raw['평균월급여(만원)'] * 12
```

국민연금 법정 요율(9%)을 역산하여 별도 연봉 정보 없이도 사업장별 평균 급여 수준을 추정

### 2. 유튜브 댓글 수집 재사용 함수

```python
def yt_review(url, content_name, end_key_input):
    browser.get(url)
    time.sleep(3)
    for i in range(end_key_input):
        browser.find_element('css selector', 'body').send_keys(Keys.END)
        time.sleep(1)
    soup = BeautifulSoup(browser.page_source, 'html.parser')
    lst = soup.select('ytd-comment-thread-renderer.style-scope.ytd-item-section-renderer')
    result = []
    for element in lst:
        reply = element.select('div#content')[0].text.strip()
        result.append([content_name, reply])
    return pd.DataFrame(result, columns=['컨텐츠명', '댓글'])
```

URL, 컨텐츠명, 스크롤 횟수를 파라미터로 받아 다양한 영상에 재사용 가능하도록 함수화

### 3. 지하철 시간대별 KMeans 클러스터링

```python
columns_for_cluster = [
    '승차_새벽시간', '하차_새벽시간', '승차_출근시간', '하차_출근시간',
    '승차_점심시간', '하차_점심시간', '승차_오후시간', '하차_오후시간',
    '승차_퇴근및저녁', '하차_퇴근및저녁', '승차_밤시간', '하차_밤시간'
]
df_cluster = df.sort_values(by='승하차일합계', ascending=False).head(20)
kmeans = KMeans(n_clusters=3, random_state=30)
kmeans.fit(df_cluster[columns_for_cluster])
```

12개 시간대 특성으로 승하차 상위 20개 역을 3개 그룹으로 분류 — 결과: {0: 9개역, 2: 6개역, 1: 5개역}

### 4. SQL 서브쿼리 및 집계 연산

```sql
-- 가장 최근 가입 고객 조회
SELECT * FROM customers
WHERE join_date = (SELECT MAX(join_date) FROM customers)

-- 상가 규모별 수량 합산
SELECT sido_nm, sgg_nm, upjong_mnm,
       opn_1 + opn_2 + opn_3 + opn_5 + opn_5up AS total
FROM sgg_upjong_cnt
WHERE sido_nm = '서울특별시' AND sgg_nm = '중구' AND upjong_mnm = '커피점/카페'
```

---

## 🛠️ 기술 스택 및 선택 이유

| 기술 | 선택 이유 |
|---|---|
| Python | 데이터 분석 생태계와 라이브러리 지원 |
| Pandas | DataFrame 기반 정형 데이터 집계·정렬·파생 컬럼 처리 |
| Selenium | JavaScript 렌더링이 필요한 동적 웹페이지 자동화 및 스크롤 제어 |
| BeautifulSoup | CSS 셀렉터 기반 HTML 파싱으로 필요한 요소 정밀 추출 |
| SQLAlchemy | Python 환경에서 MariaDB 연결 및 SQL 결과를 DataFrame으로 수신 |
| scikit-learn | KMeans 클러스터링 구현 |
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

### KMeans Windows MKL 메모리 경고

**문제 상황**

Windows 환경에서 KMeans 실행 시 아래 경고 발생:
```
UserWarning: KMeans is known to have a memory leak on Windows with MKL,
when there are less chunks than available threads.
You can avoid it by setting the environment variable OMP_NUM_THREADS=1.
```

**원인 분석**

Windows + MKL 환경에서 사용 가능한 스레드 수보다 데이터 청크 수가 적을 때 발생하는 알려진 메모리 누수 이슈

**해결 방법**

```python
import os
os.environ['OMP_NUM_THREADS'] = '1'
```

**배운 점**

scikit-learn 경고 메시지에 해결 방법이 직접 명시되어 있었으며, 라이브러리 경고를 무시하지 않고 확인하는 습관이 중요하다는 것을 확인

---

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

한국 공공데이터 수집 시 인코딩을 명시적으로 지정해야 하며, `cp949`가 기본 처리 패턴이 됨

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
