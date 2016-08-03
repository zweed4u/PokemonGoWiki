##Description
This task will fetch current pokemon spawns from /raw_data of an PokemonGo-Map instance.

For information on how to properly setup PokemonGo-Map have a look at the Github page of the project [here](https://github.com/AHAAAAAAA/PokemonGo-Map/).

There is an example config in `config/config.json.map.example`

##Configs
###address
address of the webserver of PokemonGo-Map

to test if this is correct copy&paste it into your browser and see if the map loads
###mode
* **distance:** will move to the nearest pokemon
* **priority:** will move to the pokemon with the highest priority assigned (tie breaking by distance)

###prioritize vips
will prioritize vips in distance and priority mode above all normal pokemon if set to true
###min_time:
minimum time the pokemon has to be available before despawn
###max_distance:
maximum distance the pokemon is allowed to be when walking, ignored when sniping
###snipe
* **enabled** will teleport to target pokemon, encounter it, teleport back then catch it
* **disabled** will walk normally to the pokemon

###update_map
disable/enable if the map location should be automatically updated to the bots current location
###catch
a dictionary of pokemon to catch with an assigned priority (higher => better)
vip pokemon are automatically catched without an entry here