

# 다음 분기에 어떤 게임을 설계해야 할까 [:link:](https://github.com/pitapatat/Data_Analysis_Visualization/blob/main/%5BDA%5D_video_game_sales/%5BDA%5D_video_game_sales_ver_2.ipynb)

**:rocket: library: pandas, seaborn**

### 0. 목차
1. [배경 및 목적](#1-배경-및-목적)
2. [데이터셋 소개](#2-데이터셋-소개)
3. [분석 과정](#3-분석-과정)
4. [분석 결과](#4-분석-결과)
5. [한계점](#5-한계점)
6. [기타](#6-기타)


### 1. 배경 및 목적
```
- 연도별 게임의 트렌드 분석
- 지역별 선호하는 게임의 특성 분석
- 게임 출고량을 높이기 위한 전략 수립
```

### 2. 데이터셋 소개
```
- 출처 : Kaggle datasets
- 구성 : 1980-2020년 4개 지역(북미, EU, 일본, 기타)의 게임 출고량(by Genre/Publisher/Platform)
- 특징 : 2017년 이후 데이터셋(4개), 16,598개 데이터셋 
```

### 3. 분석 과정
```
- 데이터 전처리 : 연도/단위/타입 변경, 결측치 보완
- 데이터 분석 : 연도별/지역별/장르별/플랫폼별 게임 출고량 특징 분석 및 시각화
- 가설 설정 : ① 장르-플랫폼/장르-publisher 간 연관성이 없다 ② 지역간 선호하는 장르/플랫폼/publisher가 다르지 않다  
- 가설 검정 및 결과 도출
```

#### 3-1. 결측치 보완

|결측치 포함 column| 결측치 수 | 보완 방법
|:-:|:-:|-|
|**Year** | 271|  게임 데이터는 시간에 따라 사용하는 플랫폼도 변화하는 경향이 있음</br>  'Platform' feature를 기준으로 해당 플랫폼의 사용 연도의 평균을 계산하여 결측치 보완 
|**Publisher**| 58|  'unknown' 으로 변환해 별도의 카테고리로 분류

#### 3-2. 데이터 분석 
```
- 시대별 인기 장르/플랫폼등의 변화가 두드러지며 2009년 이후 감소세를 보임
- 전체 출고량 중 미국이 차지하는 비중이 크며 지역별로 선호하는 게임의 특성이 상이함 
- 글로벌 출고량 기준 '닌텐도'의 제품(wii 시리즈, 플랫폼게임 등)이 상위에 포진됨 
```
:heavy_check_mark: 연도별 게임 트렌드 현황 및 추이 
<center><img width = '1000' height = '200' src="https://user-images.githubusercontent.com/83687942/163708357-d2a5fd4c-e898-4042-80e1-0dc86aaaad46.png"></center>


:heavy_check_mark: 시대별 지역별 게임 출고량(예: 장르별)
<center><img width = '1000' height = '400' src="https://user-images.githubusercontent.com/83687942/163708331-ad8d2356-2075-4115-9457-7b5378dd520b.png"></


:heavy_check_mark: 지역별 출고량이 높은 게임 TOP10(예: 일본)
<center><img width="600" height= '250' src = 'https://user-images.githubusercontent.com/83687942/163708417-8c07c2d7-1616-464c-88db-d1a0d28cf5cd.png'></center>

:heavy_check_mark: 출고량이 높은 게임 TOP10 시각화 (예: EU)
<center><img width="400" height= '400' src = 'https://user-images.githubusercontent.com/83687942/163713489-d9a2a24b-2b2e-457d-9ec9-e1ae6722e00c.png'></center>

#### 3-3. 가설검정
```
- 변수간 독립성 검정(chi2) 결과 : 출고량 top10 플랫폼과 장르/ 출고량 top9 publisher와 장르간 연관성이 없다고는 볼 수 없음
- 2010년대 데이터 기준 지역간 장르/플랫폼/publisher 따른 출고량의 차이를 비교하면 종합적으로 지역간 유의한 차이가 존재하나 
   ① publisher : Nintendo, Activision 일 때
   ② platform : Wii, X360 일 때
   ③ genre : Shooter, Role-playing 일 때, 북미와 EU의 출고량이 비슷하고 이는 글로벌 출고량과도 유사한 유사한 모습을 보임
- 특히 일본은 타지역과 유의한 차이를 보이지만 Action 장르의 출고량은 북미와 유사하게 나타남   
```

### 4. 분석 결과

```
- 다음 분기 출고량의 절대량을 높이기 위해서는 북미지역 집중 공략 필요
- 북미와 EU는 선호 장르/플랫폼 등이 유사하므로 
- 일본은 글로벌 출고량 중 비중이 크지는 않지만 출고량 추세가 큰 변동이 없이 안정적인 모습을 보이므로 소홀히 해서는 안됨
- 다음 분기 매출 향상을 위해 게임 장르는 Action을 주력으로 하고 XBOX 또는 PS 플랫폼으로 출시하는 것을 제안함
```

### 5. 한계점
```
- 플랫폼의 경우 시리즈 형태로 출시된 경우가 많으므로 데이터를 재구조화 하여 '플랫폼에 따른 출고량 비교'의 정확성을 높일 필요가 있음 
   - 예) PS시리즈, XBOX 시리즈 등 비슷한 카테고리로 통합하여 플랫폼 시리즈 별 비교
- 도메인 지식(특히 플랫폼별 특징에 대한 이해)의 한계로 인해 다양한 시도 부족 및 해석의 한계가 존재함
- 시대별 게임의 장르 및 플랫폼의 변화의 '배경'(인기 원인, 유저들의 여론)이 무엇인지에 대한 고민이 필요함 
   - 향후 새로운 게임 장르 및 플랫폼 등장시 판매전략 수립에 고려해볼 사항이라 생각함 
```

### 6. 기타 
* 변동사항(22.01~) - 1차(ver_1) 작성 이후 동일 데이터(결측치 부분 상이)분석을 통한 데이터 시각화 및 분석내용 보완 : [ver_2](https://github.com/pitapatat/Data_Analysis_Visualization/blob/main/%5BDA%5D_video_game_sales/%5BDA%5D_video_game_sales_ver_2.ipynb)
 
