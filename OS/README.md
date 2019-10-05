# OS
## 스케줄러
#### 프로세스를 스케줄링하기 위한 Queue
- Job Queue : 현재 시스템 내에 있는 모든 프로세스의 집합
- Ready Queue : 현재 메모리 내에 있으면서 CPU를 잡아서 실행되기를 기다리는 프로세스의 집합
- Device Queue : Device I/O 작업을 대기하고 있는 프로세스의 집합

#### 장기 스케줄러 (Long-term Scheduler, Job Scheduler)
- 대용량 메모리에 임시로 저장되어있는 프로세스 중 어떤 프로세스에 메모리를 할당하여 ready queue로 보낼지 결정하는 역할
- 메모리와 디스크 사이의 스케줄링 담당
- 프로세스에 memory 할당
- degree of Multiprogramming 제어
- 프로세스의 상태 : new => ready (in memory)
- time sharing system에서는 장기 스케줄러가 없음. 그냥 바로 메모리에 올라가 ready 상태가 된다.
#### 단기 스케줄러 (Short-term scheduler or CPU scheduler)
- CPU와 메모리 사이의 스케줄링 담당
- Ready Queue에 존재하는 프로세스 중 어떤 프로세스를 running 시킬지 결정
- 프로세스에 CPU를 할당 (scheduler dispatch)
- 프로세스의 상태 : ready => running => waiting => ready
#### 중기 스케줄러 (Medium-term scheduler or Swapper)
- 여유 공간 마련을 위해 프로세스를 통째로 메모리에서 디스크로 쫓아냄 (swapping)
- 프로세스에게서 memory 할당 해제
- degree of Multiprogramming 제어
- 현 시스템에서 메모리에 너무 많은 프로그램이 동시에 올라가는 것을 조절하는 스케줄러
- 프로세스의 상태 : ready => suspended (stopped)

## CPU 스케줄러
### 1. 비선점 스케줄링
비효율적, 비양보. 프로세스에게 이미 할당된 CPU를 강제로 빼앗을 수 없고, 사용이 끝날 때까지 기다려야 하는 방법
- 일괄처리에 적합
- 실시간 처리가 안되므로 중요한 작업이 기다리는 경우 발생
#### FCFS (First Come First Served)
Ready Queue에 도착한 순서에 따라 CPU 할당
- 장점  
  공평성 유지
- 문제점  
  convoy effect. 소요 기간이 긴 프로세스가 먼저 도달하여 효율성을 낮춤
#### SJF (Shortest-Job-First)
실행시간이 가장 짧은 프로세스에 먼저 CPU를 할당
- 장점  
  가장 적은 평균 대기시간을 제공하는 최적의 알고리즘
- 문제점  
  starvation. 특정 프로세스가 지나치게 차별 받음. 사용시간이 긴 프로세스는 거의 영원히 CPU를 할당받을 수 없음
#### HRN (Hightest Response-ratio Next)
`우선순위 = (대기시간 + 서비스 시간) / 서비스 시간`
실행 시간이 긴 프로세스에 불리한 SJF 기법을 보완하기 위한 것. 대기시간이 길수록 우선순위가 높게 나옴

### 2. 선점 스케줄링
우선 순위가 높은 다른 프로세스가 할당된 CPU를 강제로 빼앗을 수 있는 방법
- 실시간 처리, 대화식 시분할 시스템에 사용됨
- 선점으로 인한 많은 오버헤드를 초래함
#### SRT (Shortest Remaining time First)
SJF 스케줄링을 선점 형태로 변경한 기법으로, 현재 실행중인 프로세스의 남은 시간과 준비상태 큐에 새로 도착한 프로세스의 실행 시간을 비교하여 가장 짧은 실행 시간을 요구하는 프로세스에게 CPU 할당
- 문제점  
  1. starvation
  2. 새로운 프로세스가 도달할 때마다 스케줄링을 다시하기 때문에 CPU 사용시간을 측정할 수 없음
#### Round Robin
FCFS 스케줄링을 선점 형태로 변경한 기법으로, Ready Queue에 먼저 들어온 프로세스가 먼저 CPU를 할당받지만 각 프로세스는 할당된 시간 동안만 실행한 후 실행이 완료되지 않으면 다음 프로세스에게 CPU를 넘겨주고 Ready Queue의 가장 뒤로 배치됨
- 장점  
  1. Response time이 빨라짐
  2. 프로세스가 기다리는 시간이 CPU를 사용할 만큼 증가. 공정한 스케줄링
- 문제점  
  할당 시간이 너무 커지면 FCFS와 같아짐. 또 너무 작아지면 잦은 context switch로 ovrhead가 발생함. 적당한 시간을 설정하는것이 중요함!
#### Priority Scheduling
- 선점형  
  더 높은 우선순위의 프로세스가 도착하면 실행중인 프로세스를 멈추고 CPU를 선점
- 비선점형  
  더 높은 우선순위 프로세스가 도착하면 Ready Queue의 Head에 넣음
- 문제점
  1. starvation
  2. 무기한 봉쇄. 실행 준비는 되어있으나 CPU를 사용 못하는 프로세스를 CPU가 무기한 대기하는 상태
- 해결책  
  aging. 아무리 우선순위가 낮은 프로세스라도 오래 기다리면 우선순위를 높여 줌

## 페이지 교체 알고리즘
페이지 부재가 발생했을 때, 가상 기억장치의 필요한 페이지를 주기억장치에 저장해야 하는데, 이 때 주기억장치의 모든 페이지 프레임이 사용중이라면 **어떤 페이지 프레임을 선택하여 교체할지 결정하는 기법**
#### OPT (OPTimal Replacement, 최적 교체)
앞으로 가장 오랫동안 사용하지 않을 페이지를 교체
- 장점 : 가장 낮은 페이지 부재율
- 단점 : 각 페이지의 호출 순서와 참조 상황을 미리 예측해야 하므로 구현이 어려움
#### FIFO (First In First Out)
가장 먼저 들어와서 가장 오래 있었던 페이지를 교체
- 장점 : 쉽고 간단함
- 단점 : `Belady의 모순` 페이지를 저장할 수 있는 프레임의 갯수를 늘려도 되려 페이지 부재가 더 많이 발생하는 모순
#### LRU (Least Recently Used)
최근에 가장 오랫동안 사용하지 않은 페이지를 교체. 최적 알고리즘의 근사 알고리즘. 대체적으로 FIFO 알고리즘보다 우수, OPT 알고리즘보다 그렇지 못함
#### LFU (Least Frequently Used)
사용 빈도가 가장 적은 페이지를 교체
- 단점 : 프로그램 실행 초기에 많이 사용된 페이지가 그 후로 사용되지 않을 경우에도 프레임을 계속 차지할 수 있음
#### NUR (Not Used Recently)
최근에 사용하지 않은 페이지를 교체
