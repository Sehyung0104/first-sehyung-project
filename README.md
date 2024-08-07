# 의료 로봇 섹터 뉴스 데이터 감성 분석을 통한 주식 시장 경향 분석

<aside>
🚶 **1조 개미왕**: 강지훈, 고선민, 김주영, 이세형

</aside>

### 💬 목차

---

1. 주제 소개
2. 자료 조사 및 주식 데이터 수집
3. 뉴스 데이터 웹크롤링
4. 데이터 베이스 구축
5. 뉴스 데이터 가공 및 입력
6. 뉴스 데이터를 통한 감성 분석
7. 데이터 분석 및 시각화
8. 결론

[https://news.amc.seoul.kr/news/file/imageView.do?fileId=F000000031638](https://news.amc.seoul.kr/news/file/imageView.do?fileId=F000000031638)

### 🏥 주제: 의료 로봇 섹터 뉴스 데이터의 감성 분석을 통한 주식 시장 경향 분석

---

- 본 프로젝트는 뉴스 기사의 정서와 그것이 주가에 미치는 영향을 분석함으로써 시장 행동과 일반적인 투자 전략의 타당성에 대한 더 깊은 이해를 제공하는 것을 목표
- **감성 분석 (Sentiment Analysis)**이란?
    - 텍스트나 음성파일에 녹취된 감성, 평가, 의견, 태도, 말투 등의 주관적인 정보를 컴퓨터 학습을 통해 분석하는 과정. 주로 문장 안에 어떤 부분에 의견이 담겨있는지 정의를 하고 그 모아진 의견들을 요약함.

### ⁉️ 의료 로봇 섹터 선정 이유

---

- 네명의 공통 관심사인 ‘로봇’과 관련된 종목들을 한 곳씩 뽑아 한국과 미국의 주식 흐름을 비교하고 구글 트렌드 데이터와 뉴스 데이터로 감성 분석를 해보고자 했었음.
- 원래 비교하고자 했었던 종목들:
    
    
    **의료 로봇 섹터**: Intuitive Surgical vs 고영 테크놀러지
    
    ---
    
    ![Untitled](%E1%84%8B%E1%85%B4%E1%84%85%E1%85%AD%20%E1%84%85%E1%85%A9%E1%84%87%E1%85%A9%E1%86%BA%20%E1%84%89%E1%85%A6%E1%86%A8%E1%84%90%E1%85%A5%20%E1%84%82%E1%85%B2%E1%84%89%E1%85%B3%20%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%84%90%E1%85%A5%20%E1%84%80%E1%85%A1%E1%86%B7%E1%84%89%E1%85%A5%E1%86%BC%20%E1%84%87%E1%85%AE%E1%86%AB%E1%84%89%E1%85%A5%E1%86%A8%E1%84%8B%E1%85%B3%E1%86%AF%20%E1%84%90%E1%85%A9%E1%86%BC%E1%84%92%20409369059abc4482972c6710081c18ba/Untitled.png)
    
    **가정용 로봇 섹터 (로봇 청소기)**: iRobot Corporation vs 에브리봇
    
    ---
    
    ![Untitled](%E1%84%8B%E1%85%B4%E1%84%85%E1%85%AD%20%E1%84%85%E1%85%A9%E1%84%87%E1%85%A9%E1%86%BA%20%E1%84%89%E1%85%A6%E1%86%A8%E1%84%90%E1%85%A5%20%E1%84%82%E1%85%B2%E1%84%89%E1%85%B3%20%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%84%90%E1%85%A5%20%E1%84%80%E1%85%A1%E1%86%B7%E1%84%89%E1%85%A5%E1%86%BC%20%E1%84%87%E1%85%AE%E1%86%AB%E1%84%89%E1%85%A5%E1%86%A8%E1%84%8B%E1%85%B3%E1%86%AF%20%E1%84%90%E1%85%A9%E1%86%BC%E1%84%92%20409369059abc4482972c6710081c18ba/Untitled%201.png)
    
    **자율 주행 모빌리티 섹터**: Tesla vs 현대차
    
    ---
    
    ![Untitled](%E1%84%8B%E1%85%B4%E1%84%85%E1%85%AD%20%E1%84%85%E1%85%A9%E1%84%87%E1%85%A9%E1%86%BA%20%E1%84%89%E1%85%A6%E1%86%A8%E1%84%90%E1%85%A5%20%E1%84%82%E1%85%B2%E1%84%89%E1%85%B3%20%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%84%90%E1%85%A5%20%E1%84%80%E1%85%A1%E1%86%B7%E1%84%89%E1%85%A5%E1%86%BC%20%E1%84%87%E1%85%AE%E1%86%AB%E1%84%89%E1%85%A5%E1%86%A8%E1%84%8B%E1%85%B3%E1%86%AF%20%E1%84%90%E1%85%A9%E1%86%BC%E1%84%92%20409369059abc4482972c6710081c18ba/Untitled%202.png)
    
    **반도체 섹터**: NVIDIA vs SK 하이닉스
    
    ---
    
    ![Untitled](%E1%84%8B%E1%85%B4%E1%84%85%E1%85%AD%20%E1%84%85%E1%85%A9%E1%84%87%E1%85%A9%E1%86%BA%20%E1%84%89%E1%85%A6%E1%86%A8%E1%84%90%E1%85%A5%20%E1%84%82%E1%85%B2%E1%84%89%E1%85%B3%20%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%84%90%E1%85%A5%20%E1%84%80%E1%85%A1%E1%86%B7%E1%84%89%E1%85%A5%E1%86%BC%20%E1%84%87%E1%85%AE%E1%86%AB%E1%84%89%E1%85%A5%E1%86%A8%E1%84%8B%E1%85%B3%E1%86%AF%20%E1%84%90%E1%85%A9%E1%86%BC%E1%84%92%20409369059abc4482972c6710081c18ba/Untitled%203.png)
    
- 제일 유의미 해보이는 의료 로봇 섹터에 집중해보기로 결정.
- 구글 트렌드 데이터와 뉴스 데이터로 감성 분석를 해보고자 했었음.

최종 선택된 의료 로봇 (medical / surgical robot) 종목:

- 🇺🇸 미국
    - Intuitive Surgical, Inc. (ISRG, NASDAQ)
        - 최소 침습 수술이 가능한 다빈치 수술 시스템이 대표적.
    - Stryker Corporation (SYK, NYSE)
        - 다양한 의료 기기와 수술 로봇 제공. MAKO 시스템이 대표적.
    - Medtronic Plc, (MDT, NYSE)
        - 다양한 의료 기기 제공. Hugo RAS 시스템으로 로봇 수술 시장에 진출.
    - Globus Medical, Inc. (GMED, NYSE)
        - 척추 및 정형외과 수술용 로봇 개발
    - Asensus Surgical, Inc. (ASXC, NYSE)
        - senhance surgical system으로 로봇 보조 수술을 가능하게 함
    - Smith & Nephew Plc, (SNN, NYSE)
        - 정형외과 수술용 로봇인 NAVIO 보유
    - Johnson & Johnson, (JNJ, NYSE)
        - 수술 로봇 분야에서 새로운 플랫폼 개발 중

- 🇰🇷 국내
    - 고영(098460.KQ)
        - 고정밀 3D 검사 장비 로봇, 뇌수술 로봇
    - 큐렉소(060280.KQ)
        - 인공 관절 및 척추 수술용 로봇. 큐비스-조인트
    - 미래컴퍼니(049950.KQ)
        - 복강경 수술용 로봇. ‘로보틱스’ 시리즈

### 📈 자료 조사 및 주식 데이터 수집

---

> 사용한 패키지: [yfinance](https://pypi.org/project/yfinance/)
> 
> - **yfinance**: 야후 파이낸스의 주가 관련 데이터를 손쉽게 받아올 수 있는 파이썬 라이브러리

[주식 차트 관련 소스 코드](https://www.notion.so/7e21dc322dc046f08f5a38f3709aae3a?pvs=21)

- 미국 기업들의 주가 변화 및 상관관계
    - 각 기업들의 주식을 정규화해서 비교하기 위해서 해당날자의 주식을 기준일의 주식으로 나눔
    
    ```
    import yfinance as yf
    import pandas as pd
    import matplotlib.pyplot as plt
    import koreanize_matplotlib 
    # 로봇 및 자율주행 섹터에 속한 회사들의 목록
    companies = ['ISRG', 'MDT', 'SYK', 'GMED', 'SNN', 'JNJ','ASXC']
    
    # Yahoo Finance에서 역사적 데이터를 다운로드합니다.
    start_date = "2020-01-01"
    end_date = "2024-05-30"
    data = yf.download(companies, start=start_date, end=end_date)['Adj Close']
    
    # 결측 데이터 처리 (앞의 값을 채워 넣음)
    data.fillna(method='ffill', inplace=True)
    
    # 개별 주식의 정규화 데이터를 계산
    normalized_data = data / data.iloc[0]
    
    # 개별 주식을 그리기 위한 그래프 설정
    plt.figure(figsize=(14, 7))
    
    # 각 회사의 정규화된 주식 가격을 플롯
    for company in companies:
        plt.plot(normalized_data.index, normalized_data[company], label=company)
    
    # 그래프 제목 및 축 레이블 설정
    plt.xlabel('Date')
    plt.ylabel('Normalized Price')
    plt.title('SUGICAL ROBOT COMPANIES(2020-2024)')
    plt.legend()
    plt.grid(True)
    plt.show()
    
    ```
    
    ![Untitled](%E1%84%8B%E1%85%B4%E1%84%85%E1%85%AD%20%E1%84%85%E1%85%A9%E1%84%87%E1%85%A9%E1%86%BA%20%E1%84%89%E1%85%A6%E1%86%A8%E1%84%90%E1%85%A5%20%E1%84%82%E1%85%B2%E1%84%89%E1%85%B3%20%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%84%90%E1%85%A5%20%E1%84%80%E1%85%A1%E1%86%B7%E1%84%89%E1%85%A5%E1%86%BC%20%E1%84%87%E1%85%AE%E1%86%AB%E1%84%89%E1%85%A5%E1%86%A8%E1%84%8B%E1%85%B3%E1%86%AF%20%E1%84%90%E1%85%A9%E1%86%BC%E1%84%92%20409369059abc4482972c6710081c18ba/Untitled%204.png)
    
    - 미국 기업들은 의료 로봇 종목 간의 상관관계가 거의 없다싶이 함. 아마 건강(헬스케어), 의료, 로봇, 기술 등 다양한 섹터의 영향을 받았을 것 같은 느낌.
        
        ![Untitled](%E1%84%8B%E1%85%B4%E1%84%85%E1%85%AD%20%E1%84%85%E1%85%A9%E1%84%87%E1%85%A9%E1%86%BA%20%E1%84%89%E1%85%A6%E1%86%A8%E1%84%90%E1%85%A5%20%E1%84%82%E1%85%B2%E1%84%89%E1%85%B3%20%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%84%90%E1%85%A5%20%E1%84%80%E1%85%A1%E1%86%B7%E1%84%89%E1%85%A5%E1%86%BC%20%E1%84%87%E1%85%AE%E1%86%AB%E1%84%89%E1%85%A5%E1%86%A8%E1%84%8B%E1%85%B3%E1%86%AF%20%E1%84%90%E1%85%A9%E1%86%BC%E1%84%92%20409369059abc4482972c6710081c18ba/Untitled%205.png)
        
- 한국 기업들의 주가 변화 및 상관관계
    
    ![Untitled](%E1%84%8B%E1%85%B4%E1%84%85%E1%85%AD%20%E1%84%85%E1%85%A9%E1%84%87%E1%85%A9%E1%86%BA%20%E1%84%89%E1%85%A6%E1%86%A8%E1%84%90%E1%85%A5%20%E1%84%82%E1%85%B2%E1%84%89%E1%85%B3%20%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%84%90%E1%85%A5%20%E1%84%80%E1%85%A1%E1%86%B7%E1%84%89%E1%85%A5%E1%86%BC%20%E1%84%87%E1%85%AE%E1%86%AB%E1%84%89%E1%85%A5%E1%86%A8%E1%84%8B%E1%85%B3%E1%86%AF%20%E1%84%90%E1%85%A9%E1%86%BC%E1%84%92%20409369059abc4482972c6710081c18ba/Untitled%206.png)
    
    - 아래보면 한국은 의료 로봇 종목 간의 상관관계가 상당히 높음을 알 수 있음. (1에 가까울 수록 관계성이 높다고 봄)
    
    ![Untitled](%E1%84%8B%E1%85%B4%E1%84%85%E1%85%AD%20%E1%84%85%E1%85%A9%E1%84%87%E1%85%A9%E1%86%BA%20%E1%84%89%E1%85%A6%E1%86%A8%E1%84%90%E1%85%A5%20%E1%84%82%E1%85%B2%E1%84%89%E1%85%B3%20%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%84%90%E1%85%A5%20%E1%84%80%E1%85%A1%E1%86%B7%E1%84%89%E1%85%A5%E1%86%BC%20%E1%84%87%E1%85%AE%E1%86%AB%E1%84%89%E1%85%A5%E1%86%A8%E1%84%8B%E1%85%B3%E1%86%AF%20%E1%84%90%E1%85%A9%E1%86%BC%E1%84%92%20409369059abc4482972c6710081c18ba/Untitled%207.png)
    
- 한국과 미국 기업의 주가 평균 비교
    - 한국에 비해 미국은 주가 변동이 크지않은걸 알수있음
    
    ![Untitled](%E1%84%8B%E1%85%B4%E1%84%85%E1%85%AD%20%E1%84%85%E1%85%A9%E1%84%87%E1%85%A9%E1%86%BA%20%E1%84%89%E1%85%A6%E1%86%A8%E1%84%90%E1%85%A5%20%E1%84%82%E1%85%B2%E1%84%89%E1%85%B3%20%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%84%90%E1%85%A5%20%E1%84%80%E1%85%A1%E1%86%B7%E1%84%89%E1%85%A5%E1%86%BC%20%E1%84%87%E1%85%AE%E1%86%AB%E1%84%89%E1%85%A5%E1%86%A8%E1%84%8B%E1%85%B3%E1%86%AF%20%E1%84%90%E1%85%A9%E1%86%BC%E1%84%92%20409369059abc4482972c6710081c18ba/Untitled%208.png)
    

### 📰 뉴스 데이터 웹크롤링 및 데이터 가공 / 전처리

---

- [News API](https://newsapi.org/) 를 사용해서 손쉽게 뉴스 본문을 가져오려고 했으나 일일 횟수 제한 때문에 결국 beautifulSoup과 selenium를 사용해서 일일히 웹크롤링 하기로 결정.
- **네이버 기사 크롤링 과정**
    1. 웹드라이버를 통해 네이버 뉴스 검색 URL 접속
        
        `driver = webdriver.Chrome(service=webdriver_service, options=options)`
        
    2. 검색어 입력 후 스크롤을 최대치로 내린 후 잠시 대기
        1. 네이버는 최대 4000개?까지 기사가 떴음
    3. 새로운 높이 계산 후 새로운 높이가 이전 높이와 같으면 더 이상 로드할 내용 없으므로 스크롤 종료
    4. BeautifulSoup를 사용하여 기사 정보 추출
        
        `soup = BeautifulSoup(driver.page_source, 'html.parser')`
        
    5. newspaper3k의 article을 통해 본문도 추출
    
    ```python
    # 기사 본문 추출 함수
    def get_article_content(url):
        try:
            article = Article(url, language='ko')
            article.download()
            article.parse()
            return article.text
        except Exception as e:
            print(f"Error fetching article: {e}")
            return None
    ```
    
    1. konlpy.tag의 Okt를 통해 키워드 (명사) 추출
    
    ```python
    # konlpy를 활용해 키워드 (명사) 추출해내는 함수 적용
    def extract_keywords(text):
        try:
            okt = Okt()
            nouns = okt.nouns(text)
            filtered_nouns = [noun for noun in nouns if len(noun) > 1]
            count = Counter(filtered_nouns)
            keywords = count.most_common(10)
            return [keyword for keyword, _ in keywords]
        except Exception as e:
            print(f"Error extracting keywords: {e}")
            return None
    ```
    
    [네이버 기사 크롤링 소스 코드](https://www.notion.so/dd4f013e2ae74bd18a3515ea8c18059b?pvs=21)
    
- **네이버 기사 데이터 가공 / 전처리 과정**
    1. 기사 본문 ‘content’ 칼럼 쭉 살펴보고 빈칸, NaN value, 잘못된 내용이 들어가있으면 모두 unwanted_data 함수를 따로 만들어서 filtering으로 특정
        - java script를 사용한 웹사이트나 유료 구독형 (paywall) 뉴스 기사들은 본문이 안 읽혀서 어쩔 수 없이 제거.
    2. 기업 별로 혹시 잘못 들어간 뉴스 데이터 없는지 확인.
        - 예를 들어, 고영 같은 경우 고려대 고영캠퍼스가 서치에 같이 걸렸음.
    
    [네이버 크롤링 데이터 unwanted_data 처리](https://www.notion.so/unwanted_data-02f618d820d14465a724b254b239157d?pvs=21)
    

- **구글 기사 크롤링 과정**
    1. headless 웹드라이버로 구글 뉴스 검색 URL 접속
        1. 키워드 검색, 날짜 선정, 날짜순 정열, 검색 지역 (미국) 선정 등 url만 필요에 따라 바꿔주면서 크롤링 해옴.
    
    ```python
    word = "Johnson+&+Johnson"
    base_url = 'https://www.google.com/search?q={}&hl=en&tbas=0&tbs=cdr:1,cd_min:{},cd_max:{},sbd:1&tbm=nws&start={}'
    ```
    
    1. While loop 형식으로 특정 시작일부터 종료일까지 21일(3주)치의 기사량 검색
    2. 화면에 보이는 최대 10개 기사 정보를 selenium 기반으로 추출.
    3. newspaper Article을 활용해 url 링크로 기사 HTML 접근 후 다운로드 및 본문 추출.
    4. Article에 있는 자연어 처리 함수 적용 후 키워드 추출.
    
    ```python
    # newspaper 모듈을 통해 기사 다운로드
    # download, parse, and extract the whole main content of the article
    content = Article(article_data['url'], config=config)
    content.download()
    content.parse()
    article_data["content"] = content.text
    
    # 기사 본문 추출하고 난 뒤, 자연어 처리를 통해 본문의 키워드를 뽑아올 수 있음
    # once the content is found, use NLP ML to extract keywords of the article
    content.nlp()
    article_data["keyword"] = content.keywords
    ```
    
    1. 모두 추출했으면 그 다음 페이지로 넘어가는 For loop 설정 (한번에 최대 30페이지까지 서치 가능)
    
    ![Untitled](%E1%84%8B%E1%85%B4%E1%84%85%E1%85%AD%20%E1%84%85%E1%85%A9%E1%84%87%E1%85%A9%E1%86%BA%20%E1%84%89%E1%85%A6%E1%86%A8%E1%84%90%E1%85%A5%20%E1%84%82%E1%85%B2%E1%84%89%E1%85%B3%20%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%84%90%E1%85%A5%20%E1%84%80%E1%85%A1%E1%86%B7%E1%84%89%E1%85%A5%E1%86%BC%20%E1%84%87%E1%85%AE%E1%86%AB%E1%84%89%E1%85%A5%E1%86%A8%E1%84%8B%E1%85%B3%E1%86%AF%20%E1%84%90%E1%85%A9%E1%86%BC%E1%84%92%20409369059abc4482972c6710081c18ba/Untitled%209.png)
    
    [구글 기사 크롤링 소스 코드](https://www.notion.so/8d476bcc46c9490b8f10141704498952?pvs=21)
    
- **구글 기사 데이터 가공 / 전처리 과정**
    1. 네이버와 동일한 방식으로 기사 본문 ‘content’ 칼럼 쭉 살펴보고 빈칸, NaN value, 잘못된 내용이 들어가있으면 모두 unwanted_data 함수를 따로 만들어서 filtering으로 걸러냄.
    2. 기업 별로 혹시 예외적으로 잘못 들어간 뉴스 데이터 없는지 확인 작업.
        - Smith & Nephew (SNN)와 Johnson & Johnson (JNJ) 같은 경우 너무 흔한 이름이기에… 다른 동명이인 기사가 서치에 걸리기도 했었음.
        - 특히 구글 같은 경우, 최근 날짜로 검색할수록 언론사 기사가 아닌 유투브, 개인 저널리스트 블로그 등 믿음직스럽지 않은 출처의 기사들도 서치에 걸림.
        - 고급 검색 기능 중 쌍따음표 안에 검색어를 가두는 방식도 고려해봤으나 오히려 뉴스가 아닌 연관성 없는 글들이 더 많이 떴음.
        
        ![Untitled](%E1%84%8B%E1%85%B4%E1%84%85%E1%85%AD%20%E1%84%85%E1%85%A9%E1%84%87%E1%85%A9%E1%86%BA%20%E1%84%89%E1%85%A6%E1%86%A8%E1%84%90%E1%85%A5%20%E1%84%82%E1%85%B2%E1%84%89%E1%85%B3%20%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%84%90%E1%85%A5%20%E1%84%80%E1%85%A1%E1%86%B7%E1%84%89%E1%85%A5%E1%86%BC%20%E1%84%87%E1%85%AE%E1%86%AB%E1%84%89%E1%85%A5%E1%86%A8%E1%84%8B%E1%85%B3%E1%86%AF%20%E1%84%90%E1%85%A9%E1%86%BC%E1%84%92%20409369059abc4482972c6710081c18ba/Untitled%2010.png)
        
    
    [구글 크롤링 데이터 전처리](https://www.notion.so/b529697fbc4a4922a24d3c46131d91bd?pvs=21)
    

> 사용한 패키지: [newspaper3k](https://newspaper.readthedocs.io/en/latest/), [konlpy](https://konlpy.org/en/latest/api/konlpy.tag/)
> 
> - **newspaper3k** : HTTP 요청 (requests) 모듈과 lxml 모듈을 기반으로 만들어진 뉴스 기사 추출 전용 파이썬 패키지. 연산과정이 복잡하여 (computationally expensive) 방대한 양의 데이터 수집 과정에서는 오작동할 수 있음.
> - **konlpy**: 한국어 전용 자연어 처리 (NLP) 파이썬 패키지. 이중에서도 문장을 단어(어절) 단위로 토큰화를 수행해주는 토크나이저(tokenizer)인 Okt class를 사용함.

### 🚀 데이터 베이스 구축

---

[DB 스키마 정보](https://www.notion.so/DB-28b63a804c6c4fe38620a55e6291e308?pvs=21)

### 🧑‍💻 뉴스 데이터를 통한 감성 분석 모델 적용

---

- 네이버 기사에는 [Naver API (CLOVA Sentiment)](https://www.ncloud.com/product/aiService/clovaSentiment) 같은 국문 특화 감성분석 API를 사용해보려고 했으나 일일 서치 갯수가 1000회여서 포기.
- 결국 transformers의 piplines 함수를 활용해 **KR-FinBert-SC** 국문 모델과 **BERT-base-uncased** 영문 모델을 적용해서 감성 분석 진행함.

> 사용한 패키지: transformers의 [pipelines](https://huggingface.co/transformers/v3.0.2/main_classes/pipelines.html) 함수
> 
> - **transformers**: Hugging Face에서 제공하는 Transformers 라이브러리는 모든 종류의 NLP 작업을 손쉽게 해결해줌. 그중에서도 pipeline 함수는 특정 모델과 동작에 필요한 전처리 및 후처리 단계를 쉽고 간결하게 적용해줌.
- **감성분석 국문 모델 적용 (KR-FinBert-SC)**
    - 네이버에서 크롤링해온 한국 기사들은 서울대 NLP랩에서 만든 금융 관련 감성 분석 모델 [**snunlp/KR-FinBert-SC**](https://huggingface.co/snunlp/KR-FinBert-SC)  적용.
    - 약 72개의 언론사 뉴스 데이터, 16개의 증권사 실적서 데이터로 학습시킨 모델로 약 96프로의 정확도를 보인다고 함.
    - konlpy okt로 뽑았던 키워드들에 적용
    - newspaper article로 뽑아왔던 본문과 제목에 적용
    
    [감성분석 / transfomer_pipeline](https://www.notion.so/transfomer_pipeline-6553a8ce8f274557baccbc700e7cdbe4?pvs=21)
    
- **감성분석 영문 모델 적용 (BERT-base-uncased)**
    - 제품 리뷰 관련 감성 분석에 활용되는 모델 [**nlptown/bert-base-multilingual-uncased-sentiment**](https://huggingface.co/nlptown/bert-base-multilingual-uncased-sentiment) 적용
    - 서양권 언어 특히 영어에 특화되었으며 약 150,000개의 제품 리뷰로 fine-tuning된 모델. 약 67~95 프로의 정확도를 보인다고 함.
    - 다른 SNS 관련 감성 분석에 활용되는 영문 모델 (cardiffNLP)도 적용해서 비교해봤으나 NLPtown의 모델이 BERT의 가장 기본적인 모델이라 그런지 결과값이 명확하게 나왔음.
    
    [감성분석 / 영문 모델 / transfomer_pipeline](https://www.notion.so/transfomer_pipeline-e495b64c77ca4557a035ea515c53cbcc?pvs=21)
    

## 🗃️ 데이터 분석 및 시각화

---

### 📊 뉴스 기사량과 주식의 상관관계

- 기사량,주가,거래량 비교
    
    [한국](https://www.notion.so/d266cb8250d1455b910e5061ee991245?pvs=21)
    
    [미국](https://www.notion.so/d6270ec1aa7547ea95d311ebd7364553?pvs=21)
    

### 📈뉴스 데이터와 주식의 등락에 대한 상관관계 분석

[뉴스데이터와 주식의 등락에 대한            상관관계 분석](https://www.notion.so/bed6da14028b4a6f87309b9275095b30?pvs=21)

[Roberta 딥러닝모델을 활용한 모델학습과        학습모델을 활용한 감성분석](https://www.notion.so/Roberta-36c371b279c04545805ad96a10ce16be?pvs=21)

### **💻 주식과 뉴스 데이터의 감성분석 상관관계 및 키워드 시각화**

[**주식과 뉴스 데이터의 감성분석 상관관계 및 키워드 시각화**](https://www.notion.so/29614c0fcb6d45afb178eece46a05076?pvs=21)

### 🪫특정 구간에서의 특이점 파악

[특정구간에서의 특이점 파악(SNN)](https://www.notion.so/SNN-14023a58e9c0483b8e2ccb730b2df5f9?pvs=21)

[특정구간에서의 특이점 파악 (ISRG)](https://www.notion.so/ISRG-59c77ce584b14f818501a0a4cb09ddcb?pvs=21)

[특정구간에서의 특이점 파악 (ASXC)](https://www.notion.so/ASXC-035f695736654d9d8fb1d4b3a727d5c9?pvs=21)

### 📖 결론선

---

- 뉴스 데이터로 주식 시장 경향을 완전히 분석하기엔 한계가 존재함.
- 하지만, 뉴스 키워드와 감성 분석 결과는 보조 지표로서의 충분한 역할을 함.
