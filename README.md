# Github Actions - Automatización del despliegue de una aplicación

El proyecto GraphQl-actions ya nos lo ha dado el profesor. Se pueden instalar los paquetes de Node y ejecutarlo para comprobar que funione en la siguiente [URL](http://localhost:3000/graphql).

## Pasos a seguir

1. Crear un nuevo repositorio en GitHub, le llamamos graphql-actions.
2. Subimos este código fuente.
3. Para poder utilizar "actions" de manera automatizada primero deberemos ir a la pestaña "settings" dentro del repositorio, "secrets and variables", "actions" y "new repository secret".
   1. Name: DOCKER_USER
   2. Secret: iiglesias91 (que es mi nombre de usuario registrado en docker hub con la cuenta iiglesias@intecca.uned.es)
4. Deberemos crear otro secreto.
   1. Name: DOCKER_PASSWORD
   2. El secret es el token que está en bitwarden

**NOTA** : el secret es un "access token" creado en dockerhub para permitir el acceso a dicho repositorio. Para crearlo iremos a "settings", "security" y "New Access Token". Este token nos servirá para hacer deployments en dockerhub.

**NOTA** : To use the access token from your Docker CLI client:

~~~
docker login -u iiglesias91
~~~

5. Ahora crearemos un nuevo repositorio en dockerhub. Le pondremos de nombre "docker-graphql".
6. Ahora volvemos a Github y nos vamos a la pestaña "actions" dentro del repositorio que creamos al principio.
   1. Nos vamos a la opción que dice "Docker image". Build a Docker image to deploy, run, or push to a registry.
   2. Creamos el commit con el archivo que se crea por defecto ".github/workflows/docker-image.yml"

~~~
name: Docker Image CI

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

jobs:

  build:

    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v4
    - name: Build the Docker image
      run: docker build . --file Dockerfile --tag my-image-name:$(date +%s)
~~~

7. Construimos la imagen a partir del dockerfile del proyecto.

~~~
docker build -t iiglesias91/docker-graphql:0.0.1 .
~~~

8. Una vez creada la imagen comprobamos que funcione correctamente:

~~~
docker container run -p 3000:3000 iiglesias91/docker-graphql:0.0.1

# Para comprobarlo nos vamos a http://localhost:3000/graphql
~~~












# A partir de aquí es el README.md original del proyecto

<p align="center">
  <a href="http://nestjs.com/" target="blank"><img src="https://nestjs.com/img/logo-small.svg" width="200" alt="Nest Logo" /></a>
</p>

[circleci-image]: https://img.shields.io/circleci/build/github/nestjs/nest/master?token=abc123def456
[circleci-url]: https://circleci.com/gh/nestjs/nest

  <p align="center">A progressive <a href="http://nodejs.org" target="_blank">Node.js</a> framework for building efficient and scalable server-side applications.</p>
    <p align="center">
<a href="https://www.npmjs.com/~nestjscore" target="_blank"><img src="https://img.shields.io/npm/v/@nestjs/core.svg" alt="NPM Version" /></a>
<a href="https://www.npmjs.com/~nestjscore" target="_blank"><img src="https://img.shields.io/npm/l/@nestjs/core.svg" alt="Package License" /></a>
<a href="https://www.npmjs.com/~nestjscore" target="_blank"><img src="https://img.shields.io/npm/dm/@nestjs/common.svg" alt="NPM Downloads" /></a>
<a href="https://circleci.com/gh/nestjs/nest" target="_blank"><img src="https://img.shields.io/circleci/build/github/nestjs/nest/master" alt="CircleCI" /></a>
<a href="https://coveralls.io/github/nestjs/nest?branch=master" target="_blank"><img src="https://coveralls.io/repos/github/nestjs/nest/badge.svg?branch=master#9" alt="Coverage" /></a>
<a href="https://discord.gg/G7Qnnhy" target="_blank"><img src="https://img.shields.io/badge/discord-online-brightgreen.svg" alt="Discord"/></a>
<a href="https://opencollective.com/nest#backer" target="_blank"><img src="https://opencollective.com/nest/backers/badge.svg" alt="Backers on Open Collective" /></a>
<a href="https://opencollective.com/nest#sponsor" target="_blank"><img src="https://opencollective.com/nest/sponsors/badge.svg" alt="Sponsors on Open Collective" /></a>
  <a href="https://paypal.me/kamilmysliwiec" target="_blank"><img src="https://img.shields.io/badge/Donate-PayPal-ff3f59.svg"/></a>
    <a href="https://opencollective.com/nest#sponsor"  target="_blank"><img src="https://img.shields.io/badge/Support%20us-Open%20Collective-41B883.svg" alt="Support us"></a>
  <a href="https://twitter.com/nestframework" target="_blank"><img src="https://img.shields.io/twitter/follow/nestframework.svg?style=social&label=Follow"></a>
</p>
  <!--[![Backers on Open Collective](https://opencollective.com/nest/backers/badge.svg)](https://opencollective.com/nest#backer)
  [![Sponsors on Open Collective](https://opencollective.com/nest/sponsors/badge.svg)](https://opencollective.com/nest#sponsor)-->

## Description

[Nest](https://github.com/nestjs/nest) framework TypeScript starter repository.

## Installation

```bash
$ npm install
```

## Running the app

```bash
# development
$ npm run start

# watch mode
$ npm run start:dev

# production mode
$ npm run start:prod
```

## Test

```bash
# unit tests
$ npm run test

# e2e tests
$ npm run test:e2e

# test coverage
$ npm run test:cov
```

## Support

Nest is an MIT-licensed open source project. It can grow thanks to the sponsors and support by the amazing backers. If you'd like to join them, please [read more here](https://docs.nestjs.com/support).

## Stay in touch

- Author - [Kamil Myśliwiec](https://kamilmysliwiec.com)
- Website - [https://nestjs.com](https://nestjs.com/)
- Twitter - [@nestframework](https://twitter.com/nestframework)

## License

Nest is [MIT licensed](LICENSE).
