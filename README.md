# dotfiles

Personal configuration files for terminal tools and development environment.

## Structure

```
dotfiles/
└── tmux/
    ├── tmux.conf   # tmux configuration
    └── README.md   # detailed explanation of every setting
```

## Installation

Each tool has its own directory. Activate a config by symlinking it to the expected location:

```bash
# tmux
ln -sf ~/workspace/personal/dotfiles/tmux/tmux.conf ~/.tmux.conf
```
