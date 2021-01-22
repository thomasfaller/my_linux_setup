# my_linux_setup

This is intended to be for my personal use. Whenever I need to setup a new machine for all dev things.

## Pop!_OS
> Mostly taken from note: those steps are taken from https://mutschler.eu/linux/install-guides/pop-os-btrfs/

### After install

```bash
sudo sed -i 's/us./uk./' /etc/apt/sources.list
sudo local-gen en_IE.UTF.8
sudo local-gen en_GB.UTF.8
sudo update-locale LANG=en_IE.UTF-8
sudo apt update
sudo apt upgrade
sudo apt dist-upgrade
sudo apt autoremove
sudo fwupdmgr get-devices
sudo fwupdmgr get-updates
sudo fwupdmgr update
sudo reboot now
```

### Utilities
> some usefull tools
```bash
sudo apt install tree htop neofetch stress speedtest-cli -y
```

### ZSH + Oh My ZSH + Starship

```bash
# zsh
sudo apt install zsh -y
# oh-my-zsh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
# starship
curl -fsSL https://starship.rs/install.sh | bash
echo "\n# Starship Shell\neval \"$(starship init zsh)\"" >> ~/.zshrc
```


### Docker

```bash
# Replace lsb_release -cs with the correct release if using on an unsuported version .ie 20.10
sudo apt-get remove docker docker-engine docker.io containerd runc
sudo apt-get update
sudo apt-get install apt-transport-https ca-certificates curl gnupg-agent software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
sudo apt-get update
sudo apt-get install docker-ce docker-compose docker-ce-cli containerd.io
sudo groupadd docker
sudo usermod -aG docker $USER
newgrp docker
```

### Node + npm

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.0/install.sh | zsh
nvm install node
nvm install --lts
nvm use --lts
```

### Python Package Manager + Env
> installed normally by default but just in case
```
sudo apt install -y build-essential libssl-dev libffi-dev python3-dev
sudo apt install python3-pip -y
sudo apt install -y python3-venv
```

### AWS CLI Version 2

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
aws configure
```

### AWS SAM CLI (without Homebrew)
> see Github issue [here](https://github.com/aws/aws-sam-cli/issues/1424)

```bash
pip install aws-sam-cli
```


## Fixes

### Steps to fix the bcmwl-kernel-source failed to build on kernel 5.8
> Not sure it's a huge deal but Pop!_OS seems to have difficulties installing he proper drivers for my Fenvi WiFi card.


```bash
sudo apt remove --auto-remove bcmwl-kernel-source && \
sudo apt purge --auto-remove bcmwl-kernel-source && \
wget http://archive.ubuntu.com/ubuntu/pool/restricted/b/bcmwl/bcmwl-kernel-source_6.30.223.271+bdcom-0ubuntu7_amd64.deb $HOME/bcwl_drivers && \
sudo dpkg -i $HOME/bcwl_drivers/bcmwl-kernel-source_6.30.223.271+bdcom-0ubuntu7_amd64.deb
```