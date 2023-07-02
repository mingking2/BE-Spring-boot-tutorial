# 스프링 입문 - 코드로 배우는 스프링 부트, 웹 MVC, DB 접근 기술

## 1. 프로젝트 환경설정
- 프로젝트 생성
- 라이브러리 살펴보기
- View 환경설정
- 빌드하고 실행하기

## 2. 스프링 웹 개발 기초
- 정적 컨텐츠
  - static
  - 파일을 그냥 내려준다.
- MVC와 템플릿 엔진
  - MVC: Model, View, Controller
    - Controller : 내부 로직에 집중
    - View : 화면을 그리는데 집중
    - Model : Controller와 View에서 수행한 것들을 Model로 넘긴다.
- API
  - JSON으로 바꾼다.
  - 객체를 반환한다.



## 3. 회원 관리 예제 - 벡엔드 개발
- 비즈니스 요구사항 정리
  - 데이터: 회원ID, 이름
  - 기능: 회원 등록, 조회
  - 아직 데이터 저장소가 선정되지 않음(가상의 시나리오)

  - 일반적인 웹 애플리케이션 계층 구조
    ```
     컨트롤러   ->   서비스   ->   리포지토리   ->   DB
            \        |         /
                   도메인
    ```                  
    - 컨트롤러: 웹 MVC의 컨트롤러 역할
    - 서비스: 핵심 비지니스 로직 구현
    - 리포지토리: 데이터베이스에 접근, 도메인 객체를 DB에 저장하고 관리
    - 도메인: 비즈니스 도메인 객체, 예) 회원, 주문, 쿠폰 등등 주로 데이터베이스에 저장하고 관리됨
  
  - 클래스 의존관계
    ```
                              interface
    MemberService    ->    MemberRepository
                                  ^
                                  |
                                Memory
                           MemberRepository
    ```                         
    - 아직 데이터 저장소가 선정되지 않아서, 우선 인터페이스로 구현 클래스를 변경할 수 있도록 설계
    - 데이터 저장소는 RDB, NoSQL 등등 다양한 저장소를 고민중인 상황으로 가정
    - 개발을 진행하기 위해서 초기 개발 단계에서는 구현체로 가벼운 메모리 기반의 데이터 저장소 사용
- 회원 도메인과 리포지토리 만들기
- 회원 리포지토리 테스트 케이스 작성
  - 개발한 기능을 실행해서 테스트할 때 자바의 main 메서드를 통해서 실행하거나, 웹 애플리케이션의 컨트롤러를 통해 서 해당 기능을 실행한다.
  - 이러한 방법은 준비하고 실행하는데 오래 걸리고, 반복 실행하기 어렵고 여러 테스트를 한번에 실행하기 어렵다는 단점이 있다.
  - 자바는 JUnit이라는 프레임워크로 테스트를 실행해서 이러한 문제를 해결한다.
- 회원 서비스 개발
- 회원 서비스 테스트

## 4. 스프링 빈과 의존관계
- 컴포넌트 스캔과 자동 의존관계 설정
  - 스프링 빈을 등록하고, 의존관계 설정하기
  - @Component: 애노테이션이 있으면 스프링 빈으로 자동 등록한다.
  - @Controller: 컨트롤러가 스프링 빈으로 자동 등록된 이유도 컴포넌트 스캔 때문이다.

  - @Component를 포함하는 다음 애노테이션도 스프링 빈으로 자동 등록된다.
    - @Controller
    - @Service
    - @Repository
    
- 자바 코드로 직접 스프링 빈 등록하기
  - 회원 서비스와 회원 리포지토리의 @Service, @Repository, @Autowired 에노테이션을 제거하고 진행한다.
  - 여기서는 향후 메모리 리포지토리를 다른 리포지토리로 변경할 예정이므로, 컴포넌트 스캔 방식 대신에 자바 코드로 스프링 빈을 설정하겠다.
  - 참고
    - XML로 설정하는 방식도 있지만 최근에는 잘 사용하지 않으므로 생략한다.
    - DI에는 필드 주입, setter 주입, 생성자 주입 이렇게 3가지 방법이 있다. 의존관계가 실행 중에 동적으로 변하는 경우는 거의 없으므로 생성자 주입을 권장한다.
    - 실무에서는 주로 정형화된 컨트롤러, 서비스, 리포지토리 같은 코드는 컴포넌트 스캔을 사용한다. 그리고 정형화되지 않거나, 상황에 따라 구현 클래스를 변경해야 하면 설정을 통해 스프링 빈으로 등록한다.
  - 주의
    - @Autowired를 통한 DI는 helloController, MemberService 등과 같이 스프링이 관리하는ㄴ 객체에서만 동작한다.
    - 스프링 빈으로 등록하지 않고 내가 직접 생성한 객체에서는 동작하지 않는다.
  - 스프링 컨테이너 DI 관련된 자세한 내용은 스프링 핵심 원리 강의에서 설명한다.


## 5. 회원 관리 예제 - 웹 MVC 개발
- 회원 웹 기능 : 홈 화면 추가
- 회원 웹 기능 : 등록
- 회원 웹 기능 : 조회


## 6. 스프링 DB 접근 기술
- H2 데이터베이스 설치
- 순수 JDBC
  - 환경 설정
  - Jdbc 리포지토리 구현
- 스프링 통합 테스트
  - 스프링 컨테이너와 DB 통합 테스트
    - @SpringBootTest: 스프링 컨테이너와 테스트를 함께 실행한다.
    - @Transactional: 테스트 케이스에 이 애노테이션이 있으면, 테스트 시작 전에 트랜잭션을 시작하고, 테스트 완료 후에 항상 롤백한다. 이렇게 하면 DB에 데이터가 남지 않으므로 다음 테스트에 영향을 주지 않는다.
- 스프링 JdbcTemplate
- JPA
- 스프링 데이터 JPA

# 버전 수정 이력

## v2022-11-28

* 스프링 부트 3.0 내용 추가

* 프로젝트 선택에서 `Gradle - Groovy` 추가



## v2022-09-04

* 오타 `helloConroller` -> `helloController` (hswkd9895님 도움)

* 코드 오타 `template/` -> `templates/` (anthologia님 도움)



## v2021-12-01

*주의!*

h2 데이터베이스는 꼭 다음 링크에 들어가서 *1.4.200* 버전을 설치해주세요.

최근에 나온 2.0.206 버전을 설치하면 일부 기능이 정상 동작하지 않습니다.

https://www.h2database.com/html/download-archive.html



만약 이미 설치하고 실행까지 했다면 다시 설치한 이후에 *~/test.mv.db* 파일을 꼭 삭제해주세요.

그렇지 않으면 다음 오류가 발생하면서 접속되지 않습니다.

General error: "The write format 1 is smaller than the supported format 2 [2.0.206/5]" [50000-202] HY000/50000



## v2021-07-18

스프링 부트 최신 버전 선택 설명 추가

## v2021-03-03

* 윈도우 사용자는 h2.bat 실행 추가

## v2021-02-11

* 회원 리포지토리 테스트 케이스 작성에서 result, member 위치 변경

* 도움 주신 분 : 박동훈님

## v1.7 - 2020-11-23

* 스프링부트 2.4 에서 데이터베이스 커넥션 오류 해결방안 추가

* 스프링부트 2.4부터는 `spring.datasource.username=sa`를 꼭 추가해주어야 한다. 그렇지 않으면 `Wrong user name or password` 오류가 발생한다.

* [Databases that support embedded and non-embedded modes are always detected as embedded  by somayaj · Pull Request #23693 · spring-projects/spring-boot · GitHub](https://github.com/spring-projects/spring-boot/pull/23693)

## v1.6 - 2020-10-14

* helloController -> memberController 이미지 오류 수정 (도움주신분: 최성규님)

## v1.5 - 2020-10-10

*  IntelliJ JDK 설치 확인 추가

## v1.4 - 2020-09-18

* 인텔리J 커뮤니티(무료) 버전에서 `application.properties` 파일에서 키가 회색으로 인식 설명

## v1.3 - 2020-09-07

* 윈도우 gradlew.bat -> gradlew로 변경

## v1.2 - 2020-08-28

* 윈도우 사용자를 위한 IntelliJ 단축키 조회 방법 추가

## v1.1 - 2020-08-28

* 윈도우 사용자를 위한 도움 추가

윈도우에서 맥의 iTerm이 없는데 어떻게 하나요? 링크 추가

* 도움 주신 분: 루시님

## v1.0 - 2020-07-20

* 강의 오픈

 