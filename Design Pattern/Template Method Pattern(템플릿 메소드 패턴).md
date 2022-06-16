# Template Method Pattern(템플릿 메소드 패턴)

# 1. Template Method Pattern

- 특정 환경이나 상황에 맞게 확장, 변경할 때 유용한 패턴
- 추상 클래스 + 구현 클래스
    - 추상 클래스(Abstract Class)
        - 메인이 되는 로직 부분은 일반 메소드로 선언
    - 구현 클래스(Concrete Class)
        - 메소드를 선언 후 호출하는 방식
- 장점
    - 구현 클래스에서는 추상 클래스에 선언된 메소드만 사용하므로 핵심 로직 관리 용이
    - 객체 추가 및 확장이 용이
- 단점
    - 추상 메소드가 많아지면 클래스 관리가 복잡해짐
- 설명
    - HouseTemplate.java(추상 클래스)
    
    ```java
    public abstract class HouseTemplate {
    
        // 이런 식으로 buildHouse라는 함수 (핵심 로직)을 선언해 둠.
        public final void buildHouse() {
            buildFoundation();	// (1)
            buildPillars();		// (2)
            buildWalls();		// (3)
            buildWindows();		// (4)
            System.out.println("House is built.");
        }
    
        // buildFoundation(); 정의 부분 (1)
        // buildWalls(); 정의 부분		(2)
    
        // 위의 두 함수와는 다르게 이 클래스를 상속받는 클래스가 별도로 구현했으면 하는 메소드들은 abstract로 선언하여, 정의하도록 함
        public abstract void buildWalls();	// (3)
        public abstract void buildPillars();// (4)
    
    }
    ```
    
    - Template 패턴에서 사용할 추상 클래스 생성
    - 사용 시에는 구현 클래스의 객체로 생성해서 사용
        - HouseTemplate houseType = new WoodenHouse();
    - 내부에 buildHouse() 라는 핵심 로직을 만들어 놓음(핵심 로직 관리)
    - 추상 클래스 내부에서 상속받는 클래스가 핵심 로직 함수를 구현하도록 abstract로 지정
    
    - WoodenHouse.java(구현 클래스)
    
    ```java
    public class WoodenHouse extends HouseTemplate {
        @Override
        public void buildWalls() {
            System.out.println("Building Wooden Walls");
        }
        @Override
        public void buildPillars() {
            System.out.println("Building Pillars with Wood coating");
        }
    }
    ```
    
    - Template 클래스를 상속받는 클래스
    - 구현하는 추상 메소드에 따라 Template 클래스의 내부 핵심 로직이 변경 가능함