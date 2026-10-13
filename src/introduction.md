# Introduction

This book specifies the observable behavior of **Kirikiri Z** (krkrz), the
visual-novel engine forked from Kirikiri 2. It is the reference for a
cross-platform reimplementation in Rust.

The specification is derived by reading the original C++ source, which is
vendored in this repository as the `krkrz/` git submodule
(<https://github.com/kirikiroid3/krkrz>). The submodule commit is the version
this book describes.

## Goals

- Describe **what** the engine does — script-visible APIs, file formats,
  rendering and timing semantics, error behavior — precisely enough that a new
  implementation can run existing games unchanged.
- Separate portable semantics from Win32 implementation details, so the Rust
  port can choose its own platform backends.
- Record quirks and bugs that games may depend on, rather than silently
  "fixing" them.

## Non-goals

- Documenting the C++ code structure for its own sake. Internal structure
  appears only where it explains behavior.
- Specifying third-party libraries (Oniguruma, libjpeg, FreeType, …). Reference
  their own documentation and specify only how krkrz uses them.

## Reading the source

The engine source is laid out by subsystem:

| Directory   | Contents                                                        |
| ----------- | --------------------------------------------------------------- |
| `tjs2/`     | TJS2 scripting language: lexer, compiler, VM, built-in classes  |
| `base/`     | System entry, storage, XP3 archives, text/binary streams, plugins |
| `environ/`  | Application lifecycle, main window, input, OS integration       |
| `visual/`   | Window, Layer, bitmaps, image loaders, `tvpgl` pixel kernels, transitions, fonts |
| `sound/`    | Wave playback, sound buffers, loop manager, phase vocoder       |
| `movie/`    | Video playback (DirectShow / Media Foundation)                  |
| `msg/`      | User-facing messages and localization tables                    |
| `utils/`    | Timers, threads, clipboard, CP932 tables, misc helpers          |
| `extension/`| Statically linked native classes registered at VM startup       |
| `external/` | Third-party code (not specified here)                           |
| `vcproj/`   | Visual Studio project, resources, string tables                 |

Most subsystems follow a naming split: `FooIntf.cpp/.h` holds the
platform-independent part and the TJS-facing class definition, while
`win32/FooImpl.cpp/.h` holds the Windows implementation. The `Intf` files are
usually the right starting point for specifying script-visible behavior.
