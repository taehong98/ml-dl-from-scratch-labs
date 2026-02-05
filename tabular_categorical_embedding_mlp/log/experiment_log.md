# Experiment Log — Tabular Categorical Embedding + MLP (PyTorch)

## Hypothesis
- 범주형 테이블 데이터는 **컬럼별 Embedding으로 의미 있는 연속 벡터 표현**을 학습할 수 있고,
  이를 **concat 후 MLP**에 넣으면 다중분류(`output`)에서 합리적인 성능을 낼 수 있다.
- `BatchNorm + Dropout`을 포함한 MLP는 과적합을 완화하고 학습을 안정화할 수 있다.

## Setup
- **Data / Features**
  - Categorical columns: `price, maint, doors, persons, lug_capacity, safety`
  - 각 컬럼을 `astype('category')`로 변환 후 `cat.codes`로 정수 인코딩
  - 입력 텐서: `categorical_data = stack([col_codes...], axis=1)` → shape `(N, 6)`
- **Target**
  - `output`을 `pd.get_dummies()`로 원-핫 변환 후 텐서로 변환
  - 학습/평가 시 `CrossEntropyLoss`를 사용하기 위해 `dtype=int64`로 라벨 텐서 준비
- **Split**
  - 총 `1728`개 중 `20%`를 테스트로 분리 (앞 80% train / 뒤 20% test)
- **Model**
  - 컬럼별 임베딩: `Embedding(ni, nf)` 를 컬럼 수(6개)만큼 생성
  - 임베딩 크기 규칙: `nf = min(50, (ni+1)//2)`
  - Forward: 각 컬럼 임베딩 → `concat(dim=1)` → `Dropout(p=0.4)` → MLP
  - MLP 구조: `[200, 100, 50]` hidden + `ReLU + BatchNorm1d + Dropout(p=0.4)` 반복
  - Output layer: `Linear(50, 4)` (클래스 4개)
- **Training**
  - Loss: `nn.CrossEntropyLoss()`
  - Optimizer: `Adam(lr=0.001)`
  - Epochs: `500`
  - 학습 중 25 epoch 간격으로 loss 출력
- **Evaluation**
  - Test loss 측정 (no_grad)
  - 예측: `argmax(logits)`
  - Metrics: `confusion_matrix`, `classification_report`, `accuracy_score`

## Result
- 학습 루프가 정상적으로 동작하며 **훈련 loss가 감소**하는지 로그로 확인 가능(25 epoch 간격 출력).
- 테스트 구간에서 `Loss`, `confusion_matrix`, `classification_report`, `accuracy`를 출력하여
  **다중분류 성능을 정량적으로 확인**했다.
- (수치 결과는 실행 환경/랜덤 시드/데이터 전처리 상태에 따라 달라지므로)
  본 실험의 성공 기준은 아래를 만족하는 것으로 정의:
  - Train loss가 초기 대비 유의미하게 감소
  - Test accuracy가 랜덤 추정보다 충분히 높음(클래스 4개 기준 baseline ≈ 0.25 이상)
  - Confusion matrix에서 특정 클래스에만 쏠리지 않고 예측이 분산됨
