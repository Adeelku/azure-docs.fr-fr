---
title: 'Langage de requête Azure Cosmos DB : ARRAY_CONTAINS'
description: Découvrez la fonction système SQL ARRAY_CONTAINS dans Azure Cosmos DB, qui retourne une valeur booléenne indiquant si le tableau contient la valeur spécifiée
author: ginamr
ms.service: cosmos-db
ms.topic: conceptual
ms.date: 09/13/2019
ms.author: girobins
ms.custom: query-reference
ms.openlocfilehash: 47fe20888aa546e414b268b30c2e03580750a040
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2020
ms.locfileid: "78303475"
---
# <a name="array_contains-azure-cosmos-db"></a>ARRAY_CONTAINS (Azure Cosmos DB)
Retourne une valeur booléenne qui indique si le tableau contient la valeur spécifiée. Vous pouvez rechercher une correspondance partielle ou totale d'un objet en utilisant une expression booléenne dans la commande. 

## <a name="syntax"></a>Syntaxe
  
```sql
ARRAY_CONTAINS (<arr_expr>, <expr> [, bool_expr])  
```  
  
## <a name="arguments"></a>Arguments
  
*arr_expr*  
   Est l’expression de tableau faisant l’objet de la recherche.  
  
*expr*  
   Est l’expression à rechercher.  

*bool_expr*  
   Est une expression booléenne. Si elle prend la valeur « true » et que la valeur de recherche spécifiée est un objet, la commande recherche une correspondance partielle (l’objet de la recherche est un sous-ensemble de l’un des objets). Si elle prend la valeur « false », la commande recherche une correspondance totale de tous les objets du tableau. Si elle n'est pas spécifiée, la valeur par défaut est « false ». 
  
## <a name="return-types"></a>Types de retour
  
  Retourne une valeur booléenne.  
  
## <a name="examples"></a>Exemples
  
  L’exemple suivant montre comment vérifier l’appartenance à un tableau avec `ARRAY_CONTAINS`.  
  
```sql
SELECT   
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "apples") AS b1,  
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "mangoes") AS b2  
```  
  
 Voici le jeu de résultats obtenu.  
  
```json
[{"b1": true, "b2": false}]  
```  

L’exemple suivant montre comment rechercher une correspondance partielle de JSON dans un tableau avec ARRAY_CONTAINS.  
  
```sql
SELECT  
    ARRAY_CONTAINS([{"name": "apples", "fresh": true}, {"name": "strawberries", "fresh": true}], {"name": "apples"}, true) AS b1, 
    ARRAY_CONTAINS([{"name": "apples", "fresh": true}, {"name": "strawberries", "fresh": true}], {"name": "apples"}) AS b2,
    ARRAY_CONTAINS([{"name": "apples", "fresh": true}, {"name": "strawberries", "fresh": true}], {"name": "mangoes"}, true) AS b3 
```  
  
 Voici le jeu de résultats obtenu.  
  
```json
[{
  "b1": true,
  "b2": false,
  "b3": false
}]
```

## <a name="remarks"></a>Notes

Cette fonction système bénéficiera d’un [index de plage](index-policy.md#includeexclude-strategy).

## <a name="next-steps"></a>Étapes suivantes

- [Fonctions de tableau Azure Cosmos DB](sql-query-array-functions.md)
- [Fonctions système Azure Cosmos DB](sql-query-system-functions.md)
- [Présentation d’Azure Cosmos DB](introduction.md)
