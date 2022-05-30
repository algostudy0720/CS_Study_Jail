# TCP 3 Way-Handshake & 4 Way-Handshake

## TCP 3 Way-Handshake
- TCP는 장치들 사이에 논리적인 접속을 성리하기 위하여 사용한다.
- TCP의 접속을 성공적으로 성립하기 위하여 반드시 필요하다.
### 과정 
1. Client -> Server : TCP SYN
2. Server -> Client : TCP SYN ACK
3. Client -> Server : TCP ACK

- 양쪽 모두 데이터를 전송할 준비 되었다는 것을 보장하고, 데이터 전달을 시작하기 전에 한쪽이 다른 쪽이 준비되었다는 것을 알 수 있도록 한다.
![225A964D52F1BB6917](https://user-images.githubusercontent.com/55469012/170932347-89a7708d-6a51-44f0-ac58-5e1d1fd169f3.png)

1. 클라이언트는 에 접속을 요청하는 SYN 패킷을 보낸다. 클라이언트는 SYN을 보내고 SYN+ACK 응답을 기다리는 SYN-SENT 상태가 된다.
2. 서버는 SYN 요청을 받고 클라이언트에게 요청을 수락한다는 ACK 와 SYN flag가 설정된 패킷을 발송하고 클라이언트가 ACK로 응답하기를 기다린다. 서버는 SYN-RECEIVED 상태가 된다.
3. 클라리언트는 서버에게 ACK를 보내고 이후로부터는 연결이 이루어지고 데이터가 오간다. 이 때 서버 상태가 ESTABLESD이고 위와 같이 통신하는 것이 신뢰성이 있는 연결을 해주는 TCP의 3 Way Handshake 방식이다.

### TCP 4 Way-Handshake
![2152353F52F1C02835](https://user-images.githubusercontent.com/55469012/170933119-bf9892f3-7644-420c-bd4b-b0d3a3de9ef0.png)

- 4 Way Handshake는 세션을 종료하기 위해 수행되는 절차이다.

1. 클라이언트가 연결을 종료하겠다는 FIN 플래그를 전송
2. 서버는 확인 메세지를 보내고 자신이 통신이 끝날 때까지 기다리는 데 이 상태를 CLOSE-WAIT이라 한다.
3. 서버는 통신이 끝났으면 연결이 종료되었다고 FIN플래그를 클라이언트한테 보낸다.
4. 클라이언트는 ACK를 서버에게 전송하고 TIME-WAIT 상태 이 후 닫히게 된다.