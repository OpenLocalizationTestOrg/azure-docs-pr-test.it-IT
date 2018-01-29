---
title: Interfaccia della riga di comando Azure Service Fabric - sfctl | Microsoft Docs
description: Descrive i comandi dell'interfaccia della riga di comando di Service Fabric sfctl.
services: service-fabric
documentationcenter: na
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: cli
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 12/22/2017
ms.author: ryanwi
ms.openlocfilehash: 23adc7fa6ee53d1c5edd10b2772f8825dbcef2a8
ms.sourcegitcommit: f1c1789f2f2502d683afaf5a2f46cc548c0dea50
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/18/2018
---
# <a name="sfctl"></a>sfctl 
Comandi per la gestione di cluster ed entità di Service Fabric. Questa versione è compatibile con il runtime di Service Fabric 6.0. I comandi seguono il modello nome-verbo; per altre informazioni vedere i sottogruppi seguenti.

## <a name="subgroups"></a>Sottogruppi
|Sottogruppo|DESCRIZIONE|
| --- | --- |
| [application](service-fabric-sfctl-application.md)| Consente di creare, eliminare e gestire le applicazioni e i tipi di applicazioni.|
| [chaos](service-fabric-sfctl-chaos.md)   | Consente di avviare, arrestare e creare report nel servizio di test chaos.|
| [cluster](service-fabric-sfctl-cluster.md) | Selezionare, gestire e usare dei cluster di Service Fabric.|
| [compose](service-fabric-sfctl-compose.md) | Creare, eliminare e gestire applicazioni Docker Compose.|
| [is](service-fabric-sfctl-is.md)      | Consente di eseguire query e inviare comandi al servizio di infrastruttura.|
| [node](service-fabric-sfctl-node.md)    | Consente di gestire i nodi che formano un cluster.|
| [partition](service-fabric-sfctl-partition.md)  | Consente di eseguire una query e gestire partizioni per qualsiasi servizio.|
| [rpm](service-fabric-sfctl-rpm.md)        | Consente di eseguire query e inviare comandi al servizio di gestione di ripristino.|
| [replica](service-fabric-sfctl-replica.md) | Consente di gestire le repliche che appartengono alle partizioni del servizio.|
| [service](service-fabric-sfctl-service.md) | Consente di creare, eliminare e gestire servizi, tipi di servizio e pacchetti di servizi.|
| [store](service-fabric-sfctl-store.md)   | Esegue operazioni base a livello di file nell'archivio immagini del cluster.|

## <a name="next-steps"></a>Passaggi successivi
- [Configurare](service-fabric-cli.md) l'interfaccia della riga di comando di Service Fabric.
- Informazioni su come usare l'interfaccia della riga di comando Service Fabric usando gli [script di esempio](/azure/service-fabric/scripts/sfctl-upgrade-application).