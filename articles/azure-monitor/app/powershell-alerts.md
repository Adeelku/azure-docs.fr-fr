---
title: Utilisation de PowerShell pour la configuration d’alertes dans Application Insights | Microsoft Docs
description: Automatisez la configuration d’Application Insights pour recevoir des e-mails retraçant les modifications des métriques.
ms.topic: conceptual
ms.date: 07/23/2016
ms.openlocfilehash: 74d477b6660c0f7ec2ee32b34169bb85886936e5
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2020
ms.locfileid: "87322463"
---
# <a name="use-powershell-to-set-alerts-in-application-insights"></a>Utilisation de PowerShell pour la configuration d’alertes dans Application Insights

[!INCLUDE [updated-for-az](../../../includes/updated-for-az.md)]

Vous pouvez automatiser la configuration des [alertes](../platform/alerts-log.md) dans [Application Insights](./app-insights-overview.md).

En outre, vous pouvez [définir des webhooks pour automatiser votre réponse à une alerte](../platform/alerts-webhooks.md).

> [!NOTE]
> Si vous souhaitez créer des alertes et des ressources en même temps, pensez à [utiliser un modèle Azure Resource Manager](powershell.md).

## <a name="one-time-setup"></a>Installation unique
Si vous n’avez pas utilisé précédemment PowerShell avec votre abonnement Azure :

Installez le module Azure Powershell sur l’ordinateur sur lequel vous souhaitez exécuter les scripts.

* Installez le programme [Microsoft Web Platform Installer (v5 ou version ultérieure)](https://www.microsoft.com/web/downloads/platform.aspx).
* Utilisez-le pour installer Microsoft Azure PowerShell.

## <a name="connect-to-azure"></a>Connexion à Azure
Démarrez Azure PowerShell et [connectez-vous à votre abonnement](/powershell/azure/):

```azurepowershell
Add-AzAccount
```


## <a name="get-alerts"></a>Obtention d’alertes

```azurepowershell
Get-AzAlertRule -ResourceGroup "Fabrikam" `
  [-Name "My rule"] `
  [-DetailedOutput]
```

## <a name="add-alert"></a>Ajout d’alerte

```azurepowershell
Add-AzMetricAlertRule -Name "{ALERT NAME}" `
  -Description "{TEXT}" `
  -ResourceGroup "{GROUP NAME}" `
  -TargetResourceId "/subscriptions/{SUBSCRIPTION ID}/resourcegroups/{GROUP NAME}/providers/microsoft.insights/components/{APP RESOURCE NAME}" `
  -MetricName "{METRIC NAME}" `
  -Operator GreaterThan `
  -Threshold {NUMBER}  `
  -WindowSize {HH:MM:SS} `
  [-SendEmailToServiceOwners] `
  [-CustomEmails "EMAIL1@X.COM","EMAIL2@Y.COM"] `
  -Location "East US" // must be East US at present `
  -RuleType Metric
```


## <a name="example-1"></a>Exemple 1
M’envoyer un message électronique si la réponse du serveur aux demandes HTTP, en moyenne calculée sur 5 minutes, est inférieure à 1 seconde. Ma ressource Application Insights est appelée IceCreamWebApp et se trouve dans le groupe de ressources Fabrikam. Je suis le propriétaire de l’abonnement Azure.

Le GUID est l’ID d’abonnement (et non la clé d’instrumentation de l’application).

```azurepowershell
Add-AzMetricAlertRule -Name "slow responses" `
  -ResourceGroup "Fabrikam" `
  -TargetResourceId "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/Fabrikam/providers/microsoft.insights/components/IceCreamWebApp" `
  -MetricName "request.duration" `
  -Operator GreaterThan `
  -Threshold 1 `
  -WindowSize 00:05:00 `
  -SendEmailToServiceOwners `
  -Location "East US" `
  -RuleType Metric
```

## <a name="example-2"></a>Exemple 2
J’ai une application dans laquelle j’utilise [TrackMetric()](./api-custom-events-metrics.md#trackmetric) pour signaler une métrique nommée « salesPerHour ». Envoyer un message électronique à mes collègues si la métrique « salesPerHour » est inférieure à 100, en moyenne calculée sur 24 heures.

```azurepowershell
Add-AzMetricAlertRule -Name "poor sales" `
  -Description "slow sales alert" `
  -ResourceGroup "Fabrikam" `
  -TargetResourceId "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/Fabrikam/providers/microsoft.insights/components/IceCreamWebApp" `
  -MetricName "salesPerHour" `
  -Operator LessThan `
  -Threshold 100 `
  -WindowSize 24:00:00 `
  -CustomEmails "satish@fabrikam.com","lei@fabrikam.com" `
  -Location "East US" `
  -RuleType Metric
```

La même règle peut être utilisée pour la métrique signalée à l’aide du [paramètre de mesure](./api-custom-events-metrics.md#properties) d’un autre appel de suivi tel que TrackEvent ou trackPageView.

## <a name="metric-names"></a>Noms de métrique
| Nom de métrique | Nom d’écran | Description |
| --- | --- | --- |
| `basicExceptionBrowser.count` |Exceptions du navigateur |Nombre d’exceptions non interceptées levées dans le navigateur. |
| `basicExceptionServer.count` |Exceptions de serveur |Nombre d’exceptions non gérées levées par l’application |
| `clientPerformance.clientProcess.value` |Temps de traitement du client |Temps écoulé entre la réception du dernier octet d’un document et le chargement du modèle DOM. Les demandes asynchrones peuvent encore être en cours de traitement. |
| `clientPerformance.networkConnection.value` |Temps de connexion au réseau pour le chargement de page |Temps pris par le navigateur pour se connecter au réseau. Peut être 0 en cas de mise en cache. |
| `clientPerformance.receiveRequest.value` |Temps de réception de réponse |Temps écoulé entre l’envoi d’une demande par le navigateur et le début de la réception d’une réponse. |
| `clientPerformance.sendRequest.value` |Temps d’envoi de demande |Temps pris par le navigateur pour envoyer la demande. |
| `clientPerformance.total.value` |Temps de chargement de la page de navigateur |Temps s’écoulant entre la demande de l’utilisateur et le chargement du DOM, des feuilles de style, des scripts et des images. |
| `performanceCounter.available_bytes.value` |Mémoire disponible |Mémoire physique immédiatement disponible pour un processus ou pour une utilisation du système. |
| `performanceCounter.io_data_bytes_per_sec.value` |Taux d’E/S du processus |Nombre total d’octets par seconde lus et écrits sur des fichiers, un réseau et des appareils. |
| `performanceCounter.number_of_exceps_thrown_per_sec.value` |Taux d’exceptions |Exceptions levées par seconde. |
| `performanceCounter.percentage_processor_time.value` |Processeur de processus |Temps écoulé en pourcentage pour l’ensemble des threads de traitement utilisés par le processeur pour exécuter le processus des applications. |
| `performanceCounter.percentage_processor_total.value` |Temps processeur |Temps en pourcentage que le processus a passé dans des threads actifs. |
| `performanceCounter.process_private_bytes.value` |Octets privés du processus |Mémoire allouée exclusivement aux processus de l’application analysée. |
| `performanceCounter.request_execution_time.value` |Durée d’exécution de la demande ASP.NET |Durée d’exécution de la demande la plus récente. |
| `performanceCounter.requests_in_application_queue.value` |Demandes ASP.NET en file d’attente d’exécution |Longueur de la file d'attente des demandes d'application. |
| `performanceCounter.requests_per_sec.value` |Taux de demandes ASP.NET |Taux par seconde de l'ensemble des demandes à l'application provenant d'ASP.NET. |
| `remoteDependencyFailed.durationMetric.count` |Défaillances de dépendance |Nombre d'appels de l'application serveur aux ressources externes ayant échoué. |
| `request.duration` |Temps de réponse du serveur |Temps écoulé entre la réception d'une requête HTTP et la fin de l'envoi de la réponse. |
| `request.rate` |Taux de demandes |Taux par seconde de l'ensemble des demandes à l'application. |
| `requestFailed.count` |Demandes ayant échoué |Nombre de requêtes HTTP qui ont abouti au code de réponse > = 400 |
| `view.count` |Affichages de page |Nombre de demandes d’utilisateur client pour une page web. Le trafic synthétique est filtré. |
| {nom de votre mesure personnalisée} |{nom de votre mesure} |Votre valeur métrique signalée par [TrackMetric](./api-custom-events-metrics.md#trackmetric) ou dans le [paramètre de mesures d’un appel de suivi](./api-custom-events-metrics.md#properties). |

Les mesures sont envoyées par différents modules de télémétrie :

| Groupe de mesures | Module du collecteur |
| --- | --- |
| basicExceptionBrowser,<br/>clientPerformance,<br/>vue |[JavaScript du navigateur](./javascript.md) |
| performanceCounter |[Performances](./configuration-with-applicationinsights-config.md) |
| remoteDependencyFailed |[Dépendance](./configuration-with-applicationinsights-config.md) |
| request,<br/>requestFailed |[Demande serveur](./configuration-with-applicationinsights-config.md) |

## <a name="webhooks"></a>webhooks
Vous pouvez [automatiser votre réponse à une alerte](../platform/alerts-webhooks.md). Azure appelle une adresse web de votre choix lorsqu’une alerte est déclenchée.

## <a name="see-also"></a>Voir aussi
* [Script de configuration d’Application Insights](./create-new-resource.md#creating-a-resource-automatically)
* [Créer des ressources Application Insights et de test Web  templates à partir de modèles (en anglais)](powershell.md)
* [Automatiser l’association de Diagnostics Microsoft Azure avec Application Insights](powershell-azure-diagnostics.md)
* [Automatiser votre réponse à une alerte](../platform/alerts-webhooks.md)

