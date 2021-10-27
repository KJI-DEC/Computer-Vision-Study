# StarGAN: Unified Generative Adversarial Networks for Multi-Domain Image-to-Image Translation

[논문](https://arxiv.org/abs/1711.09020)

### Overview

- `multi-domain` , `image-to-image translation`
    - 하나의 이미지와 모델만을 가지고 한꺼번에 많은 도메인을 처리할 수 있음
- cycleGAN과 유사한 구조 → classification 부분, domain 정보가 추가됨
- `Mask vector`: 특정 label에 집중

### StarGAN

![Untitled](https://user-images.githubusercontent.com/71377968/135740323-f3500746-9fc7-4797-9b46-1be75bc22407.png)

- Multi-Domain Image-to-Image Translation
    - 여러 도메인간의 매핑을 학습하는 single Generator를 학습시키는 것이 목표
    - 랜덤으로 target domain label c를 만들어 Generator가 유연하게 이미지를 변환할 수 있게 함
    - auxiliary classifier로 하나의 discriminator가 소스와 도메인 label에 대한 확률 분포를 만들어냄
- Loss Function
    - Adversarial Loss: 만들어진 이미지와 오리지널 이미지가 구분되지 않도록 original GAN과 같은 adversarial loss 이용
    - Domain Classification Loss: discriminator D를 최적화하기 위해 사용되는 진짜 이미지에 대한 domain 분류 loss, generator G를 최적화하기 위한 만들어진 이미지에 대한 domain 분류 loss로 이루어짐
    - Reconstruction Loss: loss를 최소화하는 것이 변환된 이미지가 원본 이미지의 내용을 보존한다는 것을 보장하지 못하는데, 이를 완화하기 위해 도입된 loss

    → 모두 합친 Full objective

![Untitled](https://user-images.githubusercontent.com/71377968/135740330-74a47ed8-9cb5-4065-988b-7cae03a6691e.png)

- 다른 label을 가지고 있는 여러개의 dataset을 동시에 처리할 수 있음
    - 다만, dataset에서 label 정보가 부분적으로 보임 → 각 dataset마다 label이 서로 다름 → 해결: *Mask vector*
    - **Mask vector**: StarGAN이 특정화되지 않은 라벨을 무시하고 특정 dataset에 존재하는 특정 label에 집중하게 함
    - Training; domain label을 input으로 함 → generator는 알지 못하는 label을 그냥 무시하게 됨(zero vector) → discriminator는 모든 dataset에 대한 구분되는 특징들을 학습, generator는 모든 label을 제어하는 것 학습

### Experiments

- DIAT, CycleGAN, IcGAN 모델 비교

![Untitled](https://user-images.githubusercontent.com/71377968/135740337-b2e45ef8-066e-4035-99ef-59d60e48a376.png)

- CelebA에 대한 결과 - StarGAN이 타 모델에 비해 이미지의 퀄리티가 더 좋은 것을 확인할 수 있음

![Untitled](https://user-images.githubusercontent.com/71377968/135740355-167250b1-30ea-46cc-bb18-35b20dad97eb.png)

- RaFD에 대한 결과 - StarGAN이 더 자연스러운 이미지를 생성함. 특히 IcGAN의 경우 personal identity를 그대로 가져오지 못함

![Untitled](https://user-images.githubusercontent.com/71377968/135740359-a8f597a6-9f4b-40e6-9c23-043580bd444a.png)

- Mask vector에 대한 실험 결과 - mask vector를 반대로 둔 것과 바르게 둔 것을 비교한 것임. 윗줄은 바꾸고자 했던 것이 그대로 바뀌었으나 아랫줄은 원래 바꾸고자 했던 label이 무시되고 오히려 young을 old로 바꾼 것이 보임. → mask vector가 제대로 학습된 것을 확인 가능함

### Conclusion

> In this paper, we proposed StarGAN, a scalable imageto-image translation model among multiple domains using a single generator and a discriminator. Besides the advantages in scalability, StarGAN generated images of higher visual quality compared to existing methods, owing to the generalization capability behind the multi-task learning setting. In addition, the use of the proposed simple mask vector enables StarGAN to utilize multiple datasets with different sets of domain labels, thus handling all available labels from them. We hope our work to enable users to develop interesting image translation applications across multiple domains.

- multiple domain에 대한 이미지 변환을 generator와 discriminator를 통해 수행해냄
- scalability, better visual quality
- 다양한 dataset을 한꺼번에 활용할 수 있게 됨
