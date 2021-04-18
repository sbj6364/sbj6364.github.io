---
title: Kaggle for Data Science
date: 2021-04-15 10:00:00
categories:
  - Machine Learning
  - Data Science
tags:
  - machine-learning
  - data-science
  - ml
  - ds
  - data
  - kaggle
  - colab
typora-root-url: ../
---



## [ML] Kaggle: 데이터 사이언스 경진대회 플랫폼

> Reference: Prof.Choi / [Video](https://www.youtube.com/watch?v=raEi_cPfoLU&list=PL1xKqHsVFgvktrttPFUK8ayVr0oTz5RoN&index=4&t)



### About Kaggle

Kaggle은 가장 유명한 데이터 사이언스 경진대회 플랫폼이다. 2010년 예측모델 및 분석을 위한 플랫폼 서비스로 출발하여 **2017**년 구글에 인수되었으며, 2019년 기준 13,000여 개의 데이터를 공개한 상태이다. 의료, 경제, 자연과학, 공학 등 거의 모든 분야의 데이터를 다루며 무려 190개 이상의 국가로부터 100만명 이상의 회원이 가입하여 활동 중이다.

다양한 기능이 있으나, 이중 competition의 경우 주어진 과제에 예측 모델을 만들고 학습 결과를 업로드하면 정확도가 평가되는 구조로 진행되어 machine learning을 공부하기에 적합하다. 또한 이를 기반으로 포인트를 획득하여 레벨을 업그레이드 할 수 있으며, 레벨에 따라 데이터 과학자로 취업할 수 있는 기회가 주어지기도 한다. 챌린지에서 입상을 하게 되면 다양한 범주의 상금 또한 획득할 수 있다. 

> 한국에 비슷한 플랫폼으로 Daicon이 있다.



### Why Kaggle?

- 기업에서는 본인들의 문제를 공개적으로 **해결**하고 싶었다.
- 기업에서 훌륭한 data scientists를 **채용**하고 싶었다.
- 정부기관/단체에서 data scientists를 **양성**하고 싶었다.
- 개인은 data scientist로 **성장**하고 싶었다.

결국 기업/기관은 dataset과 prize를 제공함으로써 문제 해결 및 인력 발굴이 가능해지고, 개인은 제공받은 dataset과 prize, 개발 환경, community를 통해 스스로의 역량을 키울 수 있게 되는 것이다. 따라서 현재로서 우리는 실력 향상을 위한 툴로 Kaggle을 사용하는 것이 가장 좋으며, 추후 실력을 키워 다양한 활동에 참가할 수 있을 것이다. 여기서 말하는 다양한 활동들에는 아래와 같은 것들이 존재한다.

- Competition: 대회 순위에 따른 메달.

  > 대회에서 좋은 결과를 얻는 것을 목표로 한다.

- Notebook: 좋은 설명, 좋은 코드에 따른 메달

  > Community 내 소통의 창구이다. 설명과 시각화에 많은 노력이 들어간다. Jupyter Notebook의 Kaggle ver.라고 보면 된다.

- Dataset: 좋은 데이터 셋

  > 개인/단체/회사의 dataset을 공유하고, 가치 있는 dataset을 공개 및 가공한다.

- Discussion: 댓글 및 좋은 토론

  >서로의 의견을 공유하고, 집단 지성으로 모델 개선이 가능해진다.

  

뿐만 아니라 Kaggle 내에는 자체 등급, Performance Tier도 존재한다.

![Kaggle-tier]

실제로 몇몇 기업들의 경우 위 등급이 Master, Grandmaster인 경우 1차 테스트 면제 등의 기회를 부여한다고 한다.



### How to Participate

ML 학습을 위해 Kaggle competition에 참가하고자 할 때는 다음과 같은 순서를 따르면 된다.

- 참가하고자 하는 competition에 들어가서 우측 상단의 **Join competition**을 누름

- 해당 competition의 rules를 숙지한 후, **I Understand and Accept**를 누름

  

**Data** tab에는 문제 해결을 위한 train/test data 및 submit template이 있으며, Data description을 통해 제공되는 데이터를 이해할 수 있다.

**Notebook** tab은 일반 Jupyter Notebook과 동일하다고 보면 된다. Colab과 비슷한 형태로 학습용 GPU를 주 40시간에 한해 사용할 수 있다. 추가 사용 시 Google Cloud 결제가 필요하다.

본인만의 모델 예측값을 제출하는 경우, 다음과 같은 세 가지 방법을 사용할 수 있다.

- File Upload
- Kaggle Notebook
- Colab

나는 주로 Colab을 통한 submission을 선호하는 편이므로, 이번 포스팅에서는 Colab을 통해 학습하는 과정만 간단하게 소개해 보겠다.



### Colab + Kaggle



#### Install

Colab과 Kaggle을 연동하기 위해서는 먼저 kaggle 계정에서 API Token을 download 해야 한다. 우측 상단 My Account로 들어가면 Create New API Token이 있다. 이 버튼을 눌러 `kaggle.json` 파일을 받는다. 이후 Colab에서 새 노트를 생성하고, 방금 받은 `kaggle.json` 파일을 upload한다. 이후 셀을 만들어 다음 코드를 입력해보자.

~~~python
!pip uninstall -y kaggle # 기존에 kaggle이 깔려 있다면 uninstall
!pip install --upgrade pip # pip 업그레이드
!pip install kaggle==1.5.6 # kaggle 1.5.6 설치
~~~

마지막에 `Successfully installed kaggle-1.5.6` 이 떴다면 kaggle이 잘 설치된 것이다. 이후 API 등록을 위해 아래 코드를 실행한다.

~~~python
!mkdir -p ~/.kaggle # '.kaggle' 폴더 생성
!cp kaggle.json ~/.kaggle/ # 'kaggle.json' 파일을 '.kaggle' 폴더 내부로 이동
!chmod 600 ~/.kaggle/kaggle.json # 해당 파일에 대한 Permission Warning이 일어나지 않도록
~~~

위 코드에서 한 번 오류가 났다면 한 줄씩 셀을 나누어 다시 실행하기를 권장한다. 이미 폴더가 만들어지거나 파일이 이동한 경우에는 실행되지 않기 때문이다.

이제 본인이 참가한 모든 대회를 보려면 `!kaggle competitions list`를 치면 된다.



#### Data download

원하는 competition의 Data tab에 들어가 command line을 복사하여 사용하면 Colab에서 dataset을 불러올 수 있다.

`!kaggle competitions download -c '대회명'` 형태로 제공될 것이다. 압축 파일로 제공되므로 불러오면서 동시에 압축을 풀어주는 게 편하다.

~~~python
!kaggle competitions download -c '대회명'
!unzip '대회명'.zip
~~~

자, 왼쪽 file tab을 refresh하면 모든 준비가 끝난 것을 볼 수 있을 것이다. 이제 마음껏 모델을 설계하고 학습해본 뒤 submission하여 정확도와 성능을 테스트 해보시길!













