---
title: aaaCapacity e soluzione di prestazioni in Azure Log Analitica | Documenti Microsoft
description: "Hello di utilizzo della capacità e la soluzione di prestazioni in toohelp Log Analitica comprendere hello capacità dei server Hyper-V."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 51617a6f-ffdd-4ed2-8b74-1257149ce3d4
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: banders
ms.openlocfilehash: c47bb1e8bb9d4460b0241e89a616f3b356844b08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="plan-hyper-v-virtual-machine-capacity-with-hello-capacity-and-performance-solution-preview"></a>Pianificare la capacità di macchine virtuali Hyper-V con capacità hello ed Esplora prestazioni (anteprima)

![Simbolo di Capacità e prestazioni](./media/log-analytics-capacity/capacity-solution.png)

È possibile utilizzare hello capacità e soluzione di prestazioni in toohelp Log Analitica comprendere hello capacità dei server Hyper-V. soluzione Hello fornisce approfondite ambiente Hyper-V mostrando hello utilizzo complessivo (CPU, memoria e disco) di host hello e hello macchine virtuali in esecuzione negli host Hyper-V. Vengono raccolte le metriche per CPU, memoria e dischi tra host e macchine virtuali hello in esecuzione su di essi.

soluzione Hello:

-   Visualizza gli host con l'utilizzo più alto e più basso di CPU e memoria
-   Visualizza le VM con l'utilizzo più alto e più basso di CPU e memoria
-   Visualizza le VM con l'utilizzo più alto e più basso di operazioni di I/O al secondo e velocità effettiva
-   Visualizza le VM in esecuzione nei diversi host
-   Mostra primi dischi con velocità effettiva elevata, IOPS, hello e latenza in cluster i volumi condivisi
- Consente di toocustomize e filtrare in base ai gruppi

> [!NOTE]
> versione precedente di Hello di hello capacità ed Esplora prestazioni chiamato gestione delle capacità necessarie sia System Center Operations Manager e System Center Virtual Machine Manager. Questa soluzione aggiornata non prevede tali dipendenze.


## <a name="connected-sources"></a>Origini connesse

Hello nella tabella seguente descrive hello connesso origini supportate da questa soluzione.

| Origine connessa | Supporto | Descrizione |
|---|---|---|
| [Agenti Windows](log-analytics-windows-agents.md) | Sì | soluzione Hello raccoglie le informazioni di dati di capacità e prestazioni dagli agenti di Windows. |
| [Agenti Linux](log-analytics-linux-agents.md) | No    | soluzione Hello non raccoglie informazioni di dati di capacità e prestazioni dagli agenti Linux diretti.|
| [Gruppo di gestione SCOM](log-analytics-om-agents.md) | Sì |soluzione Hello raccoglie i dati di capacità e prestazioni dagli agenti in un gruppo di gestione SCOM connesso. Una connessione diretta da hello SCOM agente tooOMS non è necessaria. Dati viene inoltrati dal repository OMS toohello di hello gestione gruppo.|
| [Account di archiviazione di Azure](log-analytics-azure-storage.md) | No | Archiviazione di Azure non include dati di capacità e prestazioni.|

## <a name="prerequisites"></a>Prerequisiti

- Gli agenti Windows o Operations Manager devono essere installati in host Hyper-V Windows Server 2012 o versione successiva, non in macchine virtuali.


## <a name="configuration"></a>Configurazione

Eseguire hello seguente passaggio tooadd hello capacità e prestazioni soluzione tooyour dell'area di lavoro.

- Aggiungere hello capacità e prestazioni soluzione tooyour area di lavoro OMS tramite il processo di hello descritto in [soluzioni aggiungere Log Analitica da hello Solutions Gallery](log-analytics-add-solutions.md).

## <a name="management-packs"></a>Management Pack

Se il gruppo di gestione di SCOM è l'area di lavoro OMS tooyour connesso, hello seguenti management pack verrà quindi installata in SCOM quando si aggiunge questa soluzione. Per questi Management Pack non è richiesta alcuna configurazione o manutenzione.

- Microsoft.IntelligencePacks.CapacityPerformance

evento 1201 Hello è simile a:


```
New Management Pack with id:"Microsoft.IntelligencePacks.CapacityPerformance", version:"1.10.3190.0" received.
```

Quando viene aggiornato hello soluzione capacità e prestazioni, verrà modificato il numero di versione di hello.

Per ulteriori informazioni sulla modalità di aggiornamento dei management pack di soluzione, vedere [tooLog connettere Operations Manager Analitica](log-analytics-om-agents.md).

## <a name="using-hello-solution"></a>Utilizzo di soluzione hello

Quando si aggiunge hello capacità e prestazioni soluzione tooyour dell'area di lavoro, hello capacità e prestazioni viene aggiunto toohello dashboard Panoramica. Questo riquadro Visualizza un conteggio del numero di hello di host Hyper-V attualmente attivo e il numero di hello di macchine virtuali attive che sono stati monitorati per hello periodo di tempo selezionato.

![Riquadro Capacity and Performance](./media/log-analytics-capacity/capacity-tile.png)


### <a name="review-utilization"></a>Esaminare l'utilizzo

Fare clic su hello capacità e prestazioni riquadro tooopen hello capacità e prestazioni del dashboard. dashboard Hello sono incluse colonne hello hello nella tabella seguente. Ogni colonna sono elencati i tooten elementi corrispondenti ai criteri della colonna per hello specificato intervallo di ambito e tempo. È possibile eseguire una ricerca di log che restituisce tutti i record facendo **tutti** nella parte inferiore di hello della colonna hello o facendo clic sull'intestazione di colonna hello.

- **Host**
    - **Utilizzo della CPU host** illustra una tendenza di utilizzo della CPU hello del computer host e un elenco di host, in base al periodo di tempo selezionato hello con interfaccia grafica. Passare il mouse su hello riga grafico tooview i dettagli per uno specifico punto nel tempo. Fare clic su hello grafico tooview altre informazioni, vedere ricerca nei log. Fare clic su qualsiasi ricerca nei log tooopen nome host e visualizzare i dettagli sul contatore della CPU per le macchine virtuali ospitate.
    - **Utilizzo di memoria host** viene mostrata una tendenza di utilizzo della memoria hello del computer host e un elenco di host, in base al periodo di tempo selezionato hello grafica. Passare il mouse su hello riga grafico tooview i dettagli per uno specifico punto nel tempo. Fare clic su hello grafico tooview altre informazioni, vedere ricerca nei log. Fare clic su qualsiasi host nome tooopen log ricerca e visualizzazione contatore dettagli relativi alla memoria per le macchine virtuali ospitate.
- **Macchine virtuali**
    - **Utilizzo della CPU di VM** viene mostrata una tendenza con interfaccia grafica di utilizzo della CPU hello delle macchine virtuali e un elenco di macchine virtuali, basate su hello periodo di tempo selezionato. Passare il mouse su hello riga grafico tooview i dettagli per uno specifico punto nel tempo per hello primi 3 macchine virtuali. Fare clic su hello grafico tooview altre informazioni, vedere ricerca nei log. Fare clic su qualsiasi ricerca nei log tooopen nome macchina virtuale e visualizzare i dettagli di contatore CPU aggregati per hello VM.
    - **Utilizzo della memoria VM** viene mostrata una tendenza grafica di utilizzo della memoria hello delle macchine virtuali e un elenco di macchine virtuali, basate su hello periodo di tempo selezionato. Passare il mouse su hello riga grafico tooview i dettagli per uno specifico punto nel tempo per hello primi 3 macchine virtuali. Fare clic su hello grafico tooview altre informazioni, vedere ricerca nei log. Fare clic su qualsiasi ricerca nei log tooopen nome macchina virtuale e visualizzare i dettagli sul contatore memoria aggregati per hello macchina virtuale.
    - **Totale di IOPS disco VM** illustra una tendenza con interfaccia grafica di hello totale su disco di IOPS per macchine virtuali e un elenco di macchine virtuali con hello IOPS per ogni tipo, nel periodo di tempo selezionato hello. Passare il mouse su hello riga grafico tooview i dettagli per uno specifico punto nel tempo per hello primi 3 macchine virtuali. Fare clic su hello grafico tooview altre informazioni, vedere ricerca nei log. Fare clic su qualsiasi ricerca nei log tooopen nome macchina virtuale e una visualizzazione disco aggregato IOPS contatore i dettagli per hello macchina virtuale.
    - **Velocità effettiva del disco totale VM** Mostra una tendenza grafica della velocità effettiva totale del disco hello per le macchine virtuali e un elenco di macchine virtuali con una velocità effettiva totale del disco hello per ogni, hello in base a periodo di tempo selezionato. Passare il mouse su hello riga grafico tooview i dettagli per uno specifico punto nel tempo per hello primi 3 macchine virtuali. Fare clic su hello grafico tooview altre informazioni, vedere ricerca nei log. Fare clic su qualsiasi ricerca nei log tooopen nome macchina virtuale e visualizzare i dettagli sul contatore velocità effettiva aggregata totale su disco per hello macchina virtuale.
- **Volumi condivisi cluster**
    - **Velocità effettiva totale** Mostra somma hello di entrambi legge e scrive su volumi condivisi cluster.
    - **Totale di IOPS** somma hello Mostra operazioni di input/output al secondo in volumi condivisi cluster.
    - **Latenza totale** Mostra latenza totale hello in volumi condivisi cluster.
- **Ospitare densità** riquadro superiore di hello Mostra numero totale di hello della soluzione toohello disponibile host e macchine virtuali. Fare clic su dettagli aggiuntivi tooview riquadro superiore di hello nella ricerca nei log. Vengono elencati anche tutti gli host e numero di hello di macchine virtuali ospitate. Fare clic su un host di toodrill i risultati della VM hello in una ricerca di log.


![Pannello Host del dashboard](./media/log-analytics-capacity/dashboard-hosts.png)

![Pannello Macchine virtuali del dashboard](./media/log-analytics-capacity/dashboard-vms.png)


### <a name="evaluate-performance"></a>Valutare le prestazioni

Ambienti di produzione differiscono notevolmente dalle tooanother di un'organizzazione. Anche i carichi di lavoro di capacità e prestazioni possono dipendere da come vengono eseguite le VM e da che cosa si considera normale. Ambiente tooyour probabilmente non si applichino toohelp procedure specifiche misurare le prestazioni. Pertanto, più generalizzato indicazioni è più adatta toohelp. Microsoft pubblica una serie di istruzioni articoli toohelp misurare le prestazioni.

toosummarize, hello soluzione consente di raccogliere dati di prestazioni e capacità da diverse origini, tra cui i contatori delle prestazioni. Utilizzare i dati di capacità e prestazioni presentati in varie aree di soluzione hello e confrontare i risultati toothose in hello [misurazione delle prestazioni in Hyper-V](https://msdn.microsoft.com/library/cc768535.aspx) articolo. Anche se articolo hello è stato pubblicato qualche tempo fa, linee guida, considerazioni e le metriche hello sono ancora valide. articolo Hello contiene risorse utili tooother di collegamenti.


## <a name="sample-log-searches"></a>Ricerche di log di esempio

Hello nella tabella seguente fornisce ricerche log di esempio per i dati di capacità e prestazioni raccolti e calcolato per questa soluzione.

| Query | Descrizione |
|---|---|
| Tutte le configurazioni di memoria degli host | <code>Type=Perf ObjectName="Capacity and Performance" CounterName="Host Assigned Memory MB" &#124; measure avg(CounterValue) as MB by InstanceName</code> |
| Tutte le configurazioni di memoria delle macchine virtuali | <code>Type=Perf ObjectName="Capacity and Performance" CounterName="VM Assigned Memory MB" &#124; measure avg(CounterValue) as MB by InstanceName</code> |
| Scomposizione totale IOPS dei dischi tra tutte le macchine virtuali | <code>Type=Perf ObjectName="Capacity and Performance" (CounterName="VHD Reads/s" OR CounterName="VHD Writes/s") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |
| Scomposizione totale velocità effettiva dei dischi tra tutte le macchine virtuali | <code>Type=Perf ObjectName="Capacity and Performance" (CounterName="VHD Read MB/s" OR CounterName="VHD Write MB/s") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |
| Scomposizione totale IOPS tra tutti i CSV | <code>Type=Perf ObjectName="Capacity and Performance" (CounterName="CSV Reads/s" OR CounterName="CSV Writes/s") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |
| Scomposizione totale velocità effettiva tra tutti i CSV | <code>Type=Perf ObjectName="Capacity and Performance" (CounterName="CSV Read MB/s" OR CounterName="CSV Write MB/s") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |
| Scomposizione totale latenza tra tutti i CSV | <code> Type=Perf ObjectName="Capacity and Performance" (CounterName="CSV Read Latency" OR CounterName="CSV Write Latency") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |

>[!NOTE]
> Se l'area di lavoro è stato aggiornato toohello [Analitica Log nuovo linguaggio di query](log-analytics-log-search-upgrade.md), quindi hello sopra query modificherebbe toohello seguente.

> | Query | Descrizione |
|:--- |:--- |
| Tutte le configurazioni di memoria degli host | Perf &#124; where ObjectName == "Capacity and Performance" and CounterName == "Host Assigned Memory MB" &#124; summarize MB = avg(CounterValue) by InstanceName |
| Tutte le configurazioni di memoria delle macchine virtuali | Perf &#124; where ObjectName == "Capacity and Performance" and CounterName == "VM Assigned Memory MB" &#124; summarize MB = avg(CounterValue) by InstanceName |
| Scomposizione totale IOPS dei dischi tra tutte le macchine virtuali | Perf &#124; where ObjectName == "Capacity and Performance" and (CounterName == "VHD Reads/s" or CounterName == "VHD Writes/s") &#124; summarize AggregatedValue = avg(CounterValue) by bin(TimeGenerated, 1h), CounterName, InstanceName |
| Scomposizione totale velocità effettiva dei dischi tra tutte le macchine virtuali | Perf &#124; where ObjectName == "Capacity and Performance" and (CounterName == "VHD Read MB/s" or CounterName == "VHD Write MB/s") &#124; summarize AggregatedValue = avg(CounterValue) by bin(TimeGenerated, 1h), CounterName, InstanceName |
| Scomposizione totale IOPS tra tutti i CSV | Perf &#124; where ObjectName == "Capacity and Performance" and (CounterName == "CSV Reads/s" or CounterName == "CSV Writes/s") &#124; summarize AggregatedValue = avg(CounterValue) by bin(TimeGenerated, 1h), CounterName, InstanceName |
| Scomposizione totale velocità effettiva tra tutti i CSV | Perf &#124; where ObjectName == "Capacity and Performance" and (CounterName == "CSV Reads/s" or CounterName == "CSV Writes/s") &#124; summarize AggregatedValue = avg(CounterValue) by bin(TimeGenerated, 1h), CounterName, InstanceName |
| Scomposizione totale latenza tra tutti i CSV | Perf &#124; where ObjectName == "Capacity and Performance" and (CounterName == "CSV Read Latency" or CounterName == "CSV Write Latency") &#124; summarize AggregatedValue = avg(CounterValue) by bin(TimeGenerated, 1h), CounterName, InstanceName |


## <a name="next-steps"></a>Passaggi successivi
* Utilizzare [Accedi ricerche Log Analitica](log-analytics-log-searches.md) tooview in dettaglio i dati di capacità e prestazioni.
