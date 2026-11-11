# Ghost Client

A small, non-commercial launcher for **Minecraft: Java Edition**. Ghost Client keeps your game setups in separate instances, installs mods from Modrinth, and launches your own copy of the game. It is a personal hobby project, written in Python with Tkinter.

> Ghost Client is **not** affiliated with, endorsed by, or sponsored by Mojang, Microsoft, Modrinth or Polyfrost. "Minecraft" is a trademark of Mojang Synergies AB. You need to own Minecraft: Java Edition to play online.

## Features

- **Instances:** separate folders for each setup, with their own mods, worlds, settings and RAM limits.
- **Fabric support:** pick a Minecraft version and Ghost Client installs Fabric for you.
- **Mod management:** browse and install mods from Modrinth, add your own files, and enable, disable or remove mods, resource packs and shader packs.
- **One-click setup:** choose a version and what you want (performance, quality of life, visuals, utilities) and Ghost Client creates the instance and installs matching mods.
- **Modpack import:** import `.mrpack` modpacks.
- **Performance options:** tuned Java arguments, lightweight FPS mods for new Fabric instances, and a launcher that lowers its own priority and memory use while the game runs. All of it can be turned off in Settings.
- **Game logs**, per-instance Java path, resolution and fullscreen options, and color themes.
- **Offline mode:** play singleplayer, LAN and offline-mode servers without an account.

## Microsoft sign-in and privacy

Signing in is optional. Here is exactly how it works:

- Ghost Client is a **public client** that uses the **OAuth 2.0 authorization code flow with PKCE**. It has no client secret.
- It opens the **official Microsoft sign-in page in your own browser**. Ghost Client never sees or stores your password.
- After you sign in, Microsoft redirects to `http://localhost:8765/callback`. Ghost Client briefly runs a local-only listener on that address to receive the sign-in result, then closes it.
- The sign-in result is exchanged for an Xbox / Minecraft access token so the game can start as you. Ghost Client uses it only for this.
- Your tokens are saved **only on your own computer**, in the `config.json` file in the Ghost Client data folder (`.mylauncher` in your user folder). The file is not encrypted, so treat it like a password and don't share it. **Sign out** removes the saved login.
- Ghost Client has **no server of its own**. It collects no analytics or telemetry, and sends no personal data anywhere.
- Each user registers **their own Azure app** and pastes its Application (client) ID into Ghost Client (see below). No shared client ID is bundled with the program.

### Which services does Ghost Client contact?

| Service | Why |
| --- | --- |
| Microsoft, Xbox and Minecraft services | sign-in and getting a Minecraft access token |
| Mojang's game and library download servers (through `minecraft-launcher-lib`) | downloading the game files |
| Fabric's metadata and maven servers | installing the Fabric loader |
| Modrinth API (`api.modrinth.com`) | searching, downloading and updating mods |

### Setting up Microsoft sign-in (optional)

1. Register an app in Microsoft Entra / Azure with account type **Personal Microsoft accounts only**.
2. Add the redirect URI `http://localhost:8765/callback` under the **Mobile and desktop applications** platform, and turn on **Allow public client flows**.
3. Copy the **Application (client) ID**.
4. In Ghost Client, open **Settings → Microsoft account → Setup guide → Enter client ID**.

New apps must be approved by Mojang before they can get Minecraft tokens. Until yours is approved, sign-in fails with "Invalid app registration" and offline mode still works.

## Running it

You need **Python 3** and **Java** (Java 21 for current Minecraft versions, Java 17 for 1.17 to 1.20.4).

```
pip install -U minecraft-launcher-lib
python mc_launcher.py
```

On Windows you can use `run_launcher.bat`. To build a standalone app, run `build_exe.bat`. It uses PyInstaller and puts the result in the `dist` folder.

Your instances, mods and settings are stored in the `.mylauncher` folder in your user folder, not inside the program.

## Credits

- [minecraft-launcher-lib](https://pypi.org/project/minecraft-launcher-lib/) for game installation and launching.
- [Modrinth](https://modrinth.com) and its public API for mods.
- [Fabric](https://fabricmc.net) for the mod loader.
- The Moderniz font, included under its own license (see `Font-LICENSE.txt`).

## Contact

Open an issue on this repository for bugs, questions or concerns.
