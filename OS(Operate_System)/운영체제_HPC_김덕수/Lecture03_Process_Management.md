# 프로세스

## Job vs Process
### Job / program
- 실행 할 프로그램 + 데이터
- 컴퓨터 시스템에 실행 요청 전의 상태

### Process
- 실행을 위해 시스템(커널)에 등록된 작업
- 시스템 성능 향상을 위해 커널에 의해 관리됨

### 그림

## 프로세스 정의
- 실행중인 프로그램
  - 커널에 등록된 잡, 커널의 관리하에 있는 작업
  - 각종 자원들을 요청하고 할당 을 수 있는 개체
    - 프로세스 관리 블록을 할당 받은 개체
    - 능동적인 개체
      -  실행 중에 각종 자원을 요구 할당 반납하며 진행
> Procss Control Block(PCB)
> 커널 공간 내에 존재
> 각 프로세스들에 대한 정보를 관리

## 프로세스의 종류
- 역할에 따른 분류
  - 시스템(커널) 프로세스
  - 사용자 프로세스
- 병행 수행 방법에 따른 분류
  - 독립 프로세스
  - 협력 프로세스

## 자원의 개념
커널의 관리 하에 프로세스에게 할당/반납 되는 수동적 개체

- 자원의 분류
  - HW resource : processor memory disk
  - SW resource : message signal file

## Process Control Block(PCB)
프로세스를 제어하기 위해 필요한 정보를 모아두는 공간

- OS가 프로세스 관리에 필요한 정보 저장
- 프로세스 생성 시 생성 됨
- 커널이 관리하는 메모리 영역에 저장

### PCB가 관리하는 정보
- PID : process Identification Number
- 스케쥴링 정보 > 추후 추가
- 프로세스 상태
- 메모리 관리 정보
- 입출력 상태 정보
- 문맥 저장 영역(context save area) > 추후 추가
- 계정 정보

- PCB 정보는 os별로 서로 다름
- PCB 참조 및 갱신 속도는 OS성능을 결정하는 중요한 요소 중 하나

## 프로세스 상태 (Process States)
여러가지 상태를 거치면서 작업을 수행한다
프로세스 상태 : 자원 간의 상호작용에 의해 결정

- 프로세스 상태 및 특성 표

### Process State Transition Diagram
#### Created State
- 작업을 커널에 등록
- PCB 할당 및 프로세스 생성
- 커널
  - 가용 메모리 공간 체크 및 프로세스 상태 전이
  - memory allocated > ready
  - waiting memory allocation > suspended ready

#### Ready State
- 프로세서 외 다른 모든 자원을 할당 받은 상태
- 프로세서(CPU)만 할당 받으면 즉시 실행 가능 상태

- cpu를 할당 받으면
- dispatch(schedule) > running state

#### Running State
- 프로세서와 필요한 자원을 모두 할당 받은 상태
- 작업을 실행하는 상태

- Preemption : 할당 받은 프로세스(cpu)를 뺏김 > ready state
  - time - out, priority change로인해서 발생
- Block/Sleep : I/O등 자원 할당 요청으로 대기 > asleep 

#### Blocked/Asleep State
- 프로세서 외에 다른 자원을 기다리는 상태
  - 자원 할당은 system call에 의해 이루어짐

- 다른 자원이 도착 했다면, wakeup > ready로 가서 다음 cpu할당을 기다림
  - 다른프로세스가 작업중일 수 있기 때문에 running으로 가지 않음

#### Suspended State
- suspended ready
  - 메모리를할당 받지 못한(빼앗긴) 상태
- suspended blocked
  - blcoked 상태에서 메모리까지 빼앗긴 상태 
- memory image를 swap device에 보관
  - 프로세스가 작업을 하던 중 메모리를 빼앗기게 된다면? 
  - 현재까지 했던 작업 기록이 사라질 수 있음
  - 다시 프로세스가 작업을 하게 된다면 처음부터 다시 해야함 > 매우 비효율적
  - 메모리 이미지를 저장하여 작업 내용을 저장    
> swap device : 프로그램 정보 저장을 위한 특별한 파일 시스템 
- swap-out > suspended
- swap-in > resume, active

#### Terminated/Zombie State
- 프로세스 수행이 끝난 상태
- 모든 자원 반납 후
- 커널 내에 일부 PCB 정보만 남아 있는 상태
  - 프로세스 관리를 위해 정보 수집 
    - 이 프로세스가 어떤 자원을 주로 요청했는지 어떤 일을 했는 등에 대한 정보
  - 커널의 정보 수집이 끝나면 해당 프로세스를 삭제 한다 

## 프로세스 관리를 위한 자료구조
- ready state
  - ready Queue : ready 프로세스가 줄서 있는 공간 > scheduling
- block state : block된 프로세스가 요청한 외부 자원들 리스트
  - I/O Queue
  - Device Queue

## 인터럽트(Interrupt)
- 예상치 못한, 외부에서 발생한 이벤트 (unexpected, external events)
- 인터럽트의 종류
  - I/O
  - Clock
  - Console
  - Program check
  - Machine check
  - Inter-process interrupt
  - System call  
 
### 인터럽트 처리 과정
## Context Switching(문맥 교환)
> context
> 프로세스와 관련된 정보들의 집합
> In CPU > CPU register context
> In Memory > Code & data, Stack, PCB

- Context saving
- contet restoring
- context swiching ≌ Process switching

### Context Switching Overhead
- Context switching에 소요되는 비용
- 불필요한 Context switching을 줄이는 것이 중요
