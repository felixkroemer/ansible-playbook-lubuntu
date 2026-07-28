---
name: add-to-path
description: Use when the user says "symlink", "shortcut", "launch", "appimage", or asks to add a runnable to PATH so a launcher can find it. Creates a .desktop entry in ~/.local/share/applications/ so the app appears in launchers.
---

# Add to PATH

Creates a `.desktop` entry in `~/.local/share/applications/` so the runnable appears in application launchers (rofi drun, kickoff, etc.).

## Usage

1. Ask the user for the **path** to the runnable (e.g. `/path/to/some-app.AppImage`). The path may point to a directory (e.g. an extracted AppImage). In that case, list the directory contents and detect the actual executable binary/script inside — prefer the largest ELF binary or the file named similarly to the AppImage (e.g. `some-app` inside a `some-app-v1.0.0` directory).

2. Ensure the runnable is executable:

   ```bash
   chmod +x "$SOURCE"
   ```

3. Create the `.desktop` file in `~/.local/share/applications/`:

   ```bash
   mkdir -p ~/.local/share/applications
   ```

   Template:
   ```desktop
   [Desktop Entry]
   Type=Application
   Name=App Name
   Exec=/path/to/executable
   Categories=Utility;
   Terminal=false
   ```

4. If the app has an icon (e.g. `*.png`, `*.svg`, `*.xpm` in the same directory), set the `Icon` field to its path.

5. Confirm the result to the user.

`~/.local/share/applications/` is watched by desktop environments and launchers (rofi, ulauncher, KDE kickoff, etc.) — the app will appear immediately or after a short refresh.
