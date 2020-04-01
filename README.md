# Kickstart Linux Mint
### Table of Contents
   1. [Common Dependencies](#common-dependencies)
   2. [Common Tools & Drivers](#common-tools--drivers)
   3. [Git & Github](#git--github)
   4. [Theme](#theme)
   5. [Neovim](#neovim)
   6. [Terminal & Shell](#terminal--shell)
   7. [Node.js](#nodejs)
   8. [Laravel](#laravel)
   9. [Visual Studio Code](#visual-studio-code)
   10. [Other Tools](#other-tools)
   11. [Docker](#docker)
   12. [MySQL](#mysql)
   13. [DigitalOcean](#digitalocean)
   14. [Useful Commands](#useful-commands)

### Common Dependencies And Software
```sh
sudo apt install curl net-tools python3-pip \
  spotify-client git vim sha256sum jq automake autoconf \
  libreadline-dev libncurses-dev libssl-dev libyaml-dev \
  libxslt-dev libffi-dev libtool unixodbc-dev unzip
 ```

### Common Tools & Drivers
#### Nvidia Driver
* *Driver Manager > Install Recommended Driver*

If resolution is strange after restart you probably need to: 
> `sudo apt remove xserver-xorg-video-fbdev`

### Git & Github
#### Install Git & Configure SSH
   1. [Generate SSH Key](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/)
   2. [Add SSH Key to Github Account](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/)

### Theme
#### Fonts
Source Code Pro
   ``` sh
   git clone --depth 1 --branch release https://github.com/adobe-fonts/source-code-pro.git ~/.fonts/adobe-fonts/source-code-pro
   fc-cache -f -v ~/.fonts/adobe-fonts/source-code-pro
   ```
### Terminal & Shell
#### Tilix
1. Install Tilix
   > `sudo add-apt-repository ppa:webupd8team/terminix`
   
   > `sudo apt update`
   
   > `sudo apt install tilix`
   
   1.1. To fix the vte warnings
   
   > `sudo ln -s /etc/profile.d/vte-2.91.sh /etc/profile.d/vte.sh` 
   
   1.2. And append to end of `.zshrc`

   ```sh
   if [ $TILIX_ID ] || [ $VTE_VERSION ]; then
   source /etc/profile.d/vte.sh
   fi
   ```

2. Install Dracula Theme
   ```sh
   curl -o ~/.config/tilix/schemes/Dracula.json --create-dirs https://raw.githubusercontent.com/dracula/tilix/master/Dracula.json
   ```

3. Customize Tilix Appearance
   * *Preferences > Profile > Color > Color scheme > Dracula*
4. Configure Tilix Keyboard Shortcuts (Optional)
   * *Preferences > Shortcuts > Replace **`Switch to next session`** shortcut with **`Alt+Right`***
   * *Preferences > Shortcuts > Replace **`Switch to previous session`** shortcut with **`Alt+Left`***
   * *Preferences > Shortcuts > Replace **`Paste`** shortcut with **`Ctrl+V`***
   * *Preferences > Shortcuts > Replace **`Resize the terminal down`** shortcut with **`Shift+Ctrl+Down`***
   * *Preferences > Shortcuts > Replace **`Resize the terminal up`** shortcut with **`Shift+Ctrl+Up`***
   * *Preferences > Shortcuts > Replace **`Resize the terminal right`** shortcut with **`Shift+Ctrl+Right`***
   * *Preferences > Shortcuts > Replace **`Resize the terminal left`** shortcut with **`Shift+Ctrl+Left`***
5. Configure System Keyboard Shortcuts (Optional)
   * *Keyboard Shortcuts > Remove Default Action for **`Ctrl+Alt+T`***
   * *Keyboard Shortcuts > Bind **`Ctrl+Alt+T`** to Custom Shortcut for Launching Tilix*
   * *Keyboard Shortcuts > Disable Shortcut for **`Hide all normal windows`***

#### ZSH
1. Install Zsh
   * `sudo apt install zsh`
   * `chsh -s $(which zsh)`
2. [ZimFW](https://github.com/zimfw/zimfw)
   * `curl -fsSL https://raw.githubusercontent.com/zimfw/install/master/install.zsh | zsh`
6. Add git aliases to `.zshrc`
   ```sh
   alias gp="git push"
   alias gl="git pull"
   alias g="git status"
   alias gca="git commit -a"
   alias gc="git checkout" 
   ```

### ASDF
#### Install ASDF


1. Install by cloning and sourcing (Note that the version number may differ)
   ``` sh
   git clone https://github.com/asdf-vm/asdf.git ~/.asdf --branch v0.7.8
   . $HOME/.asdf/asdf.sh
   ```
2. Add plugins
   ```sh
   asdf plugin add erlang
   asdf plugin add elixir
   asdf plugin add nodejs
   asdf plugin add ruby
   asdf plugin-add java https://github.com/halcyon/asdf-java.git

   # source nodejs keyring
   bash ~/.asdf/plugins/nodejs/bin/import-release-team-keyring
   ```

3. Add asdf script and completions to .zshrc
   ```sh
   echo -e "\n. $HOME/.asdf/asdf.sh" >> ~/.zshrc
   echo -e "\nfpath=(${ASDF_DIR}/completions $fpath)" >> ~/.zshrc
   echo -e "\nautoload -Uz compinit && compinit" >> ~/.zshrc
   ```

4. Install plugins (this may vary A LOT)
   ```sh
   ASDF_CONCURRENCY=4 asdf install ruby 2.6.5
   asdf global ruby 2.6.5

   # asdf install erlang 22.2.1
   # asdf global erlang 22.2.1

   # asdf install elixir 1.9.4
   # asdf global elixir 1.9.4

   # asdf install nodejs 12.14.0
   # asdf global nodejs 12.14.0
   ```

### Visual Studio Code
1. [Download the .deb package](https://code.visualstudio.com/docs/?dv=linux64_deb) 
2. Download Extensions
   - Appearance
      * Overnight (Slumber) *or* Night Owl 
      * Material Icon Theme
   - Editor
      * Vim
      * GitLens
      * EditorConfig for VS Code
   - Remote Development
      * Remote - SSH
      * Remote - SSH: Editing Configuration Files
      * Remote - SSH: Explorer
   - Web Development
      * REST Client
      * Auto Rename Tag
      * Live Server
   - JavaScript & TypeScript
      * Prettier ([prettierrc](./.prettierrc.yml))
      * ESLint (`npm install -g eslint`)
      * ES7 React/Redux/GraphQL/React-Native snippets
   - PHP
      * PHP Debug
      * PHP DocBlocker
      * PHP Intelephense
      * phpfmt - PHP formatter
      * Larevel Blade Snippets
   - Go
      * Go
   - Python
      * Python
      * AREPL for python
      * autoDocstring
   - Other
      * Docker
      * Create Files & Folders: On The Go
3. Copy the [settings file](vscode.settings.json) contents into `settings.json`

#### Shortcuts
| Shortcut | Description |
| -------- | ----------- |
| `Ctrl+B` | Toggle sidebar |
| `Ctrl+,` | Open settings |
<br>

### Other Tools
* [Peek](https://github.com/phw/peek)
   ```sh
   sudo add-apt-repository ppa:peek-developers/stable
   sudo apt update && sudo apt install peek
   ```
* [ag](https://github.com/ggreer/the_silver_searcher) & [sack](https://github.com/sampson-chen/sack)
   ``` sh
   # 1. install ag
   sudo apt install silversearcher-ag
   
   # 2. install sack
   git clone https://github.com/sampson-chen/sack.git && \ 
   cd sack && \ 
   chmod +x install_sack.sh && \
   ./install_sack.sh && \
   cd .. && \
   rm -rf sack
```
<br>

### Docker
``` sh
# 1. remove any older versions
sudo apt purge docker lxc-docker docker-engine docker.io

# 2. install prerequisites
sudo apt install apt-transport-https ca-certificates software-properties-common

# 3. import official GPG key & verify signature
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add

# 4. add docker respository
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

# 5. install docker
sudo apt update && sudo apt install docker-ce

# 6. verify service status
sudo systemctl status docker

# 7. create docker group & add your user
sudo groupadd docker
sudo usermod -aG docker $USER
```

> Log out and login back.

``` sh
# 8. verify that you can run this command without 'sudo'
docker run hello-world

# 9. install docker-compose 1.24.0 (better check newer versions)
sudo curl -L "https://github.com/docker/compose/releases/download/1.24.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

# 10. apply executable permission
sudo chmod +x /usr/local/bin/docker-compose
```

See [cheatsheet](./docker.md) for more info.

<br>

### MySQL
#### Download MySQL Docker Image
```sh
docker pull mysql:<tag>
```

#### Start MySQL Container
``` sh
# publish default port, provide a root password and start mysql
docker run --name <container_name> -p 3306:3306 -e MYSQL_ROOT_PASSWORD=<root_pw> mysql:<tag>
```

#### Connect to MySQL Server from within the Container
1. **Run the MySQL Client**
   ``` sh
   # check randomly generated password
   docker logs <container_name> 2>&1 | grep GENERATED

   # run the MySQL client within the MySQL Server container
   docker exec -it <container_name> mysql -uroot -p
   ```
   When prompted, paste the generated password obtained from the previous step.

2. **Reset Root Password**
   ``` sh
   ALTER USER 'root'@'localhost' IDENTIFIED BY '<new_password>';
   ```

#### Connect via Client
``` sh
# install client
sudo apt install mysql-client

# connect
mysql -h HOST -P PORT_NUMBER -u USERNAME -p
```

#### Backup & Restore
Backup & restore a particular database while MySQL container is running:
``` sh
# backup
docker exec <mysql_container_name> mysqldump \
   -u <username> --password=<password> <database_name> > <backup_file>.sql

# restore
cat <backup_file>.sql | docker exec -i <mysql_container_name> mysql \
   -u <username> --password=<password> <database_name>

# backup & compress
docker exec <mysql_container_name> mysqldump \
   -u <username> --password=<password> <database_name> | gzip -c > <backup_file>.sql.gz 

# decompress & restore
gzip -d -c <backup_file>.sql.gz | docker exec -i <mysql_container_name> mysql \
   -u <username> --password=<password> <database_name>
```

See [cheatsheet](https://gist.github.com/bradtraversy/c831baaad44343cc945e76c2e30927b3) for more info.
<br>

### DigitalOcean
1. Follow the [Initial Server Setup](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-18-04) guide.
2. Append public SSH keys of each client machine into the `~/.ssh/authorized_keys` file in droplet.

### Useful Commands
``` sh
# list which processes listen on which TCP ports
netstat -tlnp

# get lines of code in a particular language within a Git repository
git ls-files | grep '\.py$' | xargs wc -l
```
