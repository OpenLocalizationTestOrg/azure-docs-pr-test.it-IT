---
title: log di diagnostica di hub eventi aaaAzure | Documenti Microsoft
description: Informazioni su come tooset dei log di diagnostica per gli hub di eventi in Azure.
keywords: 
documentationcenter: 
services: event-hubs
author: banisadr
manager: 
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: sethm;babanisa
ms.openlocfilehash: d2054e2e444e715e5077fe2608fe1e009e6c1d84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-diagnostic-logs"></a>Log di diagnostica di Hub eventi

È possibile visualizzare due tipi di log per Hub eventi di Azure:
* **[Log attività](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**. Questi log contengono informazioni sulle operazioni eseguite in un processo. registri Hello sono sempre abilitati.
* **[Log di diagnostica](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**. È possibile configurare i log di diagnostica per una visualizzazione più completa di tutto ciò che accade in un processo. Le attività di copertura di log di diagnostica da ora hello hello processo viene creato fino a quando non viene eliminato il processo di hello, inclusi gli aggiornamenti e le attività che si verificano durante l'esecuzione del processo di hello.

## <a name="turn-on-diagnostic-logs"></a>Attivare i log di diagnostica
I log di diagnostica sono disabilitati per impostazione predefinita. log di diagnostica tooenable:

1.  In hello [portale di Azure](https://portal.azure.com)in **monitoraggio + gestione**, fare clic su **log di diagnostica**.

    ![pannello navigazione toodiagnostic log](./media/event-hubs-diagnostic-logs/image1.png)

2.  Fare clic sulla risorsa hello da toomonitor.

3.  Fare clic su **Attiva diagnostica**.

    ![Attivare i log di diagnostica](./media/event-hubs-diagnostic-logs/image2.png)

4.  Per **Stato** fare clic su **Attivato**.

    ![Modificare lo stato di hello del log di diagnostica](./media/event-hubs-diagnostic-logs/image3.png)

5.  Destinazione di archiviazione hello set che si desidera. ad esempio, un account di archiviazione, un hub eventi o Analitica di Log di Azure.

6.  Salvare le impostazioni di diagnostica nuovo hello.

Le nuove impostazioni diventano effettive in circa 10 minuti. Successivamente, i log vengono visualizzati nella destinazione di archiviazione configurato hello, su hello **log di diagnostica** blade.

Per ulteriori informazioni sulla configurazione di diagnostica, vedere hello [panoramica dei log di diagnostica Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).

## <a name="diagnostic-logs-categories"></a>Categorie dei log di diagnostica
Hub eventi consente di acquisire i log di diagnostica per due categorie:

* **ArchiveLogs**: log relativi archivi hub tooEvent, in particolare, registra gli errori di tooarchive correlati.
* **OperationalLogs**: informazioni su ciò che avviene durante le operazioni di hub eventi, in particolare, il tipo di operazione, inclusa la creazione di hub eventi, le risorse usate, hello e hello lo stato dell'operazione di hello.

## <a name="diagnostic-logs-schema"></a>Schema dei log di diagnostica
Tutti i log vengono archiviati in formato JavaScript Object Notation (JSON). Ogni voce include i campi stringa di formato hello descritto in hello le sezioni seguenti.

### <a name="archive-logs-schema"></a>Schema dei log di archiviazione

Le stringhe JSON di log di archiviazione includono gli elementi elencati in hello nella tabella seguente:

Nome | Descrizione
------- | -------
TaskName | Descrizione dell'attività hello che non è riuscita.
ActivityId | ID interno, usato a scopo di rilevamento.
trackingId | ID interno, usato a scopo di rilevamento.
resourceId | ID della risorsa di Azure Resource Manager.
eventHub | Nome completo dell'hub eventi, include il nome dello spazio dei nomi.
partitionId | Partizione dell'hub eventi per l'operazione di scrittura.
archiveStep | ArchiveFlushWriter
startTime | Ora di inizio di un errore.
errori | Numero di volte in cui si è verificato un errore.
durationInSeconds | Durata dell'errore.
Message | Messaggio di errore.
category | ArchiveLogs

Hello codice riportato di seguito è riportato un esempio di un stringa JSON del log di archiviazione:

```json
{
     "TaskName": "EventHubArchiveUserError",
     "ActivityId": "21b89a0b-8095-471a-9db8-d151d74ecf26",
     "trackingId": "21b89a0b-8095-471a-9db8-d151d74ecf26_B7",
     "resourceId": "/SUBSCRIPTIONS/854D368F-1828-428F-8F3C-F2AFFA9B2F7D/RESOURCEGROUPS/DEFAULT-EVENTHUB-CENTRALUS/PROVIDERS/MICROSOFT.EVENTHUB/NAMESPACES/FBETTATI-OPERA-EVENTHUB",
     "eventHub": "fbettati-opera-eventhub:eventhub:eh123~32766",
     "partitionId": "1",
     "archiveStep": "ArchiveFlushWriter",
     "startTime": "9/22/2016 5:11:21 AM",
     "failures": 3,
     "durationInSeconds": 360,
     "message": "Microsoft.WindowsAzure.Storage.StorageException: hello remote server returned an error: (404) Not Found. ---> System.Net.WebException: hello remote server returned an error: (404) Not Found.\r\n   at Microsoft.WindowsAzure.Storage.Shared.Protocol.HttpResponseParsers.ProcessExpectedStatusCodeNoException[T](HttpStatusCode expectedStatusCode, HttpStatusCode actualStatusCode, T retVal, StorageCommandBase`1 cmd, Exception ex)\r\n   at Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob.<PutBlockImpl>b__3e(RESTCommand`1 cmd, HttpWebResponse resp, Exception ex, OperationContext ctx)\r\n   at Microsoft.WindowsAzure.Storage.Core.Executor.Executor.EndGetResponse[T](IAsyncResult getResponseResult)\r\n   --- End of inner exception stack trace ---\r\n   at Microsoft.WindowsAzure.Storage.Core.Util.StorageAsyncResult`1.End()\r\n   at Microsoft.WindowsAzure.Storage.Core.Util.AsyncExtensions.<>c__DisplayClass4.<CreateCallbackVoid>b__3(IAsyncResult ar)\r\n--- End of stack trace from previous location where exception was thrown ---\r\n   at System.",
     "category": "ArchiveLogs"
}
```

### <a name="operational-logs-schema"></a>Schema di log operativi

Le stringhe JSON registro operativo includono gli elementi elencati in hello nella tabella seguente:

Nome | Descrizione
------- | -------
ActivityId | ID interno, utilizzato tootrack scopo.
EventName | Nome operazione.  
resourceId | ID della risorsa di Azure Resource Manager.
SubscriptionId | l'ID sottoscrizione.
EventTimeString | Durata dell'operazione.
EventProperties | Proprietà dell'operazione.
Status | Stato dell'operazione.
Chiamante | Chiamante dell'operazione (Portale di Azure o client di gestione).
category | OperationalLogs

Hello codice riportato di seguito è riportato un esempio di una stringa JSON registro operativo:

```json
Example:
{
     "ActivityId": "6aa994ac-b56e-4292-8448-0767a5657cc7",
     "EventName": "Create EventHub",
     "resourceId": "/SUBSCRIPTIONS/1A2109E3-9DA0-455B-B937-E35E36C1163C/RESOURCEGROUPS/DEFAULT-SERVICEBUS-CENTRALUS/PROVIDERS/MICROSOFT.EVENTHUB/NAMESPACES/SHOEBOXEHNS-CY4001",
     "SubscriptionId": "1a2109e3-9da0-455b-b937-e35e36c1163c",
     "EventTimeString": "9/28/2016 8:40:06 PM +00:00",
     "EventProperties": "{\"SubscriptionId\":\"1a2109e3-9da0-455b-b937-e35e36c1163c\",\"Namespace\":\"shoeboxehns-cy4001\",\"Via\":\"https://shoeboxehns-cy4001.servicebus.windows.net/f8096791adb448579ee83d30e006a13e/?api-version=2016-07\",\"TrackingId\":\"5ee74c9e-72b5-4e98-97c4-08a62e56e221_G1\"}",
     "Status": "Succeeded",
     "Caller": "ServiceBus Client",
     "category": "OperationalLogs"
}
```

## <a name="next-steps"></a>Passaggi successivi
* [Introduzione tooEvent hub](event-hubs-what-is-event-hubs.md)
* [Panoramica dell'API di Hub eventi](event-hubs-api-overview.md)
* [Introduzione all'Hub eventi](event-hubs-csharp-ephcs-getstarted.md)
