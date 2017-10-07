---
title: Panoramica dell'API di hub eventi aaaAzure | Documenti Microsoft
description: Panoramica delle API di Hub eventi di Azure disponibili
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 3f221a0c-182d-4e39-9f3d-3a3c16c5c6ed
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 46dfcc544ff92642cfd7a967f9ec38a0d8e2bd5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="available-event-hubs-apis"></a>API di Hub eventi disponibili

## <a name="runtime-apis"></a>API di runtime

di seguito Hello è una descrizione di tutti i client di runtime hub eventi di Azure attualmente disponibili. Benché alcune di queste librerie include anche funzionalità di gestione limitata, ci sono anche [librerie specifiche](#management-apis) dedicato toomanagement operazioni. lo stato attivo principale Hello di queste librerie è toosend e ricevere messaggi da un hub eventi.

Vedere [informazioni aggiuntive](#additional-information) per ulteriori informazioni sullo stato corrente di hello ogni della libreria di runtime.

| Linguaggio/Piattaforma | Pacchetto client | Pacchetto EventProcessorHost | Repository |
| --- | --- | --- | --- |
| .NET Standard | [NuGet](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) | [NuGet](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) | [GitHub](https://github.com/azure/azure-event-hubs-dotnet) |
| .NET Framework | [NuGet](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | [NuGet](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) | N/D |
| Java | [Maven](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22) | [Maven](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22) | [GitHub](https://github.com/Azure/azure-event-hubs-java) |
| Nodo | [NPM](https://www.npmjs.com/package/azure-event-hubs) | N/D | [GitHub](https://github.com/Azure/azure-event-hubs-node) |
| C | N/D | N/D | [GitHub](https://github.com/Azure/azure-event-hubs-c) |

### <a name="additional-information"></a>Informazioni aggiuntive

#### <a name="net"></a>.NET
ecosistema .NET Hello ha più runtime, pertanto sono presenti più librerie .NET per gli hub eventi. libreria Standard di .NET Hello può essere eseguita tramite .NET Core o hello .NET Framework, mentre la libreria di .NET Framework hello può essere eseguita solo in un ambiente .NET Framework. Per altre informazioni su .NET Framework, vedere le [versioni del framework](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions).

#### <a name="node"></a>Nodo

libreria di Node.js Hello è attualmente in anteprima e viene mantenuta come progetto lato dai dipendenti Microsoft e dai collaboratori esterni. Tutti i contributi compreso il codice sorgente sono graditi e verranno presi in esame.

## <a name="management-apis"></a>API di gestione

di seguito Hello è un elenco di tutte le librerie specifiche di gestione attualmente disponibili. Nessuna di queste librerie contengono le operazioni di runtime e hello solo scopo di gestire le entità di hub eventi.

| Linguaggio/Piattaforma | Pacchetto di gestione | Repository |
| --- | --- | --- | --- |
| .NET Standard | [NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.EventHub) | [GitHub](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/ResourceManagement/EventHub) |

## <a name="next-steps"></a>Passaggi successivi
Sono disponibili ulteriori informazioni sugli hub di eventi visitando hello seguenti collegamenti:

* [Panoramica di Hub eventi](event-hubs-what-is-event-hubs.md)
* [Creare un hub eventi](event-hubs-create.md)
* [Domande frequenti su Hub eventi](event-hubs-faq.md)