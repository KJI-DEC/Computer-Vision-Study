# StyleCLIP: Text-Driven Manipulation of StyleGAN Imagery

[논문](https://arxiv.org/abs/2103.17249)

### Overview

- `StyleGAN` + `CLIP`
- image manipulation

### StyleCLIP

StyleGAN + CLIP?

- Latent Optimization: StyleGAN의 W+ space와 CLIP의 space를 비교하여 loss를 최소화하도록 최적화. source image와 text prompt pair에 대해 source image latent vector를 CLIP text vector값과의 loss가 작아지게 최적화 진행. 하지만 input마다 행해야 함
- Local Mapper: 특정 text prompt에 대한 mapping network train. mapping network 학습은 오래 걸리나, text prompt에 대해 한 번만 학습하면 됨. 하지만 완전 다른 얼굴 이미지라도 비슷하게 manipulation되는 경우가 많음
- Global Direction: global latent space에 text mapping. global direction은 StyleGAN의 style space S로부터 계산된 하나의 모델로 모든 매핑을 수행함. text 전후 imbedding 차이값이 style 전후 차이값에 매핑되도록 하려는 것. 스타일 변화의 정도는 alpha로!

- StyleGAN, CLIP 모두에 의존 → 둘 중 하나라도 pretrained model의 domain에서 벗어나는 경우, 이상한 결과가 나올 수 있음
- 학습이 잘 안된 경우에도 위와 같은 문제 발생
- 특정 케이스에 대해서만 안되는 경우도 있음

~~추후 내용 추가적으로 업데이트 예정...~~

### References

- [https://brunch.co.kr/@advisor/33](https://brunch.co.kr/@advisor/33)