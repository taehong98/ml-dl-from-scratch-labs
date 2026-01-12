# Pytorch-Train_Classifier

## What I did
- `TensorDataset` + `DataLoader(batch_size=32, shuffle=True)`로 toy 데이터 배치 로딩을 구성했다.
- `nn.Module` 기반 MLP(Linear→ReLU→Linear)를 정의하고 `CrossEntropyLoss`, `Adam`, `StepLR`를 설정해 3 epoch 학습/평가 루프를 실행했다.

## What I tested
- DataLoader 배치가 정상적으로 생성되고, 모델 출력(logits)이 3-class 분류에 맞는 형태로 나오는지 확인했다.
- `model.train()/model.eval()` 및 `torch.no_grad()` 적용 후 accuracy 계산이 정상 동작하는지 검증했다.

## Artifacts
- Notebook : result/train_mlp_toy_classifier.ipynb
- logs : logs/experiment_log.md
