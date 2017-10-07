---
title: aaaUse dati di log e le metriche toocollect Analitica di archiviazione di Azure | Documenti Microsoft
description: Archiviazione Analitica permette tootrack i dati di metrica per tutti i servizi di archiviazione e toocollect Registra per l'archiviazione Blob, coda e tabella.
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 7894993b-ca42-4125-8f17-8f6dfe3dca76
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/03/2017
ms.author: robinsh
ms.openlocfilehash: aba1a236cb69fa2e60bcb8fda5d34841e36e379a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="storage-analytics"></a>di Analisi archiviazione

Analisi archiviazione di Azure esegue la registrazione e fornisce le metriche dei dati per un account di archiviazione. È possibile usare questo richieste tootrace dati, analizzare le tendenze di utilizzo e diagnosticare i problemi con l'account di archiviazione.

toouse Analitica di archiviazione, è necessario abilitarla singolarmente per ogni servizio desiderato toomonitor. È possibile abilitarlo dalla hello [portale Azure](https://portal.azure.com). Per informazioni dettagliate, vedere [monitorare un account di archiviazione nel portale di Azure hello](storage-monitor-storage-account.md). È anche possibile abilitare Analitica di archiviazione a livello di programmazione tramite hello API REST o libreria client hello. Hello utilizzare [Get Blob Service Properties](https://msdn.microsoft.com/library/hh452239.aspx), [Get Queue Service Properties](https://msdn.microsoft.com/library/hh452243.aspx), [Get Table Service Properties](https://msdn.microsoft.com/library/hh452238.aspx), e [ottenere File Service Properties](https://msdn.microsoft.com/library/mt427369.aspx) operazioni tooenable Analitica di archiviazione per ogni servizio.

dati aggregati Hello viene archiviati in un noto blob (per la registrazione) e in tabelle note (per la metrica), che sono accessibili tramite il servizio Blob di hello e API del servizio tabelle.

Archiviazione Analitica pone un limite di 20 TB sulla quantità hello di dati archiviati che sia indipendenti dal limite totale di hello dell'account di archiviazione. Per altre informazioni sulla fatturazione e sui criteri di conservazione dei dati, vedere [Analisi archiviazione e fatturazione](https://msdn.microsoft.com/library/hh360997.aspx). Per informazioni sui limiti dell'account di archiviazione, vedere [Obiettivi di scalabilità e prestazioni per Archiviazione di Azure](storage-scalability-targets.md).

Per una guida approfondita sull'uso di archiviazione Analitica e tooidentify altri strumenti, diagnosticare e risoluzione dei problemi relativi al servizio di archiviazione Azure, vedere [Monitor, diagnosticare e risolvere i problemi di archiviazione di Microsoft Azure](storage-monitoring-diagnosing-troubleshooting.md).

## <a name="about-storage-analytics-logging"></a>Informazioni sulla registrazione di Analisi archiviazione
Archiviazione Analitica registra informazioni dettagliate sul servizio di archiviazione tooa richieste riuscite e non riuscite. Queste informazioni possono essere utilizzati toomonitor singole richieste e toodiagnose problemi con un servizio di archiviazione. Le richieste vengono registrate in base al massimo sforzo.

Le voci di log vengono create solo in presenza di attività del servizio di archiviazione. Ad esempio, se un account di archiviazione dispone di attività nel relativo servizio Blob, ma non in servizi di accodamento o tabelle, verranno creati solo i log relativi toohello servizio Blob.

La registrazione di Analisi archiviazione non è disponibile per Archiviazione file di Azure.

### <a name="logging-authenticated-requests"></a>Registrazione delle richieste autenticate
viene registrato i seguenti tipi di richieste autenticate Hello:

* Richieste riuscite
* Richieste non riuscite, tra cui timeout, limitazione, rete, autorizzazione e altri errori
* Richieste tramite una firma di accesso condiviso, incluse le richieste riuscite e non riuscite
* Tooanalytics richiede i dati.

Le richieste eseguite dalla stessa Analisi archiviazione, ad esempio, la creazione oppure l'eliminazione di log, non vengono registrate. Un elenco completo dei dati hello registrato è documentato in hello [archiviazione Analitica registrazione minima delle operazioni e messaggi di stato](https://msdn.microsoft.com/library/hh343260.aspx) e [formato di archiviazione Analitica Log](https://msdn.microsoft.com/library/hh343259.aspx) argomenti.

### <a name="logging-anonymous-requests"></a>Registrazione di richieste anonime
viene registrato i seguenti tipi di richieste anonime Hello:

* Richieste riuscite
* Errori server
* Errori di timeout per client e server
* Richieste GET non riuscite con codice di errore 304 (non modificate)

Tutte le altre richieste anonime non riuscite non vengono registrate. Un elenco completo dei dati hello registrato è documentato in hello [archiviazione Analitica registrazione minima delle operazioni e messaggi di stato](https://msdn.microsoft.com/library/hh343260.aspx) e [formato di archiviazione Analitica Log](https://msdn.microsoft.com/library/hh343259.aspx) argomenti.

### <a name="how-logs-are-stored"></a>Come vengono archiviati i log
Tutti i log vengono archiviati in BLOB di blocchi in un contenitore denominato $logs, che viene creato automaticamente quando viene abilitata Analisi archiviazione per un account di archiviazione. contenitore Hello $logs si trova nello spazio dei nomi blob hello hello dell'account di archiviazione, ad esempio: `http://<accountname>.blob.core.windows.net/$logs`. Questo contenitore non può essere eliminato una volta abilitata Analisi di archiviazione, sebbene sia possibile eliminarne il contenuto.

> [!NOTE]
> contenitore Hello $logs non viene visualizzata quando viene eseguita un'operazione elenco contenitori, ad esempio hello [ListContainers](https://msdn.microsoft.com/library/azure/dd179352.aspx) metodo. È necessario effettuare l'accesso diretto. Ad esempio, è possibile utilizzare hello [ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx) metodo tooaccess hello BLOB hello `$logs` contenitore.
> Nel momento in cui vengono registrate le richieste, Analisi archiviazione carica i risultati intermedi come blocchi. Analisi archiviazione invierà periodicamente questi blocchi e li renderà disponibili come BLOB.
> 
> 

I record duplicati possono esistere per i log creati nella hello stessa ora. È possibile determinare se un record è un duplicato verificando hello **RequestId** e **operazione** numero.

### <a name="log-naming-conventions"></a>Convenzioni di denominazione dei log
Ogni log verrà scritto nel seguente formato hello.

    <service-name>/YYYY/MM/DD/hhmm/<counter>.log

Hello nella tabella seguente vengono descritti gli attributi nel nome del log di hello.

| Attributo | Descrizione |
| --- | --- |
| <service-name> |nome Hello hello del servizio di archiviazione. Ad esempio: BLOB, tabella o coda |
| AAAA |anno a quattro cifre Hello per log hello. Ad esempio: 2011 |
| MM |mese a due cifre Hello per log hello. Ad esempio: 07 |
| GG |mese a due cifre Hello per log hello. Ad esempio: 07 |
| hh |ora a due cifre che indica l'avvio ora per hello hello Hello registra, in formato UTC 24 ore. Ad esempio: 18 |
| MM |numero a due cifre Hello che indica l'avvio minuto per i log di hello hello. Questo valore non è supportato nella versione corrente di hello di archiviazione Analitica e il relativo valore sarà sempre 00. |
| <counter> |Un contatore in base zero a sei cifre che indica il numero di hello di BLOB di log generato per il servizio di archiviazione hello in un'ora periodo di tempo. Questo contatore parte da 000000. Ad esempio: 000001 |

di seguito Hello è un nome di log di esempio completo che combina esempi precedenti hello.

    blob/2011/07/31/1800/000001.log

di seguito Hello è un URI che possono essere utilizzati tooaccess log precedente di hello di esempio.

    https://<accountname>.blob.core.windows.net/$logs/blob/2011/07/31/1800/000001.log

Quando viene registrata una richiesta di archiviazione, nome del log risultante hello correla ora toohello quando hello richiesta completata. Se ad esempio una richiesta GetBlob è stata completata alle 18:30 7/31/2011, hello log viene scritto con prefisso hello:`blob/2011/07/31/1800/`

### <a name="log-metadata"></a>Metadati dei log
Tutti i BLOB di log vengono archiviati i metadati che possono essere utilizzati tooidentify contiene il blob di hello dati di registrazione. Hello nella tabella seguente vengono descritti gli attributi di metadati.

| Attributo | Descrizione |
| --- | --- |
| LogType |Descrive se il log di hello contiene informazioni riguardanti tooread, scrittura o le operazioni di eliminazione. Questo valore può includere un solo tipo o una combinazione di tutti e tre, separati da virgola. Esempio 1: scrittura; Esempio 2: lettura, scrittura; Esempio 3: lettura, scrittura, eliminazione. |
| StartTime |Hello prima ora di una voce nel log di hello, sotto forma di hello di AAAA-MM-ddTHH. Ad esempio: 31-07-2011T18:21:46Z |
| EndTime |Hello ora più recente di una voce nel log di hello, sotto forma di hello di AAAA-MM-ddTHH. Ad esempio: 31-07-2011T18:22:09Z |
| LogVersion |versione di Hello del formato di log hello. Il valore di hello è supportato solo attualmente è 1.0. |

Hello seguente elenco vengono visualizzati i metadati di esempio completo utilizzando esempi precedenti hello.

* LogType=write
* StartTime=2011-07-31T18:21:46Z
* EndTime=2011-07-31T18:22:09Z
* LogVersion=1.0

### <a name="accessing-logging-data"></a>Accesso ai dati di registrazione
Tutti i dati hello `$logs` contenitore sono accessibili tramite l'API del servizio Blob hello, incluse le API .NET fornite da hello hello libreria gestita di Azure. amministratore dell'account di archiviazione Hello leggere ed eliminare i log, ma non è possibile creare o aggiornarli. Sia i metadati del log hello e nome del log utilizzabile durante la ricerca di un log. È possibile che tooappear i log di una determinata ora non in ordine, ma i metadati di hello specificano sempre hello timespan di voci di log in un log. Pertanto, nella ricerca di un particolare log, è possibile utilizzare una combinazione di nomi log e metadati.

## <a name="about-storage-analytics-metrics"></a>Informazioni sulle metriche di Analisi archiviazione
Archiviazione Analitica può archiviare le metriche che includono transazioni aggregate le statistiche e dati sulla capacità del servizio di archiviazione tooa richieste. Vengono dichiarate le transazioni a livello di operazione entrambi hello API, nonché a livello di servizio di archiviazione hello e capacità viene segnalata a livello di servizio di archiviazione hello. Dati di metrica possono essere utilizzati tooanalyze utilizzo di servizi di archiviazione, diagnosticare i problemi con le richieste effettuate al servizio di archiviazione hello e tooimprove hello prestazioni delle applicazioni che utilizzano un servizio.

toouse Analitica di archiviazione, è necessario abilitarla singolarmente per ogni servizio desiderato toomonitor. È possibile abilitarlo dalla hello [portale Azure](https://portal.azure.com). Per informazioni dettagliate, vedere [monitorare un account di archiviazione nel portale di Azure hello](storage-monitor-storage-account.md). È anche possibile abilitare Analitica di archiviazione a livello di programmazione tramite hello API REST o libreria client hello. Hello utilizzare **ottenere le proprietà del servizio** operazioni tooenable Analitica di archiviazione per ogni servizio.

### <a name="transaction-metrics"></a>Metriche di transazione
A intervalli di ore o minuti viene registrato un set di dati consistente per ciascun servizio di archiviazione e operazione API richiesta, inclusi ingresso/uscita, disponibilità, errori e vengono suddivise in categorie le percentuali di richieste. È possibile visualizzare un elenco completo dei dettagli relativi alla transazione hello in hello [Schema di tabella delle metriche di archiviazione Analitica](https://msdn.microsoft.com/library/hh343264.aspx) argomento.

Dati di transazione vengono registrati a due livelli: il livello di servizio hello e livello di operazione API hello. A livello di servizio hello, le statistiche che riepilogano tutte richiesto operazioni dell'API vengono scritte tooa tabella entità ogni ora anche se non esistono richieste sono state apportate toohello servizio. A livello di operazione hello API, le statistiche sono entità tooan scritto solo se è stata richiesta l'operazione di hello in quell'ora.

Ad esempio, se si esegue un **GetBlob** operazione nel servizio Blob, metriche di archiviazione Analitica registrerà richiesta hello e includere nei dati aggregato hello per entrambi hello servizio Blob, nonché hello **GetBlob** operazione. Tuttavia, se non **GetBlob** durante ora hello è richiesta l'operazione, un'entità non verrà scritti toohello `$MetricsTransactionsBlob` per l'operazione.

Le metriche delle transazioni vengono registrate sia per le richieste utente, sia per quelle eseguite dalla stessa Analisi archiviazione. Ad esempio, vengono registrate le richieste effettuate da archiviazione Analitica toowrite log ed entità tabella. Per altre informazioni su come vengono fatturate queste richieste, vedere [Analisi archiviazione e fatturazione](https://msdn.microsoft.com/library/hh360997.aspx)

### <a name="capacity-metrics"></a>Metriche della capacità
> [!NOTE]
> Attualmente, le metriche di capacità sono disponibili solo per hello servizio Blob. Capacità metriche per il servizio di tabella hello e servizio di Accodamento sarà disponibile nelle versioni future di archiviazione Analitica.
> 
> 

I dati relativi alla capacità vengono registrati quotidianamente per il servizio BLOB di un account di archiviazione e vengono scritte due entità di tabella. Un'entità fornisce le statistiche per i dati utente e altri hello fornisce statistiche sui hello `$logs` contenitore di blob utilizzato dall'archiviazione Analitica. Hello `$MetricsCapacityBlob` tabella include hello seguenti statistiche:

* **Capacità**: quantità di hello di archiviazione utilizzata dal servizio Blob dell'account di archiviazione hello, in byte.
* **ContainerCount**: numero di contenitori di blob nel servizio Blob dell'account di archiviazione hello hello.
* **ObjectCount**: numero di commit e BLOB di pagine o blocchi nel servizio Blob dell'account di archiviazione hello hello.

Per ulteriori informazioni su hello capacità metriche, vedere [Schema di tabella delle metriche di archiviazione Analitica](https://msdn.microsoft.com/library/hh343264.aspx).

### <a name="how-metrics-are-stored"></a>Come vengono archiviate le metriche
Tutti i dati di metrica per ognuno dei servizi di archiviazione hello è archiviato in tre tabelle riservate per il servizio: una tabella per informazioni sulle transazioni, una tabella per informazioni di transazioni al minuto e un'altra tabella per informazioni sulla capacità. Le informazioni sulla transazione e sulle transazioni al minuto consistono nei dati di richiesta e di risposta, mentre le informazioni sulla capacità consistono nei dati d'uso dell'archiviazione. Metrica oraria, metrica al minuto e capacità per il servizio Blob di un account di archiviazione sono accessibili nelle tabelle che sono denominate come descritto in hello nella tabella seguente.

| Livello metrica | Nomi tabella | Versioni supportate |
| --- | --- | --- |
| Metriche orarie, posizione principale |$MetricsTransactionsBlob  <br/>$MetricsTransactionsTable <br/> $MetricsTransactionsQueue |Le versioni precedenti too2013-08-15 solo. Sebbene questi nomi sono ancora supportati, è consigliabile passare tabelle hello toousing elencate di seguito. |
| Metriche orarie, posizione principale |$MetricsHourPrimaryTransactionsBlob <br/>$MetricsHourPrimaryTransactionsTable <br/>$MetricsHourPrimaryTransactionsQueue |Tutte le versioni, inclusa quella del 15-08-2013. |
| Metriche per minuto, posizione principale |$MetricsMinutePrimaryTransactionsBlob <br/>$MetricsMinutePrimaryTransactionsTable <br/>$MetricsMinutePrimaryTransactionsQueue |Tutte le versioni, inclusa quella del 15-08-2013. |
| Metriche orarie, posizione secondaria |$MetricsHourSecondaryTransactionsBlob  <br/>$MetricsHourSecondaryTransactionsTable <br/>$MetricsHourSecondaryTransactionsQueue |Tutte le versioni, inclusa quella del 15-08-2013. Deve essere abilitata la replica con accesso in lettura con ridondanza geografica. |
| Metriche al minuto, posizione secondaria |$MetricsMinuteSecondaryTransactionsBlob  <br/>$MetricsMinuteSecondaryTransactionsTable <br/>$MetricsMinuteSecondaryTransactionsQueue |Tutte le versioni, inclusa quella del 15-08-2013. Deve essere abilitata la replica con accesso in lettura con ridondanza geografica. |
| Capacità (solo servizio BLOB) |$MetricsCapacityBlob |Tutte le versioni, inclusa quella del 15-08-2013. |

Tali tabelle vengono create automaticamente quando viene abilitato Analisi archiviazione per un account di archiviazione. Sono accessibili tramite lo spazio dei nomi hello hello dell'account di archiviazione, ad esempio:`https://<accountname>.table.core.windows.net/Tables("$MetricsTransactionsBlob")`

### <a name="accessing-metrics-data"></a>Accesso ai dati delle metriche
Tutti i dati nelle tabelle di metrica hello possono essere eseguiti utilizzando l'API del servizio tabelle hello, incluse le API .NET fornite da hello hello libreria gestita di Azure. amministratore dell'account di archiviazione Hello leggere ed eliminare le entità di tabella, ma non è possibile creare o aggiornarli.

## <a name="billing-for-storage-analytics"></a>Fatturazione per Analisi archiviazione
Tutti i dati di metrica vengono scritte tramite servizi hello di un account di archiviazione. Di conseguenza, ogni operazione di scrittura eseguita da Analisi archiviazione è fatturabile. Inoltre, quantità hello di archiviazione utilizzata dai dati di metrica è fatturabile.

Hello seguenti le azioni eseguite da archiviazione Analitica sono fatturabile:

* BLOB di toocreate richieste per la registrazione. 
* Entità della tabella toocreate richieste per le metriche.

Se è stato configurato un criterio di conservazione dei dati, non verranno addebitati costi per le transazioni eliminate quando Analisi archiviazione elimina i vecchi dati di registrazione e delle metriche. Tuttavia, le transazioni eliminate da un client sono fatturabili. Per ulteriori informazioni sui criteri di conservazione, vedere [Impostazione di un criterio di conservazione dei dati di Analisi archiviazione](https://msdn.microsoft.com/library/azure/hh343263.aspx).

### <a name="understanding-billable-requests"></a>Informazioni sulle richieste fatturabili
Ogni richiesta effettuata tooan servizio account di archiviazione è fatturabile o non fatturabile. Archiviazione Analitica registra ogni singola richiesta effettuata tooa servizio, tra cui un messaggio di stato che indica la modalità di richiesta di hello. Analogamente, archiviazione Analitica archivia le metriche per un servizio e hello operazioni dell'API del servizio, inclusi le percentuali di hello e numero di determinati messaggi di stato. Insieme, queste funzionalità consentono di analizzare le richieste di fatturazione, migliorare l'applicazione e diagnosticare problemi con i servizi tooyour richieste. Per altre informazioni sulla fatturazione, vedere [Informazioni sulla fatturazione di Archiviazione di Azure - Larghezza di banda, transazioni e capacità](http://blogs.msdn.com/b/windowsazurestorage/archive/2010/07/09/understanding-windows-azure-storage-billing-bandwidth-transactions-and-capacity.aspx).

Quando si esaminano i dati di archiviazione Analitica, è possibile utilizzare tabelle hello in hello [archiviazione Analitica registrazione minima delle operazioni e messaggi di stato](https://msdn.microsoft.com/library/azure/hh343260.aspx) toodetermine argomento le richieste sono fatturabili. È quindi possibile confrontare i log e le metriche dati toohello stato messaggi toosee se è stata fatturata o per una particolare richiesta. È inoltre possibile utilizzare tabelle di hello nella disponibilità di hello precedente argomento tooinvestigate per un servizio di archiviazione o di una singola operazione API.

## <a name="next-steps"></a>Passaggi successivi
### <a name="setting-up-storage-analytics"></a>Configurazione di Analisi archiviazione
* [Monitoraggio di un account di archiviazione nel portale di Azure hello](storage-monitor-storage-account.md)
* [Abilitazione e configurazione di Analisi archiviazione](https://msdn.microsoft.com/library/hh360996.aspx)

### <a name="storage-analytics-logging"></a>Registrazione di Analisi archiviazione
* [Informazioni sulla registrazione di Analisi archiviazione](https://msdn.microsoft.com/library/hh343262.aspx)
* [Formato log Analisi archiviazione](https://msdn.microsoft.com/library/hh343259.aspx)
* [Operazioni registrate di Analisi archiviazione e messaggi di stato](https://msdn.microsoft.com/library/hh343260.aspx)

### <a name="storage-analytics-metrics"></a>Metriche di Analisi archiviazione
* [Informazioni sulle metriche di Analisi archiviazione](https://msdn.microsoft.com/library/hh343258.aspx)
* [Schema di tabella della metrica di Analisi di archiviazione](https://msdn.microsoft.com/library/hh343264.aspx)
* [Operazioni registrate di Analisi archiviazione e messaggi di stato](https://msdn.microsoft.com/library/hh343260.aspx)  

