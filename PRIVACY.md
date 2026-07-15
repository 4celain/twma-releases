# TWMA 개인정보 처리 안내

TWMA는 창 배치 복원에 필요한 정보를 이 Mac 안에만 저장합니다.

## 로컬에 저장하는 정보

- 작업공간 이름, 앱 이름과 bundle identifier
- 작업공간을 만들거나 업데이트할 때 활성 데스크탑에 보이는 일반 창의 제목·종류·순서와 배치
- 모니터 식별자·논리 해상도·배치·배율·회전 정보
- 작업공간 단축키와 앱별 배치·재시도 설정
- 언어, 레이아웃, 드래그 배치, Dock 공간, 창 간격, 자동 복원과 로그인 실행 설정

작업공간은 `~/Library/Application Support/UniMonWorkspace/profiles-v1.json`에 저장됩니다. 앱 설정과 앱 호환성 정책은 이 Mac의 TWMA 환경설정에 저장됩니다.

## 진단 로그

TWMA는 복원 실패를 확인하기 위한 기술 로그를 `~/Library/Logs/UniMonWorkspace.log`에 저장합니다. 로그에는 창 제목, 작업공간 이름, URL과 문서 내용이 들어가지 않습니다. 앱 버전·빌드·bundle identifier, 무작위 복원 세션 ID, 성공·실패 창 수, 대상 앱의 bundle identifier와 처리 시간이 기록될 수 있습니다.

로그는 512KB에서 이전 로그 한 개로 교체되며, 현재 사용자만 읽을 수 있는 권한을 사용합니다.

## 수집하거나 전송하지 않는 정보

- 계정, 비밀번호, 화면 이미지와 창 안의 문서 내용
- 분석·광고·추적 데이터
- 클라우드 또는 제3자 서버로 자동 전송되는 작업공간 데이터

TWMA는 창을 읽고 이동하기 위해 macOS 손쉬운 사용 권한을 사용합니다. 버그 제보 링크를 누르면 기본 브라우저가 GitHub를 열지만, 앱이 로그나 작업공간 데이터를 자동 첨부하지 않습니다.

사용자가 내보낸 JSON 백업은 선택한 위치에만 저장되며 자동 업로드되지 않습니다. 작업공간은 앱에서 개별 삭제할 수 있고, 전체 기록은 앱을 종료한 뒤 `profiles-v1.json`을 삭제해 제거할 수 있습니다.

공개 운영 표기는 `4celain`이며, 문의와 버그 제보는 [TWMA Issues](https://github.com/4celain/twma-releases/issues/new?template=bug_report.yml)에서 받습니다.

---

<a id="english"></a>

# TWMA Privacy Notice

TWMA stores the information required to restore window layouts only on this Mac.

## Information stored locally

- Workspace names, app names, and bundle identifiers
- Titles, roles, ordering, and placement of ordinary windows visible on the active desktop when a workspace is created or updated
- Display identifiers, logical resolutions, arrangement, scale, and rotation
- Workspace shortcuts and per-app placement or retry preferences
- Language, layouts, drag snapping, Dock reservation, window gaps, automatic restore, and launch-at-login preferences

Workspace data is stored at `~/Library/Application Support/UniMonWorkspace/profiles-v1.json`. Other preferences and app-behavior policies are stored in this Mac's TWMA preferences.

## Diagnostic log

TWMA stores technical restore diagnostics at `~/Library/Logs/UniMonWorkspace.log`. The log excludes window titles, workspace names, URLs, and document contents. It may include app version and build, bundle identifier, a random restore-session ID, restored or missing window counts, target app bundle identifiers, and processing durations.

The log rotates at 512 KB and retains one previous file with permissions limited to the current user.

## Information not collected or transmitted

- Accounts, passwords, screen images, or document contents
- Analytics, advertising, or tracking data
- Workspace data automatically uploaded to cloud or third-party servers

TWMA uses macOS Accessibility permission to inspect and move windows. Selecting the bug-report link opens GitHub in the default browser, but TWMA does not automatically attach logs or workspace data.

Exported JSON backups are written only to the location selected by the user and are not uploaded automatically. Workspaces can be deleted individually in the app. All workspace records can be removed by quitting TWMA and deleting `profiles-v1.json`.

TWMA is publicly operated as `4celain`. Support and bug reports are handled through [TWMA Issues](https://github.com/4celain/twma-releases/issues/new?template=bug_report.yml).
