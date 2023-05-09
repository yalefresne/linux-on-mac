# linux-on-mac
Somes tips and trick to install and config a linux distrib on mac

# Install wifi driver
```bash
sudo dnf install https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
sudo dnf install akmod-wl
reboot
```

# Install displayLink driver
source: https://www.reddit.com/r/Fedora/comments/yxkm3w/fedora_37_anybody_know_how_to_get_displaylink_to/
```bash
sudo dnf -y upgrade --refresh
sudo dnf -y install dkms libdrm-devel openssl
sudo openssl req -new -x509 -newkey rsa:2048 -keyout MOK.priv -outform DER -out \ MOK.der -nodes -days 36500 -subj "/CN=Displaylink/"
sudo mkdir /usr/src/evdi-1.12.0/
mkdir displaylink && cd displaylink
git clone https://github.com/DisplayLink/evdi
chmod a+x -R evdi/module/
sudo cp evdi/module/* usr/src/evdi-1.12.0/
sudo dkms build -m evdi -v 1.12.0
sudo dkms install -m evdi -v 1.12.0
```
To finish installation download file `driver/displaylink-driver-5.7.0-61.129.run` this repo and execute it.
Or you can find it on [synaptics site](https://www.synaptics.com/products/displaylink-graphics/downloads/ubuntu-5.7?filetype=exe)
```bash
chmod a+x displaylink-driver-5.7.0-61.129.run
sudo ./displaylink-driver-5.7.0-61.129.run
```
