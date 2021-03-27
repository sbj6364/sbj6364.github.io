---
title: Computer Specifications
date: 2021-03-28 03:00:03
categories:
  - CA
tags:
  - Computer-Architecture
  - CA
  - Computer
typora-root-url: ../
---



## Macbook Pro (13-inch, 2019, Four Thunderbolt 3 ports)



 현재 사용중인 개인 컴퓨터는 대학생 뿐만 아니라 디자이너, 개발자 등 많은 사람들이 사용하는 노트북 중 하나인 Apple의 MacBook Pro 이다. 평소 학업, 프로젝트 개발, 강의 시청 등 생활 다방면에서 유용하게 쓰고 있는 컴퓨터인만큼, 스스로도 제품에 대한 이해가 충분해야 할 것이다. 따라 이번 기회에 부품별 세부 설명과 제조사를 포함한 전반적인 컴퓨터 사양에 대해 자세하게 알아보고자 한다. 본격적으로 시작하기에 앞서 목차를 정리하자면 다음과 같다.



#### [Ⅰ. Overview ](#overview)

#### [Ⅱ. Specifications ](#specifications)

#####     [1. CPU ](#cpu)

#####	    [2. Memory ](#memory)

#####     [3. HDD ](#hdd)

#####     [4. Graphics](#graphics)

#####     [5. Chipset](#chipset)

#####     [6. O/S](#os)

#####     [7. Main Board](#main-board)

#### [Ⅲ. Conclusion ](#conclusion)



---





### Overview

<img src="/images/post2/1_1.png" alt="System Overview" style="zoom:48%;border:none;" />

 가장 먼저 나의 Mac에 관하여 개요를 훑어보았다. Windows의 경우 제어판의 장치관리자나 `msinfo32` 명령어를 통해 해당 컴퓨터의 시스템 정보를 알 수 있지만, Mac은 작업표시줄 좌측 상단의  `Apple 로고`를 클릭하여 시스템 정보를 알아볼 수 있었다. 대략적인 개요는 다음과 같다.



- 모델명: 맥북 프로 (13인치, 2019년형, 썬더볼트3 포트 4개 고급형)
- 회사: Apple
- 프로세서: 2.4 GHz 쿼드 코어 Intel Core i5
- 메모리: 16 GB 2133 MHz LPDDR3
- 시동디스크: Macintosh HD
- 그래픽: Intel Iris Plus Graphics 655 1536 MB
- O/S: macOS Big Sur (Version 11.2)



이외에 추가적으로 자세한 정보는 System Report에서 찾아볼 수 있었다.  



---



### Specifications



#### CPU

> 2.4 GHz Quad-Core Intel Core i5, Turbo max 4.10 GHz)

border:none;

 [EveryMac.com](http://EveryMac.com) 에 접속해 보면 지금까지 출시된 맥북의 프로세서 정보를 한 눈에 찾아볼 수 있다.

<img src="/images/post2/2_0.png" alt="Mac Processor info" style="zoom:48%;border:none;" />

본 컴퓨터와 일치하는 프로세서 번호는 `I5-8279U`이며, 이를 인텔 공식 홈페이지에서 찾아보았다.



<img src="/images/post2/2_1.png" alt="Processor" style="zoom:48%;border:none;" />



 제조 회사: **Intel®**

 해당 프로세서에 대한 수많은 정보들 중 내가 알고 있었던 정보는 '제조사', '코어 수', '프로세서 기본 주파수' 세 가지 정도 밖에 없었다. 

 CPU 캐시는 프로세서 상에 존재하는 고속 메모리이다. 인텔의 스마트 캐시는 모든 코어가 마지막 레벨 캐시에 대한 액세스 권한을 동적으로 공유할 수 있도록 제작했다고 한다.

 버스는 컴퓨터 구성 요소들 간 또는 컴퓨터들 간에 데이터를 전송하는 하위 시스템이다. 버스 종류로는 프런트 사이드 버스(FSB: CPU와 메모리 컨트롤러 허브 간 데이터 전달), 컴퓨터 마더보드의 인텔 I/O 컨트롤러 허브와 인텔 통합 메모리 컨트롤러 사이의 지점간 상호 연결인 DMI(Direct Media Interface), CPU와 통합 메모리 컨트롤러 간 지점간 상호 연결인 QPI(Quick Path Interconnect) 등이 있다.





#### Memory

> 16GB LPDDR3

<img src="/images/post2/2_2.png" alt="Memory" style="zoom:48%;border:none;" />



제조 회사: **Micron**

 현재 맥북의 메모리 슬롯을 보면 8GB의 메모리 두개, 총 16GB의 메모리로 구성되어 있다. 각각의 메모리는 동일한 정보를 나타내고 있는데, Manufacturer 부분을 통해 제조업체가 Micron인 것을 알 수 있다.

 Micron에서는 다양한 메모리를 제조하고 있는데, 타 노트북 제조사들의 경우 DDR(Double Data Rate) 시리즈의 메모리를 많이 채택한다고 한다. 맥북의 메모리로 DDR 시리즈가 아닌 LPDDR(Low Power DDR) 시리즈를 사용한다는 사실을 통해 소비 전력을 줄임으로써 밖에서도 오래 사용할 수 있도록 이동성을 추구한 애플의 의도를 조심스레 추측해 본다.

 여담으로, 나를 포함한 맥북 사용자들은 시스템 종료를 하는 일이 거의 없다. 스티브 잡스는 생전 컴퓨터를 켜고 끄는 일이 가장 비효율적인 행위라고 말한 바 있다. 애플은 그의 신념을 따라 발전했다. 맥북은 모니터를 덮기만 하면 된다. 휴대폰의 홀드와 비슷하다고 볼 수 있다. 소프트웨어 업데이트를 하지 않는 이상, 전원 재시작을 할 일은 거의 없는 것 같다.





#### HDD

> 512GB Apple SSD AP0512M

<img src="/images/post2/2_3.png" alt="Memory" style="zoom:48%;border:none;" />



제조 회사: **Apple
** 
 저장장치를 살펴보면 기본 이름이 Macintosh HD인것을 볼 수 있다. 처음에는 HD가 Hard Disk Drive를 줄인 말인가 했지만, 그랬다면 HDD로 썼을 것이다. 심지어 내 맥북의 실제 저장장치는 SSD이다. 물론 저장장치를 통칭하여 HDD라고 하지만, 요즘은 SSD와 대립하여 쓰는 경우가 많긴 하다. HD가 Home Directory의 약자라는 말도 있지만, 아직까지 저장장치의 기본 이름이 왜 Macintosh HD 인지는 찾지 못했다.

 Device Name은 APPLE SSD AP0512M 이다. 재미있는 사실은 표기된 용량이 512GB용량임에도 불구하고 실제 Capacity는 499.96 GB인 것을 볼 수 있는데, 이는 표기용량단위(Decimal)와 실제용량단위(Binary) 사이의 진법 차이 등을 원인으로 볼 수 있다.

 File System 부분에는 APFS라고 적혀있는데, 이는 Apple File System의 약자로, 기존의 HFS를 대체하여 '강력한 암호화'를 염두에 두고 설계한 파일 시스템이라 볼 수 있다.

 맨 마지막의 S.M.A.R.T. Status는 Self-Monitoring, Analysis and Reporting Technology의 약자라고 한다. 드라이브에 생긴 문제를 스스로 모니터링해서 분석 후 보고하는 기술이다.





#### Graphics

> Intel Iris Plus Graphics 655 GPU

 <img src="/images/post2/2_4.png" alt="Graphics" style="zoom:48%;border:none;" />

<img src="/images/post2/2_5.png" alt="Processor Graphics" style="zoom:48%;border:none;" />



 제조 회사: **Intel®**


 위 사진은 GPU 정보이다. 칩셋은 Intel에서 제조한 Intel Iris Plus Graphics 655인 것을 알 수 있다. 해당 그래픽을 찾아보니 왼쪽과 같은 정보들을 얻을 수 있었다.

 보통 인공지능 학습을 시킬 때 GPU가 필요하다고 하는데, 그런 학습 과정에서 GPU 내부는 어떤 일들이 일어나는지 궁금하다. 자료 2.4 사양 화면에 LG Display가 함께 뜨는 이유는 현재 LG모니터를 연결하여 더블 모니터로 사용중이기 때문이다.





#### Chipset

> Apple T2 Security Chip

<img src="/images/post2/2_6.png" alt="Chipset" style="zoom:60%;border:none;" />



제조 회사: **Apple**

 현재 나의 맥북은 보조 칩셋이라고도 할 수 있는 Apple T2 보안 칩을 탑재하고 있다. 이는 Apple의 Mac용 2세대 맞춤형 실리콘 칩으로, 암호화된 저장장치, 보안 시동 기능, 향상된 이미지 신호 처리 및 Touch ID 데이터의 보안과 같은 기능을 Mac에 제공한다.  


<img src="/images/post2/2_7.png" alt="T2 Chip" style="zoom:15%;border:none;" />

 애플의 T2 칩에 대한 자세한 정보를 소개하자면, T2 칩은 2017년 아이맥 프로에 최초 사용되었으며 BridgeOS 2.0이라는 자체 OS를 구동한다. 64비트 ARM 기반 아키텍처로서 애플 A10 계열의 칩셋이다. 암호화된 문자를 주고받을 수 있으며 컴퓨터의 구동 프로세스를 사용자가 잠글 수 있게 하며 카메라와 오디오 등 다양한 컴퓨터 기능을 담당하고, SSD를 구동하는데 큰 기여를 한다. iMac Pro FaceTime HD 카메라의 '강화된 이미지 프로세싱' 기능과 애플의 Siri 호출 기능을 컴퓨터에 지원한다. 2018년 7월 12일에 공개된 MacBook Pro또한 이 칩셋을 사용하며 2018년 11월 7일 공개된 Mac Mini 와 MacBook Air, 2020년 8월 4일 공개된 iMac 5K도 이 칩셋을 채용했다고 한다.







#### O/S

> macOS Big SUr ver.11.2



<img src="/images/post2/2_8.png" alt="macOS Big Sur" style="zoom:35%;border:none;" />



제조 회사: **Apple**

 Apple의 모든 제품은 자체 개발한 독자적인 운영 체제 macOS를 사용한다. Apple은 과거 세계 최초 GUI환경 운영 체제인 Apple Macintosh OS를 출시한 바 있고, 이 후속작으로 2001년 3월 24일 Mac 전용 운영 체제인 macOS가 개발되었다. 윈도우와 달리, 소프트웨어로 별매가 되지 않고 하드웨어와 함께 완제품으로만 판매하여, 소프트웨어 점유율에선 경쟁하지 않는다는 특징이 있다.

 내가 가장 좋아하는 macOS의 장점은 Apple 기기 간 연동성이다. iCloud를 통한 사진, 파일, 프로그램 연동기능 뿐만 아니라 Apple Watch가 있으면 Mac을 비밀번호 없이 열 수 있고 메시지나 전화를 Mac을 통해서 받을 수도 있다. AirDrop 기능도 사용할 수 있고 핫스팟도 클릭 한 번으로 가능한 점 등 Apple 생태계를 구축한다면 한 기기처럼 관리하는 것이 가능하다. 아이폰, 아이패드, 맥북, 애플워치, 에어팟 등의 모든 Apple 기기를 사용하는 나로서는 쉽게 포기할 수 없는 부분이다.

 뿐만 아니라 음성 인식, 음성 합성, Siri 등의 기본 기능을 통해 노약자 및 장애인을 위한 기능에 충실한 모습이 매력적이다. 현재 최신 버전은 macOS Big Sur 11.2.3이며, 나의 맥북에는 아직 11.2로 업데이트가 필요한 상황이다. 최근들어 High Sierra, 빅서게이트 등 macOS의 안정성이 의심되는 모습이 조금씩 보이기에 개인적으로 새로운 버전은 안정화를 기다렸다가 천천히 업데이트 하는 편이다.





#### Main Board



<img src="/images/post2/2_9.png" alt="MB Pro 13'' 2019" style="zoom:35%;border:none;" />

<img src="/images/post2/2_10.png" alt="Elements for each colors" style="zoom:40%;border:none;" />

 제조 회사: **Apple** 

 메인보드는 앞선 모든 것들을 묶어두는 하나의 판 같은 개념으로 보면 된다. 마더보드, 시스템보드라고도 불리며, 제조사인 Apple에서는 로직 보드(Logic Board)라는 명칭으로 사용한다. 조립식 데스크탑을 사용하는 사람들이 주로 메인보드 검색을 해서 그런지, 맥북 자체에서 사용하는 로직 보드에 대한 정보는 인터넷 상에 많이 존재하지 않는 것 같다. 

 추가적으로 알아본 사항으로는 품목 코드가 `IF123-150-1` 이라는 사실인데, Apple 공식 홈페이지에서는 찾을 수 없어 [ifixit](ko.ifixit.com) 이라는 수리 사이트에서 검색한 것이라 확실하지는 않다.

<img src="/images/post2/2_11.png" alt="MB Pro 13'' 2018" style="zoom:65%;border:none;" />





---



### Conclusion



 이 외에도 맥북에는 오디오/마이크, 블루투스, 썬더볼트 버스 등 자체 개발하여 독자적으로 사용하는 부품이 매우 많았다. 이번 2021년 신형 맥북에는 자체 칩셋인 M1까지 선보이며 그들만의 생태계를 구축하고 있다. 아직까지 말이 많은 호환성 문제도 조금씩 개선해나가며 성능을 발전시킨다면, IT업계에서 대적할 자 없는 기업이 되지 않을까 생각한다.

 지금까지는 별 생각 없이 사용해 오던 노트북에 대해 더 심도 있게 알아볼 수 있었고 기기에 대한 더 많은 애정이 생겼다. 이 작은 크기의 노트북 속에 하나의 거대한 세상이 담겨있는 느낌이다. 단순히 내 노트북의 사양 뿐만 아니라 연결되는 부품, 역사나 주변 지식을 자연스럽게 알게 되었고, 이런 지식들은 앞으로 전공을 공부하며 크게 도움이 되리라 확신한다.





#### Sources



- [0.1 MacBook](https://www.apple.com/kr/shop/buy-mac/macbook-pro/13형)

- [2.0 Mac processor info](https://everymac.com/systems/by_processor/intel-core-i5-macs.html)

- [2.2 Processor](https://ark.intel.com/content/www/kr/ko/ark/products/191070/intel-core-i5-8279u-processor-6m-cache-up-to-4-10-ghz.html)

- [2.5 Processor Graphics](https://ark.intel.com/content/www/kr/ko/ark/products/191070/intel-core-i5-8279u-processor-6m-cache-up-to-4-10-ghz.html)

- [2.7 T2 Chip](https://ko.m.wikipedia.org/wiki/파일:Apple_T2_APL1027.jpg)

- [2.8 Big Sur](https://www.theverge.com/2020/11/16/21569405/macos-big-sur-update-error-macbook-pro-2013-2014-models-black-screen)

- [2.9 MacBook Pro 13'' 2019 Main Board](https://ko.ifixit.com/Store/Mac/MacBook-Pro-13-Inch-Retina-2019-2-4-GHz-Logic-Board-with-Paired-Touch-ID-Sensor/IF123-150?o=1)

- [2.10 Elements for each colors](https://ko.ifixit.com/Store/Mac/MacBook-Pro-13-Inch-Retina-2019-2-4-GHz-Logic-Board-with-Paired-Touch-ID-Sensor/IF123-150?o=1)

- [2.11 MacBook Pro 13'' 2018 Main Board](https://ko.ifixit.com/Guide/MacBook+Pro+13-Inch+Touch+Bar+2018+분해도/111384)

