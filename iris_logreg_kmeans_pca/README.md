# Iris ML 미니 실습 (Logistic Regression + K-Means + PCA)

## What I did
- `sklearn.datasets`의 Iris 데이터를 로드하여 `X(특성)`, `y(정답 라벨)` 구성
- `train_test_split`으로 학습/테스트 데이터 분할 (test_size=0.2, random_state=42)
- **Logistic Regression** 모델 생성 및 학습 (`solver='liblinear'`)
- 테스트 데이터로 예측 수행 후 **정확도(Accuracy)** 계산
- 전체 데이터 `X`에 대해 **K-Means** 군집화 수행 (n_clusters=3, k-means++)
- **PCA(2차원)** 로 차원 축소하여 시각화용 좌표 생성
- PCA 공간에서
  - 실제 라벨(`y`) 기준 산점도(지도학습 관점)
  - K-Means 군집 라벨 기준 산점도(비지도학습 관점)
  를 나란히 비교 시각화

## What I tested
- Logistic Regression이 Iris 분류에서 **얼마나 잘 맞추는지(Accuracy)** 확인
- K-Means 군집 결과가 실제 클래스 구조(`y`)와 **얼마나 유사하게 분리되는지** 시각적으로 비교
- PCA로 2차원으로 줄였을 때도 클래스/군집의 **분리 경향이 유지되는지** 확인

## Files
- 'result/' : 출력 결과
- 'log/' : 실험 로그