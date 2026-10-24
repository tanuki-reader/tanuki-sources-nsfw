# tanuki-sources-nsfw — Claude Code Context

Adult-only (`nsfw: true`) WASM sources for Tanuki. Everything about how a source works, the rules, the
commands and the published format is in **`tanuki-sources/CLAUDE.md`** (the submodule); read it first.
This repo only differs in:

- **Layout:** `sources/<crate>/` and `bundles.toml` here; `tanuki-sources/` is a submodule supplying the SDK
  (`source-api`, path dep `../../tanuki-sources/source-api`) and `xtask`. Never edit inside the submodule
  from here; change `tanuki-sources` itself and bump the pointer.
- **Build:** `cargo run --manifest-path tanuki-sources/xtask/Cargo.toml -- build --root . --out out`.
  `rust-toolchain.toml` must stay identical to the submodule's (reproducible bytes).
- **Signing:** its own key, the `TANUKI_SIGNING_KEY` secret on this repo (Keychain backup
  "tanuki-sources-nsfw signing key"). Don't read, print or move it. The app doesn't pin it.
- **Publishing:** push to `main` → `publish.yml` → orphan `repo` branch → GitHub Pages
  (`https://tanuki-reader.github.io/tanuki-sources-nsfw/`). Never rewrite the `repo` branch by hand.

Current sources: `hipercool` (pt-BR, tRPC behind a session cookie the guest mints itself).
