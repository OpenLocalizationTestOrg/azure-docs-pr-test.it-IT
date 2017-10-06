---
title: API di gestione con Azure Monitor aaaMonitor | Documenti Microsoft
description: Informazioni su come toomonitor gestione API di Azure del servizio tramite il monitoraggio di Azure.
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 2fa193cd-ea71-4b33-a5ca-1f55e5351e23
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 5012d8ed57ea4f94ea6bc1b7c4e1102516ec4414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-api-management-with-azure-monitor"></a>Monitorare Gestione API con Monitoraggio di Azure
Monitoraggio di Azure è un servizio di Azure che offre un'unica origine per il monitoraggio di tutte le risorse di Azure. Con Monitor di Azure, è possibile visualizzare, richiedere, route, archiviare e intraprendere azioni metriche hello e log provenienti dalle risorse di Azure, ad esempio Gestione API. 

Hello seguente video viene illustrato come toomonitor gestione API tramite il monitoraggio di Azure. Per altre informazioni su Monitoraggio di Azure, vedere l'[introduzione a Monitoraggio di Azure]. 


> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Monitor-API-Management-with-Azure-Monitor/player]
>
>
 
## <a name="metrics"></a>Metrica
Gestione API attualmente genera cinque metriche e contiamo tooadd più hello future. Queste metriche vengono create ogni minuto, fornendo quasi in tempo reale visibilità nello stato di hello e integrità delle API. Ecco un riepilogo delle metriche hello:
* Totale richieste Gateway: hello numero di API richieste nel periodo di hello. 
* Richieste riuscite Gateway: numero hello di richieste di API che ha ricevuto i codici di risposta HTTP ha esito positivo inclusi 304, 307 e qualsiasi valore inferiore rispetto a 301 (ad esempio, 200). 
* Gateway richieste non riuscite: numero di hello di richieste di API che ha ricevuto i codici di risposta HTTP errati tra 400 e qualsiasi valore maggiore di 500.
* Richieste non autorizzate di Gateway: numero hello di richieste di API che ha ricevuto i codici di risposta HTTP inclusi 401, 403 e 429. 
* Altre richieste Gateway: numero hello di richieste di API che ha ricevuto i codici di risposta HTTP che non appartengono tooany di hello precedente categorie (ad esempio, 418).

È possibile accedere alle metriche del servizio Gestione API o alle metriche di tutte le risorse di Azure in Monitoraggio di Azure. metrica tooview nel servizio Gestione API:
1. Hello aprirlo portale di Azure.
2. Passare il servizio di gestione API tooyour.
3. Fare clic su **Metrica**.

![Pannello delle metriche][metrics-blade]

Per ulteriori informazioni su come toouse metriche, vedere [Panoramica di metriche].

## <a name="activity-logs"></a>Log attività
Log attività forniscono informazioni sulle operazioni di hello che sono stati eseguiti i servizi gestione API. In precedenza erano noti come "log di controllo" o "log operativi". Utilizzo di log di attività, è possibile determinare hello "cosa, chi e quando" per le operazioni (PUT, POST, DELETE) eseguite nei servizi gestione API di scrittura. 

> [!NOTE]
> Log attività non includono le operazioni di lettura (GET) o sulle operazioni eseguite hello portale classico di server di pubblicazione o utilizzando hello originale le API di gestione.

È possibile accedere ai log attività del servizio Gestione API o ai log di tutte le risorse di Azure in Monitoraggio di Azure. attività tooview accede al servizio Gestione API:
1. Hello aprirlo portale di Azure.
2. Passare il servizio di gestione API tooyour.
3. Fare clic su **Log attività**.

![Pannello dei log attività][activity-logs-blade]

Per ulteriori informazioni su come toouse metriche, vedere [Panoramica del log attività].

## <a name="alerts"></a>Avvisi
È possibile configurare avvisi tooreceive in base alle metriche e attività di log. Monitoraggio di Azure consente tooconfigure un avviso toodo hello seguenti attiva:

* Inviare una notifica via posta elettronica
* Chiamare un webhook
* Richiamare un'app per la logica di Azure

È possibile configurare regole per gli avvisi nel servizio Gestione API o in Monitoraggio di Azure. tooconfigure usarle in Gestione API: 
1. Hello aprirlo portale di Azure.
2. Passare il servizio di gestione API tooyour.
3. Fare clic su **Regole di avviso**.

![Pannello Regole di avviso][alert-rules-blade]

Per altre informazioni sull'uso degli avvisi, vedere [Panoramica degli avvisi].

## <a name="diagnostic-logs"></a>Log di diagnostica
I log di diagnostica offrono informazioni dettagliate sulle operazioni e gli errori importanti per il controllo e per la risoluzione dei problemi. I log di diagnostica differiscono dai log attività. Log attività forniscono informazioni dettagliate sui operazioni hello che sono state eseguite in risorse di Azure. I log di diagnostica forniscono informazioni approfondite sulle operazioni che la risorsa esegue automaticamente.

Gestione API fornisce attualmente la diagnostica di log (in batch ogni ora) sull'API singoli richiesta con ogni voce con hello seguente struttura:

```
{
    "Tenant": "",
      "DeploymentName": "",
      "time": "",
      "resourceId": "",
      "category": "GatewayLogs",
      "operationName": "Microsoft.ApiManagement/GatewayLogs",
      "durationMs": ,
      "Level": ,
      "properties": "{
          "ApiId": "",
          "OperationId": "",
          "ProductId": "",
          "SubscriptionId": "",
          "Method": "",
          "Url": "",
          "RequestSize": ,
          "ServiceTime": "",
          "BackendMethod": "",
          "BackendUrl": "",
          "BackendResponseCode": ,
          "ResponseCode": ,
          "ResponseSize": ,
          "Cache": "",
          "UserId"
      }"
 }
```

È possibile accedere ai log di diagnostica del servizio Gestione API o ai log di tutte le risorse di Azure in Monitoraggio di Azure. tooview i log di diagnostica nel servizio Gestione API:
1. Hello aprirlo portale di Azure.
2. Passare il servizio di gestione API tooyour.
3. Fare clic su **Log di diagnostica**.

![Pannello Log di diagnostica][diagnostic-logs-blade]

Per ulteriori informazioni su come toouse metriche, vedere [Panoramica del log di diagnostica].

## <a name="next-step"></a>Passaggio successivo

* [introduzione a Monitoraggio di Azure]
* [Panoramica di metriche]
* [Panoramica del log attività]
* [Panoramica del log di diagnostica]
* [Panoramica degli avvisi]

[introduzione a Monitoraggio di Azure]: ../monitoring-and-diagnostics/monitoring-get-started.md
[Panoramica di metriche]: ../monitoring-and-diagnostics/monitoring-overview-metrics.md
[Panoramica del log attività]: ../monitoring-and-diagnostics/monitoring-overview-activity-logs.md
[Panoramica del log di diagnostica]: ../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md
[Panoramica degli avvisi]: ../monitoring-and-diagnostics/insights-alerts-portal.md



[metrics-blade]: ./media/api-management-azure-monitor/api-management-metrics-blade.png
[activity-logs-blade]: ./media/api-management-azure-monitor/api-management-activity-logs-blade.png
[alert-rules-blade]: ./media/api-management-azure-monitor/api-management-alert-rules-blade.png
[diagnostic-logs-blade]: ./media/api-management-azure-monitor/api-management-diagnostic-logs-blade.png
