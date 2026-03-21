# Change Log

All notable changes to the "chooseyourdestiny-highlighter" extension will be documented in this file.

Check [Keep a Changelog](http://keepachangelog.com/) for recommendations on how to structure this file.

<<<<<<< HEAD
## [2.1.0] - 2026-03-21

### Added
- Explicit `INCLUDE "file.cyd"` highlighting inside `[[ ... ]]` code blocks with dedicated scopes for the keyword and include path

### Fixed
- Kept `INCLUDE` scoped to code sections only, matching the compiler and preprocessor rules

## [2.0.0] - 2026-02-19

### Added
=======
## [2.0.0] - 2026-02-19

### Added
>>>>>>> 50e2e8179fbc11063d429c34b66457cb84447b2d
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
