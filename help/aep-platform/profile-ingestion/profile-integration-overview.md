---
title: Aperçu du guide d’intégration de l’ingestion et de l’accès au profil [!DNL Platform]
description: Découvrez l’intégration pour l [!DNL Experience Platform] ingestion et l’accès aux profils.
exl-id: a593511c-dd4c-4437-af73-f44d795cacb8
TQID: https://experienceleague.adobe.com/whnqurJyM4QXl5ikRvez7hpKWRDuU4onzROsUk-WeSI
product_v2: id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
topic_v2: id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 6698ae880d1ad13a9387cb1ba66b9ba152d1d407
workflow-type: tm+mt
source-wordcount: 492
ht-degree: 3%

---

# Guide d’intégration : ingestion et accès aux profils [!DNL Experience Platform]

Les partenaires doivent utiliser ce guide d’intégration pour les aider à créer des fonctionnalités d’entrée et de sortie avec Adobe [!DNL Experience Platform] (AEP). Il existe des API pour l’ingestion par lots, l’ingestion par flux et l’accès au profil unifié (sortie).

Pour faciliter le développement, une collection [](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman) a été créée par l’équipe Adobe Exchange. Cette collection Postman est référencée tout au long du guide d’intégration.

Pour plus d’informations sur l’installation et l’utilisation de la collection Postman, consultez la page Github [README](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/README.md). Il existe également des exemples de jeux de données de données [fidélité](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20events.json) et [profil](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20profiles.json).

## Exemple de cas d’utilisation d’intégration : système de réponse vocale interactive

Pour les intégrateurs , les API [!DNL Experience Platform] fournissent toutes les fonctionnalités de la plateforme qui sont proposées dans l’interface utilisateur, mais offrent désormais la possibilité de créer des workflows client et des flux de données automatisés. En tant qu’intégrateur, vous vérifiez régulièrement le statut des jeux de données, configurez de nouvelles procédures d’ingestion de données et intégrez votre propre solution d’activation des audiences au profil unifié.

Explorez le monde des systèmes de réponse vocale interactive (IVR) et des logiciels de gestion de centre d&#39;appels. Le fournisseur peut utiliser les API [!DNL Experience Platform] pour ingérer des informations historiques sur l’activité du centre d’appel du client dans le lac de données d’Experience. Si les données sont ingérées dans le schéma de `ExperienceEvent` XDM (un schéma qui exprime les interactions des clients), ces interactions peuvent être ingérées sans friction directement dans le service de profil unifié. Dans ce cas, le `callerId` est utilisé comme identifiant du client. Le service d’identités se charge de la résolution d’identité et aide le service de profil unifié à ajouter au profil du client tous les points de données provenant d’interactions récentes avec le centre d’appels.

La prochaine fois qu’un client appelle le centre d’appels, l’IVR lui répondra d’abord. Pour personnaliser le message et diffuser une offre adaptée à l&#39;appelant, le système IVR doit mieux comprendre l&#39;appelant. C’est là que l’intégration de l’API avec le profil unifié entre en jeu. Le serveur principal IVR peut contacter le service de profil unifié pour une recherche de point. Ensuite, consultez les attributs de profil qui s’appliquent uniquement aux interactions du centre d’appel ou le profil client complet, qui comporte également des attributs pour les interactions sur d’autres points de contact. En associant des données provenant de plusieurs sources de données, en utilisant la résolution d’identité et le profil unifié, le centre d’appel et le fournisseur de RVI peuvent offrir une expérience client personnalisée, prise en charge par Adobe [!DNL Experience Platform]. »

## Ressources générales

* AEP [Documentation du produit](https://docs.adobe.com/content/help/fr-FR/experience-platform/landing/documentation/overview.html).
* AEP [Extensibilité](https://www.adobe.com/insights/experience-platform-api-extensibility.html).

## Questions ou commentaires ?

Envoyez toutes vos questions et vos commentaires via le [canal assistance](https://adobeexchangeec.zendesk.com/hc/fr-fr/requests/new)
