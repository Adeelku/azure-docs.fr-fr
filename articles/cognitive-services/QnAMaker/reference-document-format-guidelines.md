---
title: Instructions relatives au format des documents importés – QnA Maker
description: Suivez ces instructions pour l’importation de documents afin d’obtenir les meilleurs résultats pour votre contenu.
ms.service: cognitive-services
ms.subservice: qna-maker
ms.topic: reference
ms.date: 04/06/2020
ms.openlocfilehash: d35ea57a68e500deffa99033b83114ec518dd5e3
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91776729"
---
# <a name="format-guidelines-for-imported-documents-and-urls"></a>Instructions relatives au format pour les documents et les URL importés

Passez en revue ces instructions de mise en forme afin d’obtenir les meilleurs résultats pour votre contenu.

## <a name="formatting-considerations"></a>Mise en forme - Éléments à prendre en compte

Après l’importation d’un fichier ou d’une URL, QnA Maker convertit et stocke votre contenu dans le [format Markdown](https://en.wikipedia.org/wiki/Markdown). Le processus de conversion ajoute de nouvelles lignes dans le texte, telles que `\n\n`. Une connaissance du format Markdown vous aide à comprendre le contenu converti et à gérer le contenu de votre base de connaissances.

Si vous ajoutez ou modifiez votre contenu directement dans votre base de connaissances, utilisez la **mise en forme Markdown** pour créer un contenu de texte enrichi ou modifiez le contenu du format Markdown qui est déjà dans la réponse. QnA Maker prend en charge une grande partie du format Markdown pour offrir des fonctionnalités de texte enrichi à votre contenu. Toutefois, l’application cliente, telle qu’un bot de chat, peut ne pas prendre en charge le même ensemble de formats Markdown. Il est important de tester l’affichage des réponses de l’application cliente.

Consultez la liste complète des [types et exemples de contenu](./Concepts/content-types.md#file-and-url-data-types).

## <a name="basic-document-formatting"></a>Mise en forme de base du document

QnA Maker identifie les sections, sous-sections et relations dans le fichier en fonction d’indices visuels, notamment :

* la taille de police
* le style de police
* la numérotation
* les couleurs

## <a name="product-manuals"></a>Manuels de produit

Un manuel comprend habituellement des supports d’orientation qui accompagnent un produit. Il aide l’utilisateur à configurer, utiliser, gérer et dépanner le produit. Lorsque QnA Maker traite un manuel, il extrait les titres et les sous-titres sous forme de questions et le contenu qui suit sous forme de réponses. Un exemple vous est proposé [ici](https://download.microsoft.com/download/2/9/B/29B20383-302C-4517-A006-B0186F04BE28/surface-pro-4-user-guide-EN.pdf).

Voici un exemple de manuel avec une page d’index et du contenu hiérarchique

 ![Exemple de manuel de produit pour une base de connaissances](./media/qnamaker-concepts-datasources/product-manual.png)

> [!NOTE]
> L’extraction est plus efficace sur les manuels qui ont une table des matières et/ou une page d’index, mais aussi une structure clairement définie avec des en-têtes hiérarchiques.

## <a name="brochures-guidelines-papers-and-other-files"></a>Brochures, instructions, livres blancs et autres fichiers

De nombreux autres types de documents peuvent également être traités pour générer des paires de questions-réponses, à condition qu’ils aient une structure et une disposition claires. notamment : brochures, instructions, rapports, livres blancs, articles scientifiques, stratégies, ouvrages, etc. Un exemple vous est proposé [ici](https://qnamakerstore.blob.core.windows.net/qnamakerdata/docs/Manage%20Azure%20Blob%20Storage.docx).

Voici un exemple de document semi-structuré, sans index :

 ![Document semi-structuré de Stockage d’objets blob Azure](./media/qnamaker-concepts-datasources/semi-structured-doc.png)

## <a name="structured-qna-document"></a>Document QnA structuré

Le format des questions-réponses structurées dans les fichiers DOC consiste à alterner les questions et les réponses ligne par ligne, une question sur une ligne suivie de sa réponse sur la ligne suivante, comme indiqué ci-dessous :

```text
Question1

Answer1

Question2

Answer2
```

Voici un exemple de document Word QnA structuré :

 ![Exemple de document QnA structuré pour une base de connaissances](./media/qnamaker-concepts-datasources/structured-qna-doc.png)

## <a name="structured-txt-tsv-and-xls-files"></a>Fichiers *TXT*, *TSV* et *XLS* structurés

Les QnA sous forme de fichiers *.txt*, *.tsv* ou *.xls* structurés peuvent également être chargés vers QnA Maker pour créer ou augmenter une base de connaissances.  Il peuvent être en texte brut, ou peuvent avoir du contenu au format RTF ou HTML.

| Question  | Réponse  | Métadonnées (1 clé : 1 valeur) |
|-----------|---------|-------------------------|
| Question1 | Réponse1 | <code>Key1:Value1 &#124; Key2:Value2</code> |
| Question2 | Réponse2 |      `Key:Value`           |

Toutes les autres colonnes du fichier source sont ignorées.

### <a name="example-of-structured-excel-file"></a>Exemple de fichier Excel structuré

Voici un exemple de fichier *.xls* QnA structuré, avec du contenu HTML :

 ![Exemple de feuille Excel QnA structurée pour une base de connaissances](./media/qnamaker-concepts-datasources/structured-qna-xls.png)

### <a name="example-of-alternate-questions-for-single-answer-in-excel-file"></a>Exemple de questions multiples avec réponse unique dans un fichier Excel

Voici un exemple de fichier *.xls* QnA structuré, avec plusieurs questions pour une réponse unique :

 ![Exemple de questions multiples avec réponse unique dans un fichier Excel](./media/qnamaker-concepts-datasources/xls-alternate-question-example.png)

Une fois le fichier importé, la paire question-réponse figure dans la base de connaissances, comme indiqué ci-dessous :

 ![Capture d’écran de questions multiples avec réponse unique importées dans la base de connaissances](./media/qnamaker-concepts-datasources/xls-alternate-question-example-after-import.png)

## <a name="structured-data-format-through-import"></a>Format de données structurées via l’importation

L’importation d’une base de connaissances remplace le contenu de la base de connaissances existante. L’importation nécessite un fichier .tsv structuré qui contient des informations sur la source de données. Ces informations aident QnA Maker à regrouper les paires de question-réponse et à les attribuer à une source de données en particulier.

| Question  | Réponse  | Source| Métadonnées (1 clé : 1 valeur) |
|-----------|---------|----|---------------------|
| Question1 | Réponse1 | Url1 | <code>Key1:Value1 &#124; Key2:Value2</code> |
| Question2 | Réponse2 | Éditorial|    `Key:Value`       |

<a href="#formatting-considerations"></a>

## <a name="multi-turn-document-formatting"></a>Mise en forme multitour du document

* Utilisez des titres et sous-titres pour montrer la hiérarchie. Par exemple, vous pouvez H1 pour dénoter la QnA parente et H2 pour dénoter la QnA à considérer comme invite. Utilisez une petite taille de titre pour dénoter la hiérarchie suivante. N’utilisez pas de style, de couleur ou d’autre mécanisme pour montrer la structure de votre document. QnA Maker n’extrait pas les invites multitours.
* Le premier caractère de l’en-tête doit être en majuscule.
* Ne pas terminer un titre par un point d’interrogation (`?`).

**Exemples de documents** :<br>[Surface Pro (docx)](https://github.com/Azure-Samples/cognitive-services-sample-data-files/blob/master/qna-maker/data-source-formats/multi-turn.docx)<br>[Contoso Benefits (docx)](https://github.com/Azure-Samples/cognitive-services-sample-data-files/blob/master/qna-maker/data-source-formats/Multiturn-ContosoBenefits.docx)<br>[Contoso Benefits (pdf)](https://github.com/Azure-Samples/cognitive-services-sample-data-files/blob/master/qna-maker/data-source-formats/Multiturn-ContosoBenefits.pdf)

## <a name="next-steps"></a>Étapes suivantes

Consultez la liste complète des [types et exemples de contenu](./Concepts/content-types.md#file-and-url-data-types)