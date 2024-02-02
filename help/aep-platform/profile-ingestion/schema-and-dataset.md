---
title: Création de schémas et de jeux de données AEP
description: Créez des schémas et des jeux de données dans Experience Platform.
exl-id: a2773551-20a3-4a5b-ab53-60fa67e38ec0
source-git-commit: fe7519c35fb9155ce54cad85941c887f15881a38
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 20%

---

# Création de schémas et de jeux de données

La variable [Collection Postman](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman) est référencé tout au long de l’article à l’aide des appels associés par numéro. Pour plus d’informations sur l’installation et l’utilisation de la collection Postman, voir Github . [LISEZMOI](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/README.md) page. Il existe également des exemples de jeux de données de [loyalty](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20events.json) et [profile](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20profiles.json) data.

## Schémas

Un schéma est un jeu de règles qui représente et valide la structure et le format des données. À un niveau élevé, les schémas fournissent une définition abstraite d’un objet du monde réel (une personne, par exemple) et indiquent les données à inclure dans chaque instance de cet objet (prénom, nom, anniversaire, etc.). Les schémas peuvent être créés dans l’interface utilisateur ou à l’aide de la fonction [!DNL Experience Platform] API.

Voir [cette documentation](https://www.adobe.io/apis/experienceplatform/home/xdm/xdmservices.html#!api-specification/markdown/narrative/technical_overview/schema_registry/schema_composition/schema_composition.md) pour plus d’informations.

### Créer un schéma

Les partenaires peuvent créer un schéma à l’aide de l’interface utilisateur en procédant comme suit : [tutoriel](https://docs.adobe.com/content/help/fr-FR/experience-platform/xdm/tutorials/create-schema-ui.html). Cet exemple utilise le schéma de profil du programme de fidélité. Bien que l’exemple soit un schéma de profil, les schémas basés sur un événement peuvent être utilisés à l’aide d’un processus similaire.

Pour utiliser les API, les partenaires doivent disposer d’une intégration d’Adobe I/O existante avec [!DNL Experience Platform] autorisations activées. Consultez ce guide pour [créer une intégration I/O ;](https://docs.adobe.com/content/help/fr-FR/experience-platform/tutorials/home.html#!api-specification/markdown/narrative/tutorials/authenticate_to_acp_tutorial/authenticate_to_acp_tutorial.md).

Ensuite, visite [ce lien](https://docs.adobe.com/content/help/en/experience-platform/xdm/tutorials/create-schema-api.html) pour savoir comment créer des schémas à l’aide de l’API.

Pour créer un schéma via Postman, utilisez les appels contenus dans les dossiers 1 : Créer un schéma, 1a : Créer un schéma pour les données de PROFIL OU 1b : Créer un schéma pour les données d’ÉVÉNEMENT.

## Jeux de données

Toutes les données introduites dans Adobe [!DNL Experience Platform] est contenu dans les jeux de données. Un jeu de données est une structure de stockage et de gestion pour la collecte de données, généralement sous la forme d’un tableau, qui contient un schéma (des colonnes) et des champs (des lignes). Les jeux de données contiennent également des métadonnées qui décrivent divers aspects des données stockées.

Le service de catalogue est le système d’enregistrement de l’emplacement et de la traçabilité des données dans [!DNL Experience Platform], et est utilisé pour créer et gérer des jeux de données. Le catalogue suit les métadonnées de chaque jeu de données, ce qui inclut une référence au schéma XDM (modèle de données d’expérience) auquel le jeu de données se conforme (expliqué dans la section suivante) et le nombre d’enregistrements ingérés par ce jeu de données.

Aller [here](https://docs.adobe.com/content/help/en/experience-platform/catalog/datasets/overview.html) pour obtenir un aperçu détaillé du jeu de données.

### Créer un jeu de données

![Création d’un jeu de données animé](images/creating_a_dataset.gif)

<!-- 
We don't yet support hover text in images (and we render it poorly when included). I removed "Creating a Dataset" from the above image link. We can add it back when we support it (Summer 2020?) -Bob
-->

Créez un jeu de données via l’interface utilisateur :

1. Cliquez sur **[!UICONTROL Créer un jeu de données]**.

1. Cliquez sur **[!UICONTROL Création à partir d’un schéma]**.

1. Cliquez sur **[!UICONTROL Terminer]**.

Aller [here](https://docs.adobe.com/content/help/en/experience-platform/catalog/datasets/user-guide.html) pour un guide d’utilisation de jeux de données.

[Création d’un jeu de données à l’aide des API](https://docs.adobe.com/content/help/en/experience-platform/catalog/datasets/create.html).

Pour créer un jeu de données via Postman, utilisez les dossiers 2 : Créer un jeu de données, 2a : Créer un jeu de données pour les données PROFIL OU 2b : Créer un jeu de données pour les données EVENT.

## Bonnes pratiques relatives aux schémas et aux jeux de données pour les partenaires

* Les données du partenaire doivent utiliser un schéma de profil distinct et créer un mixin pour le schéma de profil et d’expérience existants d’un client.
* Si possible, les partenaires doivent utiliser des classes d’Adobe et des mixins.
* Les partenaires doivent charger leurs données à l’aide d’un jeu de données distinct au lieu d’essayer de combiner leurs données dans un jeu de données existant.
* Les partenaires ne peuvent pas charger leurs schémas dans le registre global pour l’instant.
