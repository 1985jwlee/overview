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
    COIN["📊 Coin Data API<br/>직접 구현한 DI · 웹서버 · 데이터 파이프라인"]
    REACT["💻 React Experiments<br/>전체 시스템 흐름 이해"]

    IOT -->|프로덕션 레벨 설계 판단| MAIN
    SHADER -->|렌더링 최적화 이해| MAIN
    VAMPIRE -->|실시간 구조 체감| MAIN
    COIN -->|DI · 파이프라인 설계 구현력| MAIN
    REACT -->|클라이언트↔서버 흐름 이해| MAIN

    style MAIN fill:#2c3e50,color:#fff
    style IOT fill:#1a6b3c,color:#fff
```

|포트폴리오                       |링크                                                                           |역할                                      |
|----------------------------|-----------------------------------------------------------------------------|----------------------------------------|
|🌡️ **Production IoT Backend**|[production-iot-backend](https://github.com/1985jwlee/production-iot-backend)|실무 IoT 시스템 · 마이크로서비스 · 보안 설계            |
|🎨 Client Rendering          |[Shader Experiments](https://github.com/1985jwlee/portpolio_shader)          |GPU, 프레임 단위 사고 이해                       |
|🎮 Real-time Game            |[Vampire Survival](https://github.com/1985jwlee/portpolio_vampiresurvival)   |실시간 루프·상태 관리 경험                         |
|📊 **Coin Data API**         |[portpolio_coindataapi](https://github.com/1985jwlee/portpolio_coindataapi)  |DI 컨테이너 · 웹서버 프레임워크 직접 구현 · 외부 데이터 파이프라인|
|💻 Frontend Literacy         |[React Experiments](https://github.com/1985jwlee/portpolio_react)            |전체 시스템 흐름 이해                            |

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

### 📊 Coin Data API 상세

**외부 데이터 파이프라인** — C#으로 DI 컨테이너와 웹서버 프레임워크를 직접 구현

> 단순히 라이브러리를 “사용”하는 것을 넘어, 프레임워크가 **왜 그렇게 설계되었는지**를 직접 구현으로 증명한 프로젝트

```mermaid
graph TB
    subgraph External["외부 데이터 소스"]
        BINANCE[Binance WebSocket<br/>실시간 Kline 스트림]
        OTHER[기타 거래소 API]
    end

    subgraph Ingestion["수집 계층 (C# / .NET)"]
        SOCKET[BinanceSocketKlineManager<br/>WebSocket 연결 관리]
        IEXCHANGE[IExchangeKlineManager<br/>거래소 추상 인터페이스]
        SOCKET -->|구현| IEXCHANGE
    end

    subgraph Core["코어 인프라 (직접 구현)"]
        DI[DIContainer<br/>직접 구현한 DI 컨테이너]
        WEB[WebServerFramework<br/>직접 구현한 웹서버]
        RX[RxConcurrentDictionary<br/>Reactive 동시성 딕셔너리]
    end

    subgraph Processing["처리 계층"]
        DR[DataResource<br/>데이터 소스 추상화]
        IND[Indicators<br/>기술 지표 계산 엔진]
    end

    subgraph Output["서비스 제공"]
        API[REST API<br/>정규화된 데이터 제공]
    end

    BINANCE -->|WebSocket| SOCKET
    OTHER --> IEXCHANGE
    IEXCHANGE --> DR
    DI -->|의존성 주입| SOCKET
    DI -->|의존성 주입| DR
    DI -->|의존성 주입| IND
    DR --> RX
    RX --> IND
    IND --> API
    WEB --> API

    style DI fill:#8e44ad,color:#fff
    style WEB fill:#8e44ad,color:#fff
    style IEXCHANGE fill:#2980b9,color:#fff
```

**핵심 설계 판단:**

|직접 구현한 것                     |이유              |얻은 것                |
|-----------------------------|----------------|--------------------|
|DI 컨테이너                      |프레임워크 내부 동작 이해  |의존성 그래프 · 생명주기 완전 제어|
|웹서버 프레임워크                    |HTTP 파이프라인 원리 체득|미들웨어 · 라우팅 구조 깊은 이해 |
|`IExchangeKlineManager` 인터페이스|거래소 교체 가능성 전제   |데이터 소스 변경 시 서비스 무영향 |
|`RxConcurrentDictionary`     |동시성 + 반응형 데이터 필요|스레드 안전 + 변경 스트림 구독  |

**장애 격리 설계:**

```mermaid
flowchart LR
    A[Binance WebSocket 장애] -->|격리| B[DataResource 캐시 유지]
    B --> C[API 정상 제공 유지]
    D[거래소 스키마 변경] -->|흡수| E[IExchangeKlineManager 구현체만 수정]
    E --> F[내부 표준 API 계약 유지]

    style A fill:#e74c3c,color:#fff
    style D fill:#e74c3c,color:#fff
    style C fill:#27ae60,color:#fff
    style F fill:#27ae60,color:#fff
```

> Supporting 포트폴리오는 독립 결과물이면서, 메인 포트폴리오의 **설계 판단을 뒷받침하는 근거**

-----

### 🎨 Shader Experiments 상세

**GPU 프레임 예산 직접 측정 — 커스텀 라이팅 · Dissolve · 아웃라인 직접 구현**

> 단순히 셰이더를 사용한 것이 아니라, 렌더링 비용을 수치로 측정하고 최적화한 경험입니다.
> 이 과정에서 얻은 클라이언트 부하 이해가 메인 포트폴리오의 서버 설계 판단으로 이어졌습니다.

| 구현 내용 | 핵심 수치 / 결과 | 메인 포트폴리오로 이어진 인사이트 |
|----------|---------------|-------------------------------|
| CustomLight.hlsl 직접 구현 | Unity 기본 라이팅 우회 → 프레임 비용 측정 가능 | 클라이언트 렌더링 비용을 블랙박스가 아닌 수치로 이해 |
| GPU Instancing 도입 | Draw Call 100개 → 1~5개 | 서버 동기화 빈도 20fps 제한의 설계 근거 |
| LOD 3단계 구성 | 근거리 LOD 300 / 원거리 Unlit | 프레임 예산 = 고정 자원, 집중과 절감의 배분 |
| Dissolve 마스크 6종 조합 | 최대 24개 동시 적용 | 확장 시 기존 코드 수정 없는 조합 구조 |

-----

### 🎮 Vampire Survival 상세

**클라이언트 중심 설계의 한계 직접 체험 — Server-authoritative 설계 판단의 출발점**

> 이 프로젝트에서 잘 설계된 구조도 **멀티플레이어 확장 시도 순간** 근본적 한계를 드러냈습니다.  
> 이 경험이 메인 포트폴리오에서 "상태 권한은 서버에만 존재해야 한다"는 설계 판단의 직접적 근거가 되었습니다.

| Vampire Survival에서 체감한 문제 | 메인 포트폴리오의 해법 | 이어진 설계 판단 |
|-------------------------------|---------------------|--------------|
| 클라이언트 간 상태 불일치 — 어느 쪽이 진실인지 판정 불가 | 서버 단독 상태 관리 | 상태 권한은 서버에만 존재한다 |
| 클라이언트 메모리 조작으로 치트 방어 구조적 불가능 | Command Validation (서버 검증) | 클라이언트 입력은 신뢰하지 않는다 |
| 동기화 기준점 부재 — 확장할수록 불일치 누적 | Server-authoritative + 단일 GameLoop | 서버 상태가 유일한 진실(Single Source of Truth) |
| 멀티플레이어 확장 시 전체 구조 교체 필요 | Zone 기반 수평 확장 설계 | 확장을 전제로 초기 구조를 설계한다 |

-----

### 💻 React Experiments 상세

**메인 포트폴리오 Admin Dashboard의 선행 기술 검증 프로토타입**

> 서버에서 설계한 상태 관리·스냅샷·이벤트 개념을 "실제로 UI로 구현할 수 있는가"를 먼저 검증한 프로젝트입니다.  
> 메인 포트폴리오의 핵심 개념을 React + Zustand로 동작하는 형태로 옮겨 증명했습니다.
```mermaid
graph LR
    subgraph Server["Main Portfolio 서버 개념"]
        S1[Game Server State<br/>In-memory]
        S2[Redis Hot Snapshot]
        S3[MongoDB Cold Snapshot]
        S4[Event Sourcing<br/>단방향 흐름]
    end

    subgraph UI["React 포트폴리오 UI 구현"]
        U1[Zustand Global Store<br/>Single Source of Truth]
        U2[메모리 스냅샷<br/>이름 붙여 저장·전환]
        U3[JSON Export / Import<br/>파일 직렬화]
        U4[Action → Store → View<br/>단방향 상태 흐름]
    end

    S1 -->|UI 레벨로 축소 적용| U1
    S2 -->|동일 개념 구현| U2
    S3 -->|동일 개념 구현| U3
    S4 -->|동일 개념 구현| U4

    style S1 fill:#2c3e50,color:#fff
    style S2 fill:#c0392b,color:#fff
    style S3 fill:#27ae60,color:#fff
    style S4 fill:#8e44ad,color:#fff
    style U1 fill:#2980b9,color:#fff
    style U2 fill:#2980b9,color:#fff
    style U3 fill:#2980b9,color:#fff
    style U4 fill:#2980b9,color:#fff
```

| Main Portfolio 설계 | React Portfolio 검증 |
|--------------------|---------------------|
| Game Server State (In-memory) | Zustand Single Source of Truth |
| Redis Hot Snapshot | 메모리 스냅샷 저장·전환 |
| MongoDB Cold Snapshot | JSON Export / Import |
| Event Sourcing | Action → Store → View 단방향 흐름 |
| Admin Dashboard 설계 | Inspector / Editor / Preview 패턴 구현 |

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
    프레임워크 이해
      DI 컨테이너 직접 구현
      웹서버 파이프라인 구현
      Reactive 동시성 설계
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
