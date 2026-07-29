# Pinman Changelog

<!--
## [Unreleased]

  Append a bullet here as each user-visible change lands — not at release time.
  At the cut, rename this heading to "## [2.0.<YYMMDD>] — Beta · <YYYY-MM-DD>",
  start a fresh empty [Unreleased] above it, and copy the section into
  release-notes/pinman-beta.md as that build's "What's new".


### Added

### Changed

### Fixed

-->

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

