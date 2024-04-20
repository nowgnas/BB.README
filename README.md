# BLOOMING BLOOMS

## 프로젝트 정보

### 팀원

| Position |  Nmae  |
| :------: | :----: |
| FrontEnd | 김정윤 |
| BackEnd  | 구지웅 |
| BackEnd  | 이상원 |
| BackEnd  | 이진우 |
| BackEnd  | 최창효 |

## 프로젝트 개요

## 사용 기술

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

## 프로젝트 아키텍처

![architecture](/images/architecture.png)

- EKS 환경에서 MSA 아키텍처 운영
- Cloud Front를 이용해 캐시 히트율 90% 달성
- 무중단 배포 스크립트 작성으로 서버 다운타임을 없애 지속적인 서비스 제공 가능
- Kubernetes Job을 사용해 안정적인 스케줄링

## 프로젝트 설명

![main](/images/main.png)

Blooming Blooms는 시장성 있는 화훼 산업을 타깃으로 화훼 쇼핑몰 및 픽업 시스템으로 정기구독, 기프트 카드 등 기존 화훼를 다루는 이커머스 시스템과는 차별화된 부가 기능들을 겸비한 개방적이고 유연한 컴포저블 커머스 시스템이다.

기존의 분산된 다양한 가게들의 꽃 상품들을 한곳에 모아볼 수 있으며, 꽃을 즐겨 사는 소비 행태에 발맞춰 매번 새로운 꽃들로 구성된 꽃 상품을 주기적으로 받아볼 수 있는 정기구독 서비스가 있다. '선물'이 주목적인 꽃의 특성을 고려하여 선물해 주는 사람의 마음을 담아 꽃과 함께 보낼 수 있는 기프트 카드 서비스에는 ChatGPT를 활용한 꽃말 기반으로 메시지 추천 기능이 있다.

일반 사용자들을 위한 쇼핑몰뿐만 아니라 꽃 가게 사장님들을 위한 가게 관리 및 관리자 기능들도 존재한다.

## 프로젝트 Repository

| Service              | Url                                                 |
| :------------------- | :-------------------------------------------------- |
| Api Gateway          | https://github.com/lotteon2/BB-APIGATEWAY-SERVICE   |
| Discovery Service    | https://github.com/lotteon2/BB-DISCOVERY-SERVICE    |
| Config Service       | https://github.com/lotteon2/BB-CONFIG-SERVICE       |
| Auth Service         | https://github.com/lotteon2/BB-AUTH-SERVICE         |
| Delivery Service     | https://github.com/lotteon2/BB-DELIVERY-SERVICE     |
| Giftcard Service     | https://github.com/lotteon2/BB-GIFTCARD-SERVICE     |
| Notification Service | https://github.com/lotteon2/BB-NOTIFICATION-SERVICE |
| Order Service        | https://github.com/lotteon2/BB-ORDER-SERVICE        |
| Order Query Service  | https://github.com/lotteon2/BB-ORDER-QUERY-SERVICE  |
| Payment Service      | https://github.com/lotteon2/BB-PAYMENT-SERVICE      |
| Product Service      | https://github.com/lotteon2/BB-PRODUCT-SERVICE      |
| Store Service        | https://github.com/lotteon2/BB-STORE-SERVICE        |
| Wishlist Service     | https://github.com/lotteon2/BB-WISHLIST-SERVICE     |
| Subscription Batch   | https://github.com/lotteon2/BB-SUBSCRIPTION-BATCH   |
| User Service         | https://github.com/lotteon2/BB-USER-SERVICE         |
| Maven Repository     | https://github.com/lotteon2/BB-COMMON-REPOSITORY    |
| FrontEnd             | https://github.com/lotteon2/BB-FRONTEND             |
| Infra                | https://github.com/lotteon2/BB-INFRA-CONTROL        |

## ERD

![erd](/images/erd.png)

## 프로젝트 문서

- [기능 명세서](https://shy-scribe-79f.notion.site/0acd63e526144ac3aeac0bea0413704a?pvs=4)
- [요구사항 명세서](https://shy-scribe-79f.notion.site/02d2867d3f5742a8939220afd152552a?pvs=4)
