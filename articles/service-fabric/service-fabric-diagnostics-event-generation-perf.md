---
title: aaaAzure monitoraggio delle prestazioni di Service Fabric | Documenti Microsoft
description: Informazioni sui contatori delle prestazioni per il monitoraggio e la diagnostica dei cluster di Azure Service Fabric.
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
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 54d4c62b7250a1f70b0898ba07ae5a37716f4cf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="performance-metrics"></a>Metriche delle prestazioni

Metriche devono essere raccolti toounderstand hello prestazioni del cluster nonché hello applicazioni in esecuzione. Per i cluster di Service Fabric, è consigliabile raccogliere hello seguenti contatori delle prestazioni.

## <a name="nodes"></a>Nodi

Per le macchine di hello del cluster, prendere in considerazione la raccolta dei seguenti contatori delle prestazioni toobetter comprendere hello carico in ogni computer e rendere cluster appropriati scalabilità decisioni hello.

| Categoria contatore | Nome contatore |
| --- | --- |
| PhysicalDisk(per Disk) | Avg. Disk Read Queue Length |
| PhysicalDisk(per Disk) | Avg. Disk Write Queue Length |
| PhysicalDisk(per Disk) | Avg. Disk sec/Read |
| PhysicalDisk(per Disk) | Avg. Disk sec/Write |
| PhysicalDisk(per Disk) | Letture disco/sec  |
| PhysicalDisk(per Disk) | Byte letti da disco/sec  |
| PhysicalDisk(per Disk) | Scritture disco/sec |
| PhysicalDisk(per Disk) | Byte scritti su disco/sec |
| Memoria | MByte disponibili |
| PagingFile | % Usage |
| Process(Total) | % di tempo processore |
| Process (per service) | % di tempo processore |
| Process (per service) | ID Process |
| Process (per service) | Private Bytes |
| Process (per service) | Thread Count |
| Process (per service) | Virtual Bytes |
| Process (per service) | Working Set |
| Process (per service) | Working Set - Private |

## <a name="net-applications-and-services"></a>Applicazioni e servizi .NET

Raccogliere i seguenti contatori se si distribuiscono cluster tooyour di .NET services hello. 

| Categoria contatore | Nome contatore |
| --- | --- |
| .NET CLR Memory (per service) | ID di processo |
| .NET CLR Memory (per service) | # Total committed Bytes |
| .NET CLR Memory (per service) | # Total reserved Bytes |
| .NET CLR Memory (per service) | # Bytes in all Heaps |
| .NET CLR Memory (per service) | # Gen 0 Collections |
| .NET CLR Memory (per service) | # Gen 1 Collections |
| .NET CLR Memory (per service) | # Gen 2 Collections |
| .NET CLR Memory (per service) | Percentuale tempo in GC |

### <a name="service-fabrics-custom-performance-counters"></a>Contatori delle prestazioni personalizzati di Service Fabric

Service Fabric genera una quantità significativa di contatori delle prestazioni personalizzati. Se si dispone di hello SDK installato, si noterà elenco completo di hello sul proprio computer Windows Performance Monitor nell'applicazione in uso (Start > Performance Monitor). 

Nelle applicazioni hello si distribuiscono cluster tooyour, se si utilizza Reliable Actors, aggiungere countes da `Service Fabric Actor` e `Service Fabric Actor Method` categorie (vedere [servizio Fabric affidabile attori diagnostica](service-fabric-reliable-actors-diagnostics.md)).

Analogamente, se si usa Reliable Services, è necessario raccogliere i contatori delle categorie `Service Fabric Service` e `Service Fabric Service Method`. 

Se si utilizzano raccolte affidabile, è consigliabile aggiungere hello `Avg. Transaction ms/Commit` da hello `Service Fabric Transactional Replicator` la latenza media commit hello toocollect per ogni metrica di transazione.


## <a name="next-steps"></a>Passaggi successivi

* Altre informazioni, vedere [la generazione di eventi a livello di piattaforma hello](service-fabric-diagnostics-event-generation-infra.md) in Service Fabric
* Raccogliere metriche delle prestazioni tramite [Diagnostica di Azure](service-fabric-diagnostics-event-aggregation-wad.md)
