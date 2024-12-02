---
# You can also start simply with 'default'
theme: ./
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://cover.sli.dev
colorSchema: "both"
lineNumbers: true

# some information about your slides (markdown enabled)
title: Github Actions 
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# apply unocss classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
# take snapshot for each slide in the overview
overviewSnapshots: true
introImage: '/chef_damien.jpg'
subjectImage: '/gha_logo.svg'
eventImage: '/afuplyon_logo.png'
layout: intro
---

# Github Actions

Reprenez votre CI en main

Damien Fernandes 

<div class="abs-br m-6 flex gap-2">
  <a href="https://github.com/damienfern" target="_blank" alt="GitHub" title="Open in GitHub"
    class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>


---
layout: quote
---

# <span v-mark>Disclaimer</span>

<!-- 

Je ne suis pas un Devops.
Je suis juste un dev qui adore apprendre de nouvelles choses.
Le but de cette prez n'est pas d'aller voir le gars qui s'en occupe à 100% et dire "j'ai vu ça dans talk" 
Si vous avez déjà quelqu'un qui s'occupe de ça et dont c'est son job à 100%, il a potentiellement une bonne raison de ne pas avoir fait ça.

Le but : 
- vous aider à mieux comprendre GA et votre CI (ou vos projets persos)
- Vous donner quelques tips qui peuvent vous faire gagner du temps

-->

---
layout: image-right
image: /portrait.jpg
---

# Moi, c'est Damien

Lead Dev chez WanadevDigital

- PHP, Symfony
- Vue, Typescript
- DevOps

<div class="grid grid-cols-2 items-center pt-10" >
  <img src="/wd-logo.webp"  height="150" width="150" class="rounded-lg" />
  <img src="/kazaplan-logo.png" height="150" width="150" />
</div>

---
layout: image
image: "/kazaplan-slide1.png"
backgroundSize: contain
---

<!--

Kazaplan est:
- application web accessible au grand public
- permet de concevoir des plans en 2D et 3D de vos espaces de vie interieur et extérieur
- visualiser, aménager et personnaliser ses espaces de vie

Un outil pratique pour donner forme à vos idées d’aménagement.

-->

---
layout: image
image: "/kazaplan-configure.png"
backgroundSize: contain
---

---
layout: image
image: "/kazaplan-hd.png"
backgroundSize: contain
---

---

<div class="flex justify-center">
  <img src="/configure.svg" class="block rounded-lg p-1" width="150" height="150" style="background-color: white;" />
</div>
<div class="flex justify-center p-10">
  <div class="grid grid-cols-3 items-center pt-10" >
    <img src="/gitlab-ci-logo.png" class="rounded-lg p-1" width="150" height="150" style="background-color: white;"  v-click />
    <span class="text-center text-8xl" v-click >&rarr;</span>
    <img v-click src="/gha_logo.svg"  class="rounded-lg p-1" width="150" height="150" style="background-color: white;" />
  </div>
</div>

<!-- 
Présentation problématique 

Migrer le BO de Gitlab vers Github Action
 -->

---

# CI ? CD ?

* Intégration Continue (CI) : ensemble de pratiques utilisées en génie logiciel consistant à vérifier à chaque modification de code source que le résultat des modifications ne produit pas de régression dans l'application développée. (Wikipedia)

* Déploiement continu (CD) : les équipes produisent des logiciels dans des cycles courts, ce qui permet de le mettre à disposition à n’importe quel moment. (Wikipedia)

<div class="p-5" v-click>

## Plus simplement ?

&rarr; automatise le test, l'intégration et le déploiement du code pour rendre le développement logiciel plus rapide et fiable.

</div>

---

# Les outils de CI

<div class="grid grid-rows-2 grid-flow-col gap-10 items-center" >
    <img src="/gitlab-ci-logo.png" class="rounded-lg p-1" width="125" height="125" style="background-color: white;" />
    <img src="/gha_logo.svg"  class="rounded-lg p-1" width="125" height="125" style="background-color: white;" />
    <img src="/jenkins-logo.png"  class="rounded-lg p-1" width="125" height="125" style="background-color: white;" />
    <img src="/travis-ci.png"  class="rounded-lg p-1" width="125" height="125" style="background-color: white;" />
    <img src="/bitbucket-logo.png"  class="rounded-lg p-1" width="125" height="125" style="background-color: white;" />
    <img src="/circleci.png"  claÒss="rounded-lg p-1" width="125" height="125" style="background-color: white;" />
    <img src="/team-city.png"  class="rounded-lg p-1" width="125" height="125" style="background-color: white;" />
    <p class="text-8xl">...</p>
</div>



---

<!-- Introduction et présentation d’une CI Gitlab avec les stages et présenter la philosophie (avec les rules et except/only) -->

# Notre existant

```yml
stages:
    - install
    - lint
    - code_analysis
    - test
    - build
    - deploy
# ...

```

<v-click>
```yml
Build Image:
    image: docker:stable
    stage: build
    only:
        - dev
        - /^v?[0-9]+\.[0-9]+\.[0-9]+(-[a-z0-9]+)?$/
    before_script:
        - docker login -u $CI_REGISTRY_USER -p $CI_REGISTRY_PASSWORD $CI_REGISTRY
    script:
        - docker build -f ./docker/Dockerfile --target prod --tag $CI_REGISTRY_IMAGE:ma_belle_image .
        - docker push $CI_REGISTRY_IMAGE:ma_belle_image
```
</v-click>

---
layout: image-right
image: /gha_logo.svg
---

# Github Actions

- Lancé en 2018
- Avant, utilisation d'outils externes à Github pour la CI
- Natif à Github et utilisable sans aucune installation préalable
- Basé sur un écosystème d'actions réutilisables via le marketplace
- Avec une philosophie de fonctionnement complètement différente de Gitlab CI/CD
- Utilisable seulement sur Github

<Alert> 
Github Actions sera abrégé en GA
</Alert>

<!-- Tip : ne mettez pas le mot "philosophie" dans vos slides au risque de se retrouver avec Amel Bent dans la tête -->

---

# Les concepts clés de GA

Une CI basée sur les évènements de votre repo :

- Pull Request et leurs états
- Push sur une branche
- Issues et leurs états
- Release
- ...etc.

Avec la possibilité d'appliquer des filtres (e.g. au push sur une branche spécifique ou lorsqu'un fichier spécifique a été modifié)

---

# Comment on fait des trucs avec ses évènements ?

<v-click>
  <p>Les workflows</p>
</v-click>

<v-click>

````md magic-move

```yml
# .github/workflows/unit-test.yml

```

```yml
# .github/workflows/unit-test.yml
name: Unit test

```

```yml
# .github/workflows/unit-test.yml
name: Unit test
on:
  push:

```

```yml
# .github/workflows/unit-test.yml
name: Unit test
on:
  push:
    branches:
      - 'main'
      - 'releases/**'

```

```yml
# .github/workflows/docker-lint.yml
name: Lint Dockerfile
on:
  push:
    paths:
      - 'Dockerfile'
```

```yml
# .github/workflows/unit-test.yml
name: Unit test
on:
  pull_request:
    types: [opened, reopened, synchronize]
```

```yml
# .github/workflows/unit-test.yml
name: Unit test
on:
  pull_request:
    types: [opened, reopened, synchronize]
  push:
    branches:
      - "master"
      - "dev"
```

```yml
# .github/workflows/unit-test.yml
name: Unit test
on: workflow_dispatch
```

````

</v-click>

<v-click>

<Alert type="info">
Certains events ne se trigger seulement avec les fichiers YAML présents sur la branche par défaut.
</Alert>

</v-click>


---

# Comment on lance des trucs ?

<v-click>

## Les jobs

- Une unité de travail qui contient un ensemble de tâche (steps)
- Possibilité d'avoir plusieurs Jobs par workflow
- Lancés en parallèle (par défaut) ou à la suite
- Configuration isolée entre les jobs 

</v-click>

---

# Exemple de jobs

````md magic-move
```yaml
# .github/workflows/test.yml
name: Test
on: workflow_dispatch
```

```yaml
# .github/workflows/test.yml
name: Test
on: workflow_dispatch

jobs:
  unit-test:
    name: Unit Testing
```

```yaml
# .github/workflows/test.yml
name: Test
on: workflow_dispatch

jobs:
  unit-test:
    name: Unit Testing
    runs-on: ubuntu-latest
```

```yaml
# .github/workflows/test.yml
name: Test
on: workflow_dispatch

jobs:
  unit-test:
    name: Unit Testing
    runs-on: ubuntu-latest
    steps:
    # ...
```

```yaml
# .github/workflows/test.yml
name: Test
on: workflow_dispatch

jobs:
  unit-test:
    name: Unit Testing
    runs-on: ubuntu-latest
    steps:
    # ...
  functional-test:
    name: Functional Testing
    runs-on: ubuntu-latest
    steps:
    # ...
```

```yaml
# .github/workflows/test.yml
name: Test
on: workflow_dispatch

jobs:
  unit-test:
    name: Unit Testing
    runs-on: ubuntu-latest
    steps:
    # ...
  functional-test:
    name: Functional Testing
    runs-on: ubuntu-latest
    steps:
    # ...
  coverage:
    name: Coverage
    runs-on: ubuntu-latest
    needs: [functional-test, unit-test]
    steps:
    # ...
```
````

---
layout: two-cols-header
---

# Qui fait tourner mes jobs ?

::left::

<v-click at="1">
  Les runners
</v-click>

<v-click at="2">

- Self Hosted
  - Réutilisation de vos ressources (serveurs, VM,...etc.)
  - Customisable selon vos besoins
  - Une config qui peut être persistée à travers les jobs

</v-click>

<v-click at="3">

- Github Hosted
  - Géré et maintenu par Github
  - Une config qui est nettoyée automatiquement à travers les jobs
  - Tarification par quota avec Tier gratuit
</v-click>

::right::

<v-click at="4">

````md magic-move {at:4}
```yaml {*|5}
# ...
jobs:
  unit-test:
    name: Unit Testing
    runs-on: ubuntu-latest
    steps:
    # ...

```
```yaml {5}
# ...
jobs:
  unit-test:
    name: Unit Testing
    runs-on: windows-latest
    steps:
    # ...

```
```yaml 
# ...
jobs:
  unit-test:
    name: Unit Testing
    runs-on: macos-latest
    steps:
    # ...

```
```yaml 
# ...
jobs:
  unit-test:
    name: Unit Testing
    runs-on: [ self-hosted, Linux, ARM64 ]
    steps:
    # ...

```
````
</v-click>

---

# Utiliser une base de donnée pour vos tests 

```yaml
# ...
jobs:
  unit-test:
    name: Unit Testing
    runs-on: macos-latest
  services:
      redis:
          image: redis:6-alpine
          ports:
              - 6379:6379
      postgres-functional:
          image: postgres:13-alpine
          env:
              POSTGRES_USER: user
              POSTGRES_PASSWORD: password
              POSTGRES_DB: db
          ports:
              - 5432:5432
```

---

# Les steps

- Des tâches qui composent un job
- Lancé de manière séquentielle
- Chaque step est lancée dans son process
- 2 grandes familles :
  - les shell
  - les actions



<Alert type="warning"> 
Si vous changez des env vars sans passer par GA, elles ne seront pas répercutés car chaque process de step est isolé
</Alert>


---


````md magic-move
```yaml
# ...
jobs:
  unit-test:
    # ... ubuntu
    steps:
```
```yaml
# ...
jobs:
  unit-test:
    # ... ubuntu
    steps:
      - name: Checkout code
```
```yaml
# ...
jobs:
  unit-test:
    # ... ubuntu
    steps:
      - name: Checkout code
        run: |
          echo "Cloning repository..."
          git clone ${{ github.repository }} .
          echo "Repository cloned."
```
```yaml
# ...
jobs:
  unit-test:
    # ... ubuntu
    steps:
      - name: Checkout code
        run: |
          echo "Cloning repository..."
          git clone ${{ github.repository }} .
          echo "Repository cloned."

      - name: Set up PHP and Composer
        run: |
          echo "Updating system packages..."
          sudo apt-get update -y
          echo "Installing PHP and required extensions..."
          sudo apt-get install -y php-cli php-xml php-mbstring unzip curl
          echo "Installing Composer..."
          curl -sS https://getcomposer.org/installer | php
          sudo mv composer.phar /usr/local/bin/composer
          echo "PHP and Composer are ready."
```
```yaml
# ...
jobs:
  unit-test:
    # ... ubuntu
    steps:
      - name: Checkout code
        run: |
          echo "Cloning repository..."
          git clone ${{ github.repository }} .
          echo "Repository cloned."

      - name: Set up PHP and Composer
        run: |
          echo "Updating system packages..."
          sudo apt-get update -y
          echo "Installing PHP and required extensions..."
          sudo apt-get install -y php-cli php-xml php-mbstring unzip curl
          echo "Installing Composer..."
          curl -sS https://getcomposer.org/installer | php
          sudo mv composer.phar /usr/local/bin/composer
          echo "PHP and Composer are ready."
        # ... install deps and run tests

```
```yaml {13,14,19}
# ...
jobs:
  unit-test:
    # ... ubuntu
    steps:
      - name: Checkout code
        run: |
          echo "Cloning repository..."
          git clone ${{ github.repository }} .
          echo "Repository cloned."

      - name: Set up PHP and Composer
        env:
          PACKAGES: "php-cli php-xml php-mbstring unzip curl"
        run: |
          echo "Updating system packages..."
          sudo apt-get update -y
          echo "Installing PHP and required extensions..."
          sudo apt-get install -y ${{ env.PACKAGES }}
          echo "Installing Composer..."
          curl -sS https://getcomposer.org/installer | php
          sudo mv composer.phar /usr/local/bin/composer
          echo "PHP and Composer are ready."
        # ... install deps and run tests
```
````

<!-- actions/upload-artifact & download-artifacts pour passer des fichiers entre jobs https://docs.github.com/en/actions/using-workflows/storing-workflow-data-as-artifacts#passing-data-between-jobs-in-a-workflow -->

---

# Les actions, simplifier vos steps

````md magic-move
```yaml
# ...
jobs:
  unit-test:
    # ... ubuntu
    steps:
      - name: Checkout code
        run: |
          echo "Cloning repository..."
          git clone ${{ github.repository }} .
          echo "Repository cloned."

```
```yaml
# ...
jobs:
  unit-test:
    # ... ubuntu
    steps:
      - name: Checkout code
        uses: actions/checkout@v4

```
```yaml
# ...
jobs:
  unit-test:
    # ... ubuntu
    steps:
      - name: Checkout code
        uses: actions/checkout@v4
        with:
          fetch-depth: 1

```
````

---

# Les steps et les outputs

#### Objectif : lancer les tests unitaires avec le coverage seulement sur la branche dev dans le même workflow

````md magic-move
```yaml
# ...
```
```yaml {all|4}
# ...
- name: Get branch name
  id: branch-name
  run: echo "current_branch=${GITHUB_REF#refs/heads/}" >> $GITHUB_OUTPUT
# ...
```
```yaml {all|6|3,4,6}
# ...
- name: Get branch name
  id: branch-name
  run: echo "current_branch=${GITHUB_REF#refs/heads/}" >> $GITHUB_OUTPUT
- name: Run tests with coverage
  if: ${{ steps.branch-name.outputs.current_branch == 'dev' }}
  run:
    # run phpunit command with coverage
# ...
```
````


---

# Les actions
But : Découper en blocs fonctionnels, modulaires et réutilisable (DRY)

<v-click>

## 3 types d'actions :

</v-click>
<br>

<v-clicks>

- Fournies par Github (`actions/checkout`, `actions/cache`, `actions/http-client`,...etc.)
- Marketplace
- Custom Actions

</v-clicks>

---

# Cacher vos dépendances pour des CI plus rapides

````md magic-move
```yaml {all|4|6,7|8|9,10|all}
# ...
steps:
    - name: Restore vendors from cache
      uses: actions/cache@v4
      with:
          path: |
              vendor
          key: ${{ runner.os }}-vendor-${{ hashFiles('composer.lock') }}
          restore-keys: |
              ${{ runner.os }}-vendor-
    - name: Behat
      run: |
        php ./vendor/bin/behat -f progress -o std
```
```yaml {all|12-15|4,13}
# ...
steps:
    - name: Restore vendors from cache
      id: cache-vendor
      uses: actions/cache@v4
      with:
        path: |
            vendor
        key: ${{ runner.os }}-vendor-${{ hashFiles('composer.lock') }}
        restore-keys: |
            ${{ runner.os }}-vendor-
    - name: Install PHP dependencies
      if: ${{ steps.cache-vendor.outputs.cache-hit != 'true' }}
      run: |
          /usr/local/bin/composer install --no-progress --no-scripts
    - name: Behat
      run: |
        php ./vendor/bin/behat -f progress -o std
```
````


<Alert type="warning"> 
Un nettoyage du cache est effectué par Github s'il n'est pas utilisé
</Alert>

---

# Le MUST des actions du Marketplace PHP

https://github.com/shivammathur/setup-php

```yaml
name: Setup PHP
uses: shivammathur/setup-php@v2
with:
    php-version: 8.3
    extensions: apcu,mbstring,opcache,pdo_pgsql,redis,xdebug,xml,zip
    coverage: xdebug
    ini-values: |
        memory_limit=-1,
```

---

# Quelques actions utiles : builder vos images Docker

https://github.com/docker/build-push-action

```yaml
- name: Set up Docker Buildx
  uses: docker/setup-buildx-action@v3
- name: Login to Docker Hub
  uses: docker/login-action@v3
  with:
    username: ${{ secrets.DOCKERHUB_USERNAME }}
    password: ${{ secrets.DOCKERHUB_TOKEN }}
- name: Build and push
  uses: docker/build-push-action@v6
  with:
    push: true
    tags: user/app:latest
```

---

# Quelques actions utiles : Node


https://github.com/actions/setup-node

```yaml
- uses: actions/setup-node@v4
  with:
    node-version: 18
- run: npm ci
- run: npm test
```


Une liste d'actions selon vos besoins : https://github.com/sdras/awesome-actions

---

# Les Custom Actions

<v-clicks>

- Partageable à :
  - Projet
  - Organisation
  - Tout le monde
- 3 manières de créer des actions :
  - Image docker 
  - Javascript
  - Yaml (les composites actions)

</v-clicks>

---

# Les actions composites

But : réutiliser et partager des étapes d'un workflow

Avantages :
- Maintenance centralisée
- Simplicité et lisibilité
- DRY

---
---

````md magic-move
```yaml {all|1,2|3-7|8-11|12-14|13}
name: 'Hello World'
description: 'Greet someone'
inputs:
  who-to-greet:  # id of input
    description: 'Who to greet'
    required: true
    default: 'World'
outputs:
  random-number:
    description: "Random number"
    value: ${{ steps.random-number-generator.outputs.random-number }}
runs:
  using: "composite"
  steps:
  # ...
```
```yaml {all|9-13|15-18|5,16|5,17}
# ...
outputs:
  random-number:
    description: "Random number"
    value: ${{ steps.random-number-generator.outputs.random-number }}
runs:
  using: "composite"
  steps:
    - name: Set Greeting
      run: echo "Hello $INPUT_WHO_TO_GREET."
      shell: bash
      env:
        INPUT_WHO_TO_GREET: ${{ inputs.who-to-greet }}

    - name: Random Number Generator
      id: random-number-generator
      run: echo "random-number=$(echo $RANDOM)" >> $GITHUB_OUTPUT
      shell: bash

```
````

---
---

```yaml

# .github/actions/install-deps/action.yml
name: "Install dependencies"
description: "Install PHP dependencies"

runs:
    using: "composite"
    steps:
        - name: Setup PHP
          uses: shivammathur/setup-php@v2
          with:
              php-version: 8.3
              extensions: apcu,bcmath,intl,ldap,mbstring,opcache,pdo_pgsql,redis,xdebug,xml,zip

        - name: Restore vendors from cache
          uses: actions/cache@v4
          with:
              path: |
                  vendor
              key: ${{ runner.os }}-vendor-${{ hashFiles('composer.lock') }}
              restore-keys: |
                  ${{ runner.os }}-vendor-

        - name: Install PHP dependencies
          run: |
              /usr/local/bin/composer install --no-progress --no-scripts
          shell: bash
```

---
---

```yaml {all|7-8}
# ...
steps:
    -   uses: actions/checkout@v4
        with:
            fetch-depth: 1

    -   name: Setup common configuration
        uses: './.github/actions/install-deps'

    # ...

```

<v-click>
  <Link to="bonus">Bonus ?</Link>
</v-click>

---

# Sécurité : les secrets

Définition : des informations sensibles (clés SSH, mots de passe, clés API,...etc.)

3 niveaux pour les définir : 
- Repository
- Environnement
- Organisation


https://docs.github.com/en/actions/security-for-github-actions/security-guides/using-secrets-in-github-actions

---

# Les secrets : exemple

```yaml
# ...
steps:
  - name: Hello world action
    with: # Set the secret as an input
      super_secret: ${{ secrets.SuperSecret }}
    env: # Or as an environment variable
      super_secret: ${{ secrets.SuperSecret }}
```

<Alert type="error">
Vous ne pouvez pas utiliser les secrets directement dans vos actions.
</Alert>

<v-click>

```yaml
# ...
steps:
  - shell: bash
    env:
      SUPER_SECRET: ${{ secrets.SuperSecret }}
    run: |
      example-command "$SUPER_SECRET"
```

<Alert type="info">
Avantage : cachez les secrets dans les logs de vos jobs.
</Alert>

</v-click>

---

# Le pricing

https://docs.github.com/en/billing/managing-billing-for-your-products/managing-billing-for-github-actions/about-billing-for-github-actions

<v-click>

Gratuit sur les repo publiques et les runners self-hosted.

<Alert type="warning">
Il existe des runners plus gros que les runners normaux mais ceux-ci sont facturés sur tous les repo publiques/privés.
</Alert>

</v-click>

<v-click>

2 "unités" qui sont facturées :
- l'espace disque des GA Artifacts + Github Registry
- Le total du temps d'exécution de vos GA

</v-click>

---

# Le pricing : les quotas

Des quotas inclus selon votre compte : 

| Plan                          | Storage | Minutes (per month) |
| ----------------------------- | ------- | ------------------- |
| GitHub Free                   | 500 MB  | 2,000               |
| GitHub Pro                    | 1 GB    | 3,000               |
| GitHub Free for organizations | 500 MB  | 2,000               |
| GitHub Team                   | 2 GB    | 3,000               |

Après le quota écoulé :
- Storage : $0.008 USD / GB / jour
- Minutes:  $0.008 USD / minute




---
layout: center
class: text-center
---

# Dernier exemple : The Last Dance

<br/>

<img src="/dunk-jordan.webp" />

---

# Demo : Déployer nos slides sur Github Pages avec GA

<br/>

<PoweredBySlidev mt-10 />

- Un outil qui permet de créer ses slides en markdown en se basant sur des layouts de slides et en y appliquant un theme
- Développé en Vue
- Une application sans backend, juste du HTML/CSS/JS à builder

<Alert type="info">
Pour déployer sur Github Pages (Free Tier), il faut que le repo soit publique.
</Alert>

https://github.com/damienfern/talk_github_actions/tree/demo/deploy-gh-pages


---
layout: center
class: text-center
---

# Merci


<div class="grid grid-cols-2 items-center pt-10 gap-20" >
  <img src="/qrcode-perso.png" width="250"  height="250"  class="rounded-lg" />
  <img src="/qrcode-slides.png" width="250"  height="250"  class="rounded-lg" />
</div>

---

# Source 

- https://blog.stephane-robert.info/docs/pipeline-cicd/github/introduction/
- https://docs.github.com/en/actions

---
layout: center
class: text-center
routeAlias: bonus
---

# BONUS

<br/>

<img src="/bonus-b99.webp" />

---

Matrices

---

Cancel des actions comme Symfony

---

Publication d’un artifact auto

---

# Trigger d’un workflow si modification d’un fichier en particulier

Peut etre pas utile car déjà présenté plus haut mais alternative à voir 
https://github.com/dorny/paths-filter

---

Créer ses propres actions à mettre sur le marketplace

