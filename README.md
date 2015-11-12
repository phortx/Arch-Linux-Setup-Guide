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

```
$ yaourt -S --needed konsole vim git zsh ruby nfs-utils htop openssh autofs libnewt yakuake kdepim-ktimetracker wget crystal keepassx openvpn etherwake sysstat nodejs jdk vlc lame k3b chromium git-extras agave atom-editor virtualbox maven 
```


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
$ systemctl enable ntpd.service
$ systemctl start ntpd.service
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
