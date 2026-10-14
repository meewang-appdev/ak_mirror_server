# AkMirrorServer

![Flutter](https://img.shields.io/badge/Flutter-3.41.6-02569B?logo=flutter&logoColor=white)
![Dart](https://img.shields.io/badge/Dart-3.11.4-0175C2?logo=dart&logoColor=white)
![Rust](https://img.shields.io/badge/Rust-Core-000000?logo=rust&logoColor=white)
![Platform](https://img.shields.io/badge/Platform-Android%20only-3DDC84?logo=android&logoColor=white)
![License](https://img.shields.io/badge/License-AGPL--3.0-red.svg)

`AkMirrorEdgeServer`는 [AkMirrorEdge](#원소스-및-라이선스)(RustDesk Flutter 클라이언트 `flutter_hbb` 기반 커스텀 파생본)에서 **Android 수신자(서버) 전용 기능만 남기고 축소한 fork 저장소**입니다. 다른 기기에서 들어오는 원격 제어를 받고, 화면을 전송하고, 입력을 받는 동작만 담당합니다. 발신(클라이언트) 경로와 비 Android 플랫폼은 모두 제거됐습니다.

> [!IMPORTANT]
> 본 저장소는 일반 Flutter 앱처럼 의존성을 자유롭게 갱신하는 구조가 아닙니다. 현재 조합은 Rust 브리지·네이티브 라이브러리·Android 셸이 함께 검증된 운영 기준점입니다.

> [!WARNING]
> `pubspec.yaml` 및 `pubspec.lock`의 라이브러리 버전은 고정 운영 값입니다. 임의 업그레이드·다운그레이드·교체를 절대 금지합니다. 특히 `flutter_rust_bridge`, RustDesk 계열 git 의존성, 렌더링/플랫폼 연동 라이브러리를 바꾸면 ABI 불일치, 브리지 재생성 문제, 런타임 크래시가 발생할 수 있습니다.

> [!CAUTION]
> Android Rust 네이티브 라이브러리는 변경 불가입니다. 아래 기존 검증본을 반드시 사용해야 하며, 임의 교체 또는 재빌드 산출물 반영은 금지합니다.
> - Android: `android/app/src/main/jniLibs/arm64-v8a/librustdesk.so`

> [!NOTE]
> 아래 `고정 라이브러리 버전` 섹션은 현재 [`pubspec.yaml`](pubspec.yaml) 기준 운영 스냅샷입니다. README에 적힌 버전과 실제 파일 버전은 항상 동일하게 유지해야 합니다.

## 개요

| 항목 | 값 |
| --- | --- |
| 프로젝트명 | `AkMirrorEdgeServer` |
| 패키지명 (Flutter) | `flutter_hbb` |
| Android `applicationId` | `com.carriez.flutter_hbb.server` |
| Android 앱 라벨 | `AkMirrorEdgeServer` |
| Kotlin 소스 네임스페이스 | `com.carriez.flutter_hbb` (JNI 호환 유지) |
| 앱 버전 | `1.4.4+64` |
| Flutter/Dart 환경 | Flutter SDK `3.41.6`, Dart SDK `^3.11.4` |
| Rust 브리지 | `flutter_rust_bridge` `1.80.1` |
| 원본 저장소 | [`AkMirrorEdge`](#원소스-및-라이선스) (`b36dd9f`) |
| 분리 시점 | 2026-04-17 (Stage A 리팩터 완료본) |
| 지원 플랫폼 | **Android 전용** (arm64-v8a) |
| 핵심 진입점 | [`lib/main.dart`](lib/main.dart) |
| 핵심 세션 컨트롤러 | [`lib/models/model.dart`](lib/models/model.dart) |
| 생성 브리지 | [`lib/generated_bridge.dart`](lib/generated_bridge.dart) |
| 운영 기준 | P0-A/B fault boundary + video pressure guard 적용, 12시간 최종 복합 테스트 PASS |
