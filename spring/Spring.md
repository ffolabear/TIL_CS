# Spring 면접대비 질문 리스트

<hr>

### 📄 Contents
> 실제 면접에서 나올법한 흐름으로 작성
- [1. Spring 의 특징에 대해서 설명해보세요.](#1-spring-의-특징에-대해서-설명해보세요)
- [2. Spring MVC 처리흐름에 대해서 말해보세요.](#2-spring-mvc-처리흐름에-대해서-말해보세요)
- [4. Spring 에서 멀티스레드의 동작 방식에 대해 설명해주세요.](#4-spring-에서-멀티스레드의-동작-방식에-대해-설명해주세요)
- [5. JPA에 대해 설명해주세요.](#5-jpa에-대해-설명해주세요)
- [6. 필터와 인터셉터에 대해 설명해주세요](#6-필터와-인터셉터에-대해-설명해주세요)
--- 

### 1. Spring 의 특징에 대해서 설명해보세요.
- 자바 엔터프라이즈 개발을 편하게 해주는 경량급 오픈소스 애플리케이션 프레임워크
- POJO 기반의 Enterprise Application 개발을 쉽고 편하게 할 수 있음


#### IOC(Inversion of Control) - 제어의 역전
- 컨트롤의 제어권이 사용자가 아니라 프레임워크에 있어 필요에 따라 스프링에서 사용자의 코드를 호출
- 결합을 느슨하게 하고 유지보수가 하기 쉽게 해줌

#### DI(Dependency Injection) - 의존성 주입
- 의존관계를 외부에서 결정하고 주입하는 것
- 의존성이 줄어듬
- 재사용성이 높은 코드를 짤 수 있음

### AOP(Aspect-Oriented Programming) - 관점지향 프로그래밍
- 트랜잭션이나 로깅, 보안과 같이 여러 모듈에서 공통적으로 사용하는 기능의 경우 해당 기능을 분리하여 관리할 수 있음

<details>
<summary>꼬리질문</summary>
<div markdown="1">

### DI 의 방법에 대해 설명해주세요.
- 필드 주입, 생성자 주입, setter 주입이 있음
- 생성자 주입이 가장 권장됨

#### 이유
- setter 주입을 할 경우 public 으로 설정해야 하므로 변경에 열려있어서 위험
- 테스트 코드를 짜기 편함
- 객체 생성 시점에 불변하게 설계해서 변경을 막을 수 있음

</div>
</details>

<br>

<br>

### 2. Spring MVC 처리흐름에 대해서 말해보세요.
1. 클라이언트의 Request 를 `DispatcherServlet` 이 받음
2. `HandlerMapping` 에서 요청한 URL과 매칭되는 컨트롤러를 검색
3. `HandlerMapping` 이 찾은 `Handler` 를 `HandlerAdapter` 가 실행
   ```java
   public class DispatcherServlet extends FrameworkServlet {
        //...
        protected void doDispatch(HttpServletRequest request, HttpServletResponse response) throws Exception {
            HandlerExecutionChain mappedHandler = null;
            //...
            try {
                //HandlerMapping 이 요청에 맞는 handler 를 가져오는 부분
                mappedHandler = getHandler(processedRequest);
                //...
                
                //요청에 맞는 handler 를 가져오는 부분
                HandlerAdapter ha = getHandlerAdapter(mappedHandler.getHandler());
            } catch (Exception ex){
   
            }
        }
        //...
   }    
   ```

4. Controller 에서 요청을 처리하고 처리 결과를 `ModelAndView` 로 리턴
5. `ModelAndView` 를 읽어서 그에 맞는 view 를 `ViewResolver` 가 해석해서 리턴
    - `doDispatch()` 메소드에서 `render()` 메소드를 호출하고 그 메소드에서 view 를 리턴

   ```java
    public class DispatcherServlet extends FrameworkServlet {
        //...
        @Nullable
        protected View resolveViewName(String viewName, @Nullable Map<String, Object> model, Locale locale, HttpServletRequest request) throws Exception {

            if (this.viewResolvers != null) {
                for (ViewResolver viewResolver : this.viewResolvers) {
                    View view = viewResolver.resolveViewName(viewName, locale);
                    if (view != null) {
                        return view;
                    }
                }
            }
            return null;
        }
        //...
   }
   ```
   
<details>
<summary>꼬리질문</summary>
<div markdown="1">

### MVC 패턴에 대해 설명해주세요.
Model, View, Controller 를 구성요소로 개발하는 패턴

#### Model
- 데이터와 비즈니스 로직을 담당

#### View
- 사용자 인터페이스를 표현하고 데이터를 시각적으로 표현하는 역할

#### Controller
- 사용자의 입력을 처리하고 Model 과 View 를 연결하는 역할


</div>
</details>

<br>

### 2. Spring MVC 처리흐름에 대해서 말해보세요.
1. 클라이언트의 Request 를 `DispatcherServlet` 이 받음
2. `HandlerMapping` 에서 요청한 URL과 매칭되는 컨트롤러를 검색
3. `HandlerMapping` 이 찾은 `Handler` 를 `HandlerAdapter` 가 실행
   ```java
   public class DispatcherServlet extends FrameworkServlet {
        //...
        protected void doDispatch(HttpServletRequest request, HttpServletResponse response) throws Exception {
            HandlerExecutionChain mappedHandler = null;
            //...
            try {
                //HandlerMapping 이 요청에 맞는 handler 를 가져오는 부분
                mappedHandler = getHandler(processedRequest);
                //...
                
                //요청에 맞는 handler 를 가져오는 부분
                HandlerAdapter ha = getHandlerAdapter(mappedHandler.getHandler());
            } catch (Exception ex){
   
            }
        }
        //...
   }    
   ```

4. Controller 에서 요청을 처리하고 처리 결과를 `ModelAndView` 로 리턴
5. `ModelAndView` 를 읽어서 그에 맞는 view 를 `ViewResolver` 가 해석해서 리턴
   - `doDispatch()` 메소드에서 `render()` 메소드를 호출하고 그 메소드에서 view 를 리턴

   ```java
    public class DispatcherServlet extends FrameworkServlet {
        //...
        @Nullable
        protected View resolveViewName(String viewName, @Nullable Map<String, Object> model, Locale locale, HttpServletRequest request) throws Exception {

            if (this.viewResolvers != null) {
                for (ViewResolver viewResolver : this.viewResolvers) {
                    View view = viewResolver.resolveViewName(viewName, locale);
                    if (view != null) {
                        return view;
                    }
                }
            }
            return null;
        }
        //...
   }
   ```

<details>
<summary>꼬리질문</summary>
<div markdown="1">

### MVC 패턴에 대해 설명해주세요.
Model, View, Controller 를 구성요소로 개발하는 패턴

#### Model
- 데이터와 비즈니스 로직을 담당

#### View
- 사용자 인터페이스를 표현하고 데이터를 시각적으로 표현하는 역할

#### Controller
- 사용자의 입력을 처리하고 Model 과 View 를 연결하는 역할


</div>
</details>

<br>

---

### 3. Spring Bean 에 대해 설명해주세요.
- 스프링 컨테이너가 관리하는 객체
- 스프링 컨테이너가 컴포넌트 스캔을 통해 Bean 으로 등록할 대상들을 탐색 후 등록
- 스프링 컨테이너가 Singleton 으로 관리해줌

<details>
<summary>꼬리질문</summary>
<div markdown="1">

### Bean 생명 주기에 대해 설명해주세요.
1. 스프링 컨테이너 생성
2. 스프링 빈 생성
3. 의존관계 주입
4. 초기화 콜백 사용
5. 빈 사용
6. 소멸전 콜백
7. 스프링 종료

빈 생성 콜백은 `@PostConstruct`, 빈 소멸 콜백은 `@PreDestroy` 어노테이션을 해당 메서드에 붙이면 됨

<br>

### Singleton 패턴에 대해 설명해주세요.
- 객체의 인스턴스가 오직 1개만 생성되는 패턴을 의미
- 일반적으로 Singleton 패턴을 구현하려면 3단계가 필요
  1. private 생성자를 선언
  2. 해당 객체를 리턴하는 `getInstance()` 메서드를 선언
  3. 해당 객체를 의미하는 필드를 private 생성자로 초기화

<br>

### 스프링 컨테이너에 대해 설명해주세요.
- 스프링 프레임워크의 핵심 컴포넌트
- Bean 객체들의 의존성을 주입하며 Bean 의 라이프 사이클을 관리
- 낮은 결함도와 높은 결합도를 가지게 개발할 수 있게 해줌

<br>

</div>
</details>

<br>

---

### 4. Spring 에서 멀티스레드의 동작 방식에 대해 설명해주세요.
- Thread pool 을 사용
- 스레드를 새롭게 생성하는것은 오버헤드가 크기 떄문 미리 생성해두고 필요할때 마다 제공하는 방식을 채택
- Thread pool 은 톰캣에서 관리 
- 요청이 들어올때마다 Thread 를 하나씩 할당하고 작업이 끝나면 다시 Thread pool 로 Thread 반환

<details>
<summary>꼬리질문</summary>
<div markdown="1">

### DB Connection Pool 에 대해 설명해주세요.
DB Connection 을 획들할때는 다음과 같은 과정을 거침
1. DB 드라이버를 통해 Connection 을 조회
2. DB 드라이버는 DB 와 TCP/IP 커넥션을 연결(3-way-handshake)
3. DB 드라이버는 DB 에 인증 정보를 전달
4. DB 는 전달받은 인증정보로 인증을 완료하고 DB 세션을 생성
5. DB 는 Connection 생성이 완료되었다고 응답
6. DB 드라이버는 커넥션 객체를 클라이언트에 반환

- 이런 과정들은 시간도 오래걸리고 오버헤드가 큰 과정이므로 Connection Pool 이 어플리케이션 실행 시점에 Connection 을 일정 갯수만큼 생성
- 요청이 올때마다 하나씩 사용하고 사용후에는 Connection Pool 에 다시 반환

#### 장점 
- 서버당 최대 Connection 수를 제한함으로써 DB 를 보호할 수 있음   

<br>

### TCP/IP 통신에 대해 설명해주세요.
- 응용, 전송, 인터넷, 네트워크 접근의 4계층으로 구성
- 
> 응 전 인 네

#### TCP - 전송 제어 프로토콜
- TCP/IP 통신의 전송 계층에 해당
- 연결 지향 - 3 way handshake
- 데이터 전달 보증
- 순서 보장
- 신뢰 할 수 있음

<br>

### 3 way handshake 에 대해 설명해주세요.
1. 클라이언트가 서버에 SYN 을 보냄
2. 서버는 SYN 과 ACK 메세지를 클라이언트로 응답
3. 클라이언트는 메세지를 받고 ACK 메세지를 보냄
4. 서버로 데이터 전송

- 클라이언트와 서버 모두 연결되었음을 믿을 수 있다는 것이 특징
- 물리적으로 연결된 것이 아니라 논리적으로 연결되었음을 의미 

</div>
</details>

<br>

---

### 5. JPA에 대해 설명해주세요.
- ORM 기술로 객체와 DB의 관계를 매핑해주는 기술
- 객체 모델과 관계형 모델의 패러다임의 불일치를 해소

#### 장점 
- DB 데이터들을 객체 지향적으로 개발할 수 있음
- 기본 CRUD 메소드를 제공으로 생산성 향상
- DBMS 의 종속성이 줄어듬

#### 단점
- 객체들간의 관계를 설계하는 과정이 복잡함
- JPA 가 생성하는 쿼리가 최적화되지 않을 경우 직접 쿼리를 작성해야함
- 높은 러닝커브

<details>
<summary>꼬리질문</summary>
<div markdown="1">

### 영속성 컨텍스트에 대해 설명해주새요.
엔티티를 영구 저장하는 환경을 의미

#### 장점 
1. 1차 캐시
   - 영속성 컨텍스트에 엔티티를 저장한다음 조회 쿼리를 날리지 않고 객체를 조회할 수 있음
   - 만약 조회한 데이터가 1차 캐시에 없다면 DB 에서 조회해온 뒤 1차 캐시에 저장

2. 동일성 보장
   - 한 트랜잭션 내에서 같은 데이터를 여러번 읽어도 항상 같은 결과를 보장

3. 트랜잭션을 지원하는 쓰기 지연
   - 엔티티의 변경시 쓰기 지연 SQL 저장소에 변경 SQL 을 쌓고 트랜잭션 커밋시 SQL 실행 

4. 변경감지 Dirty Checking
   - 엔티티의 변경시 1차 캐시에 존재하는 해당 엔티티의 스냅샷과 비교하여 다를시 Update 쿼리를 날림

5. 지연 로딩
   - 연관된 객체조회시 영속성 컨텍스트에서 객체의 프록시 객체를 가져옴
   - `FetchType=EAGER` 를 사용시 프록시 객체가 아닌 원본 객체를 가져옴

<br> 



<br>

### JPA 에서 엔티티의 생명 주기에 대해 설명해주세요.

#### 비영속
- 영속성 컨텍스트와 전혀 관계가 없는 새로운 상태

#### 영속
- 영속성 컨텍스트에 관리되는 상태

#### 준영속
- 영속성 컨텍스트에 저장되었다가 분리된 상태

#### 삭제
- 삭제된 상태

</div>
</details>

<br>

---

### 6. 필터와 인터셉터에 대해 설명해주세요

#### filter
- 톰캣과 같은 웹 컨테이너에 의해 관리되며 DispatcherServlet 의 요청전에 작동
- 요청이 전달된 전후에 부가작업을 처리할 수 있는 기능을 제공

#### interceptor
- 스프링이 제공하는 기술로 DispatcherServlet이 컨트롤러를 호출하기 전후에 요청과 응답을 참조하거나 가공할 수 있는 기능을 제공

<details>
<summary>꼬리질문</summary>
<div markdown="1">

### Spring AOP에 대해 설명해 주세요.
- 관점지향 프로그래밍의 약자
 어플리케이션을 종단관점으로 보고 핵심 로직과 공통 로직을 분리하여 모듈화하는 프로그래밍 방식

### 주요용어

#### Aspect
- 애플리케이션에서 공통된 기능을 정의한 모듈

#### Target 
- Aspect 를 적용하는 곳

#### Advice 
- 관점의 구체적인 동작을 나타내는 메서드

#### JoinPoint
- 관점이 적용될 수 있는 지점을 의미
- Advice가 적용될 수 있는 위치, 메소드 실행, 생성자 호출, 필드 값 접근, static 메서드 접근 같은 프로그램 실행 중 지점을 나타냄

#### PointCut
- 조인 포인트의 부분 집합을 정의하는 표현식

<br>

</div>
</details>

<br>


<br>
<br>