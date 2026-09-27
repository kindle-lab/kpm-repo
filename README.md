# Kindle KPM Repository Hub

Unified public KPM distribution hub for the Kindle packages maintained by [kindle-lab](https://github.com/kindle-lab).

**Status:** active hub structure · 2026-09-27

## Canonical install entry point

Use this manifest for new installations:

https://raw.githubusercontent.com/kindle-lab/kpm-repo/main/manifest.json

The application repositories remain the source of code, tests, build workflows, and release provenance. This repository owns the stable KPM-facing registry, mirrored package artifacts, and checksums.

## Package registry

| Package ID | Source repository | Current role |
| --- | --- | --- |
| `ktm` | [kindle-lab/ktm](https://github.com/kindle-lab/ktm) | Telegram bridge for Kindle |
| `korean-ime-probe` | [kindle-lab/kindle-korean-ime](https://github.com/kindle-lab/kindle-korean-ime) | Read-only compatibility probe |
| `korean-ime` | [kindle-lab/kindle-korean-ime](https://github.com/kindle-lab/kindle-korean-ime) | Korean IME package |
| `bluetooth-keymap-toggle` | [kindle-lab/kbt](https://github.com/kindle-lab/kbt) | Bluetooth HID and key-mapping toggle |

Package IDs and published versions are compatibility identifiers. Published artifact bytes must not be silently replaced under an existing version and path.

## Current layout

```text
manifest.json
packages/
  ktm/artifacts/
  korean-ime-probe/artifacts/
  korean-ime/artifacts/
  bluetooth-keymap-toggle/artifacts/
checksums/
  SHA256SUMS
.github/workflows/
  sync-artifacts.yml
```

The hub manifest uses relative artifact paths. The mirrored artifacts currently match the source repositories' Git blobs, and `checksums/SHA256SUMS` records their SHA-256 values.

## Synchronization

`.github/workflows/sync-artifacts.yml` downloads the current verified artifacts from the three source repositories, checks that every artifact path referenced by `manifest.json` exists, regenerates SHA-256 checksums, and commits synchronization changes when needed.

## Namespace migration

The active source repositories and current package metadata use the `kindle-lab` namespace. User-facing installation instructions point to this hub.

The legacy [financewiki-park/k](https://github.com/financewiki-park/k) repository remains available only as a compatibility bridge for previously configured Kindle clients. Do not delete or repurpose it while old installations may still reference it.

Historical release notes or immutable package archives may still contain the former namespace as provenance. Those historical records are not the canonical installation path.

## Migration status

- [x] Canonical hub manifest created.
- [x] Current package artifacts mirrored into the hub.
- [x] SHA-256 checksums recorded.
- [x] Hub synchronization workflow added.
- [x] Active package author metadata normalized to `kindle-lab`.
- [x] User-facing source-repository install instructions migrated to the canonical hub URL.
- [x] Legacy `financewiki-park/k` compatibility bridge kept reachable.
- [ ] Real-device add-repo/update/install/uninstall smoke test completed against the new hub on every supported Kindle target.

Until the final real-device smoke test is complete, keep the compatibility bridge available.
