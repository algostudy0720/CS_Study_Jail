# 1. Stack

- 책처럼 차곡차곡 쌓아 올린 형태의 자료구조
- 같은 구조와 크기의 자료를 탑으로만 쌓을 수 있음
- 가장 마지막에 삽입된 자료가 가장 먼저 삭제됨 ⇒ LIFO(Last In, First Out) 구조
- 탑에서만 자료의 입출력이 가능
- push : 삽입 연산
- pop : 삭제 연산
- 비어있는 Stack에서 pop을 하면 stack underflow 에러
- Stack이 넘치는 경우 stack Overflow 에러
- 활용 예시
    - 웹 브라우저의 방문 기록(뒤로 가기)
    - 역순 문자열 만들기
    - 실행 취소
    - 후위 표시법
    - 수식의 괄호 검사


# 2. Queue

- 줄을 서서 기다리는 것과 같은 형태의 자료 구조
- FIFO(First In, First Out) 방식의 선입 선출형의 자료구조
- 큐의 한 쪽 끝에서는 삭제 연산만 이루어지고 나머지 한 쪽 끝에서는 삽입 연산만 이루어진다.
- 자바의 Collection에서 Queue는 인터페이스이므로 이를 구현한 Priority Queue도 사용이 가능하다.
- front : 삭제 연산(enqueue)
- rear : 삽입 연산(dequeue)
- 활용 예시
    - 우선 순위가 같은 작업 예약
        - 프린터의 인쇄 대기열 등
    - 은행 업무
    - 프로세스 관리
    - BFS
    - Cache 구현 등


# 3. Question

2개의 Stack을 사용하여 Queue를 구현하시오

![Untitled](https://user-images.githubusercontent.com/45481007/159229080-c13483dd-9fd9-43f5-a8c1-2ef482654e5d.png)

1. inBox에 데이터를 삽입(push)한다. → A,B
2. inbox에서 데이터를 추출(pop)하여 outBox에 삽입(push)한다. → B, A
3. outBox에는 데이터가 Queue의 순서로 들어가게 됨

```jsx
import java.util.Stack;

/**
 * created by victory_woo on 2020/05/06
 * Stack 2개를 이용해서 Queue 구현하기.
 */
public class StackWithQueue {
    public static void main(String[] args) {
        StackQueue<String> queue = new StackQueue<>();
        queue.enQueue("A");
        queue.enQueue("B");
        queue.enQueue("C");

        System.out.println(queue.deQueue());
        System.out.println(queue.deQueue());
        System.out.println(queue.deQueue());
    }

    static class StackQueue<T> {
        private Stack<T> inBox;
        private Stack<T> outBox;

        StackQueue() {
            inBox = new Stack<>();
            outBox = new Stack<>();
        }

        void enQueue(T item) {
            inBox.push(item);
        }

        Object deQueue() {
            if (outBox.isEmpty()) {
                while (!inBox.isEmpty()) {
                    outBox.push(inBox.pop());
                }
            }

            return outBox.pop();
        }
    }
}
```

### [출처]

[https://creatordev.tistory.com/83](https://creatordev.tistory.com/83)
