# RViGuide
A guide to make a Raspberry Pi 2 &amp; Raspbian blind friendly.

## Download
(If there is a newer release of wheezy it will probably work fine, jesse is not working as of writing this)

https://downloads.raspberrypi.org/raspbian/images/raspbian-2015-05-07/2015-05-05-raspbian-wheezy.zip.torrent

https://downloads.raspberrypi.org/raspbian/images/raspbian-2015-05-07/2015-05-05-raspbian-wheezy.zip

## Write

###Linux
sudo dd bs=1m if=<your image file>.img of=/dev/sdX

### Windows
use win32diskimager 
http://sourceforge.net/projects/win32diskimager/

## Raspbian Modifications

### Piespeakup, Prerequisites and Necessary cli programs

sudo apt-get install git make gcc espeakup newsbeuter links mplayer zsh calibre

#### Piespeakup Setup

git clone https://github.com/cromarty/ttsprojects.git

cd ttsprojects/raspberry-pi/libilctts/build

sudo ./build.sh

cd ../../piespeakup

sudo ./build.sh

cd ../../../

rm -rf ttsprojects/

rm -rf python_games

sudo chmod -x /etc/init.d/espeakup

#### Optional keyboard layout change (default is UK)

sudo dpkg-reconfigure keyboard-configuration (optional, set to your liking)

### Shell optimisation

#### Bash (.bashrc)

echo '' >> /home/pi/.bashrc

echo 'PS1="bash, \w: "' >> /home/pi/.bashrc

echo "amixer cset numid=3 1 > /dev/null" >> /home/pi/.bashrc

echo "alias play='mplayer -quiet'" >> /home/pi/.bashrc

#### zsh

##### oh my zsh
sh -c "$(wget https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"

edit ~/.oh-my-zsh/themes/robbyrussell.zsh-theme and replace the unicode arrow with the word that is to be said before each zsh prompt, i like using sh or zsh

##### .zshrc

echo '' >> /home/pi/.zshrc

echo "amixer cset numid=3 1 > /dev/null" >> /home/pi/.zshrc

echo "alias play='mplayer -quiet'" >> /home/pi/.zshrc

### Enable Autologin

Edit /etc/inittab as root and replace '1:2345:respawn:/sbin/getty 115200 tty1' with '1:2345:respawn:/bin/login -f pi tty1 </dev/tty1 >/dev/tty1 2>&1'

cd ~

touch .hushlogin

## Making an image (on another computer)

cd 

rm -rf * (keep .bashrc)

apt-get install zerofree

umount /dev/sdx#

zerofree /dev/sdx#

dd if=/dev/sdX of=vibackup.img bs=1M count=3584

## Demofiles

https://www.dropbox.com/s/50jo0rgcrwqhioy/moby-dick.epub

https://www.dropbox.com/s/3u7ijcmgun2q17t/rss.txt

https://www.dropbox.com/s/dzrdff7vzhtsfwg/alicepogo.mp3

