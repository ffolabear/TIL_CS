# Spring 면접대비 질문 리스트

<hr>

### 📄 Contents
> 실제 면접에서 나올법한 흐름으로 작성
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


<br>
<br>