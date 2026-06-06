# tmux scripts

Hand-crafted scripts for saving and restoring tmux sessions across restarts.

## Installation

Symlink both scripts to somewhere on your `$PATH`:

```bash
ln -sf "$DOTFILES/tmux/scripts/tmux-save"    ~/.local/bin/tmux-save
ln -sf "$DOTFILES/tmux/scripts/tmux-restore" ~/.local/bin/tmux-restore
chmod +x ~/.local/bin/tmux-save ~/.local/bin/tmux-restore
```

## Scripts

### `tmux-save`

Snapshots all open sessions and windows to `~/.local/share/tmux/sessions`.

Each line in the file represents one window:

```
session_name<TAB>/path/to/working/dir
```

Runs automatically on new window, new session, and pane kill (via hooks in `tmux.conf`). Can also be triggered manually with `prefix + Ctrl-s`.

### `tmux-restore`

Reads `~/.local/share/tmux/sessions` and recreates every session and window with the saved working directory. If a saved path no longer exists, it falls back to `$HOME`.

Trigger manually after a reboot with `prefix + Ctrl-r`, or call it directly:

```bash
tmux-restore
```

## Keybindings

| Keys | Action |
|------|--------|
| `prefix + Ctrl-s` | Save sessions now |
| `prefix + Ctrl-r` | Restore sessions |
