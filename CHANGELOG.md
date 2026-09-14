# Pinman Changelog

<!--
  This changelog is an end-user-facing account of each release, not a strict internal
  "done" list. Write in plain, approachable language and emphasize what users can do,
  what feels better or safer, and the direction Pinman is moving. Avoid or translate
  internal architecture, implementation mechanics, sprint management, test-board
  bookkeeping, and similar project vocabulary unless a user needs it to understand the
  change. Consolidate overlapping entries from git history and release plans rather than
  copying their raw task lists. It is fine to group work, summarize loosely, and take
  reasonable descriptive liberties; favor a useful, honest weathervane over exhaustive or
  contractual precision. Keep concrete commands, user-visible limitations, and other
  details that help someone use or evaluate the release.

  Append a bullet under [Unreleased] as each user-visible change lands — not at release
  time. At the cut, ./scripts/build/release_stamp renames that heading to
  "## [<version>] — <channel> · <date>", taken from the built installer's own identity,
  and opens a fresh [Unreleased] above it. Then copy the stamped section into
  release-notes/pinman-beta.md as that build's "What's new".
-->

## [Unreleased]

### Added

### Changed

### Fixed

## [2.0.260914] — Beta · 2026-09-14

This beta is largely about trust: keeping captures coherent as you explore, broaden, and refresh
them, and making Profile Apply safer when it writes settings back to your machine. Pinman now does
more checking before and after a write, refuses formats it cannot yet handle safely, and does a
better job of explaining read and write failures.

Operator Mode has also been rebuilt on Pinman 2 Profiles. It remains an optional, mobile-friendly
control panel for everyday workstation controls such as volume, brightness, messages, slideshows,
and power. This new foundation brings Operator controls into the same system as other Profiles and
moves Pinman closer to letting users build custom control panels of their own.

### Added

- **Operator Kit:** Add the rebuilt Operator controls to any project with
  `pinman kit import operator`.
- **Profile and Operator controls:** A new library of reusable UI controls lays the groundwork for
  customizable control panels built around Profiles.
- **REST settings:** Pinman can now track and apply settings exposed by REST APIs. Operator Mode
  uses this new capability for its controls.
- **Capture checks:** `pinman capture check` inspects a capture for errors and inconsistencies and
  reports their severity.
- Read failures now appear on the affected setting or container with an explanation.
- New file inspection commands — `pinman file list`, `pinman file show`, and
  `pinman file check` — make it easier to see what Pinman can safely read or write. Use
  `pinman file list -v --domain all` for the current support details.
- Added read and write support for more INI and XML variants, including XML files with comments,
  mixed markup, significant whitespace, and UTF-8 content.
- Added CSV file reading.
- Added `pinman --version`.

### Changed

- **Safer Profile Apply:** Pinman checks file support before writing, validates the result afterward,
  and rolls back the whole apply when a write fails.
- Enabling Operator Mode in UI Config now installs the Operator Kit when needed and restarts the
  Pinman services for you.
- UI configuration changes that need a service restart can now perform that restart for you.
- Explorer's expand, broaden, and refresh controls are clearer, including the distinction between
  an empty container and one that has not been scanned yet.
- Scan and discovery work has been streamlined for better performance and fewer duplicate results.
- The old Operator Actions and Scheduler pages are temporarily unavailable while they are rebuilt
  around Profiles.
- The Machine Windows Services tab is temporarily unavailable while its noisy capture behavior is
  being corrected.

### Fixed

- Captures now retain tracked files, folders, and registry keys that are currently absent when you
  broaden or refresh their parent container.
- Refreshing, broadening, or selectively updating a capture now preserves its scope and change
  history more reliably, including statuses, timestamps, counts, and fingerprints.
- Pinman now distinguishes more reliably between a deleted setting, a setting that is simply
  absent, and one that could not be read.
- Fixed several cases where a refreshed capture could disagree with a newly created capture of the
  same machine state.
- Registry scans now handle very large keys, including hive roots, more reliably, and registry
  reads are no longer accidentally skipped by an unrelated backup setting.
- Windows runtime setting failures are reported consistently instead of being mistaken for missing
  settings.
- File undo now refreshes the recorded machine state after restoring a file.
- Fixed encoding and byte-order-mark handling for screen-resolution configuration files.
- The welcome popup now shows a countdown before it closes automatically.
- Deleting a project now deletes its logs too.

### Status

Pytest: 7098/7098 tests pass
Vitest: 418/418 tests pass



## [2.0.260827] — Beta · 2026-08-27

This release does two things. It makes the Basics tutorial run the way it reads, and it lays the groundwork for a change in how Pinman models what a capture actually *covers*. In real use you broaden a container here, refresh the head there, apply a profile, broaden again, and the head ends up reaching different depths in different places. Pinman now records that coverage as part of the capture itself, in its database rather than only in your browser, so it survives a refresh and a restart. The surfaces that will *show* you a capture's coverage come next. A large equivalence harness — hundreds of scenarios across files, the registry, Windows settings, and bundles — exists to keep the model honest, and much of this release's work went into it.

### Added

- **Software inventory** now tracks versions. A scan reports what was found, what's gone, and what changed version since last time, and files the result in the Journal.
- Tutorial install now offers to open the guided walkthrough for you, rather than just naming the command that would.
- Pinman registers itself as a proper Windows app identity, so notifications and the taskbar show the "Pinman" icon.

### Changed

- Adopted the new flat Pinman logo across the product.
- UI polish: Explore toolbar and item-rows. Device role picker. 
- Installer and uninstaller improvements, including unattended installs.
- Tray improvements, including watchdog on the services it supervises.
- Basics tutorial guide (content version **1.0.2**) - clarified instructions and improved other prose and screenshots. 

### Fixed

- **The Basics tutorial's chapter 7 can be completed as written.** Turning a tracked Windows setting *off* is now noticed as the setting going away — in the registry and in Windows settings alike. Pinman used to see a value appear and never see it disappear, so the chapter's round trip never closed.
- Other miscellaneous fixes and improvements in core engine, CLI, and UI.

### Status

- pytest: 5446/5446 tests pass
- vitest: 374/374 tests pass

## [2.0.260817] — Beta · 2026-08-17

This release centers on the new Basics tutorial — the guided walkthrough of what Pinman does and why. Everything else in the product is here and meant to work.

Pinman currently works with INI and XML configuration files, plus the Windows registry, Windows and device settings, and plain files and directories. Point it at another format and it will tell you that type isn't supported yet, rather than do something half-right with your file. More formats land as the write-path harness proves each one.

### Added

- Profiles page table view

**Basics Tutorial**
- Added completed Basics tutorial, with full online and static guided documentation, CLI tutorial tools, fully tested.
- Install using `pinman tutorial install basics`, or the guided `pinman setup` command.

**File Format Support Harness**
- File format support harness in place, validating Pinman's read and write capability across 88 catalogued file variants over 450 test matrix cells. Variants cover CR/LF line endings, Unicode characters, key/value delimiters and more; operations cover read, create, update and delete.
- Unsupported cases raise a refusal rather than risking data corruption when writing your files. INI and XML variants are write-ready in this release; anything not yet hardened defaults to refused.
- Full test suite for each file format.
- New CLI commands `file support` and `file check` let you test your own files against Pinman's support matrix.


### Changed

- Polished some CLI outputs 
- Polished some UI labels and messages
- Improved server startup times and user feedback
- Further registry browsing and expand performance improvements
- Cleaned up API request logging

### Fixed

- Made CLI capture COM-safe for reading audio settings
- Fixed read of Windows settings (winrt) during profile drift detection
- Fixed timeout of extracted registry (winreg) hive file preload on discovery 
- Fixed timeout of expand very large containers
- Fixed discovery of items inside kit-adopted containers
- Fixed schema import of tracked paths for all item types
- Fixed for-block items not appearing in captures at tracked scope
- Fixed refresh accuracy for registry and Windows settings captures
- Fixed change rollup status on container items
- Fixed registry captures skipping unreadable keys instead of failing
- Fixed database busy errors during concurrent operations
- Fixed capture counts and labels in CLI output
- Tutorial restart no longer clears existing logs


### Status

- pytest: 5179/5179 tests pass
- vitest: 364/364 tests pass

---

## [2.0.260729] — Beta · 2026-07-29

_First posted build._ Highlights of what Pinman 2 can do today. Consider all features to be in active development and preliminary. 

### Added

- **Dashboaard** - overview of your PC health, settings drift, and prority actions. 

- **Journal** — keep dated notes as you work and modify your PC. Include a checkpoint, which logs specific changes to the machine, in your notes.

- **Captures** - capture the state of your machine at any moment in time, including the files, registry keys, and Windows settings. A Checkpoint is a capture of the state of your machine, for comparison. A Savepoint is a capture that also backs up the changed files.

- **Explore** - browse files and properties, with side-by-side compare of changes over time, across your system, down to individual settings. Drill into data files for specific properties.

- **Schema** - defines the scope of your captures to specific tracked files, properties, settings. Ability to broaden the scope of captures to explore and compare untracked items.

- **Profiles** - defines a target state of a specific set of properties on your computer. Collect changesets of properties into reusable, applyable profiles. Surgically apply a profile to restore a previous set. Undo last apply. Detect drift of the live system against each profiles' target settings.

- **Guided Mode** - profiles can write directly to your data files, system settings, and registry. Or you can author guided manual steps to walk users through changes Pinman can't make directly (work in progress).

- **Machine** - also track hardware devices, ports, and OS settings. Choose hardware devices to watch, track video and USB ports status. Detect tracked applications status and Windows system runtime settings.

- **Operator Mode** — bonus remote-control Operator Mode for machines in a public setting. From any phone or browser, control the volume, dim the displays, lock inputs, show slideshows and text overlays, reboot or shutdown the machine.

- **Localhost** - everything runs on the machine being tracked, not a cloud service, Internet not required. The browser based UI provides access across your LAN.

- **Kits** — install configuration packages (schema + profiles + guidance) prepared for a software ecosystem. Community authoring tools.

- **Interfaces** — browser based user interface (GUI), commandline terminal interface (CLI), REST API means everything is scriptable for humans and AI agents.

- **More** - other features include readonly-mode to protect and sandbox; switch between multiple projects; code signed installer/uninstaller; run Pinman services from system tray; Windows registry blackliset and whitelist; tag tracked items (zones); 

- **Tutorials** — ability to install a disposable sample project (`pinman tutorial install basics`) and follow the matching walkthrough in the online docs. (content still being written)

- **Online docs** - concepts, guides, and the full CLI reference at [pinmantech.com/docs](https://pinmantech.com/docs). The complete structure is listed, with each page marked *draft* or *soon* while the beta fills it in.

---
