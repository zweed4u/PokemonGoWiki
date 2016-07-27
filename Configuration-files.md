## Usage (up-to-date)
  1. copy `config.json.example` to `config.json` and `release_config.json.example` to `release_config.json`
  2. Edit `config.json` and replace `auth_service`, `username`, `password`, `location` and `gmapkey` with your parameters (other keys are optional, check `Advance Configuration` below)
  3. Simply launch the script with : `./run.sh` or `./pokecli.py` or `python pokecli.py --config-file ./configs/config.json` if you want to specify a config file

## Advanced Configuration
|      Parameter     | Default |                                                                                         Description                                                                                         |
|------------------|-------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `max_steps`        | 5       | The steps around your initial location (DEFAULT 5 mean 25 cells around your location) that will be explored                                                                                 |
| `mode`             | all     | Set farming Mode for the bot ('all', 'poke', 'farm'). 'all' means both spinning Pokéstops and catching Pokémon; 'poke' means only catching Pokémon and 'farm' means only spinning Pokéstops |
| `walk`             | 4.16    | Set the walking speed in kilometers per hour. (14 km/h is the maximum speed for egg hatching)                                                                                               |
| `debug`            | false   | Let the default value here except if you are developer                                                                                                                                      |
| `test`             | false   | Let the default value here except if you are developer                                                                                                                                      |
| `initial_transfer` | false   | Set this to true to transfer your Pokémon at the beginning of the run based on your release config                                                                                          |
| `location_cache`   | true    | Bot will start at last known location if you do not have location set in the config                                                                                                         |
| `distance_unit`    | km      | Set the unit to display distance in (km for kilometers, mi for miles, ft for feet)                                                                                                          |
| `item_filter`      |         | Pass a list of unwanted items (in json format) to recycle when collected at a Pokestop                                                                                                      |
| `evolve_all`       | NONE    | Set to true to evolve Pokémon if possible, takes Pokémon as an argument as well.                                                                                                            |
| `evolve_speed`     | 20      | Set the speed between each evolves in seconds. (Defaults to 3.7 seconds if not set)                                                                                                         |
| `cp_min`           | 300     |                                                                                                                                                                                             |
| `use_lucky_egg`    | false   | Use lucky egg to boost xp loot                                                                                                                                                              |
| `evolve_captured`  | false   | Evolve Pokémon after capturing                                                                                                                                                              |

## Catch Configuration
Default configuration will capture all Pokémon.
```"any": {"catch_above_cp": 0, "catch_above_iv": 0, "logic": "or"}```
You can override the global configuration with Pokémon-specific options, such as:
```"Pidgey": {"catch_above_cp": 0, "catch_above_iv": 0.8", "logic": "and"}```
to only capture Pidgey with a good roll.
Additionally, you can specify always_capture and never_capture flags. For example:
```"Pidgey": {"never_capture": true}```
will stop catching Pidgey entirely.

## Release Configuration
Default configuration will not release any Pokémon.
```"any": {"release_below_cp": 0, "release_below_iv": 0, "logic": "or"}```
You can override the global configuration with Pokémon-specific options, such as:
```"Pidgey": {"release_below_cp": 0, "release_below_iv": 0.8", "logic": "or"}```
to only release Pidgey with bad rolls.
Additionally, you can specify always_release and never_release flags. For example:
```"Pidgey": {"always_release": true}```
will release all Pidgey caught.

### Evolve All Configuration
    By setting the `evolve_all` attribute in config.json, you can instruct the bot to automatically
    evolve specified Pokémon on startup. This is especially useful for batch-evolving after popping up
    a lucky egg (currently this needs to be done manually).
    
    The evolve all mechanism evolves only higher IV/CP Pokémon. It works by sorting the high CP Pokémon (default: 300 CP or higher)
    based on their IV values. After evolving all high CP Pokémon, the mechanism will move on to evolving lower CP Pokémon
    only based on their CP (if it can).
    It will also automatically transfer the evolved Pokémon based on the release configuration.
    
    Examples on how to use (set in config.json):
    
    1. "evolve_all": "all"
      Will evolve ALL Pokémon.
    2. "evolve_all": "Pidgey,Weedle"
      Will only evolve Pidgey and Weedle.
    3. Not setting evolve_all or having any other string would not evolve any Pokémon on startup.
    
    If you wish to change the default threshold of 300 CP, simply add the following to the config file:
    	"cp_min": <number>