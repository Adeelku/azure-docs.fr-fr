---
title: Série HBv2 – Machines virtuelles Microsoft Azure
description: Spécifications pour les machines virtuelles de la série HBv2.
author: vermagit
ms.service: virtual-machines
ms.subservice: sizes
ms.topic: conceptual
ms.date: 09/08/2020
ms.author: amverma
ms.reviewer: jushiman
ms.openlocfilehash: bf6828ff96f5bff8a65b5f62793df8bf0e65a309
ms.sourcegitcommit: 1b320bc7863707a07e98644fbaed9faa0108da97
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/09/2020
ms.locfileid: "89595153"
---
# <a name="hbv2-series"></a>Série HBv2

Les machines virtuelles de la série HBv2 sont optimisées pour des applications tributaires de la bande passante mémoire, par exemple la dynamique des fluides, l’analyse par éléments finis et la simulation de réservoir. Les machines virtuelles HBv2 disposent de 120 cœurs de processeur AMD EPYC 7742, de 4 Go de RAM par cœur de processeur, et d’aucun multithreading simultané. Chaque machine virtuelle HBv2 fournit jusqu’à 340 Go/s de bande passante de mémoire et jusqu’à 4 téraflops de calcul FP64.

Les machines virtuelles d’origine de la série HBv2 sont dotées de la technologie Mellanox HDR InfiniBand à 200 Gb/s. Ces machines virtuelles sont connectées dans une arborescence FAT non bloquante pour des performances RDMA optimisées et cohérentes. Ces machines virtuelles prennent en charge le routage adaptatif et le transport connecté dynamique (DCT, en plus des transports RC et UD standards). Ces fonctionnalités améliorent les performances, l’extensibilité et la cohérence des applications, et leur utilisation est fortement recommandée.

Premium Storage : Prise en charge

Migration dynamique : Non pris en charge

Mises à jour avec préservation de la mémoire : Non pris en charge

| Taille | Processeurs virtuels | Processeur | Mémoire (Go) | Bande passante mémoire (Go/s) | Fréquence du processeur de base (GHz) | Fréquence de tous les cœurs (GHz, pic) | Fréquence d’un cœur (GHz, pic) | Performances RDMA (Gbit/s) | Prise en charge MPI | Stockage temporaire (Go) | Disques de données max. | Cartes réseau Ethernet max. |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Standard_HB120rs_v2 | 120 | AMD EPYC 7V12 | 480 | 350 | 2.45 | 3.1 | 3.3 | 200 | Tous | 480 + 960 | 8 | 1 |


[!INCLUDE [virtual-machines-common-sizes-table-defs](../../includes/virtual-machines-common-sizes-table-defs.md)]

## <a name="other-sizes"></a>Autres tailles

- [Usage général](sizes-general.md)
- [Mémoire optimisée](sizes-memory.md)
- [Optimisé pour le stockage](sizes-storage.md)
- [Optimisé pour le GPU](sizes-gpu.md)
- [Calcul haute performance](sizes-hpc.md)
- [Générations précédentes](sizes-previous-gen.md)

## <a name="next-steps"></a>Étapes suivantes

- En savoir plus sur [la configuration de vos machines virtuelles](./workloads/hpc/configure.md), [l’activation d’InfiniBand](./workloads/hpc/enable-infiniband.md), [la configuration de MPI](./workloads/hpc/setup-mpi.md) et l’optimisation des applications HPC pour Azure dans l’article relatif aux [charges de travail HPC](./workloads/hpc/overview.md).
- Découvrez des informations sur les dernières annonces et des exemples et des résultats HPC sur les [Blogs de la communauté Azure Compute Tech](https://techcommunity.microsoft.com/t5/azure-compute/bg-p/AzureCompute).
- Pour une vision plus globale de l’architecture d’exécution des charges de travail HPC, consultez [Calcul haute performance (HPC) sur Azure](/azure/architecture/topics/high-performance-computing/).
- Lisez-en davantage sur les [Unités de calcul Azure (ACU)](acu.md) pour découvrir comment comparer les performances de calcul entre les références Azure.
