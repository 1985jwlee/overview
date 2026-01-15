# JW Lee | System-centered Engineer
**Real-time & Event-driven Architecture Specialist**

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

## 📊 Portfolio Structure

### 설계 철학의 계층적 증명

```
┌─────────────────────────────────────┐
│   Overview (본 문서)                 │
│   "어떤 엔지니어인가"                 │
└──────────────┬──────────────────────┘
               │
               ↓
┌─────────────────────────────────────┐
│   Main Portfolio                     │
│   실시간 게임 플랫폼 아키텍처          │
│   "핵심 설계 원칙 제시"               │
└──────────────┬──────────────────────┘
               │
               ├─────────────────────────────┐
               │                             │
               ↓                             ↓
┌──────────────────────┐    ┌──────────────────────┐
│ Supporting Portfolio │    │ Implementation Demo  │
│ Coin Data API        │    │ React Dashboard      │
│ "비게임 도메인 적용" │    │ "운영 도구 구현"     │
└──────────────────────┘    └──────────────────────┘
               │                             │
               ↓                             ↓
┌─────────────────────────────────────┐
│   Additional Portfolios              │
│   Shader / Vampire Survival          │
│   "기술 스택 다양성"                  │
└─────────────────────────────────────┘
```

---

## 🚩 Flagship Portfolio

### [Event-driven Real-time Game Platform](https://github.com/1985jwlee/portpolio_main)

**핵심 질문에 대한 답**:
- 실시간 판정과 기록을 어떻게 분리하는가?
- 외부 시스템 장애가 게임플레이에 영향을 주지 않으려면?
- 확장 가능한 구조란 무엇인가?

#### 시스템 개요

```
[ Unity Client ]
    ↓ TCP Command
[ C# Game Server ]
    ↓ Fire-and-Forget Event
[ Kafka Stream ]
    ↓ Async Processing
[ TypeScript Platform ]
    ↓ Persistence
[ Redis / MongoDB / MySQL ]
```

#### 핵심 설계 결정

**1. 실시간과 비동기의 완전한 분리**

```csharp
// 게임 서버: 메모리에서 즉시 판정
public void ProcessMove(MoveCommand cmd)
{
    // 1. 검증 & 상태 변경 (메모리)
    player.Position = cmd.NewPosition;
    
    // 2. Domain Event 발행 (Fire-and-Forget)
    PublishEvent(new PlayerMovedEvent { ... });
    
    // 3. 즉시 응답 (Kafka 응답 기다리지 않음)
    SendResponse(player.Position);
}
```

**판단 근거**:
- ✅ 게임플레이는 DB/Kafka 지연의 영향 없음
- ✅ 장애 격리: 백엔드 다운 시에도 게임 진행
- ✅ 확장성: 이벤트 스트림으로 신규 서비스 추가

**2. Server-authoritative 구조**

```
클라이언트: "W키 눌렀어요" (의도만 전달)
서버: 검증 → 승인 → 상태 변경
클라이언트: 서버 승인 후에만 화면 갱신
```

**판단 근거**:
- ✅ 치트 방지는 구조로 해결
- ✅ 상태 일관성 보장
- ✅ 복잡하지만 안정성을 위해 선택

**3. 의도적으로 선택하지 않은 것**

```
❌ 게임 서버 직접 DB 접근
❌ 초기부터 마이크로서비스
❌ 모든 처리를 동기로
❌ UDP 프로토콜
```

**핵심 원칙**: "지금 필요하지 않으면, 지금 만들지 않는다"

#### 장애 대응 설계

**장애 영향도 매트릭스**

| 장애 | 게임플레이 | 기록 | 복구 시간 |
|------|-----------|------|----------|
| 게임 서버 | 🔴 중단 | 🟡 일시 중단 | 10초 (Redis) |
| Kafka | 🟢 정상 | 🟡 일시 중단 | 즉시 (버퍼) |
| MySQL | 🟢 정상 | 🟡 일시 중단 | 즉시 |

**설계 철학**: "게임플레이는 어떤 백엔드 장애에도 멈추지 않는다"

#### 기술 스택

```
Game Server: C#, TCP/IP, MessagePack, Redis, Kafka
Platform Server: TypeScript (bun.js), ElysiaJS, Drizzle ORM
Client: Unity 2022.3 LTS
Storage: Redis (Hot), MongoDB (Cold), MySQL (OLTP)
```

#### 상세 문서

- 📖 [설계 결정 과정](https://github.com/1985jwlee/portpolio_main/blob/main/docs/design-decisions.md): 왜 이렇게 설계했는가
- 🔧 [운영 가이드](https://github.com/1985jwlee/portpolio_main/blob/main/docs/operational-guide.md): 장애 시나리오별 대응
- 🚀 [구현 로드맵](https://github.com/1985jwlee/portpolio_main/blob/main/docs/implementation-roadmap.md): 단계별 구현 계획

---

## 🔗 Supporting Portfolio

### [Coin Data API — Platform Server in Practice](https://github.com/1985jwlee/portpolio_coindataapi)

**목적**: 메인 포트폴리오의 "플랫폼 서버" 설계 원칙을 비게임 도메인에서 검증

#### 핵심 질문

- 동일한 설계 원칙이 다른 도메인에도 적용 가능한가?
- 외부 API 장애 시 서비스를 어떻게 유지하는가?
- 외부 스키마 변경이 내부 시스템에 영향을 주지 않으려면?

#### 시스템 개요

```
[ Binance WebSocket API ]
    ↓ Real-time Stream
[ Ingestion Service ]
    ↓ Normalization
[ Internal Schema ]
    ↓ REST API
[ Clients (Trading Bots, Dashboard) ]
```

#### 핵심 설계: 정규화 계층

```csharp
// 외부 API → 내부 표준 변환
public class DataNormalizationService
{
    public InternalIndicatorData Normalize(
        IBinanceKline candle, 
        KlineInterval interval)
    {
        // 1. 외부 포맷 → 내부 표준
        var normalized = new InternalIndicatorData
        {
            Timestamp = candle.OpenTime,
            Interval = MapInterval(interval),
            OHLC = new OHLC { ... }
        };

        // 2. 지표 계산 (내부 표준)
        normalized.Indicators = CalculateIndicators(candle);

        return normalized;
    }

    // 외부 변경이 이 계층에서 흡수됨
    private string MapInterval(KlineInterval external)
    {
        return external switch
        {
            KlineInterval.OneMinute => "1m",
            KlineInterval.FiveMinutes => "5m",
            _ => "unknown"
        };
    }
}
```

#### 메인 포트폴리오와의 대응

| 원칙 | 게임 서버 (Main) | Coin API (Supporting) |
|------|-----------------|----------------------|
| **외부 격리** | DB 장애 시 게임 진행 | 거래소 API 장애 시 제한 제공 |
| **정규화 계층** | Event → DB Schema | External → Internal Schema |
| **계약 안정성** | 운영 API 불변 | 클라이언트 API 불변 |
| **비동기 처리** | Kafka Event Stream | WebSocket Stream |

#### 핵심 메시지

> **"설계 원칙은 도메인을 넘어 일반화 가능합니다"**

---

## 🎨 Implementation Demo

### [React Object State Manager — Admin Dashboard Prototype](https://github.com/1985jwlee/portpolio_react)

**목적**: 메인 포트폴리오의 Admin Dashboard 기술 검증

> **이 프로젝트는 [Event-driven Real-time Game Platform](https://github.com/1985jwlee/portpolio_main)의 Admin Dashboard 프로토타입입니다.**

#### 메인 포트폴리오와의 관계

```
[ Main: 게임 서버 설계 ]
    ↓
    실시간 오브젝트 상태 관리
    Event-driven Architecture
    Server-authoritative 구조
    ↓
[ React: Admin Dashboard 구현 ]
    ↓
    UI 기반 오브젝트 관리
    상태 저장/복원 메커니즘
    운영 도구 프로토타입
```

#### 검증하는 능력

| Main Portfolio | React Portfolio |
|----------------|-----------------|
| 서버 오브젝트 상태 관리 | UI 오브젝트 상태 관리 |
| Event Sourcing | State Management (Zustand) |
| Snapshot 복구 (서버) | 저장/불러오기 (클라이언트) |
| 운영 대시보드 **설계** | 운영 도구 **구현** |

#### 핵심 학습

```
"운영 도구는 백엔드 엔지니어도 만들 수 있어야 한다
 시스템의 가시성이 운영 가능성을 결정한다"
```

#### 실제 적용 예정

- 메인 포트폴리오의 Admin Dashboard 완성
- 실시간 모니터링 UI
- 장애 대응 인터페이스

#### 기술 스택

```
Frontend: React 19, TypeScript
State: Zustand (전역 상태 관리)
Styling: Tailwind CSS
Build: Vite
```

---

## 🧩 Additional Portfolios

설계 판단력의 다양한 측면을 증명하는 보조 프로젝트들:

### 🎨 Client Rendering
**[Shader Experiments](https://github.com/1985jwlee/portpolio_shader)**

**증명하는 것**:
- GPU 프로그래밍 이해
- 프레임 단위 성능 최적화 사고
- 실시간 렌더링 파이프라인 이해

**핵심 학습**:
```
"클라이언트 성능 병목을 이해해야
 서버 설계에서 무엇을 최적화할지 판단할 수 있다"
```

---

### 🎮 Real-time Game Logic
**[Vampire Survival Clone](https://github.com/1985jwlee/portpolio_vampiresurvival)**

**증명하는 것**:
- 실시간 게임 루프 설계
- 상태 관리 패턴
- 클라이언트 관점의 실시간 시스템 이해

**핵심 학습**:
```
"클라이언트 중심 개발의 한계를 체감하고
 Server-authoritative 구조의 필요성을 이해하게 된 계기"
```

---

## 💡 설계 철학 & 원칙

### 핵심 가치

#### 1. 복잡도는 비용이다

```
"할 수 있다" ≠ "해야 한다"

복잡한 구조는 반드시 그만한 가치를 제공해야 함
초기 복잡도를 최소화하되, 확장 가능하게
```

#### 2. 장애는 언제나 발생한다

```
장애를 막는 것 (불가능)
    ↓
장애를 격리하는 것 (현실적)
    ↓
장애 시 예측 가능하게 동작하는 것 (목표)
```

#### 3. 확장은 선형적이어야 한다

```
사용자 2배 → 비용 2배 (이상적)
사용자 2배 → 비용 10배 (지속 불가능)

비선형 확장은 구조적 문제
```

#### 4. 문서화는 필수다

```
개인의 지식 → 조직의 자산
구조를 설명할 수 없으면 좋은 구조가 아님
시스템 자체가 설명할 수 있어야 함
```

#### 5. 운영 가능성이 구현보다 중요하다

```
만들 수 있어도 운영할 수 없으면 의미 없음
특정 개발자에게 의존하는 구조는 위험
인수인계 가능한 시스템을 설계
```

---

## 🎓 What I Do Well

### 기술적 역량

✅ **실시간 시스템 아키텍처 설계**
- Command vs Event 분리
- 동기 vs 비동기 처리 판단
- 장애 격리 전략

✅ **Server-authoritative 구조 설계**
- 클라이언트 신뢰 최소화
- 상태 일관성 보장
- 치트 방지 구조화

✅ **이벤트 기반 비동기 파이프라인**
- Kafka 기반 Event Stream
- Idempotency 처리
- DLQ 전략

✅ **확장 시 병목 포인트 식별**
- 성능 측정 지점 선정
- 캐싱 전략 수립
- 샤딩 / 파티셔닝 설계

### 조직적 역량

✅ **기술 기준 정립**
- 설계 원칙 명문화
- 의사결정 프레임워크 수립
- 트레이드오프 문서화

✅ **복잡한 구조의 설명 가능한 정리**
- 계층적 문서 구조
- 다이어그램 기반 커뮤니케이션
- 핵심 메시지 전달

✅ **운영 관점의 시스템 설계**
- 장애 시나리오별 대응 방안
- 모니터링 전략
- 인수인계 가능한 구조

---

## 📈 Career Perspective

### 현재까지의 여정

```
2019-2021: Unity 클라이언트 개발
- 실시간 게임 로직 구현
- 클라이언트 중심 설계의 한계 체감

2021-2023: 서버 전환기
- Server-authoritative 구조 학습
- 이벤트 기반 아키텍처 연구

2023-현재: 시스템 설계 중심
- 실시간 & 이벤트 기반 설계
- 장애 격리 & 복구 전략
- 운영 가능한 시스템 설계
```

### 목표

> **"설계 판단과 운영 가능성을 증명하는 시스템 엔지니어"**

단순히 코드를 작성하는 것이 아니라:
- 왜 이 구조를 선택했는지 설명할 수 있는
- 장애 시 어떻게 동작할지 예측할 수 있는
- 조직에 지식을 남길 수 있는

그런 엔지니어를 지향합니다.

---

## 🔍 How to Read This Portfolio

### 추천 읽기 순서

#### 1. 빠른 이해 (15분)
```
1. Overview (본 문서) - 전체 맥락
2. Main Portfolio README - 핵심 설계 3가지
3. React Portfolio README - 운영 도구 구현
4. Coin API README - 적용 사례
```

#### 2. 설계 판단 이해 (30분)
```
1. Main: 설계 결정 과정 문서
   → 왜 이렇게 설계했는가
2. Main: 장애 영향도 매트릭스
   → 어떻게 격리하는가
3. React: 상태 관리 설계
   → UI 상태를 어떻게 다루는가
4. Coin API: 정규화 계층 설계
   → 외부 의존성을 어떻게 격리하는가
```

#### 3. 구현 능력 검증 (1시간)
```
1. Main: 기술 스택 가이드
   → 실제 코드 예시
2. React: 컴포넌트 구조
   → Frontend 구현 능력
3. Main: 구현 로드맵
   → 단계별 구현 계획
4. Main: 운영 가이드
   → 실제 운영 시나리오
```

#### 4. 깊이 있는 이해 (2시간+)
```
1. 모든 상세 문서 읽기
2. 다이어그램 분석
3. 코드 구조 검토
```

---

## 📧 Contact & Links

**GitHub**: [1985jwlee](https://github.com/1985jwlee)  
**Email**: [Your Email]  
**Blog**: [Your Tech Blog]  
**LinkedIn**: [Your LinkedIn]

---

## 📝 License

이 포트폴리오는 학습 및 평가 목적으로 공개되었습니다.

---

## 🎯 Final Message

### 이 포트폴리오가 증명하는 것

✅ **코드 작성 능력이 아닌 시스템 설계 판단력**
- 왜 이 구조를 선택했는지
- 어떤 트레이드오프가 있었는지
- 의도적으로 무엇을 선택하지 않았는지

✅ **도메인을 넘어선 설계 원칙의 일반화**
- 게임 서버에서 증명한 원칙
- 비게임 도메인에서 재검증
- UI 구현에도 동일 원칙 적용

✅ **실무 관점의 운영 가능성 고려**
- 장애 시나리오별 대응 방안
- 복구 전략의 우선순위
- 인수인계 가능한 구조

### 검증 방법

- **설계 문서**: 모든 판단의 근거 명시
- **운영 가이드**: 장애 대응 방안 구체화
- **코드 증거**: 추상적 설명이 아닌 실제 구현
- **확장 시나리오**: 10배 성장 대응 전략

---

> **"더 만들 수 있다"가 아니라 "언제 멈춰야 하는지 안다"**

---

**Last Updated**: 2025-01-15
