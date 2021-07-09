# Développement ESP32 sur PC avec Thonny et micropython
Ce document décrit les différentes étapes pour configurer un projet ESP32 
et le développer sur l'IDE Thonny sous Windows 10. 

---

## Téléchargement et installation du driver ESP32 pour le PC
### Télécharger 
- télécharger la dernière version du driver sur le site
[ESP32 Windows driver](https://www.silabs.com/documents/public/software/CP210x_Universal_Windows_Driver.zip) 

  (par exemple : `CP210x_Universal_Windows_Driver.zip`)

- dézipper le fichier et lancer le programme d'installation du driver : `CP210xVCPInstaller_x64.exe`
- une fois le pilote installé : identifier le port COM utilisé *(COM9 dans mon cas)*
### Valider l'installation
- ouvrir un moniteur sérier (PuTTY p. ex.)
- se connecter au port COMx identifié ci-dessus
- vérifier que le microcontrôleur répond

## Installer esptool sur le PC
- installer esptool sur le PC dans un invite de commande : `pip install esptool`
---

## Configurer WEMOS ESP32-mini pour MicroPython

- télécharger le firmware [ESP32 MicroPython firmware] (https://micropython.org/download/esp8266/) 
  *(p. ex : esp32-20210418-v1.15.bin)*
- effacer complètement la mémoire flash du ESP32 : 
		`esptool --port COMx erase_flash` 
- installer le nouveau firmware : 
		`esptool --chip esp32 --port COMx write_flash -z 0x1000 esp32-20210418-v1.15a.bin`

## Configurer TTGO T-DISPLAY ESP32 pour Loboris micropython
- télécharger le firmware [MicroPython_ESP32_psRAM_LoBo] (https://github.com/loboris/MicroPython_ESP32_psRAM_LoBo/wiki/firmwares) *(p. ex : MicroPython_LoBo_esp32_all.zip)* et le dézipper
- effacer complètement la mémoire flash du ESP32 : 
		`esptool --port COM4 erase_flash` 
- dans le répertoire du firmware dézippé se placer au niveau ou se trouve le fichier `MicroPython.bin`
- installer le nouveau firmware
		`esptool --chip esp32 --port COM4 --baud 460800 --before default_reset --after no_reset write_flash -z --flash_mode dio --flash_freq 40m --flash_size detect 0x1000 bootloader/bootloader.bin 0xf000 phy_init_data.bin 0x10000 MicroPython.bin 0x8000 partitions_mpy.bin`
---
## Utiliser Thonny avec l'ESP32







