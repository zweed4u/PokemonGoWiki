PokemonGo-Bot wiki!


## Softban
One can get softbanned by using the bot. The bot itself will usually tell you and exit. When softbanned, the player can't get loot from pokestops and all wild pokemons will always escape on the first try to catch.
Avoid teleporting, use the walking feature. Avoid switching between the bot and app too often. Sometimes the bot gets banned after running too long. 


I use this script to restart the bot after an hour, so the bot can run without the need to supervise it.
```bash
until (python pokecli.py); do
    echo "Process crashed with exit code $?.  Respawning.." >&2
    sleep 3600
done
```


For windows:
@echo off
:loop
cmd /k pokecli.py
timeout /t 3600 >null
taskkill /f /im cmd.exe >null
timeout /t 5 >null
goto loop