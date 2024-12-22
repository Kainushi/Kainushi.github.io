---
layout: post
title: Installer Jekyll sur Archlinux
date: 2024-12-22 07:01 +0000
categories: [Archlinux, Jekyll]
tags: [archlinux, install, jeckyll]     # TAG names should always be lowercase
---
# Installation des dépendances

Jekyll est écrit en ruby, il faut donc installer Ruby (Duh !) et basedevel. Base-devel qui va installer tout ce qui sert a la compilation, particulièrement make et GCC qui nous interessent. Pour eviter que jekyll nous hurle dessus au moment de créer un nouveau site il nous faut aussi ruby-erb !

```bash
sudo pacman -Suy && sudo pacman -S ruby base-devel ruby-erb
```


# Configuration de Ruby

Ruby utilise un systeme de gems. L'équivalent de pip quand on parle de Python. Il faut maintenant mettre nos gems installées dans la variable d'environnement $PATH de manière a pouvoir appeller les commandes simplement. Pour ca on va rajouter quelques lignes dans la configuration de bash (.bashrc). Une ligne pour definir ou on gem va installer ses package, et enfin mettre le chemin des binaires dans le $PATH

```bash
echo 'export PATH="$HOME/.local/share/gem/ruby/3.3.0/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

# Installation de Jekyll

On passe par gem pour installer les packages de Jekyll !
```bash
gem install jekyll bundler
```