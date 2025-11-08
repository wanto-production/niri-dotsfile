# Niri Window Manager Configuration

This repository contains the configuration for [niri](https://github.com/YaLTeR/niri), a tiling Wayland compositor with columns and immersive overview.

## Overview

This configuration is designed to be similar to a Hyprland setup, with column-based tiling, custom keybindings, and various application integrations. It features a catppuccin-inspired color scheme with lavender accents.

## Features

- Column-based tiling window management
- Custom keybindings for window management, workspaces, and media controls
- Touchpad, mouse, and keyboard input configurations
- Integration with custom tools and applications
- Screenshot functionality with custom paths

## Configuration Details

### Input Settings

#### Keyboard
- Layout: US English
- Repeat delay: 600ms
- Repeat rate: 25

#### Touchpad
- Tap to click enabled
- Disable while typing (DWT)
- Natural scrolling
- Acceleration speed: 0.2

#### Mouse
- Acceleration speed: 0.0 (flat profile)
- Acceleration profile: "flat"

### Output Configuration

- Monitor: "eDP-1" (laptop display)
- Resolution: 1920x1080 @ 60Hz
- Scale: 1.0
- Position: x=0, y=0

### Layout Settings

- Gaps: 5px (internal) / 10px (external)
- Column centering: "on-overflow"
- Preset column widths: 33.33%, 50%, 66.67%
- Default column width: 100%

### Visual Elements

- Focus ring: 1px width with lavender gradient (#b4befe to #89b4fa)
- Border: 1px width with lavender gradient
- Window corner radius: 5px
- CSD (Client-Side Decoration) disabled (prefer server-side)

### Environment Variables

- Sets up Wayland session environment
- Configures Qt, GTK, and other toolkit variables
- Enables Firefox Wayland support

## Keybindings

### Application Launchers
- `Mod+Return`: Open terminal (kitty)
- `Mod+E`: File manager (nautilus)
- `Mod+B`: Web browser (brave)
- `Mod+R`: Application launcher
- `Mod+V`: Clipboard manager

### Window Management
- `Mod+Q`: Close window
- `Mod+F`: Fullscreen window
- `Mod+Shift+F`: Maximize column
- `Mod+T`: Focus floating windows
- `Mod+C`: Center column

### Focus Movement (Vi-style and Arrow keys)
- `Mod+H` / `Mod+Left`: Focus left column
- `Mod+L` / `Mod+Right`: Focus right column
- `Mod+J` / `Mod+Down`: Focus window down
- `Mod+K` / `Mod+Up`: Focus window up

### Window Movement (Vi-style and Arrow keys)
- `Mod+Shift+H` / `Mod+Shift+Left`: Move column left
- `Mod+Shift+L` / `Mod+Shift+Right`: Move column right
- `Mod+Shift+J` / `Mod+Shift+Down`: Move window down
- `Mod+Shift+K` / `Mod+Shift+Up`: Move window up

### Window Resizing (Vi-style and Arrow keys)
- `Mod+Ctrl+Left` / `Mod+Ctrl+H`: Decrease column width
- `Mod+Ctrl+Right` / `Mod+Ctrl+L`: Increase column width
- `Mod+Ctrl+Up` / `Mod+Ctrl+K`: Increase window height
- `Mod+Ctrl+Down` / `Mod+Ctrl+J`: Decrease window height

### Workspace Management
- `Mod+[1-0]`: Focus workspace 1-10
- `Mod+Shift+[1-0]`: Move column to workspace 1-10
- `Mod+Tab` / `Mod+Shift+Tab`: Cycle workspaces
- `Mod+Scroll Up/Down`: Cycle workspaces
- `Mod+S`: Toggle scratchpad (workspace 11)
- `Mod+Shift+S`: Send window to scratchpad

### Screenshot Commands
- `Print`: Take screenshot
- `Shift+Print`: Screenshot window
- `Ctrl+Print`: Screenshot to clipboard
- `Mod+Print`: Screenshot window

### Media Controls
- `XF86AudioRaiseVolume`: Volume up
- `XF86AudioLowerVolume`: Volume down
- `XF86AudioMute`: Toggle mute
- `XF86AudioMicMute`: Toggle mic mute
- `XF86AudioPlay` / `XF86AudioPause`: Play/pause
- `XF86AudioNext`: Next track
- `XF86AudioPrev`: Previous track
- `Mod+Shift+P`: Play/pause media

### Niri-Specific Functions
- `Mod+Shift+R`: Reload config
- `Mod+Shift+O`: Toggle overview
- `Mod+/`: Show all keybinds

### Session Management
- `Mod+Shift+Q`: Session menu

## Window Rules

The configuration includes specific rules for certain applications:
- Thunar file manager and web browsers are set to use 100% column width
- Floating applications like pavucontrol, blueberry, and nm-connection-editor are set to fixed width

## Startup Applications

- PolicyKit authentication agent
- wl-paste clipboard synchronization with cliphist
- Trash-empty with 30-day retention
- Custom Qtile shell (noctalia-shell)

## File Locations

- Configuration file: `~/.config/niri/config.kdl`
- Screenshot path: `~/Pictures/Screenshots/` with timestamped filenames

## Theme

- Uses the Catppuccin Mocha Lavender cursor theme
- Color accents use lavender (#b4befe) for active elements

## Notes

- This configuration was ported from a Hyprland setup
- Some commented-out animations use Expo easing functions
- The setup includes integration with custom tools like noctalia-shell

## Noctalia Shell Integration

This niri configuration makes extensive use of [noctalia-shell](https://github.com/noctalia-dev/noctalia-shell), a Qtile-based shell for Wayland compositors. The integration is done through IPC calls that allow niri to communicate with the shell for various functions.

### Functionality Provided by Noctalia Shell

- **Application Launcher**: Accessed with `Mod+R`, provides a searchable application launcher
- **Clipboard Manager**: Toggled with `Mod+V`, manages text and image clipboard history
- **Session Menu**: Toggled with `Mod+Shift+Q`, provides session management options
- **Wallpaper Management**: Toggled with `Mod+W`, allows wallpaper selection; `Mod+Shift+W` for random wallpaper
- **Volume Control**: Handles audio controls through the XF86 media keys
- **Media Controls**: Manages playback controls for media applications

### IPC Commands Used

The configuration uses the following noctalia-shell IPC commands:

- `qs -c noctalia-shell ipc call launcher toggle` - Toggles application launcher
- `qs -c noctalia-shell ipc call launcher clipboard` - Opens clipboard manager
- `qs -c noctalia-shell ipc call sessionMenu toggle` - Toggles session menu
- `qs -c noctalia-shell ipc call wallpaper toggle` - Toggles wallpaper picker
- `qs -c noctalia-shell ipc call wallpaper random` - Sets random wallpaper
- `qs -c noctalia-shell ipc call volume increase/decrease/muteOutput/muteInput` - Controls audio
- `qs -c noctalia-shell ipc call media playPause` - Controls media playback

### Startup Integration

Noctalia Shell is launched at startup with the command:
`qs -c noctalia-shell -d`

This ensures the shell is running and ready to respond to IPC commands from niri.