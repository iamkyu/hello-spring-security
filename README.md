# hello-spring-security

> Spring Security is a framework that provides authentication, authorization, and protection against common attacks. With first class support for both imperative and reactive applications, it is the de-facto standard for securing Spring-based applications.

## DelegatingFilterProxy
- 스프링 시큐리티는 서블릿에서 서블릿 필터를 기반으로 처리하는 것들이 많음.
- 스프링웹 에서는 `DelegatingFilterProxy` 라는 이름의 서블릿 컨테이너 - 스프링의 애플리케이션 컨텍스트를 이어주는 `javax.servlet.Filter` 를 제공.
- 이를 통해 서로 다른 컨텍스트인 서블릿 컨텍스트에서 스프링 컨텍스트에 정의 된 빈을 사용할 수 있게 함.
- 또한 서블릿 필터는 서블릿 컨테이너가 시작되기 전 모두 구성이 완료되어야 하는 반면, 스프링 빈들은 이 시점에 아직 로드 되지 않는 라이프 사이클 문제를 해결해주기도 함.

### See Also
- `org.springframework.boot.autoconfigure.security.servlet.SecurityFilterAutoConfiguration`
- `org.springframework.boot.web.servlet.DelegatingFilterProxyRegistrationBean`
- https://docs.spring.io/spring-security/site/docs/5.4.2/reference/html5/#servlet-delegatingfilterproxy


## FilterChainProxy
- 앞선 `DelegatingFilterProxy` 를 생성시 스프링 컨텍스트와 컨텍스트에서 찾을 빈 이름을 전달.  해당 이름을 가진 빈은 `FilterChainProxy`.
- `DelegatingFilterProxy` 은 스프링웹 모듈에서 정의되었지만 `FilterChainProxy` 은 스프링시큐리티 모듈에서 정의되어 다양한 시큐리티 필터를 연결함.

### See Also
- `org.springframework.security.web.context.AbstractSecurityWebApplicationInitializer.DEFAULT_FILTER_NAME`
- `org.springframework.security.config.annotation.web.configuration.WebSecurityConfiguration`
- https://docs.spring.io/spring-security/site/docs/5.4.2/reference/html5/#servlet-filterchainproxy


## Authentication
- 인증 요청 또는 인증된 주체에 대한 토큰을 나타내는 인터페이스
- 실제 구현체들은 모드 접미사로 *Token 이라는 이름을 가짐

`Authentication` 은 스프링 시큐리티에서 크게 2가지 역할을 함.
1. 사용자가 제공한 인증 정보를 `AuthenticationManager` 에 전달
2. 현재 인증 된 사용자 나타냄. `Authentication` 로 부터 principal, credentials, authorities 을 얻을 수 있음.

### See Also
- https://docs.spring.io/spring-security/site/docs/5.4.2/reference/html5/#servlet-authentication-authentication


## SecurityContext & SecurityContextHolder
- `SecurityContext` 는 현재 스레드에 최소한의 보안에 관한 정보를 정의하는 인터페이스. 앞서 정리한 `Authentication` 를 set, get 하는 시그니처만 가짐.
- `SecurityContextHolder` 는 `SecurityContext` 를 담고 있고 모든 시그니처는 정적(static)으로 제공 됨.
- `SecurityContextHolder` 가 `SecurityContext` 를 저장하는 모드는 크게 3가지. MODE_THREADLOCAL, MODE_INHERITABLETHREADLOCAL, MODE_GLOBAL

### See Also
- https://javacan.tistory.com/entry/ThreadLocalUsage
- https://stackoverflow.com/questions/45725888/why-does-spring-security-store-securitycontext-in-thread-local-variable


## 참고
- [스프링 시큐리티 - Spring Boot 기반으로 개발하는 Spring Security](https://www.inflearn.com/course/%EC%BD%94%EC%96%B4-%EC%8A%A4%ED%94%84%EB%A7%81-%EC%8B%9C%ED%81%90%EB%A6%AC%ED%8B%B0#)
- [Spring Security Reference 5.4.2](https://docs.spring.io/spring-security/site/docs/5.4.2/reference/html5/)