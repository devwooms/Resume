# Raspberry-Pi_BLE-HUB *(2025.04 ~ 진행중)*

## 프로젝트 개요

### 문제
> Windows 노트북과 macOS 노트북을 번갈아 사용할 때, 마우스·키보드·이어폰과 같은 주변기기를 매번 다시 연결해야 하는 번거로움

### 솔루션
> Raspberry Pi를 BLE Hub로 사용하여 여러 장치를 동시에 관리하고, 연결된 디바이스(노트북, 스마트폰 등)로 입력을 실시간 전달하는 시스템

- 하나의 마우스/키보드/이어폰을 다양한 기기에서 매끄럽게 전환/공유
- BLE(HID) 기반 입력 디바이스 전송, Classic Bluetooth(A2DP) 오디오 전송 예정
- 모듈화된 구조로 각 디바이스를 독립적으로 관리

## 현재 성과

- **BLE 마우스 프로파일 구현 완료**
  - HID Usage Table 참조하여 HID Report Descriptor 직접 작성 (버튼/축/스크롤)
  - BlueZ + dbus-python을 통한 GATT/HID 프로파일 코드 레벨 제어
  - 호스트-클라이언트 간 입력 전달 파이프라인 검증
  > ![Mouse Check](../assets/experience/project/bluetooth_hub/mouse_check.png)

- **Python 프로토타입으로 전체 구조 및 작동 검증 완료**

## 기술적 도전

- HID Report Descriptor를 직접 정의하여 OS 레벨에서 마우스로 인식되도록 구현
- BlueZ의 GATT/HID 프로파일을 D-Bus API로 다루는 저수준 BLE 제어
- 입력 장치의 이벤트를 실시간으로 연결된 디바이스에 전달하는 파이프라인 설계

## 기술 스택

| 분류 | 사용 기술 |
|------|-----------|
| 언어 | Python, C |
| BLE 스택 | BlueZ, dbus-python, GLib, PyGObject |
| 프로토콜 | Bluetooth, HID Report Descriptor |
| 컴파일러 | gcc |

## 향후 계획

- 키보드 HID 프로파일 확장
- 이어폰 오디오 프로파일 구현 (A2DP, Classic Bluetooth)
- UI 구현 (디바이스 관리/전환 인터페이스)
- Python 프로토타입 → C 리팩토링 (성능/안정성 강화)
- 프로파일 저장 (사용자 맞춤 설정 저장 및 불러오기)
- Raspberry Pi 외 다른 운영체제로 확장
