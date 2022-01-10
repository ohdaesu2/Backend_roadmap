OS및 일반적인 지식1
===============

### 터미널 사용 방법
터미널: 컴퓨터와 사용자 간의 서로 소통시켜주는 인터페이스 
> cd <이동할_디렉토리> : 디렉토리 이동  
> cd/ : 최상위 디렉토리  
> cd.. : 하위 디렉토리  
> pwd : 현재 디렉토리 위치 확인  
> ls -a : 숨겨진 파일까지 모두 확인
> ls -l: list 형태로 보여줌  
> cp /example/exFile /example2/exFile : example 폴더의 exFile 을 뒤의 파일로 복사  
> mv /example/exFile /example2/exFile : example 폴더의 exFile 을 뒤의 파일로 이동  
> mkdir <디렉토리 이름> : 디렉토리 생성  
> rmdir <디렉토리 이름> : 디렉토리 삭제  

### OS의 일반적인 작동방식  
Operating System
- computer user와 hardware(CPU, I/O) 사이의 인터페이스 역할 
- OS는 모든 어플리케이션에 대한 인터페이스를 제공하고 자원 관리자로서 CPU, RAM, I/O device등을 관리한다. 
- 운영체제가 하는 일 
  - Process management
  - Memory management
  - Storage management
  - Protection and Security
  - UI

OS가 하는 일 
- 기본적인 동작 원리로 OS는 사용자 요청이 발생하면 적절하게 지원을 분배하여 그 요청을 처리
- OS Loading 
    1) 컴퓨터 전원이 켜지면 CPU는 ROM(Read Only Memory)에 저장된 내용을 읽는다. 
       - ROM에는 POST(Power ON Self-Test)와 부트로더(Boot Loader)가 저장
       - POST : 컴퓨터 전원이 켜지면 가장 먼저 실행되는 프로그램으로 컴퓨터에 이상이 있는 지 체크
       - Boot Loader : 하드디스크에 저장되어 있는 OS 프로그램을 가져와서 RAM에 넘겨주는 역할
    2) CPU는 초기화를 위해 Boot Loader에 모인 명령들을 읽고, Dist(SSD, HDD)에 있는 프로그램들(OS..)을 RAM(Random Access Memory)에 올린다.
    3) 프로그램들이 메모리에 올라오면 CPU가 해당 프로그램을 작동시킨다.

OS 작동방식
- 멀티 프로그래밍
  - 컴퓨터에는 CPU와 다양한 I/O 디바이스들이 존재하는데 CPU에는 단 하나의 프로그램 밖에 올라가지 않는다. 
  - 만약 해결중이던 프로세스가 I/O 대기 상태면 CPU는 놀게 된다. 
  - 이를 해결하기 위해, 메모리에 여러 프로세스들을 올려두고 I/O 대기 상태가 되면 바로 다음 JOB으로 넘어가게 한다.
- 타임 셰어링 or 멀티 테스킹
  - 하나의 job이 끝날 때까지 다른 작업이 CPU를 사용할 수 없다. 
  - CPU가 스케쥴링을 통해 작업들을 빠르게 스위칭 하면서 동시에 프로그램이 작동하는 것처럼 느껴지게 한다. 

- 인터럽트
  - CPU가 job을 처리하고 있을 때, I/O 디바이스 등의 장치나 예외상황이 발생하여 처리가 필요할 경우 신호를 주어 처리할 수 있도록 하는 것을 말한다. 




### 프로세스 관리
프로세스: 메인 메모리에 할당되어 실행되고 있는 프로그램  
프로세스 상태
- New, Ready, Runninf, Waiting, Terminated(종료)  
- 프로세스들은 많지만 프로세스를 처리할 CPU는 하나인 경우가 많기 때문에 상태가 계속 변한다.

PCB(Process Control Block)
- 프로세스에 대한 모든 정보가 모여있는 곳, Task Control Block(TCB)라고도 한다.
- 프로세스의 상태, 프로세스 번호(PID), 해당 프로세스의 program counter(pc), register값, MMU정보, CPU점유 시간 등이 포함
- CPU는 한 프로세스가 종료될 때까지 수행하는 것이 아니라 여러 프로세스를 중간 중간에 바꿔가면서 수행
- 그러므로 CPU는 수행중인 프로세스를 나갈 때, 이 프로세스의 정보를 어딘가에 저장하고 있어야 다음에 이 프로세스를 수행할 때 이전에 수행한 그 다음부터 이어서 작업할 수 있다.
- 이러한 정보를 저장하는 곳이 PCB

프로세스 큐(Queue)
- 프로세스는 상태가 여러번 바뀌는데 이에 따라 서비스를 받아햐하는 곳도 다르다.
- 즉, 프로세스는 줄을 서서 기다려야 한다. 
- 프로세스는 일반적으로 여러 개가 한번에 수행되므로 그에 따른 순서가 필요하고, 이를 Queue라고 부른다. 
  - Job Queue: 하드디스크에 있는 프로그램이 실행되기 위해 메인 메모리의 할당 순서를 기다리는 큐
  - Ready Queue: CPU 점유 순서를 기다리는 큐
  - Device Queue: I/O를 하기 위한 여러 장치가 있는데, 각 장치를 기다리는 큐가 각각 존재한다. 

멀티프로그래밍(Multiprogramming)
- 단일 프로세서(CPU) 환경에서 여러 개의 프로세스가 동시에 실행되는 것을 의미.  

### 스레드와 동시성
Thread : CPU 스케줄링의 기본 단위 또는 한 프로세스 안에서 제어의 흐름
- 각각의 thread는 자신만의 레지스터 상태와 스택을 가진다. 
- 일반적으로 한 프로그램은 하나의 쓰레드를 가지지만, 둘 이상의 쓰레드를 가질 수 있다. 이를 Multithread라 한다. 

Process : 컴퓨터에서 연속적으로 실행되고 있는 컴퓨터 프로그램
- 여러개의 Processor(Process의 인칭화)를 사용하는 걸 Multi-processing라 부른다. 

Parallelism(병렬성) : 애플리케이션에서 작업을 여러 CPU에서 동시에 병렬로 작업할 수 있는 Process 단위로 분할
- 여러 개의 스레드가 있으면 데이터 및 리소스 측면에서 서로 독립적으로 유사한 작업을 처리

Concurrency(동시성): 서로 독립적인 작업을 작은 단위의 연산으로 나누고 시간 분할 형태로 연산하여 논리적으로 동시에 실행되는 것처럼 보여주는 것 
- 논리적인 개념이기 때문에 단일 스레드에서도 사용이 가능한 개념


### 기본적인 터미널 명령어
grep, awk, sed, lsof, curl, wget, tail, head, less, find, ssh, kill

