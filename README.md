# krkrz-spec

Behavioral specification of [Kirikiri Z](https://github.com/kirikiroid3/krkrz),
written as an [mdbook](https://rust-lang.github.io/mdBook/), as the reference
for a cross-platform Rust reimplementation.

```sh
git clone <this repo> && cd krkrz-spec
git submodule update --init krkrz   # not --recursive; see AGENTS.md
mdbook serve --open
```

The engine source is vendored at `krkrz/` as a git submodule. Contributors
(human or AI agent) should read [AGENTS.md](AGENTS.md) and
[src/conventions.md](src/conventions.md) before writing chapters.
