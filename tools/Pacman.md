

## Troubleshooting

```
error: <package>: signature from "Someone <someone@example.com>" is marginal trust
:: File /var/cache/pacman/pkg/<package_name_version>_x86_64.pkg.tar.zst is corrupted (invalid or corrupted package (PGP signature)).
Do you want to delete it? [Y/n] 
```

https://bbs.archlinux.org/viewtopic.php?id=267364

```
pacman -Sy archlinux-keyring
pacman-key --populate archlinux
pacman-key --refresh-keys
pacman -Syu
```
