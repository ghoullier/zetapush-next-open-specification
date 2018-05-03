# Spécification des API

Le but de ce fichier est de définir les _Cloud Services_ exposés par ZetaPush. Comme les besoins ne seront pas les mêmes en fonction de notre cible, nous allons séparer chaque spécification d'API par cible.

Pour rappel un _Cloud Service_ est un service exposé par ZetaPush qui regroupe des _Cloud Functions_. Chaque _Cloud Function_ permet de faire une action particulière. Par exemple nous pouvons avoir les _Cloud Services_ suivants :

- **UserService** avec les _Cloud Functions_ : `createUser()` / `getUserByLogin()` / ...
- **StorageService** avec les _Cloud Functions_ : `storeData()` / `searchData()` / ...

[_Cloud Services_ pour les développeurs en ESN](./api_esn/intro.md)

[_Cloud Services_ pour le développeur seul](./api_dev/intro.md)


## _Cloud Services_ pour les développeurs en ESN



## _Cloud Services_ pour le développeur seul
