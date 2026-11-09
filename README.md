# CEM — Claude Environment Manager (backup, restore and migration of your Claude Code environment)

![Licence](https://img.shields.io/badge/licence-PolyForm%20Strict%201.0.0-orange)
![Platform](https://img.shields.io/badge/platform-Windows%2010%2F11-blue)
![Use](https://img.shields.io/badge/use-non--commercial-lightgrey)

**CEM** (Claude Environment Manager) is a desktop application and a command line for people who use
**Claude Code** and want to **keep, restore, organise and carry to another computer** their own environment:
settings, skills, agents, MCP servers, `CLAUDE.md` files, prompts and templates. It finds everything on its
own, shows what is duplicated, broken or oversized, and packs the environment into a `.cem` file (with
integrity checks and optional encryption) so you can reinstall it in a few clicks. Everything is **local**:
nothing leaves your machine.

CEM **never** modifies, intercepts or reverse-engineers Claude Code or any Anthropic software: it only reads
and writes documented local files that belong to you, and it changes something only when you tell it to
(create a backup, restore, apply a fix).

This repository is CEM's **distribution page**: it holds the installation guide, the licence and the
installer (the **Releases** tab). The source code is not published: what you download is the **already-built
application**.

## Who it is for

People who use Claude Code day to day — researchers, developers, anyone who changes computers or keeps several
environments — and who want a safe way to back up and migrate, without redoing everything by hand.

## What you get

- **Dashboard**: the state of the environment, counts of skills, agents, MCPs and profiles, size on disk and
  warnings.
- **Scanner and diagnostics**: read-only discovery of every artefact; orphan references, broken MCPs,
  duplicates and files that weigh too much on the context; "Resolver problemas" proposes one fix per finding
  and you accept or ignore each one, with an automatic backup.
- **Backup and restore** in `.cem`: manifest, checksums, selective restore and optional AES-256-GCM
  encryption.
- **Token usage**: real consumption per session and project over 24 h, 3, 7 and 30 days, read from the local
  transcripts, with suggestions for improvement.
- **Server inventory** (read-only): CPU, disks, RAM, NVIDIA GPU (including VRAM that spills into RAM), conda,
  WSL, Docker, installed programs and bottleneck warnings.
- **Profiles**, MCP managers, skills, agents and markdown, history and optional git synchronisation.
- **CLI** `cem`: `scan`, `doctor`, `fix`, `backup`, `restore`, `verify`, `profiles`, `tokens`, `usage`,
  `mcp`, `history`, `sync` and others.

## Installation (summary)

All you need: **Windows 10/11 64-bit** and about 400 MB of free disk space. Nothing else — no Node.js, no
building, no internet connection during installation, no administrator rights.

1. From **Releases**, download `install_CEM-<version>.exe` and, to verify it, the `.sha256`.
2. Check the file: `Get-FileHash .\install_CEM-<version>.exe -Algorithm SHA256` must match the `.sha256`.
3. Double-click the installer. Windows will warn you that the **publisher is unknown** — the installer is not
   code-signed, which is exactly why the checksum exists: **More info → Run anyway**.
4. Read the licence and accept it; change the folder if you want. The installer creates the **Claude
   Environment Manager** shortcut on your Desktop and in the Start menu, and associates `.cem` files with CEM.
5. Open CEM from the shortcut. On first launch it scans your environment (read-only) and shows the Dashboard.

Full walkthrough, the SmartScreen warning, what is written where, how to uninstall and common problems:
[INSTALL.md](INSTALL.md).

### Command line (optional)

The CLI ships separately, because it needs **Node.js 20 or newer**. Download `cem-cli-<version>.tgz` from
**Releases** and install it with `npm install -g .\cem-cli-<version>.tgz`; then run `cem --help`. It also
works on macOS and Linux.

> Parts of the interface, and some of the diagnostic messages, are in Portuguese.

## Setting up and using

- CEM starts by only **looking** at your environment (read-only). Nothing is deleted automatically.
- To back up: the **Backup** section → choose the destination folder → (optionally) tick encryption and set a
  password → **Create backup**. To restore: the **Restore** section → choose the `.cem` → review → restore.
  Without the password, an encrypted `.cem` cannot be recovered.
- Preferences (theme, backup defaults, privacy) live in **Settings**.
- **Updates**: CEM can check for them itself. In **Settings** press *Check for updates* at any time, or turn
  on the automatic check — it is **off by default**. CEM never downloads or installs anything on its own: it
  tells you a version is available, you press *Download*, and then *Restart and install*. Before downloading,
  it creates a `.cem` backup of your environment, so you can go back. You can also skip all of that and just
  run the newer installer from **Releases**.

## Licence

**PolyForm Strict 1.0.0** ([LICENSE](LICENSE)) — a licence to **use**: you may download and use CEM free of
charge for **non-commercial** purposes (research, teaching, personal use, not-for-profit institutions and
public bodies). You may **not** redistribute copies, modify it or create derivative works, nor use CEM in
commercial activity or sell it. For any other use, contact the author. Computer program protected by Brazilian
Law 9.609/98, with a sole author.

Required Notice: Copyright Luiz Dione Barbosa De-Melo (https://github.com/luizdione/Platform_CEM)

This licence applies from version 1.5.0 onwards. Versions up to 1.4.0 were released earlier under the MIT
License and remain under it. The third-party components bundled in the application (Electron, React and the
other dependencies) have their own licences.

## Author

Luiz Dione Barbosa De-Melo — developer and sole rights holder of CEM. Questions, bug reports and requests for
uses outside the licence: open an *issue* in this repository.
