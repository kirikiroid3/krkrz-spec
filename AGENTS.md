# Agent Guide: krkrz-spec

This repository is an mdbook specifying the behavior of Kirikiri Z (krkrz).
The spec drives a cross-platform Rust rewrite. Agents analyze the C++ source
and write spec chapters.

## Where things are

| Path              | What                                                      |
| ----------------- | --------------------------------------------------------- |
| `krkrz/`          | **Reference source** (git submodule, read-only)           |
| `src/`            | Book chapters (Markdown)                                  |
| `src/SUMMARY.md`  | Table of contents; planned chapters are drafts `- [X]()`  |
| `src/conventions.md` | Writing rules every chapter MUST follow                |
| `book.toml`       | mdbook config                                             |
| `book/`           | Build output (ignored)                                    |

## Reference source

- Upstream: <https://github.com/kirikiroid3/krkrz>, pinned at the submodule
  commit. Check it with `git submodule status krkrz`.
- If `krkrz/` is empty, run `git submodule update --init krkrz`. Do **not**
  use `--recursive`: the nested `external/oniguruma` submodule is third-party
  code outside this spec's scope and uses an SSH URL.
- Treat `krkrz/` as read-only. Never edit, commit inside, or bump it as a
  side effect of writing spec text; bumping the pin is a deliberate,
  separate change.
- Layout: see `src/introduction.md`. Most subsystems are split into
  `FooIntf.*` (portable logic, TJS-facing classes) and `win32/FooImpl.*`
  (Windows backend). Comments are frequently in Japanese.

## Writing spec chapters

1. Read `src/conventions.md` first.
2. Pick a draft entry in `src/SUMMARY.md`, create `src/<area>/<topic>.md`, and
   replace `()` with the file path.
3. Cite source as `krkrz/<path>` plus symbol; mark anything not read directly
   from code as **Inferred**, **Unverified**, or **Open question**.
4. Build with `mdbook build`; it MUST succeed with no warnings about missing
   files. Preview with `mdbook serve`.
