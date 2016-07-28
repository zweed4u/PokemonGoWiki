### Quickguide to install and run PokemonGo-Bot

1. Install Python 2.7.x and all the requirements listed below.
2. Clone the git repository and install the other python dependencies with pip.
3. Copy and rename the example config file in the config directory.
4. Run bot (in the project folder) with `python pokecli.py --config configs/config.json`.

### Requirements (click each one for install guide)

- [Python 2.7.x](http://docs.python-guide.org/en/latest/starting/installation/)
- [pip](https://pip.pypa.io/en/stable/installing/)
- [git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
- [virtualenv](https://virtualenv.pypa.io/en/stable/installation/) (Optional)
- [docker](https://docs.docker.com/engine/installation/) (Optional) - [how to setup after installation](https://github.com/PokemonGoF/PokemonGo-Bot/wiki/How-to-run-with-Docker)
- [protobuf 3](https://github.com/google/protobuf) (OS Dependent, see below)

You need to install the protobuf library for python. Please choose a method according to your os.

- OS X:  `brew update && brew install --devel protobuf`
- Windows: Download protobuf 3.0: [here](https://github.com/google/protobuf/releases/download/v3.0.0-beta-4/protoc-3.0.0-beta-4-win32.zip) and unzip `bin/protoc.exe` into a folder in your PATH.
- Debian/Ubuntu linux: `apt-get install python-protobuf`
- Arch linux: `pacman -S git python2 python2-pip python2-protobuf`

### Note on branch
Please keep in mind that master is not always up-to-date whereas 'dev' is. In the installation note below change `master` to `dev` if you want to get and use the latest version.

## Update
To update your project do (in the project folder): `git pull`
and after that update python requirement packages (in the project folder): `pip install --upgrade -r requirements.txt`

### Installation Linux
(change master to dev for the latest version)

```
$ git clone --recursive -b master https://github.com/PokemonGoF/PokemonGo-Bot  
$ cd PokemonGo-Bot  
$ pip install -r requirements.txt
```

### Installation Mac
(change master to dev for the latest version)

```
$ git clone --recursive -b master https://github.com/PokemonGoF/PokemonGo-Bot  
$ cd PokemonGo-Bot  
$ virtualenv .  
$ source bin/activate  
$ pip install -r requirements.txt
```

### Installation Windows
(change master to dev for the latest version)

On Windows, you will need to install PyYaml through the installer and not through requirements.txt.

##### Windows vista, 7, 8:
Go to : http://pyyaml.org/wiki/PyYAML , download the right version for your pc and install it

##### Windows 10:
Go to [this](http://www.lfd.uci.edu/~gohlke/pythonlibs/#pyyaml) page and download: PyYAML-3.11-cp27-cp27m-win32.whl   
(If running 64-bit python or if you get a 'not a supported wheel on this platform' error,
download the 64 bit version instead: PyYAML-3.11-cp27-cp27m-win_amd64.whl )

*(Run the following commands from Git Bash.)*

```
// switch to the directory where you downloaded PyYAML
$ cd download-directory
// install 32-bit version
$ pip2 install PyYAML-3.11-cp27-cp27m-win32.whl
// if you need to install the 64-bit version, do this instead:
// pip2 install PyYAML-3.11-cp27-cp27m-win_amd64.whl
```

After this, just do:

```
$ git clone -b master https://github.com/PokemonGoF/PokemonGo-Bot  
$ cd PokemonGo-Bot  
$ pip2 install -r requirements.txt
$ git submodule init
$ git submodule update
```

### First run

Copy and rename the file `config.json.example` in the `config/` folder to `config.json` and edit the values.
After that you can run the bot (in the project folder) with `python pokecli.py --config configs/config.json`.

You can read more about configuration files and values [here](https://github.com/PokemonGoF/PokemonGo-Bot/wiki/Configuration-files).