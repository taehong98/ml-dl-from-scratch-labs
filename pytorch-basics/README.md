# Pytorch-basics

## what i did
- FactoryDataset(Dataset) 클래스를 만들어 입력 x_list와 라벨 y_list를 PyTorch 텐서로 변환했다. (x: float32, y: long)
- __len__, __getitem__을 구현해 (x, y) 샘플을 인덱스로 반환하도록 구성했다.
- DataLoader(dataset, batch_size=2, shuffle=False)로 데이터를 배치 단위로 로딩했다.
- DataLoader를 순회하면서 각 배치의 값과 shape를 출력하고, 첫 번째 배치를 따로 저장해 배치 형태가 기대와 일치하는지 확인했다.

## what i tested
-  Custom Dataset이 (x, y)를 반환할 때 DataLoader가 batch_size=2 기준으로 x_batch, y_batch를 어떻게 묶는지(shape 포함) 확인했다

## Artifacts
- notebook : factory_dataset.ipynb
- logs : logs/experimen_log.md