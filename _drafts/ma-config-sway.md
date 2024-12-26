---
layout: post
title: Ma config Sway
categories:
- Archlinux
- window manager
- Sway
tags:
- archlinux
- bureau
- window manager
---
# Pourquoi Sway

Depuis que je suis passé sur des PC portables, je me retrouve bien embêté quand je dois utiliser la souris, ca ramenti ce que je fais, et l'utilisation d'un touchpad m'est assez désagréable, sortir une souris n'est pas toujours pratique, il faut l'admettre. Un ami ayant migré sur sway, je me suis dis qu'il était temps aussi.

# L'installation

Je fais l'installation par defaut depuis le script archinstall. Si jamais le syetème est deja installé, on installe sway, de quoi gérer le lock, la mise en veille, les fonds d'écran et waybar pour la barre de notification

```bash
sudo pacman -S sway sway-lock sway-idle sway-bg waybar
```

# La configuration
## Sway
### Séparation des configurations
Le fichier de configuration se situe dans **~/.config/sway/config** sauf que j'aimerais moduler ca en plusieurs fichiers config. On va donc créet un dossier config.d et inclure tout les fichiers de se dernier a la confin de **config**

```
# Inclusion du repertoire de configuration
include /etc/sway/config.d/*
```

On va maintenant pouvoir y voir plus clair ! Il y a la possibilité aussi maintenant d'activer/desactiver des bouts de configuration spécifiques mettant des fichiers config dans et hors de ce dossier, un peu comme les config-available config-enabled de apache2.

Par convention nous allons nomer les fichier comme suit : ##-nom_de_fichier
Les # correspondent a un nombre. plus le nombre est proche, plus tôt il sera chargé. 

### Configuration des entrées
On va créer un fichier config pour gérer les périphériques d'entrée. Mon but est d'avoir un layout de clavier fr. Si j'avais plusieurs claviers, je pourrais les séparer et choisir une keymap par clavier, ou alors faire une liste de keymap et les changer en associant xkb_switch_layout sur une combinaisons de touches, mais KISS.

On va créer le fichiers **~/.config/sway/config.d/10-inputs**

```
# Configuration des entrées
# Documentation : https://man.archlinux.org/man/sway-input.5.en

# On passe les claviers en fr
input type:keyboard xkb_layout fr
```

### Configuration des sorties
Comme pour les entrées, on va faire la même chose pour les écrans. Mon objectif est extremement complexe, mettre une image d'arrière plan sur tout les écrans, et l'adapter a l'écran

On va créer le fichier **~/.config/sway/config.d/20-outputs**

```
# Configuration des sorties
# Documentation https://man.archlinux.org/man/sway-output.5.en

# On met sur tout les écran mon wallpaper !
output * background $HOME/.config/sway/wallpapers/darker_unicat.png fill
```

### Configuration des raccourcis
Maintenant qu'on a un sway, il faudrait peut-etre avoir des raccourcis pour le piloter. Attention, n'oubliez pas que nous sommes passé sur la keymap fr, donc on va adapter toutes les touches aussi.

On va créer le fichier **~/.config/sway/config.d/30-shortcurts**

```
# On met l'identifieur de la touche windows dans la variable $mod.
set $mod Mod4

# On repique le fonctionnement de vim avec les mouvements sur la lignes de touches principale et on met les directions dans les variables
set $left h
set $down j
set $up k
set $right l

## Raccourcis d'action
# win+entrer : Lance un emulateur de terminal
bindsym $mod+Return exec foot
# win+Shit+q : Kill la fenetre selectionnée
bindsym $mod+Shift+q kill
# win+d : Ouvre le launcher
bindsym $mod+d exec wofi --show drun
# win+Shift+c : Recharge la config de Sway
bindsym $mod+Shift+c reload
# win+Shift+e : Quitte sway apres un avertissement
bindsym $mod+Shift+e exec swaynag -t warning -m 'Tu va fermer Sway, U sure bro ?' -B 'Yup, dégage moi tout ça' 'swaymsg exit'

## Actions de fenetres
# win+b organiser sur une separation honrizontale
bindsym $mod+b splith
# win+v organiser sur une separation verticale
bindsym $mod+v splitv


## Bureaux virtuels
# Le changement de bureau adapté a la map azerty fr
# Tout et sur win+"1234567890"
bindsym $mod+ampersand workspace 1
bindsym $mod+eacute workspace 2
bindsym $mod+quotedbl workspace 3
bindsym $mod+apostrophe workspace 4
bindsym $mod+parenleft workspace 5
bindsym $mod+egrave workspace 6
bindsym $mod+minus workspace 7
bindsym $mod+underscore workspace 8
bindsym $mod+ccedilla workspace 9
bindsym $mod+agrave workspace 10
# Envoyer la fenetre active vers un autre bureau
# Même ligne, sauf qu'on maintient shift pour migrer la fenêtre
bindsym $mod+Shift+ampersand move container to workspace number 1
bindsym $mod+Shift+eacute move container to workspace number 2
bindsym $mod+Shift+quotedbl move container to workspace number 3
bindsym $mod+Shift+apostrophe move container to workspace number 4
bindsym $mod+Shift+parenleft move container to workspace number 5
bindsym $mod+Shift+egrave move container to workspace number 6
bindsym $mod+Shift+minus move container to workspace number 7
bindsym $mod+Shift+underscore move container to workspace number 8
bindsym $mod+Shift+ccedilla move container to workspace number 9
bindsym $mod+Shift+agrave move container to workspace number 10
```