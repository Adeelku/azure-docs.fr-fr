---
title: Schéma d’appareil dans la solution de supervision à distance - Azure | Microsoft Docs
description: Cet article décrit le schéma JSON qui définit un appareil simulé dans la solution de supervision à distance.
author: dominicbetts
manager: philmea
ms.author: dobett
ms.service: iot-accelerators
services: iot-accelerators
ms.date: 12/18/2018
ms.topic: conceptual
ms.custom:
- amqp
- mqtt
ms.openlocfilehash: ac681bb13ccea49c7a2f566a6fcdb6adb8cec5bb
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2020
ms.locfileid: "81683746"
---
# <a name="understand-the-device-model-schema"></a>Comprendre le schéma de modèle d’appareil

Vous pouvez utiliser des appareils simulés dans la solution de supervision à distance pour en tester le comportement. La solution de supervision à distance inclut un service de simulation d’appareil pour exécuter des appareils simulés. Quand vous déployez la solution de supervision à distance, une collection d’appareils simulés est provisionnée automatiquement. Vous pouvez personnaliser les appareils simulés existants ou créer les vôtres.

Cet article décrit le schéma de modèle d’appareil qui spécifie les fonctionnalités et le comportement d’un appareil simulé. Le modèle d’appareil est stocké dans un fichier JSON.

> [!NOTE]
> Ce schéma de modèle d’appareil est destiné uniquement aux appareils simulés hébergés dans le service de simulation d’appareil. Si vous voulez créer un appareil réel, consultez [Connecter votre appareil à l’accélérateur de solution de supervision à distance](iot-accelerators-connecting-devices.md).

Les articles suivants sont associées à l’article en cours :

* [Implémenter le comportement de modèle d’appareil](iot-accelerators-remote-monitoring-device-behavior.md) décrit les fichiers JavaScript que vous utilisez pour implémenter le comportement d’un appareil simulé.
* [Créer un appareil simulé](iot-accelerators-remote-monitoring-create-simulated-device.md) réunit toutes les instructions et vous montre comment déployer un nouveau type d’appareil simulé dans votre solution.

Dans cet article, vous apprendrez comment :

>[!div class="checklist"]
> * Utiliser un fichier JSON pour définir un modèle d’appareil simulé
> * Spécifier les propriétés de l’appareil simulé
> * Spécifier les données de télémétrie que l’appareil simulé envoie
> * Spécifier les méthodes cloud-à-appareil auxquelles l’appareil répond

## <a name="the-parts-of-the-device-model-schema"></a>Les parties d’un schéma de modèle d’appareil

Chaque modèle d’appareil, comme un refroidisseur ou un camion, définit le type d’appareil que peut simuler le service de simulation. Chaque modèle d’appareil est stocké dans un fichier JSON avec le schéma de niveau supérieur suivant :

```json
{
  "SchemaVersion": "1.0.0",
  "Id": "elevator-01",
  "Version": "0.0.1",
  "Name": "Elevator",
  "Description": "Elevator with floor, vibration and temperature sensors.",
  "Protocol": "AMQP",
  "Simulation": {
    // Specify the simulation behavior
  },
  "Properties": {
    // Define properties
  },
  "Telemetry": [
    // Specify telemetry
  ],
  "CloudToDeviceMethods": {
    // Specify methods
  }
}
```

Vous pouvez afficher les fichiers du schéma pour les appareils simulés par défaut dans le [dossier devicemodels](https://github.com/Azure/device-simulation-dotnet/tree/master/Services/data/devicemodels) sur GitHub.

Le tableau suivant décrit les entrées du schéma de niveau supérieur :

| Entrée de schéma | Description |
| -- | --- |
| `SchemaVersion` | La version du schéma est toujours `1.0.0` et est spécifique au format de ce fichier. |
| `Id` | Un ID unique pour ce modèle d’appareil. |
| `Version` | Identifie la version du modèle d’appareil. |
| `Name` | Un nom convivial pour le modèle d’appareil. |
| `Description` | Une description du modèle d’appareil. |
| `Protocol` | Le protocole de connexion utilisé par l’appareil. Peut être `AMQP`, `MQTT` ou `HTTP`. |

Les sections suivantes décrivent les autres sections du schéma JSON :

## <a name="simulation"></a>Simulation

Dans la section `Simulation`, vous définissez l’état interne de l’appareil simulé. Les valeurs des données de télémétrie envoyées par l’appareil doivent faire partie de cet état de l’appareil.

La définition de l’état de l’appareil contient deux éléments :

* `InitialState` définit les valeurs initiales de toutes les propriétés de l’objet état de l’appareil.
* `Script` identifie un fichier JavaScript qui s’exécute selon une planification pour mettre à jour l’état de l’appareil. Vous pouvez utiliser ce fichier de script pour rendre aléatoire les valeurs des données de télémétrie envoyées par l’appareil.

Pour plus d’informations sur le fichier JavaScript qui met à jour l’objet état de l’appareil, consultez [Comprendre le comportement du modèle d’appareil](../../articles/iot-accelerators/iot-accelerators-device-simulation-advanced-device.md).

L’exemple suivant montre la définition de l’objet état de l’appareil pour un appareil de refroidissement simulé :

```json
"Simulation": {
  "InitialState": {
    "online": true,
    "temperature": 75.0,
    "temperature_unit": "F",
    "humidity": 70.0,
    "humidity_unit": "%",
    "pressure": 150.0,
    "pressure_unit": "psig",
    "simulation_state": "normal_pressure"
  },
  "Interval": "00:00:10",
  "Scripts": {
    "Type": "javascript",
    "Path": "chiller-01-state.js"
  }
}
```

Le service de simulation exécute le fichier **chiller-01-state.js** toutes les cinq secondes pour mettre à jour l’état de l’appareil. Vous pouvez voir les fichiers JavaScript pour les appareils simulés par défaut dans le [dossier scipts](https://github.com/Azure/device-simulation-dotnet/tree/master/Services/data/devicemodels/scripts) sur GitHub. Par convention, ces fichiers JavaScript ont le suffixe **-state** pour les différencier des fichiers qui implémentent les comportements de la méthode.

## <a name="properties"></a>Propriétés

La section `Properties` du schéma définit les valeurs de propriété que l’appareil indique à la solution. Par exemple :

```json
"Properties": {
  "Type": "Elevator",
  "Location": "Building 2",
  "Latitude": 47.640792,
  "Longitude": -122.126258
}
```

Lorsque la solution démarre, elle interroge tous les appareils simulés pour générer une liste de valeurs `Type` à utiliser dans l’interface utilisateur. La solution utilise les propriétés `Latitude` et `Longitude` pour ajouter l’emplacement de l’appareil à la carte sur le tableau de bord.

## <a name="telemetry"></a>Télémétrie

Le tableau `Telemetry` répertorie tous les types de données de télémétrie que l’appareil simulé envoie à la solution.

L’exemple suivant envoie un message de télémétrie JSON toutes les 10 secondes avec les données `floor`, `vibration` et `temperature` des capteurs de l’ascenseur :

```json
"Telemetry": [
  {
    "Interval": "00:00:10",
    "MessageTemplate": "{\"floor\":${floor},\"vibration\":${vibration},\"vibration_unit\":\"${vibration_unit}\",\"temperature\":${temperature},\"temperature_unit\":\"${temperature_unit}\"}",
    "MessageSchema": {
      "Name": "elevator-sensors;v1",
      "Format": "JSON",
      "Fields": {
        "floor": "integer",
        "vibration": "double",
        "vibration_unit": "text",
        "temperature": "double",
        "temperature_unit": "text"
      }
    }
  }
]
```

`MessageTemplate` définit la structure du message JSON envoyé par l’appareil simulé. Les espaces réservés dans `MessageTemplate` utilisent la syntaxe `${NAME}` où `NAME` est une clé issue de [l’objet état de l’appareil](#simulation). Les chaînes doivent être mises entre guillemets, pas les nombres.

`MessageSchema` définit le schéma du message envoyé par l’appareil simulé. Le schéma du message est également publié sur IoT Hub pour permettre aux applications principales de réutiliser les informations afin d’interpréter les données de télémétrie entrantes.

Actuellement, vous ne pouvez utiliser que des schémas de message JSON. Les champs répertoriés dans le schéma peuvent avoir les types suivants :

* Objet - sérialisé à l’aide de JSON
* Binaire - sérialisé à l’aide de base64
* Texte
* Boolean
* Integer
* Double
* DateTime

Pour envoyer des messages de télémétrie à des intervalles différents, ajoutez plusieurs types de données de télémétrie au tableau `Telemetry`. L’exemple suivant envoie les données de température et d’humidité toutes les 10 secondes et l’état de la lumière toutes les minutes :

```json
"Telemetry": [
  {
    "Interval": "00:00:10",
    "MessageTemplate":
      "{\"temperature\":${temperature},\"temperature_unit\":\"${temperature_unit}\",\"humidity\":\"${humidity}\"}",
    "MessageSchema": {
      "Name": "RoomComfort;v1",
      "Format": "JSON",
      "Fields": {
        "temperature": "double",
        "temperature_unit": "text",
        "humidity": "integer"
      }
    }
  },
  {
    "Interval": "00:01:00",
    "MessageTemplate": "{\"lights\":${lights_on}}",
    "MessageSchema": {
      "Name": "RoomLights;v1",
      "Format": "JSON",
      "Fields": {
        "lights": "boolean"
      }
    }
  }
],
```

## <a name="cloudtodevicemethods"></a>CloudToDeviceMethods

Un appareil simulé peut répondre aux méthodes cloud-à-appareil appelées à partir d’un hub IoT. La section `CloudToDeviceMethods` dans le fichier de schéma du modèle d’appareil :

* Définit les méthodes auxquelles l’appareil simulé peut répondre.
* Identifie le fichier JavaScript qui contient la logique à exécuter.

L’appareil simulé envoie la liste des méthodes qu’il prend en charge au hub IoT auquel il est connecté.

Pour plus d’informations sur le fichier JavaScript qui implémente le comportement de l’appareil, consultez [Comprendre le comportement du modèle d’appareil](../../articles/iot-accelerators/iot-accelerators-device-simulation-advanced-device.md).

L’exemple suivant spécifie trois méthodes prises en charge et les fichiers JavaScript qui implémentent ces méthodes :

```json
"CloudToDeviceMethods": {
  "Reboot": {
    "Type": "javascript",
    "Path": "Reboot-method.js"
  },
  "EmergencyValveRelease": {
    "Type": "javascript",
    "Path": "EmergencyValveRelease-method.js"
  },
  "IncreasePressure": {
    "Type": "javascript",
    "Path": "IncreasePressure-method.js"
  }
}
```

Vous pouvez voir les fichiers JavaScript pour les appareils simulés par défaut dans le [dossier scipts](https://github.com/Azure/device-simulation-dotnet/tree/master/Services/data/devicemodels/scripts) sur GitHub. Par convention, ces fichiers JavaScript ont le suffixe **-method** pour les différencier des fichiers qui implémentent le comportement de l’état.

## <a name="next-steps"></a>Étapes suivantes

Cet article vous a décrit comment créer votre propre modèle personnalisé d’appareil simulé. Cet article vous a montré comment :

<!-- Repeat task list from intro -->
>[!div class="checklist"]
> * Utiliser un fichier JSON pour définir un modèle d’appareil simulé
> * Spécifier les propriétés de l’appareil simulé
> * Spécifier les données de télémétrie que l’appareil simulé envoie
> * Spécifier les méthodes cloud-à-appareil auxquelles l’appareil répond

Maintenant que vous avez découvert le schéma JSON, nous vous recommandons d’apprendre à [implémenter le comportement de votre appareil simulé](iot-accelerators-remote-monitoring-device-behavior.md).

Pour plus d’informations sur le développement de la solution de supervision à distance, consultez :

* [Guide d’informations de référence pour les développeurs](https://github.com/Azure/azure-iot-pcs-remote-monitoring-dotnet/wiki/Developer-Reference-Guide)
* [Guide de résolution des problèmes pour les développeurs](https://github.com/Azure/azure-iot-pcs-remote-monitoring-dotnet/wiki/Developer-Troubleshooting-Guide)
