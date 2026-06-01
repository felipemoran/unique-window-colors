# Change Log
All notable changes to the "unique-window-colors" extension will be documented in this file.

Check [Keep a Changelog](http://keepachangelog.com/) for recommendations on how to structure this file.

## [Unreleased]
- Add `Window Colors: Move Colors to a Gitignored Workspace File` command, which stores window colors in a gitignored `.code-workspace` file so they stay out of a committed `.vscode/settings.json`. `Remove Colors` and the on-exit settings-file cleanup are now workspace-aware.
- Colors are no longer written automatically when opening a plain folder — this avoids modifying a committed `.vscode/settings.json`. Auto-apply (on open and on theme change) now runs only in workspace mode, where colors go to the gitignored workspace file. Use `Reset Colors` to apply colors manually in folder mode.
- Add `windowColors.autoOpenWorkspaceFile` (default `true`): opening a folder that contains a matching `.code-workspace` file reopens it as that workspace automatically.
- Add `windowColors.autoCreateWorkspaceFile` (default `true`): opening a single-folder repository root (containing `.git` or `.jj`) with no workspace file auto-creates a gitignored `<folder>.code-workspace` and reopens as that workspace. The ignore is written to the backing clone's `.git/info/exclude` before the file is created — correct for jj workspaces (where the opened folder has no `.git` of its own) and ordered so jj never tracks the file.
- Initial release