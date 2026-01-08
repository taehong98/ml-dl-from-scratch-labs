# Experimen Log
## Hypothesis
- Custom `Dataset`이 (x, y) 한 샘플을 반환하면, `DataLoader(batch_size=2)`는 이를 묶어서
  `x_batch`는 (2, 2), `y_batch`는 (2,) 형태의 배치 텐서를 만들어 줄 것이다.
- `shuffle=False`이므로 배치 순서는 입력 리스트 순서대로 유지될 것이다.

## Setup
- Data:
  - x_list: 4개 샘플, 각 샘플 feature 2개 → shape (4, 2)
  - y_list: 4개 라벨(0/1) → shape (4,)
- Dataset: `FactoryDataset`
  - `x_data = torch.tensor(x_list, dtype=torch.float32)`
  - `y_data = torch.tensor(y_list, dtype=torch.long)`
  - `__getitem__`이 `(x_data[idx], y_data[idx])` 반환
- DataLoader:
  - `batch_size=2`, `shuffle=False`

## Result
- 총 2개의 배치가 생성됨(4 samples / batch_size 2).
- 각 배치에서:
  - `x_batch.shape == (2, 2)`
  - `y_batch.shape == (2,)`
- 첫 번째 배치(`batch_idx == 0`)의 `first_x`, `first_y` shape도 동일하게 `(2, 2)`, `(2,)`로 확인됨.