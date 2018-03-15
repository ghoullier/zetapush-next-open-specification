# Objectifs

- Un développeur front doit pouvoir mocker entièrement les appels serveurs lors de ses tests.
- Un développeur full-stack doit pouvoir tester unitairement son code serveur.
- Un développeur full-stack doit pouvoir tester fonctionnellement son code serveur en mode stateful ou stateless.
- Un développeur doit pouvoir spécifier dans son test, l'état dans lequel se trouve son application.

# Pré-requis

J'utilise mon éditeur de texte ou IDE préféré.
J'ai une application front existante créée avec mon framework préféré et initialisé avec ZetaPush.

# <a name="parcours-1"></a> Parcours 1 : Je développe une application front avec ZetaPush sans service custom

## User Stories

### ETQ dev je mock un appel à un service ZetaPush

*GIVEN*
- Dans mon test, j'ai un appel vers un service ZetaPush, par exemple : `createUser()`
- Je spécifie dans le test que lors de l'appel à `createUser()`, la réponse est mockée et me renvoie par exemple : `{firstname: "Toto", lastname: "Titi"}`

*WHEN*
- Lorsque je lance l'exécution de mon test

*THEN*
- L'appel au service ZetaPush via `createUser()` ne se fait pas
- La réponse renvoyée par `createUser()` est ce qui a été défini dans mon test. Dans l'exemple : `{firstname: "Toto", lastname: "Titi"}`


### ETQ dev je souhaite pouvoir appliquer à mon test un état de mon application précédemment sauvegardé

*GIVEN*
- J'ai écrit un test qui fait appel à un ou des services ZetaPush
- Je spécifie à mon test l'état souhaité de mon application pour l'exécution de ce test

*WHEN*
- Lorsque je lance l'exécution de mon test

*THEN*
- Mon test s'est lancé en prenant en compte l'état de mon application précédemment spécifié


# <a name="parcours-2"></a> Parcours 2 : Je développe une application avec ZetaPush et des services customs

## User Stories

### ETQ dev full-stack je teste un service custom unitairement

*GIVEN*
- J'ai écrit un service ZetaPush custom
- J'ai écrit mon test unitaire en utilisant mon framework de test préféré (Mocha, Jasmine, ...)
- J'ai mocké les appels à la plateforme ZetaPush pour seulement tester unitairement mon service

*WHEN*
- Lorsque je lance l'exécution de mon test

*THEN*
- Je reçois en réponse le retour de mon test conformément au framework utilisé


### ETQ dev full-stack je réalise un test fonctionnel sur un service custom

*GIVEN*
- J'ai écrit un service ZetaPush custom
- J'ai écrit mon test unitaire en utilisant mon framework de test préféré (Mocha, Jasmine, ...)
- Mon test implique des modifications de données sur mon application

*WHEN*
- Lorsque je lance l'exécution de mon test

*THEN*
- Je reçois en réponse le retour de mon test conformément au framework utilisé
- Les modifications de données de mon application sont effectives


### ETQ dev full-stack je réalise un test fonctionnel sur un service custom en mode stateless

*GIVEN*
- J'ai écrit un service ZetaPush custom
- J'ai écrit mon test unitaire en utilisant mon framework de test préféré (Mocha, Jasmine, ...)
- Mon test implique des modifications de données sur mon application
- J'ai spécifié dans mon test que je ne souhaite pas modifier l'état de mon application

*WHEN*
- Lorsque j'exécute la commande de lancement de test

*THEN*
- L'exécution de mon test se réalise
- J'ai le retour de mon test en console
- L'état de mon application de fin de test est le même qu'en début de test


