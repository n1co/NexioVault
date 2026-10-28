```table-of-contents
```
## Généralités à savoir

C'est quoi volatility ?

Volatility est un outil qui va nous permettre d'analyser le dump de la mémoire d'une machine (ça veut dire qu'il faut au préalable avoir fait ce dump)

Comment on dump la mémoire d'une machine ?

Avec des outils comme :

- FTK Imager
    
- Belkasoft RAMCAPTURE
    

Il y a quoi d'intéressant dans la mémoire d'une machine ?

- Executables lancés (et ceux fermés récemment)
    
- La mémoire vive de chaque processus
    
- Fichiers ouverts
    
- Sockets réseau
    
- Elements systèmes (base SAM, ...)
    

Différence entre volatility2 (python2) et volatility3 (python3) ?

python3 c'est de la merde :

- Parceque c'est pas rétrocompatible avec les trucs en python2 (histoires de syntaxe)
    
- Parceque c'est pas stable
    
- Parceque le système de parsing est moins bon que la version 2
    

Du coup en prod, on considère que la dernière version stable de python c'est 2.

> Parsing : Découpage. En gros python n'a pas de ; ou de { } donc le découpage repose uniquement sur le nombre d'espaces en début de ligne (c'est de la merde)

Conclusion => On installe volatility2

C'est quoi une règle yara ?

Une règle yara est un pattern de détection d'évènement malveillant sur une machine ou une infrastructure. Dans ce genre de règle, on va placer des "artefacts" de détection comme des adresses IP, des URL, des hash, ....

Comment un processus peut se cacher ?

Sous Windows, les processus visibles par l'utilisateur sont stockés dans une variable nommée EPROCESS. Un processus peut demander à s'en désinscrire et généralement ça va être le comportement d'un malware. Cependant, il restera visible quoi qu'il arrive en RAM (d'ou l'intérêt de l'analyse)

# Installation de volatility

Sur ubuntu (et devrait être valide pour kali) :

```
sudo apt update -y
sudo apt upgrade -y

sudo apt install -y build-essential git libdistorm3-dev yara libraw1394-11 libcapstone-dev capstone-tool tzdata

sudo apt install -y python2 python2.7-dev libpython2-dev
wget https://bootstrap.pypa.io/pip/2.7/get-pip.py
sudo python2 get-pip.py
sudo python2 -m pip install -U setuptools wheel

sudo python2 -m pip install -U distorm3 yara pycrypto pillow openpyxl ujson pytz ipython capstone
sudo ln -s /usr/local/lib/python2.7/dist-packages/usr/lib/libyara.so /usr/lib/libyara.so
python2 -m pip install -U git+https://github.com/volatilityfoundation/volatility.git

echo "export PATH=/home/$USER/.local/bin:\$PATH" >> ~/.zshrc
```

Si 'echo $SHELL' donne ' zsh alors la dernière commande on remplacera 'bashrc' par 'zshrc'

# Analyse de base avec Volatility

[https://repository.root-me.org/Forensic/EN - Volatility cheatsheet v2.4.pdf](https://repository.root-me.org/Forensic/EN%20-%20Volatility%20cheatsheet%20v2.4.pdf)

1. Identification du système d'exploitation source de l'image (le profile)
    

```
vol.py -f fichier.vmem imageinfo
```

1. Lister les processus qui tournaient au moment du dump
    

Liste simple :

```
vol.py -f fichier.vmem --profile=<profile> pslist
```

Liste arborescente :

```
vol.py -f fichier.vmem --profile=<profile> pstree
```

Liste incluant la visibilité des processus :

```
vol.py -f fichier.vmem --profile=<profile> psxview
```

1. Lister les sockets et autres
    
2. Pour Windows