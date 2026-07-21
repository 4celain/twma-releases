# TWMA Privacy / 개인정보 처리 안내

## 한국어

TWMA는 창 배치 복원에 필요한 정보를 이 Mac 안에만 저장합니다.

### 로컬에 저장하는 정보

- 작업공간 이름과 마지막 변경 시각
- 저장 대상 앱의 이름과 bundle identifier
- 작업공간을 만들거나 업데이트할 때 활성 데스크탑에 보이는 일반 창의 제목, 창 종류와 순서 및 마지막 전면 앱·창
- 모니터 식별자·이름·논리 해상도·배치·배율·회전·내장 여부
- 모니터별 레이아웃과 창별 배치 영역 번호
- 복원할 때 앱을 실행할지 여부와 자동 복원 대상으로 선택된 작업공간
- 사용자가 직접 지정한 작업공간 복원 단축키와 모든 모니터에 공통인 메뉴 고정 레이아웃 1~4번 슬롯 단축키 조합
- 사용자가 지정한 앱 배치 방식과 앱 이름·bundle identifier
- 언어, 드래그 배치, 미리보기 스타일, Dock 공간 확보, 창 사이 간격, 자동 복원, 로그인 실행과 자동 업데이트 확인 설정

작업공간 데이터는 `~/Library/Application Support/TWMA/profiles-v1.json`에 저장합니다. `새 작업공간`을 만들 때 현재 창 목록과 배치를 새로 저장하고, 저장된 작업공간에서 `업데이트`를 실행하면 해당 작업공간의 창 목록과 배치를 현재 상태로 교체합니다. `이름 변경`은 작업공간 이름만 바꾸며, `삭제`는 저장된 작업공간만 지우고 열려 있는 창은 변경하지 않습니다.

나머지 앱 설정과 앱 호환성 정책은 이 Mac의 TWMA 환경설정에 별도로 저장하며, 로그인 실행 상태는 macOS 로그인 항목이 관리합니다. 저장·복원 결과로 표시하는 호환 상태는 백업하지 않습니다.

Application Support 폴더는 현재 사용자만 접근할 수 있는 `700`, 프로필 파일은 `600` 권한으로 저장합니다.

### 진단 로그

TWMA는 드래그 배치와 복원 실패를 확인하기 위한 기술 로그를 `~/Library/Logs/TWMA.log`에 저장합니다. 로그에는 창 제목, 사용자가 붙인 작업공간 이름과 URL을 기록하지 않습니다. 실행된 앱을 정확한 빌드와 연결하기 위해 앱 버전·빌드 번호·bundle identifier·소스 commit ID와 clean/dirty 상태를 기록합니다. 복원과 성능을 진단할 때 무작위 복원 세션 ID, 실행 계기, 모니터·성공·실패 창 수, 앱의 bundle identifier, 후보 창 수와 처리 시간이 기록될 수 있습니다.

로그가 512 KiB를 넘으면 `TWMA.previous.log` 한 개로 교체하며 계속 누적하지 않습니다. 두 로그 파일 모두 현재 사용자만 읽을 수 있는 `600` 권한을 사용합니다.

### 수집하거나 전송하지 않는 정보

- 계정, 비밀번호, 사용자가 지정한 단축키 조합 외의 키 입력과 화면 이미지
- 창 안의 문서 내용
- 분석·광고·추적 데이터
- 클라우드 또는 제3자 서버에 업로드하는 창·작업공간·진단 로그 데이터

TWMA는 일반 앱 창을 읽고 이동하고 크기를 조절하기 위해 macOS 손쉬운 사용 권한을 사용합니다. 활성 데스크탑에 보이는 일반 창만 작업공간 저장 대상으로 삼습니다.

### 업데이트 확인

공개 배포본은 기본적으로 새 버전을 확인하며 `일반`에서 자동 확인을 끄거나 `업데이트 확인…`을 직접 실행할 수 있습니다. 확인 요청은 `https://raw.githubusercontent.com/4celain/twma-releases/main/appcast.xml`로 전송됩니다. 이때 GitHub는 연결에 필요한 IP 주소와 표준 HTTP 정보, `TWMA/앱 버전 Sparkle/프레임워크 버전` 형식의 User-Agent를 처리할 수 있습니다. TWMA는 시스템 프로필 전송을 끄며 창·작업공간·진단 로그·기기 모델·메모리·언어 정보를 피드 URL에 추가하지 않습니다.

새 버전이 있으면 서명된 DMG를 GitHub Releases에서 내려받습니다. 설치와 앱 재실행은 사용자가 승인할 때만 진행하며 무음 설치와 델타 업데이트는 사용하지 않습니다. 개발 Bundle ID 빌드에서는 업데이트 서비스를 시작하지 않습니다.

사용자가 앱 안의 버그 제보·지원 링크를 누르면 macOS 기본 브라우저가 구성된 외부 HTTPS 페이지를 엽니다. 앱은 해당 페이지에 창·작업공간 데이터를 첨부하거나 자동 전송하지 않습니다.

### 사용자가 내보내는 백업

`앱 및 데이터`의 `백업 내보내기`에서 만든 JSON 파일에는 저장된 작업공간의 이름·변경 시각·선택적 복원 단축키와 앱·창·모니터·레이아웃·배치 영역 정보, 앱 표시 언어·미리보기·드래그 배치·Dock 공간 확보·창 사이 간격·자동 복원·자동 업데이트 확인 설정, 기본·모니터별 레이아웃·메뉴 즐겨찾기·전역 1~4번 슬롯 단축키·자동 복원 대상, 앱 배치 방식과 백업 형식 정보가 포함됩니다. 손쉬운 사용 권한, 로그인 항목 상태와 승인, 진단 로그, 첫 실행 안내 확인 여부, 설정창 위치와 선택한 설정 메뉴는 포함하지 않습니다.

백업은 사용자가 선택한 위치에만 저장되며 자동 업로드되거나 동기화되지 않습니다. 파일 권한을 지원하는 저장소에서는 현재 사용자만 읽고 쓸 수 있는 `600` 권한을 적용합니다. 가져오는 프로필이나 백업 파일이 8 MiB를 넘으면 현재 데이터를 바꾸지 않고 거부합니다.

작업공간은 앱에서 개별 삭제할 수 있습니다. 전체 작업공간 기록을 제거하려면 TWMA를 종료한 뒤 `profiles-v1.json`을 삭제할 수 있습니다. 이 파일을 삭제해도 별도로 저장된 앱 설정, 앱 동작 정책과 진단 로그는 삭제되지 않습니다.

공개 운영 표기는 `4celain`이며, 지원과 버그 제보는 [TWMA Issues](https://github.com/4celain/twma-releases/issues/new?template=bug_report.yml)에서 받습니다.

---

<a id="english"></a>

## English

TWMA stores the information required to restore window layouts only on this Mac.

### Information stored locally

- Workspace names and last-modified dates
- App names and bundle identifiers
- Titles, roles, ordering, and the last foreground app and window among ordinary windows visible on the active desktop when a workspace is created or updated
- Display identifiers, names, logical resolutions, arrangement, scale, rotation, and built-in status
- Per-display layouts and each window's target zone
- Whether an app may be launched, the selected automatic-restore workspace, optional workspace shortcuts, and the global pinned-layout shortcuts shared by slots 1–4 on every display
- Per-app Automatic, Position Only, and Excluded choices
- Language, drag-to-snap, preview style, Dock reservation, window gaps, automatic restore, launch-at-login, and automatic update-check preferences

Workspace data is stored at `~/Library/Application Support/TWMA/profiles-v1.json`. Creating a workspace records a new window set. Updating replaces that workspace's window list and positions. Renaming changes only its name, and deleting a workspace does not close or move open windows.

Other preferences and app-behavior policies are stored in this Mac's TWMA preferences. macOS manages the login item. Diagnostic compatibility results are not included in backups.

The Application Support directory uses `700` permissions and the profile file uses `600` permissions.

### Diagnostic log

Technical drag and restore diagnostics are stored at `~/Library/Logs/TWMA.log`. The log does not include window titles, user-assigned workspace names, or URLs. To tie a running app to an exact build, the log records the app version, build number, bundle identifier, source commit ID, and clean or dirty source state. Restore and performance diagnostics may include a random restore-session ID, trigger, display and restored or missing window counts, an app bundle identifier, candidate-window count, and processing duration.

When the log exceeds 512 KiB, it is rotated to one `TWMA.previous.log` file instead of accumulating indefinitely. Both files use `600` permissions, limiting access to the current user.

### Information not collected or transmitted

- Accounts, passwords, key input other than shortcut combinations explicitly saved by the user, or screen images
- Document contents inside windows
- Analytics, advertising, or tracking data
- Window, workspace, or diagnostic-log data uploaded to cloud or third-party servers

TWMA uses macOS Accessibility permission to inspect, move, and resize ordinary app windows. Only ordinary windows visible on the active desktop are captured in a workspace.

### Update checks

Public builds check for new versions by default. Automatic checks can be disabled, and a manual check can be started, in General settings. The app requests `https://raw.githubusercontent.com/4celain/twma-releases/main/appcast.xml`. GitHub may process the connecting IP address, standard HTTP information, and a User-Agent in the form `TWMA/app-version Sparkle/framework-version`. TWMA disables system-profile transmission and does not append window, workspace, diagnostic-log, device-model, memory, or language information to the feed URL.

When an update is available, the signed DMG is downloaded from GitHub Releases. Installation and relaunch proceed only after user approval. TWMA does not use silent installation or delta updates. Development-bundle builds do not start the update service.

When the user selects a bug-report or support link in the app, the macOS default browser opens the configured external HTTPS page. The app does not attach or automatically send window or workspace data to that page.

### User-exported backups

A JSON backup created in Apps & Data includes saved workspace names, modified dates, optional shortcuts and app, window, display, layout, and zone information; language, preview, drag-to-snap, Dock reservation, window gaps, automatic restore, and automatic update-check preferences; default and per-display layouts, pinned menu layouts, the global shortcuts for slots 1–4, selected automatic-restore workspaces; app placement modes; and backup-format information. It excludes Accessibility permission, login-item state or approval, diagnostic logs, first-run acknowledgement, settings-window position, and the selected section.

Backups are written only to the location selected by the user and are not uploaded or synchronized automatically. TWMA applies `600` permissions where the destination supports file permissions. Imported profile or backup files larger than 8 MiB are rejected without replacing current data.

Workspaces can be deleted individually in the app. To remove all workspace records, quit TWMA and delete `profiles-v1.json`. This does not delete separately stored preferences, app-behavior policies, or diagnostic logs.

TWMA is publicly operated as `4celain`. Support and bug reports are handled through [TWMA Issues](https://github.com/4celain/twma-releases/issues/new?template=bug_report.yml).
