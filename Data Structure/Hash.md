# Hash

![Untitled](https://user-images.githubusercontent.com/55469012/159917595-73026e7a-d88f-4f1f-a352-01e38abbcb50.png)

데이터를 다루는 기법 중에 하나로 검색과 저장이 아주 빠르게 진행

Key, Value 한 쌍으로 존재하고 eky 값이 배열의 인덱스로 변환되기 때문에 검색과 저장의 평균적인 시간 복잡도가 O(1)

### Hash Function

key를 **고정된 길이의** hash로 변경해주는 역할

**해시충돌**

서로 다른 key 가 hashing 후 같은 hash값이 나오는 경우

**충돌 해결법**

체이닝  

![Untitled 1](https://user-images.githubusercontent.com/55469012/159917548-e1850652-4e37-4140-8697-8b947449dae4.png)

장점 : 미리 충돌을 대비해서 공간을 많이 잡아 놓을 필요가 없음

단점 : 검색 시 효율이 낮아짐

**개방 주소법**

- 선형 탐색  : 해시값에서 고정폭으로 건너 뛰면서 비어있는 해시가 나오면 저장하게 된다.
- 제곱 탐색 : ****고정폭이 아닌 1칸 -> 4칸 -> 9칸 -> 16칸 씩 건너 뛰면서 빈 칸은 찾는다. 해시값이 같은 해시들이 들어오면 공간을 많이 확보해놔야 한다.