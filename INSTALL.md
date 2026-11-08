# Installing CEM on your machine

CEM (Claude Environment Manager) handles the **backup, restore, organisation and migration** of your Claude
Code environment. The installer checks the prerequisites, downloads the dependencies, builds the desktop
application and the `cem` command line and, if you want, creates a shortcut. Everything stays inside the
package folder.

> Licence: **PolyForm Strict 1.0.0** — you may download and use CEM for **non-commercial** purposes (personal,
> academic, institutional). You may **not** redistribute copies, modify it or use it commercially. Full text in
> `LICENSE`; program protected by Brazilian Law 9.609/98. The installer asks you to accept before installing.

> The installer console is in Portuguese. The prompts you need are quoted below.

## Prerequisites (you install these)

| What | What for | Where |
|---|---|---|
| Windows 10/11 64-bit | the installer is PowerShell | — |
| **Node.js 20 or newer** (LTS release) | to build and run the app and the CLI | https://nodejs.org |
| **pnpm 10 or newer** (or `corepack`, which ships with Node up to version 24) | to install the dependencies | `npm install -g pnpm` |
| An internet connection during installation | downloads the dependencies and the Electron runtime (~100 MB) | — |
| Disk space: about 1 GB free | `node_modules` takes ~660 MB once installed | — |

CEM does not require Claude Code to be installed in order to run; it only reads Claude Code's files if they
exist.

## Step by step

1. Download the package `CEM-<version>-instalador.zip` (and the `.sha256`, if you want to verify it) from the
   *Releases* page of https://github.com/luizdione/Platform_CEM.
2. (Optional) Verify the file in PowerShell and compare it with the contents of the `.sha256`:
   `Get-FileHash .\CEM-<version>-instalador.zip -Algorithm SHA256`
3. Extract it into a **short path**, for example `C:\CEM` (the folder path must be at most 120 characters:
   Windows does not run programs under paths longer than 260 characters and the build would fail; also avoid
   folders synchronised by OneDrive). Inside the extracted folder you will find `CEM-<version>\`.
4. Double-click **`Instalar-CEM.bat`** (inside `CEM-<version>\`). A console window opens and:
   1. shows the licence summary and asks you to accept — type **S** to accept;
   2. checks Node.js (≥ 20) and pnpm (≥ 10, or falls back to corepack);
   3. installs the dependencies (`pnpm install --frozen-lockfile`);
   4. builds the packages and the CLI (`pnpm build`) and the desktop app;
   5. confirms the CLI answers with the package version;
   6. asks whether you want the **Claude Environment Manager (CEM)** shortcut on your Desktop.
5. Open CEM from the shortcut or, in the package folder:
   `apps\desktop\node_modules\electron\dist\electron.exe apps\desktop`
   On first launch it scans your environment (read-only) and shows the Dashboard.

To test it with no questions and no shortcut: `Instalar-CEM.bat -AutoTeste`.

## What the installer writes (and nothing else)

| Where | What |
|---|---|
| `<package folder>\node_modules\` and `apps\*\node_modules\` | the dependencies (including the Electron runtime) |
| `<package folder>\apps\desktop\out\` and `...\dist\` | the built app and CLI |
| `Desktop\Claude Environment Manager (CEM).lnk` | the shortcut, only if you accept it |
| pnpm / corepack cache | only pnpm's own download cache, if it is used through corepack |

It does not change the `PATH`, the Windows registry or any environment variable. To remove it, delete the
package folder and the shortcut.

## Using it

- **Application**: Dashboard, Scanner, Diagnostics, Server inventory, Token analysis and usage, MCP / Skills /
  Agents / Markdown, Profiles, Backup, Restore, History and Synchronisation. Preferences in *Settings*.
- **Command line**, in the package folder: `node apps\cli\dist\index.js --help`, for example
  `node apps\cli\dist\index.js scan`, `... doctor`, `... backup`, `... verify <file.cem>`.
- **Backup**: the app shows the path, the size and the number of files in the `.cem` it created. Tick
  AES-256-GCM encryption and set a password if the environment holds secrets; without the password there is no
  way to recover the file.
- **Updating**: download the new `.zip`, extract it into a new folder and run the installer again. Your `.cem`
  files and your preferences live outside the package folder and are not lost.

## Other systems

The `.bat` installer is for Windows only. On macOS or Linux, for personal use under the same licence, inside
the extracted folder with Node.js ≥ 20 and pnpm ≥ 10:

```bash
pnpm install --frozen-lockfile
pnpm build
pnpm --filter @cem/desktop build
node apps/cli/dist/index.js --help
```

## Common problems

- **"Node.js não encontrado" / "Node.js ... é antigo"** (not found / too old): install the LTS release from
  https://nodejs.org and open a new console before running the installer again.
- **"pnpm não encontrado"** (not found): run `npm install -g pnpm` in a new console (or enable corepack) and
  try again.
- **"A pasta do pacote tem caminho longo demais"** (package path too long): extract into a short path, such as
  `C:\CEM`.
- **"A execução de scripts foi desabilitada"** (script execution disabled): the `.bat` already passes
  `-ExecutionPolicy Bypass`; if you run the `.ps1` by hand, use
  `powershell -ExecutionPolicy Bypass -File instalador\Instalar-CEM.ps1`.
- **Electron download fails** (corporate network, proxy, antivirus): run the installer again on a network
  without blocking; it is safe to repeat.
- **Windows SmartScreen or your antivirus warns about the `.bat`**: the file is plain text and can be read
  before running; check the `.sha256` of the `.zip`.
- **Something stopped halfway**: run `Instalar-CEM.bat` again; it is safe to repeat.
