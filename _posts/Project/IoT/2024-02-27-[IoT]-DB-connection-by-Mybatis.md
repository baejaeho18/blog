---
layout: post
title: "[IoT] 3. DB와 연동하기(1)"
category: project
tags: iot
---

> CCTV 노드들의 상태와 실시간 영상 스트리밍을 위한 웹 인터페이스 구축

# 3.1 JPA & Mybatis
MyBatis 프레임워크는 반복적인 JDBC 프로그래밍을 단순화하여, 불필요한 Boilerplate 코드를 제거하고, Java 소스코드에서 SQL문을 분리하여 별도의 XML 파일로 저장하고, 이 둘을 서로 연결시켜주는 기능을 제공한다. 개발자는 Java 메소드 선언과 SQL문만 만들면 MyBatis가 자동으로 그 둘을 매핑시킨다.
Dynamic SQL 생성 기능을 제공하여 프로그램 실행 중에 입력되는 파라미터에 따라 서로 다른 SQL문을 동적으로 생성해 내는 기능을 제공한다.

JPA(Java Persistence API)는 Java 객체와 관계형 데이터베이스 간의 매핑을 위한 API다. JPA는 ORM(Object-Relational Mapping)을 구현하는 자바 표준 스펙으로, 개발자가 객체지향 프로그래밍 언어에서 사용하는 객체 모델과 관계형 데이터베이스의 테이블 간의 매핑을 자동으로 처리해준다. 
개발자는 SQL문을 작성할 필요가 없어지고, DB가 바뀌어도 DB에 따라 새로운 SQL을 작성할 필요가 없이 Hibernate와 같은 프레임워크에서 DB에 맞는 적합한 SQL문을 생성해준다.

<!--more-->

MyBatis와 JPA 모두 DB를 사용할 때 번거로운 반복작업을 줄여준다. MyBatis는 SQL문을 Java와 분리하여 별도 파일로 관리할 수 있어 SQL 개발과 유지 보수에 용이하고, JPA는 SQL문을 아예 만들 필요가 없기 때문에 더욱 자동화되어 반복작업을 극적으로 줄여준다.

Mybatis는 개발자가 SQL을 직접 작성하고 최적화할 수 있다. 또한 복잡한 쿼리 또는 특정 데이터베이스에 최적화된 쿼리 작성이 필요한 경우에 적합하다. 물론 index와 join과 같은 SQL문에 대한 이해가 뒷받침되어야 효과적으로 제어할 수 있다.
한편, JPA는 객체와 데이터베이스 간의 자동 매핑을 지원하기 때문에 별도의 SQL 작성을 필요로 하지 않는다. 테이블 간의 연관 관계와 객체 간의 연관 관계를 쉽게 다룰 수 있어 객체 지향적 개발에 어울리며, DB 종류에 종속적이지 않게 SQL이 자동으로 작성된다. 다만 JPA 작성법(@Entitity, @Table, @Column, @Id, @OneToMany, @ManyToOn)과 발생하는 이슈(즉시 로딩, 지연 로딩, 영속성 전이, 복합키 매핑 등)에 대해 익혀야 한다.

본 프로젝트는 작은 테이블에서 적은 sql 요청을 보낼 것이다. 따라서 프레임워크에 대한 이해를 하고 싶다면 JPA를 고르고, sql에 대한 간단히 복습만 하고 싶다면 Mybatis를 선택하면 될 것 같다.
JPA를 더 공부하고 만들기에는 시간이 부족하기에 우선 Mybatis로 동작하는 것을 목표로 하고, 차후 JPA로 대체해보도록 하겠다.

# 3.2 Setting for Mybatis





<!-- Links -->
[Mybatis 연동]: https://engineerinsight.tistory.com/219
[Mybatis와 JPA 비교]: https://www.elancer.co.kr/blog/view?seq=231