## API Gateway Service

API Gateway 서비스는 사용자가 설정한 라우팅 설정에 다라서 각각 앤드포인트로 
클라이언트 대신해서 요청하고 응답을 받으면 다시 클라이언트한테 전달해주는 프락시 역할을 하게 된다.

시스템의 내부 구조는 숨기고 외부의 요청에 대해서 적절한 형태로 가공해서 응답할 수 있다는 장점을 갖고 있다.

<img width="724" src="https://github.com/user-attachments/assets/226e620a-5bec-4336-bfd7-815c101a0dd8">

앞에 보이는 그림은 마이크로소프트 사에서 클라우드 아키텍처에 대해 잘 설명해놓은 그림으로,
마이크로 서비스가 3가지가 있다 가정을 했을 때 클라이언트 사이드에서 마이크로 서비스 그림으로 볼 수 있다.
그러면 모바일 어플리케이션이 됐던 웹 어플리케이션이 됐던 클라이언 측에서 마이크로서비스의 직접 주소를 이용해서 파라미터를 전달하고 요청하는 그림이다.

새로운 마이크로 서비스가 추가됐다 가정을 해보자.
새로운 마이크로 서비스가 이렇게 추가되었다 하거나 아니면 기존에 있었던 마이크로 서비스가 추가되었다 하거나 혹은 기존에 있던 마이크로 서비스의 주소가 변경되었다거나 파라미터의 인자값이 변경되었거나 이런
작업이 생겼을 때 이전 시간에 설명한 것 처럼 마이크로서비스 자체가 독립적으로 빌드가 되고 배포가 되는 장점이 있다.

문제는 클라이언트 사이드에 있다. 클라이언트 사이드에서 이렇게 마이크로서비스의 주소를 직접 이용해 엔트포인트라고 하는데 그런 엔트포인트를 직접적으로 호출했을 경우엔 클라이언트 사이드에 있는 애플리케이션도
같이 수정 배포가 되어야 한다. 그러다보니 단일 진입점을 갖고 있는 형태로서 개발하는게 필요하다.

<img width="643" src="https://github.com/user-attachments/assets/e9448d87-7bc9-4f42-a2c9-a563e2f3b105">

그래서 서버단, 백엔드단에다가 중간에 게이트웨이 역할을 해줄 수 있는 일종의 진입로인 API 게이트웨이를 하나 두고 
각각의 마이크로 서비스로 요청되는 모든 정보에 대해서 일괄적으로 처리할 수 있게 된다. 모바일, React, Angular 등을 이용한 하나의 단일 페이지, 싱글 페이지로서 애플리케이션을 구성하는 SPA 등의 형태의 앱도 상관 없이
직접적으로 마이크로 서비스를 호출하지 않고 클라이언트는 게이트웨이만 상대한다.
따라서 게이트웨이에서 우리가 필요로 하는 정보를 변경하고 갱신하는 작업이 훨씬 더 수월해질 수 있다.

이러한 API Gateway를 사용하게 되면 인증 및 권한 부여, 서비스 검색 통합, 응답 캐싱, 정책-회로 차단기 및 Qos 다시 시도, 속도 제한, 부하 분산,
일괄적 로깅 * 추적 * 상관관계, 헤더와 쿼리 문자열 및 청구 변환, IP 허용 목록에 추가 등을 수월하게 할 수 있다.

### Netflix Ribbon 

API Gateway 서비스를 실제 구현하기 전에 넷플릭스 리본과 넷플릭스 쥴에 대해서 잠깐 알아볼 것.

스프링 클라우드에서 마이크로 서비스들 간의 통신, 하나의 마이크로 서비스가 다른 마이크로 서비스를 호출하기 위해서 사용되는 방빕어 기장 대표적인 방법, REST Template 를 구현하는 방법과 Feign Client 를 구현하는 방법 2가지가 있다.
REST Template은 전통적으로 하나의 웹 서비스, 웹 어플리케이션에서 다른 어플리케이션을 사용하기 위해서 자주 사용되었던 API 이다.

<img width="627" src="https://github.com/user-attachments/assets/bfb65ab0-e94b-41f3-8f0a-7850b748ce52">

앞에 보이는 것과 같이 접속하고자 하는 서버 주소와 포트 번호가 필요하다면 포트번호를 입력하고 파라미터까지 같이 전달하고 GET 혹은 POST 메소드 형식으로 호출하게 되면 필요한 외부 서비스로 연동하는 방법이었다.
스프링 클라우드에서는 스프링 클라우드 Feign Client 라는 API를 이용해 호출할 수가 있는데, 앞에 보이는 것처럼 특정한 인터페이스를 하나 만든다.

이 인터페이스를 하나 만든 다음, 앞에 있는 인터페이스에서 우리가 웹으로 따로 호출하고 싶은 추가적인 마이크로 서비스의 이름을 등록한다. 그걸 Feign Client 라고 한다.
이걸 이용하면 만약 유저라는 서비스에서 Feign Client를 등록하고 스토어라는 서비스를 호출하겠다 하면 굳이 조금 전 만들었던 것 처럼 직접적인 마이크로 서비스의 서버의 주소나 포트번호 필요 없이 마이크로서비스 이름 갖고 호출할 수 있게 된다.
그러면 유저라는 서비스 안에서 스토어라는 서비스가 자신이 갖고 있는 API 처럼 자유롭게 호출해서 사용할 수 있게 된다.

이러한 방법으로 스프링 클라우드에서 마이크로 서비스 간의 호출을 담당해왔었는데, 
문제는 로드 밸런서를 하기 위해서 로드 밸런서를 어디에 구축해서 작업할 것인가가 고민이 됐다.
초창기 스프링 클라우드에서는 이런 로드 밸런서 역할을 해주는 별도의 서비스 프로젝트를 위해 리본이라는 서비스를 제공하기 시작했다.

다른 몇 가지 서비스와 마찬가지로 넷플릭스라는 회사가 갖고 있는 로드 밸런스 기술이 리본이라는 서비스로서 완성이 돼서 스프링 클라우드 재단에 기부가 돼서 사용되고 있었던 것.

그런데 문제점은 이 리본이라는 서비스 자체는 최근 우리가 Functional API 또는 React Java 라는 방식과는 호환이 많이 안되는 방식, 쉽게 말해 비동기가 처리가 잘 되지 않는 방식이었기 때문에 최근엔 이걸 잘 사용하지 않기 시작한다.
어쨌든 리본이라는 서비스를 이용하게 되면 마이크로 서비스의 이름을 갖고 클라이언트 안에서 우리가 필요한 데이터를 호출할 수 있게 된다.

또 하나 헬스체크라고 해서 해당 서비스가 정상적으로 작동 중인지도 확인할 수 있다. 
예를 들어 마이크로 서비스가 유저 서비스, 오더 서비스, 프로덕트 서비스로 3가지 있다고 가정해보자. 
이걸 사용하는 클라이언트가 중간에 있다. 
클라이언트가 직접적으로 마이크로 서비스에 있는 내용을 호출하는 방식은 좋지 않다. 그래서 조금 전 이야기한 API Gateway를 중간에 놔야 하는데 
그 작업을 별도의 서비스나 시스템을 구축하지 않고 클라이언트 측 내부에 리본이라는 서비스를 구축해서 사용하기 시작했다. 클라이언트 사이드에 있기 때문에 클라이언트 사이드에서 사용할 수 있는 로드 밸런서라는 뜻.
클라이언트 프로그램 안에서 우리가 이동하고자 하는 마이크로 서비스의 주소값을 직접 관리하는 걸 이야기한다.

<img width="381"  src="https://github.com/user-attachments/assets/cf10235b-d5ea-4688-b29f-9cfab298476a">

얼핏 보면 조금 전 말한 게이트웨이를 중간에 놓았던 방식의 작업을 클라이언트 사이드로 이동해와서 쓰는 방식이라 보면 될 것.
클라이언트는 리본이라는 서비스를 이용하게 되면 어떤 장점이 생기냐면 아까 말한 외부에 있는 마이크로 서비스를 호출하기 위해 IP하고 포트 번호를 명시하는 것이 아니라
그냥 마이크로 서비스의 이름만 갖고 호출할 수 있다는 장점이 생긴다.

이런 식으로 리본이라는 서비스를 이용해 로드밸런스를 구축했는데 최근 스프링 클라우드 리본은 더이상 사용하지 않고 현재의 상태를 유지하고 다음 차후 버전에 이걸 더 넣을지 말지를 보류 중인 상태로 되어있다.
그래서 스프링부트 2.4를 사용하게 되면 우리가 더 이상 이 서비스를 사용할 수 없는 maintenance 상태라고 보면 된다.

이 maintenance 상태라는 건 모듈을 유지 관리 모듈에 두는 것으로써 스프링 클라우드 팀에서 더 이상 이런 모듈에 새로운 긴응을 추가하지 않는다는 뜻이다.
그래서 다음 버전에서 문제가 생겨 다음 버전에 보완하거나 빼거나 할 수 있는 상태라고 보면 된다.

### Netflix Zuul

두번째로 넷플리스 줄에 대해서 살펴볼 것.

우리가 이번 시간에 API Gateway 서비스를 구축하기 전에 앞에서 보고 있는 넷플릭스 줄이라는 제품을 이용해 간단하게 API Gateway 가 어떤 식으로 작동하고 있는지 살펴볼 예정.
넷플릭스 줄, Spring Cloud의 넷플릭스 줄이라는 건 조금 전 얘기했던 Gateway 역할을 해주는 제품이라고 보면 된다.
Gateway의 역할을 테스트하기 위해 첫번째 서비스와 두번째 서비스라는 두가지의 마이크로 서비스 어플리케이션을 만들 것.
그래서 클라이언트에서 이런 마이크로 서비스를 호출함에 있어서 말했던 넷플릭스 줄이라는 제품을 이용해 Gateway 테스트를 해볼 것.
클라이언트가 상대하는 건 First 서비스라던가 Second 서비스를 직접 상대하는게 아니라 클라이언트에서는 넷플릭스 줄에 데이터를 요청하게 되면 넷플릭스 줄이 그 요청을 
퍼스트 서비스 또는 세컨드 서비스에 보내주는 역할을 하게 된다.
조금 전 본 API 게이트 역할과 동일한 작업을 한다고 보면 된다.

<img width="484" src="https://github.com/user-attachments/assets/4d4d4e69-e36c-42a6-9383-1db33e6c1fc3">

이 넷플릭스 줄이라는 제품을 통해 라우팅 기능이라던가 아까 말한 게이트 역할을 하게 된다.
그런데 이 넷플릭스 스프링 클라우드, 넷플릭스 줄이라는 제품도 아까 말한 리본과 마찬가지로 스프링 부트 24에서 maintenance 상태가 됐다.
더 이상 사용할 수 없는 상태라 보면 된다. 