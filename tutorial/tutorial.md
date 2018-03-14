# Créer un chat temps-réel avec ZetaPush

## Objectif

L'objectif principal de ce tutoriel est de te montrer la rapidité et la simplicité de développement avec ZetaPush. En quelques lignes de code, tu auras créé un chat temps réel qui sera déployé et utilisable immédiatement !

Pour ceci tu vas découvrir les services de ZetaPush qui te permettent de rapidement créer la partie back-end de ton application. Ensuite, tu vas voir comment étendre toi même ces services pour développer tes fonctionnalités métier.

Pour réaliser notre application, nous allons pour la partie front, nous baser sur un framework existant. À toi de choisir celui que tu préfères, nous te proposons :

- Angular
- Vue
- React

## Pré-requis

Pour suivre ce tutoriel, tu as besoin des pré-requis suivants :

- Un gestionnaire de package (npm ou yarn)
- nodejs

## Développement de l'application


### Angular

Dans cette partie, nous allons nous baser sur le framework Angular pour réaliser la partie front de notre application.

Tout d'abord créons l'architecture de notre application et générons l'application front Angular :

```bash
    $ mkdir tutorialV3
    $ cd tutorialV3
    $ ng new chatFront
```

Une fois notre arboresence crée et notre application front générée, ajoutons la dépendance à ZetaPush et lançons notre application :

```bash
    $ cd chatFront
    $ yarn add @zetapush/angular
    $ ng serve
```

À ce moment là tu as accès à ton application front sur `http://localhost:4200`.

#### Design

Nous allons maintenant réaliser le design de notre application, remplis les fichiers suivant comme ci-dessous :

##### app.component.html

TODO

##### app.component.scss

TODO

#### Intéraction avec ZetaPush

À présent, il nous faut remplir notre fichier `app.component.ts` pour faire fonctionner notre chat.

Pour ceci nous avons besoin dans un premier temps de nous connecter à ZetaPush. La connexion sera de type `weak`. C'est à dire qu'un identifiant unique sera généré pour cet utilisateur, aucune création de compte n'est nécessaire au préalable.

Ensuite il nous faut utiliser les services ZetaPush pour permettre l'envoi des messages et écouter les messages entrant.

Voici le code correspondant pour ces fonctionnalités :

##### app.component.ts

```javascript
    import { ZetaPushClient, ZetaPushService } from '@zetapush/core';

    export class AppComponent implements OnInit {
        let inputMessage = "";
        let messages = [];

        constructor(
            private zpClient: ZetaPushClient,
            private zpService: ZetaPushService
        ) {
            this.zpService.subscribe((message) => {
                this.messages.push(message);
            })
        }

        ngOnInit(): void {
            this.zpClient.connect().then(() => {
                console.log("ZetaPushConnection::Successful");

                // Get all messages at startup
                this.zpService.getAllMessages({}).then((messages) => {
                    this.messages = messages;
                })
            });
        }

        sendNewMessage(): void {
            this.zpService.sendMessage({ value: this.inputMessage });
        }
    }
```

Il est aussi nécessaire d'importer le module ZetaPush dans notre application Angular :

##### app.module.ts

```javascript
    import { ZetaPushModule } from '@zetapush/angular';

    @NgModule({
        // ...
        imports : [
            ZetaPushModule
        ],
        // ...
    })
```

#### Déploiement

Maintenant que notre code est prêt, il est nécessaire de le déployer sur la plateforme ZetaPush. Pour ceci, il suffit de lancer la commande suivante à la racine du projet :

```bash
    $ zeta push
```

Suite à ça tu peux suivre la progression du déploiement et une fois fini une URL t'es renvoyée et te donne accès à ton application déployée et fonctionnelle.


#### Ajout de fonctionnalités métier

Une fois que nous constatons que notre application fonctionne parfaitement, nous souhaitons donner la possibilité à l'utilisateur de se nommer, sans pour autant avoir à faire une création de compte. Pour ceci nous avons besoin d'étendre notre service existant.


ZetaPush comporte un ensemble de services existants qui propose un large panel de fonctionnalités. Il est possible de les étendre en écrivant nous même du code serveur en TypeScript et en le déployant de la même manière que nous venons de faire pour notre application Angular.

TODO : Liste des services existants

Rajoutons d'abord le design pour permettre à l'utilisateur de nous fournir un nom :

##### app.component.html

TODO

Pour rajouter des fonctionnalités, créons tout d'abord un projet à côté de notre application Angular :

```bash
    $ cd tutorialV3    
    $ npm init
    $ npm install --save @zetapush/core
    $ mkdir chatServerCodeExtension
    $ cd chatServerCodeExtension
    $ touch chatExtension.ts
```

Remplissons à présent notre fichier pour étendre notre service de chat :

##### chatExtension.ts

```javascript
    import { ZetaPushService } from '@zetapush/core';

    class ChatServiceExtended extends ZetaPushService.ChatService {

        function setUsername({username: string}): void {
            ZetaPushService.ChatService.username = username;
        }
    } 
```

Déployons à présent notre code sur la plateforme :

```bash
    $ cd tutorialV3
    $ zeta push
```

Maintenant nous pouvons appeler notre service custom au même titre qu'un service existant :

##### app.component.ts

```javascript
    function setName(username: string): void {
        this.zpService.setUsername({ username });
    }
```

Nous pouvons à nouveau redéployer notre code avec :

```bash
    $ zeta push
```



### React

TODO

### Vue

TODO



## Conclusion

TODO : Conclusion tuto

TODO : Lien vers les services existants

TODO : Explication création service from scratch

