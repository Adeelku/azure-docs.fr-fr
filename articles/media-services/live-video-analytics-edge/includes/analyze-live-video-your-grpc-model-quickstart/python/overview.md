---
ms.openlocfilehash: fa0c2f5bb00122b40fb4f4ea06b7cf55c0248904
ms.sourcegitcommit: eb6bef1274b9e6390c7a77ff69bf6a3b94e827fc
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91025127"
---

![Vue d’ensemble](../../../media/quickstarts/gRPC-extension.svg)

Ce diagramme montre comment les signaux circulent dans ce guide de démarrage rapide. Un [module de périphérie](https://github.com/Azure/live-video-analytics/tree/master/utilities/rtspsim-live555) simule une caméra IP hébergeant un serveur RTSP (Real-Time Streaming Protocol). Un nœud [source RTSP](../../../media-graph-concept.md#rtsp-source) extrait le flux vidéo provenant de ce serveur et envoie des images vidéo au nœud [processeur de détection de mouvement](../../../media-graph-concept.md#motion-detection-processor). Ce processeur détecte le mouvement et, après détection, envoie des images vidéo au nœud du [processeur d’extension gRPC](../../../media-graph-concept.md#grpc-extension-processor).

Le nœud d’extension gRPC joue le rôle d’un proxy. Il convertit les images vidéo dans le type d’image spécifié. Ensuite, il relaie l’image via gRPC vers un autre module de périphérie qui exécute un modèle IA derrière un point de terminaison gRPC via une [mémoire partagée](https://en.wikipedia.org/wiki/Shared_memory). Dans cet exemple, le module de périphérie est généré à l’aide du modèle [YOLOv3](https://github.com/Azure/live-video-analytics/tree/master/utilities/video-analysis/yolov3-onnx), qui peut détecter de nombreux types d’objets. Le nœud du processeur d’extension gRPC collecte les résultats de la détection et publie les événements sur le nœud [récepteur IoT Hub](https://docs.microsoft.com/azure/media-services/live-video-analytics-edge/media-graph-concept#iot-hub-message-sink). Le nœud envoie ensuite ces événements à [IoT Edge Hub](https://docs.microsoft.com/azure/iot-edge/iot-edge-glossary#iot-edge-hub).

Dans ce guide de démarrage rapide, vous allez :

1. créer et déployer le graphe multimédia ;
1. interpréter les résultats ;
1. Supprimer des ressources.
