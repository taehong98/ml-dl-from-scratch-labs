# Randomforest VS Gradienboosting

## What I did
- `load_breast_cancer` 데이터셋을 불러와 `X(DataFrame)`, `y(target)`를 구성했다.
- 데이터를 train/test로 분할했다. (`test_size=0.2`, `random_state=42`)
- 두 앙상블 모델을 학습했다.
  - `RandomForestClassifier`
  - `GradientBoostingClassifier`
- 테스트셋에서 Accuracy로 성능을 평가하고 출력했다.
- 각 모델의 `feature_importances_`에서 상위 5개 특성을 뽑아 막대그래프로 시각화했다(2개 subplot 비교).

## What I tested
- 동일한 데이터/분할 조건에서 Random Forest와 Gradient Boosting의 정확도 차이가 있는지
- 두 모델이 중요하게 보는 Top-5 특성이 어떻게 다른지
- 학습 → 예측 → 정확도 계산 → 중요도 시각화까지 전체 파이프라인이 정상 동작하는지
