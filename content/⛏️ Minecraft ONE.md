---
publish: true
tags:
  - Featured
---

# ⛏️ Minecraft: ONE

## 📑 개요

Minecraft: ONE 은 **만약 2026 년에 Minecraft 가 새롭게 다시 개발된다**는 가정 아래, 최종적으로 내려질 수 있는 하나의 선택을 탐구해보는 개인적인 연구 프로젝트이다.

Minecraft: ONE 의 최종 지향점은 Minecraft 의 정체성을 유지함과 동시에, 시스템 / 생태계 / 플레이 환경을 재설계하는 것이다. 프로젝트의 진행 과정에서 가정할 개발 주체는 Microsoft 와 Mojang Studios 이다.

ONE 이라는 부제에는 각기 다른 두 가지 의미가 담겨있다. 첫 번째 의미는 Minecraft 의 공식적인 차원 3 개, **Overworld**, **Nether**, **End**의 첫 글자를 딴 것이다. 두 번째 의미는 **하나**의 선택을 탐구한다는 프로젝트의 취지를 상징한다.

## 🎯 문제 정의

현재 Minecraft 는 크게 두 가지의 플랫폼이 공존하고 있다. 2009 년 출시된 Java Edition 과, 2011 년 출시된 Bedrock Edition 이다.

Java Edition 은 커뮤니티의 개방성과 안정적인 실행 환경, 모딩 프레임워크의 발전을 바탕으로 방대한 유저 콘텐츠 생태계를 구축하는데 성공하였다. 그러나 본질적으로 JVM 런타임 위에서 실행되기에 모바일 및 콘솔 플랫폼 지원이 전무한 상태이다. 이에 더하여 코드 베이스 전체가 Java 라는 관리형 언어로 구성되어 최적화 문제가 고질적이다. 내부 데이터 모델 또한 Plain Text (설정 파일), Anvil (청크 파일), NBT (인게임 객체) 등 현대적인 대안이 존재하는 규격을 다수 사용한다.

Bedrock Edition 은 모바일 / 콘솔 플랫폼을 대응하였던 Pocket Edition / Console Edition 의 후신으로서 현재 PC 플랫폼까지 지원하는 통합 에디션이다. 모바일 / 콘솔 플랫폼 지원에 필수적인 저사양 기기 성능 최적화를 C++ 을 통해 해결하였다. 이외에도 Xbox 생태계 연동, LevelDB 를 활용한 청크 저장 등 Java Edition 이 이루지 못하였던 기술적 성취를 이루었다.

허나 성능 최적화를 위해 도입된 적극적인 멀티스레드 비동기 연산은 비결정론적 구조의 한계상 싱글스레드 동기식 연산을 사용하는 Java Edition 과 로직 구현이 달라지는 문제가 존재한다. 이는 Minecraft 의 주요 콘텐츠 중 하나인 레드스톤 회로와 명령어 스크립팅에 결정적인 영향을 끼쳤다. 또한 C++ 로 개발된 특성상 런타임 단계에서의 자유로운 코드 주입이 어려워 모딩 플랫폼의 발전이 빈약하였고, 대안으로 도입된 스크립트 API 마저 Java Edition 의 Mixin 방식에 비하면 상대적으로 자유도가 떨어진다.

Minecraft: ONE 의 목적은 하나이다. Java Edition 의 개방성과 예측 가능성, Bedrock Edition 의 통합성과 성능 최적화라는 가치를 하나의 Minecraft 아래에 위치시키는 것. 해당 과정에서 가치들이 상충하는 지점을 명확히 직시하며 하나의 선택을 탐구할 것이다.

## ⚙️ 시스템

### 🧑‍💻 엔진 설계

Minecraft: ONE 은 Bedrock Engine 의 아키텍처 설계 원칙, 즉 크로스 플랫폼 호환성, 성능 최적화, 모듈화를 계승한 차세대 엔진, 가칭 NEO (Native Executable ) Engine 을 사용한다. Bedrock Engine 은 Bedrock Edition 에서 사용된 전례가 있으며, 모바일 / 콘솔 플랫폼 지원을 가능케한 핵심적인 엔진이다. 그러나 추후 서술할 Minecraft: ONE 이 요구하는 아키텍처 변화에 대응하기 위해서는
