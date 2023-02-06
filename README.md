## 신용카드 사기 거래 탐지 AI 경진대회

###### 진행기간: 2022.07.01 ~ 2022.08.05

###### 대회 설명:
- 신용카드 사기 거래 여부가 미확인된 방대한 데이터를 바탕으로, 사기 거래를 탐지할 수 있는 AI 모델(Unsupervised Anomaly Detection) 개발
- URL: https://dacon.io/competitions/official/235930/overview/description

###### 대회 목적: 
- Feature 30개를 이용한 비지도 학습으로 사기 거래 여부를 예측하는 AI모델 개발
- macro-f1 score를 통해 모델 성능을 평가하고 다양한 방법을 통해 모델 성능 개선을 목표로 설정

###### 대회 결과: 
- MCD모델을 바탕으로 Unsupervised Data를 Semi Supervised데이터로 변경한 후, 머신러닝 모델을 사용하여 과업 수행
- 🏆 대회 최종 2등 달성(Private 기준 3등)

-------------------------------------------------------------
###### 프로젝트 환경: Google Colab

###### 팀구성 및 역할: 
- 총원: 2명
- 역할:
1. 데이터 분석
2. 모델 개발
    - AutoEncoder, iforest, pca, mcd, sod 등 다양한 모델 테스트 진행
    - mcd모델을 바탕으로 Unsupervised 데이터 라벨링
    - 위 데이터를 바탕으로 Classification 모델 앙상블(Logistic Regression, CatBoost) 수행

#### 상세 과정:
###### 1. 데이터 분석
- 모든 데이터의 Feature은 비식별 되어 있어 파생변수 생성하기 어려움
- 정상과 비정상의 비율 차이가 큼 (비정상 비율: 0.001055%)
- 각 Feature별로 IQR을 벗어나는 이상치 다수 발견 ⇒ 대회 특성상, 비정상 구별에 중요한 역할을 할 것이라 판단하여 제거하지 않음

###### 2. 문제 접근 방식
- 일반적인 비지도 학습으로 진행한 결과, 만족스러운 결과를 얻지 못함
- 따라서 Validation Target의 통계값을 이용하여 제일 성능이 높은 비지도 학습 모델을 바탕으로 Train의 Target을 생성 ⇒ 일반적인 분류 모델로 변경
- Train의 Traget값을 바탕으로 Classification을 진행

###### 3. 모델 구축
- Train의 Target 생성
- Train의 Target 바탕으로한 Classification모델

###### 4. 성능 향상을 위한 기법
- 1차 처리 방식에서 Train Data 이상치 120개라고 판단 
  - 120±5로 최적값 118개로 지정
- Test Set에 Validation 비정상 비율을 적용하면 성능 하락
  - 평가지표 macro-f1이기 때문에 비정상 데이터를 잘 찾는 것이 중요
  - Validation 비율 2~2.5배를 적용하여 보다 비정상 데이터를 잘 찾게 구성
- Test Set을 예측할 때, 각 모델 확률값 중 K개만 비정상으로 Labeling
  - 모델마다 최적의 K값 적용
- 모델 앙상블
  - 두 모델 모두 비정상이라 판단한 데이터만 최종적으로 비정상이라 판단


