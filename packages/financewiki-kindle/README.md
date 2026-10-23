# FinanceWiki Kindle — pending KPM publication

- Package ID: `financewiki-kindle`
- Candidate version: `1.0.0`
- Target platform: `kindlehf`
- Source data contract: `financewiki-park/financewiki-private@main` + `viewer-index.json`

The candidate is a read-only Kindle cache viewer. On the first successful sync it downloads every indexed Markdown document. On later app launches it compares the canonical document hashes and downloads only new or changed documents; when GitHub or Wi-Fi is unavailable it opens the last completed local SQLite cache. It intentionally excludes graph, editing, commit, and push functionality.

No KPM manifest entry or artifact is published yet. The hub treats package/version artifact bytes as immutable. Before registering the artifact, a real Kindle must verify KPM install/uninstall, HTTPS curl, first full sync with a read-only PAT, changed-document delta sync, offline reopening, and launcher/home-screen restoration.

Build provenance and SHA-256 are retained in the local FinanceWiki Kindle worktree pending that device test.