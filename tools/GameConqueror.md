
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

## Removing the password prompt

WIP

- [Reddit: Is it possible to run a program requiring Linux password in gaming mode?](https://www.reddit.com/r/steamdeck_linux/comments/w9utc4/is_it_possible_to_run_a_program_requiring_linux/)
- [How to (reasonably) safely allow running specific commands as root without a password](https://www.reddit.com/r/SteamDeck/comments/11zu3hl/how_to_reasonably_safely_allow_running_specific/)
- [Sudoers Manual](https://www.sudo.ws/docs/man/1.7.10/sudoers.man/)

<!--
(This does not appear to work)

Write the following to the file `/etc/sudoers.d/gameconqueror

```sudoers
Cmnd_Alias GAMECONQUEROR = /usr/bin/gameconqueror
deck ALL=(ALL) NOPASSWD:GAMECONQUEROR
```

<!-- - ->

### Cleanup

To remove this file and this setting:

```
sudo rm /etc/sudoers.d/gameconqueror
```

<!-- ----------

Update: You can also specify checksums which are useful if you want to safely run scripts or binaries that the deck user has permission to modify. For example

Cmnd_Alias NEXTDNS = sha256:8873b1106aa830946923a33815c1c01449c62a43c4680c8447d2c6fca5c28dd6 /home/deck/.local/bin/nextdns

---------- -->

## Troubleshooting

Did you install using `sudo pacman -S gameconqueror` and it failed? Remove it with (from [here](https://linux-packages.com/arch-linux/package/gameconqueror))

```
sudo pacman -Rcns gameconqueror
```
