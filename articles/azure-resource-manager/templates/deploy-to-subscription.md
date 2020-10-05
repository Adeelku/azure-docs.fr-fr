---
title: Déployer des ressources sur un abonnement
description: Décrit comment créer un groupe de ressources dans un modèle Azure Resource Manager. Est également expliqué le déploiement des ressources sur l’étendue de l’abonnement Azure.
ms.topic: conceptual
ms.date: 09/15/2020
ms.openlocfilehash: 3889f5a06f138114dfe4511d0957558d6d803c8e
ms.sourcegitcommit: 80b9c8ef63cc75b226db5513ad81368b8ab28a28
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/16/2020
ms.locfileid: "90605173"
---
# <a name="create-resource-groups-and-resources-at-the-subscription-level"></a>Créer des groupes de ressources et des ressources au niveau de l’abonnement

Pour simplifier la gestion des ressources, vous pouvez utiliser un modèle Resource Manager pour déployer des ressources au niveau de votre abonnement Azure. Par exemple, vous pouvez déployer des [stratégies](../../governance/policy/overview.md) et un [contrôle d’accès en fonction du rôle Azure (Azure RBAC)](../../role-based-access-control/overview.md) sur votre abonnement, ce qui les applique à l’ensemble de votre abonnement. Vous pouvez également créer des groupes de ressources au sein de l’abonnement et déployer des ressources sur ces groupes de ressources dans l’abonnement.

> [!NOTE]
> Vous pouvez déployer sur 800 différents groupes de ressources dans un déploiement de niveau abonnement.

Pour déployer des modèles au niveau de l’abonnement, utilisez Azure CLI, PowerShell, l’API REST ou le portail.

## <a name="supported-resources"></a>Ressources prises en charge

Tous les types de ressources ne peuvent pas être déployés au niveau de l’abonnement. Cette section répertorie les types de ressources pris en charge.

Pour Azure Blueprints, utilisez :

* [artifacts](/azure/templates/microsoft.blueprint/blueprints/artifacts)
* [blueprints](/azure/templates/microsoft.blueprint/blueprints)
* [blueprintAssignments](/azure/templates/microsoft.blueprint/blueprintassignments)
* [versions (Blueprints)](/azure/templates/microsoft.blueprint/blueprints/versions)

Pour les stratégies Azure, utilisez :

* [policyAssignments](/azure/templates/microsoft.authorization/policyassignments)
* [policyDefinitions](/azure/templates/microsoft.authorization/policydefinitions)
* [policySetDefinitions](/azure/templates/microsoft.authorization/policysetdefinitions)
* [remediations](/azure/templates/microsoft.policyinsights/remediations)

Pour le contrôle d’accès en fonction du rôle, utilisez :

* [roleAssignments](/azure/templates/microsoft.authorization/roleassignments)
* [roleDefinitions](/azure/templates/microsoft.authorization/roledefinitions)

Pour les modèles imbriqués déployés sur des groupes de ressources, utilisez :

* [deployments](/azure/templates/microsoft.resources/deployments)

Pour la création de groupes de ressources, utilisez :

* [resourceGroups](/azure/templates/microsoft.resources/resourcegroups)

Pour la gestion de votre abonnement, utilisez :

* [budgets](/azure/templates/microsoft.consumption/budgets)
* [supportPlanTypes](/azure/templates/microsoft.addons/supportproviders/supportplantypes)
* [balises](/azure/templates/microsoft.resources/tags)

Les autres types pris en charge sont les suivants :

* [scopeAssignments](/azure/templates/microsoft.managednetwork/scopeassignments)
* [eventSubscriptions](/azure/templates/microsoft.eventgrid/eventsubscriptions)
* [peerAsns](/azure/templates/microsoft.peering/2019-09-01-preview/peerasns)

### <a name="schema"></a>schéma

Le schéma que vous utilisez pour les déploiements au niveau de l’abonnement est différent de celui utilisé pour les déploiements de groupes de ressources.

Pour les modèles, utilisez :

```json
https://schema.management.azure.com/schemas/2018-05-01/subscriptionDeploymentTemplate.json#
```

Le schéma d’un fichier de paramètres est le même pour toutes les étendues de déploiement. Fichiers de fichiers de paramètres, utilisez :

```json
https://schema.management.azure.com/schemas/2019-04-01/deploymentParameters.json#
```

## <a name="deployment-commands"></a>Commandes de déploiement

Les commandes utilisées pour les déploiements au niveau de l’abonnement sont différentes de celles utilisées pour les déploiements de groupes de ressources.

Pour l’interface de ligne de commande Azure, utilisez [az deployment sub create](/cli/azure/deployment/sub#az-deployment-sub-create). L’exemple suivant déploie un modèle pour créer un groupe de ressources :

```azurecli-interactive
az deployment sub create \
  --name demoSubDeployment \
  --location centralus \
  --template-uri "https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/emptyRG.json" \
  --parameters rgName=demoResourceGroup rgLocation=centralus
```

Pour la commande de déploiement PowerShell, utilisez [New-AzDeployment](/powershell/module/az.resources/new-azdeployment) ou **New-AzSubscriptionDeployment**. L’exemple suivant déploie un modèle pour créer un groupe de ressources :

```azurepowershell-interactive
New-AzSubscriptionDeployment `
  -Name demoSubDeployment `
  -Location centralus `
  -TemplateUri "https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/emptyRG.json" `
  -rgName demoResourceGroup `
  -rgLocation centralus
```

Pour l’API REST, utilisez [Déploiements - Créer au niveau de l’abonnement](/rest/api/resources/deployments/createorupdateatsubscriptionscope).

## <a name="deployment-location-and-name"></a>Emplacement et nom du déploiement

Pour les déploiements au niveau de l’abonnement, vous devez fournir un emplacement de déploiement. L’emplacement du déploiement est distinct de l’emplacement des ressources que vous déployez. L’emplacement de déploiement indique où stocker les données de déploiement.

Vous pouvez fournir un nom de déploiement ou utiliser le nom de déploiement par défaut. Le nom par défaut est le nom du fichier de modèle. Par exemple, le déploiement d’un modèle nommé **azuredeploy.json** crée le nom de déploiement par défaut **azuredeploy**.

Pour chaque nom de déploiement, l’emplacement est immuable. Il n’est pas possible de créer un déploiement dans un emplacement s’il existe un déploiement du même nom dans un autre emplacement. Si vous obtenez le code d’erreur `InvalidDeploymentLocation`, utilisez un autre nom ou le même emplacement que le déploiement précédent pour ce nom.

## <a name="deployment-scopes"></a>Étendues de déploiement

Lors du déploiement sur un abonnement, vous pouvez cibler un abonnement et des groupes de ressources au sein de l’abonnement. Vous ne pouvez déployer sur un abonnement différent de l’abonnement cible. L’utilisateur qui déploie le modèle doit avoir accès à l’étendue spécifiée.

Les ressources définies dans la section Ressources du modèle sont appliquées à l’abonnement.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2018-05-01/subscriptionDeploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
        subscription-level-resources
    ],
    "outputs": {}
}
```

Pour cibler un groupe de ressources au sein de l’abonnement, ajoutez un déploiement imbriqué et incluez la propriété `resourceGroup`. Dans l’exemple suivant, le déploiement imbriqué cible un groupe de ressources nommé `rg2`.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2018-05-01/subscriptionDeploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
        {
            "type": "Microsoft.Resources/deployments",
            "apiVersion": "2020-06-01",
            "name": "nestedDeployment",
            "resourceGroup": "rg2",
            "properties": {
                "mode": "Incremental",
                "template": {
                    nested-template-with-resource-group-resources
                }
            }
        }
    ],
    "outputs": {}
}
```

Dans cet article, vous trouverez des modèles qui montrent comment déployer des ressources sur différentes étendues. Pour un modèle qui crée un groupe de ressources et y déploie un compte de stockage, consultez [Créer un groupe de ressources et des ressources](#create-resource-group-and-resources). Pour un modèle qui crée un groupe de ressources, lui applique un verrou et lui affecte un rôle, consultez [Contrôle d’accès](#access-control).

## <a name="use-template-functions"></a>Utiliser des fonctions de modèle

Pour les déploiements au niveau de l’abonnement, il existe quelques considérations importantes liées à l’utilisation des fonctions de modèle :

* La fonction [resourceGroup()](template-functions-resource.md#resourcegroup)**n’est pas** prise en charge.
* Les fonctions [reference()](template-functions-resource.md#reference) et [list()](template-functions-resource.md#list) sont prises en charge.
* N’utilisez pas [resourceId()](template-functions-resource.md#resourceid) pour obtenir l’ID des ressources déployées au niveau de l’abonnement. À la place, utilisez la fonction [subscriptionResourceId()](template-functions-resource.md#subscriptionresourceid).

  Par exemple, pour obtenir l’ID de ressource d’une définition de stratégie déployée sur un abonnement, utilisez :

  ```json
  subscriptionResourceId('Microsoft.Authorization/roleDefinitions/', parameters('roleDefinition'))
  ```

  L’ID de ressource retourné possède le format suivant :

  ```json
  /subscriptions/{subscriptionId}/providers/{resourceProviderNamespace}/{resourceType}/{resourceName}
  ```

## <a name="resource-groups"></a>Groupes de ressources

### <a name="create-resource-groups"></a>Créer des groupes de ressources

Pour créer un groupe de ressources dans un modèle Resource Manager, définissez une ressource [Microsoft.Resources/resourceGroups](/azure/templates/microsoft.resources/allversions) avec un nom et un emplacement pour le groupe de ressources.

Le modèle suivant crée un groupe de ressources vide.

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2018-05-01/subscriptionDeploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "rgName": {
      "type": "string"
    },
    "rgLocation": {
      "type": "string"
    }
  },
  "variables": {},
  "resources": [
    {
      "type": "Microsoft.Resources/resourceGroups",
      "apiVersion": "2020-06-01",
      "name": "[parameters('rgName')]",
      "location": "[parameters('rgLocation')]",
      "properties": {}
    }
  ],
  "outputs": {}
}
```

Pour créer plus d’un groupe de ressources, utilisez l’[élément copy](copy-resources.md) avec des groupes de ressources.

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2018-05-01/subscriptionDeploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "rgNamePrefix": {
      "type": "string"
    },
    "rgLocation": {
      "type": "string"
    },
    "instanceCount": {
      "type": "int"
    }
  },
  "variables": {},
  "resources": [
    {
      "type": "Microsoft.Resources/resourceGroups",
      "apiVersion": "2020-06-01",
      "location": "[parameters('rgLocation')]",
      "name": "[concat(parameters('rgNamePrefix'), copyIndex())]",
      "copy": {
        "name": "rgCopy",
        "count": "[parameters('instanceCount')]"
      },
      "properties": {}
    }
  ],
  "outputs": {}
}
```

Pour plus d’informations sur l’itération de ressource, consultez [Déployer plusieurs instances d’une ressource dans des modèles Azure Resource Manager](./copy-resources.md) et [Tutoriel : Créer plusieurs instances de ressources grâce à des modèles Resource Manager](./template-tutorial-create-multiple-instances.md).

### <a name="create-resource-group-and-resources"></a>Créer un groupe de ressources et ses ressources

Pour créer le groupe de ressources et déployer des ressources sur celui-ci, utilisez un modèle imbriqué. Le modèle imbriqué définit les ressources à déployer sur le groupe de ressources. Définissez le modèle imbriqué comme dépendant du groupe de ressources pour vous assurer que le groupe de ressources existe avant de déployer les ressources. Vous pouvez effectuer le déploiement sur jusqu’à 800 groupes de ressources.

L’exemple suivant crée un groupe de ressources, et déploie un compte de stockage sur le groupe de ressources.

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2018-05-01/subscriptionDeploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "rgName": {
      "type": "string"
    },
    "rgLocation": {
      "type": "string"
    },
    "storagePrefix": {
      "type": "string",
      "maxLength": 11
    }
  },
  "variables": {
    "storageName": "[concat(parameters('storagePrefix'), uniqueString(subscription().id, parameters('rgName')))]"
  },
  "resources": [
    {
      "type": "Microsoft.Resources/resourceGroups",
      "apiVersion": "2020-06-01",
      "name": "[parameters('rgName')]",
      "location": "[parameters('rgLocation')]",
      "properties": {}
    },
    {
      "type": "Microsoft.Resources/deployments",
      "apiVersion": "2020-06-01",
      "name": "storageDeployment",
      "resourceGroup": "[parameters('rgName')]",
      "dependsOn": [
        "[resourceId('Microsoft.Resources/resourceGroups/', parameters('rgName'))]"
      ],
      "properties": {
        "mode": "Incremental",
        "template": {
          "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
          "contentVersion": "1.0.0.0",
          "parameters": {},
          "variables": {},
          "resources": [
            {
              "type": "Microsoft.Storage/storageAccounts",
              "apiVersion": "2019-06-01",
              "name": "[variables('storageName')]",
              "location": "[parameters('rgLocation')]",
              "sku": {
                "name": "Standard_LRS"
              },
              "kind": "StorageV2"
            }
          ],
          "outputs": {}
        }
      }
    }
  ],
  "outputs": {}
}
```

## <a name="azure-policy"></a>Azure Policy

### <a name="assign-policy-definition"></a>Affecter une définition de stratégie

L’exemple suivant assigne une définition de stratégie existante à l’abonnement. Si la définition de stratégie utilise des paramètres, fournissez-les en tant qu’objet. Si la définition de stratégie n’accepte pas de paramètres, utilisez l’objet vide par défaut.

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2018-05-01/subscriptionDeploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "policyDefinitionID": {
      "type": "string"
    },
    "policyName": {
      "type": "string"
    },
    "policyParameters": {
      "type": "object",
      "defaultValue": {}
    }
  },
  "variables": {},
  "resources": [
    {
      "type": "Microsoft.Authorization/policyAssignments",
      "apiVersion": "2018-03-01",
      "name": "[parameters('policyName')]",
      "properties": {
        "scope": "[subscription().id]",
        "policyDefinitionId": "[parameters('policyDefinitionID')]",
        "parameters": "[parameters('policyParameters')]"
      }
    }
  ]
}
```

Pour déployer cet exemple de modèle avec Azure CLI, utilisez la commande suivante :

```azurecli-interactive
# Built-in policy definition that accepts parameters
definition=$(az policy definition list --query "[?displayName=='Allowed locations'].id" --output tsv)

az deployment sub create \
  --name demoDeployment \
  --location centralus \
  --template-uri "https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/policyassign.json" \
  --parameters policyDefinitionID=$definition policyName=setLocation policyParameters="{'listOfAllowedLocations': {'value': ['westus']} }"
```

Pour déployer ce modèle avec PowerShell, utilisez :

```azurepowershell-interactive
$definition = Get-AzPolicyDefinition | Where-Object { $_.Properties.DisplayName -eq 'Allowed locations' }

$locations = @("westus", "westus2")
$policyParams =@{listOfAllowedLocations = @{ value = $locations}}

New-AzSubscriptionDeployment `
  -Name policyassign `
  -Location centralus `
  -TemplateUri "https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/policyassign.json" `
  -policyDefinitionID $definition.PolicyDefinitionId `
  -policyName setLocation `
  -policyParameters $policyParams
```

### <a name="create-and-assign-policy-definitions"></a>Créer et attribuer des définitions de stratégie

Vous pouvez [définir](../../governance/policy/concepts/definition-structure.md) et attribuer une définition de stratégie dans le même modèle.

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2018-05-01/subscriptionDeploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {},
  "variables": {},
  "resources": [
    {
      "type": "Microsoft.Authorization/policyDefinitions",
      "apiVersion": "2018-05-01",
      "name": "locationpolicy",
      "properties": {
        "policyType": "Custom",
        "parameters": {},
        "policyRule": {
          "if": {
            "field": "location",
            "equals": "northeurope"
          },
          "then": {
            "effect": "deny"
          }
        }
      }
    },
    {
      "type": "Microsoft.Authorization/policyAssignments",
      "apiVersion": "2018-05-01",
      "name": "location-lock",
      "dependsOn": [
        "locationpolicy"
      ],
      "properties": {
        "scope": "[subscription().id]",
        "policyDefinitionId": "[subscriptionResourceId('Microsoft.Authorization/policyDefinitions', 'locationpolicy')]"
      }
    }
  ]
}
```

Pour créer la définition de stratégie dans votre abonnement et l’attribuer à l’abonnement, utilisez la commande CLI suivante :

```azurecli
az deployment sub create \
  --name demoDeployment \
  --location centralus \
  --template-uri "https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/policydefineandassign.json"
```

Pour déployer ce modèle avec PowerShell, utilisez :

```azurepowershell
New-AzSubscriptionDeployment `
  -Name definePolicy `
  -Location centralus `
  -TemplateUri "https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/policydefineandassign.json"
```

## <a name="azure-blueprints"></a>Azure Blueprints

### <a name="create-blueprint-definition"></a>Créer une définition de blueprint

Vous pouvez [créer](../../governance/blueprints/tutorials/create-from-sample.md) une définition de blueprint à partir d’un modèle.

:::code language="json" source="~/quickstart-templates/subscription-deployments/blueprints-new-blueprint/azuredeploy.json":::

Pour créer la définition de blueprint dans votre abonnement, utilisez la commande CLI suivante :

```azurecli
az deployment sub create \
  --name demoDeployment \
  --location centralus \
  --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/subscription-deployments/blueprints-new-blueprint/azuredeploy.json"
```

Pour déployer ce modèle avec PowerShell, utilisez :

```azurepowershell
New-AzSubscriptionDeployment `
  -Name demoDeployment `
  -Location centralus `
  -TemplateUri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/subscription-deployments/blueprints-new-blueprint/azuredeploy.json"
```

## <a name="access-control"></a>Contrôle d’accès

Pour en savoir plus sur l’attribution de rôles, consultez [Ajouter des attributions de rôle Azure à l’aide de modèles Resource Manager](../../role-based-access-control/role-assignments-template.md).

L’exemple suivant crée un groupe de ressources, lui applique un verrou et attribue un rôle à un principal.

:::code language="json" source="~/quickstart-templates/subscription-deployments/create-rg-lock-role-assignment/azuredeploy.json":::

## <a name="next-steps"></a>Étapes suivantes

* Pour obtenir un exemple de déploiement des paramètres d’espace de travail pour Azure Security Center, consultez [deployASCwithWorkspaceSettings.json](https://github.com/krnese/AzureDeploy/blob/master/ARM/deployments/deployASCwithWorkspaceSettings.json).
* Vous trouverez des exemples de modèles dans [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/subscription-deployments).
* Vous pouvez également déployer des modèles au [niveau du groupe de gestion](deploy-to-management-group.md) et au [niveau du locataire](deploy-to-tenant.md).
