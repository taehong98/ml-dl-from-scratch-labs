# Tabular Categorical Embedding + MLP (PyTorch)

## What I did
- 범주형 컬럼(`price, maint, doors, persons, lug_capacity, safety`)을 `category` 타입으로 변환하고 `cat.codes`로 정수 인코딩
- 타겟(`output`)을 원-핫 인코딩 후 텐서로 변환(다중분류 라벨 준비)
- 각 컬럼별 카테고리 개수로 `Embedding (num_categories → embed_dim)` 크기 자동 설정
- 컬럼별 임베딩 벡터를 생성 → `concat` → `Dropout` → `MLP(Linear + ReLU + BatchNorm + Dropout)`로 분류 모델 구현
- Loss: `CrossEntropyLoss`, Optimizer: `Adam`으로 학습 루프 구성(500 epochs)
- 테스트 셋에서 loss 계산 및 `confusion_matrix / classification_report / accuracy`로 성능 평가

## What I tested
- 범주형 테이블 데이터를 **컬럼별 Embedding으로 벡터화**한 뒤 **concat + MLP**로 다중분류가 제대로 학습되는지 확인
- 임베딩 차원 설정(`min(50, (col_size+1)//2)`)이 모델 학습에 문제 없는지 확인
- Dropout, BatchNorm을 포함한 MLP 구조가 loss 감소 및 일반화에 도움이 되는지 확인
- 최종적으로 테스트 셋에서 정확도/분류 리포트/혼동행렬이 합리적으로 나오는지 확인

## Files
- 'result/' : 출력 결과
- 'log/' : 실험 로그
