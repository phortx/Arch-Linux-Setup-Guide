# Arch-Linux-Setup-Guide
A really opionionated guide how to setup a machine with Arch Linux including KDE, ruby, zsh etc


## Preparing

If you setup a Virtual Box machine, disable the 3D acceleration. Otherwise you'll get some trouble with KDE currently :(

Download the current version of the [Architect Installer](http://sourceforge.net/projects/architect-linux/). We'll use it for the installation. Mount the iso or flash it to a USB flash drive or burn it to a CD or do what ever you want with it.


## 1. Installation

Boot to the installer and install Arch Linux  with it.

-  Install KDE5
-  Install base-devel with the kernel


## 2. Setup yaourt

yaourt is a pacman wrapper to use the AUR. We love it. Yes we do.

Install yaourt like described in the yaourt [arch linux wiki article](https://wiki.archlinux.de/title/Yaourt).


## 3. Install software

### 3.1 Kernel: linux-ck

Add

```
[repo-ck]
Server = http://repo-ck.com/$arch
```

to `/etc/pacman.conf`, sign the key: `sudo pacman-key -r 79BE3E4300411886` and install the respective package for your cpu:

https://wiki.archlinux.org/index.php/Repo-ck#Selecting_the_correct_CPU_optimized_package


### 3.2 General stuff

Read before you copy and paste, there may be stuff, you don't need.

```bash
yaourt -Suyya

# install this one first
yaourt -S --needed --noconfirm phonon-qt4-vlc

# java
yaourt -S --needed --noconfirm jre jdk

# basics
yaourt -S --needed --noconfirm vim git zsh ruby nfs-utils htop openssh autofs libnewt yakuake wget crystal keepassx2 openvpn etherwake sysstat nodejs lame k3b kdeartwork kdebase kdegraphics kdemultimedia kdenetwork kdesdk kdeutils plasma-nm gtk-engines gtk2 gtk3 qt4 qt5 breeze-kde4 adobe-source-code-pro-fonts gimp libreoffice-still aspell-de hunspell hunspell-de hunspell-en thunderbird firefox owncloud-client ksshaskpass corkscrew bind-tools mesa-demos ttf-dejavu ttf-mac-fonts ttf-ms-fonts ttf-google-fonts-git xmlstarlet lshw cvs npm sshfs truecrypt vinagre

# choose one
yaourt -S --needed --noconfirm chromium
yaourt -S --needed --noconfirm google-chrome

# development
yaourt -S --needed --noconfirm git-extras agave atom-editor virtualbox maven rubymine tomcat8 mariadb-clients mariadb  libmariadbclient intellij-idea-ultimate-edition
```

And make sure `NetworkManager` is enabled:

```
$ systemctl enable NetworkManager
$ systemctl start NetworkManager
```

### 3.3 Graphics driver

[Here's a nice table what to install](http://www.linuxveda.com/2015/04/20/arch-linux-tutorial-manual/13/)


## 4. Configs

### 4.1 Disable sudo password prompt

```
$ sudo visudo
```

Uncomment this line:

```
%wheel ALL=(ALL) NOPASSWD: ALL
```

### 4.2 Enable colors for pacman

```
$ sudo sed -i 's/#Color/Color/'
```


### 4.3 NTP

```
$ sudo systemctl enable ntpd.service
$ suod systemctl start ntpd.service
```


### Enable localdomain

```
$ sudo vim /etc/NetworkManager/dnsmasq.d/localdomain
```

Write:

```
server=/localdomain/127.0.0.1
address=/localdomain/127.0.0.1
```


## 5. Ruby

```
gem install bundler rake
```


## 6 General Stuff

## 6.1 Clean up

```
$ rm -rf Documents Music Pictures Public Templates Videos examples.desktop
$ mkdir -p bin
```

## 6.2 ZSH and Dotfiles

```
$ sudo usermod -s /usr/bin/zsh [USERNAME]
```

Replace `[USERNAME]` with your username ofcourse.

Clone your personal dotfiles and setup 'em up.
