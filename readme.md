## Overview

This repository, **`https://github.com/AnubhabMukherjee2003/My-ARCH-hyprland-setup`**, contains all of my personal configuration (“dotfiles”) for an Arch Linux environment powered by Hyprland. It includes:

- Shell configs (`.bashrc`, `.zshrc`)  
- Starship prompt (`starship.toml`)  
- Hyprland session (`hyprland.conf`, `hypridle.conf`, `hyprlock.conf`, `hyprpaper.conf`)  
- Kitty terminal (`kitty.conf`, `current-theme.conf`)  
- Wofi Menu launcher (`style.css`)  
- Waybar status bar (`config`, `style.css`)  

By versioning these in Git, you can reproduce my environment on any machine with one `git clone`.

---

## Prerequisites

Before installing, ensure you have:

* **Arch Linux** (or derivative) with `sudo` privileges 
* A working **Wayland** session
* Installed packages:

  ```bash
  sudo pacman -S hyprland hyprshot hyprlock hypridle hyprpaper swaync waybar kitty wofi starship git
  ```
* Optional helpers: AUR helper (`yay`/`paru`) for additional packages like `ttf-comic-neue` ([Medium][2]).

---

## Installation

1. **Clone the repo**

   ```bash
   git clone https://github.com/youruser/anubhabmukherjee2003-my-hyprland-setup.git ~/.config/my-hyprland-setup
   cd ~/.config/my-hyprland-setup
   ```

2. **Symlink configurations**
   Using GNU Stow (recommended for modular dotfiles) ([Reddit][3]):

   ```bash
   sudo pacman -S stow
   stow --target=$HOME zshrc           # symlinks ~/.bashrc, or ~/.zshrc
   stow --target=$HOME/config hypr kitty waybar wofi starship
   ```

   Or manually copy/link the folders under `~/.config/`:

   ```bash
   cp .bashrc ~/
   cp .zshrc ~/
   cp -r .config/* ~/.config/
   ```
3. **Fonts & Icons**
   Install patched fonts for icons (e.g., **Roboto Mono Nerd Font** or **Comic Neue**):

   ```bash
   yay -S ttf-roboto-mono-nerd ttf-comic-neue
   fc-cache -fv
   ```

4. **Reload/Restart**

   * **Hyprland**:

     ```bash
     hyprctl reload
     ```
   * **Waybar**:

     ```bash
     pkill waybar && waybar &
     ```
   * **Starship** will pick up your shell changes on new sessions.

---

## Usage

* **Launchers**

  * **Wofi**: `Mod + d` (or as bound in Hyprland)
  * **Waybar**: auto-starts with `exec-once = waybar &` in `hyprland.conf`

* **Lockscreen**

  * Run `hyprlock` manually or via `Mod+Shift+L`.
  * Unlock with your system password; field only appears when typing.

* **Screensaver & Idle**

  * `hypridle` triggers `hyprlock` after inactivity (configured in `hypridle.conf`).

---

## Repository Structure

```text
anubhabmukherjee2003-my-hyprland-setup/
├── README.md              ← This file
├── .bashrc                ← Bash prompt (Starship)
├── .zshrc                 ← Zsh prompt (Starship)
└── .config/
    ├── starship.toml      ← Starship prompt config
    ├── hypr/
    │   ├── hyprland.conf
    │   ├── hyprlock.conf
    │   ├── hyprpaper.conf
    │   └── hypridle.conf
    ├── kitty/
    │   ├── kitty.conf
    │   └── current-theme.conf
    ├── waybar/
    │   ├── config
    │   └── style.css
    └── wofi/
        └── style.css
```

---

## Customization & Contributing

* Feel free to **fork** and adjust colors, fonts, or keybinds to your taste.
* To propose changes, submit a **Pull Request**—improvements in documentation and structure are always welcome ([bananamafia.dev][4]).
* **Do not** commit sensitive data (passwords, API keys). Use placeholders or environment variables.

---

