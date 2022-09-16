
- Download [CheatEngine](https://www.cheatengine.org/downloads.php)
- Install [Bottle](/tools/Bottle.md)
- Find out where your bottles are. You may customize it if you want.
  - Hamburger menu -> Preferences -> Advanced -> Custom Bottles Path
  - `/run/media/mmcblk0p1/bottle`
- Create a new bottle (Plus in upper left)
- Name it whatever. Recommend `Cheat Engine`

## References

From [Source](https://www.reddit.com/r/SteamDeck/comments/u5z8vw/comment/i56k2fg/)

> CheatEngine works pretty ok under wine/proton on desktop, so shouldn't be that different.

> The only trick (ehm) is that you need to run it inside the same proton/wine "prefix" as the game (the data stored under compdata for each game). While that's mostly just setting some environment variables, if you know what to do, it's just very simple to do with protontricks:

> `protontricks -c /path/to/cheatengine-x86_64.exe APPIP`

> where APPID is the numeric id of the game (you can search installed games with protontricks -s "name...", or use steamdb or similar site)

> I don't remember if it comes with an installer or if you just unpack a zip, but I'm sure you don't have to install it into each game's prefix, just unpack/install it somewhere in your system, than run it through that protontricks command so it has access to the game's processes


