#  서울시 문화 불균형해소를 위한 인프라 탐색 - 도시재생 지표를 활용한

#### 팀 소개
공공 빅데이터 청년 인턴십 프로젝트

[박주원](https://github.com/scppliop) [김명훈](https://github.com/minghoona) [김수현](https://github.com/soohyunme) [신민경](https://github.com/minzzing) [엄현빈](https://github.com/Umhyunbin) [이현지](https://github.com/LocalLeeFarm) [하지민](https://github.com/jimnida)

#### 분석 배경 및 목적
- 도시재생은 지역의 특색 있는 자원을 활용해 역량과 잠재력을 끌어내는 것을 목표로 한다.   
- 특히 **문화**는 지역의 특성을 대표하는 중요한 변수로 여겨진다. 최근에는 문화적 관점에서 공간과 도시를 재구성하는 등, 도시의 패러다임이 변화하면서 그 중요성이 더욱 부각된다.  
- 현재 도시재생 사업은 지원 방식에 있어 지역적 특성을 적절히 반영하지 못하는 것이 문제점으로 대두되고 있다.  
- 이에 본 프로젝트에서는 **문화**의 측면에서 각 지역별 도시재생 사업을 공간적으로 파악하고, 클러스터링과 같은 데이터 기반 방법론을 활용해 도시재생 사업의 맹점을 보완하고자 한다.  

## 목차
1. [Directory](#1-directory)
2. [분석 프로세스](#2-분석-프로세스)
3. [데이터 수집](#3-데이터-수집)
4. [데이터 전처리](#4-데이터-전처리)
5. [활성화 필요지역 선정 - Clustering](#5-활성화-필요지역-선정---clustering)
6. [문화 취약 지역 선정 및 Target 지역 선정](#6-문화-취약-지역-선정-및-target-지역-선정)
7. [인프라 선정](#7-인프라-선정)
8. [수요지 선정](#8-수요지-선정)
9. [인프라 제안](#9-인프라-제안)

## 1. directory
├─Data : 프로젝트에 사용되는 데이터 모음  
│ ├─Processing : 전처리 데이터  
│ ├─Rawdata  
│ └─Result : 모델 결과 데이터  
├─Location : 수요지 선정을 위한 파일 모음  
│ ├─QGIS : QGIS 데이터 & 수요지 선정용 코드  
│ │ ├─Administrative_area : 행정동 경계 데이터  
│ │ │ └─Demand_Singil 3,4 : 최종 수요 후보지 데이터  
│ │ ├─Demand : 수요 후보지 도출을 위한 데이터  
│ │ ├─Infra : 영등포구 인프라 데이터  
│ │ └─Population : 총인구수 격자 데이터 (2020. 10)  
├─Model_code : 클러스터링 코드  
└─Processing_code : 전처리 코드  


## 2. 분석 프로세스
### 1) 지역 선정
① 도시재생 활성화 진단지표를 활용하여 도시재생 사업이 필요한 지역을 Clustering 결과 비교를 통해 선정

② 문화생활에 대한 만족도를 통해 '만족 대비 불만족 비율'인 '개선효용도'가 상대적으로 낮은 문화 개선이 필요한 지역을 탐색

③ ①과 ②를 만족하는 분석 대상 지역(행정동) 선정
 
### 2) 인프라 선정 및 입지 선정
#### - 카테고리 선정
① 히트맵을 기반으로 대상 지역의 문화, 휴식, 운동 중 부족한 인프라 파악

② 대분류 인프라의 하위 카테고리 중 생활 밀접도를 기반으로 구체적인 문화 인프라 선정

#### - 수요지 선정
① 대상 자치구의 총인구 상위 지역에 해당하는 격자 도출
- 공간가중행렬(Spatial weights matrix)의 Queen contiguity를 통해 격자별 인근 값의 가중합 사용

② 기존 문화시설의 영향 범위(500m 버퍼)를 제외한 문화 취약 격자 집합 도출

③ ①과 ②를 만족하는 문화 인프라 수요지(설치 후보지) 선정

#### - 최적 개수 및 입지 제안
① 후보지 중 Minimum Vertex Cover 알고리즘을 통해 최적 입지 개수 선정

② 최종 입지에 적합한 문화 인프라 선정 및 제안

### 3) 분석 프로세스 흐름도
<img src="https://raw.githubusercontent.com/minzzing/giteuk_plus/main/img/Process.png" width="100%" height="100%"/>

## 3. 데이터 수집
분석을 위하여 아래 데이터를 수집했다.  
① [서울시 활성화 지표](https://city.go.kr/portal/notice/notice/view.do?nttId=7443) - 도시재생종합정보체계  

② [서울시 기초생활 수급자 통계](https://data.seoul.go.kr/dataList/10113/S/2/datasetView.do) - 서울 열린 데이터 광장  
<img src="https://github.com/minzzing/giteuk_plus/blob/main/img/data2.png?raw=true" width="65%" height="65%"/>  

③ [서울시 고령자현황](https://data.seoul.go.kr/dataList/10020/S/2/datasetView.do) - 서울 열린 데이터 광장  
<img src="https://github.com/minzzing/giteuk_plus/blob/main/img/data3.png?raw=true" width="65%" height="65%"/>  

④ [행정구역코드](https://www.mois.go.kr/frt/bbs/type001/commonSelectBoardArticle.do?bbsId=BBSMSTR_000000000052&nttId=78512) - 행정안전부  
<img src="https://github.com/minzzing/giteuk_plus/blob/main/img/data4.png?raw=true" width="65%" height="65%"/>  

⑤ [서울시 문화환경 만족도](https://data.seoul.go.kr/dataList/10305/S/2/datasetView.do) - 서울 열린 데이터 광장
<img src="https://github.com/minzzing/giteuk_plus/blob/main/img/data5.png?raw=true" width="65%" height="65%"/>

⑥. [영등포구 총인구수](http://map.ngii.go.kr/ms/map/NlipMap.do?tabGb=statsMap) - 국토정보맵, 서울특별시 영등포구 총 인구 수 100M 격자(2020.10)  
<img src="https://github.com/minzzing/giteuk_plus/blob/main/img/data6.png?raw=true" width="30%" height="35%"/>

## 4. 데이터 전처리
전처리 : Processing_code 내부 ipynb 참조  
### 전처리 과정
**1) 행정동 코드 통일**  
- 행정동 코드 통일 : 활성화 지표를 기준으로 읍면동명 변경

**2) 활성화 지표 생성**  
- 서울특별시 활성화 지표 추출 : 전국 데이터 정보를 가지고 있는 도시쇠퇴현황에서 서울특별시와 관련된 활성화 지표만 추출  
- 추가 변수 생성 : 국민기초생활보장 수급자, 고령자현황 데이터를 이용하여 비율 변수 생성  
- 변수를 추가한 활성화 지표 생성 : 활성화 지표, 추가 변수, 행정동 코드 병합하여 새로운 활성화 지표 생성

## 5. 활성화 필요지역 선정 - Clustering
활성화 지표를 이용하여 Clustering을 진행, Cluster별 특징을 분석해 활성화가 필요한 지역을 선정

---
### **Clustering**  
Model_code 내부 ipynb 참조  

#### GMM
① 필요 라이브러리 import   
② 군집 개수별 aic, bic를 비교하여 최적의 n 선정  
③ Cluster별 데이터 분포를 분석하여 Target cluster 선정  

#### K-Medoids
① 필요 라이브러리 import  
② Elbow chart를 통해 최적의 n 선정  
③ Cluster 데이터 분포를 분석하여 Target cluster 선정  
#### K-Means
① 필요 라이브러리 import  
② Elbow chart를 통해 최적의 n 선정  
③ Cluster 데이터 분포를 분석하여 Target cluster 선정  
#### Final Target
① 필요 라이브러리 import  
② 3개의 Target cluster에 모두 포함되는 행정동을 활성화 필요 지역으로 선정  
③ 선정된 지역들과 전체 지역의 활성화 지표 특징 추출  
④ 선정된 지역들과 전체 지역의 활성화 지표 특징 비교/분석  

---

<img src="https://github.com/minzzing/giteuk_plus/blob/main/img/clustering.png?raw=true" width="65%" height="65%"/>

 
 ## 6. 문화 취약 지역 선정 및 Target 지역 선정
 
 ### 1) 문화 취약 지역 선정
- 서울시 25개 자치구에 대한 **문화생활 만족도 조사**를 이용, '만족 대비 불만족 비율'인 **개선효용도**를 도출
- **개선효용도**를 통하여 문화 개선이 필요한 자치구 선정
 <img src="https://github.com/minzzing/giteuk_plus/blob/main/img/문화취약지역.jpg?raw=true" width="80%" height="80%" />
 
 ### 2) Target 지역 선정
- 활성화 필요 지역(행정동)과 문화 취약 지역(자치구)에 동시에 해당하는 지역 
<img src="https://github.com/minzzing/giteuk_plus/blob/main/img/타겟지역1.png?raw=true" width="75%" height="75%" />

- 도출된 결과 7개 행정동 중 42%를 차지하는 영등포구의 **신길3동**, **신길4동**, **신길5동**을 Target 지역으로 선정
<img src="https://github.com/minzzing/giteuk_plus/blob/main/img/타겟지역2.png?raw=true" width="60%" height="60%" />


 ## 7. 인프라 선정
 ### 1) 카테고리별 현황 분석
 - 히트맵을 이용하여 Target 지역의 카테고리(문화, 휴식, 체육)별 시설 현황 분석
 - 분석 결과 문화 카테고리가 Target 지역에 부족하다는 것을 확인
<img src="https://github.com/minzzing/giteuk_plus/blob/main/img/heatmap.png?raw=true" width="100%" height="100%" />

 ### 2) 최종 문화 시설 선정
- 문화 카테고리 중 타요소들에 비해 생활 밀집도가 높은 **도서관, 문화센터**를 최종 문화 시설로 선정
- 도보 생활권은 지점에서 걸어서 10분 즉, **500m 반경 내**에 있는 범위를 의미
- 생활 밀접도는 근거리(도보 생활권)에서 자주 이용할 정도로 **생활에 밀접한 관련**이 있다는 것을 의미
- 따라서 생활 밀접도가 높은 시설은 높은 도보 생활권에 있어서 **밀접하게 이용할 수 있는 시설**을 의미

## 8. 수요지 선정
### 1) 가설 설정
수요지 선정을 위하여 아래 두 가지 가설을 만족하는 지역을 수요지 후보로 선정
- 총인구수가 많은 곳이 인프라의 수요가 많을 것임
- 문화 시설의 영향을 받지 못하는 곳이 인프라의 수요가 많을 것임

### 2) 인구 격자 재구성
인구는 한 곳에 머물러 있는 것이 아니라 유동적인 지표이기 때문에 공간가중행렬(Spatial weights matrix)의 Queen contiguity를 이용하여 격자별 인근 값으로 가중합을 구함  

---

#### **공간가중행렬(Spatial weights matrix)**  
Location 내부 spatial weights matrix.ipynb 참조  

① 라이브러리 설치 및 import   
② 가중합 = 기준 격자 값 + 인접한 8개 격자의 평균값(Queen contiguity) 계산  
③ 새로운 인구 격자 생성  

---

- 생성된 격자에서 총인구 상위 지역 격자 선정  
<img src="https://github.com/minzzing/giteuk_plus/blob/main/img/sum_pop.png?raw=true" width="50%" height="50%" />

### 3) 문화시설 현황 분석
- 기존 문화시설로부터 500m 버퍼를 생성해 격자에 적용
- 버퍼에 해당하지 않는 부분을 문화 시설이 없는 곳으로 가정  
<img src="https://github.com/minzzing/giteuk_plus/blob/main/img/문화시설버퍼500.png?raw=true" width="70%" height="70%" />

### 4) 수요 후보지 선정
- 총인구수 상위 지역과 문화 시설이 없는 곳을 수요 후보지로 선정
- 선정된 수요 후보지들 중 신길3, 4, 5동 기준으로 500m 영향권 안에 있는 수요 후보지 추출
<img src="https://github.com/minzzing/giteuk_plus/blob/main/img/최적입지도출.jpg?raw=true" width="70%" height="70%" />

### 5) 최적 입지 선정 - 문화 시설 개수 및 위치 도출
수요 후보지들 중 최적의 입지 선정을 위해 Minimum vertex cover 알고리즘을 이용

---

#### Minimum vertex cover
Location 내부 Vertex_Cover.ipynb 참조  

① 라이브러리 설치 및 import     
② 인접행렬 정의   
③ Minimum vertex cover 알고리즘 적용  
④ 축소된 수요 후보지 도출

---
- Minimum vertex cover 알고리즘을 통해 13개의 수요 후보지를 6개로 축소
- 축소된 6개 중에서 모든 수요 후보지를 포함할 수 있는 3곳을 최종으로 선정
<img src="https://github.com/minzzing/giteuk_plus/blob/main/img/최적입지도출.jpg?raw=true" width="70%" height="70%" />

## 9. 인프라 제안
공공도서관과 국립도서관, 문화센터의 입지 현황을 히트맵으로 파악했을 때 신길3동, 신길4동, 신길5동에 속한 최적 입지 현황 분석 진행
- 현황 분석 결과, 신길3동의 경우 문화센터가 적합하다고 판단하여 문화센터를 제안
- 신길4동, 신길5동의 경우 도서관이 적합하다고 판단하여 도서관을 제안
<img src="https://github.com/minzzing/giteuk_plus/blob/main/img/인프라제안.png?raw=true" width="70%" height="70%" />

