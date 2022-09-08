
## Installing

Disable the filesystem read-only mode

```
sudo steamos-readonly disable
```

Install

```
sudo pacman -S gameconqueror
```

And for safety, enable read-only mode again

```
sudo steamos-readonly enable
```

## Troubleshooting

Did you install using `sudo pacman -S gameconqueror` and it failed? Remove it with (from [here](https://linux-packages.com/arch-linux/package/gameconqueror))

```
sudo pacman -Rcns gameconqueror
```
