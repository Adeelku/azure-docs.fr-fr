---
title: Secrets d’authentification dans l’apprentissage
titleSuffix: Azure Machine Learning
description: Transmettre des secrets à des cycles d’apprentissage de manière sécurisée à l’aide du coffre de clés d’espace de travail
services: machine-learning
author: rastala
ms.author: roastala
ms.reviewer: larryfr
ms.service: machine-learning
ms.subservice: core
ms.date: 03/09/2020
ms.topic: conceptual
ms.custom: how-to
ms.openlocfilehash: 89934470dc3bf86bb2843137a2129bff13323ca0
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91302075"
---
# <a name="use-authentication-credential-secrets-in-azure-machine-learning-training-runs"></a>Utiliser les secrets d’authentification dans les exécutions d’apprentissage Azure Machine Learning


Cet article explique comment utiliser des secrets dans des cycles d’apprentissage en toute sécurité. Les informations d’authentification, telles que votre nom d’utilisateur et votre mot de passe, sont des secrets. Par exemple, si vous vous connectez à une base de données externe pour interroger des données d’entraînement, vous devez transmettre vos nom d’utilisateur et mot de passe au contexte d’exécution à distance. La programmation de telles valeurs dans des scripts d’entraînement en texte clair n’est pas sécurisée, car elle exposerait le secret. 

Au lieu de cela, votre espace de travail Azure Machine Learning a une ressource associée appelée [Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-overview). Utilisez ce coffre de clés pour transmettre des secrets de façon sécurisée aux exécutions distantes par le biais d’un ensemble d’API dans le SDK Python pour Azure Machine Learning.

Le flux standard pour l’utilisation de secrets est le suivant :
 1. Sur l’ordinateur local, connectez-vous à Azure, puis à votre espace de travail.
 2. Sur l’ordinateur local, définissez un secret dans le coffre de clés de l’espace de travail.
 3. Commandes une exécution à distance.
 4. Dans l’exécution à distance, récupérez le secret à partir de Key Vault et utilisez-le.

## <a name="set-secrets"></a>Définir des secrets

Dans Azure Machine Learning, la classe [Keyvault](https://docs.microsoft.com/python/api/azureml-core/azureml.core.keyvault.keyvault?view=azure-ml-py&preserve-view=true) contient des méthodes pour définir des secrets. Dans votre session Python locale, obtenez d’abord une référence au coffre de clés de votre espace de travail, puis utilisez la méthode [`set_secret()`](https://docs.microsoft.com/python/api/azureml-core/azureml.core.keyvault.keyvault?view=azure-ml-py&preserve-view=true#&preserve-view=trueset-secret-name--value-) pour définir un secret à l’aide d’un nom et d’une valeur. La méthode __set_secret__ met à jour la valeur de secret si le nom existe.

```python
from azureml.core import Workspace
from azureml.core import Keyvault
import os


ws = Workspace.from_config()
my_secret = os.environ.get("MY_SECRET")
keyvault = ws.get_default_keyvault()
keyvault.set_secret(name="mysecret", value = my_secret)
```

Ne placez pas la valeur du secret dans votre code Python, car il n’est pas sûr de la stocker dans un fichier en texte clair. Au lieu de cela, obtenez la valeur du secret à partir d’une variable d’environnement telle qu’un secret de la build Azure DevOps, ou à partir d’une entrée d’utilisateur interactive.

Vous pouvez lister les noms des secrets à l’aide de la méthode [`list_secrets()`](https://docs.microsoft.com/python/api/azureml-core/azureml.core.keyvault.keyvault?view=azure-ml-py&preserve-view=true#&preserve-view=truelist-secrets--), et il existe également une version par lot, [set_secrets()](https://docs.microsoft.com/python/api/azureml-core/azureml.core.keyvault.keyvault?view=azure-ml-py&preserve-view=true#&preserve-view=trueset-secrets-secrets-batch-), qui vous permet de définir plusieurs secrets à la fois.

## <a name="get-secrets"></a>Get secrets (Obtenir les secrets)

Dans votre code local, vous pouvez utiliser la méthode [`get_secret()`](https://docs.microsoft.com/python/api/azureml-core/azureml.core.keyvault.keyvault?view=azure-ml-py&preserve-view=true#&preserve-view=trueget-secret-name-) pour obtenir la valeur de secret par son nom.

Pour les exécutions soumises avec [`Experiment.submit`](https://docs.microsoft.com/python/api/azureml-core/azureml.core.experiment.experiment?view=azure-ml-py&preserve-view=true#&preserve-view=truesubmit-config--tags-none----kwargs-), utilisez la méthode [`get_secret()`](https://docs.microsoft.com/python/api/azureml-core/azureml.core.run.run?view=azure-ml-py&preserve-view=true#&preserve-view=trueget-secret-name-) avec la classe [`Run`](https://docs.microsoft.com/python/api/azureml-core/azureml.core.run%28class%29?view=azure-ml-py&preserve-view=true). Une exécution soumise ayant connaissance de son espace de travail, cette méthode raccourcit l’instanciation de l’espace de travail et retourne directement la valeur du secret.

```python
# Code in submitted run
from azureml.core import Experiment, Run

run = Run.get_context()
secret_value = run.get_secret(name="mysecret")
```

Veillez à ne pas exposer la valeur de secret en l’écrivant ou en l’imprimant.

Il existe également une version par lot, [get_secrets()](https://docs.microsoft.com/python/api/azureml-core/azureml.core.run.run?view=azure-ml-py&preserve-view=true#&preserve-view=trueget-secrets-secrets-), pour l’accès à plusieurs secrets à la fois.

## <a name="next-steps"></a>Étapes suivantes

 * [Voir un exemple de notebook](https://github.com/Azure/MachineLearningNotebooks/blob/master/how-to-use-azureml/manage-azureml-service/authentication-in-azureml/authentication-in-azureml.ipynb)
 * [Découvrir la sécurité en entreprise avec Azure Machine Learning](concept-enterprise-security.md)
