<p align="center">
  <img src="../img/favicon.ico" alt="UniOS logo" width="200">
</p>

# unios-desktop-settings

unios-desktop-settings is the package that gives UniOS its look on KDE Plasma. It ships the UniOS wallpapers and logo, sets Breeze Dark as the default theme, replaces the Plasma Welcome Center with our own first login setup, and puts the UniOS logo on the application launcher.

It has no code of its own to build; everything it installs is described in the `PKGBUILD`.

## How it works

1. On install, the wallpapers go to `/usr/share/wallpapers/UniOS`, so they show up in Plasma's wallpaper picker as **UniOS Wallpapers**, and the logo replaces the KDE start-here and distributor icons.
2. System-wide defaults in `/etc/xdg` make Breeze Dark the look and feel, color scheme, icon theme and Plasma theme.
3. The Plasma Welcome Center is turned off, both through its autostart entry and through the defaults in `/etc/skel` that every new user gets.
4. On every login, the `unios-plasma-setup.sh` autostart script waits for Plasma to start, sets `default.jpg` as the wallpaper of every desktop, and sets the UniOS logo as the icon of the application launcher on every panel.

Since the files in `/etc/skel` are only copied when a user is created, existing users keep their Welcome Center settings. The theme defaults in `/etc/xdg` apply to anyone who hasn't changed them in their own `~/.config`.

## Installation

### As a user

**On UniOS**, unios-desktop-settings is preinstalled. If you removed it, install it again from `unios-repo`:

```bash
sudo pacman -S unios-desktop-settings
```

**On other Arch-based distributions** running KDE Plasma, build the package from the `PKGBUILD` in this repository:

```bash
git clone https://github.com/open-source-uom/unios-desktop-settings.git
cd unios-desktop-settings
makepkg -si
```

Log out and back in afterwards, so the setup script runs.

### As a developer

You only need `base-devel` and a KDE Plasma session to test the result:

```bash
sudo pacman -S base-devel
```

Build the package without installing it, and check what it would install:

```bash
makepkg -f
tar -tf unios-desktop-settings-*.pkg.tar.zst
```

When you're happy with it, install it with `makepkg -si` and log in again. To build it for `unios-repo`, follow the `pkgbuilder` process in [our build server](build.unios-project.eu.md) docs.

## Project Structure

```
unios-desktop-settings/
├── PKGBUILD                  package recipe; also generates every config file below
├── resources/
│   ├── logos/
│   │   └── unios.png         the UniOS logo
│   └── wallpapers/
│       ├── default.jpg       the wallpaper set on login
│       ├── dense_repeating_patterns.jpg
│       └── repeating_patterns.jpg
└── .github/workflows/
    └── publish_to_PPA.yml    leftover from the Debian packaging
```

### Files the package installs

| Path | What it is |
| --- | --- |
| `/usr/share/wallpapers/UniOS/contents/images/` | every image in `resources/`, except the logo |
| `/usr/share/wallpapers/UniOS/metadata.json` | names the wallpaper pack **UniOS Wallpapers** |
| `/usr/share/pixmaps/unios.png` | the UniOS logo |
| `/usr/share/icons/hicolor/.../apps/` | the logo as `unios`, `start-here-kde` and `distributor-logo` |
| `/etc/xdg/kdeglobals` | Breeze Dark look and feel, color scheme and icons |
| `/etc/xdg/plasmarc` | Breeze Dark Plasma theme |
| `/etc/skel/.config/plasma-welcome-appletsrc` | hides the Welcome Center for new users |
| `/etc/skel/.config/kded_plasma_welcomerc` | stops the Welcome Center daemon module for new users |
| `/usr/lib/unios/unios-plasma-setup.sh` | the login setup script |
| `/etc/xdg/autostart/unios-plasma-setup.desktop` | runs the setup script on login |
| `/etc/xdg/autostart/org.kde.plasma-welcome.desktop` | hides the Welcome Center autostart entry |

For example, `/etc/xdg/kdeglobals` looks like this:

```ini
[KDE]
LookAndFeelPackage=org.kde.breezedark.desktop

[General]
ColorScheme=BreezeDark

[Icons]
Theme=breeze-dark
```

### The setup script

`unios-plasma-setup.sh` uses `qdbus6` (or `qdbus`, if that's what's available) to talk to `plasmashell`. It tries for up to 15 seconds until Plasma answers, then runs a Plasma script that:

* sets `/usr/share/wallpapers/UniOS/contents/images/default.jpg` on every desktop
* finds every Kickoff, Kicker or app menu widget on every panel and sets `/usr/share/pixmaps/unios.png` as its icon

Finally it applies the wallpaper once more with `plasma-apply-wallpaperimage`. It runs in autostart phase 2, after the desktop and panels have loaded, and it doesn't write anything outside of Plasma's own config.

## Adding a Wallpaper

1. Put the image in `resources/wallpapers/`. `.jpg`, `.jpeg`, `.png` and `.webp` files are picked up.
2. Don't put `logo` in its name; those files are treated as the logo and left out of the wallpapers.
3. To change the wallpaper that is set on login, replace `default.jpg`, since that name is hardcoded in the setup script.
4. Bump `pkgrel` in the `PKGBUILD` (or `pkgver`, and reset `pkgrel` to `1`) so users get the update.

## Changing the Logo

Replace `resources/logos/unios.png`. The first file named `unios.png`, or with `logo` in its name, is used, so keep a single one in `resources/`.

## Recent Changes

* UniOS moved to Arch, so the Debian packaging and the Launchpad PPA were dropped in favour of a `PKGBUILD`. The `publish_to_PPA.yml` workflow is still in the repository, but it can no longer build anything without the `debian/` folder.
* Wallpapers and the logo moved to `resources/wallpapers/` and `resources/logos/`, and new wallpapers were added.
* The Plasma Welcome Center is now hidden through its autostart entry and the `/etc/skel` defaults.

## Contributors

Maintained by [Open Source UoM](https://github.com/open-source-uom), with contributions from:

<a href="https://github.com/open-source-uom/unios-desktop-settings/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=open-source-uom/unios-desktop-settings" />
</a>

unios-desktop-settings is part of the [UniOS project](https://unios-project.eu). Its source code is on [GitHub](https://github.com/open-source-uom/unios-desktop-settings), and changes follow the [General Dev Workflow](generalworkflow.md).
