---
layout: post
title: "Data Model"
date: 2021-07-12
categories: wiki
tags: [data]
---

## Data Model

- 데이터 모델은 해결하려는 문제를 어떻게 생각해야 하는지 자체에 영향을 줌
- 각 데이터 모델은 사용 방법에 대한 가정(어떤 사용법/동작을 지원할지, 어떤 연산을 많이 하게 될 지, 어떤 변환을 허용할지 등)을 포함하기 때문

1. Relational Model: 각 데이터는 table(relation) 내부의 tuple(row)로 모델링됨 ~ SQL
   - 게시판, SNS, 게임, SaaS 등 대부분 서비스들이 사용하는 모델
2. NoSQL
   - 대규모 데이터, write-dominant한 케이스, 오픈소스에 대한 선호, SQL에서 지원하지 않는 특수 질의, SQL 스키마에 대한 불만 등이 기반이 되어 만들어짐
   - Document model, Graph-based model
   - 동적 모델
3. Polyglot persistence: SQL + NoSQL

### 이력서 예시

예를 들어 이력서 정보를 모델링한다고 해보자.  
이 데이터는 사람 한명이 여러 직위, 학력, 연락처 등 다수의 정보를 가지고 있는 형태(one-to-many)가 될 것이다

#### 데이터 모델링

이러한 정보를 SQL로 모델링하는 방법은 여러가지고 생각해볼 수 있는데,

  1. Conventional SQL
     - 직위, 학력, 연락처 등을 각각의 테이블로 두고 '사람' 테이블에서 외래 키로 참조하는 방법
  2. SQL + xml
     - 단일 row의 하나의 필드에 여러 값을 저장할 수 있도록 xml 형태로 저장
  3. 부호화
     - text column에 정보를 부호화해서 넣고 애플리케이션 단에서 처리하는 방법
     - db 단에서는 부호화된 정보에 대한 query를 할 수 없음

반면 NoSQL로 모델링하는 경우,

  1. JSON
     - [Document-oriented db](document-oriented-data-model.MD)들이 지원하는 모델
     - 장점: 전통적인 SQL 방식에 비해 높은 locality (여러 테이블에 정규화되어 있는 경우 query할 때 각 테이블을 불러와야 하고 다중 조인을 수행해야 한다)
     - json은 tree 구조여서 1-to-many 형태의 데이터 표현에 적합

#### 세부 사항

- 

## Reference

- `마틴 클레프만, 데이터 중심 애플리케이션 설계`