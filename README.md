# Smart-Settlement System
대용량 트랜잭션 기반 비동기 정산 및 통계 플랫폼 본 프로젝트는 
매일 발생하는 수백만 건의 주문 데이터를 분석하여 판매자별 정산금을 산출하고, 대시보드용 통계 데이터를 생성하는 엔터프라이즈급 백엔드 시스템입니다.

# 핵심 설계 목표 (Core Design Goals)
・데이터 정합성 보장: 부동 소수점 오차 방지를 위해 BigInt 및 Numeric 타입을 활용한 금융권 수준의 정밀한 정산 로직 설계 
・동시성 제어: Redis(Redisson) 기반의 분산 락을 적용하여 분산 서버 환경에서의 중복 정산 이슈를 원천 차단 
・대용량 최적화: 일일 100만 건 이상의 데이터를 30분 이내에 처리하기 위한 Spring Batch Chunk 지향 아키텍처 및 페이징 조회 전략 수립

# Tech Stack
・Language & Framework: Java 17, Spring Boot 3.3, Spring Batch 5.x 
・Database: PostgreSQL 15, Redis (Redisson) 
・Data Access: QueryDSL, Spring Data JPA 
・Infra: Docker, GitHub Actions

# System Architecture
・API/Batch Separation: 관리자 대시보드 조회를 위한 API 서버와 대량 처리를 담당하는 Batch 서버를 분리하여 상호 간 성능 간섭 최소화 
・Locking Mechanism: Redisson의 Pub/Sub 기반 락 획득 방식을 사용하여 네트워크 자원 절약 및 응답성 확보

# Documentation (Design Documents)
상세한 설계 과정은 다음 문서를 통해 확인하실 수 있습니다.
https://github.com/SUJINCHO/Smart-Settlement/tree/aa53b4cd8fcde9df22d73d5e5e34746d325c968f/docs
ㄴSmart-Settlement_설계서_최종본.pdf
・요구사항 정의: 비즈니스 및 기술적 요구사항 도출 
・기술 의사결정서: 핵심 기술 스택 선정 근거 및 트레이드오프 분석 
・데이터 모델링: ERD 및 인덱스 전략을 포함한 테이블 상세 설계 
・배치 프로세스: Step-by-Step 흐름도 및 장애 복구(Restartability) 전략
