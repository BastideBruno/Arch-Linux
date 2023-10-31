# Arch-Linux
Procédure d'installation de mon environnement de travail basé sur ArchLinux et I3 Windows Manager
## Installation de ArchLinux
### Modifier la disposition du clavier
```
loadkeys fr
```
### Optimiser Pacman
Editer le fichier pacman.conf
```
nano /etc/pacman.conf
```
Décommenter et modifier les valeurs si besoin _(facultatif)_
```
Color
VerbosePkgLists
ParallelDownloads = 14
ILoveCandy
```
### Mettre à jour de ArchInstall
```
pacman -Syu archinstall
```
### Lancer ArchInstall
```
archinstall
```
***Pendant la configuration:***
+ **Profil** -> I3-wm -> Nvidia (Proprietary) -> sddm
+ **Audio** -> Pas de serveur Audio
+ **Noyaux**-> linux-zen
+ **Packages Supplémentaires** -> linux-zen-headers

## Installation après le premier démarrage
### Yay ***(assistant pour installer les paquets AUR & ARCH)***
```
sudo pacman -S --needed git base-devel
git clone https://aur.archlinux.org/yay-bin.git
cd yay-bin
makepkg -si
```
```
yay -Y --gendb
yay -Y --devel --save
```
### Driver Nvidia
Installation des pilotes avec Nvidia-all :

Les headers doivent être imperativement installés au préalable

*Exemple si le noyau linux-zen a été choisi:*
```
sudo pacman -S linux-zen-headers
```

```
git clone https://github.com/Frogging-Family/nvidia-all.git
	cd nvidia-all
	makepkg -si
```

### Serveur audio
```
sudo pacman -S pipewire-audio pipewire-alsa pipewire-pulse wireplumber pavucontrol
```

### Paquets nécessaires au partitionnement et au montage FAT32 & exFAT
```
sudo pacman -S dosfstools mtools exfat-utils ntfs-3g gparted
```

### Ajout de la partition nvme0n1p3 (EXCHANGE en exFAT)
```
	sudo mkdir /mnt/exchange
	sudo nano /etc/fstab
		# /dev/nvme0n1p3
		UUID=E7A6-F843          /mnt/exchange           exfat            rw,nofail,x-systemd.automount,nosuid,nodev,relatime,uid=1000,gid=1000,fmask=0022,dmask=0022,iocharset=utf8,errors=remount-ro   0 2
	sudo systemctl daemon-reload
	sudo mount -a
```

### Paquets nécessaires pour la compatibilitée des polices
```
sudo pacman -S ttf-liberation noto-fonts noto-fonts-emoji ttf-droid ttf-font-awesome ttf-dejavu ttf-freefont ttf-roboto terminus-font ttf-fira-code ttf-nerd-fonts-symbols
```

### Explorateur de fichier (graphique)
```
sudo pacman -Sy dolphin qt5ct
```

### Lecteur de musique & visualiseur
```
yay -Sy musikcube cava
```
### Neovim
```
sudo pacman -Sy nvim nodejs python python-pip python-pynvim	
```

### Visual Studio Code
```
yay -Sy code
```

### Color Picker
```
yay -Sy gcolor3
```

### Information sur le systeme
```
yay -Sy fastfetch
```

### Emulateur de Terminal
```
yay -Sy alacritty
```
Confugurer Dolphin pour qu'il puisse lancer un terminal Alacritty
```
nano .config/kdeglobals
```
```
[General]
TerminalApplication=alacritty
```

### Gestionnaire de Wallpaper
```
yay -Sy nitrogen
```

### Gestion de la transparence
```
sudo pacman -S picom
```

### Gestion des thèmes de fenetre
```
sudo pacman -Sy qt5-base qt5-svg qt5-x11extras kvantum
```

```
nano .xprofile
```
Ajouter :
```
# KDE theme
QT_QPA_PLATFORMTHEME=gtk2
export QT_QPA_PLATFORMTHEME="qt5ct"
```
Redémarrer
```
kvantummanager
```
