# XML
----------------
## XML이란?
- Extensible Markup Language의 약자로 W3C 권고 확장성 있는 마크업 언어
- W3C가 인간과 응용프로그램간 또는 응용프로그램간에 정보를 쉽게 교환하기 위해 만든 데이터 교환 포맷
- eXtensible : 데이터를 설명하는 태그를 사용자 마음대로 정의할 수 있음

## XML과 HTML의 차이
- `XML`은 데이터를 전달하는 것에 포커스를 맞춘 언어
- `HTML`은 데이터를 표현하는 것에 포커스는 맞춘 언어
- `XML`은 `HTML`과 달리 태그가 미리 정의되어 있지 않음

## XML의 특징
- 표준성 : W3C에서 표준화를 주도하며 `SGML`과 `HTML`의 한계를 극복하기 위하여 만든 표준 인터넷 언어
- 분리성 : 표현과 내용이 완전히 분리됨, `XML`문서는 데이터 구조와 내용을 기술하고 있으며 스타일 시트를 이용하여 다양한 방식으로 데이터 표현
- 단순성 : `XML` 문서는 텍스트로 되어 있어 HW나 SW에 의존하지 않고 읽어 들일 수 있음
- 호환성 : `XML`의 특징중 단순성으로 시스템간에 상호작용을 중계하는데 이용할 수 있음
- 수용성 : `HTML`과 같이 현재 인터넷에서 가장 많이 사용되는 `HTTP` 프로토콜을 이용하여 전달
- 확장성 : `XML`은 확장성 있는 태그를 사용하고 있어 어떤 분야의 데이터든 정확하게 기술 가능
- 정확성 : `XML`의 문서의 경우 의미가 있는 태그를 사용함으로써 원하는 데이터를 쉽게 찾음

## XML 언어의 장점
- 텍스트로 이루어져 있어 어떤한 시스템이든 읽을 수 있음
- 문서 자체가 정보와 구조를 포함하고 있기 때문에 사람이 읽어도 그 안의 데이터의 의미를 쉽게 이해 가능
- `HTML`처럼 쉬우면서도 `SGML`의 강력한 기능을 갖음
- 확장성있는 마크업 언어로 데이터를 정의하는 태그를 마음대로 정의
- 새로운 마크업 언어를 만듬

## XML의 구조
#### - XML Tree Structure
  - XML 문서는 `root`에서 시작해서 `leaves`로 뻗어나가는 트리 구조
#### - The XML Prolog
  - XML 버전과 문자 인코딩을 정의하는 `Prolog`

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  ```

#### - XML Namespaces
  - `Name Confict`를 해결하기 위해 `XML`에서는 `Prefix`를 사용할 수 있음

  ```xml
  <h:table xmlns:h="http://www.w3.org/TR/html4/">
    <h:tr>
      <h:td>Apples</h:td>
      <h:td>Bananas</h:td>
    </h:tr>
  </h:table>

  <f:table xmlns:f="https://www.w3schools.com/furniture">
    <f:name>African Coffee Table</f:name>
    <f:width>80</f:width>
    <f:length>120</f:length>
  </f:table>
  ```

#### - DTD(Document Type Definition)
  - `XML`문서의 구조를 정의

  ```xml
  <!DOCTYPE food [
  <!ELEMENT food (name,type,cost)>
  <!ELEMENT name (#PCDATA)>
  <!ELEMENT type (#PCDATA)>
  <!ELEMENT cost (#PCDATA)>
  ]>
  <food>
      <name>상추</name>
      <type>야채</type>
      <cost>2000</cost>
  </food>
  ```

#### - XML Schema
  - `DTD`와 유사하게 `XML`문서의 구조를 정의하는 기능이 있지만 그 자체가 `XML Syntax`로 쓰여진 xml 문서

  ```xml
  <xs:element name="food">
    <xs:complexType>
        <xs:sequence>
            <xs:element name="name" type="xs:string"/>
            <xs:element name="type" type="xs:string"/>
            <xs:element name="cost" type="xs:string"/>
        </xs:sequence>
    </xs:complexType>
  </xs:element>
  ```
