---
title: log di diagnostica del Bus di servizio aaaAzure | Documenti Microsoft
description: Informazioni su come tooset backup log di diagnostica per il Bus di servizio in Azure.
keywords: 
documentationcenter: .net
services: service-bus-messaging
author: banisadr
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: babanisa;sethm
ms.openlocfilehash: e48d6eaba6e865ae39f5b07ed6cd53d74c92e2ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-diagnostic-logs"></a>Log di diagnostica del bus di servizio

È possibile visualizzare due tipi di log per il bus di servizio di Azure:
* **[Log attività](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**. Questi log contengono informazioni sulle operazioni eseguite in un processo. registri Hello sono sempre abilitati.
* **[Log di diagnostica](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**. È possibile configurare i log di diagnostica per informazioni più complete su tutto ciò che accade in un processo. Le attività di copertura di log di diagnostica da ora hello hello processo viene creato fino a quando non viene eliminato il processo di hello, inclusi gli aggiornamenti e le attività che si verificano durante l'esecuzione del processo di hello.

## <a name="turn-on-diagnostic-logs"></a>Attivare i log di diagnostica

I log di diagnostica sono disabilitati per impostazione predefinita. i log di diagnostica tooenable, eseguire hello alla procedura seguente:

1.  In hello [portale di Azure](https://portal.azure.com)in **monitoraggio + gestione**, fare clic su **log di diagnostica**.

    ![pannello navigazione toodiagnostic log](./media/service-bus-diagnostic-logs/image1.png)

2. Fare clic sulla risorsa hello da toomonitor.  

3.  Fare clic su **Attiva diagnostica**.

    ![attivazione dei log di diagnostica](./media/service-bus-diagnostic-logs/image2.png)

4.  Per **Stato** fare clic su **Attivato**.

    ![modifica dello stato dei log di diagnostica](./media/service-bus-diagnostic-logs/image3.png)

5.  Destinazione di archiviazione hello set che si desidera. ad esempio, un account di archiviazione, un Hub eventi o Analitica di Log di Azure.

6.  Salvare le impostazioni di diagnostica nuovo hello.

Le nuove impostazioni diventano effettive in circa 10 minuti. Successivamente, i log vengono visualizzati nella destinazione di archiviazione configurato hello, su hello **log di diagnostica** blade.

Per ulteriori informazioni sulla configurazione di diagnostica, vedere hello [panoramica dei log di diagnostica Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).

## <a name="diagnostic-logs-schema"></a>Schema dei log di diagnostica

Tutti i log vengono archiviati in formato JavaScript Object Notation (JSON). Ogni voce include i campi stringa di formato hello descritti nella seguente sezione hello.

## <a name="operational-logs-schema"></a>Schema di log operativi

Registra in hello **OperationalLogs** categoria acquisire cosa accade durante operazioni del Bus di servizio. In particolare, tali registri acquisire il tipo di operazione hello, inclusa la creazione della coda, le risorse usate e lo stato dell'operazione hello hello.

Le stringhe JSON registro operativo includono gli elementi elencati in hello nella tabella seguente:

Nome | Descrizione
------- | -------
ActivityId | ID interno, usato a scopo di rilevamento
EventName | Nome operazione           
resourceId | ID della risorsa Azure Resource Manager
SubscriptionId | ID sottoscrizione
EventTimeString | Durata dell'operazione
EventProperties | Proprietà dell'operazione
Status | Stato dell'operazione
Chiamante | Chiamante dell'operazione (Portale di Azure o client di gestione)
category | OperationalLogs

Di seguito è riportato un esempio di stringa JSON di log operativo:

```json
{
  "ActivityId": "6aa994ac-b56e-4292-8448-0767a5657cc7",
  "EventName": "Create Queue",
  "resourceId": "/SUBSCRIPTIONS/1A2109E3-9DA0-455B-B937-E35E36C1163C/RESOURCEGROUPS/DEFAULT-SERVICEBUS-CENTRALUS/PROVIDERS/MICROSOFT.SERVICEBUS/NAMESPACES/SHOEBOXEHNS-CY4001",
  "SubscriptionId": "1a2109e3-9da0-455b-b937-e35e36c1163c",
  "EventTimeString": "9/28/2016 8:40:06 PM +00:00",
  "EventProperties": "{\"SubscriptionId\":\"1a2109e3-9da0-455b-b937-e35e36c1163c\",\"Namespace\":\"shoeboxehns-cy4001\",\"Via\":\"https://shoeboxehns-cy4001.servicebus.windows.net/f8096791adb448579ee83d30e006a13e/?api-version=2016-07\",\"TrackingId\":\"5ee74c9e-72b5-4e98-97c4-08a62e56e221_G1\"}",
  "Status": "Succeeded",
  "Caller": "ServiceBus Client",
  "category": "OperationalLogs"
}
```

## <a name="next-steps"></a>Passaggi successivi

Visitare hello toolearn collegamenti più sul Bus di servizio seguente:

* [Introduzione tooService Bus](service-bus-messaging-overview.md)
* [Introduzione al bus di servizio](service-bus-dotnet-get-started-with-queues.md)
