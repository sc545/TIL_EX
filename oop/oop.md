1. 여러분의 소프트웨어가 고객이 원하는 기능을 하도록 하세요.
2. 객체지향의 기본 원리를 적용해서 소프트웨어를 유연하게 하세요.
3. 유지보수와 재사용이 쉬운 디자인을 위해 노력하세요.

요구 사항
명사->클래스, 동사->메소드
유스케이스
주경로, 대체경로

객체지향 원리

변하는 것을 캡슐화하라.
구현에 의존하기보다는 인터페이스에 의존하도록 코딩하라.
각 클래스는 변경 요인이 오직 하나이어야 한다.

SOLID

보통은 행동(behavior)이 변하는 경우에 서브 클래스를 사용한다는 것을 기억하세요.

응집도 ↑ 결합도 ↓


개발 접근 방식

- 유스케이스 주도 개발
-> 시스템에서 하나의 유스케이스를 선정하여, 유스케이스의 모든 시나리오를 포함해서 그 전체를 구현하려고 코드 작업을 완성하는데
-> 중점을 두고 있습니다. 그 다음에 애플리케이션의 다른 것으로 넘어갑니다.

- 특징 주도 개발
-> 하나의 특징에 집중하여 그 특징의 모든 행위 모두를 코드 작업합니다. 그 다음에 애플리케이션의 다른 것으로 넘어갑니다.

- 테스트 주도 개발
-> 한 가지 기능의 테스트 시나리오를 작성하고, 그 다음에 그 기능에 대한 코드를 작성합니다. 그리고 모든 테스트를 통과할 때까지 소프트웨어를 작성합니다.

좋은 소프트웨어 개발 방법이란 대체로 개발 주기의 여러 단계에서 이러한 개발 모델 모두를 혼용합니다.


의견의 문제 (변하는 요소와 변하지 않는 요소를 명확히 구분 하는지에 대한 문제?)

- 공통점 강조하기
-> 장점: 공통 속성으로 사용될 것이라는 의도가 보임.
-> 단점: 중복이 있음, 요구사항 변경시 유지보수가 문제...

- 캡슐화 강조하기
-> 장점: 변화에 좀 더 잘 대응할 수 있으며, 좀 더 많은 캡슐화를 사용함.
-> 단점: 공통 속성으로 사용될 것이라는 의도가 보이지 않음, 런타임시의 많은 작업들(형 변환)

최선의 추측으로 선택하고, 상황을 보는 것이, 어떤 것을 선택할지 끝도 없이 논쟁하는 것보다 좋습니다.
이렇게 논쟁만 벌이는 것을 분석 마비라고 하는데, 이것으로는 아무것도 얻을 수 없습니다.

좋은 소프트웨어는 반복 작업을 통해 완성됩니다. 애플리케이션의 매우 작은 부분을 작업하면서, 분석과 설계를 하고, 다시 이를 되풀이 하세요.
반복해서 작업할 때마다, 설계 결정들을 재평가하고, 여러분의 설계에 도움이 되면 무언가 변경하는 것을 두려워하지 마세요.

프로그래밍 기술

- 약정에 의한 프로그래밍
-> 여러분과 소프트웨어 사용자가 지키기로 합의한, 소프트웨어가 어떻게 동작해야 하는지에 관한 계약을 설정합니다.

- 방어적 프로그래밍 (안전성이 중요한 소프트웨어일 경우 많이 사용할 거 같음?)
-> 다른 소프트웨어를 신뢰하지 않고, 다른 소프트웨어가 나쁜거나 안전하지 않은 정보를 제공하는지 확인하기 위해, 광범위하게 오류와 데이터를 점검합니다.
