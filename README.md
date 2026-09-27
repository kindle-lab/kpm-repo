# Kindle KPM Repository Hub

Unified public KPM distribution hub for the Kindle packages maintained by [kindle-lab](https://github.com/kindle-lab).

**Status:** design stage · 2026-09-27

## Purpose

kpm-repo will become the canonical public entry point for installing and updating the Kindle package set. It will expose one stable KPM manifest and a predictable artifact layout while the application repositories remain the source of code, tests, and build workflows.

Planned canonical manifest URL:

https://raw.githubusercontent.com/kindle-lab/kpm-repo/main/manifest.json

## Package registry

| Package ID | Source repository | Current role |
| --- | --- | --- |
| `ktm` | [kindle-lab/ktm](https://github.com/kindle-lab/ktm) | Telegram bridge for Kindle |
| `korean-ime-probe` | [kindle-lab/kindle-korean-ime](https://github.com/kindle-lab/kindle-korean-ime) | Read-only compatibility probe |
| `korean-ime` | [kindle-lab/kindle-korean-ime](https://github.com/kindle-lab/kindle-korean-ime) | Korean IME package |
| `bluetooth-keymap-toggle` | [kindle-lab/kbt](https://github.com/kindle-lab/kbt) | Bluetooth HID and key-mapping toggle |

Package IDs and published versions are compatibility identifiers. Once published, an artifact path and checksum must not be silently repointed to different bytes.

## Ownership and delivery model

- Application repositories own source code, tests, platform builds, and release provenance.
- `kpm-repo` owns the public registry, package metadata, checksums, and the stable KPM-facing layout.
- The first implementation should mirror verified package artifacts into this repository and use relative URLs from `manifest.json`. This avoids making Kindle clients depend on several repository namespaces.
- A later optimization may use release assets directly, but only after the KPM parser and update behavior are verified on a real device.

Target layout:

```text
manifest.json
packages/
  ktm/artifacts/
  korean-ime-probe/artifacts/
  korean-ime/artifacts/
  bluetooth-keymap-toggle/artifacts/
checksums/
  SHA256SUMS
```

## Migration plan

1. Create and validate the hub manifest without changing the three application repositories.
2. Import only verified artifacts and record SHA-256 checksums.
3. Add a hub workflow that validates manifest/package agreement, archive contents, supported platforms, and checksum reproducibility.
4. Test the new hub with KPM add-repo, update, install, and uninstall flows on supported Kindle targets.
5. Update user-facing installation instructions to the canonical hub URL.
6. Keep the legacy [financewiki-park/k](https://github.com/financewiki-park/k) repository as a compatibility bridge. It is not part of this migration and must remain available.

## Namespace follow-up

The repositories were transferred without source edits. Before the first hub publication, review and explicitly decide how to handle the remaining historical `financewiki-park` references in package author metadata and the old `ktm` v0.1.0 release note. This is a planned follow-up, not an automatic rewrite.

## Acceptance checklist for implementation

- [ ] KPM manifest parses as the intended manifest version.
- [ ] Every package ID has exactly one artifact entry and checksum.
- [ ] Artifact URLs resolve from the new hub namespace.
- [ ] Package versions and supported platforms match the source repositories.
- [ ] A failed or mismatched artifact cannot be published.
- [ ] Legacy `financewiki-park/k` remains unchanged and reachable.
- [ ] Real-device install/update/uninstall smoke tests pass before announcing the hub.
