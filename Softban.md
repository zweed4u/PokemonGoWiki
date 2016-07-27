``PokemonGo-Bot wiki!

**stop softban - brute force way  (needs testing)**

1. make sure you have 40+ poke balls
2. set mode to "poke"
3. catch Pokemon (make sure to remove catching filter to speed this up)
4. Between 30-40 capture attempts your ban is gone

## Softban
One can get softbanned by using the bot. The bot itself will usually tell you and exit. When softbanned, the player can't get loot from pokestops and all wild pokemons will always escape on the first try to catch.
Avoid teleporting, use the walking feature. Avoid switching between the bot and app too often. Sometimes the bot gets banned after running too long. 


(?? is this for linux??)
```bash
until (python pokecli.py); do
    echo "Process crashed with exit code $?.  Respawning.." >&2
    sleep 3600
done
```

For windows use:
```bash
@echo off
:loop
cmd /k pokecli.py
timeout /t 3600 >null
taskkill /f /im cmd.exe >null
timeout /t 5 >null
goto loop
```