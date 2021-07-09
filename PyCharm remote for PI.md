# Raspberry PI projet distant avec PyCharm
novembre 2020, Joseph Métrailler

-----------------------------------
### créer le projet sur le PI

- créer le dossier du projet exemple: ex: *`myprg`*
Ouvrir un invite de commande dans le dossier du projet
- créer le premier fichier python par exemple *`myprg`*
### Environnement virtuel

Dans un invite de commande dans le dossier du projet

- Installer / upgrader pip : `python3 -m pip install --user --upgrade pip`
- Installer venv : `python3 -m pip install virtualenv`
- créer l'environnement virtuel: `python3 -m venv venv`
- activer l'environnement virtuel : `source venv/bin/activate` l'invite devient (venv) pi@...
- installer les paquets nécessaires  ex : `pip3 install *numpy*` 
- lorsque tous les packages sont installés créer le fichier requirements.txt : `venv/bin/python -m pip freeze > requirements.txt`

### Créer et inscrire le projet dans github

Sur le site [github](https://github.com/josmet52) créer un nouveau repository

Dans un invite de commande dans le dossier du projet:

- initialiser le dépôt git local : `git init`
- créer le dépôt distant : `git remote add origin https://github.com/josmet52/*myprg*`
- user email config locale : `git config --global user.email "joseph.metrailler@bluewin.ch"`
- user name config locale : `git config --global user.name "josmet52"`
- store account data's : `git config credential.helper store`
- créer le fichier gitignore : `.gitignore` avec les lignes `*.pyc` et __pycache__/
- ajouter les nouveaux fichier y compris venv (-f) : `git add * -f`
- créer le premier commit : `git commit -m "20201120 first commit"`
- créer la branche main:  `git branch -M main`
- faire le premier push : `git push -u origin main`
### Importer le projet dans PyCharm

Dans la fenêtre d'ouverture de PyCharm choisir l'option `Get from Version Control`

- sous URL saisir : `https//github.com/josmet52/*myprg*`
- sous directory entrer le chemin et le nom du dossier de l'application : `C:\Users\jmetr\_data\dev soft\python\*myprg*`
- cliquer sur `Clone`

Dans l'IDE PyCharm :

##### Configurer le déploiement de l'application

- sélectionner le menu `File | Settings | Build, Execution, Deployment | Deployment`
- cliquer sur **+** en haut de la fenêtre Settings, choisir SFTP et entrer le nom du serveur à créer ex : `*myprg*`
- cliquer sur ... à droite de SSH configuration et compléter les champs pour la connexion SSH
- tester la connexion si OK alors cliquer `OK`autrement corriger les champs
- cliquer sur Mappings en haut de la fenêtre et sous `Deployment path:` sélectionner le path sur la plateforme distante puis `OK`
- sélectionner le menu `Tools | Deployment` et activer `Automatic upload (always)`

##### Configurer l'interpréteur distant

###### créer
  - sélectionner le menu : `File | Settings | Project:*myprg* | Python interpreter`
  - cliquer sur la roue dentée en haut à droite pour sur `Add`
  - dans le fenêtre qui s'ouvre, à gauche, cliquer sur `SSH Interpreter' 
  - remplir le champ `Host` avec l'adresse IP du RPI, laisser le port par défaut
  - remplir le champ `Username` pour se logger sur le RPI puis `Next`
  - compléter le champ `Password` et cocher `Save password` puis `Next`
  - compléter le champ `Interpreter` avec le chemin de interpréteur de venv ex: `/home/pi/dev-python/myprg/venv/bin/python3`
  - compléter le champ `Sync folder` en sélectionnant les dossiers de projet locaux et distant ex : `C:/Users/jmetr/_data/dev soft/python/myprg` et `/home/pi/dev-python/myprg`
  - cliquer sur `Finsih` puis si demandé sur `Overwrite` puis `OK`

###### l'interpréteur distant existe déjà dans la liste proposée
  - sélectionner ou créer l'interpréteur Python en choisissant le programme dossier sur le PI ex : `sftp://pi@192.168.1.142/home/pi/dev-python/myprg/venv/bin/python3`
  - sous Path mappings compléter les champs `Local Path`et `Remote Path` comme ci-dessus

##### Tester l'application

- tester l'application *myprg.py* et vérifier qu'elle est exécutée sur le RPI
