---
title: aaaView dati analitici di App Web di Azure | Documenti Microsoft
description: "È possibile utilizzare informazioni dettagliate di hello Azure Web App Analitica soluzione toogain sull'App Web di Azure raccogliendo metriche tra tutte le risorse di App Web di Azure."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 20ff337f-b1a3-4696-9b5a-d39727a94220
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: banders
ms.openlocfilehash: 7e9725f95c9faf01da89184975ad5444dd19ff95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="view-analytic-data-for-metrics-across-all-your-azure-web-app-resources"></a>Visualizzare i dati di analisi per le metriche di tutte le risorse app Web di Azure

![Simbolo di App Web](./media/log-analytics-azure-web-apps-analytics/azure-web-apps-analytics-symbol.png)  
Hello soluzione Analitica di App Web di Azure (anteprima) offre informazioni approfondite del [App Web di Azure](../app-service-web/app-service-web-overview.md) raccogliendo metriche tra tutte le risorse di App Web di Azure. Con la soluzione hello, è possibile analizzare e cercare i dati di metrica risorsa app web.

Utilizza soluzione hello, è possibile visualizzare il:

- App Web principale con tempo di risposta massimo hello
- Numero di richieste tra le app Web, incluse le richieste riuscite e non riuscite
- Principali app Web con il maggior traffico in ingresso e in uscita
- Principali piani di servizio con utilizzo elevato di memoria e CPU
- Operazioni del log attività di App Web di Azure

## <a name="connected-sources"></a>Origini connesse

A differenza della maggior parte delle altre soluzioni di Log Analytics, i dati per App Web di Azure non vengono raccolti dagli agenti. Tutti i dati utilizzati dalla soluzione hello proviene direttamente da Azure.

| Origine connessa | Supportato | Descrizione |
| --- | --- | --- |
| [Agenti di Windows](log-analytics-windows-agents.md) | No | soluzione Hello non raccoglie informazioni dagli agenti di Windows. |
| [Agenti Linux](log-analytics-linux-agents.md) | No | soluzione Hello non raccoglie informazioni dagli agenti Linux. |
| [Gruppo di gestione SCOM](log-analytics-om-agents.md) | No | soluzione Hello non raccoglie informazioni dagli agenti in un gruppo di gestione SCOM connesso. |
| [Account di archiviazione di Azure](log-analytics-azure-storage.md) | No | soluzione di Hello non non informazioni sulla raccolta dall'archiviazione di Azure. |

## <a name="prerequisites"></a>Prerequisiti

- tooaccess informazioni sulle metriche di risorsa App Web di Azure, è necessario disporre di una sottoscrizione di Azure.

## <a name="configuration"></a>Configurazione

Eseguire hello seguente soluzione Azure Web App Analitica di passaggi tooconfigure hello per le aree di lavoro.

1. Abilitare soluzioni Azure Web App Analitica hello [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureWebAppsAnalyticsOMS?tab=Overview) o tramite il processo di hello descritto in [soluzioni aggiungere Log Analitica da hello Solutions Gallery](log-analytics-add-solutions.md).
2. [Abilitare tooOMS registrazione metriche di risorse di Azure con PowerShell](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell).

soluzione Azure Web App Analitica Hello raccoglie due set di metriche da Azure:

- Metriche di App Web di Azure
  - Working set della memoria medio
  - Tempo medio di risposta
  - Byte ricevuti/inviati
  - Tempo CPU
  - Richieste
  - Working set della memoria
  - Httpxxx
- Metriche del piano di servizio app
  - Byte ricevuti/inviati
  - Percentuale CPU
  - Lunghezza coda disco
  - Lunghezza coda HTTP
  - Percentuale memoria

Le metriche del piano di servizio app vengono raccolte solo se si usa un piano di servizio dedicato. Questo non si applica toofree o piani di servizio App condiviso.

Se si aggiunge una soluzione di hello tramite il portale di OMS hello, si noterà hello seguente riquadro. È necessario troppo[abilitare tooOMS registrazione metriche di risorse di Azure con PowerShell](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell).

![Notifica di esecuzione della valutazione](./media/log-analytics-azure-web-apps-analytics/performing-assessment.png)

Dopo aver configurato la soluzione hello, dati devono avviare il flusso dell'area di lavoro tooyour entro 15 minuti.

## <a name="using-hello-solution"></a>Utilizzo di soluzione hello

Quando si aggiunge l'area di lavoro tooyour soluzione Azure Web App Analitica hello, hello **Azure Web App Analitica** riquadro viene aggiunto il dashboard di panoramica tooyour. Questo riquadro Visualizza un conteggio del numero di hello di App Web di Azure che soluzione hello disponga di accesso tooin la sottoscrizione di Azure.

![Riquadro di Analisi app Web di Azure](./media/log-analytics-azure-web-apps-analytics/azure-web-apps-analytics-tile.png)

### <a name="view-azure-web-apps-analytics-information"></a>Visualizzare le informazioni di Analisi app Web di Azure

Fare clic su hello **Azure Web App Analitica** riquadro tooopen hello **Azure Web App Analitica** dashboard. dashboard Hello include pannelli hello in hello nella tabella seguente. Ogni pannello elenca backup tooten elementi corrispondenti ai criteri del pannello per hello specificato intervallo di ambito e tempo. È possibile eseguire una ricerca di log che restituisce tutti i record facendo **tutti** nella parte inferiore di hello del pannello hello oppure facendo clic sull'intestazione di blade hello.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

| Colonna | Descrizione |
| --- | --- |
| App Web di Azure |   |
| Tendenze richieste app Web | Mostra un grafico a linee di tendenza di richiesta Web App per l'intervallo di date hello selezionato hello e Mostra un elenco di richieste web dieci superiore hello. Fare clic su una ricerca di log per hello riga grafico toorun<code>Type=AzureMetrics ResourceId=*"/MICROSOFT.WEB/SITES/"* (MetricName=Requests OR MetricName=Http*) &#124; measure avg(Average) by MetricName interval 1HOUR</code> <br>Fare clic su un toorun di elemento di richiesta web, una ricerca di log per la tendenza di metrica richiesta di web hello che lo richiedono. |
| Tempo di risposta app Web | Mostra un grafico a linee hello App Web del tempo di risposta per l'intervallo di date hello selezionato. Inoltre visualizza un elenco di hello prime dieci Web risposta App volte. Fare clic su una ricerca di log per hello grafico toorun<code>Type:AzureMetrics ResourceId=*"/MICROSOFT.WEB/SITES/"* MetricName="AverageResponseTime" &#124; measure avg(Average) by Resource interval 1HOUR</code><br> Fare clic su un toorun App Web di una ricerca log restituzione tempi di risposta per hello App Web. |
| Traffico app Web | Viene illustrato un grafico a linee per il traffico Web Apps, in MB ed elenca inizio hello traffico Web App. Fare clic su una ricerca di log per hello grafico toorun<code>Type:AzureMetrics ResourceId=*"/MICROSOFT.WEB/SITES/"*  MetricName=BytesSent OR BytesReceived &#124; measure sum(Average) by Resource interval 1HOUR</code><br> Mostra tutte le app Web con traffico per hello ultimo minuto. Fare clic su un toorun App Web, una ricerca di log che mostra byte ricevuti e inviati per hello App Web. |
| Piani di servizio app di Azure |   |
| Piani di servizio app con utilizzo della CPU &gt; 80% | Mostra hello totale App piani di servizio con l'utilizzo della CPU maggiore di 80% e gli elenchi hello piani di servizio App primi 10 per l'utilizzo della CPU. Fare clic su una ricerca di log per hello area totale toorun<code>Type=AzureMetrics ResourceId=*"/MICROSOFT.WEB/SERVERFARMS/"* MetricName=CpuPercentage &#124; measure Avg(Average) by Resource</code><br> Mostra un elenco dei piani di servizio app con l'utilizzo medio della CPU. Fare clic su un piano di servizio App toorun una ricerca di log con il relativo utilizzo medio della CPU. |
| Piani di servizio app con utilizzo della memoria &gt; 80% | Mostra hello totale App piani di servizio con utilizzo di memoria maggiore di 80% e gli elenchi hello piani di servizio App primi 10 per l'utilizzo della memoria. Fare clic su una ricerca di log per hello area totale toorun<code>Type=AzureMetrics ResourceId=*"/MICROSOFT.WEB/SERVERFARMS/"* MetricName=MemoryPercentage &#124; measure Avg(Average) by Resource</code><br> Mostra un elenco dei piani di servizio app con l'utilizzo medio della memoria. Fare clic su un piano di servizio App toorun una ricerca di log con il relativo utilizzo medio della memoria. |
| Log attività di App Web di Azure |   |
| Audit attività di App Web di Azure | Mostra il numero totale di App Web con di hello [log attività](log-analytics-activity.md) e gli elenchi di hello operazioni del log attività primi 10. Fare clic su una ricerca di log per hello area totale toorun<code>Type=AzureActivity ResourceProvider= "Azure Web Sites" &#124; measure count() by OperationName</code><br> Mostra un elenco di hello operazioni del log attività. Fare clic su un toorun di operazione log attività una ricerca di log che elenca i record di hello per operazione hello. |



### <a name="azure-web-apps"></a>App Web di Azure 

Nel dashboard di hello, è possibile drill-down tooget più approfondita delle metriche di App Web. Il primo set di pannelli Mostra tendenza hello delle richieste di applicazioni Web hello, numero di errori (ad esempio, HTTP404), il traffico e tempo medio di risposta nel tempo. Mostra anche una suddivisione delle metriche per le diverse app Web.

![v (App Web di Azure)](./media/log-analytics-azure-web-apps-analytics/web-apps-dash01.png)

Un motivo principale per visualizzare i dati è in modo che sia possibile identificare un'App Web con il tempo di risposta e ricercare causa principale di toofind hello. Un limite di soglia viene inoltre toohelp applicate per che identificare più facilmente hello quelli con problemi.

- Le app Web in rosso hanno tempi di risposta superiori a 1 secondo.
- Le app Web in arancione hanno tempi di risposta superiori a 0,7 secondi e inferiori a 1 secondo.
- Le app Web in verde hanno tempi di risposta inferiori a 0,7 secondi.

In hello dopo l'immagine del log di esempio ricerca, è possibile vedere che hello *anugup3* app web è un tempo di risposta molto più elevato rispetto a hello altre App web.

![Esempio di ricerca log](./media/log-analytics-azure-web-apps-analytics/web-app-search-example.png)

### <a name="app-service-plans"></a>Piani di servizio app

Se si usano piani di servizio dedicati, è anche possibile raccogliere le metriche per i piani di servizio app. Questa vista mostra i piani di servizio app con utilizzo elevato di memoria o CPU (&gt; 80%). Viene inoltre hello servizi App superiore con utilizzo elevato di memoria o CPU. Analogamente, un limite di soglia è toohelp applicate per che identificare più facilmente hello quelli con problemi.

- I piani di servizio app in rosso hanno un utilizzo di CPU/memoria superiore all'80%.
- I piani di servizio app in arancione hanno un utilizzo di CPU/memoria superiore al 60% e inferiore all'80%.
- I piani di servizio app in verde hanno un utilizzo di CPU/memoria inferiore al 60%.

![Pannelli della sezione Azure App Service Plans (Piani di servizio app di Azure)](./media/log-analytics-azure-web-apps-analytics/web-apps-dash02.png)

## <a name="azure-web-apps-log-searches"></a>Ricerche log di App Web di Azure

Hello **query di elenco di ricerca più diffusi Azure Web App** Mostra hello tutti i relativi log attività per le app Web, che offre informazioni approfondite operazioni hello che sono state eseguite in risorse di applicazioni Web. Inoltre, Elenca tutti hello relativi a operazioni e il numero di hello di volte in cui si sono verificate.

Utilizzo delle query di ricerca log hello come punto di partenza, è possibile creare un avviso. Ad esempio, è necessario toocreate un avviso quando il tempo di risposta medio della metrica è maggiore di 1 ogni secondo.

## <a name="next-steps"></a>Passaggi successivi

- Creare un [avviso](log-analytics-alerts-creating.md) per una metrica specifica.
- Utilizzare [ricerca nei Log](log-analytics-log-searches.md) tooview informazioni dai registri attività.
