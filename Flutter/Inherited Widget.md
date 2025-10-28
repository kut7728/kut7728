### **InheritedWidget**

- 위젯 트리에서 **하위 위젯들에게 데이터를 효율적으로 전달**하기 위한 위젯
- 트리 위쪽에서 데이터를 제공하고, 하위 위젯들이 BuildContext를 통해 쉽게 접근할 수 있게 해줍니다.
- 대표적인 예시가 **Theme.of(context)** 나 **MediaQuery.of(context)**에요.

  

1. inheritedWidget 상속

  

  

# buildContext

- BuildContext : 위젯트리상의 위젯의 위치에 관한 정보를 담고있는 참조 객체
- context : buildContext 타입의 인스턴스

  

# of 함수

- 현재 위젯의 위쪽 방향으로 가장 가까운 위젯을 찾는 함수
- Scaffold.of(context) 현재 context기준에서 위쪽방향으로 가장 가까운 Scaffold 찾기
- cost가 많이 드는 함수 → 대신 global key 이용하는 편