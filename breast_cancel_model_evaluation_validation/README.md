# breast_cancel_model_evaluation_validation

## What I did
- `load_breast_cancer` 데이터셋을 불러오고 train/test(80/20)로 분리했다.
- 기본 `RandomForestClassifier(random_state=42)`를 학습하고 테스트 예측을 생성했다.
- `GridSearchCV(cv=5, scoring='f1')`로 하이퍼파라미터(`n_estimators`, `max_depth`, `min_samples_split`)를 탐색해 최적 모델을 얻었다.
- 기본 모델 vs 최적 모델을 `Accuracy / Precision / Recall / F1-Score`로 평가해 표로 정리했다.
- 두 모델의 성능을 그룹 막대그래프로 시각화했다.
- 최적 모델의 `feature_importances_`를 계산해 특성 중요도 막대그래프로 시각화했다.

## What I tested
- 기본 RandomForest 대비 GridSearchCV 튜닝(RandomForest)이 F1-score 중심으로 성능을 개선하는지
- 하이퍼파라미터 조합 변화가 Accuracy/Precision/Recall/F1에 어떤 영향을 주는지
- 최적 모델에서 중요한 특성이 무엇인지(`feature_importances_`)로 해석 가능한지

## Files
- 'result/' : 출력 결과
- 'log/' : 실험 로그