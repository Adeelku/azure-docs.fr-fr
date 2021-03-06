---
title: Interopérabilité des réunions Teams
titleSuffix: An Azure Communication Services concept document
description: Participer aux réunions Teams
author: chpalm
manager: chpalm
services: azure-communication-services
ms.author: chpalm
ms.date: 10/10/2020
ms.topic: overview
ms.service: azure-communication-services
ms.openlocfilehash: a7e2240e3f74f82186827ec82bb1aa39a5b93f6c
ms.sourcegitcommit: 7dacbf3b9ae0652931762bd5c8192a1a3989e701
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/16/2020
ms.locfileid: "92123832"
---
# <a name="teams-interoperability"></a>Interopérabilité de Teams

[!INCLUDE [Private Preview Notice](../../includes/private-preview-include.md)]

Azure Communication Services peut être utilisé pour créer des expériences de réunion personnalisées qui interagissent avec Microsoft Teams. Les utilisateurs de vos solutions Communication Services peuvent interagir avec les participants Teams en utilisant l’audio, la vidéo et le partage d’écran.

Cette interopérabilité vous permet de créer des applications Azure personnalisées qui connectent les utilisateurs aux réunions Teams. Les utilisateurs de vos applications personnalisées n’ont pas besoin d’avoir des identités Azure Active Directory ou des licences Teams pour bénéficier de cette fonctionnalité. C’est idéal pour réunir de façon transparente des employés (qui peuvent être familiarisés avec Teams) et des utilisateurs externes (par le biais d’une expérience d’application personnalisée). Cela vous permet de créer des expériences similaires à celles-ci :

1. Les employés utilisent Teams pour planifier une réunion
2. Votre application Communication Services personnalisée utilise les API Microsoft Graph pour accéder aux détails de la réunion
3. Les détails de la réunion sont partagés avec des utilisateurs externes par le biais de votre application personnalisée
4. Les utilisateurs externes utilisent votre application personnalisée pour rejoindre la réunion Teams (via la bibliothèque de client Communication Services Calling).

L’architecture générale de ce cas d’usage se présente comme suit : 

![Architecture de l’interopérabilité de Teams](..//media/call-flows/teams-interop.png)

Tandis que certaines fonctionnalités de réunion de Teams telles que la main levée, le mode Ensemble et les salles pour petit groupe sont uniquement disponibles pour les utilisateurs Teams, votre application personnalisée a accès aux principales fonctionnalités audio, vidéo et de partage d’écran de la réunion.

Quand un utilisateur Communication Services rejoint la réunion Teams, le nom complet fourni par le biais de la bibliothèque de client Calling est présenté aux utilisateurs Teams. Sinon, l’utilisateur Communication Services est traité comme un utilisateur anonyme dans Teams. Votre application personnalisée doit envisager l’authentification des utilisateurs et d’autres mesures de sécurité pour protéger les réunions Teams. Pensez à ce que cela implique en terme de sécurité si vous autorisez les utilisateurs anonymes à rejoindre des réunions et utilisez le [Guide sur la sécurité de Teams](https://docs.microsoft.com/microsoftteams/teams-security-guide#addressing-threats-to-teams-meetings) pour configurer les fonctionnalités disponibles pour les utilisateurs anonymes.

Les utilisateurs Communication Services peuvent rejoindre les réunions Teams planifiées tant que les participations anonymes sont autorisées dans les [paramètres de la réunion](https://docs.microsoft.com/microsoftteams/meeting-settings-in-teams).



## <a name="next-steps"></a>Étapes suivantes

> [!div class="nextstepaction"]
> [Joindre votre application d’appel à une réunion Teams](../../quickstarts/voice-video-calling/get-started-teams-interop.md)
