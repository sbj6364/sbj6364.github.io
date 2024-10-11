---
title: t-SNE
date: 2024-10-12 05:12:00
categories:
  - Machine Learning
  - Paper Review
tags:
  - artificial-intelligence
  - machine-learning
  - tsne
  - python
  - pytorch
typora-root-url: ../
---





## t-SNE (t-Distributed Stochastic Neighbor Embedding)

> RNN 공부 4번째 paper (이미지 업데이트 예정)



## Abstract

- t-SNE: 고차원 데이터를 2차원 또는 3차원 맵으로 시각화하는 새로운 기법
- SNE(Stochastic Neighbor Embedding (Hinton and Roweis, 2002))의 변형, 개선된 방법론
  - 최적화가 더 용이함
  - 포인트가 맵의 중심에 몰리는 crowding problem문제를 해결
  - 여러 스케일에서 데이터의 구조를 드러내는 데 탁월
  - 특히 여러 다른 저차원 manifold에 놓인 고차원 데이터를 시각화하는 데 적합
- t-SNE는 매우 큰 데이터 세트를 시각화하기 위해 인접 그래프에서 random walks 방법을 사용
  - 전체 데이터의 암시적인 구조가 데이터 하위 집합에 영향을 미치도록 함
- 기존의 비매개변수 시각화 기법들(예: **Sammon Mapping**, **Isomap**, **Locally Linear Embedding**)보다 더 나은 시각화를 제공



## **1. Introduction**

- 고차원 데이터의 시각화 필요성
  - 고차원 데이터를 시각화하는 것은 많은 분야에서 중요하지만 어려운 문제.
  - 기존의 **PCA**(Principal Component Analysis)나 **MDS**(Multidimensional Scaling) 같은 기법은 비선형 구조를 제대로 표현하지 못함.
- 문제점
  - 비선형 구조를 제대로 반영하지 못하거나 데이터의 지역적 구조를 보존하지 못하는 문제가 있음.
- 해결책: t-SNE
  - t-SNE을 통해 기존 SNE(Stochastic Neighbor Embedding)를 개선해보자!



## **2. Stochastic Neighbor Embedding**

- **SNE의 기본 개념**

  - 고차원 데이터의 유사성을 확률로 변환하여 저차원 공간에서도 이를 유사하게 유지하는 방법.

  - 각 고차원 데이터 포인트 $x_i$에 대해 이웃 데이터 포인트 $x_j$가 선택될 확률 $p_{j|i}$를 계산.

  - 이 확률은 가우시안 분포를 기반으로 하며, 가까운 데이터 포인트일수록 확률이 큼.

    $$ ⁍ $$

- **저차원 공간에서의 확률**

  - 저차원 공간에서는 비슷한 방식으로 확률 $q_{j|i}$를 계산하지만, 여기서는 모든 데이터 포인트에 대해 동일한 분산을 가정함.

    $$ q_{j|i} = \frac{\exp(-\|y_i - y_j\|^2)}{\sum_{k \neq i} \exp(-\|y_i - y_k\|^2)} $$

- **Cost Function**

  - 고차원 공간에서의 확률 분포와 저차원 공간에서의 확률 분포 간의 차이를 **Kullback-Leibler 발산(KL divergence)으**로 최소화함.

    $$ C = \sum_i KL(P_i \| Q_i) = \sum_i \sum_j p_{j|i} \log \frac{p_{j|i}}{q_{j|i}} $$

- **문제점: 혼잡 문제(Crowding Problem)**

  - SNE는 고차원 공간의 중간 거리를 정확하게 표현하지 못해 저차원 공간에서 데이터 포인트들이 중심에 몰리는 문제 발생.



## **3. t-Distributed Stochastic Neighbor Embedding**

### **3.1 대칭화된 SNE (Symmetric SNE)**

- **SNE의 문제점**

  - 기존 SNE는 각 데이터 포인트에 대해 조건부 확률을 계산하지만, 이 조건부 확률은 비대칭적이어서 계산이 복잡하고 최적화가 어려움.

- **대칭화된 확률 사용**

  - **대칭 SNE**는 비대칭 확률 대신, 고차원과 저차원 공간 모두에서 데이터 포인트 간의 **공동 확률(joint probability)**를 사용하여 유사성을 모델링함.

  - 고차원 공간에서의 공동 확률 $p_{ij}$는 조건부 확률 $p_{j|i}$와 $p_{i|j}$의 평균으로 정의됨

    $$ p_{ij} = \frac{p_{j|i} + p_{i|j}}{2n} $$

  - 저차원 공간에서도 유사하게 $q_{ij}$를 정의

    $$ q_{ij} = \frac{\exp(-\|y_i - y_j\|^2)}{\sum_{k \neq l} \exp(-\|y_k - y_l\|^2)} $$

- **비용 함수**

  - 대칭 SNE는 고차원 공간의 공동 확률 $p_{ij}$와 저차원 공간의 공동 확률 $q_{ij}$ 간의 차이를 **Kullback-Leibler 발산(KL divergence)**으로 측정하여 이를 최소화함

$$ C = \sum_i \sum_j p_{ij} \log \frac{p_{ij}}{q_{ij}} $$

- 장점
  - 대칭화된 SNE는 더 단순한 비용 함수와 경사(gradient)를 제공하며, 최적화가 더 쉬워짐.
  - 비대칭 SNE에 비해 계산 속도가 빠름.

### **3.2 The Crowding Problem**

- 혼잡 문제의 원인
  - 고차원 데이터가 저차원으로 임베딩될 때, 중간 거리를 정확하게 표현하는 것이 어려움.
  - 저차원 공간에서는 중간 거리의 데이터 포인트를 충분히 배치할 공간이 부족하여, 데이터 포인트가 중심에 몰리는 **혼잡 문제** 발생.
- 문제의 예시
  - 고차원 매니폴드에서 서로 거리가 있는 여러 포인트들이 2차원 공간에 압축되어 배치되면서 클러스터가 뭉치는 현상이 발생.
- 혼잡 문제 해결을 위한 기존 접근
  - **Cook et al., 2007**에서는 **UNI-SNE**라는 기법을 도입해, 모든 포인트 사이에 약간의 반발력을 추가하여 혼잡 문제를 완화하려고 했음.
  - 하지만 UNI-SNE는 최적화가 까다롭고, 최적화 과정에서 포인트들이 잘못된 위치로 배치되는 경우가 많음.

### **3.3 Mismatched Tails can Compensate for Mismatched Dimensionalitie**

> **Heavy Tails of t-distribution 으로 혼잡 문제 해결**

- **혼잡 문제 해결 전략**

  - t-SNE는 고차원과 저차원 공간의 차원 불일치를 보상하기 위해, 저차원 공간에서 **학생 t-분포(특히 자유도 1의 t-분포, 즉 Cauchy 분포)**를 사용.
  - t-분포는 **꼬리가 두꺼운(heavy-tailed)** 특성이 있어, 중간 거리의 데이터 포인트들을 더 멀리 떨어뜨릴 수 있음.

- **t-분포를 사용한 확률 계산**

  $$ q_{ij} = \frac{(1 + \|y_i - y_j\|^2)^{-1}}{\sum_{k \neq l} (1 + \|y_k - y_l\|^2)^{-1}} $$

  - 이 분포는 중간 거리를 멀리 떨어뜨리면서도 멀리 떨어진 클러스터 간의 상호작용을 잘 유지함.
  - 이를 통해 **혼잡 문제**를 효과적으로 해결하고, 저차원 공간에서 클러스터 간의 명확한 분리를 가능하게 함.

- **t-분포의 장점**

  - 고차원 공간에서 적당히 떨어진 포인트들을 저차원 공간에서도 더 멀리 떨어뜨림으로써 데이터의 구조를 정확히 표현.
  - 클러스터 간의 상호작용이 일정하게 유지되어, 여러 스케일에서의 구조를 명확히 시각화 가능.

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/78d4d482-e80b-4a4b-8a2f-47415897aee5/60bffe27-bd11-4403-b413-1ae0c42ff3fb/image.png)

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/78d4d482-e80b-4a4b-8a2f-47415897aee5/1526d484-1c1f-424e-b930-d29d5c31502c/image.png)

### **3.4 Optimization Methods for t-SNE**

- **Gradient Descent**

  - t-SNE의 비용 함수를 최소화하기 위해 **경사 하강법**을 사용.

  - 초기에는 작은 모멘텀으로 시작하여 포인트들이 적절히 배치된 후 모멘텀을 증가시킴.

    $$ Y^{(t)} = Y^{(t-1)} + \eta \frac{\partial C}{\partial Y} + \alpha(t) (Y^{(t-1)} - Y^{(t-2)}) $$

- **Early Compression**

  - 최적화 초기에 데이터 포인트들이 서로 가까이 있도록 강제하여, 전체적인 구조를 더 잘 탐색할 수 있게 함.

- **Early Exaggeration**

  - 초기 최적화 단계에서 모든 확률 $p_{ij}$를 특정 계수(예: 4)로 과장시켜, 자연스러운 클러스터가 더 쉽게 형성되도록 함.

- **최적화의 안정성**

  - t-SNE는 전역 최적해를 보장하지 않지만, 초기화와 최적화 방법을 적절히 설정하면 대부분의 경우 우수한 시각화를 얻을 수 있음.



## **4. Experiments**

### Overview

- 데이터셋
  1. **MNIST**: 60,000개의 손글씨 숫자 이미지 데이터셋.
  2. **Olivetti Faces**: 40명의 얼굴 이미지를 포함한 데이터셋.
  3. **COIL-20**: 20개의 객체를 다양한 회전 각도에서 찍은 이미지 데이터셋.
- 실험 결과
  - **t-SNE**는 다른 기법들(Sammon mapping, Isomap, LLE)에 비해 각 클래스 간의 구분을 더 명확하게 시각화
  - 예를 들어, MNIST 손글씨 숫자의 클러스터가 거의 완벽하게 구분됨… 밑에 사진 보시면 신기합니다.
  - Olivetti Faces에서도 각 개체가 잘 분리되며, COIL-20 데이터셋에서는 각 객체의 회전 각도에 따라 잘 구분된 맵을 생성

### **4.1 Data Sets**

- MNIST
  - 손글씨 숫자 이미지 데이터셋.
  - 총 60,000개의 28×28 픽셀의 이미지로 구성.
  - 숫자 클래스(0-9)로 구분된 10개의 클래스를 가짐.
  - 실험에서는 계산 효율성을 위해 6,000개의 샘플을 무작위로 선택.
- Olivetti Faces
  - 40명의 개체에 대한 얼굴 이미지로 구성.
  - 각 개체당 10개의 이미지를 제공, 총 400개의 이미지.
  - 각 이미지의 크기는 92×112 픽셀.
  - 이미지 간의 관점 변화, 표정 변화, 안경 착용 여부 등의 차이가 있음.
- COIL-20
  - 20개의 객체에 대한 이미지 데이터셋.
  - 각 객체는 72개의 서로 다른 회전 각도에서 촬영된 이미지를 제공, 총 1,440개의 이미지.
  - 각 이미지의 크기는 32×32 픽셀.

### **4.2 Experimental Setup**

- **PCA를 사용한 차원 축소**

  - 모든 데이터셋은 **PCA(Principal Component Analysis)**를 사용하여 30차원으로 먼저 축소.
  - 계산 시간을 줄이고, 노이즈를 줄이며, 데이터 포인트 간의 거리를 크게 왜곡하지 않도록…

- **기법 비교**

  - t-SNE와 다른 비매개변수 차원 축소 기법들 비교.
  - 비교군: **Sammon Mapping**, **Isomap**, **Locally Linear Embedding (LLE)**.

- **각 기법의 매개변수 설정**

  ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/78d4d482-e80b-4a4b-8a2f-47415897aee5/c56af08a-4f82-4aeb-9b10-1e14fced780c/image.png)

  - **t-SNE**: 퍼플렉시티(Perplexity) = 40.
  - **Sammon Mapping**: 매개변수 없음.
  - **Isomap**: 이웃의 수 k = 12
  - **LLE**: 이웃의 수 k = 12

- **색상 및 기호로 평가**

  - 시각화를 평가하기 위해 데이터 포인트에 클래스 정보를 바탕으로 색상과 기호를 부여.
  - 하지만 클래스 정보는 시각화 과정에서 위치를 결정하는 데 사용되지 않음.

### **4.3 Results**

#### MNIST

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/78d4d482-e80b-4a4b-8a2f-47415897aee5/0815a08b-20f3-4651-9d3e-deb298306d99/image.png)

- t-SNE 결과
  - 손글씨 숫자 클래스(0-9)가 거의 완벽하게 분리된 시각화 결과를 제공.
  - 세부적으로, 같은 숫자 내에서도 숫자의 쓰기 방식이나 모양에 따라 클러스터가 세분화됨. 예를 들어, 1의 방향성이나 7과 9의 곡선형 정도가 시각적으로 구분됨. → ㄹㅇ 변태같음

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/78d4d482-e80b-4a4b-8a2f-47415897aee5/7b89a54f-a3c5-4b3a-b150-418205521f43/image.png)

- Sammon Mapping 결과
  - 대부분의 데이터 포인트가 하나의 큰 구 형태로 뭉쳐있고, 일부 클래스(예: 0, 1, 7)가 다소 분리됨.
  - 그러나 나머지 클래스 간의 혼잡한 겹침이 발생하여 클러스터 구분이 명확하지 않음.

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/78d4d482-e80b-4a4b-8a2f-47415897aee5/8f39b6c3-757a-4194-967b-f9ec4aa2fb45/image.png)

- Isomap 및 LLE 결과
  - 클래스 간 큰 겹침이 발생, 데이터의 구조가 명확하게 드러나지 않음.

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/78d4d482-e80b-4a4b-8a2f-47415897aee5/5d4a6ca1-81cf-44e7-bfc4-c7f42eba6f25/image.png)

#### **Olivetti Faces**

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/78d4d482-e80b-4a4b-8a2f-47415897aee5/e32b523d-94b0-4f7d-8130-29375d5ca609/image.png)

- t-SNE 결과
  - 각 개인에 해당하는 이미지가 대부분 잘 분리된 클러스터를 형성.
  - 일부 개체는 두 개의 클러스터로 나뉘는데, 이는 이미지의 큰 변화(예: 얼굴 방향이나 표정 변화)에 의한 것임.

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/78d4d482-e80b-4a4b-8a2f-47415897aee5/d145d820-8e05-47e1-8d89-065ad6ee5fb2/image.png)

- Sammon Mapping 결과
  - 같은 개인의 이미지는 비교적 가까이 위치하지만, 전체적으로 개체 간 명확한 분리 부족.

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/78d4d482-e80b-4a4b-8a2f-47415897aee5/59be3ad5-8035-406a-9192-f8570b134d15/image.png)

- Isomap 및 LLE 결과
  - 데이터의 구조를 잘 포착하지 못하며, 시각화 결과가 혼란스럽고 클래스 구분이 거의 없음.

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/78d4d482-e80b-4a4b-8a2f-47415897aee5/a7753e32-8126-4180-8254-46336bd4aced/image.png)

#### **COIL-20**

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/78d4d482-e80b-4a4b-8a2f-47415897aee5/90bbd76e-63de-4d04-92f1-b6e2e5637310/image.png)

- t-SNE 결과
  - 각 객체가 회전되며 나타나는 변화를 1차원 매니폴드(예: 폐쇄 루프 형태)로 시각화.
  - 앞뒤가 유사한 객체는 루프가 왜곡되어 서로 가까이 배치되며, 각 객체의 회전 방향에 따른 매니폴드가 명확하게 드러남.
  - 예를 들어, **자동차 모형**은 4개의 객체가 같은 방향으로 회전하면서 유사한 형태를 보임.

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/78d4d482-e80b-4a4b-8a2f-47415897aee5/b70b9882-87b2-437e-a00c-a0b2e4479b2d/image.png)

- Sammon Mapping, Isomap 및 LLE 결과
  - 각 객체 간의 구분이 명확하지 않으며, 특히 **Isomap**과 **LLE**는 데이터셋 내 소수의 클래스를 시각화하는 데 그침.
  - 데이터가 넓게 퍼져 있어 이웃 그래프를 통해 연결되지 않는 경우, 여러 클러스터로 분리되지 못함.

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/78d4d482-e80b-4a4b-8a2f-47415897aee5/31cdd398-56dd-4ca4-a82f-a419c085e7f0/image.png)



## **5. Applying t-SNE to Large Data Sets**

- 문제점

  - t-SNE는 계산 및 메모리 복잡도가 **O(n²)**이므로, 10,000개 이상의 데이터 포인트를 처리하는 데 어려움이 있음.

- 해결책: Random Walk

  - 랜덤 워크를 사용하여 데이터의 지역적 구조를 더 잘 반영할 수 있도록 함.

  - 랜덤 워크는 전체 데이터의 구조를 고려하여 일부 데이터만 시각화하는 데에도 적합함.

    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/78d4d482-e80b-4a4b-8a2f-47415897aee5/564e3a19-1926-420b-bd80-74f63f669fb5/image.png)

  - **확대해보세요..**

    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/78d4d482-e80b-4a4b-8a2f-47415897aee5/ba73f71e-3ce5-4e11-9818-3d3f33249f60/image.png)



## **6. Discussion**

- **다른 기법과의 비교**
- **Sammon Mapping**: 지역적 구조를 잘 표현하지만, 작은 거리 차이에 민감함.
- **Isomap**: 글로벌 구조는 잘 보존하지만, 작은 거리를 모델링하는 데 약함.
- **LLE**: 모든 포인트가 중심에 몰리는 문제 발생.
- **t-SNE의 강점**
- 지역적 및 글로벌 구조를 모두 보존하며, 클러스터 간의 명확한 분리 가능.
- **t-SNE의 단점**

1. **고차원 차원 축소 문제**: 2D나 3D 이상의 차원으로 축소할 때 성능이 떨어질 수 있음.
2. **내재된 차원의 저주**: 데이터의 내재된 차원이 매우 높을 경우 t-SNE의 성능이 떨어질 수 있음.
3. **비볼록성**: t-SNE의 비용 함수는 비볼록적이어서 최적화가 항상 전역 최적해에 도달하지는 않음.

### **6.1 Comparison with Related Techniques**

#### **Classical Scaling & PCA**

- **고전적 스케일링**은 고차원 공간에서의 유클리드 거리를 유지하기 위해 데이터를 선형 변환하는 기법.

- **PCA**와 유사하며, 큰 차원의 거리를 보존하는 데 중점을 둠.

- 이들은 

  비선형적인 매니폴드

  를 포착하는 데 약점을 가짐.

  - 고차원 공간에서 멀리 떨어진 포인트들 간의 거리를 유지하는 데 주력하므로, 가까운 포인트들 간의 거리를 정확하게 보존하지 X

#### **Sammon Mapping**

- 고차원 공간에서의 작은 거리 차이를 더 정확히 모델링하기 위해 고안된 기법.

  - 비용 함수에서 각 거리 차이를 원래의 거리로 나누어 작은 거리 차이에 높은 중요도를 부여.

    $$ C = \frac{1}{\sum_{i,j} \|x_i - x_j\|} \sum_{i \neq j} \frac{(\|x_i - x_j\| - \|y_i - y_j\|)^2}{\|x_i - x_j\|} $$

- **문제점**

  - 작은 거리 차이에 과도하게 민감하여, 거리가 매우 가까운 포인트 간의 작은 오류가 비용 함수에 큰 영향을 미침.
  - 지역적 구조를 유지하는 데 있어서 불안정.

#### **Isomap**

- **Isomap**은 **지오데식 거리(Geodesic Distance)**를 사용하여 고차원 매니폴드의 글로벌 구조를 보존하는 데 중점을 둠.
- 문제점
  - **"Short-circuiting" 문제**: 연결 그래프 상에서 짧은 경로를 따라 잘못된 연결이 발생하면, 데이터의 글로벌 구조를 왜곡할 수 있음.
  - 작은 거리를 모델링하는 데 약함.

#### **Locally Linear Embedding (LLE)**

- **LLE**는 각 데이터 포인트를 이웃 포인트들의 선형 조합으로 표현.
- 문제점
  - 데이터 포인트들이 모두 중심으로 모이는 경향이 있음. 이는 저차원 공간에서 데이터가 하나의 클러스터로 뭉쳐서 표현될 수 있다는 문제를 야기.
  - 이웃 그래프가 완전히 연결되지 않은 경우, 여러 클러스터가 자연스럽게 분리되지 않음.

#### **t-SNE와의 비교**

- **t-SNE**는 고차원 데이터에서의 유사성을 잘 보존하면서도 클러스터 간의 명확한 분리를 가능하게 함.
- **Isomap**과 **LLE**가 잘못된 연결로 인해 데이터 구조를 왜곡하는 반면, **t-SNE**는 데이터의 지역적 및 글로벌 구조를 모두 잘 유지함.



### **6.2 Weaknesses**

#### **1) Dimensionality reduction for other purposes.**

- t-SNE는 2차원 또는 3차원으로 데이터를 축소하는 시각화 작업에 특화되어 있음.
- 문제점
  - 차원이 3차원보다 높은 경우(t > 3), t-SNE가 잘 동작하지 않을 수 있음.
  - **t-분포**의 heavy tails → 고차원에서 너무 많은 확률 질량을 차지하게 되어, local structure 를 제대로 보존하지 못할 수 있기 때문임.

#### **2) Curse of Intrinsic Dimensionality**

- t-SNE는 데이터의 **지역적 특성**에 의존하여 차원 축소를 수행함.
- 문제점
  - 데이터가 높은 내재적 차원을 가질 경우(매니폴드의 차원이 높고 매우 복잡한 경우), t-SNE의 성능이 저하될 수 있음.
  - 예를 들어, 얼굴 이미지의 경우 내재 차원이 약 100차원으로 추정되는데, 이 경우 t-SNE가 locally 선형적인 가정을 위반할 수 있음.
- 해결책
  - **오토인코더(Autoencoder)**와 같은 심층 비선형 모델을 사용하여 고차원 매니폴드를 더 효율적으로 표현한 후, t-SNE를 적용하는 방법이 있을 수 있음.
  - 이러한 모델은 복잡한 비선형 구조를 더 잘 학습할 수 있고, 데이터 포인트 수를 줄이면서도 적절한 솔루션을 제공함.

#### **3) Non-convexity of the Cost Function**

- t-SNE의 비용 함수는 non-convex 이므로, 최적화가 항상 전역 최적해에 도달하지 않음.
- 문제점
  - 최적화가 여러 번 실행될 때마다 다른 로컬 최적해에 수렴할 수 있음.
  - 최적화 매개변수 선택에 따라 성능이 달라질 수 있음.
- 해결책
  - 최적화 매개변수를 적절히 설정하면 대부분의 시각화 작업에서 우수한 결과를 얻을 수 있음.
  - 실험을 통해 최적화 매개변수가 시각화 작업에 대해 매우 안정적이라는 것을 확인함.
  - 전역 최적해를 추구하는 대신, 데이터 시각화에서 중요한 특성을 잘 반영하는 로컬 최적해를 찾는 것이 더 중요할 수 있음.

------

### **7. Conclusion**

> 암튼 우리 모델이 최고다.

- t-SNE의 장점
  - 고차원 데이터를 저차원 공간에서 시각화할 때, 지역적 및 글로벌 구조를 잘 보존함.
  - 실험을 통해 t-SNE가 다른 차원 축소 기법들보다 우수한 성능을 보였음.
- Future works
  - 더 높은 차원으로의 축소 작업에서 t-SNE의 성능을 개선하는 방법 연구.
  - t-SNE를 여러 개의 저차원 포인트로 확장하는 방법 탐구.









