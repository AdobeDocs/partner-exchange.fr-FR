---
title: Accéder au sandbox AEP et l’explorer
description: Découvrez comment accéder au sandbox Experience Platform et l’explorer.
exl-id: 62c21615-4b03-4900-a1ad-8f809c836491
TQID: https://experienceleague.adobe.com/A5sl-xNZBPjIKn6HO1iwM78IaQWQs4yBgbw9wwpMrGw
product_v2:
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
feature_v2:
  - id: fdbb8fc9-ffa3-4b86-88fe-aa4c5a3e1bc6
subfeature_v2:
  - id: b75843fa-0a67-4a44-a6b1-cc627b0481dc
  - id: fef08361-6ac5-460c-93fe-d063e40b6a49
topic_v2:
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
  - id: fd2e3797-f2ea-4b36-a9af-52acf5e90513
source-git-commit: 6698ae880d1ad13a9387cb1ba66b9ba152d1d407
workflow-type: tm+mt
source-wordcount: 772
ht-degree: 3%

---

# Accéder au sandbox AEP et l’explorer

Cet article couvre les sujets suivants :

* Les différences entre une organisation sandbox partenaire Adobe Exchange existante et la sandbox AEP partagée.
* Demande d’accès au sandbox partagé AEP.
* Réception d’une invitation par e-mail au sandbox partagé AEP.
* Invitation de nouveaux utilisateurs dans le [!DNL Admin Console].
* Navigation dans l’interface utilisateur d’AEP.

Pour une présentation générale de la technologie Sandbox dans AEP, consultez cet [article](https://docs.adobe.com/content/help/fr-FR/experience-platform/sandbox/home.html).

## Sandbox AEP partagé

Les partenaires Exchange ont accès à divers produits Adobe [!DNL Experience Cloud] (produits non AEP tels que [!DNL Analytics], [!DNL Target], balises Platform, etc.) via leur propre organisation Adobe [!DNL Experience Cloud] (non partagée). Les partenaires disposent de droits d’accès d’administrateur système à leur propre organisation pour gérer les utilisateurs et d’autres autorisations. Adobe [!DNL Experience Platform] (AEP) est traité différemment des autres sandbox Adobe. Voici les principales différences :

* L’accès à AEP ne se fera PAS par l’intermédiaire de l’organisation principale du sandbox Adobe [!DNL Experience Cloud] des partenaires.
* L’accès à AEP s’effectue via une organisation Adobe Exchange partagée.
* De nombreuses autres sociétés partenaires d’Adobe Exchange accèdent à AEP en utilisant la même organisation
   * Grâce à la fonctionnalité de sandbox d’AEP, les données et les activités de cette organisation partagée ne peuvent pas être affichées ou modifiées par les autres partenaires. Chaque partenaire aura accès à un sandbox différent au sein de l’organisation partagée.
* Les droits d’administration au sein de cette organisation partagée sont très limités.
* Après avoir obtenu l’accès à un sandbox sur AEP, les partenaires verront deux organisations dans le sélecteur d’organisations en haut à droite de l’interface utilisateur, alors qu’ils se trouvent sur la page d’accueil Admin Console ou Experience Cloud principale. Cependant, lorsqu’elle est connectée à AEP, seule l’organisation partagée doit être visible.

## Demande d’accès au sandbox AEP partagé

Envoyez une [demande d’assistance](https://adobeexchangeec.zendesk.com/hc/fr-fr/requests/new) avec les informations suivantes :

* Adresse e-mail
* Objet : Demande De Sandbox AEP
* Produit : configuration générale/sandbox
* Type de ticket : Assistance du programme - Programme Exchange / Questions sur la demande de provisionnement
* Description : fournissez une brève description du ou des cas d’utilisation de l’intégration nécessitant l’utilisation d’un sandbox AEP
* Veillez également à fournir tous les noms d’utilisateur et e-mails à ajouter au sandbox AEP. Il est possible d&#39;ajouter des utilisateurs supplémentaires une fois la demande effectuée, mais les utilisateurs devront être ajoutés par Adobe via un ticket supplémentaire (voir ci-dessous).

## Recevoir l’invitation par e-mail

Le contact principal qui a demandé le sandbox AEP recevra un e-mail automatisé l’invitant à « commencer » à utiliser le [!DNL Experience Platform] Adobe. Le contact principal disposera également de droits d’administration, qui sont abordés dans la section suivante.

Au lieu de sélectionner le bouton « commencer » dans l’e-mail, accédez directement à `https://platform.adobe.com.` Se connecter avec l’Adobe ID associée à l’adresse e-mail dans l’invitation ou créez-en une si elle n’est pas associée à une Adobe ID.

## Inviter d’autres utilisateurs

Envoyez une [demande d’assistance](https://adobeexchangeec.zendesk.com/hc/fr-fr/requests/new) avec les informations suivantes :

* Adresse e-mail du demandeur
* Objet : Sandbox AEP - Ajout D’Un Administrateur/Utilisateur
* Produit : configuration générale/sandbox
* Type de ticket : Assistance du programme - Programme Exchange / Questions sur la demande de provisionnement
* Description : liste des utilisateurs à ajouter (noms et adresses e-mail)

## Naviguer dans l’interface utilisateur d’AEP

Regardez l’interface utilisateur d’AEP [vidéo d’introduction](https://docs.adobe.com/content/help/fr-FR/platform-learn/tutorials/intro-to-platform/interface-tour.html)

Il existe 12 zones principales de l’interface utilisateur d’AEP que vous pouvez parcourir à partir du panneau de gauche. Toutefois, les sections les plus importantes pour ce type d’intégration sont les schémas, les jeux de données et les profils.

* Accueil - L’écran d’entrée

   * Suggère des activités de prise en main
   * Fournit quelques liens vers le contenu de formation
   * Donne une vue de tableau de bord pour certains des principaux objets AEP, tels que les schémas, les jeux de données et les profils

* Workflows : lancement dans des workflows courants pour importer des données dans AEP
* Connexions/Sources : gérez les sources de données qui entrent dans AEP.
* Connexions/destinations : gérez les connexions pour envoyer des données à des systèmes externes.
* Profils : affichage et gestion des profils clients individuels
* Segments - parcourez, créez et modifiez des segments clients
* Identités : parcourez, créez et modifiez des espaces de noms d’identité ; il s’agit des types d’identifiants principaux utilisés pour identifier de manière unique un client
* Modèles (science des données) : participez à des activités de science des données, y compris l’utilisation d’un environnement Jupyter Notebooks intégré.
* Services (science des données) : publication de recettes de science des données en tant que services
* Schémas : parcourez, créez et modifiez des schémas. Il s’agit des définitions de données détaillées utilisées pour organiser les données
* Jeux de données : parcourez, créez et gérez des jeux de données. Un jeu de données est défini par un schéma et correspond à l’emplacement des données dans AEP
* Requêtes - Parcourez, créez, modifiez et utilisez un référentiel de requêtes pour obtenir des informations à partir des données des jeux de données
* Surveillance : affichez le statut de toutes les données qui entrent et sortent d’AEP pour les traitements par lots et par flux
