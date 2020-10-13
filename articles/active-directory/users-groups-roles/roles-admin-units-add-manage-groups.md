---
title: Ajouter, supprimer et répertorier des groupes dans une unité administrative – Azure Active Directory | Microsoft Docs
description: Gérer les groupes et leurs autorisations de rôles dans une unité administrative dans Azure Active Directory
services: active-directory
documentationcenter: ''
author: curtand
manager: daveba
ms.service: active-directory
ms.topic: how-to
ms.subservice: users-groups-roles
ms.workload: identity
ms.date: 10/07/2020
ms.author: curtand
ms.reviewer: anandy
ms.custom: oldportal;it-pro;
ms.collection: M365-identity-device-management
ms.openlocfilehash: 133ea21bf7a7c1df0fccaeacce7d7a29199c033d
ms.sourcegitcommit: d2222681e14700bdd65baef97de223fa91c22c55
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/07/2020
ms.locfileid: "91827671"
---
# <a name="add-and-manage-groups-in-administrative-units-in-azure-active-directory"></a>Ajouter et gérer des groupes dans des unités administratives dans Azure Active Directory

Dans Azure Active Directory (Azure AD), vous pouvez ajouter des groupes à une unité administrative pour obtenir une étendue administrative de contrôle plus précise.

Pour connaître les étapes de préparation à l’utilisation de PowerShell et de Microsoft Graph pour la gestion des unités administratives, consultez [Prise en main](roles-admin-units-manage.md#get-started).

## <a name="add-groups-to-an-au"></a>Ajouter des groupes à une unité administrative

### <a name="azure-portal"></a>Portail Azure

Vous ne pouvez affecter des groupes à une unité administrative qu’individuellement. Il n’existe aucune option d’affectation de groupes en bloc à une unité administrative. Vous pouvez affecter un groupe à une unité administrative de deux façons via le portail :

1. À partir de la page **Azure AD > Groupes**

    Ouvrez la page de vue d’ensemble Groupes dans Azure AD, puis sélectionnez le groupe à affecter à l’unité administrative. Sur le côté gauche, sélectionnez **Unités administratives** pour répertorier les unités administratives auxquelles le groupe est affecté. Lorsque vous cliquez sur l’option Affecter à une unité administrative en haut de la page, un panneau s’affiche à droite, dans lequel vous pouvez choisir l’unité administrative.

    ![affecter un groupe individuellement à une unité administrative](./media/roles-admin-units-add-manage-groups/assign-to-group-1.png)

1. À partir de la page **Azure AD > Unités administratives > Tous les groupes**

    Ouvrez le panneau Tous les groupes dans Azure AD > Unités administratives. Si des groupes sont déjà affectés à l’unité administrative, ils sont affichés sur le côté droit. Sélectionnez **Ajouter** en haut et un volet droit pour afficher la liste des groupes disponibles dans votre organisation Azure AD. Sélectionnez un ou plusieurs groupes à affecter aux unités administratives.

    ![sélectionner une unité administrative, puis choisir Ajouter un membre](./media/roles-admin-units-add-manage-groups/assign-to-admin-unit.png)

### <a name="powershell"></a>PowerShell

```powershell
$administrative unitObj = Get-AzureADMSAdministrativeUnit -Filter "displayname eq 'Test administrative unit 2'"
$GroupObj = Get-AzureADGroup -Filter "displayname eq 'TestGroup'"
Add-AzureADMSAdministrativeUnitMember -ObjectId $administrative unitObj.ObjectId -RefObjectId $GroupObj.ObjectId
```

Dans cet exemple, la cmdlet Add-AzureADMSAdministrativeUnitMember est utilisée pour ajouter le groupe à l’unité administrative. L’ID d’objet de l’unité administrative et l’ID d’objet du groupe à ajouter sont utilisés en tant qu’argument. Il est possible de modifier la section en surbrillance selon les besoins de l’environnement spécifique.

### <a name="microsoft-graph"></a>Microsoft Graph

```http
Http request
POST /administrativeUnits/{Admin Unit id}/members/$ref

Request body
{
"@odata.id":"https://graph.microsoft.com/v1.0/groups/{id}"
}
```

Exemple :

```http
{
"@odata.id":"https://graph.microsoft.com/v1.0/groups/ 871d21ab-6b4e-4d56-b257-ba27827628f3"
}
```

## <a name="list-groups-in-an-au"></a>Répertorier les groupes dans une unité administrative

### <a name="azure-portal"></a>Portail Azure

Accédez à **Azure AD > Unités administratives** dans le portail. Sélectionnez l’unité administrative dont vous souhaitez répertorier les utilisateurs. Par défaut, **Tous les utilisateurs** est déjà sélectionné dans le volet gauche. Sélectionnez **Tous les groupes** pour afficher, à droite, la liste des groupes membres de l’unité administrative sélectionnée.

![Répertorier les groupes dans une unité administrative](./media/roles-admin-units-add-manage-groups/list-groups-in-admin-units.png)

### <a name="powershell"></a>PowerShell

```powershell
$administrative unitObj = Get-AzureADMSAdministrativeUnit -Filter "displayname eq 'Test administrative unit 2'"
Get-AzureADMSAdministrativeUnitMember -ObjectId $administrative unitObj.ObjectId
```

Cela vous permet d’obtenir tous les membres de l’unité administrative. Si vous souhaitez afficher tous les groupes membres de l’unité administrative, vous pouvez utiliser l’extrait de code ci-dessous :

```http
foreach ($member in (Get-AzureADMSAdministrativeUnitMember -ObjectId $administrative unitObj.ObjectId)) 
{
if($member.ObjectType -eq "Group")
{
Get-AzureADGroup -ObjectId $member.ObjectId
}
}
```

### <a name="microsoft-graph"></a>Microsoft Graph

```http
HTTP request
GET /directory/administrativeUnits/{Admin id}/members/$/microsoft.graph.group
Request body
{}
```

## <a name="list-aus-for-a-group"></a>Répertorier les unités administratives pour un groupe

### <a name="azure-portal"></a>Portail Azure

Dans le portail Azure AD, vous pouvez afficher les détails d’un groupe en ouvrant **Groupes**. Sélectionnez un groupe pour ouvrir son profil. Sélectionnez **Unités administratives** pour répertorier toutes les unités administratives dont le groupe est membre.

![Répertorier les unités administratives pour un groupe](./media/roles-admin-units-add-manage-groups/list-group-au.png)

### <a name="powershell"></a>PowerShell

```powershell
Get-AzureADMSAdministrativeUnit | where { Get-AzureADMSAdministrativeUnitMember -ObjectId $_.ObjectId | where {$_.ObjectId -eq $groupObjId} }
```

### <a name="microsoft-graph"></a>Microsoft Graph

```http
https://graph.microsoft.com/v1.0/groups/<group-id>/memberOf/$/Microsoft.Graph.AdministrativeUnit
```

## <a name="remove-a-group-from-an-au"></a>Supprimer un groupe d’une unité administrative

### <a name="azure-portal"></a>Portail Azure

Il existe deux façons de supprimer un groupe d’une unité administrative dans le portail Azure.

- Supprimer d’une vue d’ensemble d’un groupe

  1. Ouvrez **Azure AD** > **Groupes**, puis ouvrez le profil du groupe à supprimer d’une unité administrative.
  1. Dans le volet gauche, sélectionnez **Unités administratives** pour répertorier toutes les unités administratives dont le groupe est membre. Sélectionnez l’unité administrative dont vous souhaitez supprimer le groupe, puis sélectionnez **Supprimer de l’unité administrative**.

    ![Supprimer un groupe d’une unité administrative](./media/roles-admin-units-add-manage-groups/group-au-remove.png)

- Supprimer d’une unité administrative

  1. Ouvrez **Azure AD** > **Unités administratives**, puis choisissez l’unité administrative dont le groupe est membre.
  1. Dans le volet gauche , sélectionnez **Groupes** pour afficher la liste des groupes membres.
  1. Sélectionnez le groupe à supprimer de l’unité administrative, puis choisissez **Supprimer les groupes**.

    ![Répertorier les groupes dans une unité administrative](./media/roles-admin-units-add-manage-groups/list-groups-in-admin-units.png)

### <a name="powershell"></a>PowerShell

```powershell
Remove-AzureADMSAdministrativeUnitMember -ObjectId $auId -MemberId $memberGroupObjId
```

### <a name="microsoft-graph"></a>Microsoft Graph

```http
https://graph.microsoft.com/v1.0/directory/AdministrativeUnits/<adminunit-id>/members/<group-id>/$ref
```

## <a name="next-steps"></a>Étapes suivantes

- [Affecter un rôle à une unité administrative](roles-admin-units-assign-roles.md)
- [Gérer les utilisateurs dans une unité administrative](roles-admin-units-add-manage-users.md)
