# Experiment Log

## Hypothesis
- `Class`, `Weapon`, `ElementCode`처럼 **범주형 특성(숫자 코드 포함)**을 원-핫 인코딩으로 수치화하면 `LinearRegression`이 학습/예측을 수행할 수 있다.
- train/test를 합쳐서 더미 컬럼을 만들면, test에 없는 범주(예: `ElementCode=3`)가 있어도 **컬럼 불일치 문제 없이** 안정적으로 예측할 수 있다.

## Setup
- **Data**
  - **Train**: `Level`, `Class`, `Weapon`, `ElementCode` → target: `CombatPower`
  - **Test**: `Level`, `Class`, `Weapon`, `ElementCode` (단, `ElementCode=3` 범주는 없음)
- **Preprocessing**
  - train/test에 `source` 컬럼 추가 후 `concat`으로 결합
  - `pd.get_dummies(columns=['Class','Weapon','ElementCode'], drop_first=True)` 적용
  - 인코딩 후 `source` 기준으로 train/test 재분리
- **Model**
  - `LinearRegression()` 학습: `X_train`(타깃 제외), `y_train`(`CombatPower`)
  - `X_test`에 대해 `predict` 수행

## Result
- 원-핫 인코딩 후 train/test가 **동일한 입력 컬럼 구조**를 가지도록 정렬되었다.
- test에 존재하지 않는 범주(예: `ElementCode=3`)는 더미 컬럼은 유지되되 값이 0으로 들어가 **입력 차원 불일치 없이** 예측이 가능했다.
- 출력으로 test 샘플(3개)에 대한 `CombatPower` 예측값 `y_pred`가 배열 형태로 생성되었다.
