<!--
  GitHub release notes body for a Pinman 2 beta installer release.
  Used as: gh release create v2.0.<YYMMDD> --notes-file release-notes/pinman-2-beta.md --prerelease
  Edit the version/date and the highlights each release, then publish.
  This file holds the CURRENT build's body; it's rewritten each cut. The running
  history lives in CHANGELOG.md and on the GitHub Releases page (each tag keeps its own).
  BETA 1 = a "what's in the box" overview (below). From beta 2 on, replace the
  "Highlights" section with a short "What's new" delta (added / changed / fixed).
  During the CLOSED beta this release carries NO downloadable asset — the installer
  is emailed to accepted testers as a private OneDrive link. Do not paste that link here.
-->

**Pinman 2 — Beta (2.0.YYMMDD)**

Welcome to the first closed-beta build of Pinman 2. Pinman captures, compares, and
manages the files and settings that configure a Windows machine — so you can see what
changed, test alternatives, and get back to a setup that works.

This build is distributed to accepted testers by a private download link sent to you
by email — there is no public installer download yet.

Not a tester? **[Apply to the beta →](https://pinmantech.com/beta)**

### Highlights

- **Track your setup** — capture the files, registry keys, and Windows settings that
  make up a working machine, and browse them in the Explorer.
- **See what changed** — checkpoints and comparisons show drift down to the
  individual setting.
- **Profiles** — collect settings into a Profile, apply it, and undo the last apply;
  guided steps handle changes Pinman can't make directly.
- **Savepoints & backups** — archive a capture to a safe copy.
- **Operator & Technician Modes** — remote controls for everyday use, full authoring
  when you need it; control the machine from any phone or browser on your network.
- **Journal, Kits, CLI & API** — dated notes tied to your changes, installable
  configuration packages, and everything scriptable from the command line.

See what's planned next in the **[roadmap](https://github.com/linojon/pinman/blob/master/ROADMAP.md)**.

### Install (quick start)

1. Download `Pinman-2-Setup-<version>.exe` from the link in your acceptance email.
2. Run it and follow the setup prompts. (Access from other machines on your network is
   an opt-in step during setup; local use needs nothing extra.)
3. When setup finishes, open the app and complete the Getting Started tutorial.

If Windows SmartScreen warns "Windows protected your PC", click **More info → Run
anyway** — the beta installer isn't code-signed yet, so this appears until it builds
download reputation.

### Verify your download

Match the SHA-256 in your email against the file:
`Get-FileHash .\Pinman-2-Setup-*.exe -Algorithm SHA256`.

### Requirements

- Windows 10 or 11 (64-bit)

### Support

Found a bug? **[Open an issue](https://github.com/linojon/pinman/issues/new/choose)** —
this tracker is public, so keep private details out and email them to
<jonathan@pinmantech.com> referencing your issue number. See
[SUPPORT.md](https://github.com/linojon/pinman/blob/master/SUPPORT.md).
