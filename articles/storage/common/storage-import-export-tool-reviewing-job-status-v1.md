---
title: Vérification de l’état des travaux Azure Import/Export - v1 | Microsoft Docs
description: Découvrez comment utiliser les fichiers journaux créés par le travail d’importation ou d’exportation pour connaître l’état du travail.
author: alkohli
services: storage
ms.service: storage
ms.topic: how-to
ms.date: 01/26/2017
ms.author: alkohli
ms.subservice: common
ms.openlocfilehash: 2fa5cfcf0cb6c20a8a0b64651da0b365e12a3d05
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2020
ms.locfileid: "90056320"
---
# <a name="reviewing-azure-importexport-job-status-with-copy-log-files"></a>Vérification de l’état des travaux Azure Import/Export avec les copies des fichiers journaux
Lorsque le service Microsoft Azure Import/Export traite les lecteurs associés à un travail d’importation ou d’exportation, il écrit les fichiers journaux de copie dans le compte de stockage utilisé pour importer ou exporter des objets blob. Le fichier journal contient l’état détaillé de chaque fichier importé ou exporté. Le service retourne l’URL de chaque fichier journal de copie lorsque vous interrogez l’état d’un travail terminé. Pour plus d’informations, consultez [Obtenir un travail](https://docs.microsoft.com/rest/api/storageimportexport/Jobs/Get).  

## <a name="example-urls"></a>Exemples d’URL

Voici des exemples d’URL de fichiers journaux de copie pour un travail d’importation avec deux lecteurs :  

 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM35C2V_20130921-034307-902_error.xml`  

 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM45A6Q_20130921-042122-021_error.xml`  

 Consultez la page [Format des fichiers journaux d’activité du Service Import-Export](../storage-import-export-file-format-log.md) pour connaître le format des journaux d’activité de copie et la liste complète des codes d’état.  

## <a name="next-steps"></a>Étapes suivantes

 * [Configuration de l’outil Azure Import/Export](storage-import-export-tool-setup-v1.md)   
 * [Préparation des disques durs pour un travail d’importation](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
 * [Réparation d’un travail d’importation](../storage-import-export-tool-repairing-an-import-job-v1.md)   
 * [Réparation d’un travail d’exportation](../storage-import-export-tool-repairing-an-export-job-v1.md)
