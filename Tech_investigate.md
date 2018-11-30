# 창의공학기초설계 기술 조사하기
### 서울시립대학교 컴퓨터과학부 4학년 김정현
##### 학번 : 2015920069
---
- 1차 수행 과제 요약
  * 현재 진행 중인 프로젝트에 쓰일 수 있을 만한 기술 조사하기
    - 특이사항 : 각 Component(Server,Client,Database,Cache) 에 대한 기술을 조사할 것.
    - 조사한 기술
      1. Database : OLAP & OLTP, Data visualization, GPU Computing, Apache kafka
      2. Server : MySQL, PHP, Scale Up & Out
      3. Client : CSS, HTML, Javascript
      4. Cache : Multi-layer Caching
    - 선택한 기술
      * Apache Kafka
    - 이유
      1. 만들고자 하는 프로젝트가 '실시간' 특성을 가지고 있음
      2. 제휴 플랫폼의 인지도가 낮을 것
          - 유저 수요가 크지 않을 것으로 예상됨
            - 서버 증설은 고려할 요인이 많음
              * 따라서 H/W 보단 S/W 적 기술에 집중할 필요성이 있음
---
- 2차 수행 과제 ( Until 2018-12-07 )
  * Apache Kafka에 대한 조사
      - 기본 개요
          1. 2011 소셜 네트워크 서비스(SNS) 운영 회사인 링크드인이 최초로 개발한 오픈소스 프로젝트.
          2. 일종의 스트리밍 플랫폼을 지향함
          3. Database, Application 과의 상호작용 및 실시간 데이터 분석을 지원
          4. Apple, Cisco, Ebay, Amazon, Kakao 등의 기업이 선택한 프로젝트
      - 개발 역사
          1. 2011년 초 오픈 소스화를 통해 링크드인이 공개
          2. 2012년 10월 23일 아파치 인큐베이터로부터 독립화
          3. 2014년 11월 Kafka 개발 엔지니어들이 Confluent 회사로 분리됨
      - 개발 비화
          * 사실 Apache Kafka는 영리의 목적으로 개발된 것이 아닌 링크드인의 문제점을 보완하기 위해서 개발된 메시징 프레임워크 입니다.
          
