---
title: U-Net 논문 리뷰
date: 2024-09-08 23:45:00
categories:
  - Machine Learning
  - Paper Review
tags:
  - artificial-intelligence
  - machine-learning
  - unet
  - python
  - pytorch
typora-root-url: ../
---



## U-Net: Convolutional Networks for Biomedical Image Segmentation



### Abstract

- U-net: CV 중에서도 Biomedical segmentation 을 위해 나온 합성곱 신경망
- 네트워크 모양이 U자
- 기존 FCN(Fully Convolutional Network) 을 수정, 확장시키면서 적은 데이터로 빠르게 효과적인 성능을 뽑아낼 수 있음



### 1. Introduction

- U-Net은 이미지의 전반적인 컨텍스트 정보를 얻기 위한 네트워크와 정확한 지역화(Localization)를 위한 네트워크가 대칭 형태로 구성되어 있음

- FCN: 기존의 Visual Recognition task 의 Single Class Label

  - 하나의 이미지가 무엇인지를 판단하는 것 → 각 픽셀이 무엇인지를 판단하는 단계로 넘어가 Segmentation 을 하는 목적

  - Segmentation Task 에서는 

    이미지의 위치정보

     가 중요

    - FC layer 를 거치며 벡터화 → 위치정보 사라짐
    - Fully - Convolutional 한 네트워크 고안 → ***FCN***

  

  ![1_unet](/images/240908/1_unet.png)

### 2. Network Architecture

- Skip Connection: Upsampling 시의 정확도를 높여주기 위해, 이전 Layer 의 Feature map을 넘겨받아 더해줌
- U-net: 좌측 input 부근의 Contraction Path 와 우측 output 부근의 Expansive Path , 그리고 그 둘을 이어주는 Bottle neck 부분으로 이루어짐

> **Contraction Path (수축 경로)**
>
> - convolution 연산부
> - 2번의 3 x 3 convolution 연산 이후 ReLU activation Func 을 사용
> - 2 x 2 , stride = 2 로 max pooling 을 진행
> - 각 단계에서 나온 Feature Map 을 crop 하여 저장
>   - ***Padding이 없어 input path 와 output path 의 사이즈 차이가 나기 때문***

> **Bottle Neck**
>
> - 3 x 3 conv , ReLU * 2
> - Drop Out

> **Expansive Path (확장 경로)**
>
> - up sampling 을 하는 구간
> - 똑같이 3 x 3 convolution 연산 2회
> - 2 x 2 max pooling 대신, 같은 scale 의 up convolution 연산 수행
> - 각 단계에서 대응되는 Contraction Path 의 Feature map 을 부착 (Conv 연산 전) → ***Skip Connection 효과***



![2_overlaptile](/images/240908/2_overlaptile.png)

- Fully Convolutional Network 구조의 특성상 입력 이미지의 크기에 제약이 없음
- 따라서 크기가 큰 이미지의 경우 이미지 전체를 사용하는 대신 overlap-tile 전략 사용

![2_overlaptile2](/images/240908/2_overlaptile2.png)

- 다음 tile에 대한 Segmentation을 얻기 위해서는 이전 입력의 일부분이 포함되어야 함. → Overlap-Tile
- 이미지의 경계 부분 픽셀에 대한 세그멘테이션을 위해 0이나 임의의 패딩값을 사용하는 대신 이미지 경계 부분의 미러링을 이용한 Extrapolation 기법을 사용

![3_mirroring](/images/240908/3_mirroring.png)

#### **Touching cells separation**

- Segmentation 작업에서 주요한 과제 중 하나는 동일한 클래스의 접촉 개체를 분리하는 것
- 닿아 있는 세포 사이의 경계부분을 분리하기 위해 사전에 학습된 가중치 맵을 사용
- 이미지 c, d와 같이 각 세포 사이의 경계를 포착할 수 있어야 함
- 이를 위해 학습 데이터에서 각 픽셀마다 클래스 분포가 다른 점을 고려하여 사전에 Ground-Truth에 대한 Weight map을 구해 학습에 반영

![4_fig3](/images/240908/4_fig3.png)

![5_weight](/images/240908/5_weight.png)

### 3. Training

- 출력 값: 픽셀 단위의 Softmax로 예측

- 최종 특징 맵(채널 k)에 대한 픽셀 x의 예측 값

  ![6_p](/images/240908/6_p.png)

- Loss Function

  - Cross-Entropy 함수가 사용
  - Touching Cells 분리를 고려하기 위해 Weight map Loss가 포함됨

  ![7_e](/images/240908/7_e.png)

## 4. Experiments

![8_ex1](/images/240908/8_ex1.png)

![9_ex2](/images/240908/9_ex2.png)

![10_ex3](/images/240908/10_ex3.png)



## 5. Conclusion

- U-Net은 FCN보다 확장된 개념의 Up-sampling과 Skip Architecture를 적용한 모델을 제안
- 결과적으로 아주 적은 양의 학습 데이터만으로 Data Augmentation을 활용하여 여러 Biomedical Image Segmentation 문제에서 우수한 성능을 보임













