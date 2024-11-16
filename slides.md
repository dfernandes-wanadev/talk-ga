---
# You can also start simply with 'default'
theme: ./
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://cover.sli.dev
colorSchema: "both"
highlighter: "all"
lineNumber: true

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

Lead Dev chez WanadevDigital depuis 2 ans et demi

- Vue, Typescript
- PHP, Symfony
- DevOps


Travaille principalement sur le projet Kazaplan

<!-- TODO : insert Wanadev digital logo -->

---

Présentation Kazaplan

---


Présentation problématique 

Migrer le BO de Gitlab vers Github Action

---

Introduction brève à la CI/CD avec les différents outils possibles (voir liste au dessus)

---

Introduction et présentation d’une CI GItlab avec les stages et présenter la philosophie (avec les rules et except/only)

---

Présentation Github Actions 

---

Présentation sur la philosophie basé sur les évènements du repo

---

Intégration du terme workflow 

---

Intégration des jobs (parallèle auto sauf si deps déclarés)

---

Introduction aux runners

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
layout: center
class: text-center
---

# Learn More

[Documentation](https://sli.dev) · [GitHub](https://github.com/slidevjs/slidev) · [Showcases](https://sli.dev/resources/showcases)

<PoweredBySlidev mt-10 />
