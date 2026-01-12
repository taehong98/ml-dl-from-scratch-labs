# Experiment Log

## Hypothesis
- `TensorDataset` + `DataLoader(batch_size=32)`로 배치가 정상적으로 생성되고,
  MLP가 각 배치에 대해 `(B, 3)` 형태의 logits를 출력할 것이다.
- `CrossEntropyLoss`로 학습 루프가 에러 없이 돌아가며, 학습 후 accuracy를 계산할 수 있을 것이다.

## Setup
- Data:
  - `X ~ N(0,1)`, shape `(128, 10)`
  - `y ∈ {0,1,2}`, shape `(128,)`
- DataLoader:
  - `batch_size=32`, `shuffle=True`
- Model:
  - MLP: `Linear(10→32) → ReLU → Linear(32→3)`
- Train:
  - Loss: `nn.CrossEntropyLoss()`
  - Optimizer: `Adam(lr=1e-3)`
  - Scheduler: `StepLR(step_size=5, gamma=0.5)`
  - Epochs: `3`
- Eval:
  - `model.eval()` + `torch.no_grad()`
  - `argmax`로 예측 후 accuracy 계산

## Result
- 학습/평가 루프가 정상 실행되었고 `accuracy: <0~1>` 형태로 출력됨.
- 배치 단위 출력 logits은 다중 클래스 분류에 맞게 `(32, 3)` 형태로 생성됨.
- (참고) 데이터가 랜덤이므로 accuracy 값은 실행마다 달라질 수 있음.