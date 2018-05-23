# ZetaPush Celtia 

## What is it ?

ZetaPush Celtia helps you to create your applications more quickly and spend less.
You can use the _cloud services_ (users management, messaging, ...) provided by ZetaPush and create your own _custom cloud services_ for your business logic.

The documentation is available [here](https://zetapush.github.io/documentation) and you can see and contribute on our open specifications on [GitHub](https://github.com/zetapush/zetapush-next-open-specification).


## Getting started

### 1. Create an application

First, you need to create a ZetaPush Celtia application. For this you can use : 

`npm init @zetapush myApp`

> More informations in the [documentation](https://zetapush.github.io/documentation/#_init)

or launch this command to get the _Hello World_ example :

```console
$ wget https://github.com/zetapush/zetapush-examples/archive/master.zip; 
  unzip master.zip -d ./all;
  rm master.zip; 
  mv all/zetapush-examples-master/hello-world-custom-cloud-service .; 
  rm -r all
```

### 2. Deploy your code

_To deploy your worker you need to have the CLI. Install it with : `npm install -g @zetapush/cli`_

Once your application is ready, you can deploy it :

`zeta push`

Your application will be deployed and an URL will be returned to use your application.

> A temporary account will be created.
> More informations in the [documentation](https://zetapush.github.io/documentation/#_deploy)

**3. Run worker in local**

_To run your worker you need to have the CLI. Install it with : `npm install -g @zetapush/cli`_

You can run your worker in local to test your application and make changes :

`zeta run worker`

> A temporary account will be created.
> More informations in the [documentation](https://zetapush.github.io/documentation/#_run)


## Create an application from scratch

**Necessary files :**

```
.
├── .zetarc
├── .gitignore
├── front
│   ├── index.html
│   └── index.js
├── worker
│   └── index.js
└── package.json
```

**.zetarc** :

```json
{
  "developerLogin" : "user@gmail.com",
  "developerPassword" : "password"
}
```

**.gitignore :**

> Optional but avoid to expose your credentials

```bash
.zetarc
```

**front :**

Your front code is in this folder.

**worker :**

Your back code is in this folder.

**package.json :**

```json
{
  "name": "myApp",
  "main": "worker/index.js",
  "version": "0.0.1",
  "dependencies": {
  },
  "zetapush": {
      "front": "./front",
      "worker": "./worker"
  }
}
```

The `main` property is the entry point of your worker (All the _custom cloud services_).

The properties `zetapush/front` and `zetapush/worker` specify the path of the front and back code.

**Dependencies :**

You need to install this following dependencies :
- `@zetapush/core`
- `@zetapush/platform` 

```bash
$ npm install --save @zetapush/core @zetapush/platform
```

After having create necessary files and install dependencies your application is ready and you can use the CLI to run your worker in local or push your code on the ZetaPush platform. 


## Create ZetaPush account

You can create a ZetaPush account using the CLI :

`zeta register --developer-login user@gmail.com`

- **--developer-login** : Email for your account

