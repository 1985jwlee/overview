# JW Lee | System-centered Engineer
**Real-time & Event-driven Architecture Specialist**

---
## 👤 커리어 타임라인

```mermaid
timeline
    title Career Timeline
    2014 : Unity 기반 게임 개발자 입문
    2020 : 이벤트 기반 시스템 설계
    2023 : 실시간 컨텐츠 개발
    2025 : Bun.js / ElysiaJS 기반 백엔드 경험
```
---

## 🎯 Portfolio Philosophy

> **"무엇을 만들었는가"보다 "어떤 판단으로 이 구조에 도달했는가"**

이 포트폴리오는 코드 작성 능력이 아닌 **시스템 설계 판단력**을 증명합니다.

---

## 🏆 Executive Summary

### 핵심 역량

```
✓ 실시간 시스템의 구조적 설계 능력
✓ Server-authoritative 구조에 대한 깊은 이해
✓ 이벤트 기반 아키텍처의 실무적 적용
✓ 장애 격리와 복구 전략 설계
✓ 설계 원칙의 도메인 간 일반화 능력
```

### Career Journey

```
초기 (클라이언트 중심)
    ↓
[ Unity 개발 경험 ]
    ↓ 실시간 시스템 한계 체감
    ↓
현재 (시스템 설계 중심)
    ↓
[ Server-authoritative ]
[ Event-driven Architecture ]
    ↓
목표 (설계 판단 증명)
    ↓
[ 운영 가능한 시스템 엔지니어 ]
```

---

## 🏗️ Portfolio Structure

```mermaid
graph TB
    subgraph "🏆 Flagship"
        MAIN[Event-driven Real-time Platform<br/>게임 도메인]
    end
    
    subgraph "🎯 Cross-Domain Proof"
        API[Coin Data API Platform<br/>금융/핀테크 도메인]
    end
    
    subgraph "🧩 Supporting"
        SHADER[Shader Experiments]
        GAME[Vampire Survival]
        REACT[React State Manager]
    end
    
    MAIN <-.->|동일 설계 원칙| API
    MAIN -.->|렌더링 이해| SHADER
    MAIN -.->|실시간 경험| GAME
    MAIN -.->|운영 도구| REACT
    
    style MAIN fill:#4A90E2,stroke:#2E5C8A,stroke-width:3px,color:#fff
    style API fill:#FFA07A,stroke:#FF4500,stroke-width:3px,color:#fff
```

-----

## 🚩 Flagship Portfolio

**Server-authoritative & Event-driven Game / Platform Architecture**  
👉 [portpolio_main](https://github.com/1985jwlee/portpolio_main)

핵심 포인트:

- 캐주얼 실시간 게임 기반 → MMO/플랫폼 확장 가능
- Server-authoritative 실시간 판정 / Kafka 이벤트 스트림
- 실시간 판정 ↔ 비동기 기록 분리
- Zone 기반 수평 확장, Redis Hot / MongoDB Cold Snapshot
- Unity 클라이언트 ↔ C# 서버 ↔ TypeScript 플랫폼 서버

> "무엇을 만들었는가"보다 "어떤 판단으로 이 구조에 도달했는가" 강조

```mermaid
flowchart TD
    subgraph Client
        Unity[Unity Client]:::client
    end

    subgraph Server
        GameServer[C# Game Server]:::server
        EventBus[Kafka Event Stream]:::server
        Platform[Bun.js / ElysiaJS]:::server
    end

    subgraph Database
        Redis[Redis Hot Snapshot]:::db
        Mongo[MongoDB Cold Snapshot]:::db
    end

    Unity --> GameServer
    GameServer --> EventBus
    EventBus --> Platform
    GameServer --> Redis
    GameServer --> Mongo

    classDef client fill:#4A90E2,stroke:#fff,color:#fff;
    classDef server fill:#FFA07A,stroke:#fff,color:#fff;
    classDef db fill:#7FFFD4,stroke:#fff,color:#000;
```
-----

## 🎯 Cross-Domain Application

### 📊 Coin Data API Platform

👉 [portpolio_coindataapi](https://github.com/1985jwlee/portpolio_coindataapi)

**동일한 설계 원칙의 금융/핀테크 도메인 적용 사례**

**핵심 구현**:
- Binance WebSocket → REST API 실시간 데이터 플랫폼
- 24개 암호화폐 선물 시장 데이터 수집 및 정규화
- 26개 기술 지표 엔진 (RSI, MACD, Stochastic, Pivot 등)
- 외부 API 스키마 변경으로부터 클라이언트 보호
- 거래소 API 장애 시 캐시 기반 서비스 연속성 보장

```mermaid
graph TB
    subgraph "External Sources"
        WS[Binance WebSocket<br/>실시간 시세]
    end
    
    subgraph "Ingestion Layer"
        Mgr[BinanceSocketKlineManager<br/>데이터 수집 및 Queue 관리]
    end
    
    subgraph "Processing Layer"
        Norm[Schema Normalizer<br/>IBinanceKline 표준화]
        Calc[Technical Indicator Engine<br/>26개 지표 계산]
    end
    
    subgraph "Cache Layer"
        Cache[(RxConcurrentDictionary<br/>In-Memory Cache)]
    end
    
    subgraph "API Layer"
        API[REST API Server<br/>WatsonWebserver]
    end
    
    WS -->|Raw Data| Mgr
    Mgr -->|Queue| Norm
    Norm --> Calc
    Calc --> Cache
    Cache --> API
    API -->|JSON| Client[Trading Clients]
    
    style Norm fill:#4A90E2,color:#fff
    style Calc fill:#FFA07A,color:#fff
    style Cache fill:#2ECC71,color:#fff
```

#### 원칙 적용 비교

|원칙        |게임 서버 (Main)      |Coin API Platform             |
|----------|------------------|------------------------------|
|**외부 격리** |DB 장애 시 게임 진행     |거래소 API 장애 시 캐시 제공            |
|**정규화 계층**|Event → DB Schema |External API → Internal Schema|
|**계약 안정성**|운영 API 불변         |클라이언트 API 불변                  |
|**비동기 처리**|Kafka Event Stream|WebSocket → Queue → Cache              |
|**실시간 처리**|GameLoop Tick (50ms)|1분 주기 지표 갱신 (지연 허용)|
|**장애 복구**|Hot/Cold Snapshot|In-Memory Cache + 자동 재연결|

#### API 엔드포인트

```bash
# 종합 지표 조회
GET /api/v1/summary?symbol=BTCUSDT&interval=1m

# 오실레이터 지표
GET /api/v1/oscillators?symbol=ETHUSDT&interval=5m

# 이동평균 지표
GET /api/v1/moving_averages?symbol=ADAUSDT&interval=15m

# 피봇 포인트
GET /api/v1/pivots?symbol=SOLUSDT&interval=1h&period=14
```

#### 금융/트레이딩 도메인 확장성

이 프로젝트는 다음 금융 서비스로 확장 가능합니다:

**트레이딩 플랫폼**:
- 자동 매매 시스템의 지표 데이터 소스
- 백테스팅 엔진의 시장 데이터 제공
- 실시간 시그널 생성 서비스

**리스크 관리**:
- 포트폴리오 리밸런싱 지표
- 변동성 모니터링 시스템
- 시장 트렌드 분석 대시보드

**데이터 분석**:
- 기술 지표 상관관계 분석
- 시장 패턴 인식 ML 모델 훈련 데이터
- 실시간 시장 센티멘트 분석

> **핵심 메시지**: "설계 원칙은 도메인을 넘어 일반화 가능합니다"

-----

## 🧩 Supporting Portfolios

### 🎨 Client Rendering

**[Shader Experiments](https://github.com/1985jwlee/portpolio_shader)** – GPU, 프레임 단위 사고 이해

### 🎮 Real-time Game

**[Vampire Survival](https://github.com/1985jwlee/portpolio_vampiresurvival)** – 실시간 루프·상태 관리 경험

### 💻 Frontend Literacy

**[React State Manager](https://github.com/1985jwlee/portpolio_react)** – Admin Dashboard 프로토타입, 전체 시스템 흐름 이해

> Supporting 포트폴리오는 메인 포트폴리오의 설계 판단을 뒷받침

-----

## 💡 What I Do Well

- ✅ 실시간 시스템 아키텍처 설계
- ✅ Server-authoritative 구조 설계
- ✅ 이벤트 기반 비동기 파이프라인 설계
- ✅ 확장 시 병목·장애 포인트 식별
- ✅ **도메인 독립적 설계 원칙 수립**
- ✅ 외부 의존성 격리 전략
- ✅ 기술 기준 정립 및 문서화
- ✅ 복잡한 구조를 설명 가능하게 정리

-----

## 📧 Contact

**GitHub**: [@1985jwlee](https://github.com/1985jwlee)  
**Email**: leejae.w.jl@icloud.com

> 💡 포트폴리오에 대한 질문이나 피드백은 각 저장소의 Issues를 활용해주세요.

-----

## 🔗 Closing

- 단순 기술 나열이 아닌 설계 판단의 축적 강조
- 각 저장소는 독립적 결과물이면서 하나의 설계 철학으로 연결
- **게임, 금융, 데이터 플랫폼 도메인에 동일한 원칙 적용 가능**
- 실무 적용 가능한 아키텍처 패턴과 트레이드오프 이해
