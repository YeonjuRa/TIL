## AOP, Filter, Interceptor 

프로그래밍 중에는 공통적인 기능이 많이 발생한다.


이러한 기능을 모든 모듈에 적용하려면 -> 상속 


하지만 java에서는 다중 상속이 불가능하고 , 상속으로 모든 모듈에 공통 기능을 부여하기에는 **한계가 존재**

예를들어 로그인 시 세션 분기, 권한 체크 등등

즉 공통적으로 존재하는 부분은 따로 빼서 관리하는 것 이 좋다. 
**프로그램 흐름의 앞, 중간, 뒤에 자동으로 추가해서 관리한다.**

위와 같은 공통처리를 위해 Spring 에서 쓰는 방법은 세가지가 있다


1) **Filter** - 요청과 응답을 거르고 정제; 
    
    필터가 동작하도록 지정된 자원의 앞에서 요청내용을 변경하거나 , 여러가지 체크 수행; 
    

    Filter는 Spring이 실행되기 전 실행되고 톰캣과 같은 WebContainer(WAS)에서 처리;


    일반적으로 인코딩 변환 처리,XSS방어 등의 요청에 대한 처리로 사용;

    - 공통된 보안 및 인증/인가 관련 작업(XSS)방어
    - 문자열 인코딩 변환 처리
    - Spring과 분리되어야 하는 기능


    

   

```
package com.gd.AOPTest;

import java.io.IOException;

import jakarta.servlet.Filter;
import jakarta.servlet.FilterChain;
import jakarta.servlet.ServletException;
import jakarta.servlet.ServletRequest;
import jakarta.servlet.ServletResponse;
import jakarta.servlet.annotation.WebFilter;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpSession;


@WebFilter("/member/*")
//member 이라고 시작되는 모든  호출 할 시 필터 실행 
//Filter -> servlet 꺼여서 스프링이 자동으로 인식 하지 못함 
public class MyFilter implements Filter{

	@Override
	public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain)
			throws IOException, ServletException {
		
		request.setCharacterEncoding("UTF-8");
		
		//requst.setCharacterEncoding 같은거 적어두면 일일히 할 필요 없음 . 
		System.out.println("==== Before Filter ====");
		chain.doFilter(request,response);
		
		
		System.out.println("==== After Filter ====");
		// TODO Auto-generated method stub
	//재귀호출 ->함수가 자기자신호출 ->recurive call 
	}
	
}

```

doFilter() - 전/후 처리 

2) **Interceptor** - 요청에 대한 작업 전/후로 가로챈다. 
   
   스프링 컨텍스트 내부에서 Controller(Handler)에 관한 요청과 응답에 대해 처리

   - 세부적인 보안 및 인증 공통작업(특정 사용자는 특정 기능을 사용못하게 막음)
   - API 호출에 대한 로깅
   - Controller로 넘겨주는 정보(데이터)의 가공(객체 자체를 조작 X -> 해당 객체가 내부적으로 갖는 값을 조작 O)
  
  

preHandler()- 컨트롤러 메서드가 실행되기 전
postHanlder() - 컨트롤러 메서드 실행 직 후 view 페이지 랜더링 전 



3) **AOP** -  OOP(Object Oriented Programming )를 보완하기 위해 나온 개념; AOP - Aspect Oriented Programming;

객체 지향의 프로그래밍을 했을 때 중복을 줄일 수 없는 부분을 줄이기 위해 종단면(관점)을 중심으로 바라보고 처리한다.
Interceptor와 Filter 와는 달리 메소드 전후의 지점에서 **자유롭게 설정 가능**

interceptor와 filter는 주소로 대상을 구분해서 걸러내야 하지만,AOP는 주소, 파라미터, 애노테이션 등 **다양한 방법**으로 대상을 지정 할 수 있다. 

- 로그처리
- 트랜젝션
- 에러처리 

```
@Aspect
//@Aspect ->AOP component 만들어주기 스프링 AOP -> 특정 메서드를 가로채서 그 전후에 -- 를 한다. 
//AOP는 라이브러리를 추가해야한다 
@Component
public class MyAop {
	
	//가로채고싶은 메서드의 풀네임 +(..) -> 매개변수는 상관없음 
	@Before("execution(* com.gd.AOPTest.HelloController.b(..))")
	public void beforePrint() {
		System.out.println("before AOP");
	}
	
	@After("execution(* com.gd.AOPTest.HelloController.b(..))")
	public void afterPrint() {
		System.out.println("after AOP");
	}
}

```

@Before - 대상 메서드의 수행전


@After - 대상 메서드의 수행 후 


세 가지 모두 무슨 행동을 하기 전에 먼저 실행되거나, 행동 후에 추가적인 행동을 할 때 사용되는 기능들이다.



#### 차이점:
- Interceptor, Filter 는 Servlet 단위로 실행, 메서드 앞의 **Proxy 패턴의 형태**

- **Filter** => 스프링 영역 밖, **Interceptor,AOP** => 스프링 영역 안 
- 실행순서 차이: Filter 가 제일 밖 -> 그 안에 Interceptor -> 그 안에 AOP

- 요청이 들어오면:
Filter -> Interceptor -> AOP -> Interceptor - Filter 순으로 실행 



-----



참고한 사이트 :


https://goddaehee.tistory.com/154

https://mangkyu.tistory.com/121

https://velog.io/@sweet_sumin/Interceptor-Filter-AOP%EC%9D%98-%EC%B0%A8%EC%9D%B4




