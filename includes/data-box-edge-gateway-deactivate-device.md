---
author: alkohli
ms.service: databox
ms.topic: include
ms.date: 03/05/2019
ms.author: alkohli
ms.openlocfilehash: 21c19027d21a87e199d74644cfc5c8f3cd52ba4c
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2020
ms.locfileid: "79129617"
---
Pour réinitialiser votre appareil, vous devez effacer en toute sécurité toutes les données sur le disque de données et le disque de démarrage de votre appareil. 

Utilisez la cmdlet `Reset-HcsAppliance` pour effacer les disques de données et le disque de démarrage ou simplement les disques de données. Les commutateurs `ClearData` et `BootDisk` permettent respectivement de réinitialiser les disques de données et le disque de démarrage.

Le commutateur `BootDisk` efface le disque de démarrage et rend l’appareil inutilisable. Il doit être utilisé seulement si l’appareil doit être renvoyé à Microsoft. Pour plus d’informations, consultez [Renvoyer l’appareil à Microsoft](https://docs.microsoft.com/azure/databox-online/data-box-edge-return-device).

Si vous utilisez la réinitialisation d’appareil dans l’interface utilisateur web locale, seuls les disques de données sont effacés en toute sécurité, mais le disque de démarrage reste intact. Le disque de démarrage contient la configuration de l’appareil.

1. [Connectez-vous à l’interface PowerShell](#connect-to-the-powershell-interface).
2. À l’invite de commandes, tapez :

    `Reset-HcsAppliance -ClearData -BootDisk`

    L’exemple suivant explique comment utiliser cette cmdlet :

    ```powershell
    [10.128.24.33]: PS>Reset-HcsAppliance -ClearData -BootDisk

    Confirm
    Are you sure you want to perform this action?
    Performing the operation "Reset-HcsAppliance" on target "ShouldProcess appliance".
    [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [?] Help (default is "Y"): N
    ```
