---
author: kgremban
ms.service: iot-edge
ms.topic: include
ms.date: 12/30/2019
ms.author: kgremban
ms.openlocfilehash: 0c43c6dcced94225e9ab9ae903535ce74286ad9a
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2020
ms.locfileid: "87406710"
---
## <a name="create-a-container-registry"></a>Créer un registre de conteneur

Dans ce tutoriel, utilisez l’extension Azure IoT Tools pour générer un module et créer une **image conteneur** à partir des fichiers. Puis envoyez cette image à un **registre** qui stocke et gère vos images. Enfin, déployez votre image à partir de votre registre de façon à l’exécuter sur votre appareil IoT Edge.

Vous pouvez utiliser n’importe quel registre Docker pour stocker vos images conteneur. [Azure Container Registry](https://docs.microsoft.com/azure/container-registry/) et [Docker Hub](https://docs.docker.com/docker-hub/repos/#viewing-repository-tags) sont deux services de registre Docker connus. Ce didacticiel utilise Azure Container Registry.

Si vous ne disposez pas d’un registre de conteneurs, suivez ces étapes pour en créer un dans Azure :

1. Dans le [portail Azure](https://portal.azure.com), sélectionnez **Créer une ressource** > **Conteneurs** > **Container Registry**.

2. Fournissez les valeurs suivantes pour créer votre registre de conteneurs :

   | Champ | Valeur |
   | ----- | ----- |
   | Abonnement | Sélectionnez un abonnement dans la liste déroulante. |
   | Resource group | Nous vous recommandons d’utiliser le même groupe de ressources pour toutes les ressources de test que vous créez dans le cadre des démarrages rapides et didacticiels IoT Edge. Par exemple, utilisez **IoTEdgeResources**. |
   | Nom du registre | Fournissez un nom unique. |
   | Location | Choisissez un emplacement proche de vous. |
   | SKU | Sélectionnez **De base**. |

3. Sélectionnez **Create** (Créer).

4. Une fois votre registre de conteneurs créé, accédez à celui-ci, puis dans le volet gauche, sélectionnez **Clés d’accès** dans le menu situé sous **Paramètres**. 

5. Cliquez pour permettre à l’utilisateur administrateur d’afficher le **nom d’utilisateur** et le **mot de passe** pour votre registre de conteneurs.

6. Copiez les valeurs pour **Serveur de connexion**, **Nom d’utilisateur** et **Mot de passe**, et conservez-les dans un endroit pratique et approprié. Vous utilisez ces valeurs dans le tutoriel pour permettre l’accès au registre de conteneurs.

   ![Copiez le serveur de connexion, le nom d’utilisateur et le mot de passe pour le registre de conteneurs.](./media/iot-edge-create-container-registry/registry-access-key.png)