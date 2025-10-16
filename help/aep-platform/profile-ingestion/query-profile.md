---
title: Accès au profil unifié
description: Utilisez les API pour accéder au profil unifié.
exl-id: c9d2fa2d-9ffe-4e66-996f-ad930bee22c6
source-git-commit: 0690a52c3be0981a626e49729e51cb1729816c87
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 8%

---

# Accéder au profil unifié à l’aide de l’API Profile

L’[!DNL Experience Platform] Adobe peut accéder au profil client en temps réel. L’API [[!DNL Experience Platform] Real-time Customer Profile](https://adobe.ly/2TtDHWr) a été conçue pour interagir avec celui-ci. Voir ce [tutoriel](https://docs.adobe.com/content/help/fr-FR/experience-platform/profile/api/getting-started.html) pour savoir comment accéder aux données du profil client en temps réel à l’aide de l’API Profile.

Cet article fera essentiellement référence au tutoriel ci-dessus.

La collection [Postman](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman) est référencée tout au long de l’article à l’aide des appels associés par numéro. Pour plus d’informations sur l’installation et l’utilisation de la collection Postman, consultez la page Github [README](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/README.md). Il existe également des exemples de jeux de données de données [fidélité](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20events.json) et [profil](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20profiles.json).

Pour cette section, utilisez le dossier Postman 5 : Recherche de profil, 5a : Données de profil de recherche en temps réel OU 5b : Données d’ÉVÉNEMENT de recherche en temps réel.

## Utilisation de l’API

Les sections suivantes vous aident à vous authentifier auprès d’Experience Platform. Découvrez le chemin d’accès à l’API, les informations d’en-tête, etc.

### S’authentifier auprès de [!DNL Platform]

Voir [ce](https://docs.adobe.com/content/help/fr-FR/experience-platform/tutorials/authentication.html) tutoriel sur l’authentification avant d’effectuer l’un des appels ci-dessous.

### Chemin d’accès à l’API

L’URL de la passerelle de plateforme nécessaire à l’API de profil client en temps réel est la suivante : `https://platform.adobe.io/`

Le chemin d’accès de base de l’API est : `/data/core/ups/access/entities`.

Voici un exemple de chemin complet : `https://platform.adobe.io/data/core/ups/access/entities`

### Informations sur l’en-tête

L’en-tête doit inclure :

* Autorisation
* x-gw-ims-org-id : à obtenir via console.adobe.io
* x-api-key - à obtenir via console.adobe.io
* x-sandbox-name : obtenu à partir d’Adobe Integration Manager
* Content-Type: application/json

Vous trouverez plus d’informations sur l’en-tête dans le [tutoriel](https://adobe.ly/2PTHuKv).

## Accès aux profils clients en temps réel à l’aide d’identités

L’API Profile permet d’accéder aux profils à l’aide d’identités via une requête GET. Les sections ci-dessous suivront ce [guide](https://docs.adobe.com/content/help/fr-FR/experience-platform/profile/api/entities.html).

### Accès aux données de profil à l’aide de l’identité

L’API donne accès aux informations de profil à l’aide de l’identité. Pour ce faire, envoyez une requête GET à /access/entities en indiquant l’ID de l’entité comme l’un des paramètres et l’espace de noms de l’ID d’entité. REMARQUE : gardez à l’esprit que toute requête qui renvoie 50 enregistrements ne fournit qu’un statut HTTP 422 et un message indiquant « trop d’identités associées » et que la recherche doit être réduite avec davantage de paramètres.

Requête :

La requête suivante récupère l’adresse e-mail et le nom d’un client à l’aide d’une identité :

```
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email&fields=identities,person.name,workEmail' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Réponse :

```
{
    "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA": {
        "entityId": "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA",
        "sources": [
            "1000000000"
        ],
        "entity": {
            "identities": [
                {
                    "id": "89149270342662559642753730269986316601",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "janedoe@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "janesmith@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316604",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "58832431024964181144308914570411162539",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316602",
                    "namespace": {
                        "code": "ecid"
                    },
                    "primary": true
                }
            ],
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                }
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "label": "Jane Doe",
                "type": "work",
                "status": "active"
            }
        },
        "lastModifiedAt": "2018-08-28T20:57:24Z"
    }
}
```

### Accès aux profils par liste d’identités

L’API donne accès aux profils à l’aide d’une liste d’identités en utilisant une requête POST au point d’entrée /access/entities et en fournissant les identités dans la payload. Ces identités se composent d’une valeur d’identifiant (entityId) et d’un espace de noms d’identité (entityIdNS).

Requête :
La requête suivante récupère les noms et adresses e-mail de plusieurs clients par une liste d’identités :

```
curl -X POST \
  https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "schema":{
        "name":"_xdm.context.profile"
    },
    "fields":["identities","person.name","workEmail"],
    "identities":[
        {
            "entityId":"89149270342662559642753730269986316601",
            "entityIdNS":{
                "code":"ECID"
            }
        },
        {
            "entityId":"89149270342662559642753730269986316900",
            "entityIdNS":{
                "code":"ECID"
            }
        },
        {
            "entityId":"89149270342662559642753730269986316602",
            "entityIdNS":{
                "code":"ECID"
            }
        }
    ]
}'
```

Réponse :
Une réponse réussie renvoie les champs demandés des entités spécifiées dans le corps de la requête.

```
{
    "A29cgveD5y64ezlhxjUXNzcm": {
        "entityId": "A29cgveD5y64ezlhxjUXNzcm",
        "sources": [
            "1000000000"
        ],
        "entity": {
            "identities": [
                {
                    "id": "89149270342662559642753730269986316601",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "janedoe@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "05DD23564EC4607F0A490D44",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316603",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "janesmith@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316604",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316700",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316701",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "58832431024964181144308914570411162539",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316602",
                    "namespace": {
                        "code": "ecid"
                    },
                    "primary": true
                }
            ],
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                }
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "label": "Jane Doe",
                "type": "work",
                "status": "active"
            }
        },
        "lastModifiedAt": "2018-08-28T20:57:24Z"
    },
    "A29cgveD5y64e2RixjUXNzcm": {
        "entityId": "A29cgveD5y64e2RixjUXNzcm",
        "sources": [
            ""
        ],
        "entity": {},
        "lastModifiedAt": "1970-01-01T00:00:00Z"
    },
    "A29cgveD5y64ezphxjUXNzcm": {
        "entityId": "A29cgveD5y64ezphxjUXNzcm",
        "sources": [
            "1000000000"
        ],
        "entity": {
            "identities": [
                {
                    "id": "89149270342662559642753730269986316602",
                    "namespace": {
                        "code": "ecid"
                    },
                    "primary": true
                },
                {
                    "id": "janedoe@example.com",
                    "namespace": {
                        "code": "email"
                    }
                }
            ],
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                }
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "label": "Jane Doe",
                "type": "work",
                "status": "active"
            }
        },
        "lastModifiedAt": "2018-08-27T23:25:52Z"
    }
}
```

## Événements de série temporelle

Les partenaires peuvent accéder aux événements de série temporelle en fonction de l’identité de l’entité de profil associée en envoyant une requête GET au point d’entrée /access/entities.

### Accès aux événements de série temporelle d’un profil par identité

Les événements de série temporelle sont accessibles par l’identité de l’entité de profil associée en envoyant une requête GET au point d’entrée /access/entities. Cette identité se compose d’une valeur d’identifiant (entityId) et d’un espace de noms d’identité (entityIdNS).

Requête :
La requête suivante recherche une entité de profil par ID et récupère les valeurs des propriétés endUserIDs, web et channel **pour tous** les événements de série temporelle associés à l’entité.

```
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Réponse :

Une réponse réussie renvoie une liste paginée d’événements de série temporelle et de champs associés spécifiés dans les paramètres de requête.

```
{
    "_page": {
        "orderby": "timestamp",
        "start": "c8d11988-6b56-4571-a123-b6ce74236036",
        "count": 1,
        "next": "c8d11988-6b56-4571-a123-b6ce74236037"
    },
    "children": [
        {
            "relatedEntityId": "A29cgveD5y64e2RixjUXNzcm",
            "entityId": "c8d11988-6b56-4571-a123-b6ce74236036",
            "timestamp": 1531260476000,
            "entity": {
                "endUserIDs": {
                    "_experience": {
                        "ecid": {
                            "id": "89149270342662559642753730269986316900",
                            "namespace": {
                                "code": "ecid"
                            }
                        }
                    }
                },
                "channel": {
                    "_type": "web"
                },
                "web": {
                    "webPageDetails": {
                        "name": "Fernie Snow",
                        "pageViews": {
                            "value": 1
                        }
                    }
                }
            },
            "lastModifiedAt": "2018-08-21T06:49:02Z"
        }
    ],
    "_links": {
        "next": {
            "href": "/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1"
        }
    }
}
```

### Pagination des événements de série temporelle pour un profil

Les résultats sont paginés lors de la récupération des événements de série temporelle. S’il existe d’autres pages de résultats, le paramètre &lowbar;page.next de la réponse contiendra un identifiant. En outre, le paramètre &lowbar;links.next.href de la réponse fournit une URI de requête pour récupérer la page suivante.

Requête :

La requête suivante récupère la page de résultats suivante en utilisant l’URI _links.next.href comme chemin d’accès à la requête.

```
curl -X GET \

  'https://platform.adobe.io/data/core/ups/access/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Réponse :

Une réponse réussie renvoie la page de résultats suivante. Cet exemple illustre une réponse où il n’y a pas de pages de résultats suivantes, comme indiqué par les valeurs de chaîne vides &lowbar;page.next et &lowbar;links.next.href.

```
{
    "_page": {
        "orderby": "timestamp",
        "start": "c8d11988-6b56-4571-a123-b6ce74236037",
        "count": 1,
        "next": ""
    },
    "children": [
        {
            "relatedEntityId": "A29cgveD5y64e2RixjUXNzcm",
            "entityId": "c8d11988-6b56-4571-a123-b6ce74236037",
            "timestamp": 1531260477000,
            "entity": {
                "endUserIDs": {
                    "_experience": {
                        "ecid": {
                            "id": "89149270342662559642753730269986316900",
                            "namespace": {
                                "code": "ecid"
                            }
                        }
                    }
                },
                "channel": {
                    "_type": "web"
                },
                "web": {
                    "webPageDetails": {
                        "name": "Fernie Snow",
                        "pageViews": {
                            "value": 1
                        }
                    }
                }
            },
            "lastModifiedAt": "2018-08-21T06:50:01Z"
        }
    ],
    "_links": {
        "next": {
            "href": ""
        }
    }
}
```

## Articles de référence

* [API Real-time Customer Profile](https://adobe.ly/2TtDHWr)
* [Accédez aux données du profil client en temps réel à l’aide du tutoriel de l’API Profile](https://docs.adobe.com/content/help/fr-FR/experience-platform/profile/api/getting-started.html)
* [[!DNL Experience Platform]  Guide d’authentification &#x200B;](https://docs.adobe.com/content/help/fr-FR/experience-platform/tutorials/authentication.html)
