# ChooseYourDestiny Syntax Highlighter

Syntax highlighting for [ChooseYourDestiny](https://github.com/cronomantic/ChooseYourDestiny) — a CYOA (Choose Your Own Adventure) creation suite for the ZX Spectrum.

## Features

- Full syntax highlighting for `.cyd` files
- Distinguishes between **printable text** (outside `[[ ]]`) and **code blocks** (inside `[[ ]]`)
- Keywords organized by category with distinct colors:
  - **Flow control**: `GOTO`, `GOSUB`, `CALL`, `RETURN`, `END`, `LABEL`, `READ`, `RESTORE`
  - **Declarations**: `DECLARE`, `AS`, `CONST`, `DIM`, `DATA`, `ENUM`, `WORD`, `DWORD`, `REPEAT`, `IMPORT`, `FROM`, `ASM`, `ENDASM`, `EXPORTS`, `USES`
  - **Assignments**: `SET`, `TO`, `LET`, `SWAP`
  - **Conditionals**: `IF`, `THEN`, `ELSE`, `ELSEIF`, `ENDIF`, `SELECT`, `CASE`, `ENDSELECT`
  - **Loops**: `WHILE`, `WEND`, `DO`, `UNTIL`, `FOR`, `NEXT`, `STEP`
  - **Options/Menus**: `OPTION`, `CHOOSE`, `MENUCONFIG`, `CLEAROPTIONS`
  - **Display**: `PRINT`, `CLEAR`, `CENTER`, `AT`, `PICTURE`, `DISPLAY`, `WINDOW`, `BLIT`, etc.
  - **Colors**: `INK`, `PAPER`, `BORDER`, `BRIGHT`, `FLASH`, `FADEOUT`, `FILLATTR`, etc.
  - **Sound**: `SFX`, `TRACK`, `PLAY`, `LOOP`
  - **I/O**: `LOAD`, `SAVE`, `RAMLOAD`, `RAMSAVE`
- Built-in functions: `INKEY()`, `RANDOM()`, `XPOS()`, `YPOS()`, `ISDISK()`, `KEMPSTON()`, `MIN()`, `MAX()`, `LASTPOS()`, `DATAEND()`, etc.
- Variable references with `@` prefix (`@myVar`, `@0`)
- Native routines: `IMPORT name FROM "file.asm"` and `CALL name` (keywords, routine name and assembler-file path highlighted)
- Inline assembler: `ASM name [EXPORTS ...] [USES ...] ... ENDASM` blocks, with the body scoped as embedded assembler (`;` comments, `$`/`0x`/`%` numbers, `source.asm.z80` when a Z80 grammar is installed) and dedicated scopes for the resident services (`CYD_PEEK`, `CYD_POKE`, `CYD_ARR_MAP`, `CYD_ARR_FLUSH`, `CYD_CALL`, `CYD_SYSCALL`) and injected ABI symbols (`FLAGS`, `SCREEN_BUFFER_*`, `VIDEO_*`, the `SVC_*` service numbers, `ARR_<name>`, `RT_<name>`)
- Short label syntax (`#MyLabel`)
- Block comments (`/* ... */`)
- Numeric literals: decimal, hexadecimal (`0xFF`), binary (`0b1010`), character (`'A'`)
- Strings (`"HI"`) in `DATA`, `DIM` initialisers and `LET`/`SET`, and the range operator (`{ 1..8 }`, `'A'..'Z'`)
- Operators: arithmetic, comparison, logical (`AND`, `OR`, `NOT`), bitwise (`&`, `|`, `!`), compound (`+=`, `-=`)
- Code folding on `[[ ]]` blocks
- Auto-closing of brackets and code blocks
- **Snippets** for common constructs (`if`, `ifelse`, `ifelseif`, `while`, `do`, `for`, `forstep`, `select`, `enum`, `swap`, `sub`, `optiongoto`, `optiongosub`, `menu`, `declare`, `dim`, `data`, `wide`, `readloop`, `include`, `import`, `call`, `asm`, `asmexports`, `cydcall`, `block`, `comment`)
- **Problem matcher** (`$cyd`) that turns compiler errors and warnings into entries in the Problems panel

## Installation

### From the Marketplace

In VSCode, go to Extensions (`Ctrl+Shift+X`), search for **ChooseYourDestiny** and click **Install**,
or open the [Marketplace page](https://marketplace.visualstudio.com/items?itemName=cronomantic.chooseyourdestiny-highlighter).
From the command line:

```bash
code --install-extension cronomantic.chooseyourdestiny-highlighter
```

VSCode then keeps the extension up to date by itself.

### From VSIX file

Download the file `chooseyourdestiny-highlighter-x.x.x.vsix` from [Releases](https://github.com/cronomantic/chooseyourdestiny-highlighter/releases).

In VSCode, go to Extensions (`Ctrl+Shift+X`), click the `...` menu, select **Install from VSIX...** and open the downloaded file.

### Manual installation

Download or clone this repository and copy the folder into:
- **Linux/macOS**: `~/.vscode/extensions/`
- **Windows**: `%USERPROFILE%\.vscode\extensions\`
- **Portable VSCode**: `data/extensions/` inside the VSCode folder

Restart VSCode after installation.

## Automated release (GitHub Actions)

### How to publish a new version

1. Update the version in `package.json` and `package-lock.json` (`npm version X.Y.Z --no-git-tag-version`
   does both) and add its entry to `CHANGELOG.md`; commit and push to `main`.
2. Push a tag `vX.Y.Z` equal to that version: `git tag v2.6.0 && git push origin v2.6.0`.
3. The `release-vsix.yml` workflow builds the VSIX, creates the GitHub release with it
   and publishes it to the VS Code Marketplace.

The tag must be exactly `v` + the version in `package.json`, or the workflow stops before
creating the release or publishing anything. The workflow can also be run by hand from the
Actions tab: it then uses `v` + the version in `package.json` as the tag.

Publishing uses Marketplace trusted publishing (`vsce publish --oidc`): no token is
stored in the repository. The `cronomantic` publisher must have a trusted publishing
policy for this repository and the `release-vsix.yml` workflow. Re-running the
workflow for a version already on the Marketplace does not fail.

Drafting a release by hand on GitHub still works: `auto-draft-release.yml` builds the
VSIX and attaches it to that release, but does not publish it to the Marketplace.

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
compiler's error and warning format (`ERROR [...]: ... file.cyd:line` and
`WARNING [...]: ... file.cyd:line`). Add a task to your
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
`ERROR [...]: ... file.cyd:line` or `WARNING [...]: ... file.cyd:line` printed by the
compiler becomes a clickable entry in the Problems panel, as an error or a warning.

## Language Reference

See the full CYD language manual at:
- [English Manual](https://github.com/cronomantic/ChooseYourDestiny/blob/main/MANUAL_en.md)
- [Manual en Español](https://github.com/cronomantic/ChooseYourDestiny/blob/main/MANUAL_es.md)

## Known Issues

- The compiler reports locations by file name only (`file.cyd:12`), so the `$cyd` problem
  matcher cannot open an included file that lives in another folder, nor a file whose name
  contains spaces.

## Release Notes

See [CHANGELOG.md](CHANGELOG.md).

---

