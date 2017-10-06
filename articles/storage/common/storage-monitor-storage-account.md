---
title: aaaHow toomonitor un account di archiviazione di Azure | Documenti Microsoft
description: Informazioni su come toomonitor un account di archiviazione in Azure utilizzando hello portale di Azure.
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: b83cba7b-4627-4ba7-b5d0-f1039fe30e78
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: marsma
ms.openlocfilehash: 9a939e0b5db687c1b7b7857399321f681df2056a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-storage-account-in-hello-azure-portal"></a>Monitoraggio di un account di archiviazione nel portale di Azure hello

[Analisi archiviazione di Azure](../storage-analytics.md) offre metriche per tutti i servizi di archiviazione e log per BLOB, code e tabelle. È possibile utilizzare hello [portale di Azure](https://portal.azure.com) tooconfigure quali le metriche e i log viene registrate per l'account e configura grafici che forniscono rappresentazioni visive dei dati di metrica.

> [!NOTE]
> Sono presenti i costi associati all'esame dei dati di monitoraggio del portale di Azure hello. Per altre informazioni, vedere [Analisi archiviazione e fatturazione](/rest/api/storageservices/Storage-Analytics-and-Billing).
>
> L’archiviazione file di Azure attualmente supporta la metrica di analisi di archiviazione, ma non supporta ancora l'accesso.
>
> Account di archiviazione con un tipo di replica di archiviazione con ridondanza della zona (ZRS) attualmente non è abilitata la funzionalità di registrazione o metrica di hello.
> 
> Per una guida approfondita sull'uso di archiviazione Analitica e tooidentify altri strumenti, diagnosticare e risoluzione dei problemi relativi al servizio di archiviazione Azure, vedere [Monitor, diagnosticare e risolvere i problemi di archiviazione di Microsoft Azure](../storage-monitoring-diagnosing-troubleshooting.md).
>

## <a name="configure-monitoring-for-a-storage-account"></a>Configurare il monitoraggio per un account di archiviazione

1. In hello [portale di Azure](https://portal.azure.com)selezionare **gli account di archiviazione**, quindi dashboard dell'account di hello storage account name tooopen hello.
1. Selezionare **diagnostica** in hello **monitoraggio** sezione del pannello menu hello.

    ![MonitoringOptions](./media/storage-monitor-storage-account/stg-enable-metrics-00.png)

1. Seleziona hello **tipo** di dati di metrica per ogni **servizio** desidera toomonitor e hello **criteri di conservazione** per i dati di hello. È anche possibile disabilitare il monitoraggio impostando **stato** troppo**Off**.

    ![MonitoringOptions](./media/storage-monitor-storage-account/stg-enable-metrics-01.png)

   Per ogni servizio è possibile abilitare due tipi di metriche, che per i nuovi account di archiviazione sono entrambi abilitati per impostazione predefinita.

   * **Metriche aggregate**: vengono raccolte metriche come ingresso/uscita, disponibilità, latenza e percentuale di operazioni riuscite, Queste metriche aggregate per hello servizi blob, coda, tabella e file.
   * **Per ogni API**: nella metrica di aggregazione toohello addizione, raccoglie hello stesso set di metriche per ogni operazione di archiviazione in hello API del servizio di archiviazione di Azure.

   criteri di conservazione dati hello tooset, hello spostamento **conservazione (giorni)** dispositivo di scorrimento o immettere hello numero di giorni di dati tooretain, da 1 too365. valore predefinito di Hello per i nuovi account di archiviazione è sette giorni. Se si desidera tooset un criterio di conservazione, immettere zero. Se è presente alcun criterio di conservazione, è attivo hello toodelete tooyou dati di monitoraggio.

   > [!WARNING]
   > Quando si eliminano manualmente i dati di metrica, viene applicato un addebito. Dati non aggiornati analitica (i dati precedenti i criteri di conservazione) viene eliminati dal sistema hello senza alcun costo. È consigliabile impostare un criterio di conservazione in base a quanto tempo dati tooretain archiviazione analitica per l'account. Per altre informazioni, vedere [Quali addebiti è necessario sostenere quando si abilitano le metriche di archiviazione?](../common/storage-enable-and-view-metrics.md#what-charges-do-you-incur-when-you-enable-storage-metrics)
   >

1. Al termine di configurazione del monitoraggio hello, selezionare **salvare**.

Un set predefinito di metriche viene visualizzato nei grafici nel Pannello di account di archiviazione hello, nonché i pannelli di singolo servizio hello (blob, coda, tabella e file). Dopo aver abilitato le metriche per un servizio, potrebbe richiedere fino a ora tooan per tooappear dati nei relativi grafici. È possibile selezionare **modifica** su qualsiasi metrica del grafico troppo[configurare le metriche](#how-to-customize-metrics-charts) vengono visualizzati nel grafico hello.

È possibile disabilitare la raccolta di metriche e registrazione impostando **stato** troppo**Off**.

> [!NOTE]
> Archiviazione di Azure Usa [archivio tabelle](../common/storage-introduction.md#table-storage) metriche hello toostore per l'account di archiviazione e archivi hello metriche nelle tabelle nell'account. Per altre informazioni, vedere [Come vengono archiviate le metriche](../common/storage-analytics.md#how-metrics-are-stored).
>

## <a name="customize-metrics-charts"></a>Personalizzare i grafici delle metriche

Utilizzare hello seguendo procedure toochoose quali tooview di metriche di archiviazione in un grafico delle metriche. 

1. Avviare la visualizzazione di un grafico di metriche di archiviazione nel portale di Azure hello. È possibile trovare grafici hello **blade di account di archiviazione** e hello **metriche** pannello per un singolo servizio (blob, coda, tabella, file).

   In questo esempio si lavora hello seguente grafico visualizzato nel hello **blade di account di archiviazione**:

   ![Selezione del grafico nel portale di Azure](./media/storage-monitor-storage-account/stg-customize-chart-00.png)

1. Fare quindi clic su un punto qualsiasi all'interno di hello di hello grafico tooopen **metrica** blade. Selezionare **Modifica grafico** tooopen hello **Modifica grafico** blade.

   ![Pulsante Modifica grafico nel pannello del grafico](./media/storage-monitor-storage-account/stg-customize-chart-01.png)

1. In hello **Modifica grafico** blade, seleziona hello **intervallo di tempo** di hello metriche toodisplay grafico hello e hello **servizio** (blob, coda, tabella, di file) il cui metriche desiderato toodisplay. Di seguito sono state selezionate hello toodisplay oltre le metriche della settimana per il servizio blob hello:

   ![Selezione intervallo e il servizio ora nel Pannello di modifica grafico hello](./media/storage-monitor-storage-account/stg-customize-chart-02.png)

1. Hello selezionare singoli **metriche** aveva come visualizzato nel grafico hello, quindi fare clic su **OK**. Ad esempio, qui abbiamo scelto hello toodisplay *ContainerCount* e *ObjectCount* metriche:

   ![Selezione delle singole metriche nel pannello Modifica grafico](./media/storage-monitor-storage-account/stg-customize-chart-03.png)

Le impostazioni del grafico non influisce su raccolta hello, aggregazione o archiviazione dei dati nell'account di archiviazione hello di monitoraggio, hello solo la visualizzazione dei dati di metrica.

### <a name="metrics-availability-in-charts"></a>Metriche disponibili nei grafici

elenco di Hello delle metriche disponibili per modifiche basato sul servizio che si è scelto nell'elenco a discesa hello e tipo di grafico hello unità hello che si sta modificando. Ad esempio, è possibile selezionare metriche relative a percentuali come *PercentNetworkError* e *PercentThrottlingError* solo se si sta modificando un grafico che visualizza unità in percentuale:

![Grafico di percentuale di errore di richiesta nel portale di Azure hello](./media/storage-monitor-storage-account/stg-customize-chart-04.png)

### <a name="metrics-resolution"></a>Risoluzione delle metriche

metriche Hello selezionate nella diagnostica determina la risoluzione di hello di metriche di hello che sono disponibili per l'account:

* Il monitoraggio **aggregato** offre metriche come ingresso/uscita, disponibilità, latenza e percentuale di operazioni riuscite, Queste metriche vengono aggregate da hello servizi blob, tabella, file e coda.
* **Per ogni API** risoluzione più accurato, con le metriche disponibili per singole operazioni di archiviazione, inoltre toohello aggregazioni a livello di servizio.

## <a name="configure-metrics-alerts"></a>Configurare avvisi relativi alle metriche

È possibile creare avvisi toonotify quando sono state raggiunte le soglie per la metrica di risorsa di archiviazione.

1. hello tooopen **pannello regole di avviso**, scorrere verso il basso toohello **monitoraggio** sezione di hello **pannello Menu** e selezionare **regole di avviso**.
1. Selezionare **Aggiungi avviso** tooopen hello **aggiungere una regola di avviso** pannello
1. Selezionare un **risorse** (blob, file, coda, tabella) da hello elenco a discesa e immettere un **nome** e **descrizione** per la nuova regola di avviso.
1. Seleziona hello **metrica** per il quale si desidera tooadd un avviso, un avviso **condizione**e un **soglia**. modifiche ai tipi di unità di Hello soglia a seconda della metrica hello scelta. Ad esempio, "count" è il tipo di unità hello per *ContainerCount*, durante l'unità di hello per hello *PercentNetworkError* metrica è una percentuale.
1. Seleziona hello **periodo**. Metriche raggiungono o superano hello soglia all'interno di trigger periodo hello un avviso.
1. (Facoltativo) Configurare le notifiche per **posta elettronica** e **webhook**. Per altre informazioni sui webhook, vedere [Configurare un webhook in un avviso relativo alle metriche di Azure](../../monitoring-and-diagnostics/insights-webhooks-alerts.md). Se non si configura notifiche di posta elettronica o webhook, gli avvisi vengono visualizzati solo nel portale di Azure hello.

!['Aggiungi una regola di avviso' blade in hello portale di Azure](./media/storage-monitor-storage-account/stg-alert-rules-01.png)

## <a name="add-metrics-charts-toohello-portal-dashboard"></a>Aggiungere dashboard del portale toohello grafici delle metriche

È possibile aggiungere grafici di metriche di archiviazione di Azure per i dashboard del portale storage account tooyour.

1. Fare clic su Seleziona **modificare il dashboard** durante la visualizzazione dashboard in hello [portale di Azure](https://portal.azure.com).
1. In hello **riquadro raccolta**selezionare **trova riquadri da** > **tipo**.
1. Selezionare **Tipo** > **Account di archiviazione**.
1. In **risorse**, selezionare l'account di archiviazione hello cui metriche desiderate tooadd toohello dashboard.
1. Selezionare **Categorie** > **Monitoraggio**.
1. Grafico di trascinamento e rilascio hello riquadro nel dashboard per metrica hello si desidera visualizzata. Ripetere per tutte le metriche desiderate visualizzate nel dashboard di hello. Nella seguente immagine di hello, grafico "BLOB - Totale richieste" hello è evidenziato come esempio, ma tutti i grafici di hello sono disponibili per la selezione nel dashboard.

   ![Raccolta riquadri nel portale di Azure](./media/storage-monitor-storage-account/stg-customize-dashboard-01.png)
1. Selezionare **eseguite di personalizzazione** superiore hello del dashboard hello una volta terminato l'aggiunta di grafici.

Dopo aver aggiunto il dashboard di tooyour grafici, è possibile personalizzare ulteriormente tali come descritto in [personalizzare grafici metriche](#how-to-customize-metrics-charts).

## <a name="configure-logging"></a>Configurare la registrazione

È possibile indicare i log di diagnostica toosave di archiviazione di Azure per leggere, scrivano ed eliminano le richieste di hello servizi blob, tabella e coda. criteri di conservazione dati Hello che è impostare si applicano anche toothese log.

> [!NOTE]
> L’archiviazione file di Azure attualmente supporta la metrica di analisi di archiviazione, ma non supporta ancora l'accesso.
>

1. In hello [portale di Azure](https://portal.azure.com)selezionare **gli account di archiviazione**, il nome di hello del Pannello di hello storage account tooopen hello storage account.
1. Selezionare **diagnostica** in hello **monitoraggio** sezione del pannello menu hello.

    ![Diagnostica della voce di menu nel monitoraggio nel portale di Azure hello.](./media/storage-monitor-storage-account/stg-enable-metrics-00.png)
    
1. Verificare **stato** è troppo**su**e seleziona hello **servizi** per il quale si desidera tooenable registrazione.

    ![Configurare la registrazione nel portale di Azure hello.](./media/storage-monitor-storage-account/stg-enable-logging-01.png)
1. Fare clic su **Salva**.

log di diagnostica Hello vengono salvati in un contenitore blob denominato $logs nell'account di archiviazione. È possibile visualizzare i dati di log hello usando l'esplorazione dell'archiviazione come hello [Esplora archivi Microsoft](http://storageexplorer.com), o a livello di codice con la libreria client di archiviazione hello o PowerShell.

Per informazioni sull'accesso contenitore hello $logs, vedere [abilitazione della registrazione di archiviazione e accesso ai dati di Log](/rest/api/storageservices/enabling-storage-logging-and-accessing-log-data).

## <a name="next-steps"></a>Passaggi successivi

* Altri dettagli su [metriche, registrazione e fatturazione](../storage-analytics.md) per Analisi archiviazione.
* [Abilitazione delle metriche di Archiviazione di Azure e visualizzazione dei dati delle metriche](../storage-enable-and-view-metrics.md) con PowerShell e a livello di codice con C#.
