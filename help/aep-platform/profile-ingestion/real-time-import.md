---
title: Importation en temps réel
description: Découvrez comment importer des données dans AEP en temps réel.
exl-id: 0b6215a9-1160-49ae-8aa5-302b47357200
source-git-commit: fe7519c35fb9155ce54cad85941c887f15881a38
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 2%

---

# Diffusion de données en continu vers AEP

Adobe [!DNL Experience Platform] permet de diffuser en continu des événements de profil et d’expérience et de les rendre disponibles en temps quasi réel. Toutes les données envoyées à AEP par flux sont conservées dans le lac de données. Les données peuvent être diffusées en continu vers des jeux de données existants ou des jeux de données entièrement nouveaux via des API ou à l’aide d’Adobe Launch.

Cet article traite des sujets suivants :

* Diffusion en continu vers XDM Individual Profile
* Diffusion en continu vers XDM ExperienceEvent
* Utilisation de l’extension Launch pour la diffusion

La variable [Collection Postman](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman) est référencé tout au long de l’article à l’aide des appels associés par numéro. Pour plus d’informations sur l’installation et l’utilisation de la collection Postman, voir Github . [LISEZMOI](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/README.md) page. Il existe également des exemples de jeux de données de [loyalty](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20events.json) et [profile](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20profiles.json) data.

## Conditions préalables

* [Authentification à la plateforme](https://docs.adobe.com/content/help/fr-FR/experience-platform/tutorials/authentication.html).
* Rassemblez les valeurs des en-têtes requis à partir du tutoriel sur l’authentification lié ci-dessus.

## Création d’une connexion en continu

Pour diffuser vers AEP, vous devez d’abord créer une connexion en continu. Les connexions en flux continu contiennent des attributs tels que la source des données en flux continu et si vous envoyez ou non des enregistrements appartenant à la variable [!DNL Experience Data Model] schémas (XDM). Après avoir créé une connexion en continu, vous recevez une URL unique que vous utilisez pour diffuser des données dans AEP.

Aller [here](https://docs.adobe.com/content/help/en/experience-platform/ingestion/tutorials/create-streaming-connection.html) pour obtenir des instructions sur la création d’une connexion en continu via l’API ou [here](https://docs.adobe.com/content/help/en/experience-platform/ingestion/tutorials/create-streaming-connection-ui.html) pour obtenir des instructions sur la création d’une connexion en continu via l’interface utilisateur.

```json
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample name",
     "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
     "description": "Sample description",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Sample connection",
             "dataType": "xdm",
             "name": "Sample connection"
         }
     }
 }
```

Réponse :

```json
 {
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

Veillez à enregistrer l’identifiant fourni dans la réponse ci-dessus pour les futurs appels d’ingestion par flux (la collection Postman l’enregistrera pour vous dans la variable d’environnement CONNECTION_ID).

## Diffusion des données de profil vers AEP

Pour cette section, utilisez les dossiers d’appels Postman : 3: Import en temps réel, 3a: Import en temps réel pour les données PROFILE.

Les requêtes JSON détaillées avec des réponses pour la diffusion en continu des données de profil sont documentées. [here](https://docs.adobe.com/content/help/en/experience-platform/ingestion/tutorials/streaming-record-data.html).

Étapes :

1. Création d’un schéma XDM Individual Profile
1. Définition du descripteur d’identité de Principal pour XDM Individual Profile (clé primaire)
1. Création d’un jeu de données pour les enregistrements XDM Individual Profile
1. Appel des API d’ingestion en flux continu pour créer un enregistrement XDM Individual Profile
1. Récupération du profil nouvellement créé

## Diffusion en continu des événements d’expérience vers AEP

Pour cette section, utilisez les dossiers d’appels Postman : 3 : import en temps réel, 3b : import en temps réel pour les données PROFILE.

Les requêtes JSON détaillées avec des réponses pour les données d’expérience de diffusion en continu sont documentées. [here](https://docs.adobe.com/content/help/en/experience-platform/ingestion/tutorials/streaming-time-series-data.html).

Étapes :

1. Création d’un schéma ExperienceEvent XDM
1. Définition du descripteur d’identité de Principal pour XDM ExperienceEvent (clé primaire)
1. Création d’un jeu de données pour XDM ExperienceEvents
1. Appel des API d’ingestion en flux continu pour créer un événement XDM ExperienceEvent
1. Récupération de l’événement nouvellement créé

## Utiliser des balises Experience Platform pour diffuser sur AEP

L&#39;Adobe [!DNL Experience Platform] L’extension Launch permet d’accéder en continu à AEP via Launch. Pour en savoir plus, voir [ce guide](https://docs.adobe.com/content/help/fr-FR/launch/using/extensions-ref/adobe-extension/aep-extension/overview.html).

## Articles de référence

* [API Data Ingestion](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#/acpdr/swagger-specs)
* [Présentation de l’ingestion par flux](https://docs.adobe.com/content/help/fr-FR/experience-platform/ingestion/home.html#!api-specification/markdown/narrative/technical_overview/streaming_ingest/streaming_ingest_overview.md)
* [Guide du développeur de l’ingestion en flux continu](https://www.adobe.io/apis/experienceplatform/home/data-ingestion/data-ingestion-services.html#!api-specification/markdown/narrative/technical_overview/streaming_ingest/getting_started_with_platform_streaming_ingestion.md)
* [Utilisation de l’extension Launch AEP](https://docs.adobe.com/content/help/fr-FR/launch/using/extensions-ref/adobe-extension/aep-extension/overview.html)
