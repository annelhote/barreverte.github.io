---
layout: post
title: L'écoconception pour les devs, de l'optimisation ?
author:
  display_name: Bruno Thomas
tags:
- greenIT
comments: true
---

Lors de l'[Agile Open France](http://agileopenfrance.com/), j'ai été déçu que mon sujet sur l'écoconception n'ait pas attiré grand monde : nous étions au plus 5. Pour ceux qui ne connaissent pas l'événement, il y a beaucoup d'indépendants, *coaches* et *software craftmen* passionnés. C'est précisément ce qui m'intéressait : l'avis d'experts du développement. Mais le peu de personnes "votant avec leurs pieds" pour l'écoconception était déjà un enseignement, et grâce aux personnes qui sont venues échanger sur le sujet (merci à elles), j'ai pu comprendre pourquoi.

> "c'est un problème d'optimisation, ça coûte"

Effectivement, c'est un soucis d'efficacité. Et ce problème est souvent abordé par nécessité économique. Lorsque vous faites en sorte d'utiliser 5 serveurs au lieu de 20 pour le même nombre d'utilisateurs, afin de baisser les coûts d'exploitation de votre service, vous faites de l'écoconception.

On retrouve la proximité entre les termes **éco-nomique** (de "*[Oikos](https://fr.wikipedia.org/wiki/Oikos)*" la maison, "*[nomos](https://fr.wiktionary.org/wiki/nomos)*" l'administration) et **éco-logique** ("*[logos](https://fr.wikipedia.org/wiki/Logos)*" le récit). Ce n'est pas toujours le cas, mais dans l'exploitation de services web, l'amélioration des performances économiques va souvent de pair avec celle des performances écologiques.

Et donc, ce n'est pas un sujet, car un bon *craftman* ou artisant logiciel, gardera toujours en tête l'efficacité des programmes qu'il développe, sans en faire une priorité.

> "L'optimisation prématurée est la racine de tous les maux" -- [Donald Knuth](http://wiki.c2.com/?PrematureOptimization)

Car de l'autre côté, si on considère non plus l'efficacité de l'exploitation des programmes sur les serveurs, mais l'efficacité du développement et de la maintenance de ces programmes, l'optimisation coûte, et peut même coûter très cher. Souvent l'optimisation du code d'un programme est antinomique avec sa lisibilité et sa testabilité : l'amélioration du temps de traitement d'un programme par la machine demandera à l'humain plus d'efforts pour le comprendre. Essayez de lire de l'assembleur, du javascript minifié ou du bytecode. Essayez également de poser des tests unitaires sur du code Java principalement statique.

Plus le code est optimisé, plus il sera cher à élaborer et à maintenir. Les sociétés qui développent les services veulent minimiser les coûts de développement. Il existe une certaine inadéquation entre ces coûts de développement et les coûts d'exploitation. Calculer le ROI en exploitation d'un investissement d'optimisation du code n'est pas simple besogne.

## Optimisation certes, et aussi

### des choix technologiques

En tant que développeur, on peut améliorer son code pour consommer moins de CPU, de mémoire et de réseau. C'est vrai pour un environnement donné mais qu'en est-il de l'impact sur la consommation d'énergie d'un serveur d'application en PHP, Java, python, nodeJS, ruby, etc. ?

[Un article](https://hal.inria.fr/hal-00681560v3/document) du CNRS à propos de la "[réduction de consommation énergétique des logiciels](http://www.cnrs.fr/ins2i/spip.php?article2365)" traite des différences entre plusieurs langages. En [mesurant la consommation électrique](http://powerapi.org/) d'un programme de résolution du problème de la tour de Hanoï écrit en différents langages, ils ont mis en évidence que :

> Pour une même application, un langage interprété comme Python consomme 100 fois plus qu’un langage compilé comme Java. (...) pour les langages compilés orientés objets, Java consomme moins que du C++ avec les options par défaut et autant en niveau d'optimisation O3.

Ces différences sont liées à la nature du programme orienté calcul (et donc utilisant quasiment exclusivement le CPU), par opposition à un programme orienté entrées/sorties. Un serveur d'application faisant du web en architecture 3 tiers, sera plutôt lié à l'optimisation de l'utilisation des entrées/sorties réseau.

La programmation asynchrone est par exemple une bonne alternative pour les programmes orientés entrées/sorties

Mais ce que montre l'article, c'est que l'environnement technologique aura des conséquences importantes sur la puissance consommée par les serveurs.

### obsolescence programmée

Si on prend en compte le cycle de vie des produits technologiques, une grande partie des gâchis générés par les nouvelles technologies est liée au rythme d'obsolescence des produits. Par exemple un mobile est changé tous les 18 mois en moyenne, alors qu'il serait capable de fonctionner jusqu'à 5 à 7 ans. La fréquentation de sites qui ne sont pas adaptés peuvent pousser certains internautes à changer leurs terminaux. Lors du développement d'un site, il est possible de prendre en compte la compatibilité avec d'anciens appareils.

En tant que développeur nous pouvons faire en sorte qu'un site se "dégrade" tout en restant fonctionnel : les bords ronds d'une CSS3 seront carrés, le *smooth scrolling* en javascript n'est pas rendu, mais la page est chargée, ou l'ancre atteinte, etc. En faisant de la sorte, nos utilisateurs peuvent consulter nos sites même avec un vieux mobile, et nous ne pesons pas dans leur décision de changer de mobile.

En revanche, cela demande généralement de consacrer plus de temps au développement, pour tester le site avec différents mobiles, et adapter le code en fonction des manquements.

### respect des standards