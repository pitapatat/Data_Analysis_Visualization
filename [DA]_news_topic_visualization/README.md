
# 뉴스 토픽별 헤드라인 키워드 시각화
**:rocket: library: pandas, seaborn, BeautifulSoup, konlpy, WordCloud, squarify, gensim, pyLDAvis**


### 1. 배경 및 목적

+ 뉴스 주제와 
+ 시청자의 호응도(engagement) 판단 지표 개발 
+ (추가) streamlit을 통해 대시보드 구성

<image  src = 'https://user-images.githubusercontent.com/83687942/170807631-17521711-ba15-4fb1-a0d2-b87b2ab03cd6.gif'>

----
### 2. [데이터셋](https://dacon.io/competitions/official/235747/data) 소개

+ 뉴스 헤드라인(title) - 뉴스 주제(topic)로 구성
+ 

----
### 3. 분석 과정
   + 데이터 전처리 : 결측치 확인, 데이터 타입(to_datetime)을 변경하여 월/주 단위 추출 후 분석

   + 데이터 분석 : 카테고리별/월별/주별 상/하위 인기동영상의 특징 분석 및 시각화

   + tag 키워드 빈도 분석 : 카테고리별/월별 tag 키워드 빈도수 분석 및 시각화

   + 호응도 지표 분석 : 인기동영상의 지표별 특징 및 조회수와 다른 변수 간 상관관계 분석

   + 인기동영상 지표 개발 : 조회수 대비 (좋아요+싫어요)수, 구독자수 대비 조회수 외 관련 변수 가중치 부여
 
----
   
### 4. 가설 설정
   > - 좋아요/싫어요 수가 많을수록(higer "likes", higer "dislikes") 인기동영상에 올라갈 가능성이 높다.
   >  - 영상 업로드 날짜와 인기동영상에 올라간 날짜(trending_on_date)의 차이가 적을수록 인기동영상에 올라갈 가능성이 높다.
   >  - 평균 하루 조회수가 높을수록 인기동영상에 올라갈 가능성이 높다.
   >  - 영상 길이(duration)가 짧을수록 인기동영상에 올라갈 가능성이 높다.
   >  - 구독자수(subscribers)가 많을수록(혹은 기준 이상) 인기동영상에 올라갈 가능성이 높다.
   >  - 카테고리별 가중치: "entertainment/music/people & blogs" 카테고리 영상일수록 인기동영상에 올라갈 가능성이 높다.
   >  - 카테고리별 인기동영상에 높은 빈도로 나타나는 단어를 사용할수록 인기동영상에 올라갈 가능성이 높다.
   >  - ~~tags, description 긍정적일수록 인기동영상에 올라갈 가능성이 높다.~~
   
----
### 5. 분석 결과
#### 5-1. 인기동영상 채널 특징 

+ entertainment > people & blogs 순으로 나타나며 pets & animals 채널의 꾸준한 상승세가 두드러짐 

+ 월별 특이점 : 6,7월 sports 채널 상승세 두드러짐(카타르월드컵, euro2020, 도쿄올림픽 등 스포츠 시즌에 영향으로 추정) 
<center><img width="1000" height= '300' alt="month-flow" src="https://user-images.githubusercontent.com/83687942/163302783-5a119f01-23c9-4c6b-8069-6cde4d8b4a70.png"></center>
<center><img width="1000" height= '300' alt="month-cat" src="https://user-images.githubusercontent.com/83687942/163302876-ef211500-aafe-44ca-9d5d-99196b0e4fd3.png"></center>
   
+ 주별 특이점 : 주별 카테고리의 변동폭이 크나 구성비에는 큰 변화 없음. howto & style 채널이 상위권에 자주 랭크됨 

<center><img width="1000" height= '300' alt="week-flow" src="https://user-images.githubusercontent.com/83687942/163304127-bbc312f6-bb14-484d-837d-21ab6898ce25.png"></center>
<center><img width="1000" height= '300' alt="week-cat" src="https://user-images.githubusercontent.com/83687942/163304167-1f863741-fcc6-4fc9-b463-51fbb52a348f.png"></center>

+ 월별 TOP10 채널 
<center><img width="1000" height= '300' alt="month-top10" src="https://user-images.githubusercontent.com/83687942/163305727-8288615b-3b71-4096-b856-fa426cf76741.png"></center>

+ 월별 tag 키워드 : "먹방", "몰카", "일상", "브이로그"는 매월 공통으로 높은 빈도로 등장하며 유행어(예: 브레이브걸스, 올림픽 등)가 tag로 주로 사용됨 
<center><img width="1000" height= '300' alt="teg-4" src="https://user-images.githubusercontent.com/83687942/163306585-b47e6725-05fc-4383-80c5-7b71dd8d0e94.png"></center>

+ 카테고리별 tag 키워드 : 카테고리별 유명 인플루언서(또는 운동선수/연예인)의 빈도가 높으며 "음식", "먹방" tag는 카테고리별 영향을 덜 받는 편임 
<center><img width="1000" height= '300' alt="sports-tag" src="https://user-images.githubusercontent.com/83687942/163305901-308b9d49-bf3c-4b52-a3f8-73f9bac84d5e.png"></center>

#### 5-2. 인기 호응도 지표 분석 
+ 인기동영상의 특징 - 10-15분 길이의 영상/업로드 후 시간당 1만회 조회수 & 2일 내 인기동영상 진입 & 3일 내 유지

+ 조회수와 높은 상관관계 지표 : 좋아요수, 싫어요수, 댓글수, 구독자수

<center><img width="500" height= '400' alt="corr" src="https://user-images.githubusercontent.com/83687942/163309811-49066ee8-8e07-4199-840e-088930729664.png"></center>

#### 5-3. 인기 호응도 지표 개발
+ 조회수와 높은 상관관계를 보이는 지표들의 가중치 평균 및 가중치 조정값을 통해 인기 호응도 지표를 개발하고자 함

+ 하지만 '조회수(또는 좋아요수)'의 상관관계/ols 검정 결과 유의미한 선형 상관관계는 나타나지 않음

----
### 6. 한계점 및 보완점
   
+ **<목적의 불명확성>**
   + 인기호응도 지표의 활용 목적 및 정의를 명확하게 하지 않고 분석하여 결국 조회수와 비슷한 성격의 인기지표들의 조합으로 지표를 개발하게 됨
   + 예를 들어 광고 타겟층 예측, 광고 수익 예측등을 목표로 호응도 지표를 개발한다면 고려해야 할 변수는 (영상 조회수, 영상이 끊기는 시점, 코멘트 내용, 사용자 정보 데이터 등)으로 좀 더 구체적이고 명확해 질 수 있음. **<u>어떤 문제를 해결하기 위한 것인지를 명확히 할 필요가 있음</u>**

+ **<가설 설정 및 검증>**
   + 가설 검증을 위해서는 인기동영상/비인기동영상의 그룹군으로 구별하여 분석해야 하므로 인기동영상이 아닌 동영상의 데이터가 추가적으로 필요함
   
   + 애초에 가설 설정이 잘못되었으며 본 데이터를 통해서는 인기동영상의 특징과 지표(변수)간 관계에 대한 분석이 가능함. 이는 향후 동영상 제작 시 고려해볼 수 있는 요소로 활용될 수 있음. **<u>주어진 데이터로 해결할 수 있는 문제가 무엇인지 우선적으로 고려해야 함</u>**

+ **<호응도 지표 개발>**
   + 지표개발을 위해 유효 변수에 가중치를 부여하는 과정에서 통한 가중치 변환이 너무 단순하게 이뤄졌음
   
+ **<기타>** 
   + 인기동영상에 영향을 미치는 요인으로 데이터에서 주어진 변수 외 다른 요인(시기적 이슈-선거, 올림픽, 김장, 음박 출시 등)을 고려하지 못함

   + 채널(계정) 생성 시기 데이터를 추가하고, 인기동영상의 tag, description의 긍/부정 분석을 통해 어떤 특징이 있는지 살펴보면 좋을 것 같음
   

----
### 7. 업데이트('22.05)
   
+ _plotly_ 와 _streamlit_ 라이브러리를 활용하여 인터렉티브하게 시각화하고 대시보드 형태로 구현 

+ HOW TO RUN 
   ```python
      git clone [주소] 
 
      cd ./youtube
   
      pip install -r requirements.txt
   
      streamlit run app.py
   ```

   





