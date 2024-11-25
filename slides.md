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


<!-- But de la présentation :
- vous aider à mieux comprendre GA
- 
- vous donner des tips 
-->

---
layout: quote
---

# <span v-mark>Disclaimer</span>


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
    <img src="/gitlab-ci-logo.png" width="150" height="150" v-click />
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

<!-- TODO : use Tailwind Alert -->
- Github Actions sera abrégé en GA

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

Tip: Certains events ne se trigger seulement avec les fichiers YAML présents sur la branche par défaut.

</v-click>

<!-- TODO : use Tailwind Alert -->

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

Intégration des actions

---

Intégration du marketplace : sélectionner quelques actions pour le php

---

Intégration du cache avec gestion des ID

---

Intégration des actions composites

---

Trigger d’un workflow si modification d’un fichier en particulier


---

Matrices

---

Cancel des actions comme Symfony

---

Publication d’un artifact auto

---

Créer ses propres actions à mettre sur le marketplace

---

Sécurité

---

Le pricing repo privé/public
---

# Source 

https://blog.stephane-robert.info/docs/pipeline-cicd/github/introduction/
Doc github actions

---
layout: center
class: text-center
---

# Learn More

[Documentation](https://sli.dev) · [GitHub](https://github.com/slidevjs/slidev) · [Showcases](https://sli.dev/resources/showcases)

<PoweredBySlidev mt-10 />
