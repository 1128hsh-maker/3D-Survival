# 🚀 [프로젝트 제목] - 3D 플레이어 및 아이템 상호작용 시스템

> Unity에서 개발된 1인칭(또는 3인칭) 환경을 위한 고급 캐릭터 컨트롤러와 모듈형 아이템 상호작용 시스템.

## 🌟 프로젝트 개요

이 프로젝트는 키보드 및 마우스 입력을 통해 조작되는 캐릭터 컨트롤러(`Player.cs`)와, 게임 내 아이템의 속성 및 상호작용 로직을 정의하는 데이터 기반 시스템을 구현합니다. 캐릭터는 점프(`launchingpad.cs`), 속도 부스트(`SpeedUp.cs`)와 같은 환경 상호작용 및 아이템 효과를 받으며, 실시간으로 HP와 인벤토리 정보를 UI에 표시합니다.

### 💡 주요 특징

* **1인칭 컨트롤러:** 입력 시스템(`UnityEngine.InputSystem` 사용 추정)을 활용한 WASD 이동 및 마우스 기반 시선 처리(`CameraLook()`)를 구현합니다.
* **아이템 시스템 (ScriptableObject):** `Item.cs`를 `ScriptableObject`로 정의하여 아이템 데이터(이름, 설명, 프리팹)를 에디터에서 쉽게 생성 및 관리할 수 있습니다.
* **HP 및 UI 관리:** `PlayerUI.cs`를 통해 플레이어의 HP 바를 시각적으로 표시하고, 대미지 반영 및 최대 HP 설정 기능을 제공합니다.
* **상호작용 로직:** 레이캐스트 또는 박스 캐스트(`ItemCheck()`)를 사용하여 플레이어가 아이템이나 상호작용 오브젝트를 바라볼 때 정보를 표시합니다.
* **환경 상호작용:** `launchingpad.cs`와 같은 오브젝트를 통해 플레이어에게 물리적인 힘(점프)을 가하거나, `SpeedUp.cs`를 통해 일정 시간 동안 속도를 증가시키는 버프를 제공합니다.

## 💻 스크립트 구성 및 역할

| 파일 그룹 | 파일명 | 역할 및 기능 상세 |
| :--- | :--- | :--- |
| **캐릭터 컨트롤러** | `Player.cs` | **핵심 플레이어 로직:** 이동(`mS`, `jP`), 마우스 시선 처리, `Rigidbody` 기반 물리 제어. 아이템 상호작용 확인(`ItemCheck()`). |
| | `PlayerManager.cs` | `Player.cs`의 상위 클래스로, 향후 캐릭터 상태 관리(HP, 스탯) 확장을 위한 기본 구조. |
| | `launchingpad.cs` | 플레이어가 밟을 때 위쪽 방향으로 순간적인 힘(`JF`)을 가하는 환경 오브젝트 로직. |
| **아이템 시스템** | `Item.cs` | **ScriptableObject 기반 아이템 데이터 정의:** 이름, 설명, 아이콘, 드롭/장착 프리팹 정보 포함. |
| | `ItemData.cs` | 씬 내 오브젝트에 `Item.cs` ScriptableObject를 연결하는 컴포넌트. |
| | `SpeedUp.cs` | 아이템 사용 또는 상호작용 시 플레이어의 이동 속도를 일정 시간 동안 증가시키는 코루틴 기반 버프 로직. |
| **UI 및 상태** | `PlayerUI.cs` | **HP 관리 UI:** 플레이어의 HP를 표시(`Slider`)하고, 최대 HP 설정 및 대미지(`GetDamage()`) 반영. |
| | `GameUI.cs` | **인게임 UI (싱글톤):** 아이템 이름(`itemName`) 등의 인게임 정보를 표시. |
| | `GameManager.cs` | 게임 로직 관리 (현재는 `GameUI`의 정보 업데이트 관련 주석 처리된 내용만 포함). |

## 🛠️ 설치 및 실행

### 1. 요구 사항

* Unity Editor (3D 프로젝트 환경)
* TextMeshPro 패키지 (UI 텍스트 출력을 위해 필요)
* **새로운 Unity Input System** 사용 (스크립트(`Player.cs`)의 `InputAction` 참조를 통해 추정)

### 2. 프로젝트 설정

1.  본 저장소를 클론하거나 다운로드합니다.
2.  Unity 프로젝트를 엽니다.
3.  **플레이어 설정:**
    * 주인공 오브젝트에 `Rigidbody`와 `Player.cs`, `PlayerManager.cs` 컴포넌트를 부착합니다.
    * 카메라 오브젝트를 `Player.cs`의 `cameraContainer`에 연결하고, 마우스 잠금(`Cursor.lockState = CursorLockMode.Locked;`)이 활성화되도록 설정합니다.
4.  **UI 설정:**
    * Canvas에 `GameUI.cs` 및 `PlayerUI.cs`가 포함된 오브젝트를 배치하고, `PlayerUI.cs`의 슬라이더(`_hpBar`)를 연결합니다.
5.  **아이템 설정:**
    * `Assets/` 폴더 내에 `CreateAssetMenu`를 통해 `Item` ScriptableObject 인스턴스를 생성하고, 이를 씬의 아이템 오브젝트에 `ItemData.cs` 컴포넌트를 통해 연결합니다.

## 🤝 기여 방법 (Contributing)

이 프로젝트는 오픈 소스로 진행됩니다. 모든 기여를 환영합니다!

1.  저장소를 Fork 합니다.
2.  새로운 브랜치를 생성합니다. (`git checkout -b feature/NewFeature`)
3.  변경 사항을 커밋합니다. (`git commit -m 'Implement New Feature'`)
4.  Pull Request를 제출합니다.

## 📜 라이선스

이 프로젝트는 **[원하는 라이선스 명시. 예: MIT License]**에 따라 배포됩니다.
