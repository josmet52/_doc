# Developpement ESP32 sur PC avec PyCharm et microPython
Ce document décrit les différentes étapes de préparation afin de pouvoir développer un projet sur un 
micro-contrôleur ESP32 connecé à un PC à l'aide de l'IDE PyCharm 

=================================================================================
## Téléchargement et installation du driver ESP32 pour le PC
### Télécharger 
- télécharger la dernière version du driver sur le site 
  [ESP32 Windows driver](https://www.silabs.com/documents/public/software/CP210x_Universal_Windows_Driver.zip) 
par exemple : `CP210x_Universal_Windows_Driver.zip`

- déziper le fichier et lancer le programme d'installation du driver : `CP210xVCPInstaller_x64.exe`
- une fois le pilote installé : `identifier le port COM utilisé` (COM9 dans mon cas)
    
### valider l'installation
- ouvrir un moniteur sérier (PuTTY p. ex.)
- se connecter au port COMx identifié ci-dessus
- vérifier que le microcontrôleur répond

=================================================================================

## Configurer l'ESP32 pour MicroPython

 
- installer esptool sur le PC dans un invite de commande : `pip install esptool`
- télécharger le firmware [ESP32 MicroPython firmware](https://micropython.org/download/esp32/) 
  *(p. ex: esp32-20180511-v1.9.4.bin)*
  
- effacer complètement la mémoire flash du ESP32 : `esptool.py --COMx /dev/ttyUSB0 erase_flash` 
- installer le nouveau firmware : 
  `esptool.py --chip esp32 --COMx /dev/ttyUSB0 write_flash -z 0x1000 esp32-20180511-v1.9.4.bin`



=================================================================================

## Installer micropython sur PyCharm
### installation du plugin MicroPython pour PyCharm
- PyCharm : File | Settings | Plugins | Marketplace
- rechercher le plugin MicroPython
- sélectionner le Plugin MicroPython -> Install
  
### Installation du plugin moniteur série dans PyCharm
- PyCharm : File | Settings | Plugins | Marketplace
- rechercher le plugin 'Serial Port Monitor'
- sélectionner le Plugin 'Serial Port Monitor' -> Install

### Créer un nouveau projet et le rendre MicroPython
`PyCharm : File | New Project  -> Create`
- Le rendre compatible MicroPython : `File | Settings | Languages & Frameworks | MicroPython`
- Sélectionner le type de microcontrôleur et le port COM concernée 
*(autodetect ne fonctionne pas bien, entrer les choix manuellement)*
  
- `File | Settings | Project:NomDuProjet | Project structure`
- click droit sur `.idea` et cocher `Excluded` *(les fichiers de .idea sont spécifiques à PyCharm et en cochant Exclude, 
  on empèche PyCharm de les copier sur l'ESP32)*


### Remarque
Le moniteur série ne peut pas accéder au port COM en même temps qu'un programme s'exécute dans l'IDE.
Il faut donc interrompre lexécution du programme avant de connecter le moniteur série pour communiquer avec 
l'application. Sur le micro contr^leur, le programme est réinitalisé chaque fois que le moniteur série se connecte 
depuis PyCharm.








