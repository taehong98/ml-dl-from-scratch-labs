# Experiment Log

## Hypothesis
- RGB 이미지를 픽셀 단위 데이터로 펼친 뒤 `MiniBatchKMeans`로 **K개의 대표 색상(centroids)**을 학습하면,
  모든 픽셀을 해당 대표 색상으로 치환하여 **색상 수가 K개로 제한된(양자화된) 이미지**를 만들 수 있다.
- `K`가 작을수록 색상이 더 단순해져 정보 손실이 커지고, `K`가 클수록 원본과 더 비슷한 결과가 나온다.

## Setup
- **Input**
  - `/content/samples.image.webp`를 `RGB`로 로드 후 `np.array(img) / 255.0`로 정규화
  - 로드 실패 시 `np.random.rand(200, 200, 3)`로 더미 이미지 생성
- **Preprocessing**
  - 이미지 shape: `(w, h, 3)`
  - 픽셀 데이터를 `img_np.reshape(-1, 3)`로 변환하여 `(w*h, 3)` 형태로 구성
- **Model**
  - `MiniBatchKMeans(n_clusters=K, random_state=42)`
  - `labels = fit_predict(pixel_data)`로 각 픽셀의 클러스터 라벨 할당
  - `centers = cluster_centers_`로 대표 색상(centroids) 추출
- **Reconstruction**
  - `quantized_pixel_data = centers[labels]`로 픽셀 색상 치환
  - `quantized_img = quantized_pixel_data.reshape(w, h, 3)`로 이미지 복원
- **Visualization**
  - 원본 이미지 vs 양자화 이미지 subplot 비교
  - `centers`를 팔레트 형태로 시각화

## Result
- 이미지가 `(w, h, 3)` 형태로 정상 로드(또는 더미 생성)되었고, 픽셀 데이터를 `(w*h, 3)`으로 변환했다.
- `MiniBatchKMeans`가 추출한 `K`개의 대표 색상으로 모든 픽셀을 치환하여 **양자화 이미지**를 생성했다.
- 시각화 결과:
  - 원본 대비 양자화 이미지는 **색상이 단순화**되어 유사한 색상들이 대표 색상으로 묶였다.
  - 팔레트 출력에서 **대표 색상 K개**가 확인되었다.
- `K` 값에 따라 단순화 정도(정보 손실)가 달라지는 것을 확인했다.