# ChooseYourDestiny Syntax Highlighter

Syntax highlighting for [ChooseYourDestiny](https://github.com/cronomantic/ChooseYourDestiny) — a CYOA (Choose Your Own Adventure) creation suite for the ZX Spectrum.

## Features

- Full syntax highlighting for `.cyd` files
- Distinguishes between **printable text** (outside `[[ ]]`) and **code blocks** (inside `[[ ]]`)
- Keywords organized by category with distinct colors:
  - **Flow control**: `GOTO`, `GOSUB`, `CALL`, `RETURN`, `END`, `LABEL`
  - **Declarations**: `DECLARE`, `AS`, `CONST`, `DIM`, `IMPORT`, `FROM`
  - **Assignments**: `SET`, `TO`, `LET`
  - **Conditionals**: `IF`, `THEN`, `ELSE`, `ELSEIF`, `ENDIF`
  - **Loops**: `WHILE`, `WEND`, `DO`, `UNTIL`
  - **Options/Menus**: `OPTION`, `CHOOSE`, `MENUCONFIG`, `CLEAROPTIONS`
  - **Display**: `PRINT`, `CLEAR`, `CENTER`, `AT`, `PICTURE`, `DISPLAY`, `WINDOW`, `BLIT`, etc.
  - **Colors**: `INK`, `PAPER`, `BORDER`, `BRIGHT`, `FLASH`, `FADEOUT`, `FILLATTR`, etc.
  - **Sound**: `SFX`, `TRACK`, `PLAY`, `LOOP`
  - **I/O**: `LOAD`, `SAVE`, `RAMLOAD`, `RAMSAVE`
- Built-in functions: `INKEY()`, `RANDOM()`, `XPOS()`, `YPOS()`, `ISDISK()`, `KEMPSTON()`, `MIN()`, `MAX()`, `LASTPOS()`, etc.
- Variable references with `@` prefix (`@myVar`, `@0`)
- Native routines: `IMPORT name FROM "file.asm"` and `CALL name` (keywords, routine name and assembler-file path highlighted)
- Short label syntax (`#MyLabel`)
- Block comments (`/* ... */`)
- Numeric literals: decimal, hexadecimal (`0xFF`), binary (`0b1010`)
- Operators: arithmetic, comparison, logical (`AND`, `OR`, `NOT`), bitwise (`&`, `|`, `!`), compound (`+=`, `-=`)
- Code folding on `[[ ]]` blocks
- Auto-closing of brackets and code blocks
- **Snippets** for common constructs (`if`, `ifelse`, `ifelseif`, `while`, `do`, `sub`, `optiongoto`, `optiongosub`, `menu`, `declare`, `dim`, `include`, `import`, `call`, `block`, `comment`)
- **Problem matcher** (`$cyd`) that turns compiler errors into entries in the Problems panel

## Installation

### From VSIX file

Download the file `chooseyourdestiny-highlighter-x.x.x.vsix` from [Releases](https://github.com/cronomantic/chooseyourdestiny-highlighter/releases).

In VSCode, go to Extensions (`Ctrl+Shift+X`), click the `...` menu, select **Install from VSIX...** and open the downloaded file.

### Manual installation

Download or clone this repository and copy the folder into:
- **Linux/macOS**: `~/.vscode/extensions/`
- **Windows**: `%USERPROFILE%\.vscode\extensions\`
- **Portable VSCode**: `data/extensions/` inside the VSCode folder

Restart VSCode after installation.

## Automated VSIX Release (GitHub Actions)

When you draft (or publish) a release on GitHub, the workflow at `.github/workflows/auto-draft-release.yml` automatically builds the VSIX and attaches it to that release.

### How to publish a new release

1. Update the version in `package.json`, commit and push to `main`.
2. On GitHub, go to **Releases → Draft a new release**.
3. Create a tag matching the version (e.g. `v2.1.0`), write release notes, and click **Publish release** (or save as draft).
4. GitHub Actions builds the VSIX and uploads it to the release automatically.

You can also trigger a release via tag push and the `release-vsix.yml` workflow (`git tag v2.1.0 && git push origin v2.1.0`), or manually from the Actions tab.

### Local VSIX build

- `npm ci`
- `npm run package`

This produces a file named `chooseyourdestiny-highlighter-<version>.vsix` in the repository root.

## Snippets

In a `.cyd` file, start typing a prefix (e.g. `if`, `while`, `menu`, `sub`) and
accept the completion to expand a template with tab stops. See the *Features* list
above for the full set of prefixes.

## Build task and error reporting

The extension contributes a problem matcher named `$cyd` that understands the
compiler's error format (`ERROR [...]: ... file.cyd:line`). Add a task to your
project's `.vscode/tasks.json` so that building surfaces errors directly in the
Problems panel (adjust the command to how you invoke the compiler):

```json
{
  "version": "2.0.0",
  "tasks": [
    {
      "label": "CYD: build",
      "type": "shell",
      "command": "make_adv",
      "args": ["48k", "${file}"],
      "group": { "kind": "build", "isDefault": true },
      "problemMatcher": "$cyd"
    }
  ]
}
```

Run it with **Terminal → Run Build Task** (`Ctrl+Shift+B`). Any
`ERROR [...]: ... file.cyd:line` printed by the compiler becomes a clickable entry
in the Problems panel.

## Language Reference

See the full CYD language manual at:
- [English Manual](https://github.com/cronomantic/ChooseYourDestiny/blob/main/MANUAL_en.md)
- [Manual en Español](https://github.com/cronomantic/ChooseYourDestiny/blob/main/MANUAL_es.md)

## Known Issues

None known yet.

## Release Notes

### 2.1.1
- Added highlighting for native routines (`IMPORT name FROM "file.asm"`, `CALL name`)
- Added code snippets for common CYD constructs
- Added the `$cyd` problem matcher so build tasks report compiler errors in the Problems panel

### 2.0.0
- Categorized keywords with distinct scopes for better theme support
- Added numeric literal, function, and variable reference highlighting
- Added code folding and improved bracket support
- Fixed keyword names to match the compiler (`XPOS`/`YPOS` instead of `POSX`/`POSY`)

### 1.0.0
- Initial release

---

