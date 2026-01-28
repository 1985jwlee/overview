# 📌 Portfolio Overview

이 저장소는 개별 프로젝트의 나열이 아닌,  
서로 다른 도메인에서 반복적으로 등장한 **설계 판단과 사고 방식**을 정리한 포트폴리오입니다.

🎮 게임 클라이언트  
🖥️ 프론트엔드  
🛠️ 백엔드  
🌐 IoT 플랫폼  

도메인과 기술 스택은 달라졌지만,  
각 프로젝트는 공통적으로 다음 질문을 중심으로 설계되었습니다.

- 📐 복잡도를 어디에서 제어할 것인가  
- 🧩 책임과 상태를 어떻게 분리할 것인가  
- ⚖️ 어떤 트레이드오프를 감수할 것인가  

---

## 🗂️ Portfolio Index

각 개별 포트폴리오는 아래 저장소들에 정리되어 있습니다.

- 🔗 Portfolio Main (Index)  
  https://github.com/1985jwlee/portpolio_main

- 🔗 IoT Backend (Production)  
  https://github.com/1985jwlee/production-iot-backend

- 🔗 Coin Data API  
  https://github.com/1985jwlee/portpolio_coindataapi

- 🔗 Frontend (React SPA)  
  https://github.com/1985jwlee/portpolio_react

- 🔗 Game Project (Unity)  
  https://github.com/1985jwlee/portpolio_vampiresurvival

- 🔗 Shader & Rendering Experiments  
  https://github.com/1985jwlee/portpolio_shader

---

## 🧭 Portfolio Direction

이 포트폴리오는 특정 기술이나 구현 결과를 강조하기보다,  
각 시점에서 **어떤 선택지를 비교했고 어떤 기준으로 판단했는지**에 초점을 둡니다.

모든 프로젝트는 요구사항, 운영 환경, 리스크 조건에 따라  
서로 다른 구조와 우선순위를 가졌으며,  
그 차이 자체가 다음 프로젝트의 설계 기준으로 이어졌습니다.

---

## 🧠 Architecture Thinking

모든 프로젝트에서 설계는  
구현 방법을 정하는 일보다,  
먼저 **어떤 문제를 복잡하게 만들지 않을 것인가**를 정하는 과정이었습니다.

이를 위해 다음과 같은 질문을 반복적으로 사용했습니다.

- 이 문제는 반드시 실시간으로 해결되어야 하는가  
- 실패했을 때 시스템 전체에 영향을 주는가  
- 변경 가능성이 높은 영역은 어디인가  
- 책임과 상태는 명확히 분리되어 있는가  

이 질문들은  
게임, 프론트엔드, 백엔드, IoT라는 서로 다른 도메인에서도  
일관되게 설계 판단의 기준으로 작동했습니다.

---

## 🏗️ Flagship Project

### 🚦 Smart Road Watering System – IoT Backend  
🔗 https://github.com/1985jwlee/production-iot-backend

실제 운영 환경을 전제로 설계된 IoT 백엔드 시스템입니다.  
장비 오류, 네트워크 불안정, 부분 장애를 **기본 조건**으로 두고 구조를 설계했습니다.

즉각적인 제어 응답성보다  
운영 안정성, 장애 격리, 시스템 복원력을 우선했으며,  
메시지 기반 처리와 책임 분리를 통해  
장애가 전체 시스템으로 확산되지 않도록 구성했습니다.

---

## 💱 Data Platform Project

### Coin Data API  
🔗 https://github.com/1985jwlee/portpolio_coindataapi

외부 API에 의존하는 데이터 수집 및 제공 플랫폼입니다.  
데이터의 완전한 실시간성보다,  
서비스의 지속 가능성과 운영 안정성을 중심으로 구조를 설계했습니다.

캐시와 비동기 처리, 장애 격리 전략을 통해  
외부 서비스 장애가 내부 시스템에 미치는 영향을 최소화하는 것을 목표로 했습니다.

---

## 🎮 Game Development Experience

### Vampire Survival (Unity)  
🔗 https://github.com/1985jwlee/portpolio_vampiresurvival  
🔗 https://github.com/1985jwlee/portpolio_shader

게임 개발 경험은 실시간 처리, 상태 관리, 사용자 체감에 대한 이해를 제공했습니다.  
프레임 단위 사고와 즉각적인 피드백 구조는  
이후 서버 및 플랫폼 설계에서 처리 우선순위를 판단하는 기준이 되었습니다.

---

## 🖥️ Frontend Experience

### React SPA Portfolio  
🔗 https://github.com/1985jwlee/portpolio_react

프론트엔드 개발 경험을 통해  
API를 단순한 구현이 아닌 **계약**의 관점에서 바라보게 되었습니다.

상태 표현, 에러 처리, 비동기 흐름에 대한 이해는  
백엔드 설계 시 인터페이스 안정성과 책임 분리를  
더 중요하게 고려하게 만든 배경이 되었습니다.

---

## 🧩 Common Architecture Themes

모든 프로젝트에 동일한 구조를 적용하지는 않았지만,  
다음과 같은 기준은 반복적으로 등장했습니다.

- 책임 분리와 명확한 경계 설정  
- 장애 전파 최소화  
- 계약(API / 인터페이스) 중심 설계  
- 운영과 유지보수를 고려한 구조  

이 기준들은 도메인에 따라 다르게 적용되었으며,  
그 과정에서 얻은 경험이 다음 프로젝트의 설계 판단으로 이어졌습니다.

---

## 🧠 Closing

이 포트폴리오는  
특정 기술이나 도메인을 증명하기 위한 기록이 아니라,  

서로 다른 환경과 요구사항 속에서  
**어떤 기준으로 구조를 선택하고 판단해왔는지**를 정리한 요약입니다.

각 프로젝트는 독립적인 결과물이면서 동시에,  
다음 선택을 위한 판단 근거로 연결되어 있습니다.