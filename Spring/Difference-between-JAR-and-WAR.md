# JAR와 WAR의 차이점
------------
- `JAR(Java Archive)`와 `WAR(Web Application Archive)`는 `JAVA`의 `jar`툴을 이용하여 생성된 아키이브 파일
- 어플리케이션을 쉽게 배포하고 동작시킬 수 있도록 관련 파일(리소스, 속성파일)들을 패키징 해주는 것이 주 역할

## JAR(Java Archive)
- `.jar`확장자 파일에는 `Class`와 같은 Java리소스와 속성 파일, 라이브러리 및 액세서리 파일이 포함
- Java 애플리케이션이 동작할 수 있도록 자바 프로젝트를 압축한 파일
- 원하는 구조로 구성이 가능
- `JDK`에 포함하고 있는 `JRE`만 가지고도 실행 가능

## WAR(Web Application Archive)
- `.war`확장자 파일은 `servlet/jsp` 컨테이너에 배치 할 수 있는 웹애플리케이션 압축 파일 포맷
- JSP, servlet, JAR, Class, xml, html, JS 등 `Servlet Context` 관련 파일들로 패키징 되어있음
- 웹 애플리케이션을 위한 포맷이기 때문에 웹 관련 자원만 포함하고 있고 이를 사용하면 웹애플리케이션을 쉽게 배포하고 테스트 할 수 있음
- `JAR`와 다르게 WEB-INF, META-INF 디렉토리로 사전 정의된 구조를 사용
- `WAR` 파일을 실행하려면 Tomcat, Weblogic, Websphere 등의 `웹서버` 또는 `WAS`가 필요

## EAR(Enterprise Archive)
