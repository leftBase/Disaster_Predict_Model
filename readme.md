# 📄 README: 건축물 화재 및 침수 위험 분석 머신러닝 모델

이 소스 코드는 **오픈소스**이며, 조영진, 허한결, 현태환. (2024). 우리 집은 화재와 침수로부터 안전한가? - 머신러닝을 활용한 건축물 화재·홍수 위험 분석. auri brief, No.278. 건축공간연구원. 및 몇 가지 참고문헌을 바탕으로 개발된 머신러닝 모델입니다.

---

## 💡 프로젝트 개요

이 프로젝트는 **머신러닝 모델**을 활용하여 지구온난화 변수를 고려한, 건축물의 **화재 및 침수 피해액을 예측**하는 것을 목표로 합니다. 주어진 데이터를 기반으로 학습된 모델은 사용자가 입력한 건축물 정보를 바탕으로 잠재적인 피해액을 산정합니다. 각 모델에서 사용하는 종속변수는 참고문헌에서 피해액과 유의미한 관련이 있는 것을 선정한 것입니다.

---

## 📊 사용된 데이터 및 변수

### 1. 화재 피해 예측 모델

| 구분 | 변수명 | 설명 및 예시 |
| :--- | :--- | :--- |
| **종속 변수 (Target)** | `damage_cost` | 예측하고자 하는 **화재로 인한 피해 비용**입니다. |
| **독립 변수 (Feature)** | `structure` | 건축물 구조 (예: `steel`, `wood`, `concrete`) |
| | `housing_type` | 주거 형태 (예: `apartment`, `villa`, `detached`) |
| | `area` | **연면적** |
| | `approval_year` | **사용 승인 연도** |
| | `floor_area_ratio` | **용적률** |
| | `location` | 지역 (예: `dong1`, `dong2`, `dong3`) |
| | `temperature` | **온도** |
| | `humidity` | **습도** |

### 2. 침수 피해 예측 모델

| 구분 | 변수명 | 설명 및 예시 |
| :--- | :--- | :--- |
| **종속 변수 (Target)** | `flood_damage_cost` | 예측하고자 하는 **침수로 인한 피해 비용**입니다. |
| **독립 변수 (Feature)** | `structure` | 건축물 구조 (예: `steel`, `wood`, `concrete`) |
| | `housing_type` | 주거 형태 (예: `apartment`, `villa`, `detached`) |
| | `land_use` | 토지 이용 (예: `residential`, `commercial`, `industrial`) |
| | `land_area` | **대지면적** |
| | `approval_year` | **사용 승인 연도** |
| | `basement_floors` | **지하층 수** |
| | `slope` | **경사도** |
| | `distance_to_river` | **하천과의 거리** |
| | `elevation` | **고도** |
| | `temperatures` | **온도** |

---

## 🛠️ 머신러닝 모델 및 라이브러리

이 프로젝트에서는 다음 Python 라이브러리 및 머신러닝 모델을 활용합니다:

* **`pandas`**: 데이터 처리 및 분석
* **`numpy`**: 수치 계산
* **`matplotlib.pyplot`, `seaborn`**: 데이터 시각화
* **`scikit-learn` (`sklearn`)**: 머신러닝 모델 구축 및 평가
    * `LinearRegression`: 선형 회귀 모델
    * `DecisionTreeRegressor`: 의사결정 트리 모델
    * `RandomForestRegressor`: **랜덤 포레스트 모델**
    * `OneHotEncoder`: 범주형 변수 **원-핫 인코딩**
    * `StandardScaler`: 데이터 **스케일링**
    * `train_test_split`: 훈련/테스트 데이터 분리

### 모델 선택 및 활용

화재 및 침수 피해 예측을 위해 다중 선형 회귀, 의사결정 트리, 랜덤 포레스트 모델이 훈련되었습니다. 각 모델의 성능은 $R^2$ 점수를 통해 평가됩니다. 가장 점수가 좋은 모델로 예측하게됩니다. 

---

## 🚧 데이터 한계점 및 개선 방향

이 모델은 **무작위로 생성된 샘플 데이터**를 사용하여 개발되었습니다. 따라서 실제 환경에서의 예측 정확도를 높이려면 다음과 같은 개선이 필요합니다:

* **데이터 확보**: **공공데이터 포털**이나 **실제 재난 피해 데이터**를 활용하여 모델의 학습 데이터를 강화해야 합니다.
* **실측 데이터 활용**: 특정 지역의 건축물 및 환경 관련 **실측 데이터**를 사용하면 모델의 지역별 특성 반영 능력을 향상시킬 수 있습니다.
* **사용성 강화**: 사용자 인터페이스를 개선하거나, 더 다양한 입력 방식을 지원하여 사용자가 쉽게 모델을 활용할 수 있도록 할 수 있습니다.

---

## 🚀 사용법

1. 순서대로 셀을 실행하면 서울시 평균 기온 데이터인 tmp.csv를 현재 작업 경로에서 찾아 읽고, 사용자의 현재 연도, 나중 연도를 입력 받아 기온 상승값인 rise를 계산/출력한다.
   <img width="1815" height="1190" alt="image" src="https://github.com/user-attachments/assets/583ec689-723d-4263-94f3-2a31457beb6f" />

2. 샘플 데이터를 생성한뒤 머신러닝 모델을 학습시켜 모델 성능을 평가하고 선택한다. (이 코드에선 모의 데이터로 고정 시드로 랜덤 생성된 값을 사용하기때문에 랜덤 포레스트 모델이 침수 피해액과 홍수 피해액 계산 모델에서 사용된다.)
<img width="2276" height="1729" alt="image" src="https://github.com/user-attachments/assets/539a6bdb-f44f-4069-a702-4556e1050ee6" />
<img width="2095" height="1516" alt="image" src="https://github.com/user-attachments/assets/d99c9762-0377-4af1-8a27-55a1ae9399df" />

3. 마지막 셀을 실행 한 뒤 침수 피해액과 홍수 피해액 중 하나를 고르고 입력해야할 값을 차례로 입력하면 예상 피해액이 산출된다.
<img width="1510" height="139" alt="image" src="https://github.com/user-attachments/assets/b5763b8e-7c54-44a3-ac27-d8acedcd112d" />
<img width="1573" height="133" alt="image" src="https://github.com/user-attachments/assets/543ae4f5-1611-4d72-82fb-248124f17e11" />
<img width="1342" height="583" alt="image" src="https://github.com/user-attachments/assets/765fd8da-7038-4c86-9e65-7b1f4c9ee4db" />



---

## 📜 라이선스

**MIT License**


