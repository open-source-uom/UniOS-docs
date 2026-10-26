# unios-repo

`unios-repo` is the pacman repository that hosts all of the UniOS packages. Its code lives in [unios-pkgs](https://github.com/open-source-uom/unios-pkgs) and it is served from `packages.unios-project.eu`.

## Adding it to your system

UniOS comes with `unios-repo` already enabled. If you want to add it to another Arch-based system, add the following to `/etc/pacman.conf`:

```ini
[unios-repo]
SigLevel = Optional TrustAll
Server = https://packages.unios-project.eu/packages/$arch
```

Then update your system and install the packages you want, for example:

```bash
sudo pacman -Syu unios-keyring unidesk
```

## Nightly channel

There is also a testing channel, `unios-repo-nightly`, hosted in [unios-pkgs-nightly](https://github.com/open-source-uom/unios-pkgs-nightly) and served from `https://nightly.unios-project.eu/packages/$arch`. Only use it if you are testing changes before they reach `unios-repo`.

## Adding packages

Packages are built and uploaded to `unios-repo` through our build server, see [Our build server](build.unios-project.eu.md).
