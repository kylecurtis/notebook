## Upgrade the archlinux-keyring

> This step should be done before the install to prevent most signing errors. It will manually sync the package database and upgrade the [archlinux-keyring](https://archlinux.org/packages/?name=archlinux-keyring) package.
>
> [Arch Wiki](https://wiki.archlinux.org/title/Pacman/Package_signing#Upgrade_system_regularly)

```bash
pacman -Sy --needed archlinux-keyring
```