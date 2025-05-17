---
layout: post
title: "Gestion des conflits de dépendances avec Maven"
description: "Comprendre et résoudre les conflits de dépendances dans les projets Java avec Maven"
summary: "Un guide pour identifier, comprendre et résoudre les conflits de versions entre dépendances Maven dans vos projets Java"
comments: true
tags: [java, maven, dépendances, spring]
---

Lorsqu'on travaille avec des projets Java, on utilise souvent des librairies (dépendances) qui viennent avec leurs propres dépendances; c'est ce qu'on appelle des dépendances transitives. Il est très fréquent pour des librairies de dépendre de différentes versions d'une même dépendance, ce qui peut conduire à des conflits de versions. Ces conflits peuvent provoquer des erreurs à la compilation ou au runtime, rendant le diagnostic difficile. Maven fournit une stratégie claire pour résoudre ce genre de conflits.

Maven résout les conflits de dépendances en utilisant la stratégie de la définition la plus proche (aussi appelée chemin le plus court) : 

{: .indented-list}
1. La version utilisée est celle de la dépendance qui est la plus proche de la racine de l'arbre de dépendance.
2. Si deux dépendances en conflit sont au même niveau, la première déclarée dans le POM est utilisée.

Dans l'exemple suivant, la librairie `library-A:1.0` sera utilisée car elle se retrouve au niveau 1 (directement déclarée dans le POM), même si `library-B` dépend d'une version plus récente.

Déclaration des dépendances :

```xml
<dependencies>
    <dependency>
        <groupId>org.example</groupId>
        <artifactId>library-A</artifactId>
        <version>1.0</version>
    </dependency>
    <dependency>
        <groupId>org.example</groupId>
        <artifactId>library-B</artifactId>
        <version>2.0</version>
    </dependency>
</dependencies>
```

Arbre des dépendances :

```
my-app
├── library-A:1.0         (depth 1)
└── library-B:2.0         (depth 1)
    └── library-A:2.0     (depth 2)
```

## Identification des conflits

Pour identifier les conflits de dépendances, on peut examiner l'arbre de dépendances soit directement dans l'IDE ou via la commande : 

```
mvn dependency:tree
```

Pour un diagnostic plus détaillé, utilisez l'option verbose :

```
mvn dependency:tree -Dverbose
```

Cette commande fournit une vue claire de l'arbre complet des dépendances, ainsi que les versions utilisées et celles qui sont omises pour cause de conflit.

## Résolution des conflits avec dependencyManagement

Une bonne pratique pour résoudre les conflits de dépendances est d'utiliser le tag `<dependencyManagement>`. Cette section donne plus de contrôle sur les versions utilisées dans le projet sans ajouter directement les dépendances.

Par exemple ici `library-A` sera utilisée dans sa version `2.0` à travers tout le projet, peu importe les versions rencontrées dans les déclarations transitives :

```xml
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>org.example</groupId>
            <artifactId>library-A</artifactId>
            <version>2.0</version>
        </dependency>
    </dependencies>
</dependencyManagement>
```

Il est important de noter que déclarer une dépendance dans `<dependencyManagement>` ne l'ajoute pas au projet. Il faudra toujours la déclarer dans la section `<dependencies>`, mais sans préciser de version :

```xml
<dependencies>
    <dependency>
        <groupId>org.example</groupId>
        <artifactId>library-A</artifactId>
        <!-- Pas besoin de spécifier la version ici -->
    </dependency>
</dependencies>
```

## Utilisation des exclusions

Parfois, vous pourriez avoir besoin d'exclure explicitement une dépendance transitive. Par exemple, si `library-B` dépend d'une version de `library-A` qui n'est pas compatible avec votre code :

```xml
<dependency>
    <groupId>org.example</groupId>
    <artifactId>library-B</artifactId>
    <version>2.0</version>
    <exclusions>
        <exclusion>
            <groupId>org.example</groupId>
            <artifactId>library-A</artifactId>
        </exclusion>
    </exclusions>
</dependency>
```

## Cas pratiques

Les conflits de dépendances ne sont pas forcément à résoudre. Le projet peut compiler et fonctionner comme il se doit avec des conflits de dépendances que Maven gère selon les règles mentionnées plus haut. Toutefois pour des soucis de cohérence il faut parfois s'assurer d'utiliser la bonne version.

Par exemple, dans un projet Spring, on peut rencontrer différentes versions de `spring-core` (par transitivité). Il est recommandé d'utiliser `<dependencyManagement>` afin de s'assurer d'utiliser une même version à travers tous les composants Spring.

On peut aussi rencontrer des problèmes lorsqu'une nouvelle version d'une librairie apporte des changements non compatibles avec des versions antérieures. Dans ce cas il faut : 

{: .indented-list}
* identifier les dépendances utilisant la nouvelle version
* mettre à jour le code avec la nouvelle API
* ou utiliser les **exclusions** et dépendre explicitement de l'ancienne librairie

## Outils supplémentaires

Pour une analyse plus poussée de vos dépendances, utilisez la commande :

```
mvn dependency:analyze
```

Cette commande identifie les dépendances utilisées mais non déclarées, ainsi que celles déclarées mais non utilisées, ce qui vous aide à optimiser votre POM.

## Utilisation des BOM (Bill of Materials)

Pour les projets complexes, l'utilisation d'un BOM peut grandement simplifier la gestion des versions :

```xml
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-dependencies</artifactId>
            <version>2.7.0</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
```

Cela importe toutes les versions de dépendances compatibles définies par Spring Boot, évitant ainsi de nombreux conflits potentiels.
