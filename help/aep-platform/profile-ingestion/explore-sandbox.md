---
title: Accès et exploration de l’environnement de test AEP
description: Découvrez comment accéder à l’environnement de test Experience Platform et l’explorer.
exl-id: 62c21615-4b03-4900-a1ad-8f809c836491
source-git-commit: fe7519c35fb9155ce54cad85941c887f15881a38
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 0%

---

# Accès et exploration de l’environnement de test AEP

Cet article traite des sujets suivants :

* Différences entre une organisation sandbox de partenaire d’Adobe Exchange existante et l’environnement de test AEP partagé.
* Demande d’accès à l’environnement de test partagé AEP.
* Recevoir une invitation par courrier électronique à rejoindre l’environnement de test partagé AEP.
* Invitation de nouveaux utilisateurs dans le [!DNL Admin Console].
* Navigation dans l’interface utilisateur AEP.

Pour un aperçu général de la technologie Sandbox dans AEP, consultez cet [article](https://docs.adobe.com/content/help/fr-FR/experience-platform/sandbox/home.html).

## Environnement de test AEP partagé

Les partenaires d’Exchange ont accès à divers produits d’Adobe [!DNL Experience Cloud] (produits non AEP tels que [!DNL Analytics], [!DNL Target], balises de plateforme, etc.) via leur propre organisation [!DNL Experience Cloud] d’Adobe (non partagée). Les partenaires disposent de droits d’accès d’administrateur système à leur propre organisation pour gérer les utilisateurs et d’autres autorisations. L’Adobe [!DNL Experience Platform] (AEP) est traité différemment des autres environnements de test d’Adobe. Voici les principales différences :

* L’accès à AEP ne sera PAS possible via l’organisation sandbox de l’Adobe principal [!DNL Experience Cloud] des partenaires.
* L’accès à AEP se fait par le biais d’une organisation d’Adobe Exchange partagée.
* De nombreuses autres sociétés partenaires d’Adobe Exchange accèdent à AEP en utilisant la même organisation.
   * Par le biais de la fonction sandbox AEP, les données et les activités de cette organisation partagée ne peuvent pas être vues ni modifiées par les autres partenaires ; chaque partenaire aura accès à un sandbox différent au sein de l’organisation partagée.
* Les droits d’administration au sein de cette organisation partagée sont très limités.
* Une fois que vous avez accès à un environnement de test sur AEP, deux organisations s’affichent sur le sélecteur d’organisation en haut à droite de l’interface utilisateur lors de l’accès à la page d’accueil de l’Admin Console ou de l’Experience Cloud principal. Cependant, lorsque vous êtes connecté à AEP, seule l’organisation partagée doit être visible.

## Demande d’accès à l’environnement de test AEP partagé

Envoyez une [demande de support](https://adobeexchangeec.zendesk.com/hc/fr-fr/requests/new) avec les informations suivantes :

* Adresse e-mail
* Objet : Demande d’environnement de test AEP
* Produit : configuration générale/sandbox
* Type de ticket : Programme d’assistance - Exchange Programme / questions de configuration
* Description : fournissez une brève description du ou des cas pratiques d’intégration qui nécessitent l’utilisation d’un environnement de test AEP.
* Veillez également à fournir tous les noms d’utilisateur et e-mails à ajouter à l’environnement de test AEP. Il est possible d’ajouter d’autres utilisateurs une fois la demande effectuée, mais les utilisateurs devront être ajoutés par Adobe via un ticket supplémentaire (voir ci-dessous).

## Réception de l’invitation par courrier électronique

Le contact principal qui a demandé l’environnement de test AEP recevra un courrier électronique automatisé l’invitant à &quot;démarrer&quot; avec l’Adobe [!DNL Experience Platform]. Le contact principal disposera également de certains privilèges d&#39;administration, qui sont décrits dans la section suivante.

Au lieu de sélectionner le bouton &quot;Commencer&quot; dans le courrier électronique, accédez directement à `https://platform.adobe.com.` Connectez-vous à l’Adobe ID associé à l’adresse électronique dans l’invitation ou créez-en une si elle n’est pas associée à une Adobe ID.

## Invitation d’autres utilisateurs

Envoyez une [demande de support](https://adobeexchangeec.zendesk.com/hc/fr-fr/requests/new) avec les informations suivantes :

* Adresse électronique du demandeur
* Objet : sandbox AEP - Ajouter un administrateur/utilisateur
* Produit : configuration générale/sandbox
* Type de ticket : Programme d’assistance - Exchange Programme / questions de configuration
* Description : Liste des utilisateurs à ajouter (noms et emails)

## Navigation dans l’interface utilisateur AEP

Regardez la [vidéo d&#39;introduction](https://docs.adobe.com/content/help/fr-FR/platform-learn/tutorials/intro-to-platform/interface-tour.html) de l&#39;interface utilisateur AEP

Il existe 12 zones principales de l’interface utilisateur AEP qui peuvent être naviguées via le panneau de gauche. Toutefois, les sections les plus importantes pour ce type d’intégration sont les schémas, les jeux de données et les profils.

* Accueil - écran d’entrée

   * Suggestion d’activités de prise en main
   * Fournit quelques liens vers du contenu d’apprentissage
   * Donne une vue de tableau de bord pour certains des objets AEP principaux, tels que les schémas, les jeux de données et les profils

* Workflows : lancement dans des workflows courants pour importer des données dans AEP
* Connexions / Sources - Gestion des sources de données entrant dans AEP
* Connexions / Destinations : gérez les connexions pour envoyer des données à des systèmes externes.
* Profils : affichage et gestion des profils client individuels
* Segments : parcourir, créer et modifier des segments client
* Identités : recherchez, créez et modifiez des espaces de noms d’identité. Il s’agit des types d’identifiants principaux utilisés pour identifier de manière unique un client.
* Modèles (Data Science) : participez à des activités Data Science, notamment à l’utilisation d’un environnement de notebooks Jupyter intégré.
* Services (Data Science) - publier des recettes de science des données en tant que services
* Schémas : recherchez, créez et modifiez des schémas. Il s’agit des définitions de données détaillées utilisées pour organiser les données.
* Visionneuses de données : parcourez, créez et gérez des jeux de données ; un jeu de données est défini par un schéma et est l’emplacement où se trouvent les données dans AEP.
* Requêtes : parcourez, créez, modifiez et utilisez un référentiel de requêtes pour obtenir des informations à partir des données des jeux de données.
* Surveillance : affichez l’état de toutes les données qui entrent et sortent d’AEP pour le traitement par lot et la diffusion en continu.
