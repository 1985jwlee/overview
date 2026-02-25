# JW Lee | System-centered Engineer

> **“무엇을 만들었는가”보다 “어떤 판단으로 이 구조에 도달했는가”**

**Real-time · Event-driven · Server-authoritative Architecture**

-----

## 🏆 Executive Summary

|키워드               |설명                                          |
|------------------|--------------------------------------------|
|🎮 **Game Server** |Unity 클라이언트 ↔ C# Server-authoritative 실시간 판정|
|⚡ **Event-driven**|Kafka 기반 이벤트 스트림 & 비동기 파이프라인                |
|🌐 **Platform API**|bun.js / ElysiaJS 기반 플랫폼 서버                 |
|📐 **Architecture**|확장성·장애 포인트 식별 중심의 설계 판단                     |

-----

## 🧭 Engineering Journey

```mermaid
timeline
    title Career Perspective
    클라이언트 중심 개발 : Unity 게임 클라이언트
                        : 셰이더·렌더링 최적화
                        : 실시간 루프 구현
    한계 체감 & 전환 : 클라이언트 권한 구조의 한계 인식
                    : 서버 권한 구조 필요성 체감
                    : 이벤트 기반 설계 학습
    현재 & 목표 : Server-authoritative 아키텍처 설계
              : Kafka 이벤트 스트림 파이프라인
              : 설계 판단과 운영 가능성 증명
```

-----

## 🚩 Flagship Portfolio

**→ [portpolio_main](https://github.com/1985jwlee/portpolio_main)**

**Server-authoritative & Event-driven Game / Platform Architecture**

### System Architecture

```mermaid
graph TB
    subgraph Client["🎮 Client Layer"]
        U[Unity Client]
    end

    subgraph Realtime["⚡ Real-time Layer (C# Server)"]
        GS[Game Server<br/>Server-authoritative]
        RT[실시간 판정 엔진]
        GS --> RT
    end

    subgraph Platform["🌐 Platform Layer (bun.js / ElysiaJS)"]
        API[Platform API Server]
        AUTH[Auth / Session]
        API --> AUTH
    end

    subgraph EventStream["📨 Event Stream (Kafka)"]
        KP[Producer]
        KC[Consumer]
        KP --> KC
    end

    subgraph Storage["💾 Storage Layer"]
        REDIS[(Redis<br/>🔴 Hot Data)]
        MONGO[(MongoDB<br/>🟢 Cold Snapshot)]
    end

    U <-->|WebSocket / TCP| GS
    U <-->|HTTP REST| API
    RT -->|이벤트 발행| KP
    KC -->|비동기 기록| MONGO
    GS <-->|세션 / 상태| REDIS
    API <-->|조회| MONGO
```

### 핵심 설계 판단

```mermaid
flowchart LR
    A[클라이언트 요청] --> B{서버 권한 판정}
    B -->|실시간 응답| C[즉각 피드백]
    B -->|이벤트 발행| D[Kafka Stream]
    D --> E[비동기 기록]
    E --> F[(MongoDB Cold)]
    C --> G[(Redis Hot)]

    style B fill:#ff6b6b,color:#fff
    style D fill:#4ecdc4,color:#fff
    style G fill:#e74c3c,color:#fff
    style F fill:#27ae60,color:#fff
```

|설계 포인트                  |판단 근거                    |
|------------------------|-------------------------|
|Server-authoritative    |클라이언트 치트 방지, 일관된 게임 상태 보장|
|실시간 판정 ↔ 비동기 기록 분리      |판정 지연 최소화, 기록 부하 격리      |
|Redis Hot / MongoDB Cold|읽기 성능 vs 영속성 트레이드오프      |
|Zone 기반 수평 확장           |단일 서버 병목 제거, 점진적 확장 가능   |

-----

## 🧩 Supporting Portfolios

```mermaid
graph LR
    MAIN["🚩 Main Portfolio<br/>Server-authoritative<br/>Event-driven Platform"]

    IOT["🌡️ Production IoT Backend<br/>실무 IoT 아키텍처 · 보안 · 성능"]
    SHADER["🎨 Shader Experiments<br/>GPU · 프레임 단위 사고"]
    VAMPIRE["🎮 Vampire Survival<br/>실시간 루프 · 상태 관리"]
    COIN["📊 Coin Data API<br/>이벤트 기반 API · 운영"]
    REACT["💻 React Experiments<br/>전체 시스템 흐름 이해"]

    IOT -->|프로덕션 레벨 설계 판단| MAIN
    SHADER -->|렌더링 최적화 이해| MAIN
    VAMPIRE -->|실시간 구조 체감| MAIN
    COIN -->|이벤트 파이프라인 경험| MAIN
    REACT -->|클라이언트↔서버 흐름 이해| MAIN

    style MAIN fill:#2c3e50,color:#fff
    style IOT fill:#1a6b3c,color:#fff
```

|포트폴리오                       |링크                                                                           |역할                          |
|----------------------------|-----------------------------------------------------------------------------|----------------------------|
|🌡️ **Production IoT Backend**|[production-iot-backend](https://github.com/1985jwlee/production-iot-backend)|실무 IoT 시스템 · 마이크로서비스 · 보안 설계|
|🎨 Client Rendering          |[Shader Experiments](https://github.com/1985jwlee/portpolio_shader)          |GPU, 프레임 단위 사고 이해           |
|🎮 Real-time Game            |[Vampire Survival](https://github.com/1985jwlee/portpolio_vampiresurvival)   |실시간 루프·상태 관리 경험             |
|📊 Data Pipeline             |[Coin Data API](https://github.com/1985jwlee/portpolio_coindataapi)          |이벤트 기반 API & 운영 경험          |
|💻 Frontend Literacy         |[React Experiments](https://github.com/1985jwlee/portpolio_react)            |전체 시스템 흐름 이해                |

### 🌡️ Production IoT Backend 상세

**도로 살수 시스템**을 위한 프로덕션 레벨 IoT 백엔드 아키텍처

```mermaid
graph TB
    subgraph Client["Client Layer"]
        WEB[Web Dashboard]
        MOBILE[Mobile App]
    end

    subgraph Gateway["API Gateway (Nginx)"]
        LB[Load Balancing<br/>Rate Limiting · SSL]
    end

    subgraph App["App Layer (Bun.js / ElysiaJS)"]
        AUTH[Auth Service<br/>JWT + MFA]
        ROAD[Cooling Road<br/>Service]
        ADMIN[Admin Service]
        WS[WebSocket<br/>Manager]
    end

    subgraph MQ["Message Queue (Kafka)"]
        K1[device.control]
        K2[operation.events]
        K3[ai.decision]
    end

    subgraph Storage["Storage"]
        MYSQL[(MySQL<br/>트랜잭션 데이터)]
        MONGO[(MongoDB<br/>로그 · 이벤트)]
        REDIS[(Redis<br/>세션 · 캐시)]
    end

    subgraph IoT["IoT Layer"]
        ADAPTER[PLC Adapter<br/>Modbus TCP]
        PLC1[PLC Site A]
        PLC2[PLC Site B]
        PLCN[PLC Site N...]
    end

    WEB & MOBILE --> LB
    LB --> AUTH & ROAD & ADMIN & WS
    ROAD -->|이벤트 발행| K1 & K2
    K3 -->|AI 판단 구독| ROAD
    AUTH --> MYSQL & REDIS
    ROAD --> MYSQL & MONGO & REDIS
    K2 --> ADAPTER
    ADAPTER --> PLC1 & PLC2 & PLCN

    style ADAPTER fill:#e67e22,color:#fff
    style LB fill:#2980b9,color:#fff
```

**핵심 설계 패턴 요약:**

|패턴                  |적용                 |성과                        |
|--------------------|-------------------|--------------------------|
|Adapter Pattern     |PLC 통신 추상화         |환경 변수 하나로 Real/Fake PLC 전환|
|Repository Pattern  |DB 접근 계층 분리        |ORM 교체 시 레포지토리만 수정        |
|Dependency Injection|tsyringe 기반 DI     |Mock 주입으로 단위 테스트 가능       |
|Semaphore Pattern   |동시 이미지 캡처 제어       |CPU 사용률 70% → 30%         |
|Event-driven (Kafka)|서비스 간 비동기 통신       |장애 전파 차단, 비동기 처리          |
|Multi-level Cache   |Memory → Redis → DB|L1 캐시 히트 시 마이크로초 응답       |


> Supporting 포트폴리오는 독립 결과물이면서, 메인 포트폴리오의 **설계 판단을 뒷받침하는 근거**

-----

## 💡 Core Competencies

```mermaid
mindmap
  root((JW Lee))
    실시간 시스템
      Server-authoritative 구조
      WebSocket / TCP 통신
      실시간 판정 엔진
    이벤트 기반 설계
      Kafka 파이프라인
      비동기 처리 분리
      장애 포인트 식별
    풀스택 시야
      Unity 클라이언트
      C# 게임 서버
      bun.js / ElysiaJS API
    운영 가능성
      수평 확장 설계
      Redis Hot / Cold 전략
      기술 기준 문서화
```

-----

## 🔗 Tech Stack

**🎮 Game Client**  
![Unity](https://img.shields.io/badge/Unity-000000?style=flat-square&logo=unity&logoColor=white)
![C#](https://img.shields.io/badge/C%23-239120?style=flat-square&logo=csharp&logoColor=white)
![HLSL](https://img.shields.io/badge/HLSL%20Shader-5C2D91?style=flat-square&logo=windows&logoColor=white)

**⚙️ Game Server / Backend**  
![C#](https://img.shields.io/badge/C%23-239120?style=flat-square&logo=csharp&logoColor=white)
![.NET](https://img.shields.io/badge/.NET-512BD4?style=flat-square&logo=dotnet&logoColor=white)
![WebSocket](https://img.shields.io/badge/WebSocket-010101?style=flat-square&logo=socketdotio&logoColor=white)

**🌐 Platform API**  
![Bun](https://img.shields.io/badge/Bun-000000?style=flat-square&logo=bun&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)
![ElysiaJS](https://img.shields.io/badge/ElysiaJS-5A67D8?style=flat-square&logo=elysia&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=nodedotjs&logoColor=white)
![Nginx](https://img.shields.io/badge/Nginx-009639?style=flat-square&logo=nginx&logoColor=white)

**🌡️ IoT / Protocol**  
![Modbus](https://img.shields.io/badge/Modbus%20TCP-FF6600?style=flat-square&logo=probot&logoColor=white)
![RTSP](https://img.shields.io/badge/RTSP%20Stream-CC0000?style=flat-square&logo=camera&logoColor=white)
![FFmpeg](https://img.shields.io/badge/FFmpeg-007808?style=flat-square&logo=ffmpeg&logoColor=white)

**📨 Event Stream & Messaging**  
![Kafka](https://img.shields.io/badge/Apache%20Kafka-231F20?style=flat-square&logo=apachekafka&logoColor=white)

**💾 Database & Cache**  
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=flat-square&logo=mysql&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=flat-square&logo=mongodb&logoColor=white)

**💻 Frontend**  
![React](https://img.shields.io/badge/React-61DAFB?style=flat-square&logo=react&logoColor=black)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)

**🔐 Security**  
![JWT](https://img.shields.io/badge/JWT-000000?style=flat-square&logo=jsonwebtokens&logoColor=white)
![TOTP](https://img.shields.io/badge/TOTP%20MFA-FF4500?style=flat-square&logo=authy&logoColor=white)
![RBAC](https://img.shields.io/badge/RBAC-6A0DAD?style=flat-square&logo=shieldsdotio&logoColor=white)

**🛠️ Tools & Infra**  
![Git](https://img.shields.io/badge/Git-F05032?style=flat-square&logo=git&logoColor=white)
![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=github&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)

-----

## 📬 Contact

각 저장소는 독립적 결과물이면서 **하나의 설계 철학으로 연결**됩니다.  
단순 기술 나열이 아닌, **설계 판단의 축적**을 확인하고 싶다면 메인 포트폴리오를 먼저 보세요.

**→ [portpolio_main](https://github.com/1985jwlee/portpolio_main)**