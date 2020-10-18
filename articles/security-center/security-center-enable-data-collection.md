---
title: Collecte de données dans Azure Security Center | Microsoft Docs
description: Cet article explique comment installer un Log Analytics Agent et de définir un espace de travail Log Analytics dans lequel stocker les données collectées.
services: security-center
author: memildin
manager: rkarlin
ms.service: security-center
ms.topic: quickstart
ms.date: 10/08/2020
ms.author: memildin
ms.openlocfilehash: e5c9540bed34de3cad5c74c7041c8d7e06aef9ca
ms.sourcegitcommit: ba7fafe5b3f84b053ecbeeddfb0d3ff07e509e40
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/12/2020
ms.locfileid: "91946057"
---
# <a name="data-collection-in-azure-security-center"></a>Collecte de données dans Azure Security Center
Azure Security Center collecte des données à partir de vos machines virtuelles Azure, groupes de machines virtuelles identiques, conteneurs IaaS et ordinateurs autres qu’Azure (y compris locaux) pour surveiller les menaces et vulnérabilités de sécurité. Les données sont collectées à l’aide de l’agent Log Analytics, qui lit divers journaux d’événements et configurations liées à la sécurité de la machine et copie les données dans votre espace de travail à des fins d’analyse. Il peut s’agir des données suivantes : type et version de système d’exploitation, journaux d’activité de système d’exploitation (journaux d’événements Windows), processus en cours d’exécution, nom de machine, adresses IP et utilisateur connecté.

La collecte de données est requise pour fournir une visibilité des mises à jour manquantes, des paramètres de sécurité du système d’exploitation mal configurés, de l’état de protection du point de terminaison ainsi que de l’intégrité et de la protection contre les menaces. La collecte de données est nécessaire uniquement pour les ressources de calcul (machines virtuelles, groupes de machines virtuelles identiques, conteneurs IaaS et ordinateurs autres qu’Azure). Vous pouvez bénéficier d’Azure Security Center même si vous ne configurez pas d’agents ; toutefois, vous disposerez d’une sécurité limitée et les fonctionnalités répertoriées ci-dessus ne sont pas pris en charge.  

Cet article explique comment installer un Log Analytics Agent et de définir un espace de travail Log Analytics dans lequel stocker les données collectées. Les deux opérations sont nécessaires pour activer la collecte de données. Le stockage de données dans Log Analytics, que vous utilisiez un espace de travail nouveau ou existant, peut occasionner des frais supplémentaires. Pour plus d’informations, consultez la [page relative aux prix appliqués](https://azure.microsoft.com/pricing/details/security-center/).

> [!TIP]
> Pour obtenir la liste des plateformes prises en charge, consultez [Plateformes prises en charge dans Azure Security Center](security-center-os-coverage.md).

## <a name="enable-automatic-provisioning-of-the-log-analytics-agent"></a>Activer l’approvisionnement automatique du Log Analytics Agent <a name="auto-provision-mma"></a>

> [!NOTE]
> Utilisateurs d’Azure Sentinel : notez que la collecte des événements de sécurité dans le contexte d’un seul espace de travail peut être configurée à partir d’Azure Security Center ou d’Azure Sentinel, mais pas des deux à la fois. Si vous envisagez d’ajouter Azure Sentinel à un espace de travail qui reçoit déjà des alertes Azure Defender du Centre de sécurité Azure, et qui est défini pour collecter des événements de sécurité, vous disposez de deux options :
> - Laissez la collecte d’événements de sécurité dans Azure Security Center telle quelle. Vous êtes alors en mesure d’interroger et d’analyser ces événements dans Azure Sentinel ainsi que dans Azure Defender. Toutefois, vous n’êtes pas en mesure de surveiller l’état de connectivité du connecteur ou de modifier sa configuration dans Azure Sentinel. Si cela est important pour vous, envisagez la deuxième option.
>
> - [Désactivez la collecte des événements de sécurité](#data-collection-tier) dans Azure Security Center, puis ajoutez le connecteur Événements de sécurité dans Azure Sentinel. Comme pour la première option, vous êtes en mesure d’interroger et d’analyser les événements à la fois dans Azure Sentinel et Azure Defender/ASC. Cependant, vous pouvez maintenant surveiller l’état de connectivité du connecteur ou modifier sa configuration dans, et uniquement dans, Azure Sentinel.


Pour collecter les données à partir des machines, vous devez avoir installé le Log Analytics Agent. L’installation de l’agent peut être automatique (recommandé), ou vous pouvez l’installer manuellement. L’approvisionnement automatique est désactivé par défaut.

Lorsque l’approvisionnement automatique est activé, Security Center déploie le Log Analytics Agent sur toutes les machines virtuelles Azure prises en charge et toutes celles nouvellement créées. L’approvisionnement automatique est recommandé, mais vous pouvez installer l’agent manuellement si nécessaire (consultez [Installation manuelle de l’agent Log Analytics](#manual-agent)).

Grâce à l’agent déployé sur vos machines, Security Center peut fournir des recommandations supplémentaires sur l’état de mise à jour du système, les configurations de la sécurité du système d’exploitation et la protection des points de terminaison, et générer des alertes de sécurité supplémentaires.

Pour activer le provisionnement automatique de l’agent Log Analytics :

1. Dans le menu de Security Center, sélectionnez **Tarification et paramètres**.
1. Sélectionnez l’abonnement approprié.
1. Dans la page **Collecte des données**, définissez **Provisionnement automatique** sur **On** (activé).
1. Sélectionnez **Enregistrer**.

    :::image type="content" source="./media/security-center-enable-data-collection/enable-automatic-provisioning.png" alt-text="Activation du provisionnement automatique de l’agent Log Analytics":::

    >[!TIP]
    > Si un espace de travail doit être approvisionné, l’installation de l’agent peut prendre jusqu’à 25 minutes.


## <a name="workspace-configuration"></a>Configuration de l’espace de travail
Les données collectées par Security Center sont stockées dans les espaces de travail Log Analytics. Vous pouvez choisir de collecter les données à partir des machines virtuelles Azure dans des espaces de travail créés par Security Center ou dans un espace de travail existant que vous avez créé. 

La configuration de l’espace de travail est définie par abonnement, et plusieurs abonnements peuvent utiliser le même espace de travail.

### <a name="using-a-workspace-created-by-security-center"></a>Utilisation d’un espace de travail créé par Security Center

Security Center peut créer automatiquement un espace de travail par défaut dans lequel stocker les données. 

Pour sélectionner un espace de travail créé par Security Center :

1. Sous **Configuration de l’espace de travail par défaut**, sélectionnez Utiliser un ou des espaces de travail créés par Security Center.
    :::image type="content" source="./media/security-center-enable-data-collection/workspace-selection.png" alt-text="Activation du provisionnement automatique de l’agent Log Analytics"::: 

1. Cliquez sur **Enregistrer**.<br>
    Security Center crée un groupe de ressources et un espace de travail par défaut dans cette zone géographique et connecte l’agent à cet espace de travail. La convention d’affectation de noms pour l’espace de travail et le groupe de ressources est la suivante :<br>
   **Espace de travail : DefaultWorkspace-[ID-abonnement]-[géolocalisation]<br> Groupe de ressources : DefaultResourceGroup-[géolocalisation]**

   Si un abonnement contient des machines virtuelles se trouvant dans plusieurs zones géographiques, Security Center crée plusieurs espaces de travail. Plusieurs espaces de travail sont créés pour tenir à jour les règles de confidentialité des données.
1. Security Center activera automatiquement une solution Security Center sur l’espace de travail, en fonction du niveau de tarification défini pour l’abonnement. 

> [!NOTE]
> Le niveau tarifaire Log Analytics des espaces de travail créés par Security Center n’affecte pas la facturation Security Center. La facturation Security Center est toujours basée sur votre stratégie de sécurité Security Center et sur les solutions installées sur un espace de travail. Pour les abonnements sans Azure Defender, Security Center active la solution *SecurityCenterFree* sur l’espace de travail par défaut. Pour les abonnements avec Azure Defender, Security Center active la solution *Security* sur l’espace de travail par défaut.
> Le stockage de données dans Log Analytics peut occasionner des frais supplémentaires de stockage de données. Pour plus d’informations, consultez la [page relative aux prix appliqués](https://azure.microsoft.com/pricing/details/security-center/).

Pour plus d’informations sur les comptes Log Analytics existants, consultez [Clients Log Analytics existants](./faq-azure-monitor-logs.md).

### <a name="using-an-existing-workspace"></a>Utilisation d’un espace de travail existant

Si vous disposez déjà d’un espace de travail Log Analytics existant, vous souhaiterez peut-être utiliser le même espace de travail.

Pour utiliser votre espace de travail Log Analytics existant, vous devez avoir des autorisations de lecture et d’écriture sur l’espace de travail.

> [!NOTE]
> Les solutions activées sur l’espace de travail existant s’appliqueront aux machines virtuelles Azure qui y sont connectées. Pour les solutions payantes, cela peut entraîner des frais supplémentaires. Pour des raisons de confidentialité de données, assurez-vous que votre espace de travail sélectionné est dans la bonne région géographique.
> Le stockage de données dans Log Analytics peut occasionner des frais supplémentaires. Pour plus d’informations, consultez la [page relative aux prix appliqués](https://azure.microsoft.com/pricing/details/security-center/).

Pour sélectionner un espace de travail Log Analytics existant :

1. Sous **Configuration de l’espace de travail par défaut**, sélectionnez **Utiliser un autre espace de travail**.
    :::image type="content" source="./media/security-center-enable-data-collection/use-another-workspace.png" alt-text="Activation du provisionnement automatique de l’agent Log Analytics"::: 

2. Dans le menu déroulant, sélectionnez un espace de travail pour stocker les données collectées.

   > [!NOTE]
   > Dans le menu déroulant, tous les espaces de travail dans l’ensemble de vos abonnements sont disponibles. Pour plus d’informations, consultez [Sélection de l’espace de travail parmi les abonnements](security-center-enable-data-collection.md#cross-subscription-workspace-selection). Vous devez avoir l'autorisation d'accéder à l’espace de travail.
   >
   >

3. Sélectionnez **Enregistrer**.
4. Après avoir sélectionné **Enregistrer**, vous serez invité à reconfigurer les machines virtuelles surveillées précédemment connectées à un espace de travail par défaut.

   - Sélectionnez **Non** si vous souhaitez que les nouveaux paramètres de l’espace de travail s’appliquent uniquement aux nouvelles machines virtuelles. Les nouveaux paramètres de l’espace de travail s’appliquent uniquement aux nouvelles installations d’agent ; machines virtuelles nouvellement détectées sur lesquelles l’agent Log Analytics n’est pas installé.
   - Sélectionnez **Oui** si vous souhaitez que les nouveaux paramètres de l’espace de travail s’appliquent à toutes les machines virtuelles. En outre, chaque machine virtuelle connectée à un espace de travail créé par Security Center est reconnectée au nouvel espace de travail cible.

   > [!NOTE]
   > Si vous sélectionnez Oui, vous ne devez pas supprimer les espaces de travail créés par Security Center tant que toutes les machines virtuelles n’ont pas été reconnectées au nouvel espace de travail cible. Cette opération échoue si un espace de travail est supprimé trop tôt.
   >
   >

   - Pour annuler l’opération, sélectionnez **Annuler**.

     ![Passer en revue les options pour reconfigurer les machines virtuelles surveillées][3]

5. Indiquez si Azure Defender sera activé ou non pour l’espace de travail.

    Pour utiliser un espace de travail existant, définissez le niveau tarifaire pour l’espace de travail. Une solution Security Center sera installée sur l’espace de travail si elle ne s’y trouve pas déjà.

    1. Dans le menu principal de Security Center, sélectionnez **Tarification et paramètres**.
     
    1. Sélectionnez l’espace de travail auquel vous connecterez l’agent.

    1. Sélectionnez **Azure Defender activé** ou **Azure Defender désactivé**.

   
   >[!NOTE]
   >Si l’espace de travail a déjà une solution **Security** ou **SecurityCenterFree** activée, la tarification sera définie automatiquement. 


## <a name="cross-subscription-workspace-selection"></a>Sélection de l’espace de travail parmi les abonnements
Quand vous sélectionnez un espace de travail dans lequel stocker vos données, tous les espaces de travail dans l’ensemble de vos abonnements sont disponibles. La sélection de l’espace de travail parmi les abonnements vous permet de collecter des données à partir de machines virtuelles exécutées dans différents abonnements, et de les stocker dans l’espace de travail de votre choix. Cette sélection est utile si vous utilisez un espace de travail centralisé de votre organisation et que vous souhaitez l’utiliser pour la collecte de données de sécurité. Pour plus d’informations sur la gestion des espaces de travail, consultez [Gérer l’accès à l’espace de travail](https://docs.microsoft.com/azure/log-analytics/log-analytics-manage-access).



## <a name="data-collection-tier"></a>Niveau de collecte des données
La sélection d’un niveau de collecte de données dans Azure Security Center n’affecte que le stockage d’événements de sécurité dans votre espace de travail Log Analytics. L’agent Log Analytics continuera de collecter et d’analyser les événements de sécurité requis pour la protection d’Azure Security Center contre les menaces, quel que soit le niveau d’événements de sécurité que vous choisissez de stocker dans votre espace de travail Log Analytics (le cas échéant). Le choix de stocker des événements de sécurité dans votre espace de travail permettra l’investigation, la recherche et l’audit de ces événements dans votre espace de travail. 
> [!NOTE]
> Le stockage de données dans Log Analytics peut occasionner des frais supplémentaires. Pour plus d’informations, consultez la [page relative aux prix appliqués](https://azure.microsoft.com/pricing/details/security-center/).

Vous pouvez choisir la stratégie de filtrage adaptée à vos abonnements et espaces de travail à partir de quatre ensembles d’événements à stocker dans votre espace de travail : 
- **Aucun** : désactiver le stockage d’événements de sécurité. Il s'agit du paramètre par défaut.
- **Minimal** : un plus petit ensemble d’événements pour les clients qui souhaitent réduire le volume d’événements.
- **Commun** : il s’agit d’un ensemble d’événements qui répond aux besoins de la plupart des clients et leur permet d’avoir une piste d’audit complète.
- **Tous les événements** : pour les clients qui souhaitent s’assurer que tous les événements sont stockés.

Ces ensembles d’événements de sécurité sont disponibles uniquement avec Azure Defender. Consultez [Tarification](security-center-pricing.md) pour en savoir plus sur les niveaux tarifaires de Security Center.

Ces ensembles ont été conçus pour des scénarios classiques. Veillez à évaluer celui qui correspond à vos besoins avant de l’implémenter.

Pour déterminer les événements qui appartiennent aux ensembles d’événements **Commun** et **Minimal**, nous avons travaillé avec les clients et les normes industrielles pour en savoir plus sur la fréquence non filtrée de chaque événement et leur utilisation. Nous avons utilisé les instructions suivantes dans ce processus :

- **Minimal** : vérifiez que cet ensemble couvre uniquement les événements qui peuvent indiquer une violation avérée et des événements importants qui ont un volume très faible. Par exemple, cet ensemble contient une connexion utilisateur ayant réussi et ayant échoué (ID d’événement 4624, 4625), mais il ne contient pas de déconnexion, ce qui est important pour l’audit, mais pas pour la détection, et a un volume relativement élevé. La plupart du volume de données de cet ensemble est constituée d’événements de connexion et d’un événement de création de processus (ID d’événement 4688).
- **Commun** : fournissez une piste d’audit utilisateur complète dans cet ensemble. Par exemple, cet ensemble contient les connexions et déconnexions de l’utilisateur (ID d’événement 4634). Nous incluons les actions d’audit, telles que les modifications de groupe de sécurité, les opérations Kerberos du contrôleur de domaine clé et les autres événements recommandés par les organisations du secteur.

Les événements qui ont un volume très faible ont été inclus dans l’ensemble Commun, car la motivation principale à préférer cet ensemble à l’ensemble Tous les événements est de réduire le volume et de ne pas filtrer d’événements spécifiques.

Voici le détail complet des ID d’événement App Locker et de sécurité pour chaque ensemble :

| Couche Données | Indicateurs d’événements collectés |
| --- | --- |
| Minimales | 1102,4624,4625,4657,4663,4688,4700,4702,4719,4720,4722,4723,4724,4727,4728,4732,4735,4737,4739,4740,4754,4755, |
| | 4756,4767,4799,4825,4946,4948,4956,5024,5033,8001,8002,8003,8004,8005,8006,8007,8222 |
| Courant | 1,299,300,324,340,403,404,410,411,412,413,431,500,501,1100,1102,1107,1108,4608,4610,4611,4614,4622, |
| |  4624,4625,4634,4647,4648,4649,4657,4661,4662,4663,4665,4666,4667,4688,4670,4672,4673,4674,4675,4689,4697, |
| | 4700,4702,4704,4705,4716,4717,4718,4719,4720,4722,4723,4724,4725,4726,4727,4728,4729,4733,4732,4735,4737, |
| | 4738,4739,4740,4742,4744,4745,4746,4750,4751,4752,4754,4755,4756,4757,4760,4761,4762,4764,4767,4768,4771, |
| | 4774,4778,4779,4781,4793,4797,4798,4799,4800,4801,4802,4803,4825,4826,4870,4886,4887,4888,4893,4898,4902, |
| | 4904,4905,4907,4931,4932,4933,4946,4948,4956,4985,5024,5033,5059,5136,5137,5140,5145,5632,6144,6145,6272, |
| | 6273,6278,6416,6423,6424,8001,8002,8003,8004,8005,8006,8007,8222,26401,30004 |

> [!NOTE]
> - Si vous utilisez l’objet de stratégie de groupe (GPO), il est recommandé d’activer les stratégies d’audit d’événement de création de processus 4688 et le champ *CommandLine* à l’intérieur de l’événement 4688. Pour plus d’informations sur l’événement de création de processus 4688, consultez la [FAQ](faq-data-collection-agents.md#what-happens-when-data-collection-is-enabled) de Security Center. Pour plus d’informations sur ces stratégies d’audit, consultez les [recommandations pour la stratégie d’audit](https://docs.microsoft.com/windows-server/identity/ad-ds/plan/security-best-practices/audit-policy-recommendations).
> -  Pour activer la collecte de données pour les [Contrôles d’application adaptatifs](security-center-adaptive-application.md), Security Center configure une stratégie AppLocker locale en mode Audit pour autoriser toutes les applications. Cela amène AppLocker à générer des événements qui sont ensuite recueillis et exploités par Security Center. Il est important de noter que cette stratégie ne sera configurée sur aucun ordinateur sur lequel une stratégie AppLocker est déjà configurée. 
> - Pour collecter la plateforme de filtrage Windows [ID d’événement 5156](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventID=5156), vous devez activer [Connexion de la plateforme de filtrage d’audits](https://docs.microsoft.com/windows/security/threat-protection/auditing/audit-filtering-platform-connection) (Auditpol /set /subcategory:"Filtering Platform Connection" /Success:Enable)
>

Pour choisir votre stratégie de filtrage :
1. Sur la page **Collecte de données**, sélectionnez votre stratégie de filtrage sous **Stocker des données brutes supplémentaires - Événements de sécurité Windows**.
 
1. Sélectionnez **Enregistrer**.
    :::image type="content" source="./media/security-center-enable-data-collection/data-collection-tiers.png" alt-text="Activation du provisionnement automatique de l’agent Log Analytics":::

### <a name="automatic-provisioning-in-cases-of-a-pre-existing-agent-installation"></a>Approvisionnement automatique en cas d’installation d’un agent préexistant <a name="preexisting"></a> 

Les cas d’usage suivants spécifient la manière dont l’approvisionnement automatique fonctionne lorsqu’un agent ou une extension sont déjà installés. 

- Log Analytics Agent est installé sur la machine, mais pas en tant qu’extension (agent direct)<br>
Si l’agent Log Analytics est installé directement sur la machine virtuelle (pas en tant qu’extension Azure), Security Center installe l’extension de l’agent Log Analytics, et peut mettre à niveau l’agent Log Analytics vers la dernière version.
L’agent installé continue de rendre compte à ses espaces de travail déjà configurés et à l’espace de travail configuré dans Security Center (multihébergement pris en charge sur les machines Windows).
Si l’espace de travail configuré est un espace de travail utilisateur (pas un espace de travail par défaut de Security Center), vous devez installer la solution « security/securityFree » sur ce dernier pour que Security Center démarre le traitement des événements à partir des machines virtuelles et ordinateurs rendant compte à cet espace de travail.<br>
<br>
Pour les machines Linux, le multihébergement d’agent n’est pas encore pris en charge, par conséquent, si une installation existante de l’agent est détectée, l’approvisionnement automatique n’a pas lieu et la configuration de la machine n’est pas modifiée.
<br>
Pour les machines existantes sur les abonnements intégrés à Security Center avant le 17 mars 2019, quand un agent existant est détecté, l’agent Log Analytics n’est pas installé et la machine n’est pas affectée. Pour ces machines, consultez la recommandation « Résoudre les problèmes d’intégrité de l’agent d’analyse sur vos machines » pour résoudre les problèmes d’installation de l’agent sur ces machines.

  
- L'agent System Center Operations Manager est installé sur la machine<br>
Security Center installe l’extension Log Analytics Agent parallèlement à l’instance Operations Manager existante. L’agent Operations Manager existant continue de rendre compte normalement au serveur Operations Manager. L’agent Operations Manager et l’agent Log Analytics partagent des bibliothèques runtime communes, qui sont mises à jour vers la dernière version lors de ce processus. Si la version 2012 de l’agent Operations Manager est installée, n’activez **pas** l’approvisionnement automatique.<br>

- Une extension de machine virtuelle existante est présente<br>
    - Lorsque l’Agent Monitoring est installé en tant qu’extension, la configuration de l’extension permet de rendre compte à un seul espace de travail. Security Center n’écrase pas les connexions existantes des espaces de travail utilisateur. Security Center stocke les données de sécurité à partir d’une machine virtuelle dans un espace de travail qui est déjà connecté, sous réserve que la solution « security » ou « securityFree » y soit installée. Security Center peut mettre à niveau la version de l'extension vers la dernière version lors de ce processus.  
    - Pour voir à quel espace de travail l’extension existante envoie des données, exécutez le test pour [Valider la connectivité avec Azure Security Center](https://blogs.technet.microsoft.com/yuridiogenes/2017/10/13/validating-connectivity-with-azure-security-center/). Vous pouvez également ouvrir des espaces de travail Log Analytics, sélectionner un espace de travail, sélectionner la machine virtuelle, puis rechercher la connexion de l'agent Log Analytics. 
    - Si vous disposez d’un environnement où l'agent Log Analytics est installé sur les stations de travail clientes et rapportent à un espace de travail Log Analytics existant, consultez la liste des [ systèmes d’exploitation pris en charge par Azure Security Center](security-center-os-coverage.md) pour vous assurer que votre système d’exploitation est pris en charge. Pour plus d’informations, voir [Clients Log Analytics actuels](./faq-azure-monitor-logs.md).
 
### <a name="turn-off-automatic-provisioning"></a>Désactiver l’approvisionnement automatique<a name="offprovisioning"></a>
Pour désactiver le provisionnement automatique de l’agent Log Analytics :

1. Dans le menu de Security Center dans le portail, sélectionnez **Tarification et paramètres**.
2. Sélectionnez l’abonnement approprié.

    :::image type="content" source="./media/security-center-enable-data-collection/select-subscription.png" alt-text="Activation du provisionnement automatique de l’agent Log Analytics":::

3. Sélectionnez **Collection de données**.
4. Sous **Provisionnement automatique**, sélectionnez **Désactivé** pour désactiver le provisionnement automatique.
5. Sélectionnez **Enregistrer**. 


Quand le provisionnement automatique est désactivé, la section de configuration de l’espace de travail par défaut n’est pas affichée.

Si vous désactivez l’approvisionnement automatique après qu’il a été précédemment activé, les agents ne seront pas approvisionnés sur les nouvelles machines virtuelles.

 
> [!NOTE]
>  La désactivation de l’approvisionnement automatique ne supprime pas le Log Analytics Agent des machines virtuelles Azure sur lesquelles l’agent était approvisionné. Pour plus d’informations sur la suppression de l’extension OMS, consultez [Comment supprimer des extensions OMS installées par Security Center](faq-data-collection-agents.md#remove-oms).
>
    
## <a name="manual-agent-provisioning"></a>Approvisionnement manuel d’un agent <a name="manual-agent"></a>
 
Il existe plusieurs manières d’installer le Log Analytics Agent manuellement. Lors de l’installation manuelle, veillez à désactiver l’approvisionnement automatique.

### <a name="operations-management-suite-vm-extension-deployment"></a>Déploiement de l’extension de machines virtuelles Operations Management Suite 

Vous pouvez installer manuellement Microsoft le Log Analytics Agent pour que Security Center puisse collecter des données de sécurité sur vos machines virtuelles et fournir des suggestions et des alertes.

1. Désactivez le provisionnement automatique.

1. Si vous le souhaitez, vous pouvez créer un espace de travail.

1. Activez Azure Defender sur l’espace de travail sur lequel vous installez l’agent Log Analytics :

    1. Dans le menu de Security Center, sélectionnez **Tarification et paramètres**.

    1. Définissez l’espace de travail sur lequel vous installez l’agent. Assurez-vous que l’espace de travail est dans le même abonnement que vous utilisez dans Security Center et que vous disposez d’autorisations en lecture/écriture sur l’espace de travail.

    1. Activez Azure Defender, puis sélectionnez **Enregistrer**.

       >[!NOTE]
       >Si l’espace de travail a déjà une solution **Security** ou **SecurityCenterFree** activée, la tarification sera définie automatiquement. 

1. Si vous voulez déployer les agents sur de nouvelles machines virtuelles en utilisant un modèle Resource Manager, installez l’agent Log Analytics :

   - [Installer l’agent Log Analytics pour Windows](../virtual-machines/extensions/oms-windows.md)
   - [Installer l’agent Log Analytics pour Linux](../virtual-machines/extensions/oms-linux.md)

1. Pour déployer les extensions sur des machines virtuelles existantes, suivez les instructions de [Collecter des données sur les machines virtuelles Azure](../azure-monitor/learn/quick-collect-azurevm.md).

   > [!NOTE]
   > La section **Collecter les données d’événements et de performances** est facultative.
   >

1. Pour utiliser PowerShell afin de déployer l’extension, suivez les instructions de la documentation relative aux machines virtuelles :

    - [Pour les machines Windows](https://docs.microsoft.com/azure/virtual-machines/extensions/oms-windows?toc=%2Fazure%2Fazure-monitor%2Ftoc.json#powershell-deployment)
    - [Pour les machines Linux](https://docs.microsoft.com/azure/virtual-machines/extensions/oms-linux?toc=%2Fazure%2Fazure-monitor%2Ftoc.json#azure-cli-deployment)



> [!NOTE]
> Pour obtenir des instructions sur la manière d’intégrer Security Center à l’aide de PowerShell, voir [Automatiser l’intégration d’Azure Security Center à l’aide de PowerShell](security-center-powershell-onboarding.md).

## <a name="troubleshooting"></a>Dépannage

-   Pour identifier des problèmes d’approvisionnement automatique, consultez [Problèmes d’intégrité de l’agent de surveillance](security-center-troubleshooting-guide.md#mon-agent).

-  Pour identifier la configuration réseau requise pour l’agent de surveillance, consultez [Résolution des problèmes de configuration réseau requise de l’agent de surveillance](security-center-troubleshooting-guide.md#mon-network-req).
-   Pour identifier des problèmes d’intégration manuelle, voir [Comment faire pour résoudre les problèmes d’intégration de Microsoft Operations Management Suite](https://support.microsoft.com/help/3126513/how-to-troubleshoot-operations-management-suite-onboarding-issues).

- Pour identifier les problèmes liés aux machines virtuelles et ordinateurs non supervisés :

    Une machine virtuelle ou un ordinateur n’est pas supervisé par Security Center si la machine n’exécute pas l’extension de l’agent Log Analytics. Un agent local peut être déjà installé sur une machine, par exemple l’agent direct OMS ou l’agent System Center Operations Manager. Les machines sur lesquelles sont installés ces agents sont considérées comme non surveillées, car ces agents ne sont pas entièrement pris en charge par Security Center. Pour tirer pleinement parti de toutes les fonctionnalités de Security Center, l’extension de l’agent Log Analytics est nécessaire.

    Pour en savoir plus sur la raison pour laquelle Security Center ne peut pas superviser correctement les machines virtuelles et ordinateurs initialisés pour le provisionnement automatique, consultez [Problèmes d’intégrité de l’agent de supervision](security-center-troubleshooting-guide.md#mon-agent).


## <a name="next-steps"></a>Étapes suivantes
Cet article vous a montré le fonctionnement de la collecte de données et de l’approvisionnement automatique dans Security Center. Pour plus d’informations sur Security Center, consultez les pages suivantes :

- [FAQ de Azure Security Center](faq-general.md): forum aux questions concernant l’utilisation de ce service.
- [Surveillance de l’intégrité de la sécurité dans Azure Security Center](security-center-monitoring.md): découvrez comment surveiller l’intégrité de vos ressources Azure.



<!--Image references-->
[3]: ./media/security-center-enable-data-collection/reconfigure-monitored-vm.png
[9]: ./media/security-center-enable-data-collection/pricing-tier.png
[11]: ./media/security-center-enable-data-collection/log-analytics.png
[12]: ./media/security-center-enable-data-collection/log-analytics2.png
