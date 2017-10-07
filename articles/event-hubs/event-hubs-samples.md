---
title: esempi di hub eventi aaaAzure | Documenti Microsoft
description: Esempi di Hub eventi di Azure
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: f01f52e6c13f9e885999a6726143440bbc70446d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-samples"></a>Esempi di Hub eventi 

set di esempi di hub eventi di Azure Hello illustra le funzionalità chiave di [hub eventi di Azure](/azure/event-hubs/). In questo articolo vengono suddivisi in categorie e vengono illustrati alcuni esempi di hello disponibili, con collegamenti tooeach.

In fase di hello della redazione del presente documento, gli esempi di hub eventi si trovano in varie posizioni:

- [Esempi di codice per sviluppatori MSDN](https://code.msdn.microsoft.com/site/search?query=event%20hubs&f%5B0%5D.Value=event%20hubs&f%5B0%5D.Type=SearchText&ac=5)
- [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples)

Per ulteriori informazioni sulle diverse versioni di .NET Framework hello, vedere [Framework e le destinazioni](/dotnet/articles/standard/frameworks).

Altri esempi saranno aggiunti in seguito, è consigliabile quindi controllare spesso gli aggiornamenti.

## <a name="net-standard"></a>.NET Standard

Hello seguenti esempi illustrano come toosend e ricevere gli eventi utilizzando hello [client hub eventi](https://github.com/Azure/azure-event-hubs-dotnet/blob/master/readme.md) per hello [libreria .NET Standard](/dotnet/articles/standard/library).

### <a name="send-events"></a>Inviare eventi 

Hello [iniziare l'invio di](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) esempio viene illustrato come un .NET Core toowrite console applicazione che invia l'hub di eventi tooan di eventi.

### <a name="receive-events"></a>Ricevere eventi 

Hello [introduzione di ricezione con hello Host processore di eventi](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) esempio è un'applicazione console .NET Core che riceve i messaggi da un hub di eventi utilizzando hello Host processore di eventi.

## <a name="net-framework"></a>.NET Framework   

Questi esempi illustrano altre funzionalità di hub di eventi di Azure, destinazione hello [libreria .NET Framework](/dotnet/framework/index).
 
### <a name="notify-users-of-events-received"></a>Inviare notifiche agli utenti sugli eventi ricevuti

Hello [AppToNotifyUsers](https://github.com/Azure-Samples/event-hubs-dotnet-user-notifications) esempio notifica agli utenti dei dati ricevuti da sensori o altri sistemi.

### <a name="get-started-with-event-hubs"></a>Introduzione all'Hub eventi 

Hello [evento hub Guida introduttiva](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097) illustra le funzionalità di base hello degli hub di eventi, ad esempio come inviare l'hub di eventi eventi tooan toocreate un hub di eventi e utilizzare gli eventi utilizzando hello [Hostprocessoredieventi](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).

### <a name="scale-out-event-processing"></a>Elaborazione di eventi con aumento delle istanze 

Hello [scalabilità l'elaborazione di eventi](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3) esempio viene illustrato come hello toouse [Host processore di eventi](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) il carico di lavoro di toodistribute hello del consumo di flusso di hub eventi. Viene illustrato come hello tooimplement **EventProcessor** e **EventProcessorFactory** flusso di eventi oggetti toomanage hello. 

###  <a name="pull-data-from-sql-into-an-event-hub"></a>Estrazione dei dati da SQL a un hub eventi

Hello [dati pull SQL](https://github.com/Azure-Samples/event-hubs-dotnet-import-from-sql) esempio viene illustrato come toopull dati da un database SQL di tabella e spingono hub eventi tooan, toouse come input in applicazioni analitiche a valle.

### <a name="pull-web-data-into-an-event-hub"></a>Estrarre i dati web in un hub eventi 

Hello [importare dati dal web hello](https://github.com/Azure-Samples/event-hubs-dotnet-importfromweb) esempio viene illustrato come dati toopull da public feed (ad esempio le informazioni sul traffico del reparto di trasporto feed hello) e inviare tooan hub di eventi.

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni sulle versioni di .NET Framework, visitare hello seguenti collegamenti:

- [Framework e destinazioni](/dotnet/articles/standard/frameworks)
- [.NET Framework 4.6 e 4.5](/dotnet/framework/index)

È possibile ottenere altre informazioni sugli hub di eventi in hello seguenti articoli:

- [Panoramica di Hub eventi](event-hubs-what-is-event-hubs.md)
- [Creare un hub eventi](event-hubs-create.md)
- [Domande frequenti su Hub eventi](event-hubs-faq.md)