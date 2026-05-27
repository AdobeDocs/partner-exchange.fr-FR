---
title: Import en temps réel
description: Découvrez comment importer des données dans AEP en temps réel.
exl-id: 0b6215a9-1160-49ae-8aa5-302b47357200
TQID: https://experienceleague.adobe.com/GvWcwNPjQdmdKSUkwvJ2EpoCKJHGvf5c1Kn4dwWRVi8
product_v2:
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
source-git-commit: 6698ae880d1ad13a9387cb1ba66b9ba152d1d407
workflow-type: tm+mt
source-wordcount: 642
ht-degree: 9%

---

# Diffusion de données vers AEP

Adobe [!DNL Experience Platform] permet la diffusion en continu et la disponibilité d’événements de profil et d’expérience en temps quasi réel. Toutes les données envoyées à AEP par le biais de la diffusion en continu sont conservées dans le lac de données. Les données peuvent être diffusées en continu vers des jeux de données existants ou vers des jeux de données entièrement nouveaux via des API ou à l’aide d’Adobe Launch.

Cet article couvre les sujets suivants :

* Diffusion en continu vers XDM Individual Profile
* Diffusion en continu vers XDM ExperienceEvent
* Utilisation d’AEP l’extension Launch pour diffuser

La collection [&#128279;](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman) est référencée tout au long de l’article à l’aide des appels associés par numéro. Pour plus d’informations sur l’installation et l’utilisation de la collection Postman, consultez la page Github [README](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/README.md). Il existe également des exemples de jeux de données de données [fidélité](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20events.json) et [profil](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20profiles.json).

## Conditions préalables

* [S’authentifier sur la plateforme](https://docs.adobe.com/content/help/fr-FR/experience-platform/tutorials/authentication.html).
* Rassemblez les valeurs des en-têtes requis à partir du tutoriel sur l’authentification ci-dessus.

## Création d’une connexion en continu

Pour diffuser vers AEP, vous devez d’abord créer une connexion en continu. Les connexions en continu contiennent des attributs tels que la source des données en continu et si vous envoyez ou non des enregistrements appartenant aux schémas [!DNL Experience Data Model] (XDM). Après avoir créé une connexion en continu, vous recevez une URL unique que vous utilisez pour diffuser des données dans AEP.

Accédez [ici](https://docs.adobe.com/content/help/en/experience-platform/ingestion/tutorials/create-streaming-connection.html) pour obtenir des instructions sur la création d’une connexion en continu via l’API ou [ici](https://docs.adobe.com/content/help/en/experience-platform/ingestion/tutorials/create-streaming-connection-ui.html) pour obtenir des instructions sur la création d’une connexion en continu via l’interface utilisateur.

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

Veillez à enregistrer l’identifiant fourni dans la réponse ci-dessus pour les appels d’ingestion en flux continu futurs (la collection Postman l’enregistrera pour vous dans la variable d’environnement CONNECTION_ID).

## Diffusion des données de profil vers AEP

Pour cette section, utilisez les dossiers d’appels Postman : 3 : importation en temps réel, 3a : importation en temps réel des données PROFILE.

Les requêtes JSON détaillées avec des réponses pour les données de profil de diffusion en continu sont documentées [ici](https://docs.adobe.com/content/help/en/experience-platform/ingestion/tutorials/streaming-record-data.html).

Étapes :

1. Création d’un schéma de profil individuel XDM
1. Définir le descripteur d’identité de Principal pour XDM Individual Profile (clé primaire)
1. Créer un jeu de données pour les enregistrements de profils individuels XDM
1. Appelez les API d’ingestion en flux continu pour créer un enregistrement de profil individuel XDM
1. Récupérer le profil nouvellement créé

## Diffusion d’événements d’expérience vers AEP

Pour cette section, utilisez les dossiers d’appels Postman : 3 : importation en temps réel, 3b : importation en temps réel des données PROFILE.

Les requêtes JSON détaillées avec des réponses pour les données d’expérience de diffusion sont documentées [ici](https://docs.adobe.com/content/help/en/experience-platform/ingestion/tutorials/streaming-time-series-data.html).

Étapes :

1. Création d’un schéma XDM ExperienceEvent
1. Définissez le descripteur d’identité de Principal pour XDM ExperienceEvent (clé primaire)
1. Créer un jeu de données pour XDM ExperienceEvents
1. Appelez les API d’ingestion en flux continu pour créer un événement d’expérience XDM
1. Récupérer l’événement nouvellement créé

## Utiliser les balises Experience Platform pour diffuser vers AEP

L’extension Adobe [!DNL Experience Platform] Launch permet d’accéder à AEP en flux continu via Launch. Pour en savoir plus, consultez [ce guide](https://docs.adobe.com/content/help/fr-FR/launch/using/extensions-ref/adobe-extension/aep-extension/overview.html).

## Articles de référence

* [API Data Ingestion](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#/acpdr/swagger-specs)
* [Vue d’ensemble de l’ingestion en flux continu](https://www.adobe.io/apis/experienceplatform/home/data-ingestion/data-ingestion-services.html#!api-specification/markdown/narrative/technical_overview/streaming_ingest/streaming_ingest_overview.md)
* [Guide de développement de l’ingestion en flux continu](https://www.adobe.io/apis/experienceplatform/home/data-ingestion/data-ingestion-services.html#!api-specification/markdown/narrative/technical_overview/streaming_ingest/getting_started_with_platform_streaming_ingestion.md)
* [Utilisation de l’extension AEP Launch](https://docs.adobe.com/content/help/fr-FR/launch/using/extensions-ref/adobe-extension/aep-extension/overview.html)
