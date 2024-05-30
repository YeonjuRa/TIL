# 웹에서의 데이터 저장 영역
### request

- 연결이 유지되는 동안은 유지 될 수 있는 데이터를 가진다.
- 하나의 요청에 의해 호출된 페이지와 forward(요청전달)된 페이지 까지 공유된다.
- 단 페이지 이동 시에는 소멸되어 사용 할 수 없다.
  
Class: ServletRequest / HttpServletRequest

Set : request.setAttribute(key,value)

Get : request.getAttribute(ket)

Delete : request.removeAttribute(key,value)

**request내장객체를 통해 forward를 수행하는 코드**
```
request.getRequestDispatcher("포워드된 파일 경로").forward(request, response)
```
### session

- 웹 브라우저가 종료되기 전까지 유지될 수 있는 데이터 영역을 가진다 
- 클라이언트가 처음 접속한 후 웹 브라우저를 닫을 때 까지 공유된다.
  

Class: HttpSession

Set : session.setAttribute(key,value)

Get: session.getAttribute(key)

Delete: session.removeAttribute(key,value)

**session이란?**
```
클라이언트가 서버에 접속해 있는 상태 혹은 단위를 말한다.

- 주로 회원인증 후 로그인 상태를 유지하는 처리에 사용된다.
- 사이트에서 웹 브라우저를 닫으면 자동으로 로그아웃 되는 이유는 이 session 객체의 특성 때문이다. 

```


### application

- 서버가 종료 되기 전까지 유지될 수 있는 데이터 영역을 담는다.
- 한 번 저장되면 웹 애플리케이션이 종료될때 까지 유지된다.
- 즉, 웹 애플리케이션은 단 하나의 application 객체만 생성하고, 클라이언트가 요청하는 모든 페이지가 application 객체를 공유하게 된다.
또한, application 객체는 웹 서버를 시작할 때 만들어지며, 웹 서버를 내릴 때 삭제된다.
- application 영역에 한 번 저장된 정보는 페이지를 이동하거나, 웹 브라우저를 닫았다가 새롭게 접속해도 삭제되지 않는다.

Class: ServletContext

Set : application.setAttribute(key,value)

Get: application.getAttribute(key)

Delete: application.removeAttribute(key, value)

## 요약

- request 영역 - 하나의 요청에 의해 호출된 페이지와 포워드된 페이지까지 공유.새로운 페이지를 요청 시 소멸
- session 영역 - 클라이언트가 처음 접속 한 후 웹 브라우저를 닫을 때까지 공유된다. 포워드나 페이지 이동 시에도 영역은 소멸되지 않는다.
- application 영역 - 한번 저장되면 웹 애플리케이션이 종료될때까지 유지(즉, 서버가 셧다운 되지않는다면 언제까지든 공유되는 영역이다.)






<br>
<br>

**참고한 사이트**

[1] https://velog.io/@xnfxnf97/JSP-%EB%82%B4%EC%9E%A5-%EA%B0%9D%EC%B2%B4-%EC%98%81%EC%97%AD

[2] https://bloodygale.tistory.com/entry/Servlet-%EC%9B%B9%EC%97%90%EC%84%9C%EC%9D%98-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EC%A0%80%EC%9E%A5