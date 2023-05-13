# 머신러닝모델 기반 고혈압의 심부전증 진행여부에 대한 과거병력마커 예측
2022.04 ~ 2022.11 (8개월)
## 📗 목차
  - 👨🏻‍💻 담당업무
  - ✍️ 서론
  - 📑 프로젝트 내용
    - 데이터 전처리
    - 모델링
  - 🏆 결과 및 성과
  - 💡 Insight

## 👨🏻‍💻 담당업무
- 팀장 - 팀 프로젝트 진행 관리, 구성 기획 및 업무 분담, 발표
- 분석방법론 설계 및 검증
- EDA
- 데이터 전처리
- 모델링

## ✍️ 서론
- 고혈압의 성인 발병률은 30%로, 성인 10명 중 3명이 고혈압으로 진단된다. 고혈압이 위험한 이유는 합병증을 유발하기 때문인데, 이 중 심부전증은 고혈압 환자에서 정상인보다 3배 높은 발병률을 보인다. 또한 심부전 환자의 생존율은 30~50%정도로 치사율이 높은 질병이다. 따라서 **고혈압 환자의 심부전증 발병을 예방하고자 고혈압 환자의 기존병력 정보를 바탕으로 심부전증 발병 여부를 예측하는 모델을 만들고, 이의 주요 과거병력이 무엇인지 분석**해보았다.
- 미국 중환자실에 입원한 환자들의 전자의료기록을 비식별화한 데이터인 MIMIC-3 데이터를 이용하여 연구를 진행했다.

## 📑 프로젝트 내용
### 1. 데이터 전처리

- 고혈압과 심부전이 차례로 진단받은 그룹 (class=1, n=601)과 고혈압만 진단받은 그룹 (class=0, n=13,080)를 생성
- 각 환자에 주어진 입원 아이디, 이전에 진단받은 질병 리스트, 나이, 성별을 병합
- 모든 feature는 binary 값으로 마킹
  - 과거질병 feature에 대해서 고혈압 전 진단 받은 적이 있으면 1, 아니면 0으로 마킹
	- 성별은 1(남), 0(여)로 마킹
	- 나이는 60세 이상은 1, 아니면 0 으로 마킹
- MCA를 진행한 데이터와 진행하지 않은 original 데이터를 두가지를 사용하여 연구 진행


### 2. 모델링

- 머신러닝 모델(Random forest, AdaBoost, XGBoost)를 이용하여 학습
    - 앞서 나누어둔 고혈압과 심부전을 차례로 진단받은 그룹과 고혈압만 진단받은 그룹의 비율을 맞추기 위해 random sapling후 두 그룹을 merge
    - 위와 같은 과정을 반복하며 보다 정확한 결과를 보기 위해 머신러닝 모델 별 30번의 trained 모델학습 진행 후 결과 확인
    - 위와 같은 과정을 MCA를 적용한 데이터와 original 데이터 모두 적용하여 결과 값 확인
- 세 가지 모델로 두 개의 데이터를 학습한 결과, original 데이터로 학습한 XGBoos의 모델의 성능이 평가지표(Precision, Recall, F-score, AUC)에서 대부분 좋은것을 확인
![image](https://github.com/DOYOON510/Medical-data-analysis/assets/129147977/82e8c33d-39f4-4b78-8fbc-d7ef3df17e0d)

- 위 결과에 따라, 고혈압 환자의 original data를 사용한 XGBoost 모델을 이용하여 심부전증 진행 여부에 대한 과거병력 예측 진행

## 3. 주요 과거질병 분석

- 특성중요도를 사용하여 심부전 발병과 관련된 주요 과거 질병을 확인
    - 심부전증 발병과 관련된 과거 질병의 특성중요도의 값의 평균을 확인해본 결과, 결과는 유의미 함을 확인
    - 고혈압 상태에서 심부전 합병증에 걸린 사람들은 그렇지 않은 사람들보다 5개의 각 과거질병 (급성 심부전, 폐렴, 요로감염, 인슐린 사용, 빈혈)에 더 많이 걸렸던 것으로 확인

![image](https://github.com/DOYOON510/Medical-data-analysis/assets/129147977/518ba08d-8054-4d3a-b8ad-2415d532b350)
![image](https://github.com/DOYOON510/Medical-data-analysis/assets/129147977/0d0626cb-95f1-4a64-a62a-5117dbe7e737)

    
![image](https://github.com/DOYOON510/Medical-data-analysis/assets/129147977/f8320087-2594-4622-9808-4e1bf5099f70)


## 🏆 결과 및 성과
- 교내 포스터발표 진행
- 고혈압 환자의 심부전증을 예측하는 머신러닝 모델 개발
- 고혈압, 심부전증 발병과 관련된 주요 과거 질병을 확인 및 분석

## 💡 Insight
- 모델링을 진행하기 전, 데이터의 특성을 살펴보며 문제점을 확인할 수 있었고, 이를 통해 어떤 변수가 중요하게 작용하는지, 데이터의 특성 이해력을 높일 수 있었음
- 모델링을 진행하며 변수 선택 및 모델 선택의 중요성을 알게되었으며, 모델의 성능을 높이기 위해 고민해야할 요소가 무엇이 있는지 파악하였음
- 범주형 변수 간의 상관관계를 분석하기 위한 MCA 기법에 대한 개념을 익히고, 이를 통해 변수 간의 상관 관계를 파악할 수 있는 분석의 폭을 더욱 넓힐 수 있었음
