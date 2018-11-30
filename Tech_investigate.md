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
          * 사실 Apache Kafka는 원래 영리의 목적으로 개발된 것이 아닌 링크드인의 문제점을 보완하기 위해서 개발된 메시징 프레임워크 입니다.
             <img src="https://github.com/KimJeongHyun/Creative_Engineering/blob/master/Tech_investigate_Resource/LinkedIn_Archi.png">
          * 첨부된 사진은 링크드인의 기존 아키텍쳐입니다.
          * 기존 아키텍쳐는 Monitoring, Splunk, Relational Database, Key-value store, Relational Data Warehouse, Hadoop의 총 6개 부분으로 구성됩니다. 이 구성은 OLTP(실시간 트랜잭션 처리) 및 비동기 처리가 동시에 수행된다는 장점이 있지만 통합 전송 영역이 없으며 마치 트리, 또는 피라미드같은 구조로 인해 수정해야되는 부분이 중간에 있다면 앞단부터 전부 수정해야하는 단점이 있습니다. 즉 파이프라인 관리가 어렵습니다.
          * 위와 같은 문제를 해결하기 위해 새로운 시스템의 개발이 필요했고, 그것이 Apache Kafka 입니다.
          * 이후 SNS나 소셜 커머스, 웹 기반 활동 등이 주류를 이루면서 데이터가 점점 거대화됐고 기존의 Hadoop 오프라인 분석 시스템으로는 실시간성에 대한 한계가 발생하게 됩니다. 그 이유로 새로운 데이터 처리 시스템에 대한 수요가 발생했고, 2014년 이후부터 Hadoop, Spark, 그리고 Apache Kafka가 데이터 취합 파이프라인으로서 주목받게 됩니다.
          
