# Installing CEM on your machine

CEM (Claude Environment Manager) handles the **backup, restore, organisation and migration** of your Claude
Code environment. What you download is a **Windows installer**: one file, a double-click, and you are using
it. No Node.js, nothing to build, and no internet connection needed while it installs.

> Licence: **PolyForm Strict 1.0.0** — you may download and use CEM for **non-commercial** purposes (personal,
> academic, institutional). You may **not** redistribute copies, modify it or use it commercially. Full text in
> `LICENSE`; program protected by Brazilian Law 9.609/98. The installer shows the licence and asks you to
> accept it before installing.

## Prerequisites

| What | What for |
|---|---|
| Windows 10 or 11, 64-bit | the application is built for that platform |
| About 400 MB of free disk space | the installed application |
| **Nothing else** | no Node.js, no pnpm, no building, no internet during installation |

You do not need administrator rights: the installation belongs to **your user account**, not to the whole
machine.

CEM does not require Claude Code to be installed in order to open; it only reads Claude Code's files if they
exist.

## Step by step

1. From the **Releases** tab of <https://github.com/luizdione/Platform_CEM>, download:
   - `install_CEM-<version>.exe` — the installer;
   - `install_CEM-<version>.exe.sha256` — the checksum (optional, but worth verifying).
2. **Check the file** before running it. In PowerShell, in the folder you downloaded to:

   ```powershell
   Get-FileHash .\install_CEM-<version>.exe -Algorithm SHA256
   ```

   The result must equal the contents of the `.sha256` file. If it differs, **do not run it**: download again.
3. Double-click `install_CEM-<version>.exe`.
4. **Windows will warn you that the publisher is unknown** — see the next section. That is expected.
5. The installer opens and:
   1. shows the licence and asks you to accept it — you must accept to continue;
   2. proposes an installation folder, which you can change;
   3. installs the application, creates the **Claude Environment Manager** shortcut on your Desktop and in the
      Start menu, and associates `.cem` files with CEM, so double-clicking a backup opens the program.
6. Open it from the shortcut. On first launch CEM scans your environment **read-only** and shows the Dashboard.

### The Windows warning (SmartScreen)

The installer **is not code-signed**, because a code-signing certificate is a paid product and CEM is
distributed by an individual author. So Windows shows *"Windows protected your PC"* / *"Publisher: unknown"*.
To continue: **More info → Run anyway**.

That warning says Windows does not recognise the publisher — not that the file has been altered. What proves
the file is the one the author published is the **SHA-256 checksum** from step 2. Verify it and, as far as the
integrity of the file goes, you have the same assurance a signature would give. Your antivirus may object for
the same reason; if it blocks the file, release it after you have checked the checksum.

## What the installer writes (and nothing else)

| Where | What |
|---|---|
| The installation folder you chose | the application |
| `Desktop\Claude Environment Manager.lnk` and the Start menu | the shortcuts |
| The user registry (`HKCU`) | the "Installed apps" entry, so you can uninstall, and the `.cem` association |
| The application data folder, in your account | your preferences (theme, backup defaults, privacy) |

It does not touch the `PATH`, does not write to `HKEY_LOCAL_MACHINE`, and installs no service and no scheduled
task.

## Uninstalling

**Windows Settings → Apps → Installed apps → Claude Environment Manager → Uninstall.** Your `.cem` files and
your preferences are **not** deleted: they live outside the installation folder, so you can reinstall or
update without losing anything. To remove the preferences as well, delete the application data folder after
uninstalling.

## Updating

Two ways, and both keep your preferences and your backups.

**From inside the application.** Open **Settings → Updates** and press *Check for updates*. There is also a
switch for checking automatically at launch, which is **off by default** — CEM does not phone home unless you
ask it to. When a newer version exists:

1. CEM tells you which version it found. Nothing is downloaded yet.
2. You press *Download*. **Before downloading, CEM creates a `.cem` backup of your environment**, so you can
   restore the previous state if the new version does not suit you. The download is verified against the
   checksum published with the release, and a failed check aborts the update.
3. You press *Restart and install*. CEM never installs on its own and never installs on quit.

**By hand.** Download `install_CEM-<new version>.exe` from the **Releases** tab, check the checksum and run
it. It updates the existing installation. Use this if your network blocks the check, or if you simply prefer
to decide when to look.

## The `cem` command line (optional)

Besides the application, CEM has a command line, delivered separately because it **needs Node.js**. From the
Releases tab, download `cem-cli-<version>.tgz` and install it:

```powershell
npm install -g .\cem-cli-<version>.tgz
```

This needs **Node.js 20 or newer** (<https://nodejs.org>). Then:

```powershell
cem --help
cem scan
cem doctor
cem backup
cem verify my-backup.cem
```

Available commands: `scan`, `doctor`, `fix`, `backup`, `export`, `restore`, `import`, `verify`, `profiles`,
`tokens`, `usage`, `mcp`, `managers`, `history` and `sync`. The same licence covers the CLI, and its text
travels inside the package.

## Using it

- **Application**: Dashboard, Scanner, Diagnostics, Server inventory, Token analysis and usage, MCP / Skills /
  Agents / Markdown, Profiles, Backup, Restore, History and Synchronisation. Preferences in *Settings*.
- **Backup**: the **Backup** section → choose the destination folder → (optionally) tick AES-256-GCM
  encryption and set a password → **Create backup**. The app shows the path, the size and the number of files
  in the `.cem` it created. **Without the password an encrypted `.cem` cannot be recovered** — keep it safe.
- **Restore**: the **Restore** section → choose the `.cem` → review what will be written → restore. You can
  restore only part of it, by artefact kind or file by file.
- CEM starts by only **looking** at your environment, read-only. Nothing is deleted automatically, and every
  fix proposed under "Resolver problemas" is accepted or ignored by you, with an automatic backup first.

> Parts of the interface, and some of the diagnostic messages, are in Portuguese.

## Other systems (macOS and Linux)

The ready-built delivery is Windows only. The command line above works on macOS and Linux with Node.js ≥ 20
(`npm install -g ./cem-cli-<version>.tgz`). For the desktop application on those systems, contact the author.

## Common problems

- **"Windows protected your PC" / "Publisher: unknown"**: expected — see the SmartScreen section above. Check
  the SHA-256 checksum and use **More info → Run anyway**.
- **The SHA-256 checksum does not match**: do not run the file. The download most likely came through
  incomplete; download it again.
- **Your antivirus deleted the installer**: check the checksum of the downloaded file and release it from the
  antivirus quarantine, or add an exception for your download folder.
- **"This app can't run on your PC"**: the installer is 64-bit; check under *Settings → System → About*
  whether your Windows is 64-bit.
- **The shortcut did not appear**: search for "Claude Environment Manager" in the Start menu. To pin it to the
  taskbar, right-click the Start menu entry → *Pin to taskbar*: no installer can do that on its own on
  Windows 10/11.
- **`cem` is not recognised after `npm install -g`**: open a new console, so it re-reads the `PATH`.
- **Something stopped halfway through the installation**: run the installer again; it is safe to repeat.
