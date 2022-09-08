
- [Fluffy Mod Manager 5000 (Modding RE2RE/RE3RE) on Steam Deck](https://www.reddit.com/r/SteamDeck/comments/tvvic2/fluffy_mod_manager_5000_modding_re2rere3re_on/) (I could not get this working)
- REFramework [Github](https://github.com/praydog/REFramework) [Nexus Mods](https://www.nexusmods.com/monsterhunterrise/mods/26)
- [Getting REFramework working in MHR on the Steam Deck](https://www.reddit.com/r/SteamDeck/comments/uhb7ft/issues_with_game_modding_on_steam_deck_reframework/) (I had to do this to get it working.) RE: Add an override for the `dinput8.dll`

> - `/home/deck/.local/share/Steam/steamapps/compatdata/1446780/pfx/` (1446780 is the steam id of MHR)
> - open "user.reg" with a text editor.
> - Search for "Software\Wine\DllOverrides" (some editors need "Software\\Wine\\DllOverrides" to find it). Should be around line 740.
> - At the end of the list add this new line : "dinput8"="native,builtin"
