---
layout: post
title: La Règle des 37%
description: Comment utiliser la théorie mathématique d'arrêt optimal pour prendre de meilleures décisions séquentielles
summary: Une explication de la règle des 37% issue du problème du secrétaire et son application dans la vie quotidienne
comments: true
tags: [algorithms, maths, books]
---

La règle des 37% trouve son origine dans le "problème du secrétaire", un classique de la théorie d'arrêt optimal. Dans ce problème, un recruteur doit embaucher un secrétaire parmi un nombre fini de candidats qu'il rencontre un par un. Après chaque entretien, il doit décider immédiatement : embaucher ce candidat ou passer au suivant, sans possibilité de rappel.

Le défi est que le recruteur ne peut pas attribuer une note absolue aux candidats, seulement les comparer entre eux. La question devient donc : quelle stratégie adopter pour maximiser les chances de sélectionner le meilleur candidat?

La stratégie optimale, démontrée mathématiquement, consiste à:

1. Observer (sans choisir) les 37% premiers candidats
2. Identifier le meilleur candidat de ce groupe initial
3. Ensuite, sélectionner le premier candidat qui surpasse cette référence

Le chiffre 37% correspond plus précisément à 1/e, où e est le nombre d'Euler (≈ 2,718). Cette formule garantit une probabilité de 37% de sélectionner le meilleur candidat possible - ce qui est le maximum atteignable dans ce contexte.

Cette règle s'applique à diverses situations impliquant des choix séquentiels: recherche immobilière (explorer 37% des options disponibles avant de prendre une décision), recrutement (évaluer 37% des candidatures avant de commencer à embaucher), ou rencontres (consacrer 37% du temps disponible à explorer avant de s'engager).

La règle fonctionne de manière optimale lorsque le nombre total d'options est connu à l'avance, les décisions sont irréversibles, et l'objectif est uniquement de trouver la meilleure option.

J'ai découvert cette règle dans le livre [Algorithms to Live By](https://amzn.eu/d/aOFENnk). Elle offre un cadre structuré pour aborder les décisions séquentielles et éviter deux erreurs communes: choisir trop tôt par impatience ou trop tard par perfectionnisme.

Le chiffre 37% constitue donc un point de référence précis et efficace pour les situations de choix séquentiels où l'on ne peut pas revenir en arrière.