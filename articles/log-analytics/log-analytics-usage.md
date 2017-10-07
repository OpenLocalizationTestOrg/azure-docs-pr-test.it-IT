---
title: utilizzo dei dati nel Log Analitica aaaAnalyze | Documenti Microsoft
description: "Utilizzare dashboard Usage hello Analitica Log tooview la quantità di dati inviata servizio Analitica Log toohello e la risoluzione dei problemi perché grandi quantità di dati viene inviata."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 74d0adcb-4dc2-425e-8b62-c65537cef270
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/21/2017
ms.author: magoedte
ms.openlocfilehash: c30373dd6edbe3ff900fbebc865575fee61ce14c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-data-usage-in-log-analytics"></a>Analizzare l'utilizzo dei dati in Log Analytics
Analitica log include informazioni sulla quantità di hello di dati raccolti, che i computer inviati dati hello e hello diversi tipi di dati inviati.  Hello utilizzare **utilizzo Analitica Log** quantità hello toosee di dashboard di dati inviati servizio Analitica Log toohello. dashboard di Hello Mostra la quantità di dati raccolti da ogni soluzione e la quantità di dati i computer inviano.

## <a name="understand-hello-usage-dashboard"></a>Dashboard Usage hello comprendere
Hello **utilizzo Analitica Log** dashboard Visualizza hello le seguenti informazioni:

- Volume dati
    - Volume dati nel tempo (in base all'ambito temporale corrente)
    - Volume dati per soluzione
    - Dati non associati a un computer
- Computer
    - Computer che inviano dati
    - Computer senza dati nelle ultime 24 ore
- Offerte
    - Nodi di informazioni dettagliate e analisi
    - Nodi di automazione e controllo
    - Nodi di sicurezza
- Prestazioni
    - Tempo impiegato dati dell'indice e toocollect
- Elenco di query

![dashboard di utilizzo](./media/log-analytics-usage/usage-dashboard01.png)

### <a name="toowork-with-usage-data"></a>toowork dati di utilizzo
1. Se non già stato fatto, accedere toohello [portale di Azure](https://portal.azure.com) tramite la sottoscrizione di Azure.
2. In hello **Hub** menu, fare clic su **più servizi** e nell'elenco di hello delle risorse, digitare **Analitica Log**. Si inizia a digitare, hello filtri di elenco in base all'input. Fare clic su **Log Analytics**.  
    ![Hub di Azure](./media/log-analytics-usage/hub.png)
3. Hello **Log Analitica** dashboard Mostra un elenco delle aree di lavoro. Selezionare un'area di lavoro.
4. In hello *dell'area di lavoro* dashboard, fare clic su **utilizzo Analitica Log**.
5. In hello **utilizzo Analitica Log** dashboard, fare clic su **tempo: ultime 24 ore** intervallo di tempo toochange hello.  
    ![Intervallo di tempo](./media/log-analytics-usage/time.png)
6. Server blade categoria utilizzo di hello visualizzazione che mostrano aree si è interessati. Scegliere un pannello e quindi fare clic su un elemento in esso tooview più in dettaglio in [ricerca nei Log](log-analytics-log-searches.md).  
    ![Pannello dell'utilizzo dei dati di esempio](./media/log-analytics-usage/blade.png)
7. Nel dashboard di ricerca nei Log hello, esaminare i risultati di hello che vengono restituiti dalla ricerca hello.  
    ![Ricerca log sull'utilizzo dei dati di esempio](./media/log-analytics-usage/usage-log-search.png)

## <a name="create-an-alert-when-data-collection-is-higher-than-expected"></a>Creare un avviso quando la raccolta dati supera le dimensioni previste
Questa sezione viene descritto come toocreate un avviso se:
- Il volume di dati supera una quantità specificata.
- Volume di dati è stimato tooexceed una quantità specificata.

Log Analytics [invia un avviso](log-analytics-alerts-creating.md) alle query di ricerca sull'utilizzo. Hello nella query seguente è un risultato quando è presente più di 100 GB di dati raccolti in hello ultime 24 ore:

`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(Quantity,1024)) as DataGB by Type | where DataGB > 100`

Hello nella query seguente utilizza un semplice toopredict formula quando più di 100 GB di dati verranno inviati in un giorno. 

`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(mul(Quantity,8),1024)) as EstimatedGB by Type | where EstimatedGB > 100`

tooalert su un volume di dati diversi, modifica Ciao 100 hello toohello numero di GB desiderato tooalert una query.

Utilizzare hello passaggi descritti in [creare una regola di avviso](log-analytics-alerts-creating.md#create-an-alert-rule) toobe una notifica quando la raccolta dei dati è supera al previsto.

Quando si crea avviso hello per query prima di hello, quando è presente più di 100 GB di dati in 24 ore, impostare il:
- **Nome** troppo*volume di dati maggiore di 100 GB nelle 24 ore*
- **Gravità** troppo*avviso*
- **Query di ricerca** troppo`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(Quantity,1024)) as DataGB by Type | where DataGB > 100`
- **Intervallo di tempo** troppo*24 ore*.
- **Avviso frequenza** toobe un'ora, poiché i dati di utilizzo hello Aggiorna solo una volta ogni ora.
- **Genera l'avviso in base a** toobe *numero di risultati*
- **Numero di risultati** toobe *maggiore di 0*

Utilizzare hello passaggi descritti in [aggiungere regole tooalert azioni](log-analytics-alerts-actions.md) configurare un'azione di posta elettronica, webhook o runbook per la regola di avviso hello.

Quando creazione avviso hello per query secondo hello, quando stimato che non vi siano più di 100 GB di dati nelle 24 ore, imposta il:
- **Nome** troppo*volume di dati previsto toogreater di 100 GB nelle 24 ore*
- **Gravità** troppo*avviso*
- **Query di ricerca** troppo`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(mul(Quantity,8),1024)) as EstimatedGB by Type | where EstimatedGB > 100`
- **Intervallo di tempo** troppo*3 ore*.
- **Avviso frequenza** toobe un'ora, poiché i dati di utilizzo hello Aggiorna solo una volta ogni ora.
- **Genera l'avviso in base a** toobe *numero di risultati*
- **Numero di risultati** toobe *maggiore di 0*

Quando si riceve un avviso, utilizzare i passaggi di hello in hello seguente sezione tootroubleshoot motivo per cui utilizzo è supera al previsto.

## <a name="troubleshooting-why-usage-is-higher-than-expected"></a>Risoluzione dei problemi che determinano un utilizzo superiore al previsto
dashboard usage Hello consente tooidentify perché utilizzo (e quindi i costi) è superiore a quello previsto.

Un utilizzo più elevato è dovuto a una o entrambe le cause seguenti:
- Più dati di quanto previsto inviati tooLog Analitica
- Più nodi del previsto l'invio di dati tooLog Analitica

### <a name="check-if-there-is-more-data-than-expected"></a>Verificare se sono presenti più dati del previsto 
Esistono due sezioni della pagina utilizzo hello chiave che consentono di identificare la causa hello toobe la maggior parte di dati raccolti.

Hello *volume di dati nel tempo* grafico Mostra volume totale di hello dei dati inviati e i computer hello invio hello la maggior parte dei dati. grafico Hello nella parte superiore di hello consente toosee se l'utilizzo di dati complessivo è in crescita, rimanenti diminuzione o costante. Hello dei computer sono elencati i computer hello 10 invio hello la maggior parte dei dati.

Hello *volume di dati per soluzione* grafico mostra il volume di hello dei dati inviati da ogni soluzione e soluzioni hello invio hello la maggior parte dei dati. grafico di Hello nella parte superiore di hello Mostra volume totale di hello dei dati inviati da ogni soluzione nel corso del tempo. Queste informazioni consentono tooidentify se una soluzione sta inviando altri dati, sull'hello stesso importo di dati, o meno dati nel tempo. elenco di Hello di soluzioni Mostra soluzioni hello 10 invio hello la maggior parte dei dati. 

Questi due grafici mostrano tutti i dati. Alcuni dati sono fatturabili, mentre altri sono gratuiti. toofocus solo sui dati che fatturabili, modificare la query hello in hello ricerca pagina tooinclude `IsBillable=true`.  

![grafici del volume dei dati](./media/log-analytics-usage/log-analytics-usage-data-volume.png)

Esaminare hello *volume di dati nel tempo* grafico. soluzioni di hello toosee e tipi di dati che inviano hello la maggior parte dei dati per un computer specifico, fare clic sul nome di hello del computer hello. Fare clic sul nome di hello del computer prima di hello nell'elenco di hello.

Nella seguente schermata di hello, hello *Log Management / prestazioni* tipo di dati invia hello la maggior parte dei dati per computer hello. 

![volume dei dati per un computer](./media/log-analytics-usage/log-analytics-usage-data-volume-computer.png)

Successivamente, tornare indietro toohello *utilizzo* dashboard ed esaminare hello *volume di dati per soluzione* grafico. computer hello toosee invio hello la maggior parte dei dati per una soluzione, fare clic sul nome di hello della soluzione hello nell'elenco di hello. Fare clic sul nome di hello della soluzione prima di hello nell'elenco di hello. 

Nella seguente schermata di hello, significa che hello *acmetomcat* computer stia inviando hello la maggior parte dei dati per la soluzione di gestione del Log hello.

![volume dei dati per una soluzione](./media/log-analytics-usage/log-analytics-usage-data-volume-solution.png)

Se necessario, eseguire i volumi di grandi dimensioni tooidentify ulteriori analisi all'interno di un soluzione o tipo di dati. Le query di esempio includono:

+ Soluzione **Sicurezza**
  - `Type=SecurityEvent | measure count() by EventID`
+ Soluzione **Gestione log**
  - `Type=Usage Solution=LogManagement IsBillable=true | measure count() by DataType`
+ Tipo di dati **Perf**
  - `Type=Perf | measure count() by CounterPath`
  - `Type=Perf | measure count() by CounterName`
+ Tipo di dati **Event**
  - `Type=Event | measure count() by EventID`
  - `Type=Event | measure count() by EventLog, EventLevelName`
+ Tipo di dati **Syslog**
  - `Type=Syslog | measure count() by Facility, SeverityLevel`
  - `Type=Syslog | measure count() by ProcessName`
+ Tipo di dati **AzureDiagnostics**
  - `Type=AzureDiagnostics | measure count() by ResourceProvider, ResourceId`

Utilizzare hello passaggi tooreduce hello volume di log raccolti seguente:

| Origine del volume di dati elevato | Come volume di dati tooreduce |
| -------------------------- | ------------------------- |
| Eventi di sicurezza            | Selezionare gli [eventi di sicurezza comuni o minimi](https://blogs.technet.microsoft.com/msoms/2016/11/08/filter-the-security-events-the-oms-security-collects/) <br> Hello sicurezza controllo criteri toocollect necessari solo eventi di modifica. In particolare, esaminare gli eventi di toocollect necessità di hello per <br> - [controllo piattaforma filtro](https://technet.microsoft.com/library/dd772749(WS.10).aspx) <br> - [controllo Registro di sistema](https://docs.microsoft.com/windows/device-security/auditing/audit-registry)<br> - [controllo file system](https://docs.microsoft.com/windows/device-security/auditing/audit-file-system)<br> - [controllo oggetto kernel](https://docs.microsoft.com/windows/device-security/auditing/audit-kernel-object)<br> - [controllo manipolazione handle](https://docs.microsoft.com/windows/device-security/auditing/audit-handle-manipulation)<br> - [controllo archivi rimovibili](https://docs.microsoft.com/windows/device-security/auditing/audit-removable-storage) |
| Contatori delle prestazioni       | Modificare la [configurazione del contatore delle prestazioni](log-analytics-data-sources-performance-counters.md) per: <br> -Consente di ridurre la frequenza di hello della raccolta <br> - Ridurre il numero di contatori delle prestazioni |
| Log eventi                 | Modificare la [configurazione del log eventi](log-analytics-data-sources-windows-events.md) per: <br> -Consente di ridurre il numero di hello dei registri eventi raccolti <br> - Raccogliere solo i livelli di eventi richiesti, ad esempio non raccogliendo gli eventi di livello *informazioni* |
| syslog                     | Modificare la [configurazione di Syslog](log-analytics-data-sources-syslog.md) per: <br> -Consente di ridurre il numero di hello delle strutture raccolti <br> - Raccogliere solo i livelli di eventi richiesti, ad esempio non raccogliendo gli eventi di livello *informazioni* e *debug* |
| AzureDiagnostics           | Modificare la raccolta dei log delle risorse per: <br> -Consente di ridurre il numero di hello di risorse trasmissione registri tooLog Analitica <br> - Raccogliere solo i log necessari |
| Dati della soluzione da computer che non richiedono una soluzione hello | Utilizzare [soluzione destinazione](../operations-management-suite/operations-management-suite-solution-targeting.md) dati toocollect da solo necessari gruppi di computer. |

### <a name="check-if-there-are-more-nodes-than-expected"></a>Verificare se sono presenti più nodi del previsto
Se si utilizza hello *per nodo (OMS)* tariffario, quindi vengono addebitati in base al numero di hello dei nodi e utilizzare le soluzioni. È possibile visualizzare il numero di nodi di ogni offerta viene utilizzato in hello *offerte* sezione di dashboard usage hello.

![dashboard di utilizzo](./media/log-analytics-usage/log-analytics-usage-offerings.png)

Fare clic su **vedere tutti... ** elenco completo di hello tooview dei computer di invio di dati per l'offerta di hello selezionato.

Utilizzare [soluzione destinazione](../operations-management-suite/operations-management-suite-solution-targeting.md) dati toocollect da solo necessari gruppi di computer.


## <a name="next-steps"></a>Passaggi successivi
* Vedere [Accedi ricerche Log Analitica](log-analytics-log-searches.md) toolearn come toouse hello ricerca language. È possibile utilizzare ricerca query tooperform ulteriori analisi sui dati di utilizzo di hello.
* Utilizzare hello passaggi descritti in [creare una regola di avviso](log-analytics-alerts-creating.md#create-an-alert-rule) viene soddisfatta toobe una notifica quando un criterio di ricerca
* Utilizzare [soluzione destinazione](../operations-management-suite/operations-management-suite-solution-targeting.md) dati toocollect da solo necessari gruppi di computer
* Selezionare gli [eventi di sicurezza comuni o minimi](https://blogs.technet.microsoft.com/msoms/2016/11/08/filter-the-security-events-the-oms-security-collects/)
* Modificare la [configurazione del contatore delle prestazioni](log-analytics-data-sources-performance-counters.md)
* Modificare la [configurazione del log eventi](log-analytics-data-sources-windows-events.md)
* Modificare la [configurazione di Syslog](log-analytics-data-sources-syslog.md)
