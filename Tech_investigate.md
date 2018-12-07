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
  * Apache Kafka의 기본 정보
  
      - 기본 개요
          1. 2011 소셜 네트워크 서비스(SNS) 운영 회사인 LinkedIn이 최초로 개발한 오픈소스 프로젝트.
          2. 일종의 스트리밍 플랫폼을 지향함
          3. Database, Application 과의 상호작용 및 실시간 데이터 분석을 지원
          4. Apple, Cisco, Ebay, Amazon, Kakao 등의 기업이 선택한 프로젝트
      - 개발 역사
          1. 2011년 초 오픈 소스화를 통해 링크드인이 공개
          2. 2012년 10월 23일 Apache Incubator로부터 독립화
          3. 2014년 11월 Kafka 개발 엔지니어들이 Confluent 회사로 분리됨
      - 개발 비화
          * 사실 Apache Kafka는 원래 영리의 목적으로 개발된 것이 아닌 링크드인의 문제점을 보완하기 위해서 개발된 메시징 프레임워크 입니다.
          
             <img src="https://github.com/KimJeongHyun/Creative_Engineering/blob/master/Tech_investigate_Resource/LinkedIn_Archi.png">
             
          * 첨부된 사진은 링크드인의 기존 아키텍쳐입니다.
          * 기존 아키텍쳐는 Monitoring, Splunk, Relational Database, Key-value store, Relational Data Warehouse, Hadoop의 총 6개 부분으로 구성됩니다. 이 구성은 OLTP(실시간 트랜잭션 처리) 및 비동기 처리가 동시에 수행된다는 장점이 있지만 통합 전송 영역이 없으며 마치 트리, 또는 피라미드같은 구조로 인해 수정해야되는 부분이 중간에 있다면 앞단부터 전부 수정해야하는 단점이 있습니다. 즉 파이프라인 관리가 어렵습니다.
          * 위와 같은 문제를 해결하기 위해 새로운 시스템의 개발이 필요했고, 그것이 Apache Kafka 입니다.
          * 이후 SNS나 소셜 커머스, 웹 기반 활동 등이 주류를 이루면서 데이터가 점점 거대화됐고 기존의 Hadoop 오프라인 분석 시스템으로는 실시간성에 대한 한계가 발생하게 됩니다. 그 이유로 새로운 데이터 처리 시스템에 대한 수요가 발생했고, 2014년 이후부터 Hadoop, Spark, 그리고 Apache Kafka가 데이터 취합 파이프라인으로서 주목받게 됩니다.
       
  * Apache Kafka란?
      1. 확장성, 고가용성을 지닌 메세지 브로커
      2. 오픈소스 분산 발행-구독 메시징 시스템
      3. 웹사이트, 어플리케이션, 센서 등에서 취합한 데이터 스트림을 실시간으로 관리하기 위한 오픈소스 시스템
      
  * Apache Kafka의 시스템
      - Producer, Consumer를 분리
      - 영구 메세지 데이터를 여러 Consumer에게 허용
      - 높은 처리량을 위해 메세지 최적화
         1. 일반 상용 서버에서도 초당 수백만 건의 메세지 처리 가능
      - 데이터 증가에 따라 Scale Out[^1]이 가능
      - 다양한 Client에 대한 지원
         1. Java, Scala로 작성됨
         2. Dot net, PHP, Ruby, Python 등 다양한 플랫폼과 연동 가능
      - 분산 처리
         1. 파티셔닝 지원을 통한 다수 서버에 대한 분산처리
         2. load balancing[^2], fault tolerance[^3] 수행 가능
      - 메세지 비휘발성
         1. 디스크 구조로 디자인된 인메모리 
      - 실시간성
         1. Producer Thread에서 생성된 메세지는 즉시 Consumer Thread에서 처리

 * Apache Kafka의 체계
 
      <img src="https://github.com/KimJeongHyun/Creative_Engineering/blob/master/Tech_investigate_Resource/Kafka_NewArchi.png">
      
    1. 기존 (트리||피라미드)와 유사했던 구조와 달리 하나의 플랫폼에서 여러 기능을 지원하는 방식으로 변화
    2. Kafka Platform이 제공하는 표준 포맷으로 통일되어 데이터 전송에 용이
    3. 변경 사항 발생시 Data store backend 관리 및 format, 기타 Application 개발이 필요했으나 이제 Platform에서 데이터를 가져다 쓰기만 하면 됨
 
 * Apache Kafka의 활용
    1. 연관 검색
    2. 인기도, 동시성, 감정 분석 기반 추천 시스템
    3. 대중 광고 전달
    4. 스팸, 미허가 데이터 수집에 대한 인터넷 Application 보안
    5. 어플리케이션 통계 수집
    6. 인터넷 유저의 웹 사이트 활동 기록 추적
    7. 메세지 처리
    
 * Apache Kafka의 시나리오와 동작 원리
 
      <img src="https://github.com/KimJeongHyun/Creative_Engineering/blob/master/Tech_investigate_Resource/Kafka_Scenario.jpg" width="40%">
      <img src="https://github.com/KimJeongHyun/Creative_Engineering/blob/master/Tech_investigate_Resource/Kafka_Scenario2.png" width="60%">
      
      - 위 첨부사진은 빅데이터 집계 및 분석 시나리오에서 Kafka의 작용을 표현함.
      - Kafka는 Zookeeper[^4]에 의해 관리되며, Producer[^5], Broker[^6], Consumer[^7]로 구성됨
        1. 시스템에서 메세지 발생
        2. Producer가 메세지를 Broker에게 전달
        3. Broker가 Consumer에게 메세지를 분산처리
        4. Consumer가 분산된 데이터를 디스크에 저장함
      - 데이터 저장소 'Topic'과 'Partition' (심화)
        1. Topics
           - Kafka는 Topics 라는 Pipeline에 데이터 레코드 스트림을 저장함
           - 게시하고자 하는 레코드에 대한 범주 또는 피드의 이름
           - Topics의 구성 ↓
           <img src="https://github.com/KimJeongHyun/Creative_Engineering/blob/master/Tech_investigate_Resource/Kafka_TopicWithPartition.png" width="60%">  
           
           - Topics는 쉽게 말해 Kafka Cluster에 들어온 데이터가 분류된 것임.
           - Topic들은 여러 노드에 분산된 Partition에 분산되어 저장됨.
           
        2. Partition
           - Partition은 Topics 파이프 라인에서 데이터를 분산시키기 위한 구조
           - Partition의 구성 ↓
           <img src="https://github.com/KimJeongHyun/Creative_Engineering/blob/master/Tech_investigate_Resource/Kafka_Partition.png" width="60%">  
           
           - Partition은 레코드가 순서대로 쌓이며, Consumer가 어디까지 메세지를 읽었는지 offset이 저장됨. 이 때 로그의 위치정보만으로 메세지를 읽을 수 있어 매우 가벼움
           
        3. Topics' Partition's distribution
        
           <img src="https://github.com/KimJeongHyun/Creative_Engineering/blob/master/Tech_investigate_Resource/Kafka_Variation.png" width="60%">
           
           - 위의 사진은 Kafka 분산을 설명하는 사진임.
           - Kafka는 이들 중 하나의 Partition으로 메세지를 전송하는 데, 이 때 라운드로빈 등의 알려진 알고리즘이나 직접 구현된 알고리즘을 사용할 수 있음. 따라서, 메세지 순서가 중요한 서비스의 경우 대비책이 필요함
           
        4. Topics' Partition's Replication 
        
           <img src="https://github.com/KimJeongHyun/Creative_Engineering/blob/master/Tech_investigate_Resource/Kafka_PartitionCopy.png" width="60%">
           
           - 위의 사진은 Kafka Partition에서 복제의 수행을 설명하는 사진임.
           - 이것은 Master-Slave 방식을 통해 복제됨.
           - P0-L이 리더가 되어 P0-R1, P0-R2가 팔로워 역할을 수행
           - 메세지의 R/W는 P0-L만 수행하며 하나의 노드에 문제가 생기더라도 타 노드의 파티션을 통해 메세지를 주고 받을 수 있음.
        
        5. 평가
           - Kafka는 Topics 파이프라인 구조를 이용해 데이터의 구분이 용이
           - Partition의 분산, 복제 운용을 통해 전송 속도의 개선 뿐만 아니라 장애가 발생했을 때의 대책까지 마련되어 있음.

* Apache Kafka의 성능
  - Zero Copy 기법
     - Zero Copy는 커널 영역에서 파일 데이터를 읽고 바로 소켓에 데이터를 담아 전달하는 기법으로, 평범하게 정적파일을 전송할 때 커널~유저 영역을 넘나들 때마다 매번 복사가 일어나 불필요하게 CPU와 메모리를 점유하는 것을 해결하는 방법임.
     - Kafka는 파일 시스템의 메세지를 네트워크를 통해 consumer로 전송할 때 Zero Copy 기법을 이용해 데이터 전송 성능을 향상시켰음.
     - 평범한 파일 데이터 전달 방식 ↓
     
     <img src="https://github.com/KimJeongHyun/Creative_Engineering/blob/master/Tech_investigate_Resource/Kafka_StdTransfer.gif" width="60%">  
     
     - Zero Copy의 전달 방식 ↓
     
     <img src="https://github.com/KimJeongHyun/Creative_Engineering/blob/master/Tech_investigate_Resource/Kafka_ZeroCopy.gif" width="60%">  
  
  - 성능
     - 이하 첨부된 사진은 기존 메시징 시스템과 비교한 Producer, Consumer의 성능 차이를 비교한 그래프로 파랑, 보라색 선이 기존 시스템의 성능이며 batch 수에 따라 Kafka의 성능은 초록색, 빨간색으로 구분되어 있습니다.
  
     - Producer 성능 ↓
     <img src="https://github.com/KimJeongHyun/Creative_Engineering/blob/master/Tech_investigate_Resource/Kafka_ProducerPerformance.png" width="60%">
     
     - Consumer 성능 ↓
     <img src="https://github.com/KimJeongHyun/Creative_Engineering/blob/master/Tech_investigate_Resource/Kafka_ConsumerPerformance.png" width="60%">
     
     - 평가
        1. 대용량의 실시간 로그 처리에 특화되어 있어 기존 시스템 대비 TPS[^8]가 매우 우수함.
        2. 분산 시스템을 기반으로 하기 때문에 기존 메시징 시스템에 비해 분산 및 복제 구성이 손쉽다.
        3. 간단한 TCP 프로토콜을 이용해 오버헤드가 감소됨.
        4. 메시지가 메모리가 아닌 파일 시스템에 저장됨.
           - 메모리에 저장하지 않기 때문에 메세지를 많이 저장해도 성능이 크게 감소하지 않는다.
           - 일정 기간을 두고 삭제하기 때문에 중간에 문제 또는 변경이 발생하더라도 메시지를 재처리할 수 있다.
        5. Consumer가 Broker에게 직접 메세지를 가져오기 때문에 자기 처리 능력 대비 최적의 성능을 낼 수 있다.
        

 * Apache Kafka의 수요가 발생한 이유
    1. 기존 데이터 시스템인 Apache Hadoop은 현대 상황에 대해 속도가 너무 느림
    2. 빅데이터의 도전과제인 '분석'을 수행하기 위한 실시간 데이터의 수집에 이용됨.
    3. 사물인터넷(IoT) 같은 서비스 작업부하에서의 사용 수요의 증가
    4. 경쟁상대인 Apache Spark는 실시간 처리가 가능하지만 최적화되어 있진 않음
    5. 새로운 시점으로 데이터 스트림을 사용할 수 있는 실시간 메시징 프레임워크 체계
 
 * Apache Kafka의 활용 사례    
     - 여러 기업들은 현대의 빅데이터 실시간 처리를 위해 데이터 처리 플랫폼의 구성요소로 Kafka를 채용하고 있음.
     
     1. Kakao RUBICS
        - 실시간 사용자 반응 분석을 통해 콘텐츠를 추천하는 Kakao의 추천 시스템
        - 사용자로부터의 피드백을 빠르고 안전하게 처리할 수 있는 시스템의 필요성에 따라 메세지 큐 시스템으로 Kafka를 선정
        
        <img src="https://github.com/KimJeongHyun/Creative_Engineering/blob/master/Tech_investigate_Resource/Kakao_RUBICS.png" width="60%">
        
        - Kafka를 통해 실시간 데이터를 처리하고 Spark Streaming으로 데이터 스트림을 처리, 이후 처리된 데이터를 Hive, Spark 를 이용해 데이터를 배치 처리하며 이를 결합해 최종 추천 서지스로 구현.
        - 99%의 데이터 요청을 3ms 이내에 처리함.
        - 99.998%의 가용성을 보이고 있으며 2015년 9월 이후로 '0'의 장애시간을 기록하고 있음.
  
    2. NetFlix Suro
        - 수집된 데이터의 성격을 파악해 알맞는 처리 시스템으로 분류해 처리함
        
        <img src="https://github.com/KimJeongHyun/Creative_Engineering/blob/master/Tech_investigate_Resource/NetFlix_Suro.jpg" width="60%">
        
        - 2013년 12월 10일 공개된 데이터 처리 플랫폼 오픈소스 'Suro'
        - Cluster로부터 데이터가 수집되면 Suro 플랫폼에서 배치 처리용 데이터, 실시간 처리용 데이터로 분류
        - 배치 처리용 데이터는 하둡 등의 시스템으로 분류되어 처리되며 실시간 처리용 데이터는 Kafka로 이동해 처리됨
    3. Ebay Pipeline, Uber Pipeline 등 여러 기업들의 데이터 처리 시스템에서 메시징 프레임워크로서 활약하고 있음
    
 * Apache Kafka의 의존성 및 연계시스템 도식
 
  <img src="https://github.com/KimJeongHyun/Creative_Engineering/blob/master/Tech_investigate_Resource/Kafka_Depends.jpeg" width="60%">
        
         
 * 결론
    - Apache Kafka는 실시간 메세징 프레임워크로서 현대 넘처나는 빅데이터와 끊임없이 생성되는 사용자 데이터에 대한 피드백을 처리하는 시스템으로 거의 독보적인 위치에 자리하고 있음.
    - 사용자의 기호에 따른 '추천' 시스템이 주목되고 있는 IT 업계에서 실시간 데이터를 활용하는 S/W에게 필수적인 역할을 할 것으로 기대됨.
    - 비단 단순히 사용자의 기호에 따른 아이템에 대한 추천 뿐만 아니라 사용자가 임의의 어떠한 패턴에 대해서 어떻게 행동했는가? 에 대한 정보 또한 처리하고 분석 알고리즘과 결합해 다양한 시나리오에 대한 데이터 처리가 예상됨.
    - Scale Out이 용이하고 오픈소스이기 때문에 서버의 확장 등 자금 부분에 대해 큰 기여를 할 것임.
    - 데이터 베이스 처리에 대해 Hadoop, Spark, Kafka 삼두마차의 형태로 분산된 지금, 실시간 데이터 처리에 대해서는 Kafka가 독보적.

---


[^1]: 서버의 가상화 기능을 사용해 접속된 서버의 대수를 늘려 처리 능력을 향상시키는 기법. 하나의 케이스 내에서 가상적으로 복수 서버를 구축해 Scale Out과 동등한 효과 제공이 가능하며 이것을 Scale Within 또는 Virtual Scale Out 등으로 부르기도 한다.

[^2]: 부하분산. 컴퓨터 네트워크 기술의 일종으로 중앙처리장치 혹은 저장장치 등의 컴퓨터 자원에 작업을 나누는 것으로 가용성, 응답시간을 최적화할 수 있는 기법

[^3]: 장애 허용 시스템, 또는 결함 감내 시스템. 시스템에서 결함 또는 고장이 발생해도 정상적 혹은 부분적으로 기능을 수행할 수 있는 시스템.

[^4]: Apache Zookeeper. 분산 코디네이터로 디렉토리 구조의 노드에 데이터를 저장할 수 있다. 노드별 특성, Watcher 기능 등을 사용하여 다양한 시나리오를 구성한다.

[^5]: Publisher. 데이터 단위를 전송하는 부분. 

[^6]: 데이터를 받아 분산처리하는 부분.

[^7]: Subscriber. 데이터 저장소 'Topic'에서 데이터를 가져가는 부분.

[^8]: Transaction Per Seconds. 초당 트랜잭션 처리의 수

---

- 조사에 사용된 웹페이지 링크 ↓    
  1. http://www.bloter.net/archives/173016
     - 넷플릭스, 데이터 처리 플랫폼 오픈소스로 공개. BLOATER, 이지영 기자. 2013.12.10
     
  2. https://medium.com/sunhyoups-story/zero-copy%EB%9E%80-e113d5df7191
     - Zero copy란? A Medium Corporation Member, "이선협". 2014.08.26
     
  3. http://epicdevs.com/17
     - [Apache Kafka] 1. 소개 및 아키텍처 정리. epicdevs. 2015.03.08
     
  4. https://www.pcworld.com/article/2999801/how-apache-kafka-is-greasing-the-wheels-for-big-data.html
     - How Apache Kafka is greasing the wheels for big data. IDG News Service, Katherine Noyes. 2015.10.30
     
  5. http://tech.kakao.com/2016/04/27/rubics/
     - 루빅스(RUBICS) - kakao의 실시간 추천 시스템. kakao Tech. sawyer.seo(RUBICS TF). 2016.04.27
     
  6. https://ko.wikipedia.org/wiki/%EC%95%84%ED%8C%8C%EC%B9%98_%EC%B9%B4%ED%94%84%EC%B9%B4
     - 아파치 카프카. Wikipedia. 2016.08.02 ~ 2018.10.21
  
  7. https://www.infoworld.com/article/3212204/big-data/all-your-streaming-data-are-belong-to-kafka.html
     - All your streaming data are belong to Kafka. InfoWorld, Matt Asay. 2017.07.31
     
  8. https://zzsza.github.io/data/2018/06/15/apache-kafka-intro/
     - Apache Kafka Intro. zzasza.github.io. 2018.06.15
     
  9. https://medium.com/zaneiru-tech-life-blog/apache-kafka-%EC%B9%B4%ED%94%84%EC%B9%B4-%EC%9D%98-%ED%8A%B9%EC%A7%95-%EB%B0%8F-%EB%AA%A8%EB%8D%B8-b3d3f7e6a4df
     - Apache Kafka의 특징 및 모델. A Medium Corporation Member, "Engineer" 2018.10.13
     
        
---
  
