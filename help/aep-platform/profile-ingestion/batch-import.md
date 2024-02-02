---
title: Importation de données par lots dans AEP
description: Découvrez comment importer des fichiers de lot dans Experience Platform
exl-id: 50576b67-b3ba-498e-86f6-7e1986b76985
source-git-commit: fe7519c35fb9155ce54cad85941c887f15881a38
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 11%

---

# Importation de données par lots dans AEP

AEP peut ingérer des fichiers de lot qui contiennent des données de profil d’un fichier plat (parquet, par exemple) ou des données conformes à un schéma connu dans la variable [!UICONTROL Experience Data Model] Registre (XDM).

AEP peut ingérer des données à l’aide de fichiers de lot. Les formats suivants sont acceptés : JSON, Parquet et CSV.

Cet article traite des sujets suivants :

* Conditions préalables à l’ingestion par lots
* Bonnes pratiques et limites de l’ingestion par lots
* Création d’un lot
* Comment terminer un lot
* Vérification de l’état d’un lot

La variable [Collection Postman](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman) est référencé tout au long de l’article à l’aide des appels associés par numéro. Pour plus d’informations sur l’installation et l’utilisation de la collection Postman, voir Github . [LISEZMOI](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/README.md) page. Il existe également des exemples de jeux de données de [loyalty](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20events.json) et [profile](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20profiles.json) data.

Pour tous les appels de ce tutoriel, utilisez les dossiers d’appels Postman : 4 : importation par lots, 4a : importation par lots pour les données de PROFIL OU 4b : importation par lots pour les données d’ÉVÉNEMENT.

## Conditions préalables à l’ingestion par lots

* Définissez un schéma et créez un jeu de données.
* Les données doivent être au format JSON, Parquet ou CSV.
* [Authentification à la plateforme](https://docs.adobe.com/content/help/fr-FR/experience-platform/tutorials/home.html#!api-specification/markdown/narrative/tutorials/authenticate_to_acp_tutorial/authenticate_to_acp_tutorial.md).
* Rassemblez les valeurs des en-têtes requis à partir du tutoriel sur l’authentification lié ci-dessus.

## Bonnes pratiques et limites de l’ingestion par lots

* Taille maximale du lot : 100 Go
* Nombre maximal de fichiers par lot : 1 500
* Si un fichier dépasse 512 Mo, il doit être divisé en petits blocs. Vous trouverez plus de détails dans la section [guide de développement](https://www.adobe.io/apis/experienceplatform/home/data-ingestion/data-ingestion-services.html#!api-specification/markdown/narrative/technical_overview/ingest_architectural_overview/batch_data_ingestion_developer_guide.md)
* Nombre maximal de propriétés ou de champs par ligne : 10 000
* Nombre maximal de lots par minute, par utilisateur : 138

## Création d’un lot

Dans ce tutoriel, nous utiliserons JSON comme format. Vous trouverez d’autres exemples de format dans la section [guide de développement](https://www.adobe.io/apis/experienceplatform/home/data-ingestion/data-ingestion-services.html#!api-specification/markdown/narrative/technical_overview/ingest_architectural_overview/batch_data_ingestion_developer_guide.md)
Créez un lot au format d’entrée JSON (veillez à inclure un identifiant de jeu de données et à ce que vos données soient conformes au schéma XDM lié au jeu de données) :

```json
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json"
           }
      }'
```

Réponse :

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{IMS_ORG}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

## Chargement de fichiers

Les fichiers peuvent désormais être chargés dans le nouveau lot (à l’aide de l’identifiant de lot de la réponse ci-dessus).

```json
curl -X PUT "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json" \
  -H "content-type: application/octet-stream" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}" \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

>[!NOTE]
>
>L’API ne prend en charge que le chargement en une seule partie, ce qui signifie que chaque fichier/micro-lot devra être chargé avec des appels individuels. Assurez-vous que le type de contenu est bien application/octet-stream.

Réponse :

```
200 OK
```

## Fin d’un lot

Une fois tous les fichiers chargés, cet appel signale que le lot est prêt pour la promotion :

```json
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

Réponse :

```
200 OK
```

## Vérification de l’état d’un lot

L’état du lot peut être vérifié dans l’interface utilisateur ou via l’API (voir appel ci-dessous). Pour archiver l’interface utilisateur, accédez au jeu de données pour afficher l’état.

Les différents états d’ingestion par lots sont disponibles. [here](https://adobe.ly/2TMMCmj).


```json
curl GET "https://platform.adobe.io/data/foundation/catalog/batch/{BATCH_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

Réponse :

```json
{
    "{BATCH_ID}": {
        "imsOrg": "{IMS_ORG}",
        "created": 1494349962314,
        "createdClient": "MCDPCatalogService",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "updated": 1494349963467,
        "externalId": "{EXTERNAL_ID}",
        "status": "success",
        "errors": [
            {
                "code": "err-1494349963436"
            }
        ],
        "version": "1.0.3",
        "availableDates": {
            "startDate": 1337,
            "endDate": 4000
        },
        "relatedObjects": [
            {
                "type": "batch",
                "id": "foo_batch"
            },
            {
                "type": "connection",
                "id": "foo_connection"
            },
            {
                "type": "connector",
                "id": "foo_connector"
            },
            {
                "type": "dataSet",
                "id": "foo_dataSet"
            },
            {
                "type": "dataSetView",
                "id": "foo_dataSetView"
            },
            {
                "type": "dataSetFile",
                "id": "foo_dataSetFile"
            },
            {
                "type": "expressionBlock",
                "id": "foo_expressionBlock"
            },
            {
                "type": "service",
                "id": "foo_service"
            },
            {
                "type": "serviceDefinition",
                "id": "foo_serviceDefinition"
            }
        ],
        "metrics": {
            "foo": 1337
        },
        "tags": {
            "foo_bar": [
                "stuff"
            ],
            "bar_foo": [
                "woo",
                "baz"
            ],
            "foo/bar/foo-bar": [
                "weehaw",
                "wee:haw"
            ]
        },
        "inputFormat": {
            "format": "parquet",
            "delimiter": ".",
            "quote": "`",
            "escape": "\\",
            "nullMarker": "",
            "header": "true",
            "charset": "UTF-8"
        }
    }
}
```

## Articles de référence

* [API Data Ingestion](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#/acpdr/swagger-specs)
* [Présentation de l’ingestion par lots](https://docs.adobe.com/content/help/fr-FR/experience-platform/ingestion/home.html#!api-specification/markdown/narrative/technical_overview/ingest_architectural_overview/ingest_architectural_overview.md)
* [Guide du développeur de l’ingestion par lots](https://www.adobe.io/apis/experienceplatform/home/data-ingestion/data-ingestion-services.html#!api-specification/markdown/narrative/technical_overview/ingest_architectural_overview/batch_data_ingestion_developer_guide.md)
* [Guide de dépannage de l’ingestion par lots](https://www.adobe.io/apis/experienceplatform/home/data-ingestion/data-ingestion-services.html#!api-specification/markdown/narrative/technical_overview/ingest_architectural_overview/batch_data_ingestion_troubleshooting_guide.md)
* [Collecte Postman d’ingestion de données](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/experience-platform/Data%20Ingestion%20API.postman_collection.json)
* [Tutoriel sur l’authentification](https://docs.adobe.com/content/help/fr-FR/experience-platform/tutorials/home.html#!api-specification/markdown/narrative/tutorials/authenticate_to_acp_tutorial/authenticate_to_acp_tutorial.md)
