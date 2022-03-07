# [OS] CPU 스케줄링

상태: 완료 🙌
작성일시: 2022년 3월 7일 오후 8:13

# 1. 스케줄링

- CPU가 효율적으로 작업할 수 있도록 프로세스(작업)를 배정하는 작업

## 1-1. 스케줄링의 조건

- 오버헤드 감소
- CPU 사용률 증가
- 기아 현상 감소

## 1-2. 스케줄링의 목표

- Batch System
    - 가능한 최대의 양의 일을 수행
    - 시간보다 처리량을 우선으로 함
- Interactive System
    - 빠른 응답시간
    - 적은 대기시간
- Real Time System
    - 기한 맞추기
    

## 1-3. 스케줄링의 종류

### 1-3-1. 선점 스케줄링(Preemptive)

- OS가 CPU의 사용권을 선점할 수 있는 경우
    
     → CPU의 강제 회수가 가능한 경우(OS가 CPU가 작업 중인 프로세스를 멈추고 원하는 작업부터 
    
    먼저 작업시킬 수 있음)
    
    - 처리시간의 예측이 어려움
        
        > Interrupt, I/O, Event Completion, Event Exit, Event 등
        > 

### 1-3-2. 비선점 스케줄링(Nonpreemptive)

- 프로세스 종료 or I/O 등의 이벤트가 있을 때까지 실행을 보장
    - 처리시간의 예측이 용이함
        
        > I/O or Event Wait, Exit
        > 

## 1-4. 프로세스 상태 전이도

![Untitled](%5BOS%5D%20CPU%20%E1%84%89%209d926/Untitled.png)

### 1-4-1. 프로세스의 상태 전이

- 승인(Admitted)
    - 프로세스의 생성이 가능하여 실행할 준비가 완료되었음을 승인한 상태
- 스케줄러 디스패치(Scheduler Dispatch)
    - 준비 상태에 있는 프로세스 중 하나를 선택하여 실행시키는 것
- 인터럽트(Interrupt)
    - 예외, 입출력, 이벤트 등이 발생하여 현재 실행 중인 프로세스를 준비 상태(ready)로 바꾸고 해당 작업을 먼저 처리하는 것
- 입출력 or 이벤트 대기(I/O or Event Wait)
    - 실행 중인 프로세스가 입출력이나 이벤트를 처리해야하는 경우, 입출력/이벤트가 모두 끝날 때까지 대기 상태(waiting)로 만드는 것
- 입출력 or 이벤트 완료(I/O or Event Completion)
    - 입출력/이벤트가 끝난 프로세스를 준비 상태로 전환하여 스케줄러의 선택을 받을 수 있도록 준비 상태(ready)로 이동시키는 것

Q. Waiting과 Ready의 차이?

- ready는 다른 작업이 먼저 수행 중이라서 기다리고 있는 상태
- waiting은 I/O나 다른 이벤트가 발생하기를 기다리고 있는 상태
    
    

# 2. CPU 스케줄링의 종류

## 2-1. 선점 스케줄링

- Priority Scheduling 방식
    - 정적/동적으로 우선순위를 부여하여 우선순위에 따라 처리
    - 우선순위가 낮은 프로세스가 무한정 대기하는 문제가 발생할 수 있음 → Starvation
    - Aging 방법으로 Starvation 문제 해결 가능
- Round Robin 방식
    - FCFS(First Come First Served)에 의해 프로세스들이 보내지면 각 프로세스들은 동일한 시간(Time Quantum)만큼 CPU를 할당받음
    - TimeQuantum이 크면 FCFS와 다를 바 없고 작으면 Context Switching이 자주 발생하여 오버헤드가 증가한다.
- Multi Level Queue(다단계 큐) 방식
    - 작업들을 여러 종류의 그룹으로 나누어 여러 개의 큐를 이용하는 방식
    - 우선순위가 낮은 큐들이 Starvation에 빠지지 않도록 각 큐마다 다른 Time Quantum을 설정
    - 우선순위가 높은 큐는 빠른 응답을 위해 작은 Time Quantum, 우선순위가 낮은 큐는 큰 Time Quantum을 설정
    
    ![Untitled](%5BOS%5D%20CPU%20%E1%84%89%209d926/Untitled%201.png)
    
- Multi Level Feedback Queue(다단계 피드백 큐)
    - 다단계 큐에서 자신의 Time Quantum을 다 채운 프로세스는 TimeQuantum이 더 긴 하위 큐로 내려가고 자신의 TimeQuantum을 다 채우지 못한 프로세스는 원래 큐 그대로
        - Time Quantum을 다 채우고도 작업을 못끝냈다면 CPU의 부하가 높은 CPU Burst 프로세스로 판단하기 때문
    - 짧은 작업에 유리, 입출력 위주(Inturrupt가 잦은) 작업에 우선권을 줌
    - 처리시간이 짧은 프로세스를 먼저 처리하므로 Turn Around의 평균시간을 줄여줌
    
    ![Untitled](%5BOS%5D%20CPU%20%E1%84%89%209d926/Untitled%202.png)
    
    - 예를 들어 작업량이 15인 작업 P를 우선순위 0인 큐에서 QT가 3으로 작업중에 입출력이 발생하면 작업 P는 같은 큐에 머무르고 3만큼의 작업을 했지만 12의 작업량이 남아있으므로 하위 큐로 이동한다.

## 2-2. 비선점 스케줄링

- FCFS(First Come First Served) 방식
    - Ready 큐에 도착한 순서대로 CPU가 할당 됨
    - 작업 시간이 짧은 작업이 뒤로 들어오면 대기 시간이 길어짐
- SJF(Shortest Job First) 방식
    - 수행시간이 짧은 순서대로 작업을 먼저 수행
    - FCFS 방식보다 평균 대기 시간은 감소, 수행 시간이 짧은 작업에 유리
- HRN(Highest Response ratio Next) 방식
    - 우선순위를 계산하여 점유 불평등을 보완하는 방식
        - 작업시간이 긴 작업이라면 자기 작업이 가장 짧은 작업이 될 때까지 대기해야하는 문제
    - 우선순위 = (대기시간 + 실행시간) / (실행시간)

# 3. CPU 스케줄링의 효율성 판단

- Response Time(응답 시간)
    - 작업이 처음 실행되기까지 대기 시간
- Turnaround Time
    - 실행 시간 + 대기 시간
    - 작업이 완료될 때까지 걸린 시간
    

## [출처]

이미지 출처

- [https://jhnyang.tistory.com/156](https://jhnyang.tistory.com/156)
- [https://jhnyang.tistory.com/7](https://jhnyang.tistory.com/7)