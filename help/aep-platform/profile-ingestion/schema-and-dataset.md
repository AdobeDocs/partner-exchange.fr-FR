---
title: Création de schémas et de jeux de données AEP
description: Création de schémas et de jeux de données dans Experience Platform.
exl-id: a2773551-20a3-4a5b-ab53-60fa67e38ec0
TQID: https://experienceleague.adobe.com/uQtIQwCgsjOd5pR5w4LF634-Whvjl0jmF5WywVWlkZQ
product_v2: id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 6698ae880d1ad13a9387cb1ba66b9ba152d1d407
workflow-type: tm+mt
source-wordcount: 617
ht-degree: 25%

---

# Création de schémas et de jeux de données

La collection [](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman) est référencée tout au long de l’article à l’aide des appels associés par numéro. Pour plus d’informations sur l’installation et l’utilisation de la collection Postman, consultez la page Github [README](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/README.md). Il existe également des exemples de jeux de données de données [fidélité](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20events.json) et [profil](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20profiles.json).

## Schémas

Un schéma est un jeu de règles qui représente et valide la structure et le format des données. À un niveau élevé, les schémas fournissent une définition abstraite d’un objet du monde réel (une personne, par exemple) et indiquent les données à inclure dans chaque instance de cet objet (comme le prénom, le nom, l’anniversaire, etc.). Les schémas peuvent être créés dans l’interface utilisateur ou à l’aide des API [!DNL Experience Platform].

Voir [cette documentation](https://www.adobe.io/apis/experienceplatform/home/xdm/xdmservices.html#!api-specification/markdown/narrative/technical_overview/schema_registry/schema_composition/schema_composition.md) pour plus d’informations.

### Créer un schéma

Les partenaires peuvent créer un schéma à l’aide de l’interface utilisateur en suivant ce [tutoriel](https://docs.adobe.com/content/help/en/experience-platform/xdm/tutorials/create-schema-ui.html). Cet exemple utilise le schéma de profil du programme de fidélité . Bien que l’exemple soit un schéma de profil, les schémas basés sur un événement peuvent être utilisés à l’aide d’un processus similaire.

Pour utiliser les API, les partenaires doivent disposer d’une intégration Adobe I/O existante avec les autorisations [!DNL Experience Platform] activées. Consultez ce guide pour [créer une intégration d’E/S](https://docs.adobe.com/content/help/fr-FR/experience-platform/tutorials/home.html#!api-specification/markdown/narrative/tutorials/authenticate_to_acp_tutorial/authenticate_to_acp_tutorial.md).

Rendez-vous ensuite sur [ce lien](https://docs.adobe.com/content/help/en/experience-platform/xdm/tutorials/create-schema-api.html) pour savoir comment créer des schémas à l’aide de l’API.

Pour créer un schéma via Postman, utilisez les appels contenus dans les dossiers 1 : Créer un schéma, 1a : Créer un schéma pour les données PROFILE OU 1b : Créer un schéma pour les données EVENT.

## Jeux de données

Toutes les données introduites dans Adobe [!DNL Experience Platform] sont contenues dans des jeux de données. Un jeu de données est une structure de stockage et de gestion pour une collection de données, généralement sous la forme d’un tableau, qui contient un schéma (des colonnes) et des champs (des lignes). Les jeux de données contiennent également des métadonnées qui décrivent divers aspects des données stockées.

Le service de catalogue est le système d’enregistrement de l’emplacement et de la traçabilité des données dans [!DNL Experience Platform]. Il est utilisé pour créer et gérer les jeux de données. Le catalogue suit les métadonnées de chaque jeu de données, ce qui inclut une référence au schéma XDM (modèle de données d’expérience) auquel le jeu de données se conforme (expliqué dans la section suivante) et le nombre d’enregistrements ingérés par ce jeu de données.

Accédez [ici](https://docs.adobe.com/content/help/en/experience-platform/catalog/datasets/overview.html) pour une présentation détaillée du jeu de données.

### Créer un jeu de données

![Création D’Un Gif Animé De Jeu De Données](images/creating_a_dataset.gif)

<!-- 
We don't yet support hover text in images (and we render it poorly when included). I removed "Creating a Dataset" from the above image link. We can add it back when we support it (Summer 2020?) -Bob
-->

Créez un jeu de données via l’interface utilisateur :

1. Cliquez sur **[!UICONTROL Créer un jeu de données]**.

1. Cliquez sur **[!UICONTROL Créer à partir d’un schéma]**.

1. Cliquez sur **[!UICONTROL Terminer]**.

Accédez [ici](https://docs.adobe.com/content/help/en/experience-platform/catalog/datasets/user-guide.html) pour obtenir un guide d’utilisation des jeux de données.

[Créer un jeu de données à l’aide des API](https://docs.adobe.com/content/help/en/experience-platform/catalog/datasets/create.html).

Pour créer un jeu de données via Postman, utilisez les dossiers 2 : Créer un jeu de données, 2a : Créer un jeu de données pour les données PROFILE OU 2b : Créer un jeu de données pour les données EVENT.

## Bonnes pratiques relatives aux schémas et aux jeux de données pour les partenaires

* Les données de partenaire doivent utiliser un schéma de profil distinct plutôt que de créer un mixin pour le schéma de profil et le schéma d’expérience existants d’un client.
* Dans la mesure du possible, les partenaires doivent utiliser les classes et les mixins d’Adobe.
* Les partenaires doivent charger leurs données à l’aide d’un jeu de données distinct au lieu d’essayer de combiner leurs données dans un jeu de données existant.
* Les partenaires ne peuvent pas charger leurs schémas dans le registre global pour l’instant.
