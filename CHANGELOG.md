# Change Log

All notable changes to the "chooseyourdestiny-highlighter" extension will be documented in this file.

Check [Keep a Changelog](http://keepachangelog.com/) for recommendations on how to structure this file.

## [Unreleased]

### Added
- Pushing a `vX.Y.Z` tag also publishes the extension on Open VSX, with trusted publishing (OIDC, no stored token)
- Highlighting for `INCLUDE LIB "file.cyd"` (includes a library from the library folders), and an `include lib` snippet with the bundled libraries

### Changed
- The `$cyd` problem matcher reads the compiler's new message format, with the place first and the path relative to the project (`ERROR [PARSER] dir/my game.cyd:12:5: ...`): it opens included files in other folders and paths with spaces, and takes the column too. The README's build task compiles the project open as the workspace

## [2.6.1] - 2026-10-31

### Changed
- README: removed the known issue about strings containing `]]`. From ChooseYourDestiny 1.6.6 the compiler does not accept `]]` inside a string either, so the compiler and the highlighter agree

## [2.6.0] - 2026-10-31

### Added
- Highlighting for strings in code (`"HI"`), used in `DATA`, `DIM` initialisers and `LET`/`SET`. A string ends on its own line and never spans a `]]`, so an unclosed `"` does not swallow the end of the code block or the text after it
- Highlighting for the range operator `..` (`{ 1..8 }`, `'A'..'Z'`)
- `ASM` blocks: `CYD_SYSCALL` as a resident service and the `SVC_*` service numbers as injected constants
- The `$cyd` problem matcher also reports compiler warnings (`WARNING [...]: ... file.cyd:line`) as warnings
- Extension icon, dark gallery banner and keywords for the VS Code Marketplace
- The extension is published on the VS Code Marketplace: pushing a `vX.Y.Z` tag publishes it with trusted publishing (OIDC, no stored token)

### Changed
- `@vscode/vsce` 4.1, which needs Node 22; both release workflows use Node 22
- README: Marketplace installation, release procedure, and the keyword and snippet lists brought up to date

## [2.5.0] - 2026-07-05

### Added
- Highlighting for the multi-branch: `SELECT` / `CASE` / `ENDSELECT` (conditional scope)
- Highlighting for `ENUM` and the `REPEAT` list operator (declaration scope) and `SWAP` (assignment scope)
- Highlighting for character literals `'A'` (`constant.character`)
- Snippets `select`, `enum` and `swap`

## [2.4.0] - 2026-07-05

### Added
- Highlighting for the counted loop: `FOR` / `NEXT` / `STEP` (loop control scope)
- Highlighting for the wide-constant markers `WORD` / `DWORD` (declaration scope), used in `DATA`, `DIM` initialisers and `LET`/`SET`
- Snippets `for` (`FOR ... NEXT`), `forstep` (`FOR ... STEP ... NEXT`) and `wide` (`LET v = WORD/DWORD ...`)

## [2.3.0] - 2026-07-05

### Added
- Highlighting for the immutable data stream: `DATA` (declaration), `READ` / `RESTORE` (statements) and the `DATAEND()` built-in function
- Snippets `data` (a `DATA` statement) and `readloop` (`RESTORE` + `WHILE (DATAEND() = 0) ... WEND` read loop)

## [2.2.0] - 2026-07-04

### Added
- Highlighting for the inline assembler: `ASM name [EXPORTS ...] [USES ...] ... ENDASM` blocks, with the body scoped as embedded assembler (`;` comments, `$`/`0x`/`%` numbers, and — when a Z80 grammar is installed — full `source.asm.z80` highlighting)
- Dedicated scopes inside `ASM` blocks for the resident services (`CYD_PEEK`, `CYD_POKE`, `CYD_ARR_MAP`, `CYD_ARR_FLUSH`, `CYD_CALL`) and the compiler-injected ABI symbols (`FLAGS`, `SCREEN_BUFFER_PXL/ATT`, `VIDEO_PXL/ATT`, `ARR_<name>`/`_LEN`/`_BANK`, `RT_<name>`)
- Snippets for inline assembly: `asm` (inline routine), `asmexports` (multi-entry block) and `cydcall` (cross-block call via `USES`/`CYD_CALL`)

## [2.1.1] - 2026-07-03

### Added
- Highlighting for native routines: `IMPORT name FROM "file.asm"` and `CALL name`, with dedicated scopes for the keywords, the routine name and the assembler-file path
- Code snippets for common CYD constructs (`IF`/`ELSEIF`, `WHILE`/`WEND`, `DO`/`UNTIL`, `OPTION GOTO`/`GOSUB`, menus, `DECLARE`, `DIM`, `INCLUDE`, `IMPORT`/`CALL`, subroutines, code blocks and comments)
- A `cyd` problem matcher (`$cyd`) that parses the compiler's `ERROR [...]: ... file.cyd:line` messages, so a build task can surface compiler errors in the editor's Problems panel

## [2.1.0] - 2026-03-21

### Added
- Explicit `INCLUDE "file.cyd"` highlighting inside `[[ ... ]]` code blocks with dedicated scopes for the keyword and include path

### Fixed
- Kept `INCLUDE` scoped to code sections only, matching the compiler and preprocessor rules

## [2.0.0] - 2026-02-19

### Added
- Categorized keywords into semantic groups (flow control, declarations, assignments, conditionals, loops, options/menu, display, color, sound, I/O) with distinct TextMate scopes for better theme support
- Numeric literal highlighting: decimal, hexadecimal (`0xFF`), and binary (`0b1010`)
- Built-in function highlighting when followed by parentheses (e.g., `INKEY()`, `RANDOM()`, `XPOS()`, `LASTPOS()`)
- Variable reference highlighting for `@var` syntax with separate scope for `@` punctuation
- Compound assignment operators `+=` and `-=`
- Shift operators `<<` and `>>`
- Code folding support for `[[ ]]` blocks
- Curly braces `{}` and parentheses `()` to bracket pairs

### Fixed
- `POSX`/`POSY` renamed to `XPOS`/`YPOS` to match the actual compiler lexer
- Missing keywords added: `ISDISK`, `KEMPSTON`, `DO`, `UNTIL`, `DECLARE`, `AS`, `SET`, `TO`
- Typo in package description: "suit" → "suite"

### Changed
- Short labels (`#MyLabel`) now use `entity.name.label.cyd` scope instead of generic `variable.other.cyd`
- Label declarations (`LABEL MyLabel`) now properly scope the label name as `entity.name.label.cyd`
- Code block delimiters `[[ ]]` now use `punctuation.definition.block` scopes
- The entire grammar structure has been reorganized for clarity and maintainability

## [1.0.0]

- Initial release
