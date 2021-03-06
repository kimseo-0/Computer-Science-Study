# Lecture 9

### 4 가상현실을 위한 위치추적 목적
- 시각(청각, 촉각)의 정확한 렌더링을 위해
하늘을 봤을때 하늘을 렌더링
바닥을 봤을때 바닥을 렌더링
내가 어디를 보고 있는지 트래킹해야 함

정확한 트래킹을 위해서는 헤드 트래킹 + 눈 트래킹

- 자연스러운 상호작용 및 사용자 의도 전달을 위해
ex) 핸드 트래킹, 헤드 트래킹도 가능, 전신 트래킹...

### 5 헤드 트래킹
추적 정확도와 속도가 중요
- 추적 오차로 인한 화면 떨림 > 어지러움
- 추적 지연으로 인해 느리게 따라오는 화면 
> 현실감 떨어짐

### 6
3 DOF/6 DOF

### 7
outside-in 추적 / inside-out 추적

### 9 HMD tracking
view matrix 는 내 눈의 위치를 의미한다.

HMD 를 트래킹하는 것은 눈의 위치가 아닌
나의 머리의 중심점쯤은 트래킹함

결국 view matrix 는 원점에서 눈까지의 거리인 offset 까지 고려해야함

### Translation
구하기 어렵다

translation : 내가 절대적으로 움직인 절대 좌표

절대적으로 움직인 좌표를 알기 위해서는
나를 따라다니는 hmd 만으로는 절대적인 포지션의 이동을 알 수 없다.
hmd가 아닌 따로 떨어진 무언가의 고정된 좌표를 알아야한다.
(ex 외부 카메라, 외부 물체 등)


### Rotation
샘플링 기반의 적분이라서 문제가 발생
각속도가 nonlinear 한 경우 에러가 누적이 되면서 부정확하다(drift 발생)
> 초기값과 변화량을 사용해서 추정하기 때문에 발생

바뀌는 가속도에서 중력가속도만 추출하는 것이 어렵다
중력가속도가 어떤 컴포넌트인지 정확하게 알 수 없다.



#### 18번 문제
 IMU는 GYROSCOPES 와 ACCELEROMETERS 를 사용하여 HMD Rotation 에 대한 추적을 한다. 
 이때, GYROSCOPES 는 측정된 각속도를 적분하여 각도의 변화량을 추출 이전의 값에 변화량을
  더해서 현재 각도를 구하는데, nonlinear 한 각속도를 적분할 때 아날로그적(continuous)인 
  적분이 아닌 샘플링 기반의 적분을 하기 때문에 오차가 발생한다. 
 
초기값에서 변화량을 더해서 추정하는 방식이기 때문에 시간이 지날수록 
더 많은 오차가 생기는 drift 가 발생한다. 

이를 보완하기 위해 ACCELEROMETERS를 활용한다. 
중력 가속도를 활용하면, 중력 가속도는 고정된 방향과 힘을 가지고 있기 때문에,
 중력가속도를 기준으로 회전 정도를 측정할 수 있다. 하지만, 
 측정된 가속도에 내가 움직여서 발생하는 가속도가 포함되기 때문에 
 중력 가속도만 추출하는 것이 거의 불가능하다. 
 즉, Translation이 많으면 내가 움직여서 발생한 가속도 값과 중력에 의해 측정되는 
 가속도 값과 구분이 안되게 되어 추적이 부정확해진다.