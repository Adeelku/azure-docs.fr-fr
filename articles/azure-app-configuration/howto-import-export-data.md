---
title: Importer ou exporter des données avec Azure App Configuration
description: Découvrez comment exporter ou importer des données de configuration vers ou depuis Azure App Configuration. Échangez des données entre votre magasin App Configuration et votre projet de code.
services: azure-app-configuration
author: lisaguthrie
ms.service: azure-app-configuration
ms.topic: conceptual
ms.date: 02/25/2020
ms.author: lcozzens
ms.openlocfilehash: 0e127a11f3821325602a78d46c69b2330bfb8293
ms.sourcegitcommit: a92fbc09b859941ed64128db6ff72b7a7bcec6ab
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/15/2020
ms.locfileid: "92074615"
---
# <a name="import-or-export-configuration-data"></a>Importer ou exporter des données de configuration

Azure App Configuration prend en charge les opérations d’importation et d’exportation de données. Ces opérations vous permettent d’utiliser des données de configuration en bloc et d’échanger des données entre votre magasin App Configuration et le projet de code. Par exemple, vous pouvez configurer un magasin App Configuration à des fins de test et un autre pour la production. Vous pouvez copier les paramètres d’application pour ne pas avoir à entrer deux fois les mêmes données.

Cet article fournit un guide pour importer et exporter des données avec App Configuration. Si vous souhaitez configurer une synchronisation continue avec votre référentiel GitHub, consultez [GitHub Actions](./concept-github-action.md).

## <a name="import-data"></a>Importer des données

L’importation a pour effet d’acheminer les données de configuration d’une source existante vers un magasin App Configuration. Utilisez la fonction d’importation pour migrer des données dans un magasin App Configuration ou agréger des données issues de plusieurs sources. App Configuration prend en charge l’importation à partir d’un fichier JSON, YAML ou de propriétés.

Importez les données à partir du [portail Azure](https://portal.azure.com) ou d’[Azure CLI](./scripts/cli-import.md). Sur le portail Azure, procédez comme suit :

1. Accédez à votre magasin App Configuration et sélectionnez **Importer/Exporter** dans le menu **Opérations**.

1. Sous l’onglet **Importation**, sélectionnez **Service source** > **Fichier config**.

1. Sélectionnez **Pour la langue**, puis sélectionnez le type d’entrée souhaité.

1. Sélectionnez l’icône **Dossier**, puis accédez au fichier à importer.

    ![Importer un fichier](./media/import-file.png)

1. Sélectionnez un **Séparateur** et entrez éventuellement le **Préfixe** à utiliser pour les noms de clés importées.

1. Si vous le souhaitez, sélectionnez une **Étiquette**.

1. Sélectionnez **Appliquer** pour terminer l’importation.

    ![Importation de fichier terminée](./media/import-file-complete.png)

## <a name="export-data"></a>Exporter des données

L’exportation a pour effet d’écrire les données de configuration stockées dans App Configuration dans une autre destination. Utilisez la fonction d’exportation, par exemple, pour enregistrer des données d’un magasin App Configuration vers un fichier incorporé à votre code d’application pendant le déploiement.

Exportez les données à partir du [portail Azure](https://portal.azure.com) ou d’[Azure CLI](./scripts/cli-export.md). Sur le portail Azure, procédez comme suit :

1. Accédez à votre magasin App Configuration et sélectionnez **Importer/Exporter**.

1. Sous l’onglet **Export**, sélectionnez **Service cible** > **Fichier config**.

1. Entrez éventuellement un **Préfixe**, puis sélectionnez une **Étiquette** et un point dans le temps pour les clés à exporter.

1. Sélectionnez un **Type de fichier** > **Séparateur**.

1. Sélectionnez **Appliquer** pour terminer l’exportation.

    ![Exportation de fichier terminée](./media/export-file-complete.png)

## <a name="next-steps"></a>Étapes suivantes

> [!div class="nextstepaction"]
> [Créez une application web ASP.NET Core](./quickstart-aspnet-core-app.md)