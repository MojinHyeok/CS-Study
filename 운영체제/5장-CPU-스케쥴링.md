## **CPU 스케줄링**

![img](https://blog.kakaocdn.net/dn/cNOMRO/btryig3jaWU/YYuMqCD5enzJnm9X7RMU3k/img.png)

프로그램의 실행은 cpu만 연속적으로 쓰는 단계, I/O만 쓰는 단계로 나뉘어 실행됩니다.

CPU burst -> CPU만 연속적으로 쓰는 단계

I/O burst ->I/O만 쓰는 단계

프로그램의 종류에 따라 **CPU만 쓰는 프로그램**(ex 과학 계산용 프로그램), **CPU와 I/O를 번갈아 쓰는 프로그램** 등 다양한 종류의 프로그램이 존재합니다.

 

## **CPU-burst Time의 분포**

![img](https://blog.kakaocdn.net/dn/uWux1/btryfjlXljD/yD1hr6pUCxLdcnMWKK9pM1/img.png)

**여러 종류**의 job이 섞여 있기 때문에 CPU 스케줄링이 필요하다.

-> 이유 CPU bound job이 오랫동안 CPU를 사용하는 도중에 I/O bound job의 경우 잠깐의 CPU만 사용하면 되는데 적절하게 스케줄링을 하지 않는 경우는 I/O bound job의 경우 계속해서 기다리기만 하는 경우가 존재하기 때문에(I/O는 사람과 상호작용하기 때문에 중요한데 계속 기다리기만 한다면?.. 안 좋다..)

CPU와 I/O장치 등 시스템 자원을 골고루 효율적으로 사용

I/O job의 경우 사람과 상호작용을 하는 job임으로 적절한 반응을 제공할 필요가 있어 CPU 스케줄링이 필요합니다.



I/O bound job -> CPU를 짧게 쓰고 I/O를 받는 작업

CPU bound job -> CPU를 오래 쓰는 작업.

프로세스는 그 특성에 따라 크게 두 가지로 나눕니다.

- I/O bound process
  - CPU를 잡고 계산하는 시간보다 I/O에 많은 시간이 필요한 job(many short CPU bursts)
- CPU_bound process
  - 계산 위주의 job(few very long CPU bursts)

## **CPU Scheduler & Dispatcher**

**CPU Scheduler**

- Ready 상태의 프로세스 중에서 이번에 CPU를 줄 프로세스를 고른다.
- OS 안에서 CPU 스케줄링하는 코드가 존재해서 그걸 CPU Schduler이라고 합니다.

**Dispatcher**

- CPU의 제어권을 CPU scheduler에 의해 선택된 프로세스에게 넘긴다
- 이 과정을 문맥 교환이라고 합니다.

CPU Scheduler(누구에게 줄지 결정) Dipatcher(CPU에게 실제로 주는 과정)



CPU 스케줄링이 필요한 경우

- CPU를 잡고 있다가

   

  오래 걸리는

   

  작업(I/O를 요청하는 경우)을 하는 경우 CPU를 오래 가지고 있어도 의미가 없으므로 자진해서 CPU를 반납하는 경우(자진반납)

  - Running -> Blocked (예: I/O 요청하는 시스템 콜) 

- CPU를 빼앗고 다른 프로세스에게 CPU를 넘겨주는 경우(강제) 

  - Running -> Ready( 예 : 할당 시간 만료로 timer interrupt)

- I/O를 요청

   

  완료 후

   

  CPU를 얻고 처리하는 경우(강제)

  - Blocked -> Ready(예 : I/O 완료후 인터럽트)

- 프로세스가 종료하여 새로운 프로세스에게 넘기는 경우(자진반납)

  - Terminate

nonpreemptive(강제로 빼앗기 않고 자진 반납 **비선점**)

preemptive(강제로 빼앗음 **선점**)



## **적절한 스케줄링인가?(성능 척도)**

시스템 입장에서의 성능 척도(CPU 하나 가지고 최대한 일을 많이 시키는 경우)

이용률, 처리량

프로그램 입장에서의 성능 척도(고객 입장 시간을 얼마나 빨리 처리할 수 있느냐)

소요시간, 대기시간, 응답 시간,



- CPU utilization(이용률)
  - 가능한 CPU를 바쁘게 일을 시켜라
- Throughput(처리량)
  - 주어진 시간 동안 몇 개의 작업을 처리했느냐
- Turnaround time(소요시간, 반환시간)
  - CPU를 쓰러 들어와서 다 쓰고 나간 시간
- Wating time(대기시간)
  - CPU를 쓰고자 Ready Queue에 기다리는 시간(대기한 시간의 총합)
- Response Time(응답 시간)
  - Ready Queue에 들어와서 **첫** CPU를 얻기까지 기다리는 시간 

Wating time과 Response time의 차이점은 선점형의 경우 CPU를 사용하다가 뺏길 수 있는데 이러면서 계속 Ready Queue에 들어가게 됩니다. 그러면서 계속 기다리는 시간을 합친 것이 Wating time이고 Response의 경우 맨 처음 CPU를 얻기까지 기다리는 시간을 의미합니다.



## **스케줄링의 종류**

**FCFS(FirstComeFirstServed)**

![img](https://blog.kakaocdn.net/dn/vlk4j/btryd2E1hpn/nWW0k1prYTi3KyeI81uEtk/img.png)최악의 경우

그렇게 썩 효율적이진 않습니다.

처음으로 온 CPU가 길게 가져가 버리면 짧게 쓰는 CPU라도 늦게 온다면 오래 기다리기만 해야 합니다.

![img](https://blog.kakaocdn.net/dn/brwTWl/btrymjFguEN/Bk18qB415H7mu49JTW9l91/img.png)최선의 경우

이렇듯 최악의 경우 최선의 경우의 차이가 크게 존재합니다.



**SJF(Shortest_Job-First)**

각 프로세스의 다음번 CPU burst time을 가지고 스케줄링에 활용.

**CPU burst time이 가장 짧은 프로세스를 제일 먼저 스케줄링.**

**SJF는 대기시간이 제일 짧습니다.(이 경우는 선점을 활용한 경우입니다.)**

SJF의 경우 두 가지 방법으로 나뉠 수 있습니다.

비선점을 활용한

일단 CPU를 잡으면 이빈 CPU burst가 완료될 때까지 CPU를 선점당하지 않음

선점을 활용한

현재 수행 중인 프로세스의 남은 burst time보다 더 짧은 CPU burst time을 가지는 새로운 프로세스가 도착하면 CPU를 빼앗깁니다.

이 방법을 SRTF(Shortest-Remaining-Time-First)라고도 부릅니다.



하지만 SJF의 경우 문제점이 존재합니다.

- Starvation(기아 현상)
  - Burst Time이 긴 경우 계속해서 대기만 해야 하는 경우가 나올 수 있습니다.
- CPU 사용시간을 정확히 알 수 없다.(추정은 가능)
  - 과거의 이력을 통해 burst time을 예측은 가능하지만 정확한 시간을 알 수 없습니다.

**Priority Scheduling**

우선순위가 높은 프로세스에게 CPU를 할당

선점, 비선점의 스케줄링의 방법이 있습니다.

문제점으로는 

SJF와 똑같이 우선순위가 낮은 프로세스의 경우 계속해서 기다리기만 하는 경우가 존재합니다.

해결책으로는

Aging(노화): 시간이 지나면서 우선순위가 점차 높아지는 현상으로 위와 같은 문제를 해결합니다.



**Round Robin(RR)**

현대적인 컴퓨터 시스템에서 사용되는 시스템은 RR에 기반하고 있습니다.

CPU를 줄 때 각 프로세스마다 동일한 크기의 할당 시간을 가집니다.

할당 시간이 지나면 프로세스는 선점당하고 ready quee의 제일 뒤에 가서 다시 줄을 서게 됩니다.



RR의 장점으로서는 응답 시간을 최소화할 수 있습니다.

I/O의 경우 짧게 CPU를 사용하면 되는데 RR의 경우 잘 작동될 수 있습니다.



Example: 시간을 20으로 나누어 사용되는 경우

![img](https://blog.kakaocdn.net/dn/LU8Gb/btryhOGyxe1/0UlNtSYzdd15SSj2O6TSJk/img.png)



Ready Queue는 한 줄로 줄서기인데 아래의 경우는 여러 줄로 줄서기입니다.

## **Multilevel Queue**

![img](https://blog.kakaocdn.net/dn/boRCAg/btryk1LGDUg/9O0dQcp0uaF1Lck4u4Mpo0/img.png)

계급제로 진행..

- Ready queue를 여러 개로 분할
  - foreground(interactive)
  - background(batch -no human interaction)
- 각 큐는 독립적인 스케줄링 알고리즘을 가짐
  - foreground- RR
  - background - FCFS
- 큐에 대한 스케줄링이 필요
  - Fixed priority scheduling(starvation의 발생 가능성..)
  - Time slice
    - 각 큐에 CPU time을 적절한 비율로 할당
    - 전체의 80%는 우선순위가 높은 곳에 20%는 우선순위가 낮은 곳에 배치.

## **Multilevel Feedback Queue**

![img](https://blog.kakaocdn.net/dn/bTcfMl/btrye3R9YzQ/cnZVc31fA0SCKEP3OaBPpK/img.png)

위 스케줄링의 경우 계급제로 진행되더라도 계급이 상승되거나 하락할 수 있는 가능성이 있는 스케줄링입니다.

Multi-Level Queue를 보완한 방식

프로세스가 다른 큐로 이동 가능

Multilevel Feedback Queue의 경우 고려해야 할 사항이 존재합니다.

Queue를 몇 개 둘 것인가.

어떻게 강등시키고 승급시킬 것인가.

어떤 스케줄링을 사용할 것인가

처음 프로세스가 들어갈 때 어느 Queue로 들어갈 것인가?..



보통 진행을 할 때 처음 들어오는 프로세스는 가장 우선순위가 높은 프로세스가 삽입을 시킵니다.

그리고 RR으로 quantum을 점차 길게 Queue를 두게 됩니다. 그리하여 프로세스가 삽입되었을 때 시간이 초과되면 아래의 RR으로 강등시키는 과정을 반복합니다.

![img](https://blog.kakaocdn.net/dn/mIFYg/btryf1mlebC/tEQzuFwykNbwgaezNeh2Xk/img.png)

그리하여 이 방식은 CPU 사용시간이 짧은 프로세스에게 우선순위를 높게 주는 스케줄링입니다.



아래의 방식은 CPU가 여러 개인 경우입니다.

## **Multiple-Processor Scheduling**

CPU가 여러 개인 경우 스케줄링은 더욱 복잡해짐

(은행원이 한 명이었다가 여러 명으로 늘어난 경우)

- Homogeneous processor인 경우 
  - 반드시 특정 프로세서에서 수행되어야 하는 프로세스가 있는 경우는 문제가 복잡해짐
  - ex) 여러 미용사가 있는데 특정 미용사에게 커트를 해야 하는 경우
- Load Sharing
  - 일부 프로세서에 job이 몰리지 않도록 부하를 적절히 공유하는 메커니즘이 필요
  - 특정 CPU만 일하는 것을 방지해야 한다
- Symmetric Multiproccessing(SMP)
  - 각 프로세서가 각자 알아서 스케줄링 결정
- Asymmetric multiprocessing
  - 하나의 프로세서가 시스템 데이터의 접근과 공유를 책임지고 나머지 프로세서는 거기에 따름
  - 하나의 CPU가 안내자 역할을 하는 것 

## **Real-Time Scheduling**

#### 실시간 운영체제(Real-Time Operating System, RTOS)

- 개념 : 제한된 시간 내에 원하는 작업을 처리하는 것을 보장하는 운영체제

Real-Time Job(데드라인이 있는 잡)은 처리를 완료하는 것이 목적입니다.



- Hard real-time systems
  - 정해진 시간 안에 반드시 끝내도록 스케줄링해야 함
  - 요구사항이 엄격합니다.
  - 업무는 마감 기한까지 완료되어야 한다.
    - ex) 우주선: 조금만 잘못 계산해도 궤도가 달라짐.
- Soft real-time computing 
  - 일반 프로세스에 비해 높은 priority를 갖도록 해야 함.
  - 중요한 프로세스가 중요하지 않은 프로세스보다 선호된다는 점만 보장한다.
    - ex) 전화기 : 통화 중 음성 끊김.

## **Thread Scheduling**

Thread의 종류로서는 크게 User level thread와 Kernel level thread가 존재합니다

User -> 유저가 임의로 생성하여 OS가 thread의 존재를 모름

kernel -> OS가 thread의 존재를 인지함.

그리하여 종류가 다르기 때문에 그에 맞는 스케줄링이 필요함.

- Local Scheduling
  - User level thread의 경우 사용자 수준의 thread library에 의해 어떤 thread를 스케줄 할지 결정(os가 하는것이 아니라 사용자 프로세스가 직접 결정)
- Global Schedulign
  - kernel level thread의 경우 일반 프로세스와 마찬 가지로 커널의 단기 스케줄러가 어떤 thread를 스케줄할지 결정



## **스케줄링이 좋은지 평가 방법**

- Queueing model
  - 도착률과 처리율을 통해 각종 수식을 통해 값을 계산 이론적인 방법
- implementation(구현) & Measurement(성능 측정)
  - 실제 시스템에 알고리즘을 구현하여 실제 작업(workload)에 대해서 성능을 측정 비교
- Simulation(모의실험)
  - 알고리즘을 모의 프로그램으로 작성 후 trace를 입력으로 하여 결과 비교