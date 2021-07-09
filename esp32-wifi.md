# Mise en oeuvre du WIFI sur ESP32

Ce document explique la procédure pour se connecter à un réseau WIFI en utilisant MicroPython sur un ESP32

## Procédure de test

Exécuter les opération suivantes :

\>>> `import network` 

\>>> `station = network.WLAN(network.STA_IF)`

\>>> `station.active(True)`

\>>> `station.connect("jmb-guest","pravidondaz")`

    `<ENTER>`

\>>> `station.isconnected()`

    True

\>>> `station.ifconfig()`  

    ('192.168.1.108', '255.255.255.0', '192.168.1.1', '192.168.1.1')