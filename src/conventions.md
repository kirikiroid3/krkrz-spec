# Writing Conventions

Rules for every chapter of this book. They exist so that chapters written by
different agents stay consistent, verifiable, and usable as an implementation
reference.

## Normative language

Use the RFC 2119 keywords (**MUST**, **SHOULD**, **MAY**, …) for requirements on
an implementation. Plain prose is descriptive.

## Source citations

Every behavioral claim must be traceable to the reference source.

- Cite with a path relative to the repository root and the symbol, e.g.
  `krkrz/base/XP3Archive.cpp` — `tTVPXP3Archive::tTVPXP3Archive`.
- Line numbers are optional; when given, they refer to the pinned submodule
  commit and use the form `krkrz/base/XP3Archive.cpp:120-185`.
- Begin each chapter with a **Sources** list of the files it was derived from.

## Certainty

Mark anything not read directly from the code:

- **Inferred:** behavior deduced but not confirmed in source.
- **Unverified:** claims about real games or the original Kirikiri 2 that were
  not checked.
- **Open question:** unresolved points, so a later pass can pick them up.

## Platform specifics

Describe portable semantics first. Put Win32-only behavior (window messages,
DirectShow, registry, etc.) in a clearly labelled subsection, stating what the
cross-platform implementation must emulate and what it may drop.

## Quirks

When the original behaves surprisingly or incorrectly, document the actual
behavior under a **Quirk** note and say whether compatibility likely requires
reproducing it.

## Chapter lifecycle

Planned chapters appear in `SUMMARY.md` as drafts (`- [Title]()`). To write
one, create the Markdown file under `src/`, link it in `SUMMARY.md`, and run
`mdbook build` — the book is configured with `create-missing = false`, so broken
links fail the build.
