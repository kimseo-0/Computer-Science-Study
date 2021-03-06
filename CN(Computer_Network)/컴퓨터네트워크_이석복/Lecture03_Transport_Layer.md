# chapter 3: Transport layer

## 3.1 Intro
> | |  |  |  | |
> |:---:|:---:|:---:|:---:|:---:|
> |App| | Message | | HTTP |
> |Trans| | Segment | | TCP |
> |Net| | Packet | | |
> |Link| | | | |
> |Physic| | | | |

## 3.2 multiplexing and demultiplexing
- multiplexing : handle data from multiple sockets   
application layer 에서 내려온 multiple data 를 하나의 data 로 합치고,
header 를 추가하여 segment 로 만드는 것

- demultiplexing : use header info to deliver received segments to correct socket   
receive 한 segment 에서 header 정보를 통해 
segment 안의 여러 data 를 맞는 socket 에 전달하는 것

### TCP/UDP segment format
- source port #
- destination port #
- other header fields
- application data

### demultiplexing
#### Connectionless demux : UDP
destination IP & destination port 만을 사용해서 demultiplexing 한다.

#### Connection-oriented demux : TCP
source IP & source port
destination IP & destination port 를 사용해서 demultiplexing 한다.

destination IP & destination port 가 동일해도
source IP & source port 가 다르면 다른 소켓으로 들어간다.

## 3.3 connectionless transport : UDP
### UDP(User Datagram Protocol) segment
- source port/destination port > demultiplexing
- length
- checksum > error checking   
> checksum 을 통해 에러를 체크하고
> 만약 에러가 발생 했다면, socket 으로 보내기 전에 drop 함

## 3.4 Reliable Data Transfer Protocol
### 기본 개념
- mechanism for packet error
    - error detection
    - feedback
    - retransmission
    - sequence #
- mechanism for packet loss 
    - time out
### 1
- underlying 에 패킷 에러 없음
- 그냥 보내면 됨
### 2.0 packet error
- underlying 에 패킷 에러 있음

- Error detection
    - add checksum bits
- Feedback
    - Acknowledge
    - Negative feedback

- FSM ???
---
### 2.1
- feedback ACK 에 에러가 발생
- Duplicate packets 발생

- handling duplicate packet
패킷에 번호(seq#)를 붙인다

패킷
헤더 | 데이터
헤더에 seq#을 추가한다
헤더의 정보는 최소화 해야한다
sequence 정보도 최소화 한다

패킷을 하나씩 보내는 상황에서는 seq# 를 0, 1로 표현 가능

---
### 2.2 a NAK-free
ACK(seq#)을 보냄
이때 seq#은 마지막으로 제대로 받은 패킷의 seq#
### 3.0 channel loss & packet error
- Timer
: 일정 timer 동안 feedback 이 없으면 재전송 
> 일정 시간 : 'reasonable' amount
> 타이머의 시간이 너무 짧을 경우 : 필요 없는 재전송이 늘어남 > overhead 발생
> 타이머의 시간이 너무 길 경우 : 실제 loss 를 잡아내지 못할 수 있음

> TCP 가 제공하는 기능들에 필요한 데이터 > 패킷 헤더에 저장하여 전송

> stop-and-wait operation
> 신뢰성은 매우 높지만 성능이 좋지 않다

### pipelined protocols : increased utilization
#### GBN (Go-Back-N)
##### GBN 특징
> window size : 한번에 보낼 패킷 사이즈
> ACK N : N 번 packet 까지 완벽하게 잘 받았다는 의미

##### GBN : sender extended FSM
##### GBN : receiver extended FSM
receiver 는 현재 기다리는 패킷 번호가 제대로 도착할 때까지 기다림
> 데이터 유실 발생시 window 안의 N개의 패킷만큼 돌아와서 다시 send
> N이 클수록 유실 발생시 재전송할 패킷의 양이 늘어남

#### Selective Repeat
##### seletive Repeat 특징
> ACK N : N 번 packet 을 완벽하게 잘 받았다는 의미

> 순서에 맞지 않는 패킷이라도 에러가 없다면 저장함 <br>
> 유실된 패킷만 재전송

##### Selective Repeat dilemma
- seq# 을 얼마나 할것인가 > window size * 2

> sender 에서 모든 패킷에 timer 를 다는 것이 이론적으로는 좋은 방법이지만
> 실질적으로는 오버헤드 발생

## 3.5 connection-oriented transport : TCP
### TCP
#### TCP 특징
- point-to-point <br>
하나의 소켓(P1)과 하나의 소켓(P2) 사이(한쌍의 소켓 사이)의 통신
- reliable, in-order byte
- pipelined
- full duplex data : data 양방향 진행 
> sender/receive buffer 두 가지 모두 가지고 있음 <br>
>    - Sender Buffer(window size) : 재전송 하기 위해서
>    - Receive Buffer(window size) : out of order 로 들어온 패킷의 저장을 위해서

- flow controlled : receiver 가 소화할 수 있는 양만큼 알맞게 데이터 전송
- congestion controlled : 내부 network 상황에 맞춰 알맞게 데이터 전송

#### TCP segment structure
- source port/destination port
- sequence number (seq #)
- ACK (acknowledgement number)
- receive window : 나의 receive window 에 남은 공간
- checksum

##### TCP seq.# and ACK
- seq N : segment data의  제일 첫번째 byte N으로 설정
- ACK N : seq N의 다음 byte, N번 byte를 기대하고, 기다리고 있음
    - cumulative ACK : N - 1 번 byte 까지 잘 받았다는 의미

`그림`

##### timeout = RTT
RTT 값은 매번 다를 수밖에 없음
- 각 segment 의 경로가 다름
- 경로가 동일 해도, 매번 queue delay 가 다름

time out = EstimatedRTT(보정한 RTT)
- 수식을 별로 중요하지 않음 그렇구나 하고 넘기자

#### TCP reliable data transfer
- pipelined segment
- cumulative ack
- TCP use single timer
    - 유실된 하나의 패킷 만 재전송

##### TCP : retransmission scenarios
`그림`

> 📝 TCP ACK 권고 사항
> fast retransmit <br>
> 동일한 ACK N을 세 번 이상 받는 경우 유실 되었다 판단 <br>
> \* 필수는 아님, 최적화 권고 사항

#### TCP flow control
TCP Header 의 receive buffer size 에 
receive buffer 의 available space 를 담아서 sender 에 전송

sender 는 해당 필드를 확인해 전송 데이터 양을 조절

if 만약 receiver buffer 의 available space 가 0byte 라면 <br>
sender 는 receiver buffer 에 공간이 생길 때까지 <br>
계속 빈 data 의 segment 를 전송 <br>

#### TCP connection management
send buffer 와 receive buffer 를 생성
자신이 send 할 seq# 을 생성 후 receiver 에 알림, <br>
상대가 send 한 seq# 을 받음 (receive 할 seq#을 받음)

##### TCP 3-way handshake
###### Opening TCP Connection
1. TCP SYN <br>
TCP Header 의 SYN = 1, 자신의 seq# = x 전송 <br>
상대방에게 connection 하고 싶음을 알림

2. TCP SYNACK <br>
SYN = 1, seq# = y, ACK bit = 1, ACK# = x + 1

3. TCP ACK
SYN = 0, <br>
ACK bit = 1, ACK# = y + 1 <br>
Data 도 함께 전송 가능

`그림`

###### Closing TCP Connection
1. client TCP FIN
2. server TCP FIN

`그림`

> 📝 timed wait <br>
> 마지막 server TCP 의 FIN 에 대한 ACK 가 유실될 경우
> server 는 계속 FIN 을 보내고 종료 할 수 없다.
> 마지막 ACK 가 제대로 도착할 때 까지 기다리는 시간

## 3.6 Principle of Congestion Control
- Network-assisted congestion control : 
network 의 router 가 feedback 제공
- End-end congestion control : 
network 내부의 상황을 알아서 유추, 판단 하는 방식(실제 사용)
 
### End-end congestion control
#### 3 main phases
1. slow start
네트워크 상황을 아직 모르는 상황
보내는 패킷을 늘려가면서 네트워크 상황을 유추
> 늘리는 패킷 양은 linear 보다 더 빠르다

2. additive increase
threshold 를 지나면 linear 하게 증가

3. multiplicative decrease
보내는 양 감소

> TCP Tahoe vs TCP Reno   
> - TCP Tahoe : 보내는 양 1/2
> - TCP Reno : 
> 패킷 유실이 발생하는 두가지 상황에 따라 다르게 동작
> 1. time out : 처음부터 다시 시작(slow start 부터)
> 2. 3 duplicate ACK : 패킷 양 1/2 후 linear 하게 증가 
> time out 이 발생했을 때 3 duplicate ACK
> 보다 네트워크 상황이 더 나쁠 확률이 높기 때문에 

> MSS(Maximum segment size) : 500byte   
> 위에서 증가하는 하나의 단위는 500byte

> 보낼 수 있는 패킷의 양에 따라 윈도우 사이즈가 변경된다
> 즉, 가장 처음 패킷의 양은 1MSS 이므로 윈도우 사이즈도 500byte

> rate = CongWin / RTT (bytes/sec)
> CongWin : dynamic, function of perceived network congestion

#### TCP Fairness
fairness goal : if K TCP sessions share same bottleneck link of bandwidth R, each should have average rate of R/K

##### why is RCP fair?
Tow competing sessions
- additive increase give slope of 1, as throughout increase
- multiplicative decrease decreases throughput proportionally
> 시간이 지날수록 equal bandwidth share 그래프에 수렴한다.