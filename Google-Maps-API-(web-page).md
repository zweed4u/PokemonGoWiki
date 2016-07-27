The webpage is a submodule to this repository and config related to that is in ./web folder

[OpenPoGoWeb] (https://github.com/OpenPoGo/OpenPoGoWeb) uses Google Maps. Read their [README] (https://github.com/OpenPoGo/OpenPoGoWeb/blob/master/README.md) for how to configure web frontend

### Additional info
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