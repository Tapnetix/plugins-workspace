# RecapIt patch for tauri-plugin-updater 2.14.0

Base: `44293a5722efcaf27060504e63b17aeba721b40f` (`updater-v2.14.0`), package `plugins/updater`.

The package manifest is normalized from the crates.io 2.14.0 archive so Cargo resolves the same registry dependencies when this package is consumed from the plugins-workspace monorepo. The verified archive SHA-256 is `7259989d4fe11b2bf51f7d671642249b1837c4ae2da1430dc713ae38f98ceeec`.

RecapIt pins the Windows ZIP dependency to exact `zip = 9.0.5` and adds it as a dev dependency for host-independent tests. `src/updater.rs` factors the existing ZIP extraction and root-level `.exe`/`.msi` selection through `extract_zip_installer`, with tests for traversal, symlink, malformed archive, nested entry and installer selection. `src/error.rs` makes the ZIP error conversion available in test builds while retaining the production installer type's Windows-only configuration.

The patch does not change signature verification or public-key handling. The minisign verifier, configured pubkey flow, and verification-before-install path are unchanged from the 2.14.0 source.
