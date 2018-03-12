# Objectifs

- Un développeur front doit pouvoir mocker entièrement les appels serveurs.
- Un développeur full-stack doit pouvoir tester unitairement son code serveur.
- Un développeur full-stack doit pouvoir tester fonctionnellement son code serveur en mode statefull ou stateless.
- Un développeur doit pouvoir tester la performance de son code serveur. (rapidité d'exécution)
- Un développeur doit pouvoir passer en contexte "test" à tout moment pour faciliter l'éxécution de ses tests

# Pré-requis

J'utilise mon éditeur de texte ou IDE préféré.
J'ai une application front existante créée avec mon framework préféré et initialisé avec ZetaPush.

# <a name="parcours-1"></a> Parcours 1 : Je développe une application front avec ZetaPush sans service custom

## User Stories

### ETQ dev front je mock un appel à un service ZetaPush

*GIVEN*
- J'ai un appel de service côté client (`createUser()` par exemple)

*WHEN*
- Lorsque j'appelle un service mocké avec une annotation, exemple :
    ```
    @Mock({ "id": 865751698, "login": "test", "password": "test"})
    this.zpService.createUser({ login: "test", password: "test"}).then((user) => {
        console.log("UserCreated", user);
    })
    ```

*THEN*
- L'appel au service ne se fait pas
- L'objet renvoyé est celui spécifié dans l'annotation
 

### ETQ dev front je veux tester la performance d'un service

*GIVEN*
- J'ai un appel de service côté client (`createUser()` par exemple)
- Mon appel au service est annoté pour spécifier que je veux connaitre la performance de cet appel, exemple :

    ```
    @TestPerformance()
    this.zpService.createUser({ login: "test", password: "test"}).then((user) => {
        console.log("UserCreated", user);
    })
    ```

*WHEN*
- Lorsqu'un appel à ce service se fait

*THEN*
- Une trace dans les logs est retournée avec différentes métriques, exemple :
    ```
    ServeurTrace-DEBUG::PerformanceTesting(createUser):duration->26ms
    ServeurTrace-DEBUG::PerformanceTesting(createUser):ram_used->20ko
    ServeurTrace-DEBUG::PerformanceTesting(createUser):memory_used->126o
    ```

# <a name="parcours-2"></a> Parcours 2 : Je développe une application avec ZetaPush et des services custom

## User Stories

### ETQ dev full-stack je mock un appel à un service custom ZetaPush

*GIVEN*
- J'ai écris un service custom, par exemple un service qui lance une action sur un Raspberry Pi

    ```
    function launchActionOnPi(action: string, params: any) {
        ...
    }
    ```
*WHEN*
- Lorsque j'appelle un service mocké avec une annotation, exemple :
    ```
    @Mock({ "success": true})
    this.zpService.launchActionOnPi(action: "shutdown", params: {}).then((result) => {
        console.log("PiActionLaunched", result);
    })
    ```

*THEN*
- L'appel au service ne se fait pas
- L'objet renvoyé est celui spécifié dans l'annotation
 

### ETQ dev full-stack je teste un service custom unitairement

*GIVEN*
- J'ai écris un service custom, par exemple un service qui lance une action sur un Raspberry Pi

    ```
    function launchActionOnPi(action: string, params: any) {
        ...
    }
    ```
- J'utilise mon framework de test préféré
- J'écris mon test unitaire qui appelle mon service custom

*WHEN*
- Lorsque j'exécute la commande de lancement de test

*THEN*
- L'éxécution des tests de réalise
- J'ai le retour de mes tests en console


### ETQ dev full-stack je réalise un test fonctionnel sur un service custom en mode stateful

*GIVEN*
- J'ai écris plusieurs services custom
- J'utilise mon framework de test préféré
- J'écris mon test fonctionnel qui fait appel à un (ou plusieurs) service(s) custom

*WHEN*
- Lorsque j'exécute la commande de lancement de test

*THEN*
- L'éxécution des tests se réalise
- J'ai le retour de mes tests en console
- Les modifications apportées aux données sont effectives et enregistrées côté back


### ETQ dev full-stack je réalise un test fonctionnel sur un service custom en mode stateless

*GIVEN*
- J'ai écris plusieurs services custom
- J'utilise mon framework de test préféré
- J'écris mon test fonctionnel qui fait appel à un (ou plusieurs) service(s) custom

*WHEN*
- Lorsque j'exécute la commande de lancement de test

*THEN*
- L'éxécution des tests se réalise
- J'ai le retour de mes tests en console
- Les modifications apportées aux données ne sont pas effectives
- L'état en fin de test est exactement le même quand début de test



### ETQ dev full-stack je veux tester la performance d'un service custom

*GIVEN*
- J'ai écris un service custom, par exemple un service qui lance une action sur un Raspberry Pi

    ```
    function launchActionOnPi(action: string, params: any) {
        ...
    }
    ```
- Mon appel au service custom est annoté pour spécifier que je veux connaitre la performance de cet appel, exemple :
    ```
    @TestPerformance()
    this.customZpService.launchActionOnPi("shutdown", "now").then((result) => {
        console.log("PiActionLaunched", result);
    })
    ```

*WHEN*
- Lorsqu'un appel à ce service custom se fait

*THEN*
- Une trace dans les logs est retournée avec différentes métriques, exemple :
    ```
    ServeurTrace-DEBUG::PerformanceTesting(launchActionOnPi):duration->26ms
    ServeurTrace-DEBUG::PerformanceTesting(launchActionOnPi):ram_used->20ko
    ServeurTrace-DEBUG::PerformanceTesting(launchActionOnPi):memory_used->126o
    ```

### ETQ dev full-stack je peux configurer le contexte d'éxécution de mon application pour effectuer mes tests

*GIVEN*
- J'ai écris un ou plusieurs services custom
- J'ai écris un test
- J'utilise mon framework de test préféré
- J'ai ajouté appel dans le `beforeAll()` de mon test pour configurer le contexte d'éxécution, exemple :

    ```
    this.client.setRuntimeContext({ stateMode: statelesss, trace: 'debug'});
    ```

*WHEN*
- Lorsque j'éxécute mon test

*THEN*
- L'éxécution des tests se réalise
- J'ai le retour de mes tests en console
- Le contexte est stateless ou statefull en fonction du paramètre de `setRuntimeContext()`
- Le niveau de trace est configuré en fonction du paramètre de `setRuntimeContext()`

### ETQ dev full-stack je peux créer et utiliser un ou plusieurs contextes d'éxécution

*GIVEN*
- J'ai écris un ou plusieurs services custom
- J'ai écris un test
- J'utilise mon framework de test préféré
- J'ai créé au préalable un contexte d'éxécution, exemple :

    ```
    const context1 = this.client.createRuntimeContext({ stateMode: stateful, trace: 'warn'});
    ```
- J'ai ajouté appel dans le `beforeAll()` de mon test pour configurer le contexte d'éxécution, exemple :

    ```
    this.client.setRuntimeContext({ context: context1});
    ```

*WHEN*
- Lorsque j'éxécute mon test

*THEN*
- L'éxécution des tests se réalise
- J'ai le retour de mes tests en console
- Le contexte est stateless ou statefull en fonction du paramètre de `setRuntimeContext()`
- Le niveau de trace est configuré en fonction du paramètre de `setRuntimeContext()`