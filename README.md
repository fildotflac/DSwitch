# DSwitch

**Desktop instance manager built for KDE Plasma.**

DSwitch lets you keep several separate desktops (for example *Work*, *Game*, *School*) and swap between them with a single command. Each desktop is just a folder in your home directory, so every one of them has its own icons, files and shortcuts. DSwitch re-points your `~/Desktop` symlink at the one you pick and restarts Plasma so the change shows up right away.

## How it works

- Every desktop lives in `~/Desktop_<Name>` (e.g. `~/Desktop_Work`, `~/Desktop_Game`).
- `~/Desktop` is a **symlink** to the currently active desktop folder.
- Switching = updating the symlink, then restarting `plasmashell`.
- Names are case-insensitive: `dswitch work`, `dswitch Work` and `dswitch WORK` all do the same thing.

## Requirements

- KDE Plasma (the script uses `kquitapp5` and `kstart5` to restart `plasmashell`)
- Bash
- `sudo` access for installation

> **Plasma 6 users:** `kquitapp5` / `kstart5` were replaced by `kquitapp6` / `kstart` in Plasma 6. If the refresh step fails, edit the two places in `dswitch` that call them (the `switch_to_desktop` and `refresh_desktop` functions).

## Installation

```bash
git clone https://github.com/fildotflac/DSwitch.git
cd DSwitch
sudo chmod +x install.sh
sudo ./install.sh
```

The installer moves the `dswitch` script to `/bin/dswitch`, so you can run it from anywhere. See [INSTALL.md](INSTALL.md) for the short version.

> The script is moved into `/bin`, so make sure `dswitch` is executable before installing (`chmod +x dswitch`) if it isn't already.

## First-time setup

DSwitch expects `~/Desktop` to be a symlink. If yours is currently a regular folder, convert it once:

```bash
mv ~/Desktop ~/Desktop_Main
ln -s ~/Desktop_Main ~/Desktop
```

After that, create as many extra desktops as you like.

## Usage

```text
dswitch <name>              Switch to the desktop called <name>
dswitch create <name>       Create a new desktop (offers to switch to it)
dswitch delete <name>       Delete a desktop (asks for confirmation)
dswitch list                List all available desktops
dswitch refresh             Restart plasmashell to refresh the desktop
```

Running `dswitch` with no arguments prints the usage line and the list of available desktops.

### Examples

```bash
# Create a desktop for gaming and switch to it
dswitch create game

# See what you have
dswitch list

# Jump between desktops
dswitch work
dswitch game

# Remove one you no longer need
dswitch delete game
```

### Notes and safety

- You **cannot delete the desktop you're currently on**. Switch to another one first.
- `delete` removes the whole `~/Desktop_<Name>` folder (`rm -rf`) after you confirm, so move anything you want to keep first.
- `create` refuses to overwrite a desktop that already exists.
- Switching to the desktop you're already on just reports that and does nothing.

## Repository contents

| File | Purpose |
| --- | --- |
| `dswitch` | The main script |
| `install.sh` | Installs `dswitch` to `/bin` |
| `INSTALL.md` | Quick install guide |

## Uninstall

```bash
sudo rm /bin/dswitch
```

Your `~/Desktop_*` folders are not touched.

## License

No license has been specified yet. Add a `LICENSE` file (for example MIT or GPL-3.0) to let others know how they can use the project.
