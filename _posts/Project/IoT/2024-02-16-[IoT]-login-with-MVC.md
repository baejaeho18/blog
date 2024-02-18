---
layout: post
title: "[IoT] 4. 웹서버 구동하기(3)"
category: project
tags: iot
author: author1
comments: true
---

> CCTV 노드들의 상태와 실시간 영상 스트리밍을 위한 웹 인터페이스 구축

# 4.1 MVC 구현
> model, view, controller

첫 화면에 로그인/회원가입 페이지를 띄워, 로그인을 해야만 home 화면에 접속할 수 있도록 한다. home 화면에서 좌측 2/3 부분이 mapList와 dashboard가 tab으로 전화할 수 있도록 한다.
home의 우측에는 cctv 상태 정보가 포함된 목록이 있다. cctv 목록에서 checkbox로 선택된 cctv들은 좌측 dashboard에서 영상으로 송출되고, mapList에서 marker로 위치정보를 표시한다.

# 4.2 로그인 화면 구현
> /login.html
첫 화면을 로그인/회원가입 화면으로 한다. 회원가입 후, 자동으로 로그인을 진행한다. 로그인이 완료되면 home 화면으로 이동한다.

```java
package com.example.demo.Config;

import {..}

@Configuration
@EnableWebSecurity
public class SecurityConfig {

    @Bean
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
        http
                .authorizeHttpRequests((auth) -> auth
                        .requestMatchers("/", "/login", "/signup").permitAll()
                        .requestMatchers("/home").authenticated()
                        .requestMatchers("/admin").hasRole("ADMIN")
                )
                .formLogin((form) -> form
                        .loginPage("/login")
                        .defaultSuccessUrl("/home", true)
                        .permitAll()
                );
        return http.build();
    }

    @Bean
    public UserDetailsService userDetailsService() {
        UserDetails user = User.withDefaultPasswordEncoder()
                .username("user")
                .password("password")
                .roles("USER")
                .build();
        UserDetails admin = User.withDefaultPasswordEncoder()
                .username("admin")
                .password("password")
                .roles("ADMIN", "USER")
                .build();
        return new InMemoryUserDetailsManager(user, admin);
    }
}
```

인터넷 블로그들에 퍼져있는 정보들은 대부분 SpringSecurity 라이브러리 3.0 버전 이전이라 에러들이 많았다. 3.0 버전 이전과 이후를 비교한 [블로그]도 있다.
따라서 spring [정규문서]로 들어가 어떻게 변했는지 직접 확인해야 했다. 해당 문서를 읽어보니 github에도 sample code들이 작성되어 있었다. [spring-security-samples] 레포지토리에서 필요한 코드들을 찾아 작성했다.

위 코드는 각 페이지들에 대한 접근 권한과 login 후 redirect할 path를 정의하고, default로 user와 admin 유저 두 명을 저장한다.


<!-- reference -->
[블로그] https://this-circle-jeong.tistory.com/162
[정규문서] https://docs.spring.io/spring-security/reference/servlet/authorization/authorize-http-requests.html
[spring-security-samples] https://github.com/spring-projects/spring-security-samples/blob/main/servlet/java-configuration/authentication/username-password/in-memory/src/main/java/example/SecurityConfiguration.java
