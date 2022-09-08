
Give Bottle access to the SD card ([docs](https://docs.usebottles.com/flatpak/expose-directories))

```
flatpak override --user --filesystem=/run/media/mmcblk0p1/  com.usebottles.bottles
flatpak override --user --filesystem=/run/media/  com.usebottles.bottles
```
