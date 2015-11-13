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

to `/etc/pacman.conf` and install the respective package for your cpu:

https://wiki.archlinux.org/index.php/Repo-ck#Selecting_the_correct_CPU_optimized_package


### 3.2 General stuff
```
yaourt -Suya
yaourt -S --needed --noconfirm jre jdk
yaourt -S --needed --noconfirm phonon-qt4-vlc
yaourt -S --needed --noconfirm vim git zsh ruby nfs-utils htop openssh autofs libnewt yakuake wget crystal keepassx openvpn etherwake sysstat nodejs lame k3b chromium git-extras agave atom-editor virtualbox maven kdeartwork kdebase kdegraphics kdemultimedia kdenetwork kdesdk kdeutils plasma-nm gtk-engines gtk2 gtk3 qt4 qt5 breeze-kde4 adobe-source-code-pro-fonts gimp libreoffice-still hunspell hunspell-de hunspell-en rubymine thunderbird firefox owncloud-client
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
