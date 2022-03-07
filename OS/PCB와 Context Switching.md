# PCB와 Context Switching

## PCB ( Process Control Block)

**정의**

-   특정한 프로세스를 관리할 필요가 있는 정보를 포함하는 운영 체제 커널의 자료구조
-   프로세스가 생성될 때마다 고유의 PCB가 생성, 완료되면 PCB도 함께 제거
-   프로세스 상태관리와 문맥 교환(Context Switch)을 위해서 필요

**저장정보**

![Untitled](https://user-images.githubusercontent.com/55469012/156910460-4343604c-5fd9-4d92-bc74-62a24fa2e550.png)

-   Pointer : 부모와 자식 프로세스, 할당한 자원, 프로세스가 위치한 메모리에 대한 포인터
-   Process ID : 프로세스 구분하는 ID
-   Process State : 각 state 들의 상태 저장
-   Program Counter : 다음 명령어의 주소를 저장하는 카운터
-   Register : 누산기, 베이스 , CPU 레지스터 및 범용 레지스터에 있는 정보
-   Memory Limits : 운영 체제에서 사용하는 메모리 관리 시스템에 대한 정보, 페이지 테이블 세그먼트 테이블 등이 포함
-   Opne File Lists : 프로세스를 위해 열린 파일 목록

운영체제는 PCB에 빠르게 접근하기 위해 프로세스 테이블을 사용하여 각 프로세스의 PCB를 관리

![Untitled 1](https://user-images.githubusercontent.com/55469012/156910457-d2dd015e-949b-4148-9ec0-685a79c22eb3.png)

## Context Switching

**Context 란?**

-   OS에서의 콘텍스트란 CPU가 해당 프로세스를 실행하기 위한 프로세스의 정보

**정의**

-   CPU가 현재 실행하고 있는 Task(Process, Thread)의 상태를 저장하고, 다음 진행할 Task의 상태 및 Register 값들에 대한 정보(Context)를 읽어 새로운 Task의 Context 정보로 교체하는 과정
-   CPU가 이전의 프로세스 상태를 PCB에 보관하고, 또 다른 프로세스의 정보를 PCB에서 읽어서 레지스터에 적재하는 과정을 말합니다**.**
-   다중 프로그래밍 시스템에서 CPU가 할당되는 프로세스를 변경하기 위해 현재 CPU를 사용하여 실행되고 있는 프로세서의 상태 정보를 저장하고 제어권을 인터럽트 서비스 루틴(ISR)에게 넘기는 작업

**Context Switching**는 **인터럽트 요청**이 올 때 발생

**Context Switching 과정**

![Untitled 2](https://user-images.githubusercontent.com/55469012/156910459-0a55745b-fc29-4155-afd6-239908fe5838.png)
