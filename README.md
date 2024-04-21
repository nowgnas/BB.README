# BLOOMING BLOOMS

## 프로젝트 정보

### 팀원

| Position          |  Nmae  |
| :---------------- | :----: |
| FrontEnd, BackEnd | 김정윤 |
| BackEnd           | 구지웅 |
| BackEnd, Infra    | 이상원 |
| BackEnd           | 이진우 |
| BackEnd           | 최창효 |

## 프로젝트 개요

### 사용 기술

![tech map](/images/techmap.png)

| Position | Stack            |
| :------: | :--------------- |
| FrontEnd | React            |
|          | Typescript       |
|          | Tailwind         |
|          | Recoil           |
|          | React Query      |
|          | Styled Component |
| BackEnd  | Spring Boot      |
|          | Spring Cloud     |
|          | Spring Batch     |
| Database | Mysql            |
|          | MongoDB          |
|          | DynamoDB         |
|          | Redis            |
|  Infra   | EKS              |
|          | SQS              |
|          | SNS              |
|          | Event Bridge     |
|          | Cloud Front      |
|          | S3               |
|          | Route53          |
|          | Terraform        |
|          | Kuberbetes       |
|          | Kafka            |

### 프로젝트 아키텍처

![architecture](/images/architecture.png)

- EKS 환경에서 MSA 아키텍처 운영
- Cloud Front를 이용해 캐시 히트율 90% 달성
- 무중단 배포 스크립트 작성으로 서버 다운타임을 없애 지속적인 서비스 제공 가능
- Kubernetes Job을 사용해 안정적인 스케줄링

### 프로젝트 설명

![main](/images/main.png)

Blooming Blooms는 시장성 있는 화훼 산업을 타깃으로 화훼 쇼핑몰 및 픽업 시스템으로 정기구독, 기프트 카드 등 기존 화훼를 다루는 이커머스 시스템과는 차별화된 부가 기능들을 겸비한 개방적이고 유연한 컴포저블 커머스 시스템이다.

기존의 분산된 다양한 가게들의 꽃 상품들을 한곳에 모아볼 수 있으며, 꽃을 즐겨 사는 소비 행태에 발맞춰 매번 새로운 꽃들로 구성된 꽃 상품을 주기적으로 받아볼 수 있는 정기구독 서비스가 있다. '선물'이 주목적인 꽃의 특성을 고려하여 선물해 주는 사람의 마음을 담아 꽃과 함께 보낼 수 있는 기프트 카드 서비스에는 ChatGPT를 활용한 꽃말 기반으로 메시지 추천 기능이 있다.

일반 사용자들을 위한 쇼핑몰뿐만 아니라 꽃 가게 사장님들을 위한 가게 관리 및 관리자 기능들도 존재한다.

### ⚙️ 프로젝트 주요기능 소개

- Chat GPT를 이용한 편지 메세지 추천
  - 상품에 대표꽃의 꽃말과 어떤 사람에게 보낼지 선택하면 편지 내용 생성
- Chat GPT를 이용한 상품 검색
  - "친구 생일에 선물하기 좋은 50000원 이하 꽃다발 추천해줘"로 검색하면 서비스 내에 50000원 이하의 "친구" 태그를 가지고 있는 꽃다발 상품이 검색됨
- 사용자는 상품을 픽업, 배송, 정기 구독 가능
- 상품 판매 상태가 일시 품절인 경우 재입고 알림을 신청해 상품 재입고 시 SSE와 SMS 알림 수신 가능
- 셀러는 셀러 페이지에서 가게 정보, 상품을 관리 가능
- 시스템 관리자는 관리자 페이지에서 서비스에 입점되어 있는 가게 관리, 일반회원, 셀러 관리 가능

### 🛠️ 서비스에 적용된 기술

- Spring Cloud 기반의 MSA 아키텍처
- SAGA Coreography 패턴을 이용한 분산 트랜잭션 처리
  - 1:1 kafka pub/sub 방식으로 결과적 데이터 정합성을 보장
- msa 아키텍처에서 효율적인 알림 전달을 위해 aws의 sns, sqs, lambda를 사용해 알림을 처리
  - 부득이한 상황에 의해 sse와 문자 알림이 전송된 후 데이터베이스 저장에 실패하게 되어 큐에서 데이터를 다시 폴링 하는 경우 sse와 문자 알림의 중복 전송을 방지하기 위해 AOP를 사용해 방지
- MongoDB를 사용한 상품 데이터 관리
  - 비정형 데이터 구조를 가진 셀러가 등록하는 상품은 최대 7의 태그와 22개의 꽃 종류에서 원하는 꽃을 골라 상품을 구성
  - schemaless 한 mongodb 의 특징으로 일반 상품과 카테고리와 태그가 없는 구독 상품을 동일한 collection에서 관리
- 확장성을 고려한 CQRS 패턴 설계
  - CQRS의 효율적인 Scale Out을 위해 DynamoDB 사용

### 프로젝트에서 본인의 역할

#### Backend

- **비정형 상품 데이터 관리를 위한 MongoDB 적용**
  - 속성이 각각 다른 상품 데이터를 유연하게 관리하기 위해 상품 데이터베이스로 mongoDB를 사용
  - 일반 배송 상품과 정기 구독 상품을 하나의 컬렉션에서 관리
- **product 마이크로 서비스를 유연하고 확장성을 가진 헥사고날 구조 설계**
  - 상품 모듈에 의존성을 가지고 있는 재입고 알림을 분리
  - SQS를 이용해 모듈 간 낮은 결합도로 구성
  - 재입고 알림은 매일 Event Bridge로 일정 시간에 체크하도록 설정 되어 있기 때문에 중복 전송을 방지하기 위해 redis cache 사용
- **각 모듈에서 알림 이벤트 발생 시 코드 재사용을 위한 노력**
  - SSE와 SMS 알림 템플릿 작성
  - 이벤트별 SQS 큐를 생성하여 일시적으로 서버에 장애가 발생해도 알림은 보장되도록 구성
  - 각 모듈에서 SQS로 publish하는 메서드와 listen 하는 부분을 maven repository로 관리하여 유지보수에 용이하게 구성
  - 알림 받을 사람 정보의 타입을 제네릭으로 설정하여 1명 혹은 여러 명의 고객에게 알림을 보낼 수 있도록 구성
- **Chat GPT를 이용한 상품 검색**
  - 서비스의 상품을 모두 학습시키지 못하기 때문에 사용자의 입력에서 카테고리, 가격, 태그에 대한 정보를 추출하여 데이터베이스 조회 조건으로 사용

#### Infra

- **EKS를 이용한 MSA 아키텍처 관리**
  - EKS 환경에서 POD을 모니터링할 수 있는 환경 구성 (Grafana, kube-ops-view)
  - kubernetes node selector를 사용해 원하는 worker node에 POD을 할당해서 관리
  - Blue Green 무중단 배포 스크립트로 사용자에게 지속적인 서비스 제공
- **Terraform을 이용한 AWS 자원 관리**
  - SQS, SNS, EKS, S3, Cloud Front를 terraform으로 관리하여 AWS 자원 관리 시간 단축
- **Cloud Front를 이용한 빠른 컨텐츠 제공**
  - Cloud Front 캐시 히트율 90% 이상으로 해상도가 높은 이미지를 빠르게 제공
- SQS, SNS를 이용해 적은 비용으로 메세지 큐 관리
  - SNS와 SQS, Lambda 함수를 이용해 적은 비용으로 메세지 큐 관리

#### Retrospect

**KEEP (지속할 것)**

- **Jira를 이용한 업무 관리**
  - Jira 티켓으로 팀의 업무 진행 상황을 파악하고 주어진 기간 내에 해야할 업무량을 파악할 수 있는 점
- **팀원들과 매주 금요일 기술 공유**
  - 금요일 오전 스크럼을 마친 후 한 주 동안 해결했던 이슈나 새로 도입한 기술을 공유하는 시간을 가지며 개선점에 대해서도 얘기할 수 있었던 점
- **PROBLEM (문제가 된 것)**
  - 패키지 컨벤션과 코드 컨벤션을 정하지 않아 기술적 문제가 발생했지만 코드와 구조에 대한 이해가 어려워 이슈 해결에 시간이 소요된 점
- **TRY (다음에 시도할 것)**
  - **각 모듈의 프로젝트 구조 설계 근거가 팀원들에게 설득력이 있도록 협의된 구조를 사용**
  - **기획 단계에서 세부적인 정책을 고민할 것**
  - **CQRS 개념을 가지고 설계할 것**
    - 조회와 데이터 조작 테이블을 분리하여 데이터베이스 부하 분산

### 프로젝트 Repository

| Service              | Url                                                 | In charge of Project |
| :------------------- | :-------------------------------------------------- | :------------------: |
| Api Gateway          | https://github.com/lotteon2/BB-APIGATEWAY-SERVICE   |                      |
| Discovery Service    | https://github.com/lotteon2/BB-DISCOVERY-SERVICE    |                      |
| Config Service       | https://github.com/lotteon2/BB-CONFIG-SERVICE       |                      |
| Auth Service         | https://github.com/lotteon2/BB-AUTH-SERVICE         |                      |
| Delivery Service     | https://github.com/lotteon2/BB-DELIVERY-SERVICE     |                      |
| Giftcard Service     | https://github.com/lotteon2/BB-GIFTCARD-SERVICE     |                      |
| Notification Service | https://github.com/lotteon2/BB-NOTIFICATION-SERVICE |          ✅          |
| Order Service        | https://github.com/lotteon2/BB-ORDER-SERVICE        |                      |
| Order Query Service  | https://github.com/lotteon2/BB-ORDER-QUERY-SERVICE  |                      |
| Payment Service      | https://github.com/lotteon2/BB-PAYMENT-SERVICE      |                      |
| Product Service      | https://github.com/lotteon2/BB-PRODUCT-SERVICE      |          ✅          |
| Store Service        | https://github.com/lotteon2/BB-STORE-SERVICE        |                      |
| Wishlist Service     | https://github.com/lotteon2/BB-WISHLIST-SERVICE     |                      |
| Subscription Batch   | https://github.com/lotteon2/BB-SUBSCRIPTION-BATCH   |                      |
| User Service         | https://github.com/lotteon2/BB-USER-SERVICE         |                      |
| Maven Repository     | https://github.com/lotteon2/BB-COMMON-REPOSITORY    |          ✅          |
| FrontEnd             | https://github.com/lotteon2/BB-FRONTEND             |                      |
| Infra                | https://github.com/lotteon2/BB-INFRA-CONTROL        |          ✅          |

### ERD

![erd](/images/erd.png)

### 프로젝트 문서

- [기능 명세서](https://shy-scribe-79f.notion.site/0acd63e526144ac3aeac0bea0413704a?pvs=4)
- [요구사항 명세서](https://shy-scribe-79f.notion.site/02d2867d3f5742a8939220afd152552a?pvs=4)
