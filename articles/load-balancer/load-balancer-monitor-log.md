---
title: aaaMonitor operazioni, gli eventi e i contatori per il bilanciamento del carico | Documenti Microsoft
description: "Informazioni su come gli eventi di avviso, tooenable e verificare la presenza di registrazione dello stato di integrità servizio di bilanciamento del carico di Azure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 56656d74-0241-4096-88c8-aa88515d676d
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: ac53c2254e06cad780ad6144c5c30f0085d12576
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-for-azure-load-balancer"></a>Analisi dei log per il servizio di bilanciamento del carico di Azure

È possibile utilizzare diversi tipi di registri in Azure toomanage e risolvere i problemi relativi a servizi di bilanciamento del carico. Alcuni di questi log sono accessibili tramite il portale di hello. Tutti i log possono essere estratti da Archiviazione BLOB di Azure e visualizzati in strumenti differenti, ad esempio Excel e PowerBI. È possibile ulteriori informazioni sui tipi diversi hello dei log dall'elenco di hello seguente.

* **Log di controllo:** è possibile utilizzare [registri di controllo Azure](../monitoring-and-diagnostics/insights-debugging-with-events.md) (precedentemente noto come registri) tooview tutte le operazioni vengono inviati tooyour sottoscrizioni Azure e il relativo stato. I log di controllo sono abilitati per impostazione predefinita e possono essere visualizzati nel portale di Azure hello.
* **I registri eventi di avviso:** è possibile utilizzare questo rasied gli avvisi di log tooview dal servizio di bilanciamento del carico hello. stato Hello di bilanciamento del carico hello verrà raccolti ogni cinque minuti. Questo log viene scritto solo se viene generato un evento di avviso del bilanciamento del carico.
* **I registri di probe di integrità:** è possibile utilizzare questo log tooview problemi per il probe di integrità, ad esempio il numero di hello di istanze del pool di back-end che non ricevano richieste dal bilanciamento del carico hello a causa di errori di probe di integrità. Questo log viene scritto toowhen viene apportata una modifica nello stato di probe di integrità hello.

> [!IMPORTANT]
> Attualmente l'analisi di log funziona solo per i servizi di bilanciamento del carico con connessione Internet. I log sono disponibili solo per le risorse distribuite nel modello di distribuzione di gestione risorse di hello. Non è possibile utilizzare i log per le risorse nel modello di distribuzione classica hello. Per ulteriori informazioni sui modelli di distribuzione hello, vedere [distribuzione classica e gestione di informazioni sulle risorse](../azure-resource-manager/resource-manager-deployment-model.md).

## <a name="enable-logging"></a>Abilitazione della registrazione

La registrazione di controllo viene abilitata automaticamente per ogni risorsa di Resource Manager. È necessario evento tooenable e integrità probe registrazione toostart la raccolta dei dati di hello disponibili tramite tali log. Utilizzare hello registrazione tooenable i passaggi seguenti.

Accedi toohello [portale di Azure](http://portal.azure.com). Prima di procedere, [creare un servizio di bilanciamento del carico](load-balancer-get-started-internet-arm-ps.md) , se non se ne ha già uno.

1. Nel portale di hello, fare clic su **Sfoglia**.
2. Selezionare **Bilanciamento del carico**.

    ![portale - bilanciamento del carico](./media/load-balancer-monitor-log/load-balancer-browse.png)

3. Selezionare un bilanciamento del carico esistente >> **Tutte le impostazioni**.
4. Sul lato destro di hello di hello nella finestra di dialogo Nome hello di bilanciamento del carico hello, scorrere troppo**monitoraggio**, fare clic su **diagnostica**.

    ![portale - impostazioni di bilanciamento del carico](./media/load-balancer-monitor-log/load-balancer-settings.png)

5. In hello **diagnostica** riquadro, in **stato**selezionare **su**.
6. Fare clic su **Account di archiviazione**.
7. In **LOG** selezionare un account di archiviazione esistente o crearne uno nuovo. Utilizzare hello dispositivo di scorrimento toodetermine quanti giorni verranno archiviati i dati di eventi relativi a nei registri eventi di hello. 
8. Fare clic su **Salva**.

    ![Portale - Log di diagnostica](./media/load-balancer-monitor-log/load-balancer-diagnostics.png)

> [!NOTE]
> I log di controllo non richiedono un account di archiviazione separato. utilizzo di Hello di archiviazione per l'evento e l'integrità probe registrazione spese del servizio.

## <a name="audit-log"></a>Log di controllo

Per impostazione predefinita, viene generato il log di controllo di Hello. Hello registri vengono mantenuti per 90 giorni nell'archivio di registri eventi di Azure. Altre informazioni su questi registri leggendo hello [visualizzare eventi e log di controllo](../monitoring-and-diagnostics/insights-debugging-with-events.md) articolo.

## <a name="alert-event-log"></a>Log eventi di avviso

Questo log viene generato solo se è stato abilitato per ogni bilanciamento del carico. gli eventi di Hello vengono registrati in formato JSON e archiviati nell'account di archiviazione hello specificato quando è abilitata la registrazione di hello. Hello Ecco un esempio di un evento.

```json
{
    "time": "2016-01-26T10:37:46.6024215Z",
    "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
    "category": "LoadBalancerAlertEvent",
    "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
    "operationName": "LoadBalancerProbeHealthStatus",
    "properties": {
        "eventName": "Resource Limits Hit",
        "eventDescription": "Ports exhausted",
        "eventProperties": {
            "public ip address": "40.117.227.32"
        }
    }
}
```

Hello JSON output illustrato hello *eventname* proprietà che descrivono il motivo di hello di bilanciamento del carico hello creato un avviso. In questo caso, l'avviso di hello generato è stato scadenza tooTCP esaurimento delle porte causato da un'origine che IP NAT limita (SNAT).

## <a name="health-probe-log"></a>Log del probe di integrità

Questo log viene generato solo se è stato abilitato per ogni bilanciamento del carico, come indicato in precedenza. Hello dati vengono archiviati nell'account di archiviazione hello specificato quando è abilitata la registrazione di hello. Viene creato un contenitore denominato 'insights-log-loadbalancerprobehealthstatus' e viene registrato hello dati seguenti:

```json
{
    "records":[
    {
        "time": "2016-01-26T10:37:46.6024215Z",
        "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
        "category": "LoadBalancerProbeHealthStatus",
        "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
        "operationName": "LoadBalancerProbeHealthStatus",
        "properties": {
            "publicIpAddress": "40.83.190.158",
            "port": "81",
            "totalDipCount": 2,
            "dipDownCount": 1,
            "healthPercentage": 50.000000
        }
    },
    {
        "time": "2016-01-26T10:37:46.6024215Z",
        "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
        "category": "LoadBalancerProbeHealthStatus",
        "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
        "operationName": "LoadBalancerProbeHealthStatus",
        "properties": {
            "publicIpAddress": "40.83.190.158",
            "port": "81",
            "totalDipCount": 2,
            "dipDownCount": 0,
            "healthPercentage": 100.000000
        }
    }]
}
```

l'output JSON Hello Mostra hello proprietà campo hello informazioni di base per lo stato di integrità di hello probe. Hello *dipDownCount* numero totale di hello di istanze vengono visualizzate le proprietà nel back-end di hello che non ricevano il traffico di rete a causa delle risposte probe toofailed.

## <a name="view-and-analyze-hello-audit-log"></a>Visualizzare e analizzare i log di controllo hello

È possibile visualizzare e analizzare i dati di log di controllo utilizzando uno dei seguenti metodi hello:

* **Gli strumenti di Azure:** recuperare informazioni dai log di controllo hello tramite Azure PowerShell, hello interfaccia della riga di comando (CLI di Azure), l'API REST di Azure hello o hello portale di anteprima di Azure. Istruzioni dettagliate per ogni metodo sono descritti in dettaglio in hello [controllare le operazioni con Gestione risorse](../azure-resource-manager/resource-group-audit.md) articolo.
* **Power BI:** se non esiste ancora un account [Power BI](https://powerbi.microsoft.com/pricing) , è possibile crearne uno di prova gratuitamente. Utilizzo di hello [di contenuto log di controllo di Azure per Power BI](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs), è possibile analizzare i dati con i dashboard configurati in precedenza oppure è possibile personalizzare le visualizzazioni toosuit i requisiti.

## <a name="view-and-analyze-hello-health-probe-and-event-log"></a>Visualizzare e analizzare i probe di integrità hello e registro eventi

È necessario un archivio tooyour tooconnect account e recupero delle voci di log hello JSON per i log di probe di evento e l'integrità. Dopo avere scaricato i file JSON hello, è possibile convertirli tooCSV e view in Excel, Power BI o qualsiasi altro strumento di visualizzazione di dati.

> [!TIP]
> Se si ha familiarità con Visual Studio e concetti di base di modificare i valori costanti e variabili in c#, è possibile utilizzare hello [log strumenti convertitore](https://github.com/Azure-Samples/networking-dotnet-log-converter) disponibili da GitHub.

## <a name="additional-resources"></a>Risorse aggiuntive

* [visualizzazione dei log di controllo di Azure con Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) .
* [visualizzazione e analisi dei log di controllo di Azure in Power BI e altri strumenti](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) .

## <a name="next-steps"></a>Passaggi successivi

[Informazioni sui probe di bilanciamento del carico](load-balancer-custom-probe-overview.md)
