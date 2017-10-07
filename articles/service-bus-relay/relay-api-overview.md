---
title: Panoramica dell'API di inoltro aaaAzure | Documenti Microsoft
description: Panoramica delle API di Inoltro di Azure disponibili
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: fdaa1d2b-bd80-4e75-abb9-0c3d0773af2d
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: sethm
ms.openlocfilehash: 3c4d737d5fee9a8babce094fa6dfddb28910834b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="available-relay-apis"></a>API di Inoltro disponibili

## <a name="runtime-apis"></a>API di runtime

Hello nella tabella seguente sono elencati tutti i client di runtime inoltro attualmente disponibili.

Hello [informazioni aggiuntive](#additional-information) sezione contiene ulteriori informazioni sullo stato di hello ogni della libreria di runtime.

| Linguaggio/Piattaforma | Funzionalità disponibile | Pacchetto client | Repository |
| --- | --- | --- | --- |
| .NET Standard | Connessioni ibride | [Microsoft.Azure.Relay](https://www.nuget.org/packages/Microsoft.Azure.Relay/) | [GitHub](https://github.com/azure/azure-relay-dotnet) |
| .NET Framework | Inoltro WCF | [WindowsAzure.ServiceBus](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | N/D |
| Nodo | Connessioni ibride | [`hyco-ws`](https://www.npmjs.com/package/hyco-ws)<br/>[`hyco-websocket`](https://www.npmjs.com/package/hyco-websocket) | [GitHub](https://github.com/Azure/azure-relay-node) |

### <a name="additional-information"></a>Informazioni aggiuntive

#### <a name="net"></a>.NET
ecosistema .NET Hello ha più runtime, pertanto sono presenti più librerie .NET per gli hub eventi. libreria Standard di .NET Hello può essere eseguita tramite .NET Core o hello .NET Framework, mentre la libreria di .NET Framework hello può essere eseguita solo in un ambiente .NET Framework. Per altre informazioni su .NET Framework, vedere le [versioni del framework](/dotnet/articles/standard/frameworks#framework-versions).

## <a name="next-steps"></a>Passaggi successivi
toolearn ulteriori informazioni sull'inoltro di Azure, visitare i collegamenti:
* [Che cos'è il servizio di inoltro di Azure?](relay-what-is-it.md)
* [Domande frequenti sul servizio di inoltro](relay-faq.md)