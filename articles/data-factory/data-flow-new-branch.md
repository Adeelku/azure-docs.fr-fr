---
title: Plusieurs branches dans le flux de données de mappage
description: Réplication de flux de données dans le flux de données de mappage avec plusieurs branches
author: kromerm
ms.author: makromer
ms.reviewer: douglasl
ms.service: data-factory
ms.topic: conceptual
ms.custom: seo-lt-2019; seo-dt-2019
ms.date: 01/08/2020
ms.openlocfilehash: daebd6a4a00d82706ceda68f94736f21b8fe5a84
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2020
ms.locfileid: "81606390"
---
# <a name="creating-a-new-branch-in-mapping-data-flow"></a>Création d’une nouvelle branche dans le flux de données de mappage

[!INCLUDE[appliesto-adf-asa-md](includes/appliesto-adf-asa-md.md)]

Ajoutez une nouvelle branche pour effectuer plusieurs ensembles d’opérations et de transformations sur le même flux de données. L’ajout d’une nouvelle branche est utile lorsque vous souhaitez utiliser la même source pour plusieurs récepteurs ou pour effectuer la jointure réflexive des données.

Une nouvelle branche peut être ajoutée à partir de la liste des transformations de la même façon que d’autres transformations. L’action **Nouvelle branche** est disponible uniquement lorsqu’une transformation existante suit la transformation pour laquelle vous tentez de créer une branche.

![Ajout d’une nouvelle branche](media/data-flow/new-branch2.png "Ajout d’une nouvelle branche")

Dans l’exemple ci-dessous, le flux de données lit des données de trajet en taxi. La sortie agrégée par jour et par fournisseur est requise. Au lieu de créer deux flux de données distincts qui lisent à partir de la même source, il est possible d’ajouter une nouvelle branche. De cette façon, les deux agrégations peuvent être exécutées dans le cadre du même flux de données. 

![Ajout d’une nouvelle branche](media/data-flow/new-branch.png "Ajout d’une nouvelle branche")
