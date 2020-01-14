# Lombok

## Lombok이란?
- getter/setter나 toString 등의 코드를 어노테이션으로 대체해서 선언
- java코드를 컴파일 할 때 그에 맞는 코드를 생성해줌

## Lombok 의존성 추가
build.gradle
```java
configurations {
	compileOnly {
		extendsFrom annotationProcessor
	}
}

dependencies {
    compileOnly 'org.projectlombok:lombok'
    annotationProcessor 'org.projectlombok:lombok'
}
```
## Lombok 다운로드
https://projectlombok.org/download

1. lombok.jar 다운로드
2. cmd에서 JDK설치 경로 이 (C:\Program Files\Java\jdk1.8.0_231\bin)
3. lombok.jar 실행 (java -jar 설치경로\lombok.jar)
4. 설치 진행

## Lombok 적용
VO 또는 Domain에 적용
```java
package com.ms.study.domain;

import java.time.LocalDateTime;

import javax.persistence.Column;
import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;
import javax.persistence.Table;

import org.hibernate.annotations.CreationTimestamp;
import org.hibernate.annotations.UpdateTimestamp;

import com.fasterxml.jackson.annotation.JsonIgnoreProperties;

import lombok.Getter;
import lombok.Setter;

@Entity //domain 클래스라는 것을 나타냄
@Table(name="board")
@JsonIgnoreProperties({"hibernateLazyInitializer", "handler"}) //Lazy 예외를 방지
@Getter
@Setter
public class Board {

	@Id //Primary key 컬럼인 것을 나타냄
	@GeneratedValue(strategy = GenerationType.IDENTITY)
	@Column(name="id")
	private Integer id;

	@Column(name="writer")
	private String writer;

	@Column(name="title")
	private String title;

	@Column(name="content")
	private String content;

	@CreationTimestamp
	@Column(name="created_time", updatable=false)
	private LocalDateTime created_time;

	@UpdateTimestamp
	@Column(name="updated_time", insertable=false)
	private LocalDateTime updated_time;

}

```
