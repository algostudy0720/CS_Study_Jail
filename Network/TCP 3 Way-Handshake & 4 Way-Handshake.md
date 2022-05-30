# TCP 3 Way-Handshake & 4 Way-Handshake

## TCP 3 Way-Handshake
- TCP는 장치들 사이에 논리적인 접속을 성리하기 위하여 사용한다.
- TCP의 접속을 성공적으로 성립하기 위하여 반드시 필요하다.
### 과정 
1. Client -> Server : TCP SYN
2. Server -> Client : TCP SYN ACK
3. Client -> Server : TCP ACK

- 양쪽 모두 데이터를 전송할 준비 되었다는 것을 보장하고, 데이터 전달을 시작하기 전에 한쪽이 다른 쪽이 준비되었다는 것을 알 수 있도록 한다.
![TCP 과정](https://t1.daumcdn.net/cfile/tistory/225A964D52F1BB6917)