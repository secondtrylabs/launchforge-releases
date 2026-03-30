# LaunchForge

**Game Session Launcher & Process Manager**

LaunchForge is a Windows desktop application that manages your game sessions by automatically launching supporting applications alongside your games. Whether you need TrackIR running before your flight simulator, voice attack software for space games, or telemetry apps for racing sims, LaunchForge handles the entire launch sequence for you.

<img width="1200" height="800" alt="image" src="https://github.com/user-attachments/assets/4ada6ddc-539a-4d4b-b2da-e56c3cd5f66e" />

Developed by **SecondTry Labs**

---

## Table of Contents

- [Installation](#installation)
- [Getting Started](#getting-started)
- [Adding a Game](#adding-a-game)
- [Managing Launch Applications](#managing-launch-applications)
- [Launch First Mode](#launch-first-mode)
- [Keep Alive (CTD Protection)](#keep-alive-ctd-protection)
- [Desktop Launch Shortcuts](#desktop-launch-shortcuts)
- [Drag and Drop](#drag-and-drop)
- [Custom Icons](#custom-icons)
- [Disabling Profiles and Apps](#disabling-profiles-and-apps)
- [Settings](#settings)
- [Import and Export](#import-and-export)
- [Updates](#updates)
- [Logging](#logging)
- [FAQ](#faq)

---

## Installation

1. Download the latest `LaunchForge Setup x.x.x.exe` from the [Releases](https://github.com/secondtrylabs/launchforge-releases/releases) page
2. Run the installer — it will install to `%LOCALAPPDATA%\Programs\LaunchForge`
3. LaunchForge will launch automatically after installation
4. A desktop shortcut is created for easy access

**System Requirements:**
- Windows 10 or later
- No additional dependencies required

---

## Getting Started

When you first open LaunchForge, you'll see the empty state with an **+ Add Game** button.

<img width="1200" height="800" alt="image" src="https://github.com/user-attachments/assets/8ad9d27c-6e68-4c90-8324-9b64e05367d9" />

The interface is split into three sections:
- **Sidebar** (left) — Navigation between Games, Settings, and About
- **Profile List** (center) — Your saved game profiles
- **Profile Details** (right) — Configuration for the selected game

<img width="1200" height="800" alt="image" src="https://github.com/user-attachments/assets/7f1235ad-9c34-44e6-ba99-f6fdf59be7fa" />

---

## Adding a Game

Click **+ Add Game** to open the game selection modal. You can find games through four methods:

### Running Apps
Shows applications currently running on your system. The list updates in real-time every 2 seconds — start an app and it appears automatically.

<img width="1200" height="800" alt="image" src="https://github.com/user-attachments/assets/97c9bbf7-5b5a-4559-8d49-cd78214fd9ff" />

### Installed Apps
Scans your Windows Start Menu shortcuts to find installed applications. Every app with a valid executable path is shown with its icon.

<img width="531" height="465" alt="image" src="https://github.com/user-attachments/assets/c428b5bc-fa3d-416f-9bb4-f52b063669b2" />

### Steam Library
Automatically detects your Steam installation and lists all installed Steam games. Scans all Steam library folders across multiple drives.

<img width="525" height="460" alt="image" src="https://github.com/user-attachments/assets/6f3f83ae-c6ec-439e-acca-453bb0b5f7c4" />

### Browse .exe
Click **Browse .exe** to manually select any executable file on your system using the Windows file picker.

### Search
All tabs include a search bar for quick filtering. Type to instantly filter the list.

<img width="527" height="252" alt="image" src="https://github.com/user-attachments/assets/d7d77319-a86a-4966-b985-8f579a088623" />

---

## Managing Launch Applications

Once a game profile is created, you can add applications that should launch alongside it.

Click **+ Add Application** in the profile details panel. The same selection modal appears (Running, Installed, Steam, Browse .exe).

<img width="590" height="748" alt="image" src="https://github.com/user-attachments/assets/0391c261-41d1-4641-8a5a-0c77dde735b1" />

Each launch application displays:
- **App icon** — extracted automatically, or click to set a custom one
- **App name** — from the executable or shortcut
- **Executable path** — full path to the .exe
- **Launch arguments** — optional command-line arguments
- **Control buttons** — Launch First, Keep Alive, Disable, and Delete

### Launch Arguments

Each application has an arguments field below its name. Enter any command-line arguments your app needs:

```
--airline=019cef0b-cbd1-7347-a9c2-b9246690ecc2
--mode fullscreen
-config "C:\path\to\config.ini"
```

Arguments support quoted values and are parsed correctly when launching.

---

## Launch First Mode

Some applications need to be running **before** your game starts. For example, TrackIR must be initialized before a flight simulator loads, or it can't hook into the game.

Click the **fast-forward icon** (>>) on any launch application to enable Launch First mode. The button turns green when active.

<img width="110" height="26" alt="image" src="https://github.com/user-attachments/assets/660e6f7b-9641-46cc-8916-2320b690a652" />

### How It Works

**Without a desktop shortcut (auto-detect mode):**
1. You start your game normally
2. LaunchForge detects it running
3. LaunchForge closes the game
4. Launches all "Launch First" apps
5. Waits 3 seconds for them to initialize
6. Relaunches your game
7. Launches remaining (non-first) apps

**With a desktop shortcut (recommended for sensitive games):**
1. You click the LaunchForge desktop shortcut
2. LaunchForge starts all "Launch First" apps
3. Waits 3 seconds
4. Launches your game
5. Launches remaining apps
6. No kill/relaunch needed

> **Note:** For games like MSFS 2024 that don't handle force-close well, use the desktop shortcut method instead. See [Desktop Launch Shortcuts](#desktop-launch-shortcuts).

### App Sorting

Launch First apps are automatically sorted to the top of the list, followed by remaining apps in alphabetical order.

---

## Keep Alive (CTD Protection)

Click the **pin icon** on any launch application to enable Keep Alive. The button turns orange when active.

{image placeholder: Launch application row showing the pin button highlighted in orange}

When Keep Alive is enabled, LaunchForge will **not** close that application when your game exits. This is useful for:

- **Crash-to-desktop (CTD) protection** — If your game crashes, apps with recovery data (like flight planning software) stay open
- **Apps you want running across multiple game sessions** — Start once, use across game restarts
- **Background services** — Apps that should persist regardless of game state

Without Keep Alive, all launched apps are automatically closed when the game exits.

---

## Desktop Launch Shortcuts

When a profile has at least one Launch First app enabled, a **Create Shortcut** button (with a rocket icon) appears next to the game name in the profile header.

<img width="110" height="26" alt="image" src="https://github.com/user-attachments/assets/faa2eef0-5533-437c-a0a0-eb9c99fcef72" />

Clicking it creates a `.lnk` shortcut on your desktop with the game's icon. You can:
- **Double-click** it to launch the entire profile
- **Pin it to your taskbar** for quick access
- **Move it** anywhere you like

The shortcut tells LaunchForge to handle the entire launch sequence without needing to close and relaunch the game. This is the recommended approach for games that don't handle force-close well (e.g., MSFS 2024).

> **Requirement:** LaunchForge must be running (or set to start with Windows) for the shortcut to work. If LaunchForge isn't running, it will start automatically.

---

## Drag and Drop

You can copy launch applications between game profiles by dragging them.

1. Grab any launch application by the **grip handle** (dots on the left side of the row)
2. Drag it over to a different game profile in the left panel
3. The target profile highlights in purple when ready to receive
4. Drop to copy the app with all its settings

<img width="500" height="203" alt="image" src="https://github.com/user-attachments/assets/26196654-e4ac-472d-8377-a263fd069d78" />

**Details:**
- The app is **copied**, not moved — the original stays in the source profile
- All settings are preserved: Launch First, Keep Alive, arguments, custom icon
- Duplicate apps (same executable path) are automatically prevented
- Your current profile selection doesn't change during drag/drop

---

## Custom Icons

### Game Icons

Click the game icon in the profile details header to replace it. A hover overlay appears with an image icon. The file picker opens to the game's executable directory.

<img width="245" height="83" alt="image" src="https://github.com/user-attachments/assets/c0e965e4-81d9-492a-8c29-ac121e6598ab" />

### App Icons

Click any launch application's icon to replace it the same way. The file picker opens to the app's directory.

**Supported formats:** `.ico`, `.png`, `.jpg`, `.jpeg`, `.bmp`

Custom icons are stored as embedded data in your profile, so they survive export/import and work on any machine.

---

## Disabling Profiles and Apps

### Disable a Single Profile

Click the **power icon** on any game profile in the left panel. The profile dims and LaunchForge ignores it — no apps will launch when that game starts.

<img width="329" height="62" alt="image" src="https://github.com/user-attachments/assets/578a386e-b8cb-455b-a910-1079a901fb72" />

Click again to re-enable.

### Disable All Profiles

Click **Disable All** in the profile list header to globally pause all monitoring. The button turns red when active.

<img width="339" height="410" alt="image" src="https://github.com/user-attachments/assets/385b7f14-fe8e-4baa-b096-6924f8b5870f" />

### Disable Individual Apps

Click the **power icon** on any launch application within a profile. That specific app won't launch, but other apps in the profile still will. The row dims to indicate it's disabled.

<img width="573" height="108" alt="image" src="https://github.com/user-attachments/assets/d6443ece-09da-4c1f-bfc1-11a0e0453d4a" />

---

## Settings

Access settings from the **Settings** item in the sidebar.

<img width="1200" height="800" alt="image" src="https://github.com/user-attachments/assets/b2f2c072-9fad-425e-bf18-a07d6e75ea96" />

### Start LaunchForge when Windows starts

Adds LaunchForge to your Windows startup. The app launches automatically when you log in.

### Start Minimized

*Requires "Start with Windows" to be enabled.*

LaunchForge starts in the background instead of showing the window. Combine with "Minimize to System Tray" for a completely invisible startup.

### Minimize to System Tray

When enabled, clicking the minimize button (or the X button) sends LaunchForge to the system tray (notification area) instead of closing or minimizing to the taskbar.

<img width="35" height="32" alt="image" src="https://github.com/user-attachments/assets/c229f52e-3a70-4419-8a3f-b0e74cc2f355" />

Right-click the tray icon for options:
- **Open LaunchForge** — Show the main window
- **Quit** — Fully exit the application

---

## Import and Export

### Export Profiles

Go to **Settings** > **Export Profiles** to save all your game profiles to a JSON file. This includes:
- All game profiles and their configurations
- Launch applications with all settings
- Custom icons (embedded in the file)
- Launch arguments
- Launch First, Keep Alive, and Disable states

Use this to **back up** your configuration or **transfer** it to another machine.

### Import Profiles

Go to **Settings** > **Import Profiles** to load profiles from a previously exported JSON file. Imported profiles replace your current profiles.

> **Safety:** Importing profiles while games are running will not trigger any kills or relaunches. LaunchForge recognizes already-running games and skips them.

---

## Updates

LaunchForge automatically checks for updates when you launch the app. If a new version is available, a centered modal appears with two options:

- **Install & Restart** — Downloads the new installer, runs it silently, and restarts the app
- **Later** — Dismisses the notification for 24 hours

Updates are downloaded from GitHub Releases. No data is collected or sent — the app only checks the version number.

---

## Logging

LaunchForge maintains log files for troubleshooting at:

```
%APPDATA%\LaunchForge\logs\
```

| Log File | Contents |
|----------|----------|
| `app.log` | App startup, settings changes, shortcuts, general events |
| `profiles.log` | Profile updates, import/export operations |
| `launch.log` | Process detection, app launches, kills, desktop shortcut triggers |
| `errors.log` | All errors from every category |

Logs automatically rotate when they exceed 2MB (previous log renamed to `.old.log`).

---

## FAQ

### LaunchForge detected my game and killed it — how do I prevent this?

This happens with the auto-detect flow when you have Launch First apps configured. For games that don't handle force-close well (like MSFS 2024), create a **desktop shortcut** instead. Click "Create Shortcut" on the profile, then always launch your game through that shortcut.

### My profiles disappeared after a restart

Profiles are saved to `%APPDATA%\LaunchForge\profiles.json`. If this file is missing or corrupted, profiles may be lost. Use **Export Profiles** regularly to create backups.

### An installed app isn't showing in the list

LaunchForge scans Windows Start Menu shortcuts for installed apps. If an app doesn't have a Start Menu entry, use **Browse .exe** to add it manually.

### Can I use LaunchForge with Steam games?

Yes. The **Steam** tab in the game selection modal automatically detects all installed Steam games across all library folders.

### The desktop shortcut icon is wrong or blank

Delete the old shortcut and click "Create Shortcut" again from the profile. If you changed the game's custom icon, the shortcut needs to be recreated to pick up the new icon.

### LaunchForge is running twice

LaunchForge has a single-instance lock — only one copy should run. If you see duplicates, check **Task Manager > Startup apps** for duplicate entries and disable the extra one.

### The shortcut doesn't launch anything

Make sure LaunchForge is running (or set to start with Windows). The desktop shortcut sends a command to the running LaunchForge instance — it doesn't work standalone.

### Where is my data stored?

| Data | Location |
|------|----------|
| Profiles | `%APPDATA%\LaunchForge\profiles.json` |
| Settings | `%APPDATA%\LaunchForge\settings.json` |
| Logs | `%APPDATA%\LaunchForge\logs\` |
| Shortcut icons | `%APPDATA%\LaunchForge\icons\` |
| Application | `%LOCALAPPDATA%\Programs\LaunchForge\` |

---

## About

The About page (accessible from the sidebar) shows the current version, copyright, and a full changelog of all releases.

{image placeholder: About page showing version number, copyright, and scrollable changelog}

---

*Copyright SecondTry Labs. All rights reserved.*
