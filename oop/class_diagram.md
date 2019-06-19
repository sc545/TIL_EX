Class Diagram

Dependency 의존

Dependency는 클래스 A가  가진 메소드들에서 클래스 B를 참조함을 의미한다. 또한 B의 메소드들을 참조할 수 있음을 의미한다.
영어로는 'A' depends on 'B'.

public class A {
	public A(){}
	public void useClassB(B classB) {
		//any operations here.
	}
}

Association 연관 (Dependency Injection ??)

Association은 Dependency 와 비슷하지만 클래스 B 에대해 직접적인 참조를 한다는 것 에서 차이를 둔다. 말인즉,
Dependency 의 경우 메소드 레벨에서 B를 참조하나, Association 같은 경우에는 클래스의 Instance variable 로써 B를 참조한다는 뜻이다.

public class A {
	public A(){}
	B classB;
	public A(B classB) {
		this.classB = classB;
	}
}

Aggregation 집합

Aggregation 은 Association 의 종류 중 한개로, A가 B와 다른 인스턴스들로 이루어진 인스턴스 임을 의미한다.
Aggregation 의 경우에는 A의 파트 인스턴스들(예를 들면 B)이 A로 부터 독립적이기 때문에, A의 소멸시 다른 파트 인스턴스들이 소멸하지 않게된다. 이는 파트 인스턴스들의 생성 또한 A에게서 독립적임을 의미한다.
아래는 자바 예제이다, 예제를 보면 파트 인스턴스 B가 생성된 후, 파라미터로 인스턴스 A에 포함된다

public class A {
	public A(){}
	B classB;
	public A(B classB) {
		this.classB = classB;
	}
	public getB(){
		return classB;
	}
}

Composition 구성

Composition은 다른 종류의 Association이다. 인스턴스 A가 B와 다른 인스턴스들로 이루어진다는 것은 Aggregation 과 같으나,
인스턴스 A의 소멸시, 다른 파트 인스턴스들까지 소멸한다는것이 Aggregation과의 차이이다. 이는 즉 파트 인스턴스들이 A로 부터 독립적이지 않음을 말한다.
또한, Aggregation 과는 달리 파트 인스턴스의 생성은 순수히 인스턴스 A에 맞겨진다
아래는 자바 예제이다. 위의 Aggregation 예제와 달리, 파트 인스턴스 B가 A의 컨스트럭터에 의해 생성된다.

public class A {
	public A(){}
	B classB;
	public A() {
		classB = new B();
	}
}
