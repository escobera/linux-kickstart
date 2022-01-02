# Kickstart Manjaro Dev Machine

### Table of Contents
- [Kickstart Manjaro Dev Machine](#kickstart-manjaro-dev-machine)
    - [Table of Contents](#table-of-contents)
    - [Common Dependencies And Software](#common-dependencies-and-software)
    - [Git & Github](#git--github)
      - [Install Git & Configure SSH](#install-git--configure-ssh)
    - [Terminal & Shell](#terminal--shell)
      - [Konsole](#konsole)
      - [ZSH](#zsh)
    - [ASDF](#asdf)
      - [Install ASDF](#install-asdf)
    - [Visual Studio Code](#visual-studio-code)
    - [Dbeaver](#dbeaver)
    - [Docker](#docker)
    - [Postgresql 13](#postgresql-13)
    - [VPN](#vpn)
    - [Useful Commands](#useful-commands)

### Common Dependencies And Software
```sh
sudo pacman-mirrors --fasttrack && sudo pacman -Syyu
sudo pacman -S git curl zsh exa unzip base-devel yay docker docker-compose

# Make sure you have the Color option in your /etc/pacman.conf
yay -Y --gendb
yay -Syu --devel
yay -Y --devel --save
```

### Git & Github
#### Install Git & Configure SSH
1. [Generate SSH Key](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/)
2. [Add SSH Key to Github Account](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/)

### Terminal & Shell
#### Konsole
1. Install Dracula Theme
  Instruction [here](https://draculatheme.com/konsole)

#### ZSH
1. Change to Zsh
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
  alias l='exa --group-directories-first -l --git -a' 
  ```

### ASDF
#### Install ASDF

1. Install by cloning and sourcing (Note that the version number may differ)
  ``` sh
    git clone https://github.com/asdf-vm/asdf.git ~/.asdf --branch v0.9.0
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
  ASDF_CONCURRENCY=4 asdf install ruby 2.6.6
  asdf global ruby 2.6.6

  asdf install erlang 24.2
  asdf global erlang 24.2

  asdf install elixir 1.13.1-otp-23
  asdf global elixir 1.13.1-otp-24

  asdf install nodejs 12.22.8
  asdf global nodejs 12.22.8

  asdf install java adoptopenjdk-16.0.2+7
  asdf global java adoptopenjdk-16.0.2+7
  echo -e "\n. $HOME/.asdf/plugins/java/set-java-home.sh" >> ~/.zshrc
  ```
****

### Visual Studio Code
1. yay aur/visual-studio-code-bin
2. Install settings sync

### Dbeaver
1. Install via flatpak (add instructions)
2. Import project
   
### Docker
``` sh
# 1. configure service status
sudo systemctl start docker.service
sudo systemctl enable docker.service

# 2. create docker group & add your user
sudo usermod -aG docker $USER

```

> reboot after this

### Postgresql 13
```sh
sudo pacman -S postgresql
sudo su postgres -l
initdb --locale $LANG -E UTF8 -D '/var/lib/postgres/data/'
exit
sudo systemctl enable --now postgresql.service


# create users
sudo su postgres
createuser -W --interactive

# or 
sudo su postgres
psql
> CREATE ROLE 'role_name' WITH LOGIN SUPERUSER PASSWORD 'role_password';
> \q
```

### VPN
```sh
docker run -ti --privileged --rm --net=host -v /etc/resolv.conf:/etc/resolv.conf robertbeal/openconnect:latest --protocol=gp acessoremoto.tjdft.jus.br
```

or

```sh
yay globalprotect
```


### Useful Commands
``` sh
# list which processes listen on which TCP ports
netstat -tlnp
```
