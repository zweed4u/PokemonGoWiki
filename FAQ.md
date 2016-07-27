### What's IV?
Here's the [introduction](http://bulbapedia.bulbagarden.net/wiki/Individual_values)

### Does it run automatically?
Not yet, still need a trainer to train the script param. But we are very close to.
### Set GEO Location
It works, use "location": "59.333409,18.045008", in configs/config.json to set lat long for location.
### Google login issues (Login Error, Server busy)?

Try to generate an [app password](!https://support.google.com/accounts/answer/185833?hl=en) and set is as
```
-p "<your-app-password>"
```
This error mostly occurs for those who are using 2 factor authentication, but either way, for the purpose of security it would be nice to have a separate password for the bot app.


### FLEE
The status code "3" corresponds to "Flee" - meaning your Pokemon has ran away.
   {"responses": { "CATCH_POKEMON": { "status": 3 } }
### My pokemon are not showing up in my Pokedex?
Finish the tutorial on a smartphone. This will then allow everything to be visible.
### How can I maximise my XP per hour?
Quick Tip: When using this script, use a Lucky egg to double the XP for 30 mins. You will level up much faster. A Lucky egg is obtained on level 9 and further on whilst leveling up. (from VipsForever via /r/pokemongodev)
### How do I use the map??
You can either view the map via opening the html file, or by serving it with SimpleHTTPServer (runs on localhost:8000)  
To use SimpleHTTPServer:  
```$ python -m SimpleHTTPServer [port]```
The default port is 8000, you can change that by giving a port number.
Anything above port 1000 does not require root.
You will need to set your username(s) in the userdata.js file before opening:  
Copy userdata.js.example to userdata.js and edit with your favorite text editor.
put your username in the quotes instead of "username"
If using multiple usernames format like this:  
```var users = ["username1","username2"];```