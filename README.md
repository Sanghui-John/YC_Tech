# YC_Tech
Yonsei University Codepresso Tech Academy
<br>Backend Web Programming

<p>
  <b>REST API 설계</b>
  <br>API : "Application Programming Interface"
  <br>다른 소프트웨어 애플리케이션과 상호 작용하기 위한 규칙과 규약을 정의한 인터페이스를 나타냄. 
  <br>API는 데이터나 서비스를 요청하고 응답하기 위한 <b>일련의 규칙</b>을 제공하며, 프로그래머가 다른 소프트웨어 컴포넌트와 상호 작용할 수 있게 해줌
  <br>API는 데이터를 제공하며, 클라이언트(사용자 또는 다른 애플리케이션)는 이를 통해 요청하고 응답을 받음. 요청과 응답은 일반적으로 데이터를 주고받는 형태이며, 클라이언트가 서버에게 무엇을 요청하고 어떻게 응답을 받을 것인지에 대한 규칙을 따름
  
  <br>REST 아키텍처는 <b>HTTP 프로토콜을 기반</b>으로 하므로, HTTP 메서드(GET, POST, PUT, DELETE 등)를 사용하여 요청을 수행하고, 상태를 변경하거나 데이터를 가져오는 데 사용됨. 
</p>
<p>
  <b>Controller 작성 & 설계</b> 
  <br>Controller : Spring Framework에서 웹 애플리케이션의 요청(Request)을 처리하고 응답(Response)을 생성하는 역할을 수행하는 클래스, Spring 웹 애플리케이션의 핵심 구성 요소 중 하나, 클라이언트로부터 들어오는 HTTP 요청을 받아들이고 그에 따른 작업을 처리한 뒤, 클라이언트에게 응답을 제공하는 역할을 하는 클래스
  <br>이를 통해 클라이언트(웹 브라우저, 모바일 앱, 다른 서비스)와 웹 애플리케이션 사이의 상호 작용을 관리함
  <b>컨트롤러의 주요 역할</b>
  <br>
  (1) HTTP 요청 처리: 컨트롤러는 특정 URL 경로로 들어오는 HTTP 요청을 수신하고 해당 요청을 처리하는 메서드를 호출. 예로, 웹 페이지에 접속하거나 API를 호출할 때 컨트롤러가 요청을 처리
(2) 비즈니스 로직 호출: 컨트롤러는 요청에 따라 필요한 비즈니스 로직을 호출. 이 비즈니스 로직은 데이터베이스 조회, 계산, 외부 서비스 호출 등과 같은 작업을 수행
(3) 데이터 모델 준비: 컨트롤러는 클라이언트에게 전달할 데이터 모델을 준비. 이 모델은 응답에 포함될 데이터를 나타내며, 주로 Java 객체로 표현
(4) 뷰 선택 및 데이터 전달: Spring MVC에서는 뷰(View)가 데이터를 가공하여 클라이언트에게 보여주는 역할. 컨트롤러는 적절한 뷰를 선택하고 데이터 모델을 뷰에 전달하여 화면 또는 응답 데이터를 생성
(5) 응답 생성: 컨트롤러는 뷰로부터 생성된 응답을 클라이언트에게 반환. 이 응답은 HTML 웹 페이지, JSON 데이터, XML 등의 형식
(6) HTTP 상태 코드 설정: 컨트롤러는 요청 처리 결과에 따라 HTTP 상태 코드를 설정. 이것은 클라이언트에게 요청 성공 또는 실패 여부를 공유
(7) 리다이렉션 및 예외 처리: 컨트롤러는 필요한 경우 클라이언트를 다른 URL로 리다이렉션하거나 예외를 처리.
<br>컨트롤러는 Spring MVC에서 웹 애플리케이션의 논리적 부분을 구성하며, 요청과 응답을 조율하여 사용자와 애플리케이션 간의 원활한 상호 작용을 도움. 이를 통해 웹 애플리케이션의 다양한 기능과 페이지를 구현하고 관리할 수 있음.



<br><b>컨트롤러 작성과 설계 단계</b>
<p>
  (1) 의존성 설정:
먼저 Spring 프로젝트를 시작하고 Spring MVC를 사용하려면 필요한 의존성을 설정이 필요. spring-web과 spring-webmvc 의존성을 프로젝트에 추가
    [xml]
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-web</artifactId>
            <version>현재_버전</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-webmvc</artifactId>
            <version>현재_버전</version>
        </dependency>
</p>
  <p>
    (2) 컨트롤러 클래스 작성:
    컨트롤러 : HTTP 요청을 처리하고 응답을 생성하는 클래스

    [java]
        import org.springframework.stereotype.Controller;
        import org.springframework.web.bind.annotation.GetMapping;
        import org.springframework.web.bind.annotation.ResponseBody;
        
        @Controller
        public class MyController {
        
            @GetMapping("/hello")
            @ResponseBody
            public String helloWorld() {
                return "Hello, World!";
            }
        }
    @Controller: 이 클래스가 컨트롤러임을 나타냄
    @GetMapping("/hello"): HTTP GET 요청이 "/hello" 경로로 들어오면 이 메서드를 실행하도록 설정
    @ResponseBody: 이 어노테이션은 메서드가 직접 HTTP 응답 내용을 반환함을 나타냄
  </p>
<p>
  (3) RequestMapping 및 메서드 정의 :
  컨트롤러 클래스 내에서 @RequestMapping 어노테이션 또는 HTTP 메서드에 대한 별도의 어노테이션(예: @GetMapping, @PostMapping)을 사용하여 URL 경로와 요청을 처리할 메서드를 정의. 각 메서드는 요청을 처리하고 응답을 생성하는 로직을 포함

</p>
<p>
  (4) 뷰 템플릿 설정(Optional) :
  만약 HTML 뷰를 생성하여 클라이언트에게 제공하려면 뷰 템플릿 엔진(예: Thymeleaf, JSP, FreeMarker 등)을 설정하고 뷰 템플릿을 작성.
</p>
<p>
  (5) DispatcherServlet 설정:
  Spring MVC를 사용하려면 DispatcherServlet을 설정해야 함. (웹 애플리케이션의 진입점 역할) Spring의 설정 파일(예: web.xml 또는 Java 설정 클래스)에서 DispatcherServlet을 설정
</p>
<p>
  (6) URL 매핑과 View 결정:
  컨트롤러 메서드에서 반환하는 데이터 또는 뷰 이름을 기반으로 Spring MVC는 적절한 뷰 템플릿을 결정하고 응답을 생성. URL 경로와 뷰 이름 간의 매핑을 통해 이루어짐
</p>
<p>
  (7) 실행 및 테스트:
  컨트롤러를 실행하기 위해 애플리케이션을 시작하고 브라우저 또는 API 클라이언트를 통해 컨트롤러에 요청을 보내고 응답을 확인
</p>

</p>

