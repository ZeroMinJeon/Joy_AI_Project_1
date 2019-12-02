# JOY AI - Final Project

Created: Dec 02, 2019 5:22 PM
Reviewed: No

# Team Project 1조 - CycleGAN

---

조원: 전영민, 김은호,김윤섭

---

## 프로젝트 소개

이 프로젝트는 CycleGAN을 사용하여 input 과 output의 pair 없이, 이미지를 변형시킬 수 있습니다.  이를 사용하여, 간단하게 말을 얼룩말로 변환해보는 예제를 해보았습니다.

## 다루게 될 기술

---

1. GAN
2. Tensorflow
3. CycleGAN

## 이론 설명

- GAN
    - 간단히 설명하면 GAN은 Real Data와 Fake(generated) Data가 진짜인지 가짜인지 판별하면서 학습하는 모델입니다.
    - 아래의 그림처럼 지폐 위조범(Generator)은 가짜 돈(Fake data)을 생성하고 경찰은(Discriminator)는 가짜 돈(Fake Data)과 진짜 돈(Real data)을 구분하는 역할을 합니다. 이러한 적대적 관계를 통해서 Generator는 더욱 진짜 같은 fake data를 만드는 법을, Discriminator는 더욱 정교한 방법으로 real data를 판별하는 방법을 학습합니다. 이것이 GAN의 핵심 아이디어입니다.

![https://files.slack.com/files-pri/T25783BPY-F9SHTP6F9/picture2.png?pub_secret=6821873e68](https://files.slack.com/files-pri/T25783BPY-F9SHTP6F9/picture2.png?pub_secret=6821873e68)

출처 : [https://files.slack.com/files-pri/T25783BPY-F9SHTP6F9/picture2.png?pub_secret=6821873e68](https://files.slack.com/files-pri/T25783BPY-F9SHTP6F9/picture2.png?pub_secret=6821873e68)

- Pix2Pix2
    - Paired Data을 사용한다. 이 모델에서 신발의 윤곽선에 맞는 신발 이미지를 생성할 때는 왼쪽 그림처럼 (신발 윤곽이나 온전한 신발의 이미지)가 Pair로 필요하다.
    - 단점으로 Paired data를 얻는 것은 어렵기도 하고, 비용이 크다. 그리고 말 형태를 보존한채 얼룩말 무늬만 넣을 때에 Paired data처럼 같은 포즈를 취하는 말 - 얼룩말 이미지를 구하는 것은 더더욱 어렵다.
    - 이러한 문제들이 Unpaired data를 사용한 학습인 Cycle GAN이 생겼다.

    ![JOY%20AI%20Final%20Project/Untitled.png](JOY%20AI%20Final%20Project/Untitled.png)

- CycleGAN
    - Pix2Pix2와 다르게 Unpaired Data를 사용한다.
    - 오리지널 도메인의 이미지에 있는 개체를 이해하고, 대상 도메인의 이미지에 있는 동일한 개체의 모양이 일치하도록 필요한 변환을 적용한다. 이 알고리즘 적용은 말을 얼룩말로, 사과를 오렌지로 사진을 그림으로 바꾸는 결과물을 보여줍니다.

    ![JOY%20AI%20Final%20Project/Untitled%201.png](JOY%20AI%20Final%20Project/Untitled%201.png)

    - CycleGAN의 목표는 두 Domain간(X, Y)사이의 mapping function을 학습하는 것입니다.
    - 논문에는 CycleGAN은 생성된 이미지의 분포를 대상 도메인의 데이터 분포와 일치시키기위한 'Adversarial loss'와 학습된 mapping G, F가 서로 모순되는 것을 방지 하기 위한 'Cycle consistnecy loss'를 포함하고 있습니다.

    ![JOY%20AI%20Final%20Project/Untitled%202.png](JOY%20AI%20Final%20Project/Untitled%202.png)

    - 위의 사진에서 (a)에서 X가 G를 통과하고 다시 Y를 통과했을 다시 X가 나오는 것을 cycle consistency라고 한다. 그런데 mode collapse라는 문제로 GAN에서는 이런 cycle consistency가 힘이 든다. 다시 사진 (b)에서, X가 G를 통과하고 다시 F를 통과했을 때의 상황을 보면, X가 아닌 조금 다른 X2가 나온다. 이때 원래의X와 X2의 차이를 우리는 cycle-consistency loss라고 부르고, 학습할때에 이 값도 포함한 objective function을 구성해서 학습을 진행을 하게 된다.

## 코드 설명

- [https://colab.research.google.com/drive/1MqReESGQQcSCRBT4OTiDnVIBInBEOMBj#scrollTo=KUgSnmy2nqSP](https://colab.research.google.com/drive/1MqReESGQQcSCRBT4OTiDnVIBInBEOMBj)

## 실행방법

- 노트북으로 돌리기에 무겁기에 저희는 Colab에서 사용할 것 입니다.
- 위의 URL을 타고 들어갑니다.
- 순서대로 실행하면 됩니다.

## Project Data

- 'apple2orange', 'summer2winter_yosemite', 'horse2zebra', 'monet2photo', 'cezanne2photo', 'ukiyoe2photo', 'vangogh2photo', 'maps', 'cityscapes', 'facades', 'iphone2dslr_flower'

![JOY%20AI%20Final%20Project/Untitled%203.png](JOY%20AI%20Final%20Project/Untitled%203.png)

![JOY%20AI%20Final%20Project/Untitled%204.png](JOY%20AI%20Final%20Project/Untitled%204.png)

## Youtube Link

## Usage

---

- 현재, Training Epoch가 40이라서 좋은 결과값을 얻기 힘들었다. 논문에서는 200번 정도를 돌려서 좋은 결과를 얻었으므로, 예시와 같은 좋은 결과를 얻을 수 있을 것 같다.
- Paired 된 data가 아닌 Unpaired data를 사용하므로써 상대적으로 값싼 비용으로 학습시킬 수 있다.

## 한계

---

- 우리의 결과로는 Training Epoch가 현저히 적어 좋은 결과값을 얻기 힘들었다.
- 학습하는데 시간이 많이 소모하였다. 40번 학습하는데에 6시간이 소요하였다.
- 논문에서도 말과 얼룩말을 학습한 상황에서 사람이 말 또는 얼룩말을 탔을 경우에 사람도 얼룩무늬가 생기게 되었다.

## Reference

---

CycleGAN Paper: [https://junyanz.github.io/CycleGAN/](https://junyanz.github.io/CycleGAN/)

GAN의 모델의 이해와 구현 출처: [https://yamalab.tistory.com/98](https://yamalab.tistory.com/98)

딥러닝(CydeGAN)을 이용해 Fortnite를 PUBG로 바꾸기 출처: [https://keraskorea.github.io/posts/2018-10-24-딥러닝(CycleGAN)을 이용해 Fornite 를 PUBG 로 바꾸기/](https://keraskorea.github.io/posts/2018-10-24-%EB%94%A5%EB%9F%AC%EB%8B%9D(CycleGAN)%EC%9D%84%20%EC%9D%B4%EC%9A%A9%ED%95%B4%20Fornite%20%EB%A5%BC%20PUBG%20%EB%A1%9C%20%EB%B0%94%EA%BE%B8%EA%B8%B0/)

[논문] Unpaired Image-to-Image Translation using Cycle-Consistent Adversarial Networks출처:

[https://dogfoottech.tistory.com/177](https://dogfoottech.tistory.com/177)

CycleGAN(Unpaired Image-to-Imgae Translation)출처: [https://rm-7.tistory.com/4](https://rm-7.tistory.com/4)