# Experiment Log

## Hypothesis
- Breast Cancer 데이터셋에서 `RandomForestClassifier`는 기본 설정만으로도 높은 성능을 내지만,
  `GridSearchCV`로 하이퍼파라미터(`n_estimators`, `max_depth`, `min_samples_split`)를 튜닝하면
  **F1-score를 중심으로 성능이 개선**될 수 있다.
- 최적화된 RandomForest의 `feature_importances_`를 통해 **예측에 크게 기여하는 핵심 특성**을 확인할 수 있다.

## Setup
- **Dataset**
  - `sklearn.datasets.load_breast_cancer`
  - Features: `X = data.data`, Target: `y = data.target` (이진 분류)
- **Split**
  - `train_test_split(test_size=0.2, random_state=42)` (train 80%, test 20%)
- **Baseline Model (Default)**
  - `RandomForestClassifier(random_state=42)`
  - Train: `fit(X_train, y_train)`
  - Test prediction: `y_pred_default = predict(X_test)`
- **Hyperparameter Search**
  - `param_grid`:
    - `n_estimators`: [50, 100, 200]
    - `max_depth`: [None, 10, 20]
    - `min_samples_split`: [2, 5, 10]
  - `GridSearchCV`:
    - Estimator: `RandomForestClassifier(random_state=42)`
    - `cv=5`
    - `scoring='f1'`
    - `n_jobs=-1`
  - Best model: `best_model = grid_search.best_estimator_`
  - Test prediction: `y_pred_optimized = best_model.predict(X_test)`
- **Evaluation Metrics**
  - `Accuracy`, `Precision`, `Recall`, `F1-Score`
  - `performance_df`로 기본 모델 vs 최적 모델 비교
  - 성능 비교 grouped bar chart 시각화
- **Model Interpretation**
  - `best_model.feature_importances_` 추출
  - 특성명(`data.feature_names`)과 결합 후 내림차순 정렬
  - Feature importance bar chart 시각화

## Result
- 기본 RandomForest와 GridSearchCV로 튜닝된 RandomForest의 테스트 성능을
  `Accuracy / Precision / Recall / F1-Score`로 정리하여 비교했다(`performance_df`).
- `scoring='f1'` 기반 탐색을 통해 **F1-score 관점에서 더 적합한 하이퍼파라미터 조합**을 찾고,
  최적 모델(`best_estimator_`)을 얻었다.
- 성능 비교 막대그래프를 통해 두 모델의 지표 차이를 시각적으로 확인했다.
- 최적 모델의 `feature_importances_`를 시각화하여,
  **예측에 가장 크게 기여하는 특성들이 무엇인지** 확인했다.