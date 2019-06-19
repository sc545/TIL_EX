1.

Spring
- 초기에 스프링은 EJB 같은 무거운 엔터프라이즈 자바 기술에 대한 대안으로 만들어짐.
- EJB 에 비해 더 가벼운 프로그래밍 모델 -> '자바 개발 간소화'
	= POJO 를 이요한 가볍고(lightweight) 비침투적(non-invasive)인 개발
	= DI 와 인터페이스 지향(interface orientation)을 통한 느슨한 결합도(loose couping)
	= 애스펙트와 공통 규약을 통한 선언적(declarative) 프로그래밍
	= 애스펙트와 템플릿(template)을 통한 반복적인 코드 제거


엔터프라이즈 자바빈즈(Enterprise JavaBeans; EJB)
- 기업환경의 시스템을 구현하기 위한 서버측 컴포넌트 모델이다. 즉, EJB는 애플리케이션의 업무 로직을 가지고 있는 서버 애플리케이션이다.
  EJB 사양은 Java EE의 자바 API 중 하나로, 주로 웹 시스템에서 JSP는 화면 로직을 처리하고, EJB는 업무 로직을 처리하는 역할을 한다.


자바빈 (JavaBean)
- 일반적인 웹사이트는 디자이너와 프로그래머가 협력하여 개발한다. 그런데 프로그래머가 JSP페이지에 자바코드를 입력했을때 디자이너 입장에서는 해석하기 어려워지고 효율또한 매우 떨어지게 된다. 이런 비효율적인 부분을 지원하기위해 제공되는 기능의 형태가 자바빈이다.

JavaBean is just a standard

1.All properties private (use getters/setters)
2.A public no-argument constructor
3.Implements Serializable.

That's it. It's just a convention. Lots of libraries depend on it though....


자바 플랫폼, 엔터프라이즈 에디션(Java Platform, Enterprise Edition; Java EE)
- 자바를 이용한 서버측 개발을 위한 플랫폼이다. Java EE 플랫폼은 PC에서 동작하는 표준 플랫폼인 Java SE에 부가하여,
  웹 애플리케이션 서버에서 동작하는 장애복구 및 분산 멀티티어를 제공하는 자바 소프트웨어의 기능을 추가한 서버를 위한 플랫폼이다.
  이전에는 J2EE라 불리었으나 버전 5.0 이후로 Java EE로 개칭되었다.
  이러한 Java EE 스펙에 따라 제품으로 구현한 것을 웹 애플리케이션 서버 또는 WAS라 불린다.

WAS
-> Web Server + Web Container

Inversion of Controller(제어 역전),
Dependency Injection(의존관계 주입),
Aspect Orient Programming(관점 지향 프로그래밍)

POJO DI Loose Coupling AOP

DI(Dependency Injection)
- 종속객체 주입은 객체가 스스로 종속객체를 획득하는 것과는 반대로 객체에 종속객체가 부여되는 것을 의미한다.
- 결합도가 높은 코드는 한편으로 테스트와 재활용이 어렵고 이해하기도 어려우며, 오류를 하나 수정하면 다른 오류가 발생하는 경향이 있다.
  반면에 전혀 결합이 없는 코드는 아무것도 할 수 없다. 무언가 쓸 만한 일을 하려면 클래스들끼리 어떻게든 서로 알고 있어야 한다.
  결합은 필요하지만 주의해서 관리해야 한다.

- 생성자 주입(constructor injection): 객체 생성 시점에 생성자 인자에 종속객체가 부여된다.
// 종속 객체는 Interface 를 사용하여 여러가지 구현된 객체를 주입 할 수 있게 결합도가 낮게(loose coupling)

// 여기서 잠깐! 그럼 Spring 에서는 어떻게 의존 주입을 하는가? -> 와이어링

와이어링(wiring)
- 애플리케이션 컴포넌트 간의 관계를 정하는 것.
- 스프링에서 컴포넌트를 와이어링하는 방법은 여러 가지가 있지만 가장 일반적인 방법은 XML 을 이용하는 방법이다.
// xml 설정의 대안으로 자바 기반 설정도 제공함.
====================================================================================================================
// 1. 먼저 xml 파일을 통해서 선언
// knights.xml
	<bean id="knight" class="com.example.tempspring.BraveKnight">
		<constructor-arg ref="quest" />
	</bean>

	<bean id="quest" class="com.example.tempspring.SlayDragonQuest">
		<!-- #T(System).out -> Spring Expression Language -->
		<constructor-arg value="#{T(System).out}" />
	</bean>

// 2. ClassPathXmlApplicationContext 클래스로 스프링 컨텍스트를 로드한다.
// KnigtMain.java
	ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("META-INF/spring/knights.xml");
	// 스프링 컨텍스트 로드
	Knight knight = context.getBean(Knight.class);
	// 빈 얻기
	knight.embarkOnQuest();
	context.close();
====================================================================================================================


AOP(Aspect-Oriented Programming)
- 컴퓨팅에서 메인 프로그램의 비즈니스 로직으로부터 2차적 또는 보조 기능들을 고립시키는 프로그램 패러다임이다.

====================================================================================================================
// knights.xml
	<aop:config>
		<aop:aspect ref="minstrel">
			<aop:pointcut id="embark"
				expression="execution(* *.embarkOnQuest(..))"/>

			<aop:before pointcut-ref="embark" method="singBeforeQuest"/>

			<aop:after pointcut-ref="embark" method="singAfterQuest"/>
		</aop:aspect>
	</aop:config>
====================================================================================================================

스프링 컨테이너
- 스프링 기반 애플리케이션에서는 스프링 컨테이너(container) 안에서 객체가 태어나고, 자라고, 소멸한다. 스프링 컨테이너는
  객체를 생성하고, 서로 엮어 주고, 이들의 전체 생명주기를 관리한다.

- 스프링 컨테이너는 스프링 프레임워크의 핵심부에 위치한다. 스프링 컨테이너는 종속객체 주입을 이용해서 애플리케이션을
  구성하는 컴포넌트를 관리하며, 협력 컴포넌트 간 연관간계의 형성도 여기에서 이뤄진다.

- 스프링에는 여러 컨테이너 구현체가 존재하며, 이들은 크게 두 가지로 분류된다. 첫 번째 부류는 빈 팩토리(org.springframework.beans.factory.BeanFactory 인터페이스에 의해 정의)로,
  이는 DI 에 대한 기본적인 지원을 제공하는 가장 단순한 컨테이너다. 두 번째 부류는 애플리케이션 컨텍스트(org.springframework.context.ApplicationContext 인터페이스에 의해 정의)로,
  빈 팩토리를 확장해 프로퍼티(property) 파일에 텍스트 메시지를 읽고 해당 이벤트 리스너(listener)에 대한 애플리케이션 이벤트 발행 같은 애플리케이션 프레임워크 서비스를 제공하는 컨테이너다.

애플리케이션 컨텍스트
- 빈에 관한 정의들을 바탕으로 빈들을 엮어 주며, 애플리케이션을 구헝하는 객체의 생성과 와이어링을 전적으로 책임진다.
- 스프링에는 다양한 종류의 애플리케이션 컨텍스트가 있다. 그중에서 가장 많이 접하게 될 몇가지는 다음과 같다.
	= AnnotationConfigApplicationContext: 하나 이상의 자바 기반 설정 클래스에서 스프링 애플리케이션 컨텍스트를 로드한다.
	= AnnotationConfigWebApplicationContext: 하나 이상의 자바 기반 설정 클래스에서 스프링 웹 애플리케이션 컨텍스트를 로드한다.
	= ClassPathXmlApplicationContext: 클래스패스(classpath)에 위치한 XML 파일에서 컨텍스트 정의 내용을 로드한다.
	= FileSystemXmlApplicationContext: 파일 시스템에서, 즉 파일 경로로 지정된 XML 파일에서 컨테스트 정의 내용을 로드한다.
	= XmlWebApplicationContext: 웹 애플리케이션에 포함된 XML 파일에서 컨텍스트 정의 내용을 로드한다.


2.

빈 와이어링

// 여기서 잠깐! Spring 은 항상 DI 패턴을 이용해야 되나??
-> DI 는 스프링의 가장 밑바탕을 이루는 개념으로서  스프링 기반 애플리케이션을 개발할 때는 언제나 이용하게 되는 기법이다.
-> 이를 보통 와이어링(wiring)이라 한다.

- 세가지 기본적인 와이어링 메커니즘을 제공
	= XML 에서의 명시적 설정 (xml name-space 기능이 JavaConfig 에 없을 경우)
	= 자바에서의 명시적 설정 (type-safe 보장)
	= 내재되어 있는 빈을 찾아 자동으로 와이어링하기 (추천!)


2-1. 자동으로 와이어링하기

- 스프링은 두 가지 방법으로 오토와이어링을 수행한다.

(1) 컴포넌트 스캐닝: 스프링은 애플리케이션 컨텍스트에서 생성되는 빈을 자동으로 발견한다.

====================================================================================================================
// 1. java 로 컴포넌트 스캐닝 활성화하기
// CDPlayerConfig.java
	@ComponentScan("com.example.tempspring.cdplayer")
	public class CDPlayerConfig {
	}
// CDPlayerTest.java
	@ContextConfiguration(classes=CDPlayerConfig.class)
	// @ContextConfiguration 애너테이션은 CDPlayerConfig 클래스를 통해서 설정을 로드한다.
	public class CDPlayerTest {
	}

// 2. xml 로 컴포넌트 스캐닝 활성화하기
// cd.xml
	<context:component-scan base-package="com.example.tempspring.cdplayer" />
====================================================================================================================

-> @ComponentScan 을 사용 -> @Component 클래스를 찾음 -> 스프링이 찾은 클래스를 빈으로 만듦

(2) 오토와이어링: 스프링은 자동으로 빈 의존성을 충족시킨다.

-> SgtPeppers 빈처럼 애플리케이션의 모든 객체가 혼자이고 의존성이 없다면, 컴포넌트 스캔으로 충분하다. 그러나 많은 객체는 일을 처리하기 위해 다른 객체에 의존관계를 가진다.
   의존성을 가지고 컴포넌트 스캔된 빈을 묶기 위한 방법이 필요한데 이를 위해서 자동 스프링 설정의 다른 측면인 오토와이어링이 필요하다.

-> 오토와이어링은 스프링이 빈의 요구 사항과 매칭되는 애플리케이션 컨텍스트상에서 다른 빈을 찾아 빈 간의 의존성을 자동으로 만족시키도록 하는 수단이다.
   오토와이어링 수행을 하도록 지정하기 위해서는 다음 스프링의 @Autowired 애너테이션을 사용한다.

====================================================================================================================
@Autowired
private CompactDisc cd;

-------------------------------------

private CompactDisc cd;

@Autowired
public CDPlayer(CompactDisc cd) {
	this.cd = cd;
}

@Autowired
public void setCompactDisc(CompactDisc cd) {
	this.cd = cd;
}

@Autowired
public void insertDisc(CompactDisc cd) {
	this.cd = cd;
}
====================================================================================================================
-> 생성자나 세터 메소드를 포함한 어떤 메소드이든 스프링은 메소드 파라미터에 의존성을 가진다. 한 개의 빈이 일치하면 그 빈은 와이어링된다.

-> 매칭되는 빈이 없다면 스프링은 애플리케이션 컨텍스트가 생성될 때 예외를 발생시킨다. 예외를 피하기 위해서 @Autowired 에서 required 애트리뷰트를 false 로 설정한다.

====================================================================================================================
@Autowired(required=false)
public CDPlayer(CompactDisc cd) {
	this.cd = cd;
}
====================================================================================================================
-> Required 가 false 일 때, 스프링은 오토와이어링을 시도하지만 매칭되는 빈이 없으면 와이어링되지 않은 상태로 남겨진다.
   이런경우 코드에서 널(null)을 체크하지 않으면, NullPointerException 이 생길 수 있다.
   다중 빈이 의존성을 가질 경우에도 스프링은 오토와이어링을 위한 빈을 선택할 때 애매모호한 경우에는 예외(exception)를 발생한다.

// 오토와이어링을 위한 애너테이션

 		@Autowired 		@Inject 		@Resource

범용		스프링 전용		자바에서 지원		자바에서 지원

연결방식	타입에 맞춰서 연결	타입에 맞춰서 연결	이름으로 연결


2-1. 자바로 빈 와이어링하기

- 대부분 컴포넌트 스캐닝과 오토 와이어링을 사용한 자동 스프링 설정을 선호하지만, 이때 자동 설정은 옵션이 아니며 스프링을 명시적으로
  설정해야 한다. 예를 들면, 타사 라이브러리의 컴포넌트를 애플리케이션으로 와이어하고자 한다. 그 라이브러리의 소스 코드를 가지고 있지
  않으므로 클래스를 @Component 와 @Autowired 를 사용하여 애너테이트할 수 없다. 따라서 자동 설정은 선택지가 아니다.
  그 경우에 명시적인 설정을 해야 한다. 명시적 설정에는 두 가지 선택 방법이 있다. 자바와 XML.

- JavaConfig 클래스 만들기의 핵심은 @Configuration 으로 애너테이트하는 것이다.

- 기본적으로 스프링의 모든 빈은 싱글톤(singletons)이다.

2-2. XML로 빈 와이어링하기

-

3. 오토와이어링의 모호성

- @Primary
- @Qualifier


- 빈 범위
- 스프링은 빈이 생성될 수 있는 여러 개의 범위를 정의하며 다음을 포함한다.
	= 싱글톤(Singleton): 전체 애플리케이션을 위해 생성되는 빈의 인스턴스 하나.
	= 프로토타입(Prototype): 빈이 주입될 때마다 생성되거나 스프링 애플리케이션 컨텍스트에서 얻는 빈의 인스턴스 하나.
	= 세션(Session): 웹 애플리케이션에서 각 세션용으로 생성되는 빈의 인스턴스 하나.
	= 요청(Request): 웹 애플리케이션에서 각 요청용으로 생성되는 빈의 인스턴스 하나.

ConfigurableBeanFactory.SCOPE_PROTOTYPE
WebApplicationContext.SCOPE_SESSION

====================================================================================================================
@Component
@Scope(ConfigurableBeanFactory.SCOPE_PROTOTYPE)
public class Notepad {}

@Bean
@Scope(ConfigurableBeanFactory.SCOPE_PROTOTYPE)ㄴ
public Notepad notepad() {
	return new Notepad();
}

<bean id="notepad" class="com.myapp.Notepad" scope="prototype" />
====================================================================================================================

3.5.1 외부 값 주입
- property

4. AOP

- 조인 포인트(join point)
- 포인트커트(pointcut)
- 애스펙트(aspect)
- 인트로덕션(introduction): 기존 클래스에 코드 변경 없이도 새 메서드나 멤버 변수를 추가하는 기능
- 위빙(weaving): 타깃 객체에 애스펙트를 적용해서 새로운 프록시 객체를 생성하는 절차다. 애스펙트는 타깃 객체의 조인 포인트로 위빙된다.
                 위빙은 대상 객체의 생애 중 다음과 같은 몇 가지 시점에서 수행된다.
	= 컴파일 시간(compile time): 타깃 클래스가 컴파일될 때 애스펙트가 위빙되며, 별도의 컴파일러가 필요하다. AspectJ 의 위빙 컴파일러는 이러한 목적으로 사용된다.
	= 클래스로드 시간(classload time): 클래스가 JVM 에 로드될 때 애스펙트가 위빙된다. 이렇게 하려면 애플리케이션에서 사용되기 전에 타깃 클래스의 바이트 코드를 인핸스(enhance)하는 특별한 ClassLoader 가 필요하다. AspectJ 5 의 로드 시간 위빙(LTW, Load-Time Weaving) 기능을 사용하면 클래스로드 시간에 위빙된다.
	= 실행 시간(runtime): 애플리케이션 실행 중에 애스펙트가 위빙된다. 보통 타깃 객체에 호출을 위임하는 구조의 프록시 객체를 위빙 중에 AOP 컨테이너가 동적으로 만들어 낸다. 스프링 AOP 애스펙트가 위빙되는 방식이다.
5. 스프링 MVC

스프링 요청(request)을

- 디스패처 서블릿(dispatcher servlet): 요청을 스프링 MVC 컨트롤러에 전달해 주는 역할을 한다. (단일 프런트 컨트롤러)
// DispatcherServlet 같은 서블릿들은 웹 애플리케이션의 war 파일 안에 전달되는 web.xml 로 설정을 해 왔다.
// java 로도 설정 가능 대신 아파치 톰캣 7 과 같이 서블릿 3.0 이상을 지원하는 서버에 배포될 때만 동작함.

- 핸들러 매핑(handler mapping): 일반적으로 애플리케이션은 여러 개의 컨트롤러를 가지고 있기 때문에 DispatcherServlet 은 요청을 전달할 컴포넌트를 선택하기 위해 여러 개의 핸들러 매핑에게 도움을 요청한다.
- 컨트롤러(controller): 적절한 컨트롤러가 선택되면, DispatcherServlet 은 선택도니 컨트롤러에 요청을 보낸다. 컨트롤러에서 요청은 페이로드(사용자에 의해 입력된 정보)를 떨군다. 컨트롤러가 그 정보들을 처리하는 시간을 참을성 있게 기다린다(사실 잘 디자인된 컨트롤러는 비즈니스 로직을 직접 처리하기보다는 다수의 서비스 객체에 처리를 떠넘기거나 아주 짧은 시간만을 할애한다).
			컨트롤러가 하는 마지막 일은 모델을 패키징하는 일과 결과물을 렌더링하기 위한 뷰의 이름을 확인하고 모델과 뷰 이름을 포함하여 다시 DispatcherSerlet 에게 요청을 돌려보낸다.
- 모델(model): 컨트롤러에서 처리되는 로직의 결과는 사용자의 브라우저의 표시되기 위한 형태의 정보로 반환된다. 이 정보를 일반적으로 모델이라고 한다. 이런 정보들은 HTML 과 같이 사용자 편의성을 갖춘 형태로 전환한다. 이를 위해 정보들에게는 JSP(JavaServer Page)같은 뷰(view)를 필요로 한다.
- 뷰 리졸버(view resolver): DispatcherServlet 에 전달된 뷰의 이름은 직접적으로 특정 jsp 를 의미하지 않게 된다. 다시 말해 반드시 뷰가 jsp 임을 말하고 있는 것은 아니다. 대신 결과를 만들어 내기 위한 실제 뷰를 찾아내는 데 필요한 논리적인 이름을 전달해 주면 된다. DispatcherServlet 은 뷰 리졸버에게 논리적으로 주어진 뷰의 이름과 실제로 구현된 뷰를 매핑해 줄 것을 요청한다.

//?? DispatcherServlet ContextLoaderListener


스프링 MVC 활성화하기
xml -> <mvc:annotation-driven>

java -> @EnableWebMvc

5.3 요청 입력받기

- 쿼리 파라미터
- 폼 파라미터
- 패스 변수

6 웹 뷰 렌더링

뷰 리졸버(view resolver): 스프링이 모델을 실제로 렌더링하기 위해 구현되어 있는 뷰를 결정하는 역할.

InternalResourceViewResolver -> jsp 로 뷰를 결정.

TilesViewResolver -> Apache Tiles 로 뷰를 결정.

6.2.2 스프링의 JSP 라이브러리 사용하기

<%@ taglib uri="http://www.springframework.org/tags/form" prefix="sf"%>

6.3.1 타일 뷰 리졸버 설정하기

TilesConfigurer
TilesViewResolver



Servlet
-> 서버에서 웹페이지 등을 동적으로 생성하거나 데이터 처리를 수행하기 위해 자바(Java)로 작성된 프로그램을 말한다.

 CGLib (Code Generator Library)
- 기존의 자바 클래스파일로부터 자바의 소스코드를 동적으로 생성하는 라이브러리.





16 스프링 REST API

SOAP (Simple Object Access Protocl)
- 웹서비스를 실제로 이용하기 위한 객체 간의 통신규약으로 인터넷을 통하여 웹서비스가 통신할 수 있게 하는 역할을 담담하는 기술임.
