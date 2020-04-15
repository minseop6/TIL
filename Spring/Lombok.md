# Lombok

## Lombok이란?
- getter/setter나 toString 등의 코드를 어노테이션으로 대체해서 선언
- java코드를 컴파일 할 때 그에 맞는 코드를 생성해줌

## Lombok 다운로드
https://projectlombok.org/download

1. lombok.jar 다운로드
2. cmd에서 JDK설치 경로 이 (C:\Program Files\Java\jdk1.8.0_231\bin)
3. lombok.jar 실행 (java -jar 설치경로\lombok.jar)
4. 설치 진행

## Lombok 의존성 추가
#### Gradle
```java
//build.gradle
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

#### Maven
```xml
<!-- pom.xml -->
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.16.16</version>
</dependency>
```

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

## 자주 사용하는 어노테이션

### @ToString
- 해당 메소드의 모든 필드를 출력하는 toString 메소드를 생성

### @Getter / @Setter
- getter 함수와 setter 함수를 생성

### @Builder
- 빌더 패턴을 생성

### @EqualsAndHashCode
- hashcode와 equals 메소드를 생성

### @NoArgsConstructor
- 파라미터를 요구하지 않는 생성자를 생성

### @RequiredArgsConstructor
- 파라미터를 요구하는 생성자 생성

### @AllArgsConstructor
- 모든 인자를 가진 생성자를 생성

### @Data
- `@toString`, `@Getter`, `@Setter`, `@EqualsAndHashCode`, `@NoArgsConstructor`, `@RequiredArgsConstructor`, `@AllArgsConstructor` 를 모두 포함
