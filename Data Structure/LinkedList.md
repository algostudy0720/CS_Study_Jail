# LinkedList

![Untitled](https://user-images.githubusercontent.com/55469012/159224225-7b0a01da-ff4d-450a-8383-56fb69d72e0d.png)

### **종류**

1. 단일 연결 리스트

![Untitled 1](https://user-images.githubusercontent.com/55469012/159224250-af5e59ef-7020-4656-84ac-2a598e0216ca.png)

2. 이중 연결 리스트

![Untitled 2](https://user-images.githubusercontent.com/55469012/159224285-fa8fc978-76e3-48e9-9d7a-7a83bfd4b5f2.png)

3. 단순 원형 연결 리스트

![Untitled 3](https://user-images.githubusercontent.com/55469012/159224296-89e13c10-cd4b-4dd0-9019-9cf4b0cbf0d2.png)

단일 연결 리스트 자바 코드

```jsx
public class Node {

	// 데이터 필드
	String data;
	// 링크 필드
	Node link;

	public Node(String data) {
		super();
		this.data = data;
	}

	public Node(String data, Node link) {
		this(data);
		this.link = link;
	}

	@Override
	public String toString() {
		return "Node [data=" + data + ", link=" + link + "]";
	}

}

public class SinglyLinkedList {

	private Node head;

	// 첫번째 노드로 삽입하기
	public void addFirstNode(String data){
		Node newNode = new Node(data,head);
		head = newNode;
	}

	// 마지막 노드 찾기
	public Node getLastNode() {
		for(Node currNode=head; currNode !=null ; currNode=currNode.link) {
			if(currNode.link ==null) {  // 자신의 뒤에 아무도 없으면 자신이 막내
				return currNode;
			}
		}
		return null;
	}

	// 마지막 노드로 삽입하기
	public void addLastNode(String data) {

		if(head == null) { // 공백리스트
			addFirstNode(data);
			return;
		}

		Node lastNode = getLastNode();
		Node newNode = new Node(data);

		lastNode.link=newNode;
	}

	public void insertAfterNode(Node preNode, String data) {

		if(preNode==null) {
			System.out.println("선행노드가 없어 삽입이 불가능합니다.");
			return;
		}
		Node newNode = new Node(data,preNode.link);
		preNode.link =newNode;
	}

	// data를 데이터로 갖고 있는 처음 맘나는 노드 리턴
	public Node getNode(String data) {

		for(Node currNode=head; currNode !=null ; currNode=currNode.link) {
			if(currNode.data.equals(data)) {
				return currNode;
			}
		}
		return null;
	}

	// target의 이전 노드 찾기
	public Node getPreviousNode(Node target) {
		for(Node currNode=head; currNode !=null ; currNode=currNode.link) {
			if(currNode.link == target) {
				return currNode;
			}
		}
		return null;
	}

	// data를 갖고 있는 첫번째 노드 찾아 삭제
	public void deleteNode(String data) {

		Node targetNode = getNode(data);
		if(targetNode == null) {
			System.out.println("삭제할 노드가 없어서 삭제가 불가능합니다.");
			return;
		}

		Node preNode = getPreviousNode(targetNode);

		if(preNode ==null) { // target이 첫 번째 노드인 상황
			head = targetNode.link;
		}else { // target이 첫번째 노드가 아닌 상황
			preNode.link=targetNode.link;
		}
		targetNode.link=null;
	}
}

```

### 순환 검사

```jsx
public boolean circle(){

        Node rabbit=head;//fast
        Node turtle=head;//slow
        while(rabbit!=null&&rabbit.link!=null){
            rabbit=rabbit.link.link;
            turtle=turtle.link;
            if(rabbit==turtle){
                return true;
            }
        }
        return false;

    }
```

참고 사이트 : [https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=software705&logNo=220530519573](https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=software705&logNo=220530519573)
