
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
- [Polkit Docs](https://wiki.archlinux.org/title/Polkit)

<!-- ----------

(The below does not appear to make it not require a password to launch.)

~~And add an entry to your Sudoers file so it does not require a password to launch.~~

```
echo "${USER} ALL = (root) NOPASSWD: $( which gameconqueror )" | sudo tee /etc/sudoers.d/gameconqueror
```

~~And make sure this file looks good~~

```
sudo cat /etc/sudoers.d/gameconqueror
```

~~Which should look something like~~

```
deck ALL = (root) NOPASSWD: /usr/bin/gameconqueror
```

### Cleanup

To remove this file and this setting:

```
sudo rm /etc/sudoers.d/gameconqueror
```

---------- -->

## Troubleshooting

Did you install using `sudo pacman -S gameconqueror` and it failed? Remove it with (from [here](https://linux-packages.com/arch-linux/package/gameconqueror))

```
sudo pacman -Rcns gameconqueror
```
