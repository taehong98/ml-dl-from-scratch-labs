# Experiment Log — Iris (Logistic Regression / K-Means / PCA)

## Hypothesis
- Iris 데이터는 4개 특성만으로도 **Logistic Regression**이 높은 분류 정확도를 낼 것이다.
- **K-Means(n=3)** 군집은 실제 클래스(y)와 완벽히 일치하진 않아도, **PCA 2D 공간**에서 전반적으로 유사한 분리 패턴을 보일 것이다.

## Setup
- Dataset: `sklearn.datasets.load_iris()`
  - Features `X`: (150, 4)
  - Target `y`: (150,)
- Train/Test split: `train_test_split(X, y, test_size=0.2, random_state=42)`
- Model (Supervised): `LogisticRegression(solver='liblinear', random_state=42)`
  - Train: `model_lr.fit(X_train, y_train)`
  - Predict: `y_pred_lr = model_lr.predict(X_test)`
  - Metric: `accuracy_score(y_test, y_pred_lr)`
- Model (Unsupervised): `KMeans(n_clusters=3, init='k-means++', n_init=10, random_state=42)`
  - Fit on full X: `model_kmeans.fit(X)`
  - Labels: `clusters_kmeans = model_kmeans.labels_`
- Dimensionality reduction: `PCA(n_components=2, random_state=42)`
  - `X_pca = pca.fit_transform(X)`
- Visualization:
  - PCA 산점도 2개 비교
    1) 실제 라벨 `y` 색상
    2) K-Means 라벨 `clusters_kmeans` 색상

## Result
- Logistic Regression:
  - 테스트 데이터에 대한 예측(`y_pred_lr`)을 생성하고 **정확도(Accuracy)** 를 계산함.
  - (코드 실행 결과로 출력된 Accuracy 값이 실험 성능 지표)
- K-Means + PCA 시각화:
  - PCA 2D 공간에서 실제 라벨 분포와 K-Means 군집 분포를 **나란히 비교**하여,
    군집이 클래스 구조를 어느 정도 반영하는지 **정성적으로 확인**함.
- 결론:
  - 지도학습(Logistic Regression)은 수치 지표(Accuracy)로 성능을 확인했고,
  - 비지도학습(K-Means)은 PCA 시각화를 통해 클래스 분리와의 유사성을 비교했다.
