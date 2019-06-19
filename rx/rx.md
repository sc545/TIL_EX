리액티브 프로그래밍이란 데이터나 이벤트 변화의 반응에 초점을 맞춘 프로그래밍을 뜻하는 일반적인 용어이다.
-> 리액티브 함수형 프로그래밍이란 무엇인지 짧게 답하자면 동시성과 별렬성 해결이다.
-> 조금 더 풀어 말하면 리액티브 비동기 요구사항을 명령형 방식으로 만들었을 때 나타나는 결과물인 콜백 지옥 문제를 해결하는 것이다.
-> RxJava 를 사용한 리액티브 프로그래밍은 함수형 프로그래밍의 영향을 바탕으로 리액티브 명령형 방식의 전형적인 위험 요소를 회피하기 위한 선언적 접근을 사용한다.


리액티브 익스텐션(Rx, RxJava)이 함수형 프로그램밍의 영향을 받았다고 해서 '함수형 리액티브 프로그래밍(functional reactive programming, FRP)'은 아니다.
FRP 는 리액티브 프로그래밍의 매우 특별한 형태로, 연속적인 시간의 흐름을 포함하는 반면 RxJava 는 시간에 대해 불연속적인 이벤트만을 다룬다.

명령형 프로그래밍 vs 함수형 프로그래밍(선언형 프로그래밍)

https://github.com/funfunStudy/study/wiki/%EB%AA%85%EB%A0%B9%ED%98%95-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D%EA%B3%BC-%ED%95%A8%EC%88%98%ED%98%95-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D-%EB%B9%84%EA%B5%90

https://sungjk.github.io/2017/07/17/fp.html

함수형 프로그래밍이라는 유령
http://www.cnet.co.kr/view/18272

->

명령형에 찌든 구식 개발자 입장에서 보건데 함수형 프로그래밍이 부상되는 동인은 분명히 multi-core crisis 때문입니다.??

명령형 언어 -> 절차형 언어 -> 모듈화 -> OOP로 진화하는 과정이 software crisis에 대한 반응 때문이었다면, 무어의 법칙이 깨지고 숙명적으로 애플리케이션이 동시성을 다뤄야 하는 상황에 그 복잡성을 다루려면 함수형에서 추구하는 부작용 없는(side effect free) 프로그래밍이 필요해진 것이지요

언제 리액티브 프로그래밍이 필요한가
- 마우스 움직임이나 클릭, 키보드 타이핑, GPS 신호, 자이로스코프 신호, 터치 이벤트 등을 처리할 때
- (요청이 시작되고 일정 시간이 지난 후 응답 여부에 따라 다른 작업이 진행되는) 본질적으로 비동기성을 띠는 디스크나 네트워크 등 지연 바인딩 I/O 이벤트 응답.
- 서버의 시스템, 이벤트나 앞서 나온 사용자 이벤트, 하드웨어 신호, 각종 아날로그 세선의 이벤트 트리거링(triggering) 등 통제 불가능한 애플리케이션에서 발생하는 이벤트나 데이터를 다룰 때


스트림(Stream) 이란?
- 일반적으로 데이터, 패킷, 비트 등의 일련의 연속성을 갖는 흐름을 의미
-> 음성, 영상, 데이터 등의 작은 조각들이 하나의 줄기를 이루며 전송되는 데이터 열

Observable
- 데이터나 이벤트 스트림을 나타탬.
- push(지향), pull 방식 모두 사용 가능.
- 즉시 동작 하지 않고 지연 실행 됨.
- 비동기, 동기 방식 모두 사용 가능.
- 시간에 따라 0, 1, 다수 혹은 무한 개를 아우르는 이벤트를 다룰 수 있음.

interface Observable<T> {
	Subscription subscribe(Observer s)
}

- onNext 함수를 통한 데이터
-> 0, 1, 다수 혹은 무한 번 호출될 수 있음.

- onError 함수를 통한 오류(Exception 혹은 Throwable)
- onCompleted 함수를 통한 스트림 완료 통보
-> 종료 이벤트로, 둘 중 하나만 단 한번 호출됨.
-> 무한 스트림이고 실패하지 않는 경우에는 onError 와 onCompleted 에서 종료 이벤트가 발생하지 않음.

interface Oberserver<T> {
	void onNext(T t)
	void onError(Throwable t)
	void onCompleted()
}

interactive pull 을 지원하는 추가적인 타입 시그니처가 있다.

interface Producer {
	void request(long n)
}

이는 Subscriber 라 부르는 조금 더 발전된 Observer 와 함꼐 사용한다.
interface Subscriber<T> implements Observer<T>, Subscription {
	void onNext(T t)
	void onError(Throwable t)
	void onCompleted()
	...
	void unsubscribe()
	void setProducer(Producer p)
}

- unsubscribe 함수는 Subscription 인터페이스의 일부분으로 Observable 스트림 구독을 끊을 때 사용한다.
동시성 vs 병렬성

http://atin.tistory.com/567

https://huns.me/development/2051
