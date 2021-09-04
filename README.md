#  서울시 문화 불균형해소를 위한 인프라 탐색 - 도시재생 지표를 활용하여

#### 팀 소개
공공 빅데이터 청년 인턴십 프로젝트

[박주원](https://github.com/scppliop) [김명훈](https://github.com/minghoona) [김수현](https://github.com/soohyunme) [신민경](https://github.com/minzzing) [엄현빈](https://github.com/Umhyunbin) [이현지](https://github.com/LocalLeeFarm) [하지민](https://github.com/jimnida)

#### 분석 배경 및 목적
도시재생은 지역의 특색 있는 자원을 활용해 역량과 잠재력을 끌어내는 것을 목표로 한다.   
하지만 도시재생 사업을 지원함에 있어서 지역적 특성을 반영하지 않은 지원 방식이 문제점으로 대두되고 있다.   
본 프로젝트에서는 지역의 특성을 대표하는 중요한 변수이며, 도시재생 패러다임 변화에 따라 중요성이 부각되고 있는 문화의 측면에서 도시재생 사업에 접근하고자 한다.  

목차
----------
1. [Directory](#1-directory)
2. [분석 프로세스](#2-분석-프로세스)
3. [데이터 수집](#3-데이터-수집)
4. [데이터 전처리](4-데이터-전처리)
5. [Clustering](5-clustering)
6. [수요지 선정](6-수요지-선정)
7. [인프라 분석](7-인프라-분석)
8. [최종 입지 선정](8-최종-입지-선정)

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
│ │ └─Population : 총 인구수 격자 데이터 (2020. 10)  
├─Model_code : 클러스터링 코드  
└─Processing_code : 전처리 코드  


## 2. 분석 프로세스
### 1) 지역 선정
① 도시재생 활성화 진단지표를 활용하여 도시재생사업이 필요한 지역을 Clustering 결과비교를 통해 선정

② 문화 생활에 대한 만족도를 통해 '만족 대비 불만족 비율'인 '개선효용도'가 상대적으로 낮은 문화 개선이 필요한 지역을 탐색

③ ①과 ②를 만족하는 분석 대상 지역(행정동) 선정
 
### 2) 인프라 선정 및 입지 선정
#### - 카테고리 선정
① 히트맵을 기반으로 대상 지역의 문화, 휴식, 운동 중 부족한 인프라 파악

② 대분류 인프라의 하위 카테고리 중 생활밀접도를 기반으로 구체적인 문화 인프라 선정

#### - 수요지 선정
① 대상 자치구의 총인구 상위 지역에 해당하는 격자 도출
- 공간가중행렬(Spatial weights matrix)의 Queen contiguity를 통해 격자별 인근 값의 가중합 사용

② 기존 문화시설의 영향 범위(500m 버퍼)를 제외한 문화 취약 격자 집합 도출

③ ①과 ②를 만족하는 문화 인프라 수요지(설치 후보지) 선정

#### - 최적 개수 및 입지 제안
① 후보지 중 Minimum Vertex Cover 알고리즘을 통해 최적 입지 개수 선정

② 최종 입지에 적합한 문화 인프라 선정 및 제안

### 3) 분석 프로세스 흐름도
![분석프로세스](https://user-images.githubusercontent.com/50040550/130420742-92fc76e3-ac7b-4390-b471-e1363995db76.png)

## 3. 데이터 수집
분석을 위하여 아래 데이터를 수집했다.
1. [서울특별시 활성화 지표](https://city.go.kr/portal/notice/notice/view.do?nttId=7443)
2. [서울특별시 기초생활 수급자 통계](https://data.seoul.go.kr/dataList/10113/S/2/datasetView.do)
![2](https://user-images.githubusercontent.com/50914564/132093956-0ccdbd76-c20a-4c3e-bc17-aa1434b4581e.png)
3. [서울특별시 고령자현황](https://data.seoul.go.kr/dataList/10020/S/2/datasetView.do)
![3](https://user-images.githubusercontent.com/50914564/132093953-c5e023e9-46fb-470e-b8c3-1517e6796e3f.png)
4. [행정구역코드](https://www.mois.go.kr/frt/bbs/type001/commonSelectBoardArticle.do?bbsId=BBSMSTR_000000000052&nttId=78512)  
![4](https://user-images.githubusercontent.com/50914564/132094090-ff926f91-0323-4e72-a977-d818fe4aa5ed.png)

## 4. 데이터 전처리
전처리 : Processing_code 내부 ipynb 참조
Clustering : Model_code 내부 ipynb 참조
### 전처리 과정
---
