# RViGuide

A guide to make a Raspberry Pi 2 &amp; Raspbian blind friendly.

## Download the base image

(If there is a newer release of Debian Wheezy it will probably work fine, Debian Jesse is not working as of writing this)

File: 2015-05-05-raspbian-wheezy.img

SHA-1: FD11A319A8E93FC5F93902C67D337AD419706E5E

[Download .torrent](https://downloads.raspberrypi.org/raspbian/images/raspbian-2015-05-07/2015-05-05-raspbian-wheezy.zip.torrent)

[Direct Download](https://downloads.raspberrypi.org/raspbian/images/raspbian-2015-05-07/2015-05-05-raspbian-wheezy.zip)

## Write the image to a Micro SD

###Linux

Use dd

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
sudo apt-get upgrade
sudo apt-get install git make gcc zsh mplayer2 espeak espeak-data libespeak1 libsonic0 
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

In the file /etc/inittab add '--autologin pi' after '1:2345:respawn:/sbin/getty' and before '--noclear 38400 tty1'

```bash
sudo nano /etc/inittab 
```

Remove login messages

```bash

cd ~

touch .hushlogin

```




