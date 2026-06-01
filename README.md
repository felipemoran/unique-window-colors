> **Note:** This extension is currently under active development. A new version with additional features is in progress. 🚧

# Window Colors

Uniquely and automatically colors each VSCode window.

<img src="https://raw.githubusercontent.com/stuartcrobinson/unique-window-colors/master/img/live_dark_screenshot.png" alt="drawing" width="330"/> &nbsp;&nbsp;&nbsp;
<img src="https://raw.githubusercontent.com/stuartcrobinson/unique-window-colors/master/img/live_light_screenshot.png" alt="drawing" width="330"/>

## What it does

This extension gives each new VS Code window a unique color based on a hash of the root directory name when it is opened.  It does this by immediately writing three colors to the following settings in `.vscode/settings.json`:

```javascript
  "workbench.colorCustomizations": {
    "activityBar.background": "#13332E",
    "titleBar.activeBackground": "#19423B",
    "titleBar.activeForeground": "#F6FBFB"
  }
```

The extension deletes this file and folder each time the VS Code window is closed unless the colors have been modified or unless they contain any other settings.  

You can optionally set a single Base Color (see Window Colors settings) by hex code or css color name.  

## Usage with Git

To avoid checking `.vscode/settings.json` in to your remote repository without modifying `.gitignore`, you can either:

1. **locally:** add `.vscode/settings.json` to your project's `.git/info/exclude` file

    _or_

2.  **globally:** create and use a global `.gitignore_global` file like so:

    ```git config --global core.excludesfile ~/.gitignore_global```

## Keep colors out of a committed `settings.json`

If your project **commits** `.vscode/settings.json` (shared team settings), you may not want the generated window colors landing in it. VS Code can only render window tinting from a settings source it loads natively — `.vscode/settings.json`, your user settings, or a `.code-workspace` file — so the colors have to live in one of those. The `.code-workspace` option lets you keep them out of the committed file entirely.

Run **`Window Colors: Move Colors to a Gitignored Workspace File`** from the command palette. It will:

1. Create a `<folder>.code-workspace` file at your project root.
2. Move any existing window colors out of `.vscode/settings.json` and into that workspace file (leaving the committed file clean).
3. Add the workspace file to `.git/info/exclude` so it stays out of version control.
4. Offer to reopen the window using the workspace file.

Once the window is opened as a workspace, all window colors are written to the gitignored `.code-workspace` file instead of `.vscode/settings.json`. This is the same approach popularized by [Peacock](https://www.peacockcode.dev/guide/) for keeping personal colors out of shared settings.

By default (`windowColors.autoOpenWorkspaceFile`), opening a folder that already contains a matching `.code-workspace` file will reopen it as that workspace automatically, so you don't have to remember to open the workspace file directly. Set it to `false` to disable.

Also by default (`windowColors.autoCreateWorkspaceFile`), opening a single-folder **repository** root (a folder containing `.git` or `.jj`) that has no workspace file yet will create a gitignored `<folder>.code-workspace` and reopen as that workspace — so colors "just work" on any repo you open without ever touching a committed `settings.json`. The ignore entry is written to the backing clone's `.git/info/exclude`, which is resolved correctly for jj workspaces (whose opened folder has no `.git` of its own). Set it to `false` to disable. Both settings belong in your User Settings.

Note: in plain folder mode the extension no longer writes colors automatically — that would modify a committed `.vscode/settings.json`. Use `Window Colors: Reset Colors in This Window` to apply colors manually if you are not using a workspace file.

## Usage

Colors do not get overwritten.  This allows you to set custom colors (or a single Base Color).  To switch between light and dark themed colors, you must first delete the current colors from `.vscode/settings.json`.  You can do this manually or by or selecting `remove` in the extension's `Window Colors: Theme` settings and reloading the VS Code window.

<!-- <img src="https://github.com/stuartcrobinson/unique-window-colors/blob/master/img/settings.png?raw=true" alt="drawing" width="500"/> -->

## Notes

Workspaces containing multiple root folders are not currently supported by this extension.  The current behavior for multi-folder workspaces is that the workspace color settings will be set by the first window opened, and can be saved in the workspace's `<workspace-name>.code-workspace` configuration file.

When opening new VSCode windows, you might see the relevant theme colors change as they are updated to the new workspace.  This is normal:

<img src="https://github.com/stuartcrobinson/unique-window-colors/blob/master/img/colorflicker.gif?raw=true" alt="drawing" width="200"/>

## Credits

Hashing and color generation functions adapted from https://www.designedbyaturtle.co.uk/convert-string-to-hexidecimal-colour-with-javascript-vanilla/ by Edd Turtle.

Workspace root folder detection function adapted from https://itnext.io/how-to-make-a-visual-studio-code-extension-77085dce7d82 by Van Huynh.



<br><br>
<img style="vertical-align: middle;" src="https://raw.githubusercontent.com/stuartcrobinson/unique-window-colors/master/img/icon_602.png" width="60" />
