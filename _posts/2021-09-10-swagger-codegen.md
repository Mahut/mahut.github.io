---
layout: post
title: Swagger Codegen
description: 
summary: 
comments: true
tags: [swagger]
---


Récemment au travail, nous avions eu besoin de connecter à l'API REST d’un SAAS, le progiciel autour duquel nous effectuons nos développements. La documentation de l’API nous a été fournie sous forme de spécification Swagger. Nos développements se faisant essentiellement en Java, nous avons donc besoin d’implémenter un client d’API REST en Java. La méthode naïve aurait été de partir du Swagger et de tout construire manuellement à partir de la description des modèles, des opérations etc. mais la tâche me semblait plutôt fastidieuse.

Après quelques recherches, j’ai découvert [Swagger Codegen](https://swagger.io/docs/open-source-tools/swagger-codegen/). Il s’agit d’un utilitaire qui permet la génération automatique de clients d’API REST, de stubs de serveurs et de documentation, et ce à partir d’une spécification [OpenAPI](https://github.com/OAI/OpenAPI-Specification). Plusieurs langages et frameworks sont supportés dont Java.

Swagger Codegen est téléchargeable sous forme de fichier .jar et peut se lancer en ligne de commande avec un `java -jar` : 

```
java -jar swagger-codegen-cli-2.2.1.jar generate -i specification-api-swagger.json -l java rest-client/
```

La spécification de l'API avec laquelle on doit communique est sous forme de fichier .json qu'on peut télécharger depuis la page HTML de la documentation Swagger. Elle est passée à la commande avec l'argument `-i`. `-l` est utilisé pour spécifier le langage dans lequel l'on souhaite générer le code pour notre client REST.

Et voilà! Swagger Codegen nous génère un projet Java Maven bien structurée avec les POJO représentant le modèle de donnée, les utilitaires pour effecturer les appels d'API, la gestion de l'authentification et même la document Javadoc, ... Ce projet peut désormais servir de base pour démarrer l'implémentation de notre client REST et permettre d'aller plus vite.

Pour plus d'infos : [https://swagger.io/docs/open-source-tools/swagger-codegen/](https://swagger.io/docs/open-source-tools/swagger-codegen/)
