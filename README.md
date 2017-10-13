### 1. Install ZSH and Oh My ZSH

```bash
sudo apt-get install zsh
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

### 2. Install powerline font
It has been explained how to install the font [here](https://powerline.readthedocs.io/en/latest/installation/linux.html#fonts-installation) but it didn't work for me unless I used the following command line.

```bash
sudo apt-get install fonts-powerline
```
### 3. Configure ZSH
To configure ZSH you need to modify its configuration file by opening it with an editor like *nano* or *vim*.

```bash
nano ~/.zshrc
```

#### 3.1. Using Theme
Change the content of variable ```ZSH_THEME``` to whatever you like; look into the [offical themes](https://github.com/robbyrussell/oh-my-zsh/wiki/themes) and change the content of ```ZSH_THEME="robbyrussell"``` to the name of the theme.

```bash
ZSH_THEME="agnoster"
```

#### 3.2. Remove Username from Terminal
By default in the Terminal it is shown the username before the place you can write the command with something like ```user@host```. To remove it, it is just needed to add the following code to the end of the file ```~/.zshrc ```.

```bash
DEFAULT_USER=$USER
```


### 4. Change Theme colors to Solarize

```bash
sudo apt-get install dconf-cli
git clone git://github.com/sigurdga/gnome-terminal-colors-solarized.git ~/.solarized
cd ~/.solarized
./install.sh
```

To activate dark solarize theme in Terminal just right click on the terminal and then go to ```profile``` and after that go to ```Profile Preferences```. Then you need to go to the ```Colors``` tab and select ```Solarize Dark/Light``` form ```Built-in Schemes```.

### 5. Installing External Theme
You also can use external theme which needs to be installed before using; the way of installing is explained in its own repository. Look into them [here](https://github.com/robbyrussell/oh-my-zsh/wiki/External-themes). My choice is [Power Level 9k](https://github.com/bhilburn/powerlevel9k).

```bash
git clone https://github.com/bhilburn/powerlevel9k.git ~/.oh-my-zsh/custom/themes/powerlevel9k
```
Then you need to change the ``ZSH_THEME``` of the file ```~/.zshrc``` into ```powerlevel9k/powerlevel9k```.

```bash
ZSH_THEME="powerlevel9k/powerlevel9k"
```

### 6. Letting Terminal to Understand Farsi/Arabic Characters
First it is needed to install some packages which are explained below.

```bash
sudo apt update
sudo apt install libfribidi0 libfribidi-dev
wget https://launchpad.net/~behnam/+archive/ubuntu/ppa/+build/574787/+files/bicon_0.2.0-1ubuntu0~ppa4_amd64.deb
sudo dpkg -i bicon_0.2.0-1ubuntu0~ppa4_amd64.deb
rm bicon_0.2.0-1ubuntu0~ppa4_amd64.deb
```
Afterwards, it is needed to tell the Terminal to run ```bicon.bin```. To do so, it is needed to edit ```/usr/share/applications/gnome-terminal.desktop``` and add the following lines to the end of it.

```bash
Terminal=true
Exec=/usr/bin/bicon.bin
```

### 7. Installing [tmux](https://github.com/tmux/tmux/wiki)
For me, Tmux is the combination of Terminator and Screen.

```bash
sudo apt-get install tmux
```
#### 7.1. Cheatlist and Shortcuts of *tmux*
Here are the commands to manage *tmux*

Command | Explanation
--- | ---
tmux | Run tmux 
tmux new -s session_name | Start a new session
tmux ls | List Sessions
tmux kill-session -t session_name | Kill a session
tmux kill-session -a | Kill all sessions except the one is active
logout | Logout form the current pane/window (doesn't clsoe it)
exit | Close the current pane/window


And the shortcuts when *tmux* is run. Note is that ^ means *Control* key and *<alt>* means *Alt* key; *<command>* means to write a command and <0-9> means a digit between 0 and 9.

Shortcut | Explanation
--- | ---
^b : <command> | Run a command
^b s | List current sessions
^b $ | Rename the current session
^b c | Create a new window (tab)
^b w | List current windows (tabs)
^b <0-9> | Go to the window (tab) number 0 to 9
^b n | Move to the next window (tab)
^b p | Move to the previous window (tab)
^b f | Find a window (tab)
^b , | Rename a window (tab)
^b & | Kill a window (tab)
^b % | Split a window vertically to panes
^b " | Split a window horizontally to panes
^b x | Kill the active pane
^b <alt><arrow> | Change the size of the pane
^b ^<arrow> | Change the size of the pane
^b <arrow> | Switch between panes of a window (tab)
^b o | Switch between panes of a window (tab)
^b ^o | Swap panes
^b { | Move to the next pane of a window (tab)
^b } | Move to the previous pane of a window (tab)

#### 7.2. Changing the *tmux* Configuration File
To do so it is needed to create/modify a file in the home directory under the name of ```.tmux.conf```.

```bash
nano ~/.tmux.conf
```

For exmaple to change the default prefix which is ^b (or C-b or <ctrl>+b) to something else like ^a (or C-a or <ctrl>+a) which is used in *Screen* it is needed to unbind the current prefix and add the new one.
  
```bash
unbind C-b
set-option -g prefix C-a
bind C-a send-prefix
```
