---
title: "[!DNL Platform] Présentation du guide d’intégration Profile Ingestion et Access"
description: En savoir plus sur l’intégration pour [!DNL Experience Platform] l’ingestion et l’accès des profils.
exl-id: a593511c-dd4c-4437-af73-f44d795cacb8
source-git-commit: fe7519c35fb9155ce54cad85941c887f15881a38
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 0%

---

# Guide d’intégration : [!DNL Experience Platform] ingestion et accès des profils

Les partenaires doivent utiliser ce guide d’intégration pour les aider à créer des fonctionnalités d’entrée et de sortie avec l’Adobe. [!DNL Experience Platform] (AEP) Il existe des API pour l’ingestion par lots, l’ingestion par flux et l’accès au profil unifié (sortie).

Pour faciliter le développement, une [Collection Postman](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman) a été créé par l’équipe Adobe Exchange. Cette collection Postman est référencée dans le guide d’intégration.

Pour plus d’informations sur l’installation et l’utilisation de la collection Postman, voir Github . [LISEZMOI](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/README.md) page. Il existe également des exemples de jeux de données de [loyalty](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20events.json) et [profile](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20profiles.json) data.

## Exemple de cas d’utilisation d’intégration : système de réponse vocale interactive

Pour les intégrateurs, la variable [!DNL Experience Platform] Les API offrent toutes les fonctionnalités de la plateforme qui sont proposées dans l’interface utilisateur, mais qui permettent désormais de créer des workflows client et des flux de données automatisés. En tant qu’intégrateur, vous vérifiez régulièrement l’état des jeux de données, configurez de nouvelles procédures d’ingestion de données et intégrez votre propre solution d’activation d’audience avec le profil unifié.

Prenons l’exemple des systèmes de réponse vocale interactive (IVR) et des logiciels de gestion du centre d’appels. Le fournisseur peut utiliser la variable [!DNL Experience Platform] API permettant d’ingérer des informations historiques sur l’activité du centre d’appels du client dans le lac de données d’expérience. Si les données sont ingérées dans XDM `ExperienceEvent` Schéma (schéma qui exprime les interactions client), ces interactions peuvent être ingérées sans friction directement dans le service de profil unifié. Dans ce cas, la variable `callerId` est utilisé comme identifiant du client. Le service Identity se charge de la résolution des identités et aide le service de profil unifié à ajouter au profil du client tous les points de données provenant d’interactions récentes avec le centre d’appels.

La prochaine fois qu’un client fera appel au centre d’appels, il y aura une première réponse de la part de la FIV. Pour personnaliser le message et diffuser une offre adaptée à l’appelant, le système IVR doit en savoir plus sur l’appelant. C’est là que l’intégration de l’API au profil unifié entre en jeu. Le serveur principal IVR peut contacter le service de profil unifié pour une recherche de point. Consultez ensuite les attributs de profil qui s’appliquent uniquement aux interactions du centre d’appel ou au profil client complet, qui comporte également des attributs pour les interactions sur d’autres points de contact. En combinant des données provenant de plusieurs sources de données, à l’aide de la résolution des identités et du profil unifié, le centre d’appels et le fournisseur de téléphonie mobile peuvent offrir une expérience client personnalisée, prise en charge par Adobe. [!DNL Experience Platform].&quot;

## Ressources générales

* AEP [Documentation du produit](https://docs.adobe.com/content/help/fr-FR/experience-platform/landing/documentation/overview.html).
* AEP [Extensibilité](https://www.adobe.com/insights/experience-platform-api-extensibility.html).

## Questions ou commentaires ?

Veuillez envoyer toutes les questions et commentaires via [canal de prise en charge](https://adobeexchangeec.zendesk.com/hc/fr-fr/requests/new)
