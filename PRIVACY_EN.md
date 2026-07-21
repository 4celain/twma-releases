# TWMA Privacy Notice

TWMA stores the information required to restore window layouts only on this Mac.

## Information stored locally

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

## Diagnostic log

Technical drag and restore diagnostics are stored at `~/Library/Logs/TWMA.log`. The log does not include window titles, user-assigned workspace names, or URLs. To tie a running app to an exact build, the log records the app version, build number, bundle identifier, source commit ID, and clean or dirty source state. Restore and performance diagnostics may include a random restore-session ID, trigger, display and restored or missing window counts, an app bundle identifier, candidate-window count, and processing duration.

When the log exceeds 512 KiB, it is rotated to one `TWMA.previous.log` file instead of accumulating indefinitely. Both files use `600` permissions, limiting access to the current user.

## Information not collected or transmitted

- Accounts, passwords, key input other than shortcut combinations explicitly saved by the user, or screen images
- Document contents inside windows
- Analytics, advertising, or tracking data
- Window, workspace, or diagnostic-log data uploaded to cloud or third-party servers

TWMA uses macOS Accessibility permission to inspect, move, and resize ordinary app windows. Only ordinary windows visible on the active desktop are captured in a workspace.

## Update checks

Public builds check for new versions by default. Automatic checks can be disabled, and a manual check can be started, in General settings. The app requests `https://raw.githubusercontent.com/4celain/twma-releases/main/appcast.xml`. GitHub may process the connecting IP address, standard HTTP information, and a User-Agent in the form `TWMA/app-version Sparkle/framework-version`. TWMA disables system-profile transmission and does not append window, workspace, diagnostic-log, device-model, memory, or language information to the feed URL.

When an update is available, the signed DMG is downloaded from GitHub Releases. Installation and relaunch proceed only after user approval. TWMA does not use silent installation or delta updates. Development-bundle builds do not start the update service.

When the user selects a bug-report or support link in the app, the macOS default browser opens the configured external HTTPS page. The app does not attach or automatically send window or workspace data to that page.

## User-exported backups

A JSON backup created in Apps & Data includes saved workspace names, modified dates, optional shortcuts and app, window, display, layout, and zone information; language, preview, drag-to-snap, Dock reservation, window gaps, automatic restore, and automatic update-check preferences; default and per-display layouts, pinned menu layouts, the global shortcuts for slots 1–4, selected automatic-restore workspaces; app placement modes; and backup-format information. It excludes Accessibility permission, login-item state or approval, diagnostic logs, first-run acknowledgement, settings-window position, and the selected section.

Backups are written only to the location selected by the user and are not uploaded or synchronized automatically. TWMA applies `600` permissions where the destination supports file permissions. Imported profile or backup files larger than 8 MiB are rejected without replacing current data.

Workspaces can be deleted individually in the app. To remove all workspace records, quit TWMA and delete `profiles-v1.json`. This does not delete separately stored preferences, app-behavior policies, or diagnostic logs.

TWMA is publicly operated as `4celain`. Support and bug reports are handled through [TWMA Issues](https://github.com/4celain/twma-releases/issues/new?template=bug_report.yml).
