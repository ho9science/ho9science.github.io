---
title: "MVC 패턴이란?"
date: 2019-04-10 00:00:01 
categories: spring
tag: spring
---

# MVC 패턴이란?
Model-View-Controller의 약자로 소프트웨어 디자인 패턴입니다.

* Model : 일반적으로 데이터베이스에 대응되는 비즈니스 로직이 수행된 후 처리될 데이터. 상태 변화가 있을 때 컨트롤러와 뷰에 통보합니다.
* View : UI요소로 사용자가 데이터를 볼 수 있도록 결과물을 보여주기 위해 모델로 부터 정보를 얻어옵니다.
* Controller : 모델의 상태를 변경하거나 뷰에 모델의 표시 방법을 변경할 수 있습니다.

## MVC의 장점
1. Model과 View가 분리되어 재사용성이 높아짐
2. 각각의 역할을 분명히 하여 스파게티 코드 방지
3. 협업을 위한 업무 분할 원할함

## MVC의 단점
1. 프로그램이 커질수록 모델(model)과 뷰(view)가 복잡하여 컨트롤러와 종속적이 되고 컨트롤러가 비대해지는 massive view controller 패턴이 됩니다.
2. 모델(model)과 뷰(view)가 완전히 분리되지는 않고 서로 의존적입니다.

## MVC 패턴 구조
![mvc](https://docs.spring.io/spring/docs/3.2.x/spring-framework-reference/html/images/mvc.png)

Spring은 다른 웹어플리케이션과 동일하게 front controller를 사용하고 있습니다.

아키텍쳐는 프론트 컨트롤러 패턴과 함께 사용하고 프론트 컨트롤러 패턴은 중앙 집중형 컨트롤러를 표현(presentation)계층의 제일 앞에서 서버로 들어오는 모든 요청을 받아서 처리합니다. 프론트 컨트롤러는 클라이언트의 요청을 받아 공통적인 작업을 먼저 수행 후 세부 컨트롤러에 위임합니다. 스프링에서는 *dispatcherServlet*이 프론트 컨트롤러의 역할을 합니다.

## Spring MVC
![spring mvc](https://www.tutorialspoint.com/spring/images/spring_dispatcherservlet.png)

1. 클라이언트의 요청(request)이 서버로 수신되면 *dispatcherServlet* 인스턴스로 송신됩니다. 
2. dispatcherServlet은 *HandlerMapping* 인스턴스를 참조하여 해당 *controller*로 전달합니다. 
3. 컨트롤러 인스턴스는 필요한 비즈니스 로직을 호출하여 결과(model)와 이동할 화면(view)정보를 dispatcherServlet에 반환합니다. 
4. dipatcherServlet은 *viewResolver* 인스턴스에 문의하여 view 정보를 반환하여 렌더링합니다.

### dispatcherServlet
클라이언트의 요청을 관리하는 핵심 컴포넌트
```
<servlet>
  <servlet-name>dispatcherServlet</servlet-name>
  <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    <init-param>
      <param-name>contextConfigLocation</param-name>
      <param-value>/WEB-INF/config/servlet-context.xml</param-value>
    </init-param>
    <load-on-startup>1</load-on-startup>
  </servlet>
  <servlet-mapping>
    <servlet-name>dispatcherServlet</servlet-name>
    <url-pattern>/</url-pattern>
  </servlet-mapping>
```

### viewResolver
컨트롤러부터 반환된 view 정보가 논리적인 이름일 경우 viewResolver 클래스를 통해 클라이언트에 출력할 view 객체를 반환합니다.
```
<beans:bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
  <beans:property name="prefix" value="/WEB-INF/views/" />
  <beans:property name="suffix" value=".jsp" />
</beans:bean>
```

### controller
비즈니스 로직을 호출하여 결과(model)와 화면 정보(view)를 dispatcherServlet에 반환합니다. 스프링 3.1부터 @RequestMapping은 RequestMappingHandlerMapping 클래스와 RequestMappingHandlerAdapter 클래스를 바로 불러옵니다. 

```
@Controller
@RequestMapping("/samdasu")
public class SamdasuController {
 
  @Resource(name="WaterService")
  private WaterService waterService;
    
  @RequestMapping( "/")
  public ModelAndView root() throws Exception{
    ModelAndView mv = new ModelAndView();
    ArrayList<Water> bottle = waterService.searchSource();
    mv.setViewName("home");
    mv.addObject("bottle", bottle);
   }
}
```

### HandlerMapping
컨트롤러의 모든 정보(클래스, 메서드, 리턴타입, 파라미터 타입 등)를 담고 있어 dispatcherServlet에서 요청이 오면 어떤 컨트롤러(controller)에 위임할 것인지 결정합니다.
