---
title: "[논문 /수정중]CognitiveSSD 보충"
categories:
 - SSD
tags:
 - ssd
last_modified_at: 2021-02-07T14:23:00-05:00
---


1.1 Cognitive SSD 논문 리뷰
---------------------------

Cognitive SSD와 관련해서 정리해놓은 포스팅이다. 시간이 있을때 Github 블로그로 옮길 예정이다.

-	네이버 블로그 https://blog.naver.com/sb1016/222229150256

포스팅 중간에 보면 알겠지만, *Bandwidth 분석*, *NSG(Navigating Spreading-out Graph)* 에 대한 설명이 다소 부족하다.

이번 시간에는 위 부분들에 대해 보충 공부를 해보고자 한다.

1.2 Bandwidth 분석
------------------

논문에서는 NAND Flash의 내부 Bandwidth가 DLG-x 가속기에서 Deep neural network를 돌리는데 필요한 정도를 만족하는지 파악하고자 한다.

DLG-x와 Flash controller는 같은 frequency에 의해 돌아간다고 가정하며,

DLG-x의 NPE unit(뉴럴 네트워크 관련 프로세싱을 하는 유닛)은 $$N_{PE}$$ $$ PEs$$ 를 포함하고 있다.

이러한 NandFlash 하나의 채널 Bandwidth를
$${BW}_{flash}$$
라고 해보자.

만약 이 SSD에 M개의 채널이 달려있다면, Bandwidth는 다음과 같을 것이다

<p>
$$ BW^m_{flash} = M \times BW_{flash} $$

<center>(c는 컬러 RGB channel, h는 height, w는 width)</center>  </p>


자 여기에서 Convolution layer에 곱해지는 input ( 즉, 인풋 이미지나 전 단계의 feature map)의 크기가  
$$ I_C \times I_h \times I_w $$ 라고 해보자.

그리고 여기에서 추출되는 feature map(이미지의 특징을 나타내는 feature map)의 차원은 $$ O_C \times O_h \times O_w $$ 라 해보자.



이 연산에서 사용되는 커널의 차원은 다음과 같다고 하자.

$$ K_C \times K_h \times K_w $$

컨볼루션을 잘 모르는 사람을 위하여 그림을 준비했다.

<p align="center">
<img src="/assets/images/cognitive1.png" width="200">
</p>

인풋이나 가중치 값은 8bit fixed-point(고정소수점) representation을 사용한다고 가정하자.

예를 들어
$$ a = 0101.0110_2 $$
8bit 로 표현되어있다면, 이 값은 실제로
$$ a = 0 \times 2^3 + 1 \times 2^2 + 0 \times 2^1 + 1 \times 2^0 + 0 \times 2^{-1} + 1 \times 2^{-2} + 1 \times 2^{-3} + 0 \times 2^{-4} $$
를 의미한다.

하나의 feature map에 NANDFlash의 하나의 채널이 연결되도록 했을 때 computation에 필요한 Latency와 data access를 위한 latency를 조절하기 쉬워진다.

$$L*{compute} = \frac{OP_{compute}}{OP_{PE}} $$



$$ = \frac{2 \times K_c \times K_h \times K_w \times O_h \times O_w }{2\times N_{PE}} $$

<small>OP compute : 컨볼루션 레이어에서 연산횟수</small>

<small>OP PE: DLG-x 가 한 주기당 몇번의 연산을 하는. 성능</small>



1.3 NSG(Navigating Spreading-out Graph)
---------------------------------------

2 앞으로 무엇을 공부할 것인가!
------------------------------
