---
title: Format ORC dans Azure Data Factory
description: Cette rubrique décrit comment traiter le format ORC dans Azure Data Factory.
author: linda33wj
manager: shwang
ms.reviewer: craigg
ms.service: data-factory
ms.workload: data-services
ms.topic: conceptual
ms.date: 09/15/2020
ms.author: jingwang
ms.openlocfilehash: 3aa42d6060ecdd93dd97438a025c4f5e4f05ac52
ms.sourcegitcommit: 03662d76a816e98cfc85462cbe9705f6890ed638
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90531727"
---
# <a name="orc-format-in-azure-data-factory"></a>Format ORC dans Azure Data Factory

[!INCLUDE[appliesto-adf-asa-md](includes/appliesto-adf-asa-md.md)]

Suivez cet article si vous souhaitez **analyser des fichiers ORC ou écrire des données au format ORC**. 

Le format ORC est pris en charge pour les connecteurs suivants : [Amazon S3](connector-amazon-simple-storage-service.md), [Azure Blob](connector-azure-blob-storage.md), [Azure Data Lake Storage Gen1](connector-azure-data-lake-store.md), [Azure Data Lake Storage Gen2](connector-azure-data-lake-storage.md), [Azure File Storage](connector-azure-file-storage.md), [Système de fichiers](connector-file-system.md), [FTP](connector-ftp.md), [Google Cloud Storage](connector-google-cloud-storage.md), [HDFS](connector-hdfs.md), [HTTP](connector-http.md) et [SFTP](connector-sftp.md).

## <a name="dataset-properties"></a>Propriétés du jeu de données

Pour obtenir la liste complète des sections et propriétés disponibles pour la définition de jeux de données, consultez l’article [Jeux de données](concepts-datasets-linked-services.md). Cette section fournit la liste des propriétés prises en charge par le jeu de données ORC.

| Propriété         | Description                                                  | Obligatoire |
| ---------------- | ------------------------------------------------------------ | -------- |
| type             | La propriété type du jeu de données doit être définie sur **Orc**. | Oui      |
| location         | Paramètres d’emplacement du ou des fichiers. Chaque connecteur basé sur un fichier possède ses propres type d’emplacement et propriétés prises en charge sous `location`. **Consultez les détails dans l’article du connecteur -> section des propriétés du jeu de données**. | Oui      |

Voici un exemple de jeu de données ORC sur Stockage Blob Azure :

```json
{
    "name": "ORCDataset",
    "properties": {
        "type": "Orc",
        "linkedServiceName": {
            "referenceName": "<Azure Blob Storage linked service name>",
            "type": "LinkedServiceReference"
        },
        "schema": [ < physical schema, optional, retrievable during authoring > ],
        "typeProperties": {
            "location": {
                "type": "AzureBlobStorageLocation",
                "container": "containername",
                "folderPath": "folder/subfolder",
            }
        }
    }
}
```

Notez les points suivants :

* Les types de données complexes ne sont pas pris en charge (STRUCT, MAP, LIST, UNION).
* Les espaces blancs dans le nom de colonne ne sont pas pris en charge.
* Le fichier ORC a trois [options liées à la compression](https://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/) : NONE, ZLIB, SNAPPY. Data Factory prend en charge la lecture des données du fichier ORC dans tous ces formats compressés. Il utilise le codec de compression se trouvant dans les métadonnées pour lire les données. Toutefois, lors de l’écriture dans un fichier ORC, Data Factory choisit ZLIB, qui est la valeur par défaut pour ORC. Actuellement, il n’existe aucune option permettant de remplacer ce comportement.

## <a name="copy-activity-properties"></a>Propriétés de l’activité de copie

Pour obtenir la liste complète des sections et des propriétés disponibles pour la définition des activités, consultez l’article [Pipelines](concepts-pipelines-activities.md). Cette section fournit la liste des propriétés prises en charge par la source et le récepteur ORC.

### <a name="orc-as-source"></a>ORC en tant que source

Les propriétés prises en charge dans la section ***\*source\**** de l’activité de copie sont les suivantes.

| Propriété      | Description                                                  | Obligatoire |
| ------------- | ------------------------------------------------------------ | -------- |
| type          | La propriété type de la source d’activité de copie doit être définie sur **OrcSource**. | Oui      |
| storeSettings | Un groupe de propriétés sur la façon de lire les données d’un magasin de données. Chaque connecteur basé sur un fichier possède ses propres paramètres de lecture pris en charge sous `storeSettings`. **Consultez les détails dans l’article du connecteur -> section des propriétés de l’activité de copie**. | Non       |

### <a name="orc-as-sink"></a>ORC en tant que récepteur

Les propriétés prises en charge dans la section ***\*récepteur\**** de l’activité de copie sont les suivantes.

| Propriété      | Description                                                  | Obligatoire |
| ------------- | ------------------------------------------------------------ | -------- |
| type          | La propriété type de la source d’activité de copie doit être définie sur **OrcSink**. | Oui      |
| formatSettings | Un groupe de propriétés. Reportez-vous au tableau **Paramètres d’écriture ORC** ci-dessous. |    Non      |
| storeSettings | Groupe de propriétés sur la méthode d’écriture de données dans un magasin de données. Chaque connecteur basé sur un fichier possède ses propres paramètres d’écriture pris en charge sous `storeSettings`. **Consultez les détails dans l’article du connecteur -> section des propriétés de l’activité de copie**. | Non       |

**Paramètres d’écriture ORC** pris en charge sous `formatSettings` :

| Propriété      | Description                                                  | Obligatoire                                              |
| ------------- | ------------------------------------------------------------ | ----------------------------------------------------- |
| type          | Le type de formatSettings doit être défini sur **OrcWriteSettings**. | Oui                                                   |
| maxRowsPerFile | Lorsque vous écrivez des données dans un dossier, vous pouvez choisir d’écrire dans plusieurs fichiers et de spécifier le nombre maximal de lignes par fichier.  | Non |
| fileNamePrefix | Applicable lorsque `maxRowsPerFile` est configuré.<br> Spécifiez le préfixe du nom de fichier lors de l’écriture de données dans plusieurs fichiers, ce qui a généré ce modèle : `<fileNamePrefix>_00000.<fileExtension>`. S’il n’est pas spécifié, le préfixe du nom de fichier est généré automatiquement. Cette propriété ne s’applique pas lorsque la source est un magasin basé sur des fichiers ou un [magasin de données partition-option-enabled](copy-activity-performance-features.md).  | Non |

## <a name="using-self-hosted-integration-runtime"></a>Utilisation du runtime d’intégration auto-hébergé

> [!IMPORTANT]
> Dans le cas de copies permises par le runtime d’intégration auto-hébergé, par exemple entre des magasins de données locaux et cloud, si vous ne copiez pas les fichiers ORC **tels quels**, vous devez installer **JRE 8 (Java Runtime Environment) 64 bits ou OpenJDK** et le **package redistribuable Microsoft Visual C++ 2010** sur votre machine de runtime d’intégration. Pour plus de détails, consultez le paragraphe suivant.

Dans le cas de copies s’exécutant sur l’IR auto-hébergé avec sérialisation/désérialisation des fichiers ORC, ADF localise le runtime Java en vérifiant d’abord le registre *`(SOFTWARE\JavaSoft\Java Runtime Environment\{Current Version}\JavaHome)`* pour JRE puis, s’il ne le trouve pas, en vérifiant la variable système *`JAVA_HOME`* pour OpenJDK.

- **Pour utiliser JRE** : Le runtime d’intégration de 64 bits requiert la version 64 bits de JRE. Vous pouvez la récupérer [ici](https://go.microsoft.com/fwlink/?LinkId=808605).
- **Pour utiliser OpenJDK** : il est pris en charge à compter de la version 3.13 du runtime d’intégration. Empaquetez jvm.dll avec tous les autres assemblys requis d’OpenJDK dans la machine d’IR auto-hébergé et définissez la variable d’environnement système JAVA_HOME en conséquence.
- **Pour installer le package redistribuable Visual C++ 2010** : Le package redistribuable Visual C++ 2010 n’est pas installé avec les installations du runtime d’intégration auto-hébergé. Vous pouvez la récupérer [ici](https://www.microsoft.com/download/details.aspx?id=14632).

> [!TIP]
> Si, en copiant des données au format ORC avec le runtime d’intégration auto-hébergé, vous obtenez une erreur indiquant « An error occurred when invoking java, message: **java.lang.OutOfMemoryError:Java heap space** », vous pouvez ajouter une variable d’environnement `_JAVA_OPTIONS` sur l’ordinateur qui héberge le runtime d’intégration auto-hébergé afin d’ajuster la taille de segment de mémoire minimale/maximale nécessaire pour que la machine virtuelle Java puisse effectuer une copie de ce type, puis réexécuter le pipeline.

![Définir la taille de segment de mémoire JVM sur le runtime d’intégration auto-hébergé](./media/supported-file-formats-and-compression-codecs/set-jvm-heap-size-on-selfhosted-ir.png)

Exemple : donnez la valeur `-Xms256m -Xmx16g` à la variable `_JAVA_OPTIONS`. L’indicateur `Xms` spécifie le pool d’allocation de mémoire initial pour une Machine virtuelle Java (JVM), tandis que `Xmx` spécifie le pool d’allocation de mémoire maximal. En d’autres termes, JVM démarrera avec la quantité de mémoire `Xms` et pourra au maximum utiliser la quantité de mémoire `Xmx`. Par défaut, ADF utilise au minimum 64 Mo et au maximum 1 Go.

## <a name="next-steps"></a>Étapes suivantes

- [Vue d’ensemble des activités de copie](copy-activity-overview.md)
- [Activité de recherche](control-flow-lookup-activity.md)
- [Activité GetMetadata](control-flow-get-metadata-activity.md)
