# ChooseYourDestiny Syntax Highlighter

Syntax highlighting for [ChooseYourDestiny](https://github.com/cronomantic/ChooseYourDestiny) — a CYOA (Choose Your Own Adventure) creation suite for the ZX Spectrum.

## Features

- Full syntax highlighting for `.cyd` files
- Distinguishes between **printable text** (outside `[[ ]]`) and **code blocks** (inside `[[ ]]`)
- Keywords organized by category with distinct colors:
  - **Flow control**: `GOTO`, `GOSUB`, `RETURN`, `END`, `LABEL`
  - **Declarations**: `DECLARE`, `AS`, `CONST`, `DIM`
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
- Short label syntax (`#MyLabel`)
- Block comments (`/* ... */`)
- Numeric literals: decimal, hexadecimal (`0xFF`), binary (`0b1010`)
- Operators: arithmetic, comparison, logical (`AND`, `OR`, `NOT`), bitwise (`&`, `|`, `!`), compound (`+=`, `-=`)
- Code folding on `[[ ]]` blocks
- Auto-closing of brackets and code blocks

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

This repository includes two release workflows:

### Auto-draft on version bump

Workflow: `.github/workflows/auto-draft-release.yml`

When you push to `main` with a changed version in `package.json`, a **draft** GitHub Release is automatically created with the VSIX attached. You can then review the draft and publish it from the GitHub Releases page.

### Tag-based release

Workflow: `.github/workflows/release-vsix.yml`

- Trigger on git tags like `v2.1.0`
- Manual trigger from the GitHub Actions tab (`workflow_dispatch`)
- Builds the VSIX using `vsce`
- Creates a published GitHub Release and uploads the generated `.vsix`

### How to publish a new release

**Option A — Auto-draft (recommended):**
1. Update the version in `package.json`.
2. Commit and push to `main`.
3. A draft release with the VSIX will appear in GitHub Releases — review and publish it.

**Option B — Tag-based:**
1. Update the version in `package.json`.
2. Commit and push to `main`.
3. Create and push a matching tag:
   - `git tag v<version>`
   - `git push origin v<version>`

The tag must match `package.json` exactly (for example: package version `2.1.0` requires tag `v2.1.0`).

### Local VSIX build

- `npm ci`
- `npm run package`

This produces a file named `chooseyourdestiny-highlighter-<version>.vsix` in the repository root.

## Language Reference

See the full CYD language manual at:
- [English Manual](https://github.com/cronomantic/ChooseYourDestiny/blob/main/MANUAL_en.md)
- [Manual en Español](https://github.com/cronomantic/ChooseYourDestiny/blob/main/MANUAL_es.md)

## Known Issues

None known yet.

## Release Notes

### 2.0.0
- Categorized keywords with distinct scopes for better theme support
- Added numeric literal, function, and variable reference highlighting
- Added code folding and improved bracket support
- Fixed keyword names to match the compiler (`XPOS`/`YPOS` instead of `POSX`/`POSY`)

### 1.0.0
- Initial release

---

