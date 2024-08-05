# System-Design-wiki

![image (1)](https://github.com/al1kite/System-Design-wiki/assets/102217402/d8bdd46c-0ba7-4d7d-a9f3-0cb3ad08b141)
대규모 시스템 설계 관련 공부를 진행하고 정리하는 페이지 입니다.


## 대규모 시스템 설계 Part 1

 <details>
    <summary>대규모 시스템 기본 이론</summary>
   
    __01-1 Estimation
   
    __01-2 사용자 수에 따른 규모 확장

    __01-3 CAP 이론
    
    __01-4 Replication
    
    __01-5 Partitioning & Sharding
  </details>

   <details>
    <summary>분산 시스템의 컴포넌트</summary>
   
    __01-1 Consistent Hashing
   
    __01-2 Rate Limiter - 1

    __01-3 Rate Limiter - 2
    
    __01-4 Unique ID Generator  
  </details>

  <details>
    <summary>Case Study</summary>
   
    __01-1 Dynamo - 1
   
    __01-2 Dynamo - 2

    __01-3 Scaling Memcache At Facebook
    
    __01-4 Real World Unique ID
  </details>

## EDA 기반 Microservice 구현 (with Hexagonal, DDD)

  <details>
    <summary>전체 아키텍처 구성도 및 구현전략</summary>
   
    __01-1 요구사항 및 설계과정 Review
   
    __01-2 전체 아키텍처 구성도

    __01-3 마이크로서비스 별 구현전략
    
    __01-4 헥사고널 아키텍처 (도메인/애플리케이션/프레임워크 헥사곤)
  </details>

  <details>
    <summary>대여 마이크로서비스 개발(DDD+헥사고널 아키텍처)</summary>
   
    __01-1 프로젝트 생성과 패키지 구조 정의(헥사고널 아키텍처)
   
    __01-2 설계된 도메인 모델 살펴보기

    __01-3 내부영역-도메인모델개발(도메인헥사곤)- 비지니스 개념정의
    
    __01-4 내부영역:도메인모델 구현(도메인 헥사곤)-비지니스로직구현

    __01-4 내부영역:도메인모델 구현(도메인 헥사곤)-비지니스로직구현
    
    __01-5 내부영역:도메인모델 구현(도메인 헥사곤)-도메인모델테스트

    __01-6 내부영역:응용서비스 구현(어플리케이션 헥사곤)-인터페이스 정의(유스케이스)

    __01-7 내부영역:응용서비스 구현(어플리케이션 헥사곤)-InputPort구현,아우터 포트 정의

    __01-8 외부영역 구현(프레임워크 헥사곤)-OR매핑 및 저장소 어댑터구현

    __01-9 외부영역 구현(프레임워크 헥사곤)-API어댑터 구현

    __01-9 외부영역 구현(프레임워크 헥사곤)-API어댑터 구현

    __01-10 API테스트 수행
  </details>

  <details>
    <summary>도서 마이크로서비스 개발(DDD+헥사고널 아키텍처)</summary>
   
    __01-1 내부영역:도메인모델 구현(도메인 헥사곤)- 비지니스 개념정의
   
    __01-2 내부영역:도메인모델 구현(도메인 헥사곤) - 비지니스로직구현&도메인모델테스트

    __01-3 내부영역:응용서비스 구현(어플리케이션 헥사곤)
    
    __01-4 외부영역 구현(프레임워크 헥사곤)

    __01-5 API테스트 수행
  </details>

  <details>
    <summary>사용자 마이크로서비스 개발(DDD+헥사고널 아키텍처)</summary>
   
    __01-1 내부영역:도메인모델 구현(도메인 헥사곤)
   
    __01-2 내부영역:응용서비스 구현(어플리케이션 헥사곤)

    __01-3 외부영역 구현(프레임워크 헥사곤),API테스트 수행
  </details>
  
  <details>
    <summary>Best서적마이크로서비스 개발(레이어드 아키텍처 ,CQRS)</summary>
   
    __01-1 패키지 구조 정의: 레이어드 아키텍처 + 비지니스로직레이어 구현
   
    __01-2 데이터 엑세스 레이어/프리젠테이션 레이어 구현/API 테스트 수행    
  </details>

  <details>
    <summary>EDA구현(기본 Pub & Sub)</summary>
   
    __01-1 내부영역: 도메인헥사곤 (대여서비스의 도메인이벤트 정의)
   
    __01-2 내부영역: 애플리케이션 헥사곤 구현(대여서비스)

    __01-3 내부영역: 애플리케이션 헥사곤 구현(대여서비스)

    __01-4 외부영역: 프레임워크 헥사곤 구현(카프카어댑터) - 대여서비스의 Producer

    __01-5 외부영역: 프레임워크 헥사곤 구현(카프카어댑터) - 도서/회원/Best도서서비스의 Consumers

    __01-6 통합테스트 전 버그 수정

    __01-7 EDA 통합테스트 수행1(테스트 환경설정 및 시나리오 설명)

    __01-8 EDA 통합테스트 수행2(터미널로 test 수행)
  </details>

  <details>
    <summary>EDA구현 Advance (SAGA)</summary>
   
    __01-1 이벤트 흐름 설계 변경
   
    __01-2 도서서비스의 응답 메시지 정의 및 응답 발송 구현

    __01-3 대여 서비스의 보상 트랜젝션 정의 및 구현

    __01-4 회원서비스 수정

    __01-5 SAGA 테스트
  </details>

  
