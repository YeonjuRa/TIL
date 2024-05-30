## MVC 패턴
#### JSP Model-1

Model 1은 
1) jsp 페이지
2) javaBeans 혹은 서비스 클래스

로 이루어져 있다.

JSP 페이지에서는 로직을 처리하는 코드와 출력을 위한 코드가 함께 있다.즉 html 페이지에 자바코드를 직접 삽입한다.

모델 1 에서는 브라우저(Client)에서 요청이 오면 jsp페이지는 직접 자바빈이나 서비스클래스(MODEL)를 사용하여 작업을 처리하고, 그 결과를 클라이언트에게 출력한다.

#### JSP Model-2
MVC 패턴이 적용된 모델
JSP model 2 는 크게 3가지로 나눌 수 있다.

1) 자바빈 혹은 서비스 클래스(model)
2) JSP(VIEW)
3) 서블릿(Controller)
   
#### MVC 패턴
Model, View, COntroller의 약자
**웹 애플리케이션을 세가지의 역할로 구분한 개발 방법론**
- Model - 서버에서 수행하는 실질적인 비즈니스 로직
- View - Controller 에서 전달받은 데이터를 사용자에게 보여주기 위해 출력하는 역할
- Controller - 사용자의 입력처리, 전체적인 흐름을 제어

Model-2 는 MVC 패턴과 같이 
1) 브라우저(Client)에서 요청이 들어오면 
2) 서블릿(Controller)이 전체 요청을 처리할 Model(자바빈,서비스클래스)를 선택한다.
3) 로직을 모두 처리하면 이를 클라이언트에 출력하기 위해 Jsp 페이지를 응답한다
   
   
