
Steam Deck ([Official site](https://store.steampowered.com/steamdeck))

## Operating system

- Arch Linux ([FAQ](https://wiki.archlinux.org/title/Frequently_asked_questions), [User Repository](https://aur.archlinux.org/))
- Command line package manager: `pacman` ([Guide](https://wiki.archlinux.org/title/pacman), [CLI Reference](https://archlinux.org/pacman/pacman.8.html))

## Steam Deck general

- [Paths](/steam-deck/paths.md)
- [Tips](/steam-deck/tips.md)

## Tools

- [Decky](https://github.com/SteamDeckHomebrew/decky-loader) - Adds a menu that can install plugins that add functionality.
  - [Plugin DB](https://github.com/SteamDeckHomebrew/decky-plugin-database)

## Games

----

## Folders of interest

| Note | Path |
| ---- | ---- |
| Steam root folder | `/home/deck/.steam/steam/` |
| Proton root of virtual C drive | `/home/deck/.local/share/Steam/steamapps/compatdata/{{Steam App ID}}/pfx/drive_c/` |
| Example | `/home/deck/.local/share/Steam/steamapps/compatdata/251730/pfx/drive_c/users/steamuser/Documents/Almost Human/Legend of Grimrock 2` | 
| Proton virtual windows user home folder | `/home/deck/.local/share/Steam/steamapps/compatdata/{{Steam App ID}}/pfx/drive_c/users/steamuser/` |
| Example | `/home/deck/.local/share/Steam/steamapps/compatdata/251730/pfx/drive_c/users/steamuser/Documents/Almost Human/Legend of Grimrock 2/` |
| SD Card root | `/run/media/mmcblk0p1` |

Related notes
- [How to get the Steam `App ID`](https://gaming.stackexchange.com/questions/149837/how-do-i-find-the-id-for-a-game-on-steam)

Here are some paths after copying the `steamapps` folder to the SD card and creating a symlink in the old location, like I did. If you don't know what this means, ignore this table.

| Note | Path |
| ---- | ---- |
| Game data on the SD card | `/run/media/mmcblk0p1/steamapps/common/{{Game Name}}` |
| Example |  `/run/media/mmcblk0p1/steamapps/common/Legend of Grimrock 2/` |

## Tips and tricks

### Steam Deck Desktop Mode

The steam deck is closer to a computer than a console. It has a whole desktop environment, just like your PC. To get to this, you follow the [instrucitons on the Steam Deck page](https://help.steampowered.com/en/faqs/view/671A-4453-E8D2-323C#:~:text=How%20do%20I%20get%20to%20the%20desktop%3F)

> **From the STEAM menu, select Power, then Switch to Desktop**
