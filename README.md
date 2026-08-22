# ThisisnotD

Unity 기반으로 제작한 3D 플랫포머 게임입니다.

제한 시간 안에 스테이지를 진행하며, 장애물과 보스의 공격을 피하고 목표 지점까지 도달하는 게임입니다.

---

## 📖 프로젝트 소개

ThisisnotD는 플레이어의 이동과 물리 상호작용을 기반으로 스테이지를 진행하는 3D 플랫포머 게임입니다.

게임 진행 과정에서 체크포인트를 통해 현재 진행 상태를 관리하고, 플레이어가 사망할 경우 마지막 체크포인트에서 다시 게임을 진행할 수 있도록 구현했습니다.

후반부에는 보스의 이동과 시야를 활용한 추적 및 감지 시스템을 구현했으며, 플레이어는 이동 가능한 오브젝트나 엄폐물을 활용하여 보스의 감지를 피하며 스테이지를 진행합니다.

| 항목 | 내용 |
| --- | --- |
| 개발 기간 | 3개월 |
| 개발 인원 | 총 3명 |
| 팀 구성 | 그래픽 2명 / 프로그래밍 1명 (본인) |
| 플랫폼 | PC |
| 개발 엔진 | Unity |
| 개발 언어 | C# |
| 담당 역할 | 클라이언트 프로그래밍 |

---

## 🎮 Gameplay

게임 플레이 영상은 아래 링크에서 확인할 수 있습니다.

[ThisisnotD Gameplay Video](https://youtu.be/aMAQvpVFlr4)

---

## 👨‍💻 My Role

### Client Programming

- 플레이어 이동 및 물리 기반 상호작용 구현
- 체크포인트 및 사망·리스폰 시스템 구현
- 게임 진행 상태 및 제한 시간 관리
- 보스의 단계별 이동 및 플레이어 감지 시스템 구현
- 이동 오브젝트 및 엄폐물 시스템 구현
- 카메라 전환 및 장면 이동 구현
- UI 및 게임 사운드 처리

---

# 🎯 주요 구현 기능

## 👁️ 보스 감지 및 단계별 행동 시스템

게임 진행 상태에 따라 보스의 이동과 플레이어 감지 방식이 변경되도록 구현했습니다.

플레이어의 체크포인트를 기준으로 보스의 페이즈를 관리하며, 각 단계에 따라 이동 속도와 행동 범위를 변경하도록 구성했습니다.

보스의 양쪽 눈은 각각 독립적으로 플레이어를 탐색하며, 두 감지 결과를 `BossEyes`에서 확인하여 플레이어의 감지 여부를 결정합니다.

**관련 코드**

- [BossControll.cs](https://github.com/Thispring/GameDesign02-ScriptOnly/blob/main/Script/Boss/BossControll.cs)
- [BossEyes.cs](https://github.com/Thispring/GameDesign02-ScriptOnly/blob/main/Script/Boss/BossEyes.cs)
- [LeftEye.cs](https://github.com/Thispring/GameDesign02-ScriptOnly/blob/main/Script/Boss/LeftEye.cs)
- [RightEye.cs](https://github.com/Thispring/GameDesign02-ScriptOnly/blob/main/Script/Boss/RightEye.cs)

---

## 🫥 엄폐 오브젝트를 고려한 플레이어 감지

보스의 시야 판정에 단순히 플레이어의 위치만 사용하는 것이 아니라, 플레이어와 보스 사이에 존재하는 오브젝트를 함께 고려하도록 구현했습니다.

`SphereCast`를 이용해 보스의 시야 방향에 존재하는 오브젝트를 탐색하고, 플레이어보다 먼저 이동 오브젝트나 엄폐물이 감지될 경우 플레이어가 숨겨진 상태로 처리합니다.

엄폐 오브젝트는 별도의 상태를 관리하며, 보스의 시야 판정에서 플레이어 감지 여부를 결정하는 데 활용됩니다.

**관련 코드**

- [LeftEye.cs](https://github.com/Thispring/GameDesign02-ScriptOnly/blob/main/Script/Boss/LeftEye.cs)
- [RightEye.cs](https://github.com/Thispring/GameDesign02-ScriptOnly/blob/main/Script/Boss/RightEye.cs)
- [HideObject.cs](https://github.com/Thispring/GameDesign02-ScriptOnly/blob/main/Script/HideObject.cs)
- [ObjectMove.cs](https://github.com/Thispring/GameDesign02-ScriptOnly/blob/main/Script/ObjectMove.cs)

---

## 📍 체크포인트 기반 사망 및 리스폰 시스템

플레이어의 현재 진행 위치를 체크포인트 단위로 관리하고, 사망 시 마지막으로 도달한 체크포인트에서 게임을 다시 진행할 수 있도록 구현했습니다.

체크포인트에 도달하면 현재 위치를 플레이어의 마지막 체크포인트로 저장하고 게임 진행 상태를 갱신합니다.

플레이어가 낙하하거나 보스에게 감지되어 사망할 경우, 일정 시간 후 저장된 체크포인트 위치를 기준으로 플레이어를 리스폰하도록 구성했습니다.

**관련 코드**

- [CheckPoint.cs](https://github.com/Thispring/GameDesign02-ScriptOnly/blob/main/Script/CheckPoint.cs)
- [PlayerState.cs](https://github.com/Thispring/GameDesign02-ScriptOnly/blob/main/Script/Player/PlayerState.cs)
- [FallChecker.cs](https://github.com/Thispring/GameDesign02-ScriptOnly/blob/main/Script/FallChecker.cs)

---

# 🛠 사용 기술

| 기술 | 활용 |
| --- | --- |
| Unity | 게임 클라이언트 개발 |
| C# | 게임 로직 및 시스템 구현 |
| Unity Physics | 플레이어 및 오브젝트 물리 상호작용, 충돌 및 감지 처리 |
| Unity UI | 게임 진행 정보 및 인터페이스 구현 |

---

# 🔗 Links

### 🎥 Gameplay Video

[YouTube - ThisisnotD Gameplay](https://youtu.be/aMAQvpVFlr4)

### 💾 Download

**Windows**

[Download for Windows](https://drive.google.com/file/d/13_nnEqndyE6TdsRHDRKyuC7JMCueaRo7/view?usp=drive_link)

**macOS**

[Download for macOS](https://drive.google.com/file/d/1YgbZ_0cqSjRkVH5SivMYDDFPsDBWPGR3/view?usp=drive_link)

---

> 본 리포지토리는 포트폴리오 공개를 목적으로 프로젝트의 스크립트 코드만 포함하고 있습니다.
>
> 게임 에셋 및 전체 Unity 프로젝트 파일은 포함되어 있지 않습니다.
