# Repository Guidelines

## Project Structure & Module Organization
- Cargo workspace with core crates in `crates/`: `snxcore` (VPN engine, IPC, networking) and `i18n` (localization assets and helpers).
- Applications live in `apps/`: `snx-rs` (standalone/command-mode service), `snxctl` (control CLI talking over the socket), and `snx-rs-gui` (GTK4 tray UI). Packaging/service files reside in `package/`, and platform notes in `nixos.md` and `options.md`.
- Tests sit next to the code they cover (`mod tests { .. }`); add broader integration/UI cases under each app’s `tests/` directory.

## Build, Test, and Development Commands
- `cargo fmt` formats the workspace (120-column width via `rustfmt.toml`).
- `cargo clippy --workspace --all-targets --all-features -D warnings` lints; address or justify diagnostics.
- `cargo test --workspace` runs the suite; narrow scope with `-p snxcore` or `-p snxctl` during iteration.
- `cargo build --release -p snx-rs` builds the CLI/daemon; add `-p snx-rs-gui` for the GTK frontend. Use `RUSTFLAGS="-C target-cpu=native"` only for local perf checks.

## Coding Style & Naming Conventions
- Rust 2024 edition; keep modules small and domain-focused (core logic in `crates/snxcore`, UI-only code in apps).
- Prefer early returns and `?` for error propagation; avoid `unwrap` outside tests.
- Logging uses `tracing`; avoid `println!` and include meaningful context in spans/events.
- File/module names stay `snake_case`; types `PascalCase`; constants `SCREAMING_SNAKE_CASE`.

## Testing Guidelines
- Add unit tests near implementations; mock IPC and network boundaries when feasible.
- For behavioral changes, add integration coverage in the relevant app (`apps/snxctl/tests`, `apps/snx-rs-gui/tests`, etc.).
- Cover auth flows, tunnel negotiation, and error paths; add a regression test for every bug fix where practical.
- Run `cargo fmt`, `cargo clippy`, and `cargo test --workspace` before opening a PR.

## Commit & Pull Request Guidelines
- Commit messages: present tense, concise summary (e.g., `Add IPSec reconnect backoff`); keep commits focused.
- PRs should describe user-facing impact (flags, env vars, UI), testing performed, and linked issues. Include screenshots for GUI changes and note any installer/service updates (`package/`).
- Maintainers expect lint/format/test clean; call out skipped checks explicitly if unavoidable.

## Security & Configuration Tips
- Never commit certificates, private keys, or real VPN endpoints; use placeholders in examples.
- Redact secrets from logs; prefer configurable paths over hardcoded ones when touching options in `options.md`.
- Keep secure defaults (TLS verification on, least privilege) when adding new settings and update docs accordingly.

## Localization & Assets
- Translatable strings live in `crates/i18n`; keep English source concise and neutral.
- New locales go under `crates/i18n/assets/<locale>`; ensure both CLI and GUI surfaces pull strings through the existing helper APIs.
