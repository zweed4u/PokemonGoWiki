## Usage (up-to-date)
  1. copy `config.json.example` to `config.json` and `release_config.json.example` to `release_config.json`
  2. Edit `config.json` and replace `auth_service`, `username`, `password`, `location` and `gmapkey` with your parameters (other keys are optional, check `Advance Configuration` below)
  3. Simply launch the script with : `./run.sh` or `./pokecli.py` or `python pokecli.py -cf ./configs/config.json` if you want to specify a config file

## Advanced Configuration
|      Parameter     | Default |                                                                                         Description                                                                                         |
|------------------|-------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `tasks`            | []     | The behaviors you want the bot to do. Read [how to configure tasks](#configuring-tasks).
| `max_steps`        | 5       | The steps around your initial location (DEFAULT 5 mean 25 cells around your location) that will be explored                                                                              
| `forts.avoid_circles`             | False     | Set whether the bot should avoid circles |
| `forts.max_circle_size`             | 10     | How many forts to keep in ignore list |
| `walk`             | 4.16    | Set the walking speed in kilometers per hour. (14 km/h is the maximum speed for egg hatching)                                                                                               |
| `action_wait_min`   | 1       | Set the minimum time setting for anti-ban time randomizer
| `action_wait_max`   | 4       | Set the maximum time setting for anti-ban time randomizer
| `debug`            | false   | Let the default value here except if you are developer                                                                                                                                      |
| `test`             | false   | Let the default value here except if you are developer                                                                                                                                      |                                                                                       |
| `location_cache`   | true    | Bot will start at last known location if you do not have location set in the config                                                                                                         |
| `distance_unit`    | km      | Set the unit to display distance in (km for kilometers, mi for miles, ft for feet)                                                                                                          |                                                                                                    |
| `evolve_all`       | NONE    | Set to "all" to evolve Pokémon if possible when the bot starts. Can also be set to individual Pokémon as well as multiple separated by a comma. e.g "Pidgey,Rattata,Weedle,Zubat"                                                                                                           |
| `evolve_cp_min`           | 300   |                   Min. CP for evolve_all function             

## Configuring Tasks
The behaviors of the bot are configured via the `tasks` key in the `config.json`. This enables you to list what you want the bot to do and change the priority of those tasks by reordering them in the list. This list of tasks is run repeatedly and in order. For more information on why we are moving config to this format, check out the [original proposal](https://github.com/PokemonGoF/PokemonGo-Bot/issues/142).

### Task Options:
* CatchLuredPokemon
* CatchVisiblePokemon
* EvolveAll
  * `evolve_speed`: Default `20`
  * `use_lucky_egg`: Default: `False`
* FollowPath
  * `path_mode`: Default `loop` | Set the mode for the path navigator (loop or linear).
  * `path_file`: Default `NONE` | Set the file containing the waypoints for the path navigator. 
* FollowSpiral
* HandleSoftBan
* IncubateEggs
  * `longer_eggs_first`: Default `True`
* MoveToFort
* RecycleItems
  * `item_filter`: Pass a list of unwanted [items (using their JSON codes)](https://github.com/PokemonGoF/PokemonGo-Bot/wiki/Item-ID's) to recycle when collected at a Pokestop  
* SpinFort
* TransferPokemon

### Example configuration:
The following configuration tells the bot to transfer all the Pokemon that match the transfer configuration rules, then recycle the items that match its configuration, then catch the pokemon that it can, so on, so forth. Note the last two tasks, MoveToFort and FollowSpiral. When a task is still in progress, it won't run the next things in the list. So it will move towards the fort, on each step running through the list of tasks again. Only when it arrives at the fort and there are no other stops available for it to move towards will it continue to the next step and follow the spiral.

```
{
  // ...
  "tasks": [
    {
      "type": "TransferPokemon"
    }, 
    {
      "type": "RecycleItems"
    }, 
    {
      "type": "CatchVisiblePokemon"
    }, 
    {
      "type": "CatchLuredPokemon"
    }, 
    {
      "type": "SpinFort"
    }, 
    {
      "type": "MoveToFort"
    }, 
    {
      "type": "FollowSpiral"
    }
  ]
  // ...
}
```

### Specifying configuration for tasks
If you want to configure a given task, you can pass values like this:

```
{
  // ...
  "tasks": [
    {
      "type": "IncubateEggs",
      "config": {
        "longer_eggs_first": true
      }
    }
  ]
  // ...
}
```

### An example task configuration if you only wanted to collect items from forts:
```
{
  // ...
  "tasks": [
    {
      "type": "RecycleItems"
    },
    {
      "type": "SpinFortWorker"
    },
    {
      "type": "MoveToFortWorker"
    }
  ],
  // ...
}
```

## Catch Configuration
Default configuration will capture all Pokémon.

```"any": {"catch_above_cp": 0, "catch_above_iv": 0, "logic": "or"}```

You can override the global configuration with Pokémon-specific options, such as:

```"Pidgey": {"catch_above_cp": 0, "catch_above_iv": 0.8", "logic": "and"}``` to only capture Pidgey with a good roll.

Additionally, you can specify always_capture and never_capture flags.

For example: ```"Pidgey": {"never_capture": true}``` will stop catching Pidgey entirely.

## Release Configuration

### Common configuration

Default configuration will not release any Pokémon.

```"release": {"any": {"release_below_cp": 0, "release_below_iv": 0, "logic": "or"}}```

You can override the global configuration with Pokémon-specific options, such as:

```"release": {"Pidgey": {"release_below_cp": 0, "release_below_iv": 0.8, "logic": "or"}}``` to only release Pidgey with bad rolls.

Additionally, you can specify always_release and never_release flags. For example:

```"release": {"Pidgey": {"always_release": true}}``` will release all Pidgey caught.

### Keep the strongest pokemon configuration (dev branch)

You can set ```"release": {"Pidgey": {"keep_best_cp": 1}}``` or ```"release": {"any": {"keep_best_iv": 1}}```.

In that case after each capture bot will check that do you have a new Pokémon or not.

If you don't have it, it will keep it (no matter was it strong or weak Pokémon).

If you already have it, it will keep a stronger version and will transfer the a weaker one.

```"release": {"any": {"keep_best_cp": 2}}```, ```"release": {"any": {"keep_best_cp": 10}}``` - can be any number.

## Evolve All Configuration

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

```
"evolve_cp_min":  <number>
```

## Path Navigator Configuration

Setting the `navigator.type` setting to `path` allows you to specify waypoints which the bot will follow. The waypoints can be loaded from a GPX or JSON file. By default the bot will walk along all specified waypoints and then move directly to the first waypoint again. When setting `navigator.path_mode` to `linear`, the bot will turn around at the last waypoint and along the given waypoints in reverse order.

An example for a JSON file can be found in `configs/path.example.json`. GPX files can be exported from many online tools, such as gpsies.com.The bot loads the first segment of the first track.

