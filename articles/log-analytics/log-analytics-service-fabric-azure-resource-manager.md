---
title: applicazioni di Service Fabric con Log Analitica aaaAssess hello portale di Azure | Documenti Microsoft
description: "È possibile utilizzare soluzioni di Service Fabric hello in Analitica Log utilizzando hello tooassess portale Azure hello rischio e l'integrità delle applicazioni di Service Fabric, micro servizi, nodi e i cluster."
services: log-analytics
documentationcenter: 
author: niniikhena
manager: jochan
editor: 
ms.assetid: 9c91aacb-c48e-466c-b792-261f25940c0c
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: nini
ms.openlocfilehash: 891c7f6e5ed511ac18599bdc280ab3dc09700fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="assess-service-fabric-applications-and-micro-services-with-hello-azure-portal"></a>Valutare micro-servizi con hello portale di Azure e le applicazioni di Service Fabric

> [!div class="op_single_selector"]
> * [Gestione risorse](log-analytics-service-fabric-azure-resource-manager.md)
> * [PowerShell](log-analytics-service-fabric.md)
>
>

![Simbolo di Service Fabric](./media/log-analytics-service-fabric/service-fabric-assessment-symbol.png)

In questo articolo viene descritto come toouse hello soluzione Service Fabric in Log Analitica toohelp identificare e risolvere i problemi del cluster di Service Fabric.

Hello soluzione Service Fabric utilizza i dati di diagnostica di Azure delle macchine virtuali dell'infrastruttura di servizio, raccogliendo i dati dalle tabelle di Azure WAD. Successivamente, Log Analytics legge gli eventi del framework di Service Fabric, tra cui: **Eventi del servizio affidabile**, **Eventi relativi agli attori**, **Eventi operativi** ed **Eventi ETW personalizzati**. Con dashboard soluzione hello, si tooview in grado di problemi e degli eventi di Service Fabric nell'ambiente in uso.

tooget avviato con la soluzione hello, è necessario tooconnect Service Fabric cluster tooa Log Analitica area di lavoro. Ecco tre scenari tooconsider:

1. Se il cluster di Service Fabric non sono stati distribuiti, utilizzare i passaggi di hello in ***distribuire un'area di lavoro Cluster di Service Fabric connesso Analitica Log tooa*** toodeploy un nuovo cluster e aver configurato tooreport tooLog Analitica.
2. Se è necessario toocollect contatori delle prestazioni da toouse l'host altre soluzioni OMS, ad esempio sicurezza il cluster di infrastruttura del servizio, seguire passaggi hello ***distribuire un'area di lavoro Log Analitica tooa Cluster di Service Fabric connesso con l'estensione della macchina virtuale installato.***
3. Se si hanno già distribuito il cluster di Service Fabric e si desidera tooconnect è tooLog Analitica, seguire i passaggi hello ***aggiungendo un tooLog di account di archiviazione esistente Analitica.***

## <a name="deploy-a-service-fabric-cluster-connected-tooa-log-analytics-workspace"></a>Distribuire un'area di lavoro di Cluster di Service Fabric connesso tooa Analitica di Log.
Questo modello hello seguenti:

1. Consente di distribuire un'area di lavoro Log Analitica di tooa cluster già connessi di Azure Service Fabric. È necessario hello opzione toocreate una nuova area di lavoro durante la distribuzione modello hello o nome hello input di un'area di lavoro Log Analitica già esistente.
2. Aggiunge l'area di lavoro hello archiviazione diagnostica account toohello Analitica di Log.
3. Consente di soluzioni di Service Fabric hello nell'area di lavoro Log Analitica.

[![Distribuire tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-oms%2F%2Fazuredeploy.json)

Dopo aver selezionato hello distribuire pulsante sopra riportato, hello apre portali Azure con i parametri per si tooedit. Essere toocreate che un nuovo gruppo di risorse, se l'input di un nuovo nome dell'area di lavoro Analitica Log:

![Service Fabric](./media/log-analytics-service-fabric/2.png)

![Service Fabric](./media/log-analytics-service-fabric/3.png)

Accettare i termini legali specifici hello e fare clic su **crea** distribuzione hello toostart. Al termine della distribuzione di hello, si dovrebbe vedere nuova area di lavoro hello e cluster creato e hello WADServiceFabric * eventi, WADWindowsEventLogs e WADETWEvent tabelle aggiunte:

![Service Fabric](./media/log-analytics-service-fabric/4.png)

## <a name="deploy-a-service-fabric-cluster-connected-tooa-log-analytics-workspace-with-vm-extension-installed"></a>Distribuire un'area di lavoro di Cluster di Service Fabric connesso tooa Analitica Log con l'estensione della macchina virtuale installato.

Questo modello hello seguenti:

1. Consente di distribuire un'area di lavoro Log Analitica di tooa cluster già connessi di Azure Service Fabric. È possibile creare una nuova area di lavoro o usarne una esistente.
2. Aggiunge l'area di lavoro hello archiviazione diagnostica account toohello Analitica di Log.
3. Consente di soluzioni di Service Fabric hello nell'area di lavoro Log Analitica hello.
4. Installa l'estensione hello MMA agente in ogni scalabilità della macchina virtuale impostato nel cluster di Service Fabric. Agente hello MMA installato, le metriche delle prestazioni in grado di tooview si sta i nodi.

[![Distribuire tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-vmss-oms%2F%2Fazuredeploy.json)

Di seguito hello stessi passaggi illustrati in precedenza, i parametri necessari hello input e avviano una distribuzione. Verrà visualizzato nuovamente nuova area di lavoro hello del cluster e create tutte le tabelle di diagnostica AZURE:

![Service Fabric](./media/log-analytics-service-fabric/5.png)

### <a name="viewing-performance-data"></a>Visualizzazione dei dati sulle prestazioni

tooview dati delle prestazioni dai nodi:


[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

- Avviare l'area di lavoro Log Analitica hello da hello portale di Azure.
  ![Service Fabric](./media/log-analytics-service-fabric/6.png)
- Passare tooSettings hello riquadro a sinistra e selezionare dati >> i contatori delle prestazioni di Windows >> "Aggiungi hello selezionato i contatori delle prestazioni": ![Service Fabric](./media/log-analytics-service-fabric/7.png)
- Nella ricerca di Log, utilizzare hello seguente query toodelve nelle metriche principali relative i nodi:

    a. Confronto hello utilizzo medio della CPU in tutti i nodi di hello toosee di un'ora ultimo i nodi che hanno problemi e in quale intervallo di tempo un nodo ha un picco:

    ```
    Type=Perf ObjectName=Processor CounterName="% Processor Time"|measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/10.png)

    b. Visualizzare i grafici a linee simili relativi alla memoria disponibile in ciascun nodo con questa query:

    ```
    Type=Perf ObjectName=Memory CounterName="Available MBytes Memory" | measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    tooview un elenco di tutti i nodi, che mostra il valore medio hello esatto per MByte disponibili per ogni nodo, usare questa query:

    ```
    Type=Perf (ObjectName=Memory) (CounterName="Available MBytes") | measure avg(CounterValue) by Computer
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/11.png)

    c. In caso di hello che si desidera toodrill verso il basso in un nodo specifico esaminando Media oraria hello, utilizzo della CPU minimo, massimo e di 75 percentile, si è in grado di toodo il problema, utilizzare questa query (sostituire campo del Computer):

    ```
    Type=Perf CounterName="% Processor Time" InstanceName=_Total Computer="BaconDC01.BaconLand.com"| measure min(CounterValue), avg(CounterValue), percentile75(CounterValue), max(CounterValue) by Computer Interval 1HOUR
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/12.png)

Altre informazioni sulle metriche delle prestazioni nel Log Analitica a hello [Operations Management Suite blog](https://blogs.technet.microsoft.com/msoms/tag/metrics/).


## <a name="adding-an-existing-storage-account-toolog-analytics"></a>Aggiunta di un tooLog di account di archiviazione esistente Analitica

Questo modello aggiunge semplicemente l'archiviazione account tooa nuovo o esistente Log Analitica area di lavoro esistente.

[![Distribuire tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Foms-existing-storage-account%2Fazuredeploy.json)

> [!NOTE]
> La selezione di un gruppo di risorse, se si utilizza un'area di lavoro Log Analitica già esistente, selezionare "Usa esistente" e cercare il gruppo di risorse hello contenente l'area di lavoro di hello Analitica di Log. Altrimenti, crearne uno nuovo.
> ![Service Fabric](./media/log-analytics-service-fabric/8.png)
>
>

Dopo la distribuzione di questo modello, sarà in grado di toosee hello archiviazione account connesso tooyour Log Analitica dell'area di lavoro. In questo caso, aggiunto uno più storage account toohello Exchange area di lavoro che è stato creato in precedenza.
![Service Fabric](./media/log-analytics-service-fabric/9.png)

## <a name="view-service-fabric-events"></a>Visualizzare gli eventi di Service Fabric

Una volta completate le distribuzioni di hello e hello soluzione Service Fabric è stata abilitata nell'area di lavoro, selezionare hello **Service Fabric** riquadro nel dashboard di hello Analitica Log toolaunch portale hello Service Fabric. dashboard Hello sono incluse colonne hello hello nella tabella seguente. Ogni colonna elenca gli eventi di 10 superiore di hello associando conteggio che i criteri della colonna per hello specificato intervallo di tempo. È possibile eseguire una ricerca di log che fornisce l'intero elenco hello facendo **tutti** hello in basso a destra di ogni colonna, oppure facendo clic sull'intestazione di colonna hello.

| **Evento di Service Fabric** | **description** |
| --- | --- |
| Errori rilevanti |Visualizzazione dei problemi, ad esempio RunAsyncFailures RunAsynCancellations e Node Downs. |
| Eventi operativi |Eventi operativi rilevanti, ad esempio l'aggiornamento dell'applicazione e le distribuzioni. |
| Eventi del servizio affidabile |Eventi del servizio affidabile rilevanti come Runasyncinvocations. |
| Eventi relativi agli attori |Gli eventi relativi agli attori rilevanti generati dai micro-servizi, ad esempio le eccezioni generate da un metodo attore, le attivazioni e disattivazioni relative all'attore e così via. |
| Eventi dell'applicazione |Tutti gli eventi ETW personalizzati che sono stati generati dalle applicazioni. |

![Dashboard di Service Fabric](./media/log-analytics-service-fabric/sf3.png)

![Dashboard di Service Fabric](./media/log-analytics-service-fabric/sf4.png)

Hello nella tabella seguente illustra i metodi di raccolta dati e altri dettagli sulla modalità di raccolta dati per l'infrastruttura del servizio.

| Piattaforma | Agente diretto | Agente di Operations Manager | Archiviazione di Azure | È necessario Operations Manager? | Dati dell'agente Operations Manager inviati con il gruppo di gestione | Frequenza della raccolta |
| --- | --- | --- | --- | --- | --- | --- |
| Windows |  |  | &#8226; |  |  |10 minuti |

> [!NOTE]
> È possibile modificare l'ambito di hello di questi eventi in una soluzione di Service Fabric hello facendo **i dati basati su ultimi 7 giorni** nella parte superiore di hello del dashboard hello. È inoltre possibile visualizzare gli eventi generati all'interno di hello ultimi sette giorni, un giorno o sei ore. In alternativa, è possibile selezionare **personalizzato** toospecify un intervallo di date personalizzato.
>
>

## <a name="next-steps"></a>Passaggi successivi

* Utilizzare [ricerche nei Log nel Log Analitica](log-analytics-log-searches.md) tooview in dettaglio i dati di evento di Service Fabric.
