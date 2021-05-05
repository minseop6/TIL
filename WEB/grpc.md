# gPRC

## RPC
- 한 프로그램이 네크워크의 세부정보를 이해하지 않고도 네트워크 안의 다른 컴퓨터에 있는 프로그램에서 서비스를 요청하는 프로토콜
- client-server 모델을 사용
- 클라이언트에서 서비스를 요청하면, 서버에서 서비스를 제공

## gRPC
- gRPC는 Google에서 개발한 RPC(Remote Procedure Call) 시스템
- 전송을 위해 TCP/IP 프로토콜과 HTTP 2.0 프로토콜을 사용
- IDL(Interface Definition Language)로 Protocol buffer 사용
- Java, C++, Python, Ruby, Javascript, Objective-C, C# 등에서 사용 가능
- SSL/TLS를 사용하여 서버를 인증하고 클라이언트와 서버간에 교환되는 모든 데이터를 암호화함
- HTTP 2.0을 사용하여 성능이 뛰어나고 높은 헤더 압축률을 보장
- 프로토콜 버퍼는 바이너리 데이터이므로 변환 작업 없이 빠르게 처리할 수 이음
- gRPC에서 클라이언트 응용 프로그램에서 서버에서 함수를 바로 호출 할 수 있어서 MSA에 적합함
- 서버에서는 서버 인터페이스를 구현하고 gRPC서버를 실행하여 클라이언트의 호출을 처리