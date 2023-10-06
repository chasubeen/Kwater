# **💧2023년 K-water 대국민 물 빅데이터 공모전💧**
🔗 [모집요강](https://www.water.or.kr/kor/board/index.do?mode=view&bid=BD_00017&menuId=17_189&wid=110185)

## **0. 대회 소개**
- 물 관련 데이터 활용 확대 및 물 분야 현안해결을 위한 창의적 아이디어·신규 비즈니스 모델 발굴

## **1. 참여 분야**
- **데이터 융합** 분야
  - 사회 현안 해결을 위한 데이터 분석 아이디어 및 분석 결과

## **2. 참여자**
|**팀장**|**팀원 1**|**팀원 2**|
|:----------:|:----------:|:----------:|
|<img src="https://github.com/chasubeen/Kwater/assets/98953721/7e911a02-df0e-49f9-a6ae-f787819661cd" width = 150 height = 150>|<img src = "https://github.com/chasubeen/Kwater/assets/98953721/0a7f6fbf-9ed6-438b-a934-e1d7513e2606" width = 150 height = 150>|<img src = "https://github.com/chasubeen/Kwater/assets/98953721/09833b53-66be-4e28-947d-143f34a83884" width = 150 height = 150>|
|[차수빈](https://github.com/chasubeen)|[배주원](https://github.com/baejuwon-30)|[박신영](https://github.com/D-dior)|

## **3. 진행 과정**
- **기간**: 2023.07.08(토) ~ 2023.08.22(화)  
- **세부 일정**  
<img src = "https://github.com/chasubeen/Kwater/assets/98953721/a02b6601-610a-4416-af05-10ece6cc698d" width = 600 height = 350>

   
- **역할**  
  
|**이름**|**역할**|
|:-----:|:----------:|
|차수빈|데이터 수집&전처리&병합 / EDA / 군집분석(그룹 2,4) / 모델링(AutoML, 그룹 2,4) / 대시보드 제작(tableau) / 보고서 작성|
|배주원|데이터 수집&전처리&병합 / EDA / 군집분석(그룹 1) / 모델링(그룹 1) / 보고서 작성&정리|
|박신영|데이터 수집&전처리&병합 / EDA / 군집분석(그룹 3) / 모델링(그룹 3) / 보고서 작성&정리|

- **개발 프로세스**
<img src = "https://github.com/chasubeen/Kwater/assets/98953721/de4fcfc1-a115-4886-816b-eb25105351b2" width = 850 height = 500>

---
## **4. 과제 목표**
- 다목적 댐의 상태 점검과 기능 확인을 위한 머신러닝 기반 모델 개발  
  - 댐에 대한 여러 정보를 통해 댐의 (현재) 저수량을 예측 -> 댐의 활용 능력 계산  
  - 댐의 활용능력과 수질 상태를 종합적으로 고려하여 각 댐의 현황을 파악  
=> 댐 상태에 대한 신속한 평가 + 이상 상황 모니터링  

## **5. 디렉토리 구조**
```
├── Kwater
|   ├── 원본 데이터(private)
│   ├── data_merge.ipynb(데이터 가공, 병합)
│   ├── final.csv(수문정보/제원정보/기상자료 가공 이후 데이터셋)
│   ├── quality.csv(수질정보 가공 이후 데이터셋)
│   ├── EDA_Clustering.ipynb(EDA, 군집분석)
│   ├── data(각 그룹별로 모델링을 하기 위한 train/test 데이터셋)
│   │   ├── train_group1.csv
│   │   ├── train_group2.csv
│   │   ├── train_group3.csv
│   │   ├── train_group4.csv
│   │   ├── test_group1.csv
│   │   ├── test_group2.csv
│   │   ├── test_group3.csv
│   │   └── test_group4.csv
|   ├── AutoML.ipynb(최적화 모델 선정을 위한 모델링 자동화)
|   ├── Modeling.ipynb(그룹별 최종 모델링 및 저수량 예측)
│   └── README.md
```

## **6. Data Description**
- 데이터 시점: 2019.01.01 ~ 2022.12.31
  - 데이터는 주로 일 단위(수질 데이터는 월 단위)
- 데이터 수집/가공 후 하나의 ```csv``` 파일로 가공
- 성격과 목적에 맞게 **4가지**로 분류

### **1) 수문자료**
- ```강우량```, ```유입량```, ```방류량```, ```(현재)저수량```, ```저수율(%)```을 수집
- 결측치 처리
  - 강우량: 해당 연도 -> 해당 월의 최빈값으로 대체
    
### **2) 제원 정보**
- 다목적댐 21곳의 ```총저수량```, ```유효저수량```, ```홍수조절용량```, ```비활용용량```을 수집
- 저수지 용량 배분에 따라 ```이수용량```을 계산(파생 변수)
  
### **3) 기상자료**
- 다목적댐이 위치한 지역 혹은 인근 지역의 ```평균습도```, ```평균기온```, ```평균풍속```, ```합계일사량```을 수집
  
### **4) 수질자료**
- 월별로 10가지 검사항목을 수집 -> 호소의 생활 환경기준에 따라 7개 등급으로 분류
  - 등급 산정이 어려운 경우 ```총유기탄소량(TOC)```만을 사용하여 등급을 결정
- 특정 월의 데이터가 모두 결측치인 경우 해당 댐의 등급 최빈값으로 대체

## **7. EDA(데이터 탐색)**
- 학습용 데이터에 대해 수행
### **⊙ target 변수**(저수량, ```reserve_qy```)
- 각 댐 내에서는 저수량이 대부분 일정하게 유지되는 것을 확인
  - 기술통계량, 왜도 -> 낮은 비대칭성
- 댐별로는 평균 저수량에 큰 차이가 있음을 확인(스케일 차이)
  - 연도별/계절별로 특징적인 모습을 보임 -> 연도(```year```)와 계절(```season```)을 파생 변수로 생성
### **⊙ feature 변수**
- 댐별로 각 변수의 분포, 계절별 분포, 연도별 분포를 분석
- 기술통계량, 왜도 파악
  - 왜도가 큰 변수들: 강우량(```rain_qy```), 유입량(```inflow_qy```), 방류량(```outflow_qy```)
     

➕ [태블로 시각화](https://public.tableau.com/views/K-WaterDashboard/sheet3?:language=ko-KR&:display_count=n&:origin=viz_share_link)

## **8. 군집분석(+ 추가적인 전처리)**
- EDA 결과 다목적 댐 21개소를 유사한 특징을 가지는 그룹으로 군집화
  - ```KMeans``` 알고리즘 활용
  - KMeans 알고리즘은 이상치에 민감하게 반응하기에 이상치 제거 후 진행
- 최적 군집 개수 설정을 위해 ```Elbow Method```를 활용하여 2 ~ 5개 군집화 결과를 비교
  - **4개**를 최적 군집 개수로 선택

- 군집분석 결과
  ```
  - group 1: 군위, 김천부항, 남강, 밀양 등 12개소
  - group 2: 소양강, 충주
  - group 3: 섬진강, 용담, 임하, 주암(본댐), 합천
  - group 4: 대청, 안동
  ```
  
- 군집마다 **고유한** 데이터 특징을 확인할 수 있음
  - 각 그룹의 차이를 최대한 유지하기 위해 **군집별**로 전처리를 다르게 진행
    - 로그 변환: 변수들이 왜곡된 경우(= 왜도가 1 이상인 경우) 수행
    - 스케일링: 이상치에 영향을 덜 받는 ```RobustScaler```를 적용
    - 범주형 변수: ```One-hot Encoding``` 적용

## **9. 모델링(회귀 분석)**
### **⊙ 모델링을 위한 알고리즘 선택**  
- AutoML 기법 중 하나인 ```PyCaret```을 통해 다양한 회귀 알고리즘의 성능을 개략적으로 평가  
=> 평균 제곱근 오차(RMSE)를 기준으로 ```RandomForestRegressor```, ```CatBoostRegressor```, ```XGBRegressor```, ```ExtraTreesRegressor```, ```LGBMRegressor```을 최종 알고리즘으로 선택

### **⊙ (현재) 저수량 예측을 위한 모델링**
- 위에서 선택된 **5개**의 알고리즘을 활용해 각 그룹에 대해 모델링을 진행
  - 평가 지표: RMSE, Adjusted R-Square
  - 기본 모델 생성 후 하이퍼 파라미터 튜닝을 통해 모델 성능 최적화 시도
- 최적 모델 1개를 예측을 위한 모델로 선택

### **⊙ 예측 결과 얻기**
- 최적 모델 선택  
  => 공통적으로 ```ExtraTreesRegressor```의 성능이 가장 좋음을 확인할 수 있음
  - group 1: ```ExtraTreesRegressor``` 기본 모델
  - group 2: 하이퍼 파라미터 튜닝된 ```ExtraTreesRegressor``` 모델
  - group 3: ```ExtraTreesRegressor``` 기본 모델
  - group 4: ```ExtraTreesRegressor``` 기본 모델
  
- 최적 모델로 테스트 데이터에 대한 예측 수행
  - 각 댐의 (현재) 저수량을 예측
  - 예측된 저수량을 통해 각 댐의 활용 능력 계산

### **⊙ 활용 능력 계산**
- (최대) 이수 용량에 대한 활용 가능 용량의 비율을 계산
  - 각 댐마다 (최대) 이수용량에 비해 **실제로** 물을 얼마나 활용할 수 있는지를 산정

<img src = "https://github.com/chasubeen/Kwater/assets/98953721/1583aab6-a0a8-48c7-a935-2d83f20d9a69" width = 400 height = 250>

- 평가 산식  
  <img src = "https://github.com/chasubeen/Kwater/assets/98953721/a085bb22-dd26-4ccb-bffe-6ac23236145e" width = 500 height = 70>

- 변수 설명
```
- tot_qy: 총저수량
- valid_qy: 유효저수용량
- flood_qy: 홍수조절용량
- unused_qy: 비활용용량
- usable_qy: 활용 가능 용량
- maximum_use_qy: 이수용량
- efficiency: 활용 능력
```

## **10. 결과 정리**
- 예측된 (현재) 저수량 + 수질 등급 + 활용 능력을 복합적으로 평가한 후 21개의 다목적 댐을 다시 5개의 그룹으로 분류
  - 각 그룹의 현 상황을 분석하고, 각각에 맞는 솔루션 제시  
    
※ 자세한 내용은 [결과보고서](https://github.com/chasubeen/Kwater/blob/main/2023%EB%85%84%20K-water%20%EB%8C%80%EA%B5%AD%EB%AF%BC%20%EB%AC%BC%20%EB%B9%85%EB%8D%B0%EC%9D%B4%ED%84%B0%20%EA%B3%B5%EB%AA%A8%EC%A0%84%20%EC%88%98%ED%96%89%20%EA%B2%B0%EA%B3%BC%EB%B3%B4%EA%B3%A0%EC%84%9C.pdf)를 참고 바람

## **11. 기대 효과**
- 그룹 별로 처한 상황은 다르지만, 모델링 결과를 바탕으로 추후 댐의 관리 방향을 설정하는 데 중요한 지침을 얻을 수 있음
  - 지속적인 발전과 효율적인 자원 활용 가능
---
## **회고**


