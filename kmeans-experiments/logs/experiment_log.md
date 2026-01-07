# Experiment Log

## Hypothesis
- k를 늘리면 inertia는 감소하지만, 어느 지점부터는 감소 폭이 급격히 줄어드는 "elbow"가 나타날 것이다.
- elbow 지점의 k를 선택하면 과도하게 많은 군집을 쓰지 않으면서도 데이터 구조를 충분히 설명하는 군집화를 얻을 수 있다.

## Setup
- Data:
  - make_blobs(n_samples=300, centers=5, cluster_std=0.60, random_state=42)
  - Feature dimension: 2 (X[:,0], X[:,1])
- Model:
  - KMeans (sklearn)
  - random_state=42, n_init=10
- Sweep:
  - k_range = 1..10
  - For each k: fit(X) and record inertia (kmeans.inertia_)
- Evaluation:
  - Metric: inertia (within-cluster sum of squares, WCSS)
  - Selection rule: elbow point from inertia-vs-k curve (visual inspection)
- Final run:
  - optimal_k = 3
  - Fit KMeans(n_clusters=3) and predict labels (fit_predict)
- Output:
  - Plot 1: inertia vs k (elbow curve)
  - Plot 2: scatter plot of X colored by predicted cluster

## Result
- Inertia decreased monotonically as k increased (expected).
- The elbow appeared around k = 3 (visual), so optimal_k was set to 3.
- With k=3, points were separated into 3 clusters in 2D scatter visualization.
