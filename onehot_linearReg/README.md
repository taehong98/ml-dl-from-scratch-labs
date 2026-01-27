# Onehot encoding and LinearRegression

## What I did
- train/test 데이터를 만들고 `Class`, `Weapon`, `ElementCode`(숫자지만 범주형)을 포함시켰다.
- train/test를 합친 뒤 `pd.get_dummies`로 원-핫 인코딩했다.
- 다시 train/test로 분리해서 `LinearRegression`으로 `CombatPower`를 학습/예측했다.

## What I tested
- 범주형 변수를 원-핫 인코딩하면 선형회귀로 학습/예측이 되는지
- test에 없는 범주가 있어도(예: `ElementCode=3` 없음) 컬럼 불일치 없이 처리되는지

