# tmux configuration

## Installation

```bash
ln -sf ~/workspace/personal/dotfiles/tmux/tmux.conf ~/.tmux.conf
```

Then reload inside a running tmux session with `Ctrl+a r`, or start a fresh session.

---

## General

| Setting | Value | What it does |
|---|---|---|
| `default-terminal` | `tmux-256color` | Tells tmux to advertise itself as a 256-color terminal, enabling richer color support in apps running inside it. |
| `terminal-overrides` | `Tc` on xterm-256color | Enables **true color** (24-bit RGB) passthrough so colors rendered inside tmux match what your terminal actually supports. Without this, colors may look washed out. |
| `prefix` | `Ctrl+a` | Replaces the default `Ctrl+b`. Easier to reach and familiar to `screen` users. `Ctrl+a Ctrl+a` sends the prefix key itself to the underlying program. |
| `base-index` | `1` | Windows start numbering at 1 instead of 0, matching the keyboard layout. |
| `pane-base-index` | `1` | Same as above but for panes within a window. |
| `renumber-windows` | `on` | When a window is closed, remaining windows are renumbered to close any gaps (e.g. 1, 3, 4 → 1, 2, 3). |
| `history-limit` | `50000` | How many lines of scrollback each pane stores. |
| `escape-time` | `0` | Removes the default 500ms delay after pressing `Escape`. Essential for vim — without this, `Escape` in vim feels sluggish. |
| `focus-events` | `on` | Passes focus gain/loss events from the terminal into tmux and down to running programs. Lets vim trigger `autoread` when you switch back to its pane. |
| `mouse` | `on` | Enables mouse support: click to select panes/windows, scroll to enter copy mode, drag to resize panes. |
| `status-interval` | `5` | Status bar refreshes every 5 seconds (default is 15). Keeps the clock and other dynamic info reasonably current. |
| `automatic-rename` | `on` | Window names update automatically based on the running command. |
| `automatic-rename-format` | `#{b:pane_current_path}` | Uses the **basename** of the current directory as the window name, so you see `dotfiles` instead of `/home/user/workspace/dotfiles`. |
| `set-titles` | `on` | Updates the terminal window/tab title. |
| `set-titles-string` | `#S · #W` | Format: `session-name · window-name`. Useful when you have multiple terminal tabs each hosting a tmux session. |

---

## Key Bindings

All bindings use the prefix (`Ctrl+a`) unless noted.

### Config

| Key | Action |
|---|---|
| `prefix r` | Reload `~/.tmux.conf` in place and display a confirmation message. No need to kill the session. |

### Panes

| Key | Action |
|---|---|
| `prefix \|` | Split the current pane **horizontally** (left/right). Opens in the same directory. |
| `prefix -` | Split the current pane **vertically** (top/bottom). Opens in the same directory. |
| `prefix h/j/k/l` | Move focus to the pane left / down / up / right. |
| `prefix ←/↓/↑/→` | Same as above using arrow keys. |
| `prefix H/J/K/L` | **Resize** the current pane left / down / up / right by 5 cells. Repeatable — hold prefix and keep pressing. |
| `prefix x` | Kill the current pane without a confirmation prompt. |

### Windows

| Key | Action |
|---|---|
| `prefix c` | Create a new window, opening in the current directory. |
| `prefix Ctrl+h` | Go to the previous window. Repeatable. |
| `prefix Ctrl+l` | Go to the next window. Repeatable. |
| `prefix <` | Move the current window one position to the left. |
| `prefix >` | Move the current window one position to the right. |
| `prefix X` | Kill the current window without a confirmation prompt. |

---

## Copy Mode

tmux has a built-in copy mode for scrolling and selecting text. It's configured to use **vi key bindings**.

| Key | Action |
|---|---|
| `prefix Enter` | Enter copy mode. |
| `q` or `Escape` | Exit copy mode. |
| `v` | Start a visual (character) selection. |
| `V` | Start a line selection. |
| `Ctrl+v` | Toggle rectangle (block) selection. |
| `y` | Yank (copy) the selection to the tmux clipboard and exit copy mode. |
| `H` | Jump to the start of the line. |
| `L` | Jump to the end of the line. |
| `j/k` | Scroll down/up one line. |
| `Ctrl+d/u` | Scroll down/up half a page. |
| `/` | Search forward. |
| `?` | Search backward. |
| `n/N` | Next/previous search match. |

> To paste the copied text: `prefix ]`.

---

## Catppuccin Mocha Theme

The status bar and UI elements use the [Catppuccin Mocha](https://github.com/catppuccin/catppuccin) palette, implemented natively without any plugins. Here are the colors in use:

| Variable | Hex | Used for |
|---|---|---|
| `mocha_base` | `#1e1e2e` | Status bar background |
| `mocha_surface0` | `#313244` | Inactive window tab background, message bar |
| `mocha_surface1` | `#45475a` | Date segment background |
| `mocha_overlay1` | `#7f849c` | Subtle UI text |
| `mocha_subtext1` | `#bac2de` | Inactive window tab text, date text |
| `mocha_text` | `#cdd6f4` | Default foreground text |
| `mocha_lavender` | `#b4befe` | Active pane border, active window tab |
| `mocha_blue` | `#89b4fa` | Time segment background |
| `mocha_mauve` | `#cba6f7` | Session name pill |

### Status Bar Layout

```
 session ▶  1  window-a   2  window-b              ◀ Thu 05 Jun ◀ 14:32
 ^mauve^    ^inactive tabs^   ^active tab^            ^surface1^   ^blue^
```

- **Left**: Session name in a mauve pill with powerline arrows.
- **Center**: Window tabs — inactive in `surface0`, active in `lavender`.
- **Right**: Date in `surface1`, time in `blue`.

---

## Cheatsheet

```
Prefix = Ctrl+a

─ Panes ──────────────────────────────
prefix |       split right
prefix -       split down
prefix h/j/k/l  move between panes
prefix ←/↓/↑/→  move between panes
prefix H/J/K/L resize pane
prefix x       kill pane

─ Windows ────────────────────────────
prefix c       new window
prefix Ctrl+h  previous window
prefix Ctrl+l  next window
prefix < / >   reorder window
prefix X       kill window

─ Copy mode ──────────────────────────
prefix Enter   enter copy mode
v              begin selection
V              line selection
Ctrl+v         rectangle selection
y              yank & exit
prefix ]       paste

─ Other ──────────────────────────────
prefix r       reload config
```
