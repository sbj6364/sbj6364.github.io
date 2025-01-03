---
title: GAN Overview
date: 2024-10-27 23:12:00
categories:
  - Machine Learning
tags:
  - artificial-intelligence
  - machine-learning
  - gan
  - generative-model
  - python
  - pytorch
typora-root-url: ../
---



## Generative Adversarial Networks(GAN)



### What is GAN?

GAN은 생성적 적대 신경망으로, 두 개의 신경망이 상호 경쟁하는 구조를 가진 인공지능 모델이다. 이 모델은 생성자(Generator)와 판별자(Discriminator)로 구성되며, 생성자는 실제와 유사한 데이터를 생성하려고 시도하고, 판별자는 해당 데이터가 실제 데이터인지 생성된 데이터인지를 판별하려고 한다. 이 과정에서 두 네트워크는 점차적으로 성능을 향상시키며, 최종적으로 현실적인 데이터를 생성할 수 있게 된다. 쉽게 말해 진짜 같은 가짜를 만들고, 이를 판별하는 과정을 지속적으로 거쳐 완성도를 높이는 과정이다.



### Architecture

GAN의 핵심은 두 개의 주요 구성 요소인 생성자와 판별자로 이루어져 있다.

#### Generator

- **목적:** 실제 데이터와 유사한 가짜 데이터를 생성
- **입력:** 주로 잠재 공간(latent space)에서 샘플링된 노이즈 벡터
- **출력:** 합성된 데이터 (이미지 등)

#### Discriminator

- **목적:** 입력된 데이터가 실제 데이터인지 생성된 데이터인지를 판별
- **입력:** 실제 데이터 또는 생성자가 만든 가짜 데이터
- **출력:** 데이터가 실제일 확률



### 동작 원리

GAN은 생성자와 판별자가 동시에 학습되는 적대적 과정(adversarial training)을 통해 동작한다. 생성자는 판별자를 속이기 위해 점점 더 현실적인 데이터를 생성하려고 시도하고, 판별자는 생성자가 만든 가짜 데이터를 정확하게 구분하려고 노력한다. 이 과정에서 생성자는 판별자가 더 이상 가짜 데이터를 구분하지 못할 정도로 정교한 데이터를 생성하게 된다.

1. **생성자의 역할:** 랜덤 노이즈를 입력으로 받아 실제와 유사한 데이터를 생성
2. **판별자의 역할:** 실제 데이터와 생성자가 만든 데이터를 구분하여 실제 데이터일 확률을 출력
3. **학습 과정:** 생성자는 판별자를 속이기 위해 데이터를 개선하고, 판별자는 이를 정확하게 판별하기 위해 업데이트



### 종류

GAN에는 다양한 변형이 존재하며, 각각의 목적과 응용 분야에 따라 설계가 다르다.

#### Deep Convolutional GAN(DCGAN)

- 합성곱 신경망(Convolutional Neural Networks, CNN)을 기반으로 한 GAN의 일종
- 이미지 생성에 특히 효과적이며, 합성곱 층을 사용하여 생성자와 판별자의 성능을 향상시킴

#### Conditional GAN

- 추가적인 조건 정보를 입력으로 사용하여 특정한 속성을 가진 데이터를 생성할 수 있음
- 특정 클래스의 이미지를 생성하거나, 텍스트 설명에 맞는 이미지를 생성 가능

#### CycleGAN

- 두 도메인 간의 이미지 변환을 가능하게 하는 GAN의 변형
- 말 이미지를 얼룩말 이미지로 변환하거나, 낮 이미지를 밤 이미지로 변환하는 등
- 쌍으로 된 데이터 없이도 학습이 가능

#### StyleGAN

- 이미지의 스타일을 제어할 수 있는 GAN의 변형, 높은 해상도의 이미지를 생성 가능
- 생성된 이미지의 다양한 세부 사항을 조절할 수 있어, 예술적이고 창의적인 이미지 생성에 적합



