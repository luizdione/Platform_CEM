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
installable package (the **Releases** tab). The source code is maintained by the author and is not published
here.

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

Prerequisites you install yourself: Windows 10/11 64-bit, **Node.js 20 or newer** (https://nodejs.org) and an
internet connection during installation.

1. Download `CEM-<version>-instalador.zip` (and the `.sha256`, to verify it) from **Releases**.
2. Extract it into a **short path** of your own (for example `C:\CEM`) and double-click
   **`Instalar-CEM.bat`**.
3. Read the licence and type **S** to accept. The installer checks Node.js and pnpm, downloads the
   dependencies, builds the app and the CLI and, if you want, creates a desktop shortcut.
4. Open CEM from the shortcut or, in the package folder, with
   `apps\desktop\node_modules\electron\dist\electron.exe apps\desktop`.

Full walkthrough, what is written where, and common problems: [INSTALL.md](INSTALL.md).

> The installer console and parts of the interface are in Portuguese. The prompts you need are quoted above
> and in the guide.

## Setting up and using

- CEM starts by only **looking** at your environment (read-only). Nothing is deleted automatically.
- To back up: the **Backup** section → choose the destination folder → (optionally) tick encryption and set a
  password → **Create backup**. To restore: the **Restore** section → choose the `.cem` → review → restore.
  Without the password, an encrypted `.cem` cannot be recovered.
- Preferences (theme, backup defaults, privacy) live in **Settings**.
- From the command line, inside the installation folder: `node apps\cli\dist\index.js --help`.
- To update: download the new `.zip` from **Releases**, extract it into a new folder and run the installer
  again. There is no automatic update.

## Licence

**PolyForm Strict 1.0.0** ([LICENSE](LICENSE)) — a licence to **use**: you may download and use CEM free of
charge for **non-commercial** purposes (research, teaching, personal use, not-for-profit institutions and
public bodies). You may **not** redistribute copies, modify it or create derivative works, nor use CEM in
commercial activity or sell it. For any other use, contact the author. Computer program protected by Brazilian
Law 9.609/98, with a sole author.

Required Notice: Copyright Luiz Dione Barbosa De-Melo (https://github.com/luizdione/Platform_CEM)

This licence applies from version 1.5.0 onwards. Versions up to 1.4.0 were released earlier under the MIT
License and remain under it. The third-party components the installer downloads (Electron, React and the other
npm dependencies) have their own licences and are not redistributed here.

## Author

Luiz Dione Barbosa De-Melo — developer and sole rights holder of CEM. Questions, bug reports and requests for
uses outside the licence: open an *issue* in this repository.
