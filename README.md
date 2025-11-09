# AeroSpace Configuration for macOS

This repository contains my personal [AeroSpace](https://github.com/nikitabobko/AeroSpace) tiling window manager configuration for macOS, optimized to work seamlessly with [Ghostty terminal](https://github.com/ghostty-org/ghostty).

## 🚀 Features

- **Vim-style Navigation**: Navigate between windows using `Alt+hjkl` (doesn't conflict with Ghostty's `Ctrl+hjkl` split navigation)
- **Workspace Management**: 9 workspaces with automatic app placement
- **Seamless Ghostty Integration**: Use `Ctrl+hjkl` for terminal splits and `Alt+hjkl` for window navigation
- **Intuitive Keybindings**: All keybindings follow a consistent pattern
- **Smart Window Rules**: Automatic workspace assignment for common applications

## 📦 Installation

### 1. Install AeroSpace

If you haven't already installed AeroSpace:

```bash
brew install --cask nikitabobko/tap/aerospace
```

### 2. Link Configuration

Create a symlink to the AeroSpace configuration:

```bash
# Backup existing config if present
[ -f ~/.aerospace.toml ] && mv ~/.aerospace.toml ~/.aerospace.toml.backup

# Create symlink
ln -s $PWD/aerospace.toml $HOME/.aerospace.toml
```

### 3. Start AeroSpace

Start AeroSpace for the first time:

```bash
# Start AeroSpace
open -a AeroSpace

# Grant accessibility permissions when prompted
# Go to System Preferences > Security & Privacy > Accessibility
# Make sure AeroSpace is checked
```

### 4. Make AeroSpace Start on Login

```bash
# Enable auto-start
aerospace enable --start-at-login
```

## ⌨️ Keybindings

### Window Navigation (Works Across Applications)

| Keybinding | Action             |
| ---------- | ------------------ |
| `Alt+h`    | Focus window left  |
| `Alt+j`    | Focus window down  |
| `Alt+k`    | Focus window up    |
| `Alt+l`    | Focus window right |

### Terminal Split Navigation (Within Ghostty Only)

| Keybinding | Action                  |
| ---------- | ----------------------- |
| `Ctrl+h`   | Navigate to left split  |
| `Ctrl+j`   | Navigate to down split  |
| `Ctrl+k`   | Navigate to up split    |
| `Ctrl+l`   | Navigate to right split |

### Window Movement

| Keybinding    | Action            |
| ------------- | ----------------- |
| `Alt+Shift+h` | Move window left  |
| `Alt+Shift+j` | Move window down  |
| `Alt+Shift+k` | Move window up    |
| `Alt+Shift+l` | Move window right |

### Window Resizing

| Keybinding  | Action          |
| ----------- | --------------- |
| `Alt+Cmd+h` | Decrease width  |
| `Alt+Cmd+j` | Increase height |
| `Alt+Cmd+k` | Decrease height |
| `Alt+Cmd+l` | Increase width  |

### Workspace Management

| Keybinding                     | Action                             |
| ------------------------------ | ---------------------------------- |
| `Alt+1` to `Alt+9`             | Switch to workspace 1-9            |
| `Alt+Shift+1` to `Alt+Shift+9` | Move window to workspace 1-9       |
| `Alt+Shift+←`                  | Move workspace to previous monitor |
| `Alt+Shift+→`                  | Move workspace to next monitor     |

### Layout Control

| Keybinding        | Action                                        |
| ----------------- | --------------------------------------------- |
| `Alt+/`           | Toggle between horizontal and vertical layout |
| `Alt+,`           | Toggle accordion layout                       |
| `Alt+Shift+F`     | Toggle fullscreen                             |
| `Alt+Shift+Space` | Toggle floating/tiling                        |
| `Alt+Shift+R`     | Reload configuration                          |
| `Alt+Shift+0`     | Setup 60/40 split layout (browser 40%, terminal 60%) |

### Service Mode (Advanced)

Press `Alt+Shift+;` to enter service mode, then:

| Key                 | Action                            |
| ------------------- | --------------------------------- |
| `h/j/k/l`           | Focus window (exits service mode) |
| `Alt+Shift+h/j/k/l` | Join window with adjacent window  |
| `b`                 | Balance window sizes              |
| `f`                 | Toggle float/tile                 |
| `r`                 | Flatten workspace tree            |
| `Backspace`         | Close all windows except current  |
| `Esc`               | Exit service mode                 |

## 🗂 Workspace Layout

The configuration automatically assigns applications to specific workspaces:

| Workspace | Applications                   | Layout                                    |
| --------- | ------------------------------ | ----------------------------------------- |
| 1         | Browser (Chrome/Brave) + Terminal (Ghostty) | Browser 40% left, Terminal 60% right |
| 2         | General purpose                |                                           |
| 3         | Code Editors (VS Code, Atom)   |                                           |
| 4         | Email (Mail)                   |                                           |
| 5         | Communication (Discord, Slack) |                                           |
| 6-8       | General purpose                |                                           |
| 9         | Music (Spotify, Apple Music)   |                                           |

### Setting up the 60/40 Split (Workspace 1)

Your main workspace (1) is configured for a browser and terminal side-by-side. To achieve the perfect 60/40 split:

**Option 1: Use the Quick Setup Keybinding**
- Press `Alt+Shift+0` to automatically arrange windows in 60/40 split
- Browser will be on the left (40%), Terminal on the right (60%)

**Option 2: Manual Setup**
1. Open your browser and terminal on workspace 1
2. Position terminal on the right: Focus terminal → `Alt+Shift+L`
3. Position browser on the left: Focus browser → `Alt+Shift+H`  
4. Adjust sizes:
   - Focus browser (left) → `Alt+Cmd+H` press 5-6 times to shrink to ~40%
   - Focus terminal (right) → `Alt+Cmd+L` press 5-6 times to grow to ~60%

**Note**: The layout will persist across restarts once set up.

## 🔧 Customization

### Modifying Gaps

Edit the `[gaps]` section in `aerospace.toml`:

```toml
[gaps]
inner.horizontal = 8  # Gap between windows
inner.vertical =   8
outer.left =       8  # Gap from screen edge
outer.bottom =     8
outer.top =        8
outer.right =      8
```

### Adding Custom App Rules

Add new `[[on-window-detected]]` sections:

```toml
[[on-window-detected]]
if.app-id = 'com.example.MyApp'
run = 'move-node-to-workspace 6'
```

To find an app's bundle ID:

```bash
osascript -e 'id of app "AppName"'
```

### Changing Keybindings

Modify the `[mode.main.binding]` section. See [AeroSpace commands reference](https://nikitabobko.github.io/AeroSpace/commands) for available commands.

## 🎯 Workflow Tips

### Seamless Terminal + Window Navigation

1. **Within Ghostty**: Use `Ctrl+hjkl` to navigate between terminal splits
2. **Between Applications**: Use `Alt+hjkl` to navigate between different application windows
3. **Quick Switch**: Your muscle memory stays consistent with vim-style navigation

### Multi-Monitor Setup

1. Move entire workspaces between monitors: `Alt+Shift+←` or `Alt+Shift+→`
2. AeroSpace will automatically follow your cursor to the focused monitor

### Quick Window Management

1. Open a new window → It tiles automatically
2. Need more space? → `Alt+Shift+F` for fullscreen
3. Temporary window? → `Alt+Shift+Space` to float it
4. Done with a window? → `Cmd+Q` to quit normally

## 🔍 Troubleshooting

### AeroSpace isn't responding to keybindings

1. Check that AeroSpace has accessibility permissions:

   ```bash
   System Preferences > Security & Privacy > Accessibility
   ```

2. Restart AeroSpace:
   ```bash
   killall AeroSpace && open -a AeroSpace
   ```

### Conflicts with Ghostty keybindings

The configuration uses `Alt` for AeroSpace and `Ctrl` for Ghostty, so they shouldn't conflict. If you experience issues:

1. Verify your Ghostty config at: `~/c/ghostty-conf/config/ghostty.conf`
2. Check that Ghostty uses `ctrl+hjkl` for splits (as configured)
3. Reload both configs:
   - Ghostty: `Ctrl+Shift+R`
   - AeroSpace: `Alt+Shift+R`

### Windows not tiling properly

1. Some apps force floating mode. You can manually tile them:

   ```
   Alt+Shift+Space
   ```

2. Check the `[[on-window-detected]]` rules in the config

### Configuration not loading

1. Verify the symlink:

   ```bash
   ls -la ~/.aerospace.toml
   ```

2. Reload the configuration:
   ```bash
   aerospace reload-config
   ```

## 📚 Resources

- [AeroSpace Documentation](https://nikitabobko.github.io/AeroSpace/)
- [AeroSpace GitHub](https://github.com/nikitabobko/AeroSpace)
- [Ghostty Terminal](https://github.com/ghostty-org/ghostty)
- [Ghostty Documentation](https://ghostty.org/docs)

## 🤝 Contributing

Feel free to suggest improvements or report issues!

## 📝 License

This configuration is free to use and modify for personal use.
