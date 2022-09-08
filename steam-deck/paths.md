
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
