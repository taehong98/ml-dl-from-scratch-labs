# Experiment Log

## Hypothesis
- 유방암 데이터셋에서 **Random Forest**와 **Gradient Boosting**은 모두 높은 정확도를 보이지만,
  학습 방식 차이(배깅 vs 부스팅)로 인해 **정확도와 중요 특성(Top-5 feature)**이 다르게 나타날 수 있다.
- 특히 Boosting은 순차적으로 오차를 보정하므로, 같은 데이터에서도 중요하게 보는 특성이 Random Forest와 일부 달라질 수 있다.

## Setup
- **Dataset**
  - `sklearn.datasets.load_breast_cancer`
  - Features: `data.feature_names` (연속형 특성들)
  - Target: `data.target` (이진 분류)
- **Split**
  - `train_test_split(test_size=0.2, random_state=42)`
- **Models**
  - `RandomForestClassifier()` (기본 하이퍼파라미터)
  - `GradientBoostingClassifier()` (기본 하이퍼파라미터)
- **Metric**
  - Accuracy (`sklearn.metrics.accuracy_score`)
- **Analysis / Visualization**
  - 각 모델의 `feature_importances_` 추출
  - 중요도 내림차순 정렬 후 **상위 5개** 인덱스 선택
  - `seaborn.barplot`으로 Top-5 중요 특성 시각화(2개의 subplot)

## Result
- 두 모델 모두 테스트 데이터에서 Accuracy를 계산하여 출력했다.
  - `🌲 Random Forest 정확도: {rf_acc:.4f}`
  - `🚀 Gradient Boosting 정확도: {gb_acc:.4f}`
- 각 모델별로 중요 특성 Top-5를 막대그래프로 확인하여,
  - 모델에 따라 중요하게 평가하는 특성이 다를 수 있음을 시각적으로 비교했다.
- 결과적으로 **성능(정확도) 비교 + 해석(중요 특성 비교)**를 한 번에 수행하는 기본 실험 파이프라인을 완성했다.
