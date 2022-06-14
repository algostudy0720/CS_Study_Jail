# Blocking/Non-blocking & Synchronous/Asynchrounous

Blocking 과 Synchronous 둘이 비슷하고 Non-blocking과 Asynchrounous 둘이 비슷함

### Blocking/NonBlocking

Blocking/NonBlocking은 호출되는 함수가 바로 리턴하느냐 마느냐가 관심사이다

Blocking은 호출한 함수가 자신의 작업을 모두 마칠 때까지 호출한 함수에게 제어권을 남겨주지 않고 대기하게 만든다. NonBlocking은 호출한 함수가 다른 일을 할 수 있는 기회를 줄 수 있으면 NonBlokcing이다.

### Synchronous/Asynchronous

Synchronous/Asynchronous는 호출되는 함수의 작업 완료 여부를 누가 신경쓰냐가 관심사이다.

호출되는 함수에게 callback을 전달해서, 호출되는 함수의 작업이 완료되면 호출되는 함수가 전달받은 callback을 실행하고, 호출하는 함수는 작업 완료 여부를 신경쓰지 않으면 Asynchronous이다.

호출하는 함수가 호출되는 함수의 작업 완료후 리턴을 기다리거나, 또는 호출되는 함수로부터 바로 리턴 받더라도 작업 완료 여부를 호출하는 함수 스스로 계속 확인하며 신경쓰면 Synchronous다.

![Untitled](https://user-images.githubusercontent.com/55469012/173499862-5ddc7dfd-497c-4126-9a67-139f5a6cf8b5.png)