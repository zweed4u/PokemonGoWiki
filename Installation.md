## Mac Installation
There has been lots of people reporting the same if not similar errors when trying to setup the current codebase on Mac.

**Install PIP**

Navigate to: https://pip.pypa.io/en/stable/installing/

Right-click > save as the `get-pip.py` file - save to desktop

`cd /path/to/Desktop`

`sudo python get-pip.py`

**Install Homebrew**

`/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`


**Install virtualenv**

`cd /path/to/PokemonGo-Bot`

`sudo pip install virtualenv`

`virtualenv venv`

`source venv/bin/activate`

**Install prerequisite files**

`brew update && brew install --devel protobuf`

`sudo pip install -r requirements.txt`


***

## Windows Installation

## Linux Installation

#### Master Branch  
`sudo git clone -b master https://github.com/PokemonGoF/PokemonGo-Bot
cd PokemonGo-Bot
sudo pip install -r requirements.txt
sudo git submodule init
sudo git submodule update`

#### Dev Branch  