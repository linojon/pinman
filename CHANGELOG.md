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

## [2.0.261115] — Beta · 2026-11-15

This beta makes Pinman substantially more authorable. Schema authors now have a complete
interactive CLI for building and validating schemas, while the UI gains a clearer common path for
tracking rules. Profiles can now be created, composed and maintained in a guided editor instead of
requiring direct source edits for ordinary work.

The rest of Pinman has caught up around those workflows. Explore, the Dashboard and Operator Mode
are easier to use; the online documentation now covers the principal Technician screens and core
concepts; and the capture engine stores and transfers less redundant item data without losing
comparison or failure detail.

> **Important:** Reset existing beta projects after installing this build. Beta 5 replaces
> Pinman's internal item-evidence storage without migrating projects from earlier beta builds, so
> reinstall or reseed disposable/tutorial projects and recreate other test projects before use.
> Custom Python Profiles must also move from `p.param(...)` to typed `p.input(...)` declarations,
> read values through `p.inputs.<name>`, and pass CLI values with `--input` instead of `--param`.

### Schema

Schema CLI
- Build a schema from a blank project with interactive CLI commands to inspect, add, edit, move and
  remove definitions. Commands support structured output, dry runs and confirmation for destructive
  changes, so advanced authoring no longer requires replacing an entire YAML file.
- Validate a schema or preview an import against an isolated copy of the active project. The preview
  reports definitions, declarations and ordering that would change without touching the live
  schema.
- Manage Zones, Software declarations and Device roles from the CLI, including reference-aware
  previews before a rename, replacement or deletion.
- Replacing a tutorial or disposable project's schema is safer: Pinman validates the new schema
  before removing the old project, and preserves a supported retry path if a later setup step fails.

Schema UI
- The Schema item dialog has a clearer Advanced section for constants and saved definitions.
- The UI can now add, edit and remove single-level matching rules for files, INI sections and XML
  elements, including the template item created by each rule.

### Profiles UI and scripts

- Create and edit Profiles in the UI, including metadata, literal targets and typed inputs such as
  choices. Targets can be selected from the live Head or a historical Capture.
- Organize Profile contents into settings that are always used and settings selected by a choice.
  A choice can also include another Profile, with its inputs mapped into the parent Profile.
- Compose reusable Profiles to run together, inspect the effective targets and resolve conflicting
  inputs before saving.
- Profile edit history keeps bounded source snapshots, with Undo Last Edit and restore for an
  earlier version.
- Profiles can be pinned to the Dashboard, and those pins persist between sessions.
- Large Profile libraries, editors and Preview/Apply reviews are more compact and responsive when a
  Profile contains dozens of inputs or targets.
- Profile status now refreshes correctly after the live Head changes, and editing a Profile rechecks
  only the affected status instead of leaving stale results.
- Zone selection, linked choice content and target grouping are more reliable and easier to
  understand across live and historical sources.
- An optional restricted mode for Profile scripts blocks unapproved Python while the Machine is
  read-only. Pinman shows why a script was blocked and lets a Technician grant full Python to one
  exact script version. This is a guard rail, not a security sandbox.

### Explore and Captures UI

- Explore's flat table now shows the items that actually match the current view without adding
  ancestor rows whose status came only from a matching child.
- Keyboard and row focus stay aligned when navigating, selecting items or switching between tree
  and table views.
- Item-type icons, expansion controls and column-resize handles are more consistent across Explore
  and the rest of the UI.
- Profile target views now group settings under recognizable containers, while Explore's Table view
  remains flat and change-focused.
- Stored capture evidence and Item API responses no longer repeat several derived representations,
  reducing database use and response size while preserving comparison, completeness and read-failure
  meaning.

### Dashboard, Operator and Journal UI

- The Technician Dashboard has clearer status blocks, quick actions and machine presentation, plus
  a machine-image picker whose selection is saved with that machine's identity.
- Operator controls use space more effectively on phones and narrow displays, with improved power,
  mode, message and color controls.
- Operators can add a note directly from the controls screen and review recent Operator notes
  without switching to the full Journal.
- Operator and Technician requests no longer interfere with each other's Profile data while both
  interfaces are in use.
- The welcome window can now be disabled from its own controls or the tray menu; the preference is
  retained for later launches and removed on uninstall.

### CLI and terminology

- Product language now uses **Software** consistently across schemas, Explore, the Software catalog,
  the API and the CLI. Catalog-wide status now says **Available** or **Unavailable** when Pinman is
  reporting whether it can find that Software.
- CLI object names, identifiers, option labels and help now follow a more consistent command
  structure. Registry search logic also uses the shared core implementation instead of a separate
  CLI-only path.

### Documentation

- New visual reference pages cover Dashboard, Explore, Captures, Schema, Profiles, the Profile
  editor, Journal, Machine, Services and Config, with layouts and controls shown at desktop and
  narrow widths.
- New and rewritten guides cover how Pinman works, core concepts, Captures, Profiles, schema
  authoring, supported file formats, Windows Registry and runtime settings, external Software, Kits
  and what Pinman will and will not change.

### Reliability

- Database upgrades now reconcile the independent Profile-script and item-evidence changes in this
  release instead of leaving competing migration heads.
- Profile authoring errors and blocked linked content remain visible in the library, status and
  preview paths instead of disappearing or failing later during Apply.

### Status

Pytest: 17,230/17,230 passed
Vitest: 1,284/1,284 tests pass

## [2.0.261031] — Beta · 2026-10-31

This beta introduces **Tracking from Scratch**, a guided tutorial for building a Pinman schema from a
blank project. It covers tracking whole files and individual settings, excluding unwanted files,
creating Captures, and reviewing changes in Explorer.

Blank projects can now be configured in the UI without starting from a prebuilt kit. You can add
and edit tracking for files, INI settings, directories, Registry values, and Windows settings.
Profiles can also update JSON, YAML, CSV, SQLite, PinMAME, and PinVol data in this release.

Explorer now shows when a comparison is incomplete because something could not be read or was not
fully scanned. Incomplete results are no longer presented as a confirmed match. This release also
improves the accuracy of Capture and Refresh, makes Profile Apply and Undo more reliable, and
better handles items that disappear and return.

> **Important:** Reset your projects after installing this build. Captures from earlier builds are
> not carried forward reliably, so start each project fresh.

### Added

- **Tracking from Scratch tutorial (1.0.0):** Start with a blank project and build a useful schema around
  the files, settings, and Windows configuration that matter. Install it with
  `pinman tutorial install tracking`, or choose it from guided setup.
- **Additional formats for Profile Apply:** Profiles can now update JSON, YAML, CSV, SQLite,
  PinMAME INI, and PinVol settings and tables. CSV and SQLite rows use declared identities so
  Pinman can verify and undo changes to the intended record.
- **Capture Details:** Explorer and the CLI now distinguish failed reads, incomplete scans, and
  missing reference evidence. Counts indicate whether they are exact (`N`), a known minimum
  (`N+`), or unknown (`?`). The Details panel explains unresolved items without silently scanning
  anything.
- **Show hidden:** When a folder scan leaves out Windows hidden or temporary items, Explorer shows
  how many were withheld and lets you include them for that folder until the next capture.

### Changed

- The System page now reads Monitoring values live. Discovered Windows settings also retain their
  catalog labels, descriptions, units, and read/write policy.
- **Tracking UI:** Improved the dialogs and controls for adding and editing tracked items.

### Fixed

- Captures preserve their selected scope, stored evidence, historical detail, and change counts
  more reliably through Refresh, local scans, missing-and-returning items, sparse history, and
  alternate-reference comparisons.
- Profile Apply can create a declared setting in a tracked file that has never appeared in a
  capture, verify it, and Undo it normally. Missing or unreadable targets still refuse safely.
- Explorer no longer loses restored settings during Broaden, invents removed settings below the
  recorded scope, or leaves stale rows and expansion state after a refresh or tracking change.
- Browsing untracked files no longer hashes their contents just to list them, avoiding unnecessary
  reads and access-denied warnings on locked files.
- Fixed several UI interaction problems, including first-click scan conflicts, current-row
  activation, realm-root expansion, narrow-layout status controls, and login-role timing.
- Live Windows Monitoring no longer serves stale capture values, loses concurrent extract updates,
  or lets a slow NVIDIA query hold up the Pinman service.

### Status

Pytest: 16,664/16,664 tests pass
Vitest: 1,128/1,128 tests pass

## [2.0.261016] — Beta · 2026-10-16

This beta brings **Restore**: you can now put files back the way a Savepoint recorded them, straight
from your capture history, without building a Profile first. Alongside it, Pinman is more careful
about every change it makes to your machine. When it won't write something, it now tells you why
and what you can do about it, before anything is touched, and you can tell it to make no file
changes at all until you've saved a backup.

Under the hood, the capture engine has had a large round of improvements: captures stay accurate as
you broaden and refresh them, Pinman is clearer about the difference between a setting that is
missing and one it simply couldn't read, and the writers for many file formats are now stricter
about preserving your files exactly as they were. The Journal, Operator Mode, and log files all
received attention too.

Watch the new **Pinman Basics walkthrough video** on YouTube: https://youtu.be/irBQdxMNfgA

### Added

- **Restore:** Put a Savepoint's files back on your machine, for the whole capture or just the
  items you choose. Use **Restore…** on a Savepoint in the capture history, or
  `pinman capture restore`. Add `--preview` to see what would change first.
- **Require a Savepoint:** A new setting in UI Config. When it's on, Pinman changes a file only if
  a Savepoint already holds that file as it is now; otherwise it asks you to take one first or to
  overwrite anyway.
- **Journal:** Notes now have a formatted editor, can be deleted, and can be filtered by where they
  came from.
- **Operator login** is enabled. Pinman now has two roles: Operator and Technician.
- **Log rotation:** Log files now roll over automatically, with configurable limits.
  `pinman log rotate` starts a fresh log on demand, and `pinman log list` shows the older ones.
- Tutorial commands in the CLI now show each tutorial's version number.

### Changed

- **Clear reasons when a write is refused:** If Pinman won't change a setting, it says why and what
  to do about it, the same way in the UI and the CLI, and before it writes anything.
- **Checkpoint is now the default capture** (settings granularity), instead of File Checkpoint.
- **Profiles:** Status, Preview, and Apply now agree with each other. A Profile can no longer show
  "In sync" while Apply refuses to run. Profiles also cope better with settings that can't be read
  and devices that are unavailable, and Undo now refreshes your capture correctly afterward.
- **Operator Mode** follows its on/off setting everywhere, and tells the operator when something
  will be refused or hasn't been picked up yet.
- **Safer file writes:** Writing settings back keeps each value's original type and preserves the
  rest of the file as it was, with more checking before and after each write across INI, XML,
  JSON, YAML, CSV, SQLite, PinMAME, and PinVol files. Formats that aren't yet approved for writing
  are still refused.
- **Upper and lower case** in registry keys and file settings is now handled the way each format
  expects.
- Paths and names containing special characters such as `*`, `/`, and `\` are now handled
  correctly.
- Explorer now shows absent items by default.
- The Explorer toolbar collapses gradually as the window gets narrower.
- The tray menu has been updated.
- Backup files are now named in a way that keeps working when a schema update or kit import adds
  locations to your tree.
- Pinman no longer lets two operations that change the same capture run over each other.

### Fixed

- Pinman now tells you when it couldn't read a setting (because it was unavailable or access was
  denied) instead of reporting it as missing or removed. This covers the registry, Windows
  settings, and REST services.
- Captures stay more accurate as you broaden, refresh, and narrow them, including values carried
  forward from earlier captures.
- Mapped and network drives are handled more reliably.
- Importing a kit whose locations overlap your existing tree now works correctly.
- Deleting a capture in the middle of a chain no longer breaks the backups that later captures rely
  on.
- Deleting a merged capture after a revert could destroy the only copy of its data. Fixed.
- Resuming a backup after cancelling it now keeps its backup location.
- `pinman capture delete --latest` deletes the right capture.
- `pinman winreg diff --live` no longer crashes, and registry keys Pinman isn't allowed to read are
  reported as unread.
- The installer no longer risks starting Pinman twice.
- Fixed a problem saving schema edits.

### Status

Pytest: 14,371/14,371 tests pass
Vitest: 726/726 tests pass

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
