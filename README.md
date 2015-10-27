# RViGuide

A guide to make a Raspberry Pi 2 &amp; Raspbian blind friendly.

## Download the base image

(If there is a newer release of Debian Wheezy it will probably work fine, Debian Jesse is not working as of writing this)

File: 2015-05-05-raspbian-wheezy.zip

SHA-1: CB799AF077930FF7CBCFAA251B4C6E25B11483DE

[Download .torrent](https://downloads.raspberrypi.org/raspbian/images/raspbian-2015-05-07/2015-05-05-raspbian-wheezy.zip.torrent)

[Direct Download](https://downloads.raspberrypi.org/raspbian/images/raspbian-2015-05-07/2015-05-05-raspbian-wheezy.zip)

## Write the image to a Micro SD

###Linux

```bash
sudo dd bs=1m if=<your image file>.img of=/dev/sdX
```

### Windows

Use [win32diskimager](http://sourceforge.net/projects/win32diskimager/).

## Raspbian Modifications

Make sure you exand the file system when prompted on your first startup.

### Install Piespeakup, Prerequisites and Necessary cli programs

```bash
sudo apt-get update
sudo apt-get install git make gcc zsh espeak espeak-data libespeak1 libsonic0 
```

#### Piespeakup Setup

```bash
git clone https://github.com/cromarty/ttsprojects.git

cd ttsprojects/raspberry-pi/libilctts/build

sudo ./build.sh

cd ../../piespeakup

sudo ./build.sh

cd ../../../

rm -rf ttsprojects

rm -rf /home/pi/python_games

sudo chmod -x /etc/init.d/espeakup

```

#### Change keyboard layout (Default is UK) (Optional)

```bash
sudo dpkg-reconfigure keyboard-configuration
```

### Shell optimisation

#### Bash 

##### Editing .bashrc

```bash

echo '' >> /home/pi/.bashrc

echo 'PS1="bash, \w: "' >> /home/pi/.bashrc

echo "amixer cset numid=3 1 > /dev/null" >> /home/pi/.bashrc

echo "alias play='mplayer -quiet'" >> /home/pi/.bashrc

```

#### Zsh

##### Oh My Zsh

```bash

sh -c "$(wget https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"

```

edit ~/.oh-my-zsh/themes/robbyrussell.zsh-theme and replace the unicode arrow with the word that is to be said before each zsh prompt, i like using sh or zsh.

##### Editing .zshrc

```bash

echo '' >> /home/pi/.zshrc

echo "amixer cset numid=3 1 > /dev/null" >> /home/pi/.zshrc

echo "alias play='mplayer -quiet'" >> /home/pi/.zshrc

```

### Enable Autologin

Edit /etc/inittab as root and replace '1:2345:respawn:/sbin/getty 115200 tty1' with '1:2345:respawn:/bin/login -f pi tty1 </dev/tty1 >/dev/tty1 2>&1'

```bash

cd ~

touch .hushlogin

```




