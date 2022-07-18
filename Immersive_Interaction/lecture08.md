# Lecture 8

몰입형 환경을 구성하는 가장 중요한 컴포넌트 중 하나가
몰입형 시각 디스플레이다.
가상현실의 붐을 일으킨 기계
가장 쉽고, 고도화하게 몰입형 시각 환경을 구성해준다.

### 4
대부분의 일반적인 HMD 디스플레이 형태

렌즈를 통해 작은 디스플레이로 
실제 디스플레이의 뒤에 넓은 스크린을 보는 것 같은 효과를 준다.

- 마이크로 디스플레이가 필요 > 렌즈를 통해 확장하는 작업이므로
확대해도 사람의 눈에 픽셀이 보이지 않을 정도로 해상도가 높아야함

- 렌즈 
    - 렌즈의 굴절률: 렌즈의 굴절률에 따라 같은 마이크로 디스플레이어도
    굴절률이 크면 더 화면의 사이즈가 커 보이는 효과가 있다
    - 렌즈의 도수: 마이크로 디스플레이를 눈앞에 바로 가까이 대면 
    눈안에 있는 렌즈로 인해, 눈이 초점을 맞출 수 있는 가장 가까운 물체의 거리가 있다
    스크린을 너무 눈앞에 가까이 가져다 대면 초점이 맞지 않는 문제 발생한다.
    가까이 가면 갈수록 초점이 맞지 않아 눈이 피로해짐. 
    렌즈가 디스플레이가 가까이 와도 초점을 맞추고 선명하게 볼 수 있게 해준다.
    렌즈의 도수가 커지면 커질수록 마이크로 디스플레이를 더 가까이 위치시킬 수 있다.

렌즈의 도수가 무조건 높을수록 좋을까?
- 렌즈의 도수를 높이려면 렌즈를 두껍게 만들면 된다. 
너무 두껍게 하면, 렌즈의 두께가 두꺼워질수록 무겁고 커지는 문제 발생
- 렌즈가 도수가 높아질수록 수차가 생긴다. 
    - 렌즈를 끼면, 어둡고 밝은 곳의 사이에 초록,노랑 색의 경계선이 보이는 색 수차 발생
    - 색수차와 같이 렌즈의 imperfection 으로 인해 발생하는 원하지 않는 효과가 발생함

- motion sickness, cyber sickness
양눈으로 하는 거리는 잘 렌더링 되지만
한쪽 눈의 렌즈로 하는 거리큐는 렌더링이 잘 안된다
why? 픽스된 환경의 hmd 기는 눈과 스크린 사이의 거리의 인지가 고정되어있음 (렌즈와 스크린이 고정되어있기 때문에)
하지만 실제 상황에서는, 초점을 맞추기 위해서 눈 안의 렌즈를 조절함, 멀리 있는 물체는 눈 안의 렌즈를 얕게 하고, 가까이 있으면 두껍게하여,
거리감을 렌즈의 두께를 통해 느낄 수 있다 > HMD 에서는 거리가 고정되어있어서 다음과 같은 방식을 통해 거리를 인지 할 수 없다.
 
- hmd 에서 멀미를 줄이는 방법에 대해서 다룰 예정

- 렌더링 이슈
실제 디스플레이 하는 결과물은 실시간으로 움직인 3차원 환경의 디스플레이다
사람이 느끼는 시야각과 hmd 가 만들어 내는 시야각과 일치해야함
내가 눈에서 인지하는 시야각과 컴퓨터 그래픽에서 렌더링 되는 시야각이 정확히 일치해야함  

렌즈의 정확한 focal length 와 디스플레이와 렌즈 사이의 거리,
최정적으로 사용자가 느끼는 시야각, 최종적으로 사용자가 느끼는 스크린 사이즈
등을 물리적으로 측정하여 파라미터로 연결

### 5 렌즈
아날로그 디바이스로 0 과 1로 이루어지는 것이 아니라 스펙트럼이 있다

아날로그 디바이스는 어떻게 튜닝하느냐에 따라 달라짐 > 가격대의 스펙트럼이 넓어짐

렌즈는 일반적으로 렌즈가 두꺼우면 두꺼울 수록 퀄리티가 높아짐(하지만 무거워짐)

- 일반 렌즈와 프레넬 렌즈와 비교   
프레넬 렌즈는 렌즈의 구역을 나눠서 일반 렌즈와 동일한 역할을 하면서
훨씬 얇게 만들었음
> 구역을 나누었기 때문에 구역을 나눈 지점들이 자연스럽게 이어지지 않는다.
> 약간의 구형태의 선들이 보인다

얼마나 정밀하게 디자인해서 일반 렌즈를 대체할 수 있는가가 관건
 
> 이미지 퀄리티와 렌즈의 무게 사이는 tradoff 관계

### 6
더 줄일 수 있는 공간은
렌즈와 디스플레이 사이의 공간으로
빛이 직선으로 쭉 이어지는 공간이다. > 많은 공간 차지
사이 간격을 줄이기 위해서는 더 굴절이 많이 일어나는 렌즈 필요 > 렌즈가 무거워짐

- 팬케이크 렌즈
빛이 일직선으로 가는 것을 접어보자

단점 : 모든 반사체가 빛의 반사율을 100프로로 만들 수 없다. 즉 빛이 반사될 때마다 빛의 세기가 약해짐
> 처음 디스플레이를 훨씬 더 밝게 만들면 해결 가능

### 7 Chromatic aberration 색수차

하얀색 빛이 렌즈에 들어왔을 때, 빛의 모든 파장이 동일하게 들어오는 경우

렌즈의 원리가 공기의 매질, 렌즈의 매질의 특징에 의해 굴절이 발생하는 것임

파장에 따라 굴절률이 달라짐, 즉, 빨, 초, 파등 파장이 다른 빛은 굴절이 달라
디스플레이에 도달하는 지점이 달라짐

모든 빛이 한 지점에 맞아야 이미지가 선명하게 나오지만 
색수차로 인해 경계가 흐릿하게 나오면서 특정 파장의 빛의 색이 경계에 나타남
> 몰입도 떨어짐

### 8
색수차 해결 방법

- 비구면 렌즈 (최근에 더 많이 사용하는 방법)    
파장별로 굴절률이 같다면 문제 발생 x,
위치마다 곡률이 모두 다르게 제조
    - 제조가 어렵
    - 파장별로 굴절률이 같게 유지
    - 시뮬레이션을 통해 제조

> 구면 렌즈
> - 제조가 쉽다
> - 렌즈 표면의 곡률을 일정하게 유지 
> - CA  해결 못함

- 렌즈 중첩   
렌즈를 세개 겹쳐서 모든 파장이 하나의 점으로 모이게 함

최근 여러 렌즈를 붙이는 기술도 발전해서 난반사가 발생하지 않게 하고 있음

### 9 Lens Distortion 왜곡
하드웨어 적으로 고퀄리티의 렌즈를 만들고,
소프트웨어적으로도 해결 

렌즈의 극단으로 갈수록 왜곡이 많이 되는 현상 발생

- pincussion distortion : 이미지가 늘어나는 현상
소프트웨어적으로 해결하는 것이 매우 어렵
하드웨어로 해결

- barrel distortion : 이미지가 압축되는 현상
소프트웨어적으로 해결 가능 (이미지를 늘려서 해결)

### 10
왜곡이 발생에 대한 함수를 만들고
렌즈에 의해서 생긴 화면에 역함수를 취해서 왜곡을 제거한다

중앙에서 멀리 떨어질수록 왜곡이 커짐

### 14
그래픽 렌더링을 이미지가 자연스럽게 잘 할것인가?

f = 렌즈 도수
d' = 렌즈와 디스플레이 사이의 거리, focal length
h' = 디스플레이 높이
h = 인식한 디스플레이 높이
M = h / h'
eye relief = 눈과 렌즈 사이의 거리 > 허용 범위가 있고, 허용 범위가 클수록 좋다

### 18
가상 카메라 디자인
그래픽 렌더링을 위해 사용하는 카메라와 현재 내 눈에 보이는 hmd 스크린이 만들어 내는 카메라
를 최대한 일치시켜야 자연스럽게 보임

---
# Lecture 8.1 

### 1
- 실제 사람의 눈 사이의 거리
- ipd = 렌즈 사이의 거리
- 그래픽적으로 사용되는 ipd 값

세가지가 물리적으로 일치한다면 문제가 없지만 현실에서는 그렇지 않다..

사람의 양 눈 사이의 거리는 변경 불가,
렌즈 사이의 거리를 조절하는 것은 어려움

그래픽적인 두 눈사이의 거리를 소프트웨어적으로 변경하는 것은 가능하지만,
실제 사람의 두 눈 사이의 거리에 대한 정보가 필요

### 10 vergence-accommodation conflict
- 가까이 있는 물체를 고해상도로 보기 위해서는 양 눈을 해당 위치를 바라보도록 회전시킨다.
- 멀리 있는 물체에 초점을 맞추기 위해서 눈의 렌즈의 두께가 얇아지고, 가까이 있는 물체는 두꼐가 두꺼워진다.

물체를 선명하게 보기 위한 눈의 회전 정도와, 눈의 렌즈의 두께의 정도를 통해
물체의 거리를 측정한다.

가상 환경에서는 양쪽 눈에 다른 이미지를 띄움으로써, 눈의 회전 정도를 충족 시킬 수 있음.
하지만, 기본적으로 눈과 디스플레이 사이의 거리는 항상 고정되어있기 때문에,
눈의 렌즈의 두께의 정도는 현실에서 물체를 볼 때와 다르다.
즉, 보이는 물체와의 거리와, 눈의 렌즈의 두께 정보에 따른 
물체와 거리가 서로 불일치 하게됨.

### 11 Fixed Focus Displays
사용자가 느끼는 사용자와 가상의 스크린 사이의 거리를 변화시켜 conflict 를 최소화 하고 싶다.

d 값을 변경하는 방법은 d' 와 f 를 실시간으로 제어할 수 있다면?
1 / d + 1 / d' = 1 / f

### varifocal displays
- display 와 렌즈 사이의 거리를 제어할 수 있는 디스플레이

단점 - 물리적으로 무언가 움직이기 위해서, 모터를 달아야 하기 때문에 무거워 진다. > 실용성이 떨어짐

필수적으로 eye tracking camera 가 필요
사용자가 지금 어떤 물체를 보고 있는지 알아야 해당 물체에 초점을 맞춘 상태로 변경
내 양안 큐와 내 렌즈 두께 큐가 일치하려면, 실시간으로 내가 어떤 물체를 보고있는지 알아야함

눈의 초점을 바꾸는 것은 매우 빠른 움직임, 기계적인 움직임의 딜레이가 발생

- focal length 를 변화시킴
렌즈의 두께를 변경 > 물리적으로 변화가 없음

단점 - 렌즈의 focal length 를 변경할 수 있는 zoom 렌즈 사용해야함
실제로 렌즈의 두꼐를 컨트롤하는 것이 아님. 렌즈 여러개를 중첩시켜 조절
결국 많은 렌즈가 들어가 무거워짐 > 실용성 낮아짐

- 렌즈 자체를 deformable 한 물체로 만든다
ex) 풍선에 물을 채우기


