# tanuki-sources-nsfw

Adult-only sources for [Tanuki](https://github.com/tanuki-reader/tanuki), kept out of the first-party
[`tanuki-sources`](https://github.com/tanuki-reader/tanuki-sources) repo. Same SDK, same build gate, same
repo format: `tanuki-sources` is a submodule here and supplies `source-api` and `xtask`.

Add it in the app (Settings → Sources → Add repo): `https://tanuki-reader.github.io/tanuki-sources-nsfw/`.
Its sources only show with "Show adult content" on.

```bash
git submodule update --init
cargo run --manifest-path tanuki-sources/xtask/Cargo.toml -- build --root . --out out
```

Writing a source, the rules and the repo format are all in `tanuki-sources` (its `README.md`, `CLAUDE.md`
and `docs/repo-format.md`). Differences here:

- Every source sets `nsfw: true` in `meta()`.
- Its own signing key: the `TANUKI_SIGNING_KEY` Actions secret on this repo, backed up in the maintainer's
  macOS Keychain as **"tanuki-sources-nsfw signing key"** (account `tanuki-reader`). The app does **not**
  pin it; users confirm its fingerprint on first add. Public key: `XN8n+ClEWdG5eukT4SlHX1lJaPxugayIXe2RyuDJJDg=`.
  To restore the secret:
  `security find-generic-password -a tanuki-reader -s "tanuki-sources-nsfw signing key" -w | gh secret set TANUKI_SIGNING_KEY -R tanuki-reader/tanuki-sources-nsfw`.
- Updating the SDK means bumping the `tanuki-sources` submodule. A wire or ABI change lands there first.
