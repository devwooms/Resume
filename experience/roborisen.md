## 경력사항
### (주)로보라이즌 *(2020.07 ~ 2024.09)*
**앱 개발 전담 (1인)** | Lead Developer | 설계·개발·배포·유지보수 전 과정 담당

**핵심 성과:**
  - Scratch 모바일 포팅(WebView + WebSocket + BLE) → 누적 다운로드 **10만+** 달성
  - Android SpeechRecognizer 기반 STT 인식률 **45% → 85%** 개선 (아동 음성 1,000회 테스트)
  - KT(MOU 체결), LG, 네이버 커넥트재단, 팀모노리스 등 **4개 외부 기업** 연동 소프트웨어 개발 및 기술 지원
  - Android/iOS/Windows 하드웨어 연동 앱 **7개 신규 개발**, **5개 기능 확장·유지보수**
  - Nordic BLE 기반 하드웨어 데이터 통신, 펌웨어 업데이트 프로토콜 구현

### 기술 스택
  - 주력
    - Kotlin (Android, 4년), JavaScript/TypeScript (Electron/WebSocket, 4년)
  - 활용
    - Swift (iOS), Java (Android), Python (라이브러리/자동화)
  - 경험
    - Dart/Flutter, C# (Windows BLE 연결 브릿지 앱)
  - 아키텍처/디자인 패턴
    - MVVM, MVC, MVI
  - 프레임워크/플랫폼
    - Android: Jetpack
    - Web: Node.js, React, Electron
    - Cross-platform: Flutter
  - 빌드/의존성 도구
    - Gradle, Webpack, CocoaPods
  - 통신/프로토콜
    - BLE(Bluetooth Low Energy), HTTP/HTTPS(REST API), WebSocket
  - 인프라/배포
    - AWS (EC2)

## 프로젝트 개요

### 핵심 프로젝트

- [**1. PingPong Scratch (Android)**](#1-pingpong-scratch-android)
    > WebView+BLE 기반 Scratch 모바일 포팅, 누적 다운로드 **10만+**

- [**2. PingPong Voice Coding (Android)**](#2-pingpong-voice-coding-android)
    > STT 인식률 **45% → 85%** 개선 (1,000회 테스트 기준)

- [**3. PingPong Scratch (Windows)**](#3-pingpong-scratch-windows)
    > Scratch 오픈소스 커스텀 개발, 메모리 누수 해결, Teachable Machine 확장

### 주요 프로젝트

- [**4. PingPong Play (Android)**](#4-pingpong-play-android)
    > WebView Bridge 기반 하드웨어-게임 통신 아키텍처 구현

- [**5. KT Codiny (MOU 체결)**](#5-kt-codiny-mou-체결)
    > KT Ai Codiny 플랫폼 내 BLE 하드웨어 확장 모듈 개발

- [**6. PingPong Robot (Android, iOS)**](#6-pingpong-robot-android-ios)
    > 모든 BLE 하드웨어 모델을 지원하는 메인 앱 (Android/iOS)

- [**7. 네이버 커넥트재단 Entry**](#7-네이버-커넥트재단-entry)
    > Entry 플랫폼 하드웨어 확장 모듈 유지보수

- [**8. 팀모노리스 Codle**](#8-팀모노리스-codle)
    > Codle 플랫폼 하드웨어 연동 기술 검토 및 확장 모듈 개발

### 기타 프로젝트

| 프로젝트 | 플랫폼 | 핵심 내용 |
|----------|--------|-----------|
| [서양네트웍스 R:Robot 코딩로비](#9-서양네트웍스-rrobot-코딩로비-android-ios) | Android, iOS | 외부 기업 콜라보 BLE 코딩 교육 앱 개발 및 배포 |
| [PingPong Maker Coding](#10-pingpong-maker-coding-android) | Android | BLE 하드웨어 최대 4개 동시 연결 및 개별 모터 실시간 제어 |
| [PingPong Block Coding](#11-pingpong-block-coding-android) | Android | 하드웨어 부저 활용 작곡 + 반복문 블록 코딩 기능 개발 |
| [Python 라이브러리](#12-python-라이브러리) | Python | Jupyter Notebook 기반 BLE 하드웨어 제어 라이브러리 유지보수 |

## 프로젝트 상세

### 1. PingPong Scratch (Android)
- PC 전용 교육 플랫폼 Scratch를 모바일·태블릿에서 사용하려는 수요에 대응하여 Android 앱으로 포팅
 - Android WebView에서 WebBluetooth API 미지원으로, Scratch(WebView) ↔ WebSocket ↔ Android Native BLE 브릿지 구조 설계 및 구현
   > ![Scratch Android Working](../assets/experience/roborisen/Pingpong-Scratch_Android/working.gif)
 - BLE 연결 불안정 해결: Android 표준 BluetoothGatt의 연결 안정성 문제 → Nordic BLE 라이브러리로 전면 교체하여 내부 큐 기반 안정적 GATT 통신 확보
 - ChromeBook 미노출 해결: Manifest uses-feature 조건 수정으로 카메라 등 하드웨어 없이도 검색 가능하게 처리
 - 안드로이드 버전별 BLE 권한 대응 (Android 12 BLUETOOTH_SCAN/CONNECT 분리 등)
 - Scratch Window 업데이트 시 모바일 버전 최신화
 - 화면 확대/축소 기능, BLE Advertisement 기반 특정 기기 필터 연결 로직 추가
 - 누적 다운로드 **10만+** 달성
   > ![Scratch Android Download](../assets/experience/roborisen/Pingpong-Scratch_Android/download.png)

### 2. PingPong Voice Coding (Android) — 기능 추가·유지보수
 - 기존 STT 인식률 45%로 아동 사용자의 음성 명령 오인식 빈번하여 정확도 개선 착수
 - 아동 10명 대상 실제 사용 환경에서 음성 데이터 1,000회 수집 및 발화 패턴 분석
 - SpeechRecognizer 파라미터 튜닝 (침묵 감지 시간 등) 및 인식 결과 필터링 로직 추가 (아동 발화 오인식 보정)
 - UI/UX 변경으로 인식 재시도 편의성 향상
   > ![PingPong Voice Coding (Android) Voice 1](../assets/experience/roborisen/PingPong-Voice-Coding_Android/voice1.gif)
 - 삭제 기능 추가 및 음성 인식 방법 변경
   > ![PingPong Voice Coding (Android) Voice 2](../assets/experience/roborisen/PingPong-Voice-Coding_Android/voice2.gif)
 - 인식률 **45% → 85%** 개선 (동일 조건 10명 × 100회 = 1,000회 재테스트 기준)

### 3. PingPong Scratch (Windows) — 기능 추가·유지보수
 - Webpack + Node.js + Electron 기반 Scratch 오픈소스를 커스텀한 자사 하드웨어 연동 데스크탑 앱의 기능 확장 및 유지보수
 - 장시간 실행(2시간+) 시 프로그램 크래시 발생 → 전역 참조로 유지되어 GC가 회수하지 못하는 센서 데이터 누적 확인 → 센서 루프 주기마다 데이터 초기화 로직 추가하여 해결, **6시간 연속 실행 × 5회 반복** 메모리 모니터링으로 크래시 **0건** 검증
 - canvas 렌더링 누적으로 인한 성능 저하 → 렌더링 초기화 로직 추가
 - 하드웨어 연결 및 동작 컨트롤 확장 기능 개발
   > ![Scratch Window Extension](../assets/experience/roborisen/Pingpong-Scratch_Window/scratch_extension.png)
 - Tensorflow 기반 Google Teachable Machine을 활용한 Scratch 확장 기능 개발 (포즈/이미지 인식)
   > ![Scratch Window Teachable Machine Pose](../assets/experience/roborisen/Pingpong-Scratch_Window/teachablemachine_pose.gif)
 - Google Sheets REST API를 활용한 그래프 기능 개발 (Sheet 선택, 행/열 지정 등)
   > ![Scratch Window Google Spread Sheets](../assets/experience/roborisen/Pingpong-Scratch_Window/google-spread-sheet.gif)
 - 새로운 하드웨어 모델 추가, 각종 센서 데이터 처리 (습도, 초음파, 색 인식, 소리, 자석, 빛 등)
 - 도트매트릭스 표시 기능 추가 및 펌웨어 버전별 프로토콜 대응

### 4. PingPong Play (Android)
 - 학생들의 흥미 향상을 위한 하드웨어 연동 게임 앱 개발
 - WebView Bridge 기반 하드웨어-게임 통신 아키텍처 설계 및 구현
   - Three.js/WebGL 기반 HexGL 레이싱 게임에 자이로·가속도 센서 입력 연동
   - BLE 데이터 수신 → WebView Bridge → 게임 컨트롤 전달 파이프라인 구현
   > ![Play Android Game1](../assets/experience/roborisen/Pingpong-Play_Android/game1.gif)
 - Phaser 3/TypeScript 기반 2인용 슈팅게임에 동일 아키텍처 확장 적용
   > ![Play Android Game2](../assets/experience/roborisen/Pingpong-Play_Android/game2.gif)
 - RTSP 기반 IP 카메라 SDK를 활용한 Custom SurfaceView 구현
   > ![Play Android Camera](../assets/experience/roborisen/Pingpong-Play_Android/camera.gif)

### 5. KT Codiny (MOU 체결)
 - KT와 MOU 체결을 통해, KT Ai Codiny 플랫폼에 BLE 하드웨어 연동 확장 모듈 신규 개발
 - KT 플랫폼의 코드 구조에 맞춰 BLE 하드웨어 확장 모듈 개발 후 merge
 - 데이터 송수신·연결 안정성 검증 후 플랫폼 정식 적용, 현재 실 서비스 운영 중
 - 하드웨어 **3종** 추가 지원 및 고객 피드백 기반 UI/UX 개선
   > ![KT Codiny AI Codiny](../assets/experience/roborisen/KT-Codiny/Ai-Codiny.png)

### 6. PingPong Robot (Android, iOS) — 기능 추가·유지보수
 - 회사의 모든 BLE 하드웨어 모델을 지원하는 메인 앱 (Android/iOS)
 - 여러 하드웨어 모델의 동작을 블록 코딩으로 제어하는 기능 구현
 - 펌웨어 업데이트 및 특정 기기 연결을 위한 BLE 프로토콜 구현
 - 새로운 모델 추가 개발 및 동작 계산 로직 구현 (Mono, Single Car 등)
 - 펌웨어 버전별 프로토콜 변경 대응
 - 배터리 잔량 표시, 조이스틱, 그룹 지정 기능 추가
 - 안드로이드 버전 업데이트 시 BLE 권한 대응

### 7. 네이버 커넥트재단 Entry — 유지보수
 - 네이버 커넥트재단 Entry 플랫폼의 하드웨어 확장 모듈 유지보수
 - BLE 연결 해제 후 재인식 불가 이슈의 근본 원인(상태 미초기화)을 추적하여 해결 → 연결 끊어짐 감지 시 상태 초기화 후 재시작 로직 구현
   > ![네이버 커넥트재단 Entry](../assets/experience/roborisen/네이버-커넥트재단-Entry/entry.png)

### 8. 팀모노리스 Codle
 - 팀모노리스 교육용 코스웨어 플랫폼 Codle에 하드웨어 연동 확장 모듈 신규 개발 및 기술 지원
 - Codle 플랫폼의 API 연동 방식과 BLE 프로토콜 버전 호환성을 검토하여 연결 방안 설계
 - 하드웨어 모델별 동작 확장 모듈 개발 및 플랫폼 적용
   > ![팀모노리스 Codle](../assets/experience/roborisen/팀모노리스-Codle_Window/codle.png)

### 9. 서양네트웍스 R:Robot 코딩로비 (Android, iOS)
 - 서양네트웍스 R:Robot과의 콜라보레이션으로 BLE 코딩 교육 앱 개발
 - Android/iOS 앱 개발 및 배포
   > ![서양네트웍스 코딩로비](../assets/experience/roborisen/서양네트웍스-코딩로비_iOS&Android/codingroby.gif)

### 10. PingPong Maker Coding (Android)
 - 기존 앱의 모델 종속 제약을 해소하기 위해 개발한 하드웨어 개별 제어 앱 (최대 4개 동시 제어)
 - BLE 하드웨어 최대 4개 동시 연결 및 실시간 개별 모터 제어 기능 구현
 - 타이머 기능 및 하드웨어별 기능 재할당 기능 개발

### 11. PingPong Block Coding (Android)
 - 메인 앱에 없는 작곡(하드웨어 부저 활용)과 반복문 기능을 추가한 블록 코딩 앱
 - 하드웨어 부저를 활용한 작곡 기능 및 반복문 블록 코딩 기능 개발
   > ![PingPong Block Coding (Android)](../assets/experience/roborisen/PingPong-Block-Coding_Android/block.gif)

### 12. Python 라이브러리 — 유지보수
 - Jupyter Notebook 환경에서 Python 수업을 지원하는 BLE 하드웨어 제어 라이브러리 유지보수
 - 센서별 데이터 처리 오류 수정 및 라이브러리 안정화

---

### 기타 업무
- 자사 홈페이지 및 자체몰 수정·관리 (JavaScript, HTML/CSS)
