---
title: aaaTroubleshoot Analitica di flusso di Azure con i log di diagnostica | Documenti Microsoft
description: Informazioni su come diagnostica tooanalyze registra dal flusso Analitica processi in Microsoft Azure.
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 600fce73636dd137f8f3a137f1d77b59b4a88801
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-stream-analytics-by-using-diagnostics-logs"></a>Risoluzione dei problemi di Analisi di flusso di Azure mediante i log di diagnostica

In alcuni casi un processo di Analisi di flusso di Azure arresta l'elaborazione in modo imprevisto. È importante toobe tootroubleshoot in grado di questo tipo di evento. evento Hello potrebbe essere causato da un risultato imprevisto della query, la connettività toodevices o un'interruzione imprevista del servizio. Hello registri di diagnostica nel flusso Analitica consentono di identificare causa hello dei problemi quando si verificano e ridurre il tempo di recupero.

## <a name="log-types"></a>Tipi di log

Analisi di flusso offre due tipi di log: 
* [Log attività](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) (sempre attivi). I log attività forniscono informazioni dettagliate sulle operazioni eseguite sui processi.
* [Log di diagnostica](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs) (configurabili). I log di diagnostica forniscono informazioni più complete su tutto ciò che accade con un processo. Diagnostica registra quando viene creato il processo di hello di inizio e fine hello processo viene eliminato. Coprono eventi quando il processo di hello viene aggiornato e in fase di esecuzione.

> [!NOTE]
> È possibile utilizzare i servizi come archiviazione di Azure, hub eventi di Azure e Azure Log Analitica tooanalyze dati non conformi. Vengono addebitati in base a hello prezzi per tali servizi.
>

## <a name="turn-on-diagnostics-logs"></a>Attivare i log di diagnostica

I log di diagnostica sono **disattivati** per impostazione predefinita. tooturn nei log di diagnostica, completare questi passaggi:

1.  Accedi al portale di Azure toohello e passare toohello pannello processo di streaming. In **Monitoraggio**selezionare **Log di diagnostica**.

    ![Pannello navigazione toodiagnostics log](./media/stream-analytics-job-diagnostic-logs/image1.png)  

2.  Selezionare **Attiva diagnostica**.

    ![Attivare i log di diagnostica](./media/stream-analytics-job-diagnostic-logs/image2.png)

3.  In hello **le impostazioni di diagnostica** pagina per **stato**selezionare **su**.

    ![Cambiare lo stato per i log di diagnostica](./media/stream-analytics-job-diagnostic-logs/image3.png)

4.  Impostare la destinazione dell'archivio di hello (account di archiviazione, hub eventi, Log Analitica) che si desidera. Quindi, selezionare le categorie di hello di log che si desidera toocollect (esecuzione, creazione e modifica). 

5.  Salvare hello nuova configurazione di diagnostica.

configurazione della diagnostica Hello ha effetto di tootake circa 10 minuti. Successivamente, hello registra nella destinazione di archiviazione configurato hello inizio (è possibile visualizzare tali informazioni in hello **log di diagnostica** pagina):

![Pannello navigazione toodiagnostics log - destinazioni di archiviazione](./media/stream-analytics-job-diagnostic-logs/image4.png)

Per altre informazioni sulla configurazione di diagnostica, vedere [Raccogliere e usare i dati di diagnostica dalle risorse di Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs).

## <a name="diagnostics-log-categories"></a>Categorie del log di diagnostica

Attualmente vengono acquisite due categorie di log di diagnostica:

* **Creazione**. Le acquisizioni registrare gli eventi che sono correlati toojob operazioni di creazione: creazione del processo, aggiunta ed eliminazione di input e output, aggiungere e aggiornare query hello, avvio e processo di arresto hello.
* **Esecuzione**. Acquisisce gli eventi che si verificano durante l'esecuzione del processo:
    * Errori di connettività
    * Errori di elaborazione dei dati, fra cui:
        * Gli eventi che non sono conformi toohello query di definizione (tipi di campo non corrispondenti e i valori, i campi mancanti e così via)
        * Errori di valutazione delle espressioni
    * Altri eventi ed errori

## <a name="diagnostics-logs-schema"></a>Schema dei log di diagnostica

Tutti i log vengono archiviati in formato JSON. Ogni voce include hello campi stringa comuni seguenti:

Nome | Descrizione
------- | -------
time | Timestamp (in UTC) del log hello.
resourceId | ID di risorsa hello hello operazione ha avuto luogo, in lettere maiuscole. Include l'ID sottoscrizione hello, gruppo di risorse hello e nome del processo hello. Ad esempio, **/SUBSCRIPTIONS/6503D296-DAC1-4449-9B03-609A1F4A1C87/RESOURCEGROUPS/MY-RESOURCE-GROUP/PROVIDERS/MICROSOFT.STREAMANALYTICS/STREAMINGJOBS/MYSTREAMINGJOB**.
category | Categoria del log, ovvero **Execution** o **Authoring**.
operationName | Nome dell'operazione di hello che viene registrato. Ad esempio, **inviare eventi: Output SQL scrivere l'errore toomysqloutput**.
status | Stato dell'operazione di hello. Ad esempio **Failed** o **Succeeded**.
necessario | Il livello del log. Ad esempio **Error**, **Warning** o **Informational**.
properties | Dettagli specifici delle voci di log; serializzazione come stringa JSON. Per ulteriori informazioni, vedere le sezioni seguenti di hello.

### <a name="execution-log-properties-schema"></a>Schema delle proprietà dei log di esecuzione

I log di esecuzione hanno informazioni sugli eventi che si sono verificati durante l'esecuzione del processo di analisi di flusso. schema di Hello della proprietà varia a seconda di tipo hello dell'evento. Attualmente, abbiamo hello seguenti tipi di log di esecuzione:

### <a name="data-errors"></a>Errori nei dati

Qualsiasi errore che si verifica durante l'elaborazione dati di processo hello è in questa categoria di log. Questi log vengono creati più spesso durante le operazioni di lettura dei dati, serializzazione e scrittura. Questi log non includono errori di connettività. Gli errori di connettività vengono trattati come eventi generici.

Nome | Descrizione
------- | -------
Sorgente | Nome del processo di hello di input o output in cui si è verificato l'errore hello.
Message | Messaggio associato all'errore hello.
Tipo | Tipo di errore. Ad esempio **DataConversionError**, **CsvParserError** o **ServiceBusPropertyColumnMissingError**.
Dati | Contiene i dati che si rivela utili tooaccurately individuare hello origine errore hello. Oggetto tootruncation, a seconda delle dimensioni.

A seconda di hello **operationName** valore, gli errori di dati presentano hello seguente schema:
* **Eventi di serializzazione**. Gli eventi di serializzazione si verificano durante le operazioni di lettura degli eventi. Si verificano quando hello dati nell'input hello non soddisfano schema query hello per uno dei motivi seguenti:
    * *Mancata corrispondenza del tipo durante l'evento (de) serializzare*: identifica il campo hello che ha causato l'errore hello.
    * *Non è in grado di leggere un evento, la serializzazione non valido*: Elenca le informazioni sulla posizione hello nei dati di input hello in cui si è verificato l'errore hello. Include il nome di blob per l'input di blob, offset e un campione di dati hello.
* **Eventi di invio**. Gli eventi di invio si verificano durante le operazioni di scrittura. Consentono di identificare il flusso di eventi che ha causato hello errore hello.

### <a name="generic-events"></a>Eventi generici

Gli eventi generici sono tutti gli altri.

Nome | Descrizione
-------- | --------
Tipi di errore | (facoltativo) Informazioni sugli errori. Si tratta in genere di informazioni sulle eccezioni, se disponibili.
Message| Messaggio del log.
Tipo | Tipo di messaggio. Esegue il mapping di categorizzazione toointernal degli errori. Ad esempio **JobValidationError** o **BlobOutputAdapterInitializationFailure**.
ID correlazione | [GUID](https://en.wikipedia.org/wiki/Universally_unique_identifier) che identifica in modo univoco l'esecuzione del processo hello. Tutte le voci di log di esecuzione da hello ora hello processo viene avviato fino a quando non si arresta processo hello hanno hello stesso **ID di correlazione** valore.

## <a name="next-steps"></a>Passaggi successivi

* [Introduzione tooStream Analitica](stream-analytics-introduction.md)
* [Introduzione ad Analisi di flusso](stream-analytics-real-time-fraud-detection.md)
* [Scalabilità dei processi di Analisi di flusso](stream-analytics-scale-jobs.md)
* [Informazioni di riferimento sul linguaggio di query di Analisi di flusso](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Informazioni di riferimento sull'API REST di gestione di Analisi di flusso](https://msdn.microsoft.com/library/azure/dn835031.aspx)
