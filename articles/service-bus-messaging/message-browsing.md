---
title: Azure Service Bus – Exploration des messages
description: Le parcours et aperçu des messages Service Bus permet à un client Azure Service Bus d’énumérer tous les messages qui résident dans une file d’attente ou un abonnement.
ms.topic: article
ms.date: 06/23/2020
ms.openlocfilehash: 6e50fc737f6c81c07854ff07d8cc64061306749b
ms.sourcegitcommit: d2222681e14700bdd65baef97de223fa91c22c55
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/07/2020
ms.locfileid: "91827441"
---
# <a name="message-browsing"></a>Parcours des messages

Le parcours des messages, ou « peeking », permet à un client Service Bus d’énumérer tous les messages résidant dans une file d’attente ou un abonnement, en général pour des besoins de diagnostic et de débogage.

Les opérations de peeking retournent tous les messages contenus dans le journal des messages de la file d’attente ou de l’abonnement, au lieu de retourner uniquement les messages disponibles pour acquisition immédiate avec `Receive()` ou la boucle `OnMessage()`. La propriété `State` de chaque message vous indique si le message est actif (prêt à être reçu), [différé](message-deferral.md) ou [planifié](message-sequencing.md).

Les messages consommés ou expirés sont nettoyés par un processus asynchrone de nettoyage de la mémoire (« garbage collection ») qui ne se produit pas toujours au moment même de leur expiration. Par conséquent, `Peek` peut retourner des messages qui ont déjà expiré et qui seront supprimés ou mis dans la file d’attente de lettres mortes au prochain appel d’une opération de réception sur la file d’attente ou l’abonnement.

C’est un point très important à prendre en compte lorsque vous tentez de récupérer des messages différés de la file d’attente. Un message dont l’instant [ExpiresAtUtc](/dotnet/api/microsoft.azure.servicebus.message.expiresatutc#Microsoft_Azure_ServiceBus_Message_ExpiresAtUtc) est passé n’est plus éligible pour la récupération normale par d’autres moyens, même quand il est retourné par Peek. Le retour de ces messages est délibéré, car Peek est un outil de diagnostic reflétant l’état actuel du journal.

Peek retourne également les messages qui ont été verrouillés et dont le traitement en cours par d’autres destinataires n’est pas encore terminé. Toutefois, comme Peek retourne un instantané déconnecté, l’état de verrouillage d’un message n’est pas visible sur les messages parcourus, et les propriétés [LockedUntilUtc](/dotnet/api/microsoft.azure.servicebus.message.systempropertiescollection.lockeduntilutc) et [LockToken](/dotnet/api/microsoft.azure.servicebus.message.systempropertiescollection.locktoken#Microsoft_Azure_ServiceBus_Message_SystemPropertiesCollection_LockToken) déclenchent une exception [InvalidOperationException](/dotnet/api/system.invalidoperationexception) quand l’application tente de lire ces messages.

## <a name="peek-apis"></a>API de l’outil Peek

Les méthodes [Peek/PeekAsync](/dotnet/api/microsoft.azure.servicebus.core.messagereceiver.peekasync#Microsoft_Azure_ServiceBus_Core_MessageReceiver_PeekAsync) et [PeekBatch/PeekBatchAsync](/dotnet/api/microsoft.servicebus.messaging.queueclient.peekbatchasync#Microsoft_ServiceBus_Messaging_QueueClient_PeekBatchAsync_System_Int64_System_Int32_) sont fournies dans toutes les bibliothèques de client .NET et Java, ainsi que sur tous les objets récepteurs : **MessageReceiver**, **MessageSession**. Peek traite l’ensemble des files d’attente et des abonnements, ainsi que leurs files d’attente de lettres mortes respectives.

Quand elle est appelée à plusieurs reprises, la méthode Peek énumère tous les messages contenus dans le journal des files d’attente ou des abonnements, dans l’ordre de leur numéro séquentiel (du plus petit au plus grand). Cela correspond à l’ordre dans lequel les messages ont été mis en file d’attente, et pas à l’ordre dans lequel ils peuvent être récupérés au final.

[PeekBatch](/dotnet/api/microsoft.servicebus.messaging.queueclient.peekbatch#Microsoft_ServiceBus_Messaging_QueueClient_PeekBatch_System_Int32_) récupère plusieurs messages et les retourne sous la forme d’une énumération. Si aucun message n’est disponible, l’objet d’énumération est vide (non Null).

Vous pouvez également utiliser une surcharge de la méthode en définissant un [SequenceNumber](/dotnet/api/microsoft.azure.servicebus.message.systempropertiescollection.sequencenumber#Microsoft_Azure_ServiceBus_Message_SystemPropertiesCollection_SequenceNumber) de démarrage, puis appeler la surcharge de la méthode sans paramètre pour continuer l’énumération. **PeekBatch** fonctionne de façon équivalente, mais récupère tout un ensemble de messages à la fois.

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur la messagerie Service Bus, consultez les articles suivants :

* [Files d’attente, rubriques et abonnements Service Bus](service-bus-queues-topics-subscriptions.md)
* [Prise en main des files d’attente Service Bus](service-bus-dotnet-get-started-with-queues.md)
* [Utilisation des rubriques et abonnements Service Bus](service-bus-dotnet-how-to-use-topics-subscriptions.md)
