<!--
  GitHub release notes body for a Pinman 2 beta installer release.
  Used as: gh release create v2.0.<YYMMDD> --notes-file release-notes/pinman-2-beta.md --prerelease
  Edit the version/date and the "What's new" bullets each release, then publish.
  During the CLOSED beta this release carries NO downloadable asset — the installer
  is emailed to accepted testers as a private OneDrive link. Do not paste that link here.
-->

**Pinman 2 — Beta (2.0.YYMMDD)**

Pinman 2 is in **closed beta**. This build is distributed to accepted testers by a
private download link sent to you by email — there is no public installer download yet.

Not a tester? **[Apply to the beta →](https://pinmantech.com/beta)**

### What's new

- _(summarize notable changes since the last beta build)_

### Install (quick start)

1. Download the zip from the link in your acceptance email and unzip it.
2. Run `install-pinman.bat` (or `install-pinman.ps1 -RunInit`).
3. Follow the prompts, then open the app and complete the Getting Started tutorial.

If Windows SmartScreen warns "Windows protected your PC", click **More info → Run
anyway** — this appears for installers that aren't yet widely downloaded.

### Verify your download

Match the SHA-256 in your email against the file:
`Get-FileHash .\Pinman-2-*.zip -Algorithm SHA256`.

### Requirements

- Windows 10 or 11 (64-bit)

### Support

Found a bug? **[Open an issue](https://github.com/linojon/pinman/issues/new/choose)** —
this tracker is public, so keep private details out and email them to
<jonathan@pinmantech.com> referencing your issue number. See
[SUPPORT.md](https://github.com/linojon/pinman/blob/master/SUPPORT.md).
