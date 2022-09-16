
- Download [CheatEngine](https://www.cheatengine.org/downloads.php)
- Install [Bottle](/tools/Bottle.md)
- Find out where your bottles are. You may customize it if you want.
  - Hamburger menu -> Preferences -> Advanced -> Custom Bottles Path
  - To put it on your SD card, use: `/run/media/mmcblk0p1/bottle`
- Create a new bottle (Plus in upper left)
- Name it whatever. (Recommend `Cheat Engine`)
- Click Create and wait. (This typically takes less than 1 minute from my experience.)
- A new bottle should now show up in the list. The one you just created. Click on it.
- At the top of Details & Utilities, Click Run Executable
- Go to the Cheat Engine installer, select it, and click Run.
- Step through the installer, being careful not to install the extras (Likely harmless under Linux, but no need to risk it)
- Once the installer finishes, some entries should appear under Programs. You want `Cheat Engine` with the space. (`CheatEngine` is the help docs)

Now, if you launch Cheat Engine from this, it will run, but it will not work. It's not running in a games Proton container, like it needs to be. We have some more steps to take.

- Locate the Cheat Engine executable.
  - Under your Bottle Root (from above) it will be here: `Cheat-Engine/drive_c/Program Files/Cheat Engine 7.4/cheatengine-x86_64.exe`
  - If you use your SD card, like me, this is the full path: `/run/media/mmcblk0p1/bottle/Cheat-Engine/drive_c/Program Files/Cheat Engine 7.4/cheatengine-x86_64.exe`

```
protontricks -c /path/to/cheatengine-x86_64.exe {{APPIP}}
```



## References

Fro [StackOverflow: How do I find the ID for a game on Steam?](https://gaming.stackexchange.com/questions/149837/how-do-i-find-the-id-for-a-game-on-steam)

[steamdb](https://steamdb.info/)

Or

> Go to the game's store page and check the URL. The last number in the URL is the application ID. All the store URLs are in format store.steampowered.com/app/APPID, so for Wasteland 2, the URL is http://store.steampowered.com/app/240760/, and appID 240760.

-----

From [Reddit: How to use Cheat Engine on the Steam Deck](https://www.reddit.com/r/SteamDeck/comments/u5z8vw/comment/i56k2fg/)

> CheatEngine works pretty ok under wine/proton on desktop, so shouldn't be that different.

> The only trick (ehm) is that you need to run it inside the same proton/wine "prefix" as the game (the data stored under compdata for each game). While that's mostly just setting some environment variables, if you know what to do, it's just very simple to do with protontricks:

> `protontricks -c /path/to/cheatengine-x86_64.exe APPIP`

> where APPID is the numeric id of the game (you can search installed games with protontricks -s "name...", or use steamdb or similar site)

> I don't remember if it comes with an installer or if you just unpack a zip, but I'm sure you don't have to install it into each game's prefix, just unpack/install it somewhere in your system, than run it through that protontricks command so it has access to the game's processes
