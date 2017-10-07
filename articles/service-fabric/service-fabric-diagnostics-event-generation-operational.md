---
title: Canale operativo dell'infrastruttura del servizio aaaAzure | Documenti Microsoft
description: Elenco completo dei log generati in cluster canale operative di Azure Service Fabric hello.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/19/2017
ms.author: dekapur
ms.openlocfilehash: 358782420ed62b202d6a89fe0f200b5ef0384c9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="operational-channel"></a>Canale operativo 

canale operativo Hello è costituito dai registri di alto livello azioni eseguite da Service Fabric i nodi e il cluster. Quando "Diagnostics" è abilitato per un cluster, hello agente diagnostica Azure viene distribuito il cluster e per impostazione predefinita è configurato tooread nei log dal canale operativo hello. Ulteriori informazioni sulla configurazione di hello [agente diagnostica Azure](service-fabric-diagnostics-event-aggregation-wad.md) configurazione di diagnostica di hello toomodify di toopick il cluster più registri o i contatori delle prestazioni. 

## <a name="operational-channel-logs"></a>Log del canale operativo 

Di seguito è riportato un elenco completo dei log forniti dall'infrastruttura di servizio in canale operativo hello. 

| EventId | Nome | Origine (attività) | Level |
| --- | --- | --- | --- |
| 25620 | NodeOpening | FabricNode | Informazioni |
| 25621 | NodeOpenedSuccess | FabricNode | Informazioni |
| 25622 | NodeOpenedFailed | FabricNode | Informazioni |
| 25623 | NodeClosing | FabricNode | Informazioni |
| 25624 | NodeClosed | FabricNode | Informazioni |
| 25625 | NodeAborting | FabricNode | Informazioni |
| 25626 | NodeAborted | FabricNode | Informazioni |
| 29627 | ClusterUpgradeStart | CM | Informazioni |
| 29628 | ClusterUpgradeComplete | CM | Informazioni |
| 29629 | ClusterUpgradeRollback | CM | Informazioni |
| 29630 | ClusterUpgradeRollbackComplete | CM | Informazioni |
| 29631 | ClusterUpgradeDomainComplete | CM | Informazioni |
| 23074 | ContainerActivated | Hosting | Informazioni |
| 23075 | ContainerDeactivated | Hosting | Informazioni |
| 29620 | ApplicationCreated | CM | Informazioni |
| 29621 | ApplicationUpgradeStart | CM | Informazioni |
| 29622 | ApplicationUpgradeComplete | CM | Informazioni |
| 29623 | ApplicationUpgradeRollback | CM | Informazioni |
| 29624 | ApplicationUpgradeRollbackComplete | CM | Informazioni |
| 29625 | ApplicationDeleted | CM | Informazioni |
| 29626 | ApplicationUpgradeDomainComplete | CM | Informazioni |
| 18566 | ServiceCreated | FM | Informazioni |
| 18567 | ServiceDeleted | FM | Informazioni |

## <a name="next-steps"></a>Passaggi successivi

* Altre informazioni su Generale [la generazione di eventi a livello di piattaforma hello](service-fabric-diagnostics-event-generation-infra.md) in Service Fabric
* Modifica il [diagnostica Azure](service-fabric-diagnostics-event-aggregation-wad.md) toocollect configurazione più log
* [Configurazione di Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) registra il canale operativo toosee
