---
title: aaaMonitor, diagnosticare e risolvere i problemi di archiviazione | Documenti Microsoft
description: "Utilizzare le funzionalità, ad esempio analitica di archiviazione e registrazione lato client tooidentify altri strumenti di terze parti, diagnosticare e risolvere i problemi correlati ad archiviazione di Azure."
services: storage
documentationcenter: 
author: fhryo-msft
manager: jahogg
editor: tysonn
ms.assetid: da57e844-705d-449d-8ed5-5607d2a6170b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: fhryo-msft
ms.openlocfilehash: 294a0bd27bd03913e01a719c0175cab827d58225
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-diagnose-and-troubleshoot-microsoft-azure-storage"></a>Monitorare, diagnosticare e risolvere i problemi dell'Archiviazione di Microsoft Azure
[!INCLUDE [storage-selector-portal-monitoring-diagnosing-troubleshooting](../../includes/storage-selector-portal-monitoring-diagnosing-troubleshooting.md)]

## <a name="overview"></a>Overview
La diagnosi e la risoluzione dei problemi in un'applicazione distribuita ospitata in un ambiente cloud possono essere più complesse rispetto agli ambienti tradizionali. Le applicazioni possono essere distribuite in un'infrastruttura PaaS o IaaS, in locale, su un dispositivo mobile o in una combinazione di questi tipi di distribuzione. In genere, il traffico di rete dell'applicazione può attraversare reti pubbliche e private e l'applicazione potrà usare più tecnologie di archiviazione, ad esempio tabelle di archiviazione di Microsoft Azure, BLOB, code o vengono archiviati i file di dati tooother aggiunta, ad esempio relazionale e database di documenti.

toomanage tali applicazioni correttamente è necessario monitorarli in modo proattivo e comprendere come toodiagnose e risolvere i problemi relativi a tutti gli aspetti e le tecnologie dipendenti. Come utente di servizi di archiviazione di Azure, si deve continuamente monitorare i servizi di archiviazione hello l'applicazione utilizza per impreviste modifiche del comportamento (ad esempio, più lento rispetto a tempi di risposta normale) e utilizzare toocollect registrazione più dettagliati dati e tooanalyze un problema di profondità. informazioni di diagnostica Hello ottenute da monitoraggio e registrazione consentirà si toodetermine hello causa radice di hello di eseguire l'applicazione ha rilevato. È possibile risolvere il problema di hello e determinare i passaggi appropriati di hello è possibile eseguire tooremediate è. Archiviazione di Azure è un componenti di base del servizio di Azure e costituisce una parte importante della maggior parte di hello delle soluzioni che i clienti distribuire toohello dell'infrastruttura di Azure. Archiviazione di Azure include funzionalità toosimplify monitoraggio, diagnosi e risoluzione dei problemi di archiviazione nelle applicazioni basate su cloud.

> [!NOTE]
> Account di archiviazione con un tipo di replica di archiviazione con ridondanza della zona (ZRS) non dispone delle metriche hello o abilitata al momento la funzionalità di registrazione. 
> 
> 

Per un Guida pratica tooend-to-end risoluzione dei problemi in applicazioni di servizio di archiviazione Azure, vedere [risoluzione dei problemi con le metriche di archiviazione di Azure e la registrazione, AzCopy e Message Analyzer End-to-End](storage-e2e-troubleshooting.md).

* [Introduzione]
  * [Organizzazione di questa guida]
* [monitoraggio del servizio di archiviazione]
  * [Monitoraggio dello stato del servizio]
  * [Monitoraggio della capacità]
  * [Monitoraggio della disponibilità]
  * [Monitoraggio delle prestazioni]
* [la diagnosi dei problemi di archiviazione]
  * [Problemi di stato del servizio]
  * [Problemi di prestazioni]
  * [Diagnostica degli errori]
  * [Problemi dell'emulatore di archiviazione]
  * [Strumenti di registrazione dell'archiviazione]
  * [Uso degli strumenti di registrazione in rete]
* [traccia End-to-end]
  * [Correlazione dei dati di log]
  * [ID richiesta client]
  * [ID richiesta Server]
  * [Timestamp]
* [le indicazioni di Troubleshooting]
  * [metrica Mostra AverageE2ELatency alta e bassa AverageServerLatency]
  * [Metrica Mostra AverageE2ELatency bassa e bassa AverageServerLatency ma hello client si è verificato ad alta latenza]
  * [Le metriche indicano un valore AverageServerLatency alto]
  * [Si stanno verificando ritardi imprevisti nel recapito dei messaggi di una coda]
  * [metriche mostrano un aumento PercentThrottlingError]
  * [metriche mostrano un aumento PercentTimeoutError]
  * [Le metriche indicano un aumento di PercentNetworkError]
  * [client hello è la ricezione di messaggi HTTP 403 (accesso negato)]
  * [client hello è la ricezione di messaggi HTTP 404 (non trovato)]
  * [client hello è la ricezione di messaggi HTTP 409 (conflitto)]
  * [metrica Mostra PercentSuccess bassa o voci di log analitica sono operazioni con stato delle transazioni di ClientOtherErrors]
  * [Le metriche della capacità indicano un aumento imprevisto dell'uso della capacità di archiviazione]
  * [Si stanno verificando riavvii imprevisti delle macchine virtuali con un numero elevato di VHD allegati]
  * [Il problema si verifica di utilizzare l'emulatore di archiviazione hello per lo sviluppo o test]
  * [Si sono verificati problemi di installazione hello Azure SDK per .NET]
  * [Si è verificato un problema diverso con un servizio di archiviazione]
* [appendici]
  * [appendice 1: il traffico HTTP e HTTPS toocapture tramite Fiddler]
  * [appendice 2: il traffico di rete utilizzando Wireshark toocapture]
  * [appendice 3: il traffico di rete utilizzando Microsoft Message Analyzer toocapture]
  * [Appendice 4: Utilizzando i dati di metrica e di log tooview di Excel]
  * [appendice 5: monitoraggio con Application Insights per Visual Studio Team Services]

## <a name="introduction"></a>Introduzione
Problemi relativi al Mostra questa guida si come toouse funzionalità quali Analitica di archiviazione di Azure, la registrazione lato client in Azure Storage Client Library hello e tooidentify altri strumenti di terze parti, diagnosticare e risolvere i problemi di archiviazione di Azure.

![][1]

*Figura 1 Monitoraggio, diagnostica e risoluzione dei problemi*

Questa guida è previsto toobe leggere principalmente dagli sviluppatori di servizi online che usano servizi di archiviazione di Azure e i professionisti IT responsabili della gestione di tali servizi in linea. Hello obiettivi di questa guida sono:

* toohelp conservare hello integrità e le prestazioni degli account di archiviazione di Azure.
* tooprovide processi necessarie hello e si decide se un problema in un'applicazione si riferisce tooAzure archiviazione toohelp di strumenti.
* tooprovide con informazioni aggiuntive utilizzabili per risolvere i problemi correlati tooAzure archiviazione.

### <a name="how-this-guide-is-organized"></a>Organizzazione di questa guida
sezione Hello "[monitoraggio del servizio di archiviazione]" viene descritto come toomonitor hello integrità e le prestazioni dei servizi di archiviazione di Azure utilizzando Azure Storage Analitica metriche (metriche di archiviazione).

sezione Hello "[la diagnosi dei problemi di archiviazione]" viene descritto come toodiagnose problemi utilizzando Azure registrazione Analitica archiviazione (registrazione archiviazione). Viene inoltre descritto come tooenable registrazione lato client utilizzando hello funzioni in una delle librerie client hello, ad esempio hello libreria Client di archiviazione per .NET o hello Azure SDK per Java.

sezione Hello "[traccia End-to-end]" viene descritto come è possibile correlare informazioni hello contenute nei diversi file di log e dati di metrica.

sezione Hello "[le indicazioni di Troubleshooting]" vengono fornite indicazioni sulla risoluzione dei problemi per alcune delle hello correlati ad archiviazione di problemi comuni che potrebbero verificarsi.

Hello "[appendici]" includono informazioni sull'utilizzo di altri strumenti, ad esempio Wireshark e Netmon per analisi dei dati del pacchetto, Fiddler per l'analisi dei messaggi HTTP/HTTPS, di rete Microsoft Message Analyzer per correlare i dati e di registro.

## <a name="monitoring-your-storage-service"></a>Monitoraggio del servizio di archiviazione
Per chi ha familiarità con il monitoraggio delle prestazioni di Windows, le metriche di archiviazione di Azure corrispondono ai contatori di Windows Performance Monitor. In metriche di archiviazione si troverà un set completo di metriche (contatori nella terminologia di Performance Monitor di Windows), ad esempio la disponibilità del servizio, numero totale di richieste tooservice o percentuale di richieste riuscite tooservice (per un elenco completo di hello le metriche disponibili, vedere <a href="http://msdn.microsoft.com/library/azure/hh343264.aspx" target="_blank">Schema di tabella delle metriche di archiviazione Analitica</a> su MSDN). È possibile specificare se si desidera toocollect servizio di archiviazione hello e metrica di aggregazione, ogni ora o ogni minuto. Per ulteriori informazioni sulle metriche tooenable e monitorare gli account di archiviazione, vedere <a href="http://go.microsoft.com/fwlink/?LinkId=510865" target="_blank">l'abilitazione di metriche di archiviazione</a> su MSDN.

È possibile scegliere le metriche orarie desiderato toodisplay hello portale classico di Azure e configurare le regole di notifica agli amministratori tramite posta elettronica ogni volta che una metrica oraria supera una determinata soglia (per ulteriori informazioni, vedere la pagina hello <a href="http://msdn.microsoft.com/library/azure/dn306638.aspx" target="_blank">come: Ricevere notifiche di avviso e gestire le regole di avviso in Azure</a>). il servizio di archiviazione Hello raccoglie le metriche di utilizzo migliore, ma non è stato possibile registrare ogni operazione di archiviazione.

Figura 2 Mostra pagina monitoraggio hello in hello portale di Azure classico in cui è possibile visualizzare metriche, ad esempio disponibilità, richieste totali e i numeri di latenza media per un account di archiviazione. Una regola di notifica inoltre configurata la tooalert amministratore se disponibilità scende di sotto di un determinato livello. Dalla visualizzazione di questo tipo di dati, un'area possibili per l'analisi è percentuale di completamento del hello tabella servizio essere inferiore al 100% (per ulteriori informazioni, vedere la sezione hello "[metrica Mostra PercentSuccess bassa o voci di log analitica sono operazioni con stato delle transazioni di ClientOtherErrors]").

![][2]

*Figura 2, la visualizzazione delle metriche di archiviazione nel portale di Azure classico hello*

È necessario monitorare continuamente tooensure le applicazioni Azure sono integri e verrà eseguito come previsto:

* Creazione di alcune metriche di base per l'applicazione che consentono di dati corrente toocompare e rilevare eventuali modifiche significative di comportamento hello di archiviazione di Azure e l'applicazione. i valori Hello metriche della linea di base saranno, in molti casi, un'applicazione specifica e si deve stabilire quando si è l'applicazione di test delle prestazioni.
* La registrazione di metrica al minuto e il relativo utilizzo toomonitor attivamente per errori imprevisti e anomalie, ad esempio picchi di conteggi di errori o frequenza richieste.
* Registrazione delle metriche orarie e il relativo utilizzo toomonitor i valori medi, ad esempio Media conteggi di errori e richiedere tariffe.
* Analisi dei problemi potenziali usando gli strumenti di diagnostica, come illustrato più avanti nella sezione hello "[la diagnosi dei problemi di archiviazione]."

grafici di Hello nella figura 3 viene illustrato come hello Media che si verifica per la metrica oraria possa nascondere picchi di attività. metrica oraria Hello visualizzato tooshow una velocità costante delle richieste, durante il minuto hello metriche rivelano fluttuazioni hello che vengono effettivamente eseguiti.

![][3]

Hello resto di questa sezione vengono descritte le metriche da monitorare e sul motivo.

### <a name="monitoring-service-health"></a>Monitoraggio dello stato del servizio
È possibile utilizzare hello [portale di Azure classico](https://manage.windowsazure.com) hello di integrità hello tooview del servizio di archiviazione hello (e altri servizi di Azure) in tutte le aree di Azure in tutto il mondo hello. In questo modo si toosee immediatamente se il servizio di archiviazione nell'area di hello che è utilizzare per l'applicazione hello interessa un problema all'esterno del controllo.

Hello portale classico di Azure può inoltre fornire le notifiche degli eventi imprevisti che interessano hello diversi servizi di Azure.
Nota: Queste informazioni è stata precedentemente disponibili, insieme ai dati cronologici, in hello Dashboard del servizio di Azure in <a href="http://status.azure.com" target="_blank">http://status.azure.com</a>.

Mentre hello portale classico di Azure raccoglie informazioni sull'integrità all'interno di hello Data Center di Azure (monitoraggio interno-out), è inoltre possibile adottare un approccio esterno aggiuntivo toogenerate le transazioni sintetiche che accedono a periodicamente l'ospitato in Azure applicazione Web da più posizioni. Hello servizi offerti da <a href="http://www.keynote.com/solutions/monitoring/web-monitoring" target="_blank">Keynote</a>, <a href="https://www.gomeznetworks.com/?g=1" target="_blank">Gomez</a>, e Application Insights per Visual Studio Team Services sono esempi di questo approccio di esterno. Per ulteriori informazioni su Application Insights per Visual Studio Team Services, vedere l'appendice hello "[appendice 5: monitoraggio con Application Insights per Visual Studio Team Services]."

### <a name="monitoring-capacity"></a>Monitoraggio della capacità
Metriche di archiviazione sono archiviate solo le metriche di capacità per il servizio blob hello perché BLOB è in genere conto quota più grande di hello dei dati archiviati (in fase di hello di scrittura, non è possibile toouse capacità hello toomonitor di metriche di archiviazione tabelle e code) . È possibile trovare questi dati in hello **$MetricsCapacityBlob** tabella se è stato attivato il monitoraggio per hello servizio Blob. Metriche di archiviazione registra i dati una volta al giorno e che è possibile utilizzare il valore di hello di hello **RowKey** toodetermine se la riga hello contiene un'entità che si riferisce a dati toouser (valore **dati**) o (dati analitica valore **analitica**). Ogni entità stored contiene informazioni sulla quantità di hello di memoria utilizzata (**capacità** espresso in byte) e il numero corrente dei contenitori di hello (**ContainerCount**) e i BLOB ( **ObjectCount**) in uso nell'account di archiviazione hello. Per ulteriori informazioni sulle metriche di capacità hello archiviate in hello **$MetricsCapacityBlob** tabella, vedere <a href="http://msdn.microsoft.com/library/azure/hh343264.aspx" target="_blank">Schema di tabella delle metriche di archiviazione Analitica</a> su MSDN.

> [!NOTE]
> È necessario monitorare questi valori per un avviso anticipato che si siano per raggiungere i limiti di capacità hello dell'account di archiviazione. Nel portale classico di Azure, di hello in hello **monitoraggio** pagina dell'account di archiviazione, è possibile aggiungere regole di avviso toonotify se utilizzo aggregazione dell'archiviazione supera o scende di sotto le soglie specificate.
> 
> 

Per informazioni sulla stima delle dimensioni di hello dei vari oggetti di archiviazione, ad esempio BLOB, vedere hello post di blog <a href="http://blogs.msdn.com/b/windowsazurestorage/archive/2010/07/09/understanding-windows-azure-storage-billing-bandwidth-transactions-and-capacity.aspx" target="_blank">comprensione archiviazione fatturazione di Azure: larghezza di banda, transazioni e capacità</a>.

### <a name="monitoring-availability"></a>Monitoraggio della disponibilità
Monitorare la disponibilità di hello dei servizi di archiviazione hello nell'account di archiviazione monitorando valore hello hello **disponibilità** colonna hello tabelle metrica oraria o di minuti, **$ MetricsHourPrimaryTransactionsBlob**, **$MetricsHourPrimaryTransactionsTable**, **$MetricsHourPrimaryTransactionsQueue**, **$ MetricsMinutePrimaryTransactionsBlob**, **$MetricsMinutePrimaryTransactionsTable**, **$MetricsMinutePrimaryTransactionsQueue**, **$ MetricsCapacityBlob**. Hello **disponibilità** colonna contiene un valore percentuale che indica la disponibilità di hello del servizio di hello o operazione API hello rappresentata dalla riga hello (hello **RowKey** indica se la riga hello contiene metriche per il servizio di hello nel suo complesso o per un'operazione API specifica).

Eventuali valori inferiori al 100% indicano che alcune richieste di archiviazione hanno esito negativo. È possibile visualizzare i motivi per cui essi hanno esito negativo esaminando hello altre colonne in dati di metrica hello che mostrano, ad esempio un numero di richieste con vari tipi di errore hello **ServerTimeoutError**. È necessario prevedere toosee **disponibilità** autunno temporaneamente inferiore al 100% per motivi, ad esempio il timeout del server temporaneo mentre il servizio di hello Sposta partizioni toobetter il bilanciamento del carico richiesta; hello la logica dell'applicazione client di riesecuzione deve gestire tali condizioni intermittenti. pagina Hello <a href="http://msdn.microsoft.com/library/azure/hh343260.aspx" target="_blank"> </a> elenchi hello tipi di transazione che include metriche di archiviazione nel relativo **disponibilità** calcolo.

Nel portale classico di Azure, di hello in hello **monitoraggio** pagina dell'account di archiviazione, è possibile aggiungere regole di avviso toonotify è se **disponibilità** per un servizio scende sotto una soglia specificata.

Hello "[le indicazioni di Troubleshooting]" sezione di questa guida vengono descritte alcune comuni tooavailability correlati di archiviazione servizio problemi.

### <a name="monitoring-performance"></a>Monitoraggio delle prestazioni
prestazioni di hello toomonitor hello servizi di archiviazione, è possibile utilizzare hello seguenti metriche dagli hello ogni ora e minuto tabelle di metrica.

* Hello valori hello **AverageE2ELatency** e **AverageServerLatency** Mostra il servizio di archiviazione hello tempo medio di hello o il tipo di operazione API richiede tooprocess richieste. **AverageE2ELatency** è una misura della latenza end-to-end che include una richiesta di hello tooread tempo hello e inviare una risposta hello nella richiesta di aggiunta toohello tempo tooprocess hello (pertanto include la latenza di rete dopo la richiesta hello il servizio di archiviazione hello raggiunge); **AverageServerLatency** misura solo il tempo di elaborazione hello e pertanto esclude qualsiasi latenza di rete correlato toocommunicating con client hello. Vedere la sezione hello "[metrica Mostra AverageE2ELatency alta e bassa AverageServerLatency]" più avanti in questa guida per una descrizione del motivo per cui potrebbe esserci una differenza significativa tra questi due valori.
* Hello valori hello **TotalIngress** e **TotalEgress** colonne mostrano quantità totale di hello di dati, in byte, entrano tooand passare fuori il servizio di archiviazione o tramite un tipo di operazione API specificato.
* Hello valori hello **TotalRequests** riceve colonna Mostra hello totale delle richieste che il servizio di archiviazione di operazione API hello. **TotalRequests** hello il numero totale di richieste ricevute dal servizio di archiviazione hello.

In genere, questi valori vengono monitorati per verificare la presenza di eventuali cambiamenti imprevisti che possono indicare l'esistenza di problemi da sottoporre ad analisi.

Nel portale classico di Azure, di hello in hello **monitoraggio** pagina dell'account di archiviazione, è possibile aggiungere regole di avviso toonotify se una delle metriche di prestazioni hello per questo servizio scende di sotto o superi la soglia specificata.

Hello "[le indicazioni di Troubleshooting]" sezione di questa guida vengono descritte alcune comuni tooperformance correlati di archiviazione servizio problemi.

## <a name="diagnosing-storage-issues"></a>Diagnosi dei problemi di archiviazione
Esistono alcuni sintomi che indicano la presenza di un problema dell'applicazione, tra cui:

* Errore grave che causa l'utilizzo di toocrash o toostop applicazione hello.
* Modifiche significative da valori di base di metriche di hello monitorata come descritto nella sezione precedente hello "[monitoraggio del servizio di archiviazione]."
* Segnalazione da parte degli utenti dell'applicazione in merito al fatto che una determinata operazione non viene completata come previsto o che non è possibile usare una funzionalità.
* Errori generati all'interno dell'applicazione che appaiono nei file di log o vengono segnalati con altri metodi.

In genere, servizi di archiviazione di problemi correlati tooAzure rientrano in una delle quattro categorie generali:

* L'applicazione dispone di un problema di prestazioni segnalati dagli utenti o rivelati dalle modifiche apportate ai dati statistici sulle prestazioni di hello.
* Si verifica un problema con l'infrastruttura di archiviazione di Azure hello in uno o più aree.
* L'applicazione viene rilevato un errore, segnalati dagli utenti o ottenuti da un aumento in una delle metriche di numero di errore hello monitorate.
* Durante lo sviluppo e test, che si stia utilizzando emulatore di archiviazione locale hello; è possibile riscontrare alcuni problemi che si riferiscono in particolare toousage dell'emulatore di archiviazione hello.

Hello sezioni seguenti descrivono i passaggi di hello è consigliabile seguire toodiagnose e risolvere i problemi in ognuna delle quattro categorie. sezione Hello "[le indicazioni di Troubleshooting]" più avanti in questa guida fornisce informazioni dettagliate per alcuni problemi comuni che possono verificarsi.

### <a name="service-health-issues"></a>Problemi di stato del servizio
I problemi di stato del servizio di solito sono al di fuori del controllo dell'utente. Hello portale classico di Azure fornisce informazioni su eventuali problemi in corso con servizi Azure, inclusi i servizi di archiviazione. Se si è scelto per l'archiviazione con ridondanza geografica e accesso in lettura al momento della creazione dell'account di archiviazione, quindi nell'evento hello dei dati non è disponibile nel percorso primario hello, l'applicazione potrebbe passare temporaneamente toohello copia di sola lettura nel percorso secondario hello. toodo, l'applicazione deve essere in grado di tooswitch tra l'utilizzo di percorsi di archiviazione primario e secondario di hello, e toowork in grado di essere in modalità con funzionalità ridotte con dati di sola lettura. le librerie Client di archiviazione di Azure Hello consentono toodefine un criterio di ripetizione in grado di leggere dall'archivio secondario in caso di una lettura dall'archiviazione primaria. L'applicazione deve inoltre toobe tenere presente che i dati di hello nella posizione secondaria hello sono alla fine coerenti. Per ulteriori informazioni, vedere hello post di blog <a href="http://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/04/introducing-read-access-geo-replicated-storage-ra-grs-for-windows-azure-storage.aspx" target="_blank">opzioni di ridondanza di archiviazione di Azure e archiviazione con ridondanza geografica di accesso in lettura</a>.

### <a name="performance-issues"></a>Problemi di prestazioni
prestazioni Hello di un'applicazione possono essere soggettiva, soprattutto dalla prospettiva dell'utente. È pertanto importante toohave baseline metriche toohelp disponibili è identificare dove potrebbe esserci un problema di prestazioni. Molti fattori potrebbero prestazioni hello di un servizio di archiviazione di Azure dalla prospettiva dell'applicazione hello client. Questi fattori potrebbero funzionare nel servizio di archiviazione hello, nel client hello o nell'infrastruttura di rete hello; è pertanto importante toohave una strategia per identificare l'origine di hello del problema di prestazioni hello.

Dopo aver identificato hello probabile posizione causa hello del problema di prestazioni hello dalle metriche di hello, è possibile quindi utilizzare hello log file toofind toodiagnose informazioni dettagliate e risoluzione dei problemi di hello ulteriormente.

Hello sezione "[le indicazioni di Troubleshooting]" più avanti in questa guida fornisce informazioni relative alle prestazioni comuni problemi riscontrati.

### <a name="diagnosing-errors"></a>Diagnostica degli errori
Gli utenti dell'applicazione possono notificare errori segnalati da un'applicazione hello client. Le metriche di archiviazione registrano anche i conteggi dei diversi tipi di errore riscontrati dai servizi di archiviazione, quali **NetworkError**, **ClientTimeoutError** o **AuthorizationError**. Benché Metriche di archiviazione registrino solo i conteggi dei diversi tipi di errore, è possibile ottenere più dettagli sulle singole richieste esaminando i file di log di lato server, lato client e rete. In genere, codice di stato HTTP hello restituito dal servizio di archiviazione hello fornirà un'indicazione dei motivi per cui non è riuscita richiesta hello.

> [!NOTE]
> Tenere presente che si dovrebbero toosee alcuni errori intermittenti: ad esempio, gli errori a causa di condizioni della rete tootransient o errori dell'applicazione.
> 
> 

salve le risorse seguenti nel sito Web MSDN sono utili per informazioni sui codici di stato e di errore correlati ad archiviazione:

* <a href="http://msdn.microsoft.com/library/azure/dd179357.aspx" target="_blank">Codici di errore comuni dell'API REST</a>
* <a href="http://msdn.microsoft.com/library/azure/dd179439.aspx" target="_blank">Codici di errore del servizio BLOB</a>
* <a href="http://msdn.microsoft.com/library/azure/dd179446.aspx" target="_blank">Codici di errore del servizio di accodamento</a>
* <a href="http://msdn.microsoft.com/library/azure/dd179438.aspx" target="_blank">Codici di errore del servizio tabelle</a>

### <a name="storage-emulator-issues"></a>Problemi dell'emulatore di archiviazione
Hello Azure SDK include un emulatore di archiviazione che è possibile eseguire in una workstation di sviluppo. L'emulatore simula la maggior parte del comportamento di hello dei servizi di archiviazione Azure hello e risulta utile durante lo sviluppo e test, consentendo toorun applicazioni che utilizzano servizi di archiviazione di Azure senza hello necessario per una sottoscrizione di Azure e un account di archiviazione di Azure.

Hello "[le indicazioni di Troubleshooting]" sezione di questa guida vengono descritti alcuni problemi comuni riscontrati usando l'emulatore di archiviazione hello.

### <a name="storage-logging-tools"></a>Strumenti di registrazione dell'archiviazione
La registrazione dell'archiviazione consente di registrare sul lato server le richieste di archiviazione presenti nell'account di archiviazione di Azure. Per ulteriori informazioni sulla modalità di registrazione sul lato server tooenable e hello di accesso ai dati di log, vedere <a href="http://go.microsoft.com/fwlink/?LinkId=510867" target="_blank">utilizzando la registrazione sul lato server</a> su MSDN.

Libreria Client di archiviazione per .NET Hello consente toocollect dati del log sul lato client che si riferisce toostorage le operazioni eseguite dall'applicazione. Per ulteriori informazioni sulla modalità di registrazione lato client tooenable e hello di accesso ai dati di log, vedere <a href="http://go.microsoft.com/fwlink/?LinkId=510868" target="_blank">registrazione lato Client utilizzando hello libreria Client di archiviazione</a> su MSDN.

> [!NOTE]
> In alcuni casi (ad esempio gli errori di autorizzazione di firma di accesso condiviso), un utente può segnalare un errore per il quale è non possibile trovare alcun dato di richiesta in hello i log di archiviazione sul lato server. È possibile utilizzare le funzionalità di registrazione hello di hello libreria Client di archiviazione tooinvestigate se causa hello del problema hello client hello o usare rete hello tooinvestigate di strumenti di monitoraggio della rete.
> 
> 

### <a name="using-network-logging-tools"></a>Uso degli strumenti di registrazione in rete
È possibile acquisire il traffico di hello tra hello client e server tooprovide dettagliate informazioni hello dati hello client e server sono lo scambio e hello le condizioni della rete sottostante. Sono disponibili alcuni strumenti utili per la registrazione in rete:

* Fiddler (<a href="http://www.telerik.com/fiddler" target="_blank">http://www.telerik.com/fiddler</a>) è un proxy che consente le intestazioni di hello tooexamine e dati del payload dei messaggi di richiesta e risposta HTTP e HTTPS per debug gratuitamente dal web. Per ulteriori informazioni, vedere "[appendice 1: il traffico HTTP e HTTPS toocapture tramite Fiddler]".
* Microsoft Network Monitor (Netmon) (<a href="http://www.microsoft.com/download/details.aspx?id=4865" target="_blank">http://www.microsoft.com/download/details.aspx?id=4865</a>) e Wireshark (<a href="http://www.wireshark.org/" target="_blank">http://www.wireshark.org/</a>) è gli analizzatori di protocollo che consentono di rete disponibile si tooview dettagliate informazioni sul pacchetto per un'ampia gamma di protocolli di rete. Per ulteriori informazioni su Wireshark, vedere "[appendice 2: il traffico di rete utilizzando Wireshark toocapture]".
* Microsoft Message Analyzer è uno strumento di Microsoft che sostituisce Netmon e che inoltre toocapturing rete dati del pacchetto, consente di tooview e analizzare i dati di log hello acquisiti da altri strumenti. Per ulteriori informazioni, vedere "[appendice 3: il traffico di rete utilizzando Microsoft Message Analyzer toocapture]".
* Se si desidera tooperform un toocheck di test di connettività di base che nel computer client può connettersi toohello servizio di archiviazione di Azure tramite rete hello, non è possibile farlo tramite hello standard **ping** strumento client hello. Tuttavia, è possibile utilizzare hello **tcping** strumento toocheck connettività. **Tcping** può essere scaricato da <a href="http://www.elifulkerson.com/projects/tcping.php" target="_blank">http://www.elifulkerson.com/projects/tcping.php</a>.

In molti casi, i dati di log hello dalla registrazione archiviazione e hello libreria Client di archiviazione sarà sufficiente toodiagnose un problema, ma in alcuni scenari, potrebbe essere necessario hello che informazioni che questi strumenti di registrazione di rete possono fornire più dettagliate. Ad esempio, consente di messaggi HTTP e HTTPS tooview intestazione e il payload dati inviati tooand da hello servizi di archiviazione, che consentono tooexamine come un'applicazione client tramite Fiddler tooview tentativi di operazioni di archiviazione. Gli analizzatori di protocollo, ad esempio Wireshark operano a livello di pacchetto hello permette di dati, TCP tooview consentirebbero tootroubleshoot perdita di pacchetti e problemi di connettività. Message Analyzer è in grado di funzionare sia sul livello HTTP che sul livello TCP.

## <a name="end-to-end-tracing"></a>Traccia end-to-end
La funzionalità di traccia end-to-end basata sull'utilizzo di una varietà di file di log è una tecnica utile per l'analisi dei potenziali problemi. È possibile utilizzare le informazioni di data/ora hello dai dati di metrica come indicazione della dove toostart ricerca nei file di log hello per hello informazioni che consentono di risolvere il problema di hello.

### <a name="correlating-log-data"></a>Correlazione dei dati di log
Quando si visualizzano i log dalle applicazioni client, tracce di rete e archiviazione sul lato server, registrazione è critico toobe toocorrelate in grado di richieste tra hello diversi file di log. file di log di Hello includono un numero di campi diversi che sono utili come identificatori di correlazione. id di richiesta client hello è hello utili toouse toocorrelate voci del campo nei diversi log hello. Tuttavia in alcuni casi può essere utile toouse id richiesta server di hello o timestamp. Hello nelle sezioni seguenti vengono forniscono ulteriori dettagli su queste opzioni.

### <a name="client-request-id"></a>ID richiesta client
Libreria Client di archiviazione Hello genera automaticamente un id richiesta client univoci per ogni richiesta.

* In hello crea log lato client che hello libreria Client di archiviazione, id di richiesta client hello viene visualizzato in hello **ID richiesta Client** campo di ogni voce del registro relative toohello richiesta.
* In una traccia di rete, ad esempio uno acquisiti da Fiddler, id di richiesta client hello è visibile in messaggi di richiesta come hello **x-ms-client-request-id** valore dell'intestazione HTTP.
* Nel log di registrazione archiviazione sul lato server hello, id di richiesta client hello viene visualizzato nella colonna di ID richiesta Client hello.

> [!NOTE]
> È possibile che più richieste tooshare hello lo stesso id di richiesta client perché il client hello può assegnare questo valore (sebbene hello libreria Client di archiviazione assegna automaticamente un nuovo valore). In caso di hello di tentativi da client hello, tutti i tentativi di condividono hello lo stesso id di richiesta client. Nel caso di hello di un batch inviato dal client hello, batch hello ha un id richiesta client singolo.
> 
> 

### <a name="server-request-id"></a>ID richiesta server
il servizio di archiviazione Hello genera automaticamente l'ID richiesta server.

* Nel log di registrazione archiviazione sul lato server hello, id richiesta server di hello visualizzato hello **intestazione ID richiesta** colonna.
* In una traccia di rete, ad esempio uno acquisiti da Fiddler, id richiesta server di hello viene visualizzato nei messaggi di risposta come hello **x-ms-request-id** valore dell'intestazione HTTP.
* In hello crea log lato client che hello libreria Client di archiviazione, id richiesta server di hello viene visualizzato in hello **testo operazione** colonna per la voce di log hello con dettagli hello della risposta del server.

> [!NOTE]
> il servizio di archiviazione Hello assegna sempre univoche di un server id tooevery richiesta che riceve, pertanto ogni nuovo tentativo da client hello e ogni operazione incluso in un batch ha un id richiesta server univoci.
> 
> 

Se hello libreria Client di archiviazione genera un **StorageException** nel client hello hello **RequestInformation** proprietà contiene un **oggetto RequestResult** oggetto che include un **ServiceRequestID** proprietà. È anche possibile accedere a un oggetto **RequestResult** da un'istanza **OperationContext**.

Nell'esempio di codice Hello riportato di seguito viene illustrato come tooset personalizzato **ClientRequestId** valore collegando un **OperationContext** oggetto servizio di archiviazione toohello hello richiesta. Viene inoltre illustrato come hello tooretrieve **ServerRequestId** valore dal messaggio di risposta hello.

```csharp
//Parse hello connection string for hello storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Create an Operation Context that includes custom ClientRequestId string based on constants defined within hello application along with a Guid.
OperationContext oc = new OperationContext();
oc.ClientRequestID = String.Format("{0} {1} {2} {3}", HOSTNAME, APPNAME, USERID, Guid.NewGuid().ToString());

try
{
    CloudBlobContainer container = blobClient.GetContainerReference("democontainer");
    ICloudBlob blob = container.GetBlobReferenceFromServer("testImage.jpg", null, null, oc);  
    var downloadToPath = string.Format("./{0}", blob.Name);
    using (var fs = File.OpenWrite(downloadToPath))
    {
        blob.DownloadToStream(fs, null, null, oc);
        Console.WriteLine("\t Blob downloaded toofile: {0}", downloadToPath);
    }
}
catch (StorageException storageException)
{
    Console.WriteLine("Storage exception {0} occurred", storageException.Message);
    // Multiple results may exist due tooclient side retry logic - each retried operation will have a unique ServiceRequestId
    foreach (var result in oc.RequestResults)
    {
            Console.WriteLine("HttpStatus: {0}, ServiceRequestId {1}", result.HttpStatusCode, result.ServiceRequestID);
    }
}
```

### <a name="timestamps"></a>Timestamp
È inoltre possibile utilizzare i timestamp toolocate relative voci di log, ma è necessario assicurarsi di qualsiasi dello sfasamento di orario tra hello client e server che potrebbero esistere. È consigliabile cercare più o meno di 15 minuti per la corrispondenza di voci sul lato server in base al timestamp hello client hello. Tenere presente che i metadati blob hello per i BLOB hello contenente le metriche indicano l'intervallo di tempo hello per le metriche di hello archiviate in blob hello; Ciò è utile se si dispone di molti BLOB metriche per hello stesso minuti o ore.

## <a name="troubleshooting-guidance"></a>Guida alla risoluzione dei problemi
In questa sezione consentono di diagnosi hello e risoluzione dei problemi relativi ad alcuni problemi comuni di hello dell'applicazione possono verificarsi quando si utilizza servizi di archiviazione Azure hello. Utilizzare l'elenco di hello sotto toolocate hello informazioni pertinenti tooyour specifico problema.

**Albero delle decisioni per la risoluzione dei problemi**

- - -
È il problema correlato toohello delle prestazioni di uno dei servizi di archiviazione hello?

* [metrica Mostra AverageE2ELatency alta e bassa AverageServerLatency]
* [Metrica Mostra AverageE2ELatency bassa e bassa AverageServerLatency ma hello client si è verificato ad alta latenza]
* [Le metriche indicano un valore AverageServerLatency alto]
* [Si stanno verificando ritardi imprevisti nel recapito dei messaggi di una coda]

- - -
È il problema correlato toohello disponibilità di uno dei servizi di archiviazione hello?

* [metriche mostrano un aumento PercentThrottlingError]
* [metriche mostrano un aumento PercentTimeoutError]
* [Le metriche indicano un aumento di PercentNetworkError]

- - -
L'applicazione client riceve una risposta HTTP 4XX (ad esempio 404) da un servizio di archiviazione?

* [client hello è la ricezione di messaggi HTTP 403 (accesso negato)]
* [client hello è la ricezione di messaggi HTTP 404 (non trovato)]
* [client hello è la ricezione di messaggi HTTP 409 (conflitto)]

- - -
[metrica Mostra PercentSuccess bassa o voci di log analitica sono operazioni con stato delle transazioni di ClientOtherErrors]

- - -
[Le metriche della capacità indicano un aumento imprevisto dell'uso della capacità di archiviazione]

- - -
[Si stanno verificando riavvii imprevisti delle macchine virtuali con un numero elevato di VHD allegati]

- - -
[Il problema si verifica di utilizzare l'emulatore di archiviazione hello per lo sviluppo o test]

- - -
[Si sono verificati problemi di installazione hello Azure SDK per .NET]

- - -
[Si è verificato un problema diverso con un servizio di archiviazione]

- - -
### <a name="metrics-show-high-AverageE2ELatency-and-low-AverageServerLatency"></a>Le metriche indicano un valore AverageE2ELatency alto e un valore AverageServerLatency basso
Hello soffiare via figura dallo strumento di monitoraggio di hello portale classico di Azure viene illustrato un esempio in cui hello **AverageE2ELatency** è notevolmente superiore hello **AverageServerLatency**.

![][4]

Si noti che il servizio di archiviazione hello solo Calcola metrica hello **AverageE2ELatency** per le richieste riuscite e, a differenza di **AverageServerLatency**, incluso il tempo di hello client hello accetta toosend hello dati e ricevere acknowledgement dal servizio di archiviazione hello. Pertanto, una differenza tra **AverageE2ELatency** e **AverageServerLatency** potrebbe essere una scadenza toohello client applicazione da rallentare toorespond o tooconditions scadenza nella rete hello.

> [!NOTE]
> È inoltre possibile visualizzare **E2ELatency** e **ServerLatency** per singole operazioni di archiviazione nella registrazione archiviazione hello registrare i dati.
> 
> 

#### <a name="investigating-client-performance-issues"></a>Analisi dei problemi di prestazioni del client
Possibili motivi per i client hello risponde lentamente includono la presenza di un numero limitato di connessioni disponibili o thread. Potrebbe essere in grado di tooresolve problema di hello modificando hello client codice toobe più efficiente (ad esempio tramite il servizio di archiviazione toohello chiamate asincrone) o tramite una macchina virtuale di dimensioni maggiori (con più core e memoria).

Per i servizi tabelle e code di hello, algoritmo Nagle hello può essere causato anche elevata **AverageE2ELatency** rispetto troppo**AverageServerLatency**: per ulteriori informazioni vedere hello post <a href="http://blogs.msdn.com/b/windowsazurestorage/archive/2010/06/25/nagle-s-algorithm-is-not-friendly-towards-small-requests.aspx" target="_blank">Nagle L'algoritmo non è descrittivo verso le richieste di piccole dimensioni</a> su hello blog del Team di archiviazione di Microsoft Azure. È possibile disabilitare l'algoritmo Nagle hello nel codice utilizzando hello **ServicePointManager** classe hello **System.Net** dello spazio dei nomi. È consigliabile farlo prima apportare qualsiasi tabella toohello chiamate o aprire Servizi coda dell'applicazione, poiché questa operazione non influenza le connessioni che sono già. Hello seguente esempio è tratto da hello **Application_Start** metodo in un ruolo di lavoro.

```csharp
var storageAccount = CloudStorageAccount.Parse(connStr);
ServicePoint tableServicePoint = ServicePointManager.FindServicePoint(storageAccount.TableEndpoint);
tableServicePoint.UseNagleAlgorithm = false;
ServicePoint queueServicePoint = ServicePointManager.FindServicePoint(storageAccount.QueueEndpoint);
queueServicePoint.UseNagleAlgorithm = false;
```

È consigliabile controllare hello log lato client toosee quanti l'applicazione client invia richieste e controllare .NET generali correlati eventuali colli di bottiglia nel client, ad esempio CPU, operazioni di garbage collection .NET, utilizzo della rete o memoria (come un tipo di avvio punto di risoluzione dei problemi nelle applicazioni client .NET, vedere <a href="http://msdn.microsoft.com/library/7fe0dd2y(v=vs.110).aspx" target="_blank">debug, traccia e profilatura</a> su MSDN).

#### <a name="investigating-network-latency-issues"></a>Analisi dei problemi di latenza di rete
In genere, ad alta latenza end-to-end causata dalla rete hello è a causa di condizioni tootransient. Per l'analisi dei problemi transitori e persistenti della rete, ad esempio le interruzioni della trasmissione dei pacchetti, sono disponibili strumenti come Wireshark o Microsoft Message Analyzer.

Per ulteriori informazioni sull'utilizzo Wireshark tootroubleshoot problemi di rete, vedere "[appendice 2: il traffico di rete utilizzando Wireshark toocapture]."

Per ulteriori informazioni sull'utilizzo di problemi di rete tootroubleshoot Microsoft Message Analyzer, vedere "[appendice 3: il traffico di rete utilizzando Microsoft Message Analyzer toocapture]."

### <a name="metrics-show-low-AverageE2ELatency-and-low-AverageServerLatency"></a>Metrica Mostra AverageE2ELatency bassa e bassa AverageServerLatency ma hello client si è verificato ad alta latenza
In questo scenario, la causa più probabile di hello è un ritardo nelle richieste di archiviazione hello raggiungere il servizio di archiviazione hello. È necessario individuare perché le richieste da client hello non rendono tramite il servizio blob toohello.

Possibili cause per ritardare l'invio di richieste client di hello includono la presenza di un numero limitato di connessioni disponibili o thread. Si deve verificare se il client hello esegue più tentativi e analizzare il motivo di hello in caso di hello. È possibile farlo a livello di programmazione esaminando hello **OperationContext** oggetto associato richiesta hello e il recupero hello **ServerRequestId** valore. Per ulteriori informazioni, vedere l'esempio di codice hello nella sezione hello "[ID richiesta Server]."

Se nel client hello non siano presenti problemi, è necessario esaminare i potenziali problemi di rete, ad esempio la perdita di pacchetti. È possibile utilizzare strumenti quali problemi di rete tooinvestigate Wireshark o Microsoft Message Analyzer.

Per ulteriori informazioni sull'utilizzo Wireshark tootroubleshoot problemi di rete, vedere "[appendice 2: il traffico di rete utilizzando Wireshark toocapture]."

Per ulteriori informazioni sull'utilizzo di problemi di rete tootroubleshoot Microsoft Message Analyzer, vedere "[appendice 3: il traffico di rete utilizzando Microsoft Message Analyzer toocapture]."

### <a name="metrics-show-high-AverageServerLatency"></a>Le metriche indicano un valore AverageServerLatency alto
Nel caso di hello di elevata **AverageServerLatency** per le richieste di download di blob, è consigliabile utilizzare hello registrazione archiviazione registra toosee se sono presenti le ripetute richieste di hello stessi blob (o set di BLOB). Le richieste di caricamento blob, è necessario esaminare quali blocco dimensioni hello client utilizza (ad esempio blocchi minore di 64 KB di dimensioni può comportare costi generali, a meno che la legge hello sono presenti anche in meno di 64K blocchi), e se più client sta caricando Blocca toohello stesso BLOB in parallelo. È inoltre consigliabile controllare le metriche al minuto hello per eventuali picchi nel numero hello di richieste che comportano il superamento di hello al secondo obiettivi di scalabilità: Vedere anche "[metriche mostrano un aumento PercentTimeoutError]."

Se si verifica alto **AverageServerLatency** per le richieste di download di blob quando vi sono ripetuti richieste hello stesso blob o set di BLOB, quindi è consigliabile prendere in considerazione la memorizzazione nella cache tali BLOB utilizzando la Cache di Azure o hello contenuti di Azure Rete (CDN). Per le richieste di caricamento, è possibile migliorare la velocità effettiva di hello con dimensioni maggiori del blocco. Per query tootables, è anche possibile tooimplement la cache lato client nei client che eseguono hello stessi per operazioni di query e hello in dati non cambiano frequentemente.

Elevata **AverageServerLatency** valori possono anche essere un sintomo di tabelle progettate in modo inadeguato o anti-pattern accodare o anteporre le query che i risultati in operazioni di analisi o che seguono hello. Per ulteriori informazioni, vedere "[metriche mostrano un aumento PercentThrottlingError]".

> [!NOTE]
> Un elenco di controllo completo delle prestazioni è disponibile qui: [Elenco di controllo di prestazioni e scalabilità per Archiviazione di Microsoft Azure](storage-performance-checklist.md).
> 
> 

### <a name="you-are-experiencing-unexpected-delays-in-message-delivery"></a>Si stanno verificando ritardi imprevisti nel recapito dei messaggi di una coda
Se si verificano un ritardo tra il momento di hello un'applicazione aggiunge un messaggio tooa coda e hello tempo che diventa tooread disponibile dalla coda di hello, quindi è necessario intraprendere hello problema hello toodiagnose di passaggi seguente:

* Verificare l'applicazione hello correttamente viene aggiunta la coda toohello messaggi hello. Verificare che un'applicazione hello non tentativo in corso di hello **AddMessage** metodo più volte prima successiva. i registri di libreria Client di archiviazione Hello mostrerà qualsiasi ripetuti tentativi di operazioni di archiviazione.
* Non verificare sia presente alcun clock sfasamento di orario tra i ruoli di lavoro hello che aggiunge la coda toohello hello e ruolo di lavoro hello che legge un messaggio dalla coda hello che rende vengono visualizzati come se si verifica un ritardo nell'elaborazione.
* Controllare se i ruoli di lavoro hello che legge i messaggi hello dalla coda hello non sono riuscito. Se un client di coda chiama hello **GetMessage** metodo ma ha esito negativo toorespond con un acknowledgement, hello messaggio rimarrà invisibile in coda hello finché hello **invisibilityTimeout** scadenza del periodo. A questo punto, il messaggio hello diventa disponibile per l'elaborazione di nuovo.
* Controllare se è in aumento lunghezza coda hello nel tempo. Ciò può verificarsi se non si dispone tooprocess disponibili sufficienti lavoratori hello tutti i messaggi che altri thread di lavoro sono l'inserimento in coda hello. Controllare inoltre hello metriche toosee se hello ed Elimina le richieste non sono stati superati rimozione dalla coda di count per i messaggi, che potrebbe indicare ripetuti tentativi non riusciti toodelete hello messaggio.
* Analizzare i log di registrazione archiviazione hello per le operazioni di coda che hanno maggiore del previsto **E2ELatency** e **ServerLatency** valori in un periodo più lungo di tempo superiore al normale.

### <a name="metrics-show-an-increase-in-PercentThrottlingError"></a>Le metriche indicano un aumento di PercentThrottlingError
Quando si superano le destinazioni di scalabilità hello di un servizio di archiviazione, si verificano errori di limitazione delle richieste. il servizio di archiviazione Hello effettua questo tooensure che nessun client o tenant può usare servizio hello spese hello di altri utenti. Vedere <a href="http://msdn.microsoft.com/library/azure/dn249410.aspx" target="_blank">Obiettivi di scalabilità e prestazioni di Azure</a> per maggiori dettagli sugli obiettivi di scalabilità per gli account di archiviazione e gli obiettivi di prestazioni per le partizioni all'interno degli account di archiviazione.

Se hello **PercentThrottlingError** metrica mostrare un aumento percentuale hello di richieste che si è verificato un errore di limitazione, è necessario tooinvestigate uno dei seguenti scenari:

* [Aumento temporaneo di PercentThrottlingError]
* [Aumento permanente di PercentThrottlingError]

Un aumento **PercentThrottlingError** spesso avviene in hello stesso ora sotto forma di un aumento hello numero di richieste di archiviazione, o quando sono inizialmente il test di carico dell'applicazione. Questo può manifestarsi anche nel client hello come "503 Server occupato" o messaggi di stato HTTP "500 Timeout dell'operazione" da operazioni di archiviazione.

#### <a name="transient-increase-in-PercentThrottlingError"></a>Aumento temporaneo di PercentThrottlingError
Se vengono visualizzati eventuali picchi nel valore hello **PercentThrottlingError** che coincidono con periodi di intensa attività per un'applicazione hello, è necessario implementare un (non lineare) di backoff esponenziale strategia per i tentativi nel client: questo verrà ridurre il carico di immediato hello sulla partizione hello e Guida toosmooth l'applicazione out picchi di traffico. Per ulteriori informazioni su come i criteri di ripetizione tooimplement mediante hello libreria Client di archiviazione, vedere <a href="http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.retrypolicies.aspx" target="_blank">Microsoft.WindowsAzure.Storage.RetryPolicies Namespace</a> su MSDN.

> [!NOTE]
> È inoltre possibile visualizzare eventuali picchi nel valore hello **PercentThrottlingError** non coincidono con periodi di intensa attività per un'applicazione hello: hello qui causa più probabile è il servizio di archiviazione hello lo spostamento di partizioni tooimprove carico bilanciamento del carico.
> 
> 

#### <a name="permanent-increase-in-PercentThrottlingError"></a>Aumento permanente di PercentThrottlingError
Se viene visualizzato un valore costantemente elevato per **PercentThrottlingError** seguendo un aumento permanente dei volumi di transazioni o quando si esegue il caricamento iniziale test sull'applicazione, quindi è necessario tooevaluate modalità con cui l'applicazione utilizza le partizioni di archiviazione e se sta per raggiungere obiettivi di scalabilità hello per un account di archiviazione. Ad esempio, se si verifica la limitazione delle richieste di errori in una coda (che viene considerato come una singola partizione), considerare l'utilizzo di transazioni di hello toospread di code aggiuntive tra più partizioni. Se si verifica la limitazione delle richieste di errori in una tabella, è necessario tooconsider utilizzando un diverso toospread di schema di partizionamento delle transazioni tra più partizioni con una vasta gamma di valori di chiave di partizione. Una causa comune di questo problema è hello accodare o anteporre anti-pattern in cui si seleziona data hello come chiave di partizione hello e quindi tutti i dati in un determinato giorno viene scritto partizione tooone: sotto carico, questo può comportare un collo di bottiglia di scrittura. Può essere opportuno prendere in considerazione una progettazione diversa della partizione o valutare se l'utilizzo dell'archiviazione BLOB non sia una soluzione migliore. È inoltre necessario verificare se la limitazione delle richieste di hello si verifica in seguito a picchi di traffico e provare a utilizzare modalità di anti-aliasing del modello delle richieste di.

Se si distribuiscono le transazioni tra più partizioni, è necessario comunque tenere hello limiti di scalabilità per account di archiviazione hello. Ad esempio, se si utilizza dieci code ogni elaborazione hello massimo 2.000 1KB messaggi al secondo, sarà in hello limite generale di 20.000 messaggi al secondo per l'account di archiviazione hello. Se è necessario tooprocess più di 20.000 entità al secondo, è consigliabile usare più account di archiviazione. È inoltre tenere presente che le dimensioni hello delle richieste di e l'entità ha un impatto sui quando il servizio di archiviazione hello limita i client: se si dispone di maggiore di richieste e le entità, possono essere limitate prima.

Progettazione query non efficiente può essere causato anche si limiti di scalabilità toohit hello per le partizioni della tabella. Ad esempio, una query con un filtro che seleziona solo uno percento delle entità hello in una partizione, ma esegue l'analisi di tutte le entità hello in una partizione che sarà necessario tooaccess ogni entità. Ogni entità di lettura verrà considerato come uno numero totale di hello di transazioni in quella partizione; Pertanto, si possono facilmente raggiungere obiettivi di scalabilità hello.

> [!NOTE]
> I test delle prestazioni dovrebbero rivelare eventuali progettazioni inefficaci delle query nell'applicazione.
> 
> 

### <a name="metrics-show-an-increase-in-PercentTimeoutError"></a>Le metriche indicano un aumento di PercentTimeoutError
Le metriche indicano un aumento di **PercentTimeoutError** per uno dei servizi di archiviazione. In hello stesso tempo hello client riceve un numero elevato di messaggi di stato HTTP "500 Timeout dell'operazione" da operazioni di archiviazione.

> [!NOTE]
> È possibile riscontrare errori di timeout temporaneamente come servizio di archiviazione hello del carico delle richieste di saldi spostando un nuovo server tooa di partizione.
> 
> 

Hello **PercentTimeoutError** metrica è un'aggregazione di hello seguenti metriche: **ClientTimeoutError**, **AnonymousClientTimeoutError**,  **SASClientTimeoutError**, **ServerTimeoutError**, **AnonymousServerTimeoutError**, e **SASServerTimeoutError**.

timeout del server di Hello sono causati da un errore nel server di hello. timeout dei client Hello dovuto al fatto che un'operazione nel server di hello ha superato il timeout di hello specificato dal client hello. ad esempio, un client usando hello libreria Client di archiviazione può impostare un timeout per un'operazione utilizzando hello **ServerTimeout** proprietà di hello **QueueRequestOptions** classe.

Timeout del server indicare un problema con il servizio di archiviazione hello che richiede un'ulteriore analisi. Se si raggiunge i limiti di scalabilità hello per servizio hello e tooidentify eventuali picchi di traffico che potrebbero causare questo problema, è possibile utilizzare toosee metriche. Se il problema di hello è intermittente, potrebbe essere dovuto bilanciamento del carico tooload attività nel servizio hello. Se il problema di hello è permanente e non è causato dall'applicazione raggiunge i limiti di scalabilità hello del servizio di hello, è necessario generare un problema di supporto. Per i timeout dei client, è necessario decidere se hello timeout è impostato un valore appropriato tooan nel client hello e il valore di timeout hello modifica impostato nel client hello o analizzare come è possibile migliorare le prestazioni di hello di operazioni di hello nel servizio di archiviazione hello, per esempio ottimizzando le query di tabella o la riduzione delle dimensioni hello dei messaggi.

### <a name="metrics-show-an-increase-in-PercentNetworkError"></a>Le metriche indicano un aumento di PercentNetworkError
Le metriche indicano un aumento di **PercentNetworkError** per uno dei servizi di archiviazione. Hello **PercentNetworkError** metrica è un'aggregazione di hello seguenti metriche: **NetworkError**, **AnonymousNetworkError**, e  **SASNetworkError**. Si verifica quando il servizio di archiviazione hello rileva un errore di rete quando hello client effettua una richiesta di archiviazione.

la causa più comune di questo errore Hello è un client disconnessione prima della scadenza del timeout del servizio di archiviazione hello. È necessario esaminare il codice hello in toounderstand il client perché e quando il client di hello si disconnette dal servizio di archiviazione hello. È inoltre possibile utilizzare Wireshark, Microsoft Message Analyzer o problemi di connettività di rete Tcping tooinvestigate da client hello. Questi strumenti sono descritti in hello [appendici].

### <a name="the-client-is-receiving-403-messages"></a>client hello è la ricezione di messaggi HTTP 403 (accesso negato)
Se l'applicazione client che genera errori HTTP 403 (accesso negato), una causa probabile è che client hello utilizza un scaduti condiviso (firma di accesso) quando viene inviata una richiesta di archiviazione (anche se altre cause possibili includono le chiavi di orologio inclinazione, non è valido e vuoto intestazioni). Se una chiave di firma di accesso condiviso scaduta è causa di hello, si noterà non tutte le voci nei dati di log registrazione archiviazione sul lato server hello. Hello nella tabella seguente viene illustrato un esempio dal log di hello sul lato client generati da hello libreria Client di archiviazione che illustra questo problema si verifica:

| Sorgente | Livello di dettaglio | Livello di dettaglio | ID richiesta client | testo dell'operazione |
| --- | --- | --- | --- | --- |
| Microsoft.WindowsAzure.Storage |Informazioni |3 |85d077ab-… |Avvio operazione con posizione primaria in base alla modalità di posizionamento PrimaryOnly. |
| Microsoft.WindowsAzure.Storage |Informazioni |3 |85d077ab-… |Avvio sincrono richiesta toohttps://domemaildist.blob.core.windows.netazureimblobcontainer/blobCreatedViaSAS.txt?sv=2014-02-14&amp;sr = c&amp;si = mypolicy&amp;sig = OFnd4Rd7z01fIvh % 2BmcR6zbudIH2F5Ikm % 2FyhNYZEmJNQ % 3D&amp;api-version = 2014-02-14. |
| Microsoft.WindowsAzure.Storage |Informazioni |3 |85d077ab-… |In attesa di risposta. |
| Microsoft.WindowsAzure.Storage |Avviso |2 |85d077ab-… |Eccezione generata durante l'attesa della risposta: server remoto hello ha restituito un errore: (403) accesso negato... |
| Microsoft.WindowsAzure.Storage |Informazioni |3 |85d077ab-… |Risposta ricevuta. Codice stato = 403, ID richiesta = 9d67c64a-64ed-4b0d-9515-3b14bbcdc63d, Content-MD5 = , ETag = . |
| Microsoft.WindowsAzure.Storage |Avviso |2 |85d077ab-… |Eccezione generata durante l'operazione di hello: server remoto hello ha restituito un errore: (403) accesso negato... |
| Microsoft.WindowsAzure.Storage |Informazioni |3 |85d077ab-… |Verifica se ripetere l'operazione di hello. Numero di tentativi = 0, codice di stato HTTP 403, eccezione = = hello server remoto ha restituito un errore: (403) accesso negato... |
| Microsoft.WindowsAzure.Storage |Informazioni |3 |85d077ab-… |posizione successiva Hello è stato impostato tooPrimary, in base alla modalità percorso hello. |
| Microsoft.WindowsAzure.Storage |Tipi di errore |1 |85d077ab-… |Il criterio di ripetizione non ha consentito un nuovo tentativo. Esito negativo con server remoto hello ha restituito un errore: (403) accesso negato. |

In questo scenario, è necessario analizzare i motivi per cui il token di firma di accesso condiviso hello sta per scadere prima hello client invia al server di token toohello di hello:

* In genere, non è necessario impostare un'ora di inizio quando si crea una firma di accesso condiviso per un client di toouse immediatamente. Se vi sono piccole differenze di clock tra host hello generazione hello SAS utilizzando hello ora corrente e il servizio di archiviazione hello, è possibile per tooreceive servizio di archiviazione hello una firma di accesso condiviso che non è ancora valido.
* Non impostare tempi troppo brevi per la scadenza di una SAS. Nuovamente, differenze piccolo orologio tra host hello generazione hello SAS e il servizio di archiviazione hello può causare tooa SAS apparentemente scade prima del previsto.
* Hello parametro di versione nella chiave di firma di accesso condiviso hello (ad esempio **sv = 2012-02-12**) hello uguale alla versione di hello libreria Client di archiviazione in uso. È necessario utilizzare sempre hello versione hello libreria Client di archiviazione. Per altre informazioni sul controllo delle versioni dei token della firma di accesso condiviso, vedere le [novità di Archiviazione di Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/14/what-s-new-for-microsoft-azure-storage-at-teched-2014.aspx).
* * Se si rigenerano le chiavi di accesso di archiviazione (fare clic su **Gestisci chiavi di accesso** in qualsiasi pagina account di archiviazione nel portale di Azure classico hello) si può invalidare il token di firma di accesso condiviso esistente. Può trattarsi di un problema se si genera il token di firma di accesso condiviso con un'ora di scadenza lunga toocache applicazioni client.

Se si utilizza i token di firma di accesso condiviso toogenerate di hello libreria Client di archiviazione, è facile toobuild un token valido. Tuttavia, se si utilizza hello API REST di archiviazione e la creazione di token SAS hello manualmente è necessario leggere attentamente argomento hello <a href="http://msdn.microsoft.com/library/azure/ee395415.aspx" target="_blank">la delega dell'accesso con una firma di accesso condiviso</a> su MSDN.

### <a name="the-client-is-receiving-404-messages"></a>client hello è la ricezione di messaggi HTTP 404 (non trovato)
Se un'applicazione hello client riceve un messaggio HTTP 404 (non trovato) dal server di hello, ciò implica che il client hello oggetto hello stava tentando toouse (ad esempio, un'entità, tabella, blob, contenitore o coda) non esiste nel servizio di archiviazione hello. I motivi possono essere diversi, ad esempio:

* [eliminato in precedenza oggetto hello client Hello o un altro processo]
* [Si è verificato un problema di autenticazione della firma di accesso condiviso]
* [Il codice JavaScript sul lato client non dispone dell'autorizzazione tooaccess hello oggetto]
* [Errore della rete]

#### <a name="client-previously-deleted-the-object"></a>eliminato in precedenza oggetto hello client Hello o un altro processo
In scenari in cui hello client sta tentando tooread, aggiornamento o eliminazione di dati in un servizio di archiviazione che è in genere tooidentify semplice sul lato server hello registra un'operazione precedente eliminati oggetto hello in questione dal servizio di archiviazione hello. Molto spesso, i dati di log hello mostrano un altro utente o processo eliminato hello oggetto. Nel log di registrazione archiviazione sul lato server hello, hello-tipo di operazione e le colonne chiave di un oggetto richiesto mostrano quando un client ha eliminato un oggetto.

Nello scenario di hello in cui un client tenta tooinsert un oggetto, potrebbe non essere immediatamente evidente il motivo per cui il risultato in una risposta HTTP 404 (non trovato), dato che hello client crea un nuovo oggetto. Tuttavia, se il client di hello è la creazione di un blob che deve essere in grado di toofind hello contenitore blob, la se client hello è la creazione di un messaggio che deve essere in grado di toofind una coda, e se client hello viene aggiunta una riga deve essere tabella hello toofind in grado di.

È possibile utilizzare i log lato client hello da hello libreria Client di archiviazione toogain che più dettagliata comprensione delle specifiche richieste di invio hello del client toohello il servizio di archiviazione.

Hello seguenti log lato client generati dalla libreria Client di archiviazione hello illustra hello problema quando il client hello Impossibile trovare il contenitore di hello per blob hello che la creazione. Questo log include i dettagli di hello dopo operazioni di archiviazione:

| ID richiesta | Operazione |
| --- | --- |
| 07b26a5d-... |**DeleteIfExists** contenitore blob hello toodelete di metodo. Si noti che questa operazione include un **HEAD** richiesta toocheck esistenza hello del contenitore di hello. |
| e2d06d78… |**CreateIfNotExists** contenitore blob hello toocreate di metodo. Si noti che questa operazione include un **HEAD** richiesta che controlla l'esistenza di hello del contenitore di hello. Hello **HEAD** restituisce un messaggio 404 ma continua. |
| de8b1c3c-... |**UploadFromStream** blob hello toocreate di metodo. Hello **inserire** richiesta ha esito negativo con un messaggio 404 |

Voci del log:

| ID richiesta | testo dell'operazione |
| --- | --- |
| 07b26a5d-... |Avvio toohttps://domemaildist.blob.core.windows.net/azuremmblobcontainer richiesta sincrona. |
| 07b26a5d-... |StringToSign = HEAD............x-ms-client-request-id:07b26a5d-....x-ms-date:Tue, 03 Jun 2014 10:33:11 GMT.x-ms-version:2014-02-14./domemaildist/azuremmblobcontainer.restype:container. |
| 07b26a5d-... |In attesa di risposta. |
| 07b26a5d-... |Risposta ricevuta. Codice stato = 200, ID richiesta = eeead849-...Content-MD5 = , ETag =    &quot;0x8D14D2DC63D059B&quot;. |
| 07b26a5d-... |Le intestazioni di risposta sono state elaborate correttamente, procedere con il resto di hello dell'operazione di hello. |
| 07b26a5d-... |Download del corpo della risposta. |
| 07b26a5d-... |Operazione completata correttamente. |
| 07b26a5d-... |Avvio toohttps://domemaildist.blob.core.windows.net/azuremmblobcontainer richiesta sincrona. |
| 07b26a5d-... |StringToSign = DELETE............x-ms-client-request-id:07b26a5d-....x-ms-date:Tue, 03 Jun 2014 10:33:12    GMT.x-ms-version:2014-02-14./domemaildist/azuremmblobcontainer.restype:container. |
| 07b26a5d-... |In attesa di risposta. |
| 07b26a5d-... |Risposta ricevuta. Codice stato = 202, ID richiesta = 6ab2a4cf-..., Content-MD5 = , ETag =. |
| 07b26a5d-... |Le intestazioni di risposta sono state elaborate correttamente, procedere con il resto di hello dell'operazione di hello. |
| 07b26a5d-... |Download del corpo della risposta. |
| 07b26a5d-... |Operazione completata correttamente. |
| e2d06d78-... |Avvio toohttps://domemaildist.blob.core.windows.net/azuremmblobcontainer richiesta asincrona.</td> |
| e2d06d78-... |StringToSign = HEAD............x-ms-client-request-id:e2d06d78-....x-ms-date:Tue, 03 Jun 2014 10:33:12 GMT.x-ms-version:2014-02-14./domemaildist/azuremmblobcontainer.restype:container. |
| e2d06d78-... |In attesa di risposta. |
| de8b1c3c-... |Avvio toohttps://domemaildist.blob.core.windows.net/azuremmblobcontainer/blobCreated.txt richiesta sincrona. |
| de8b1c3c-... |StringToSign = PUT...64.qCmF+TQLPhq/YYK50mP9ZQ==........x-ms-blob-type:BlockBlob.x-ms-client-request-id:de8b1c3c-....x-ms-date:Tue, 03 Jun 2014 10:33:12 GMT.x-ms-version:2014-02-14./domemaildist/azuremmblobcontainer/blobCreated.txt. |
| de8b1c3c-... |Preparazione dei dati richiesta toowrite. |
| e2d06d78-... |Eccezione generata durante l'attesa della risposta: server remoto hello ha restituito un errore: (404) non trovato... |
| e2d06d78-... |Risposta ricevuta. Codice stato = 404, ID richiesta = 353ae3bc-..., Content-MD5 = , ETag =. |
| e2d06d78-... |Le intestazioni di risposta sono state elaborate correttamente, procedere con il resto di hello dell'operazione di hello. |
| e2d06d78-... |Download del corpo della risposta. |
| e2d06d78-... |Operazione completata correttamente. |
| e2d06d78-... |Avvio toohttps://domemaildist.blob.core.windows.net/azuremmblobcontainer richiesta asincrona. |
| e2d06d78-... |StringToSign = PUT...0.........x-ms-client-request-id:e2d06d78-....x-ms-date:Tue, 03 Jun 2014 10:33:12 GMT.x-ms-version:2014-02-14./domemaildist/azuremmblobcontainer.restype:container. |
| e2d06d78-... |In attesa di risposta. |
| de8b1c3c-... |Scrittura dei dati della richiesta. |
| de8b1c3c-... |In attesa di risposta. |
| e2d06d78-... |Eccezione generata durante l'attesa della risposta: server remoto hello ha restituito un errore: (409) conflitto... |
| e2d06d78-... |Risposta ricevuta. Codice stato = 409, ID richiesta = c27da20e-..., Content-MD5 = , ETag =. |
| e2d06d78-... |Download del corpo della risposta con errore. |
| de8b1c3c-... |Eccezione generata durante l'attesa della risposta: server remoto hello ha restituito un errore: (404) non trovato... |
| de8b1c3c-... |Risposta ricevuta. Codice stato = 404, ID richiesta = 0eaeab3e-..., Content-MD5 = , ETag =. |
| de8b1c3c-... |Eccezione generata durante l'operazione di hello: server remoto hello ha restituito un errore: (404) non trovato... |
| de8b1c3c-... |Il criterio di ripetizione non ha consentito un nuovo tentativo. Esito negativo con server remoto hello ha restituito un errore: (404) non trovato... |
| e2d06d78-... |Il criterio di ripetizione non ha consentito un nuovo tentativo. Esito negativo con server remoto hello ha restituito un errore: (409) conflitto... |

In questo esempio Mostra client hello è interfoliazione richieste da hello log hello **CreateIfNotExists** metodo (... e2d06d78 id richiesta) con le richieste hello hello **UploadFromStream** ((metodo) de8b1c3c-...). Questo avviene perché l'applicazione client hello chiama questi metodi in modo asincrono. È consigliabile modificare il codice asincrono di hello in hello client tooensure che crea contenitore hello prima di tentare di tooupload qualsiasi blob tooa dati in tale contenitore. La soluzione migliore sarebbe creare prima tutti i contenitori.

#### <a name="SAS-authorization-issue"></a>Si è verificato un problema di autenticazione della firma di accesso condiviso
Se un'applicazione client hello tenta una chiave di firma di accesso condiviso che non dispone delle autorizzazioni necessarie hello per operazione hello toouse, il servizio di archiviazione hello restituisce un client di toohello messaggio HTTP 404 (non trovato). In hello stesso tempo, verrà visualizzato anche un valore diverso da zero per **SASAuthorizationError** nelle metriche hello.

Hello nella tabella seguente viene mostrato un messaggio di log del server di esempio dal file di log di registrazione archiviazione hello:

| Nome | Valore |
| --- | --- |
| Orario di inizio richiesta | 2014-05-30T06:17:48.4473697Z |
| Tipo di operazione     | GetBlobProperties            |
| Stato della richiesta     | SASAuthorizationError        |
| Stato codice HTTP   | 404                          |
| Tipo di autenticazione| Sas                          |
| Tipo di servizio       | BLOB                         |
| URL richiesta        | https://domemaildist.blob.core.windows.net/azureimblobcontainer/blobCreatedViaSAS.txt |
| nbsp;              |   ?sv=2014-02-14&sr=c&si=mypolicy&sig=XXXXX&;api-version=2014-02-14 |
| intestazione dell'ID richiesta  | a1f348d5-8032-4912-93ef-b393e5252a3b |
| ID richiesta client  | 2d064953-8436-4ee0-aa0c-65cb874f7929 |

È necessario individuare perché tenta tooperform un'operazione non dispone delle autorizzazioni per l'applicazione client.

#### <a name="JavaScript-code-does-not-have-permission"></a>Il codice JavaScript sul lato client non dispone dell'autorizzazione tooaccess hello oggetto
Se si utilizza un client JavaScript e il servizio di archiviazione hello è restituzione di messaggi HTTP 404, per verificare gli errori JavaScript nel browser hello seguenti hello:

```
SEC7120: Origin http://localhost:56309 not found in Access-Control-Allow-Origin header.
SCRIPT7002: XMLHttpRequest: Network Error 0x80070005, Access is denied.
```

> [!NOTE]
> È possibile utilizzare gli strumenti di sviluppo F12 hello in Internet Explorer tootrace hello messaggi scambiati tra il browser hello e il servizio di archiviazione hello durante la risoluzione di problemi di JavaScript sul lato client.
> 
> 

Questi errori si verificano perché browser web hello implementa hello <a href="http://www.w3.org/Security/wiki/Same_Origin_Policy" target="_blank">criteri stessa origine</a> restrizione di sicurezza che impedisce che una pagina web chiama un'API in un dominio diverso dalla pagina di hello dominio hello proviene da.

toowork intorno hello problema JavaScript, è possibile configurare Cross condivisione risorse origini (CORS) per l'accesso client hello del servizio di archiviazione hello. Per altre informazioni, vedere <a href="http://msdn.microsoft.com/library/azure/dn535601.aspx" target="_blank">Supporto della condivisione delle risorse tra le origini (CORS) per i servizi di archiviazione Azure</a> su MSDN.

Hello nell'esempio di codice seguente viene illustrato come tooconfigure il blob del servizio tooallow JavaScript in esecuzione in hello tooaccess dominio Contoso un blob nel servizio di archiviazione di blob:

```csharp
CloudBlobClient client = new CloudBlobClient(blobEndpoint, new StorageCredentials(accountName, accountKey));
// Set hello service properties.
ServiceProperties sp = client.GetServiceProperties();
sp.DefaultServiceVersion = "2013-08-15";
CorsRule cr = new CorsRule();
cr.AllowedHeaders.Add("*");
cr.AllowedMethods = CorsHttpMethods.Get | CorsHttpMethods.Put;
cr.AllowedOrigins.Add("http://www.contoso.com");
cr.ExposedHeaders.Add("x-ms-*");
cr.MaxAgeInSeconds = 5;
sp.Cors.CorsRules.Clear();
sp.Cors.CorsRules.Add(cr);
client.SetServiceProperties(sp);
```

#### <a name="network-failure"></a>Errore della rete
In alcuni casi, i pacchetti di rete persa possono provocare il servizio di archiviazione toohello restituzione client toohello di messaggi HTTP 404. Ad esempio, quando l'applicazione client è l'eliminazione di un'entità dal servizio tabelle hello vedere hello client generano un'eccezione di archiviazione reporting un "HTTP 404 (non trovato)" messaggio di stato dal servizio tabelle hello. Quando si esamina la tabella hello nel servizio di archiviazione tabella hello, vedrai che il servizio hello eliminare entità hello come richiesto.

dettagli dell'eccezione Hello client hello includono id richiesta di hello (7e84f12d) assegnato dal servizio tabelle hello per richiesta hello: è possibile utilizzare questo toolocate hello richiesta informazioni nei registri di archiviazione sul lato server hello eseguendo una ricerca in hello  **intestazione di id richiesta** colonna nel file di log hello. È anche possibile usare hello metriche tooidentify quando gli errori, ad esempio questo si verificano e quindi cercare il file di log hello in base alle metriche di hello hello ora registrato l'errore. Questo Mostra voce di log che hello di eliminazione non riuscita con un messaggio di stato "HTTP (404) Client altro errore". Hello stessa voce di log include anche id richiesta hello generato dal client hello in hello **client-request-id** colonna (813ea74f).

log lato server Hello include anche un'altra voce con hello stesso **client-request-id** valore (813ea74f) per una corretta eliminazione per hello stessa entità, e da hello stesso client. Questa operazione di eliminazione ha avuto luogo poco prima della richiesta di eliminazione non hello.

Hello più probabile di questo scenario è che il client hello ha inviato una richiesta di eliminazione per hello entità toohello servizio tabelle, che ha avuto esito positivo, ma non ha ricevuto un acknowledgement dal server hello (probabilmente a causa il problema di rete temporanei tooa). client Hello quindi ripetute automaticamente nel operazione hello (utilizzando hello stesso **client-request-id**), questo nuovo tentativo non è riuscita perché l'entità hello era già stata eliminata.

Se il problema si verifica frequentemente, è necessario esaminare client hello motivi riconoscimenti tooreceive dal servizio tabelle hello. Se il problema di hello è intermittente, si deve trap di errore "HTTP (404) non trovato" hello e registrarla nel client hello, ma consentire hello client toocontinue.

### <a name="the-client-is-receiving-409-messages"></a>client hello è la ricezione di messaggi HTTP 409 (conflitto)
Hello nella tabella seguente viene illustrato un estratto del log sul lato server hello per le due operazioni di client: **DeleteIfExists** seguita immediatamente da **CreateIfNotExists** utilizzando hello stesso nome del contenitore blob. Si noti che ogni client operazione comporta due richieste inviate toohello server, prima di tutto un **GetContainerProperties** toocheck richiesta se il contenitore di hello esiste, seguito da hello **DeleteContainer** o  **CreateContainer** richiesta.

| Timestamp | Operazione | Risultato | Nome contenitore | ID richiesta client |
| --- | --- | --- | --- | --- |
| 05:10:13.7167225 |GetContainerProperties |200 |mmcont |c9f52c89-… |
| 05:10:13.8167325 |DeleteContainer |202 |mmcont |c9f52c89-… |
| 05:10:13.8987407 |GetContainerProperties |404 |mmcont |bc881924-… |
| 05:10:14.2147723 |CreateContainer |409 |mmcont |bc881924-… |

Elimina Hello codice hello client applicazione e quindi ricrea immediatamente un contenitore blob tramite hello stesso nome: hello **CreateIfNotExists** metodo (richiesta Client ID bc881924-...) alla fine ha esito negativo con hello HTTP 409 (conflitto) errore. Quando un client elimina i contenitori di blob, tabelle o code che si verifica un breve periodo prima nome hello diventa nuovamente disponibile.

un'applicazione Hello client deve utilizzare nomi di contenitore univoco a ogni volta che vengono create nuovi contenitori se il criterio di eliminazione e creazione di hello è comune.

### <a name="metrics-show-low-percent-success"></a>Le metriche indicano un valore PercentSuccess basso o le voci del log di analisi contengono operazioni con stato della transazione ClientOtherErrors
Hello **PercentSuccess** metrica acquisisce % hello delle operazioni che hanno avuto esito positivo in base relativi al codice di stato HTTP. Operazioni con i codici di stato di 2XX conteggio completata correttamente, mentre le operazioni con i codici di stato 3XX e 4XX o 5XX intervalli vengono conteggiate come esito negativo e minore hello **PercentSucess** valore della metrica. Nei file di log di archiviazione sul lato server hello, queste operazioni vengono registrate con lo stato delle transazioni **ClientOtherErrors**.

È importante toonote che queste operazioni sono state completate e pertanto non influire sulle altre metriche quali disponibilità. Alcuni esempi di operazioni eseguite correttamente ma che possono restituire codici di stato HTTP negativi sono:

* **ResourceNotFound** (non trovato 404), ad esempio da un'operazione GET richiesta tooa blob che non esiste.
* **ResouceAlreadyExists** (409 conflitto), ad esempio da un **CreateIfNotExist** operazione in cui la risorsa hello esiste già.
* **ConditionNotMet** (non modificato 304), ad esempio da un'operazione condizionale, ad esempio quando un client invia un **ETag** valore e un HTTP **If-None-Match** toorequest intestazione un'immagine solo se è stato aggiornato dall'ultima operazione hello.

È possibile trovare un elenco di codici di errore comuni API REST che restituiscono i servizi di archiviazione hello nella pagina hello <a href="http://msdn.microsoft.com/library/azure/dd179357.aspx" target="_blank">comuni codici di errore API REST</a>.

### <a name="capacity-metrics-show-an-unexpected-increase"></a>Le metriche della capacità indicano un aumento imprevisto dell'uso della capacità di archiviazione
Se viene visualizzato improvvisi, modifiche impreviste nell'utilizzo della capacità nell'account di archiviazione, è possibile esaminare i motivi hello analizzando le metriche di disponibilità; ad esempio, un aumento nel numero di hello di richieste di eliminazione potrebbe causare tooan aumento in una quantità di spazio di archiviazione blob che si utilizza come operazioni di pulizia specifico dell'applicazione che si aspetterebbe toobe liberare lo spazio potrebbe non funzionare come previsto (hello l'esempio, perché è scaduti il token di firma di accesso condiviso hello utilizzati per liberare lo spazio).

### <a name="you-are-experiencing-unexpected-reboots"></a>Si stanno verificando riavvii imprevisti delle macchine virtuali di Azure con un numero elevato di VHD allegati
Se una macchina virtuale di Azure (VM) è un numero elevato di dischi rigidi virtuali collegati in hello stesso account di archiviazione, si può superare obiettivi di scalabilità hello per un singolo account di archiviazione causando toofail VM hello. È consigliabile controllare metrica al minuto per l'account di archiviazione hello hello (**TotalRequests**/**TotalIngress**/**TotalEgress**) per i picchi obiettivi di scalabilità hello per un account di archiviazione superiore. Vedere la sezione hello "[metriche mostrano un aumento PercentThrottlingError]" per determinare se la limitazione delle richieste è stata eseguita su account di archiviazione.

In generale, ogni singolo input o output operazione in un disco rigido virtuale da una macchina virtuale viene convertita troppo**ottenere pagina** o **Put Page** operazioni su hello sottostante blob di pagine. Pertanto, è possibile utilizzare hello stimato IOPS per l'ambiente tootune quanti dischi rigidi virtuali è possibile disporre in un singolo account di archiviazione in base alle comportamento specifico di hello dell'applicazione. Non è consigliabile usare più di 40 dischi virtuali in un unico account di archiviazione. Vedere <a href="http://msdn.microsoft.com/library/azure/dn249410.aspx" target="_blank">Azure obiettivi di scalabilità e prestazioni</a> per informazioni dettagliate di obiettivi di scalabilità per account di archiviazione corrente hello, in particolare hello richiesta totale frequenza e totale della larghezza di banda per il tipo di hello dell'account di archiviazione in uso .
Se è stato superato obiettivi di scalabilità hello dell'account di archiviazione, è consigliabile inserire i dischi rigidi virtuali in più spazio di archiviazione diverso account tooreduce hello attività per ogni singolo account.

### <a name="your-issue-arises-from-using-the-storage-emulator"></a>Il problema si verifica di utilizzare l'emulatore di archiviazione hello per lo sviluppo o test
In genere usare l'emulatore di archiviazione hello durante lo sviluppo e test tooavoid hello requisito per un account di archiviazione di Azure. Hello i problemi comuni che possono verificarsi quando si utilizza l'emulatore di archiviazione hello sono:

* [Funzionalità "X" non funziona nell'emulatore di archiviazione hello]
* [Errore "valore hello per una delle intestazioni HTTP hello non è nel formato corretto hello" quando utilizzando hello emulatore di archiviazione]
* [Emulatore di archiviazione in esecuzione hello richiede privilegi amministrativi]

#### <a name="feature-X-is-not-working"></a>Funzionalità "X" non funziona nell'emulatore di archiviazione hello
emulatore di archiviazione Hello non supporta tutte le funzioni hello di servizi di archiviazione di Azure hello come servizio file hello. Per ulteriori informazioni, vedere <a href="http://msdn.microsoft.com/library/azure/gg433135.aspx" target="_blank">differenze tra hello emulatore di archiviazione e servizi di archiviazione Azure</a> su MSDN.

Per le funzionalità hello archiviazione emulatore non supporta, utilizzare il servizio di archiviazione di Azure hello nel cloud hello.

#### <a name="error-HTTP-header-not-correct-format"></a>Errore "valore hello per una delle intestazioni HTTP hello non è nel formato corretto hello" quando utilizzando hello emulatore di archiviazione
Si sta testando l'applicazione che utilizzano ad esempio hello libreria Client di archiviazione su hello archiviazione locale emulatore e chiamate al metodo **CreateIfNotExists** non riesce con errore hello il messaggio "hello valore per una delle intestazioni HTTP hello non è in Hello formato corretto." Ciò indica che hello versione dell'emulatore di archiviazione hello in uso non supporta la versione di hello della libreria client di archiviazione hello in uso. Libreria Client di archiviazione Hello aggiunge intestazione hello **x-ms-version** tooall hello richiede rende. Se emulatore di archiviazione hello non riconosce il valore di hello in hello **x-ms-version** intestazione, rifiuta la richiesta di hello.

È possibile utilizzare il valore hello del Client di archiviazione libreria registri toosee hello di hello **intestazione x-ms-version** di invio. È inoltre possibile visualizzare il valore di hello di hello **intestazione x-ms-version** se si utilizzano le richieste di hello tootrace Fiddler dall'applicazione client.

Questo scenario si verifica in genere quando si installa e usare hello l'ultima versione di hello libreria Client di archiviazione senza aggiornare l'emulatore di archiviazione hello. Si deve installare una versione più recente di hello dell'emulatore di archiviazione hello oppure utilizzare l'archiviazione cloud anziché emulatore hello per lo sviluppo e test.

#### <a name="storage-emulator-requires-administrative-privileges"></a>Emulatore di archiviazione in esecuzione hello richiede privilegi amministrativi
Quando si esegue l'emulatore di archiviazione hello verrà chiesto di credenziali di amministratore. Ciò si verifica solo quando si inizializza emulatore di archiviazione hello hello per la prima volta. Dopo aver inizializzato l'emulatore di archiviazione hello, non è necessario privilegi amministrativi toorun nuovamente.

Per ulteriori informazioni, vedere <a href="http://msdn.microsoft.com/library/azure/gg433132.aspx" target="_blank">hello inizializzazione emulatore di archiviazione da hello tramite lo strumento da riga di comando</a> su MSDN (è possibile inizializzare anche emulatore di archiviazione hello in Visual Studio, che verrà inoltre richiede privilegi amministrativi).

### <a name="you-are-encountering-problems-installing-the-Windows-Azure-SDK"></a>Si sono verificati problemi di installazione hello Azure SDK per .NET
Quando si tenta di hello tooinstall SDK, l'esito negativo durante il tentativo dell'emulatore di archiviazione hello tooinstall sul computer locale. log dell'installazione Hello contiene uno dei seguenti messaggi hello:

* CAQuietExec: Errore: istanza di SQL Server non è possibile tooaccess
* CAQuietExec: Errore: Impossibile toocreate database

causa Hello è un problema con l'installazione del database locale esistente. Per impostazione predefinita, emulatore di archiviazione hello Usa dati toopersist LocalDB simula hello servizi di archiviazione Azure. È possibile reimpostare l'istanza di LocalDB eseguendo i seguenti comandi in una finestra del prompt dei comandi prima di tentare di hello tooinstall SDK hello.

```
sqllocaldb stop v11.0
sqllocaldb delete v11.0
delete %USERPROFILE%\WAStorageEmulatorDb3*.*
sqllocaldb create v11.0
```

Hello **eliminare** comando rimuove qualsiasi file di database precedenti da installazioni precedenti dell'emulatore di archiviazione hello.

### <a name="you-have-a-different-issue-with-a-storage-service"></a>Si è verificato un problema diverso con un servizio di archiviazione
Se le sezioni di risoluzione dei problemi precedente hello non includono problema hello con un servizio di archiviazione, è necessario adottare hello dopo l'approccio toodiagnosing e la risoluzione dei problemi relativi al problema.

* Controllare la metrica toosee se vengono apportate modifiche dal comportamento previsto di linea di base. Dalle metriche di hello, potrebbe essere in grado di toodetermine se il problema hello è temporaneo o permanente e le operazioni di archiviazione hello problema interessa.
* È possibile utilizzare le informazioni di metrica hello toohelp cercare i dati dei log sul lato server per informazioni più dettagliate sugli errori che si sono verificati. Queste informazioni consentono di risolvere il problema di hello.
* Se hello informazioni nei registri di hello sul lato server non sono sufficienti problema di hello tootroubleshoot correttamente, è possibile utilizzare il comportamento hello libreria Client di archiviazione sul lato client registri tooinvestigate hello dell'applicazione client e gli strumenti, ad esempio, Fiddler, Wireshark, Microsoft Message Analyzer tooinvestigate e della rete.

Per ulteriori informazioni sull'uso di Fiddler, vedere "[appendice 1: il traffico HTTP e HTTPS toocapture tramite Fiddler]."

Per ulteriori informazioni sull'utilizzo Wireshark, vedere "[appendice 2: il traffico di rete utilizzando Wireshark toocapture]."

Per ulteriori informazioni sull'utilizzo di Microsoft Message Analyzer, vedere "[appendice 3: il traffico di rete utilizzando Microsoft Message Analyzer toocapture]."

## <a name="appendices"></a>Appendici
appendici Hello vengono descritti i diversi strumenti che possono risultare utili durante la diagnosi e la risoluzione dei problemi di archiviazione di Azure (e altri servizi). Tali strumenti non fanno parte del servizio di archiviazione Azure e alcuni sono prodotti di terze parti. Di conseguenza, gli strumenti di hello descritti in queste appendici non sono coperto da un contratto di supporto che potrebbe avere con Microsoft Azure o di archiviazione di Azure, e pertanto come parte del processo di valutazione è necessario esaminare hello licenze e supporto per le opzioni disponibili da provider di Hello di questi strumenti.

### <a name="appendix-1"></a>Appendice 1: Utilizzo di Fiddler toocapture HTTP e il traffico HTTPS
Fiddler è uno strumento utile per analizzare il traffico HTTP e HTTPS hello tra l'applicazione client e hello servizio di archiviazione di Azure in uso. È possibile scaricare Fiddler all'indirizzo <a href="http://www.telerik.com/fiddler" target="_blank">http://www.telerik.com/fiddler</a>.

> [!NOTE]
> Fiddler è grado di decodificare il traffico HTTPS; leggere attentamente la documentazione di Fiddler hello toounderstand suo funzionamento e le implicazioni di sicurezza hello toounderstand.
> 
> 

Questa appendice vengono fornite una breve procedura dettagliata di come il traffico tooconfigure Fiddler toocapture tra hello locale in cui sia stato installato Fiddler hello servizi di archiviazione Azure.

Dopo l'avvio, Fiddler inizia ad acquisire il traffico HTTP e HTTPS sul computer locale. di seguito Hello sono alcuni comandi utili per il controllo Fiddler:

* Interruzione e avvio dell'acquisizione del traffico. Menu principale, hello andare troppo**File** e quindi fare clic su **acquisire il traffico** tootoggle acquisizione e disattivare.
* Salvare i dati del traffico acquisiti. Menu principale, hello andare troppo**File**, fare clic su **salvare**, quindi fare clic su **tutte le sessioni**: in questo modo il traffico di hello toosave in un file di archivio di sessione. È possibile inviarla se ha richiesto il supporto di tooMicrosoft o ricaricare un archivio di sessione in un secondo momento per l'analisi.

quantità di hello toolimit di Fiddler consente di acquisire il traffico, è possibile utilizzare i filtri che si configura in hello **filtri** hello scheda seguente schermata mostra un filtro che acquisisce solo il traffico inviato toohello  **contosoemaildist.Table.Core.Windows.NET** endpoint di archiviazione:

![][5]

### <a name="appendix-2"></a>Appendice 2: Utilizzo del traffico di rete toocapture Wireshark
Wireshark è un analizzatore di protocollo di rete che consente di tooview pacchetto informazioni dettagliate per un'ampia gamma di protocolli di rete. È possibile scaricare Wireshark all'indirizzo <a href="http://www.wireshark.org/" target="_blank">http://www.wireshark.org/</a>.

Hello procedura riportata di seguito viene illustrato come toocapture pacchetto informazioni dettagliate per il traffico dal computer locale hello in cui è installato servizio di Wireshark toohello tabelle nell'account di archiviazione di Azure.

1. Avviare Wireshark sul computer locale.
2. In hello **avviare** sezione, un'interfaccia di rete locale selezionare hello o interfacce che sono connesso toohello internet.
3. Fare clic su **Capture Options**.
4. Aggiungere un filtro toohello **Filtro acquisizione** casella di testo. Ad esempio, **host contosoemaildist.table.core.windows.net** configurerà Wireshark toocapture solo i pacchetti inviati tooor dall'endpoint del servizio tabelle hello in hello **contosoemaildist** archiviazione account. Per un elenco completo dei filtri di acquisizione, vedere <a href="http://wiki.wireshark.org/CaptureFilters" target="_blank">http://wiki.wireshark.org/CaptureFilters</a>.
   
   ![][6]
5. Fare clic su **Avvia**. Wireshark ora consente di acquisire tutti tooor di trasmissione di pacchetti di hello dall'endpoint del servizio tabelle hello quando si utilizza l'applicazione client nel computer locale.
6. Al termine, fare clic su menu principale di hello **acquisire** e quindi **arrestare**.
7. hello toosave acquisiti i dati in un File di acquisizione Wireshark, hello dal menu principale scegliere **File** e quindi **salvare**.

WireShark verranno evidenziati eventuali errori presenti in hello **packetlist** finestra. È inoltre possibile utilizzare hello **Info esperto** finestra (fare clic su **Analizza**, quindi **Info esperto**) tooview un riepilogo degli errori e avvisi.

![][7]

È inoltre possibile scegliere i dati TCP hello tooview come livello di applicazione hello vengono visualizzati facendo clic sul hello dati TCP e selezionando **seguire il flusso TCP**. Ciò è particolarmente utile se si acquisisce il dump senza un filtro di acquisizione. Leggere <a href="http://www.wireshark.org/docs/wsug_html_chunked/ChAdvFollowTCPSection.html" target="_blank">qui</a> per ulteriori informazioni.

![][8]

> [!NOTE]
> Per ulteriori informazioni sull'utilizzo Wireshark, vedere hello <a href="http://www.wireshark.org/docs/wsug_html_chunked/" target="_blank">manuale dell'utente Wireshark</a>.
> 
> 

### <a name="appendix-3"></a>Appendice 3: Utilizzo del traffico di rete di Microsoft Message Analyzer toocapture
È possibile utilizzare Microsoft Message Analyzer toocapture HTTP e il traffico HTTPS in una tooFiddler modo simile e acquisire il traffico di rete in un tooWireshark modo simile.

#### <a name="configure-a-web-tracing-session-using-microsoft-message-analyzer"></a>Configurazione di una sessione di traccia Web tramite Microsoft Message Analyzer
tooconfigure una sessione di analisi web per il traffico HTTP e HTTPS utilizzando Microsoft Message Analyzer, eseguire l'applicazione di Microsoft Message Analyzer hello e quindi hello **File** menu, fare clic su **/traccia**. Nell'elenco di scenari di traccia disponibili hello selezionare **Proxy Web**. Quindi in hello **configurazione dello Scenario di traccia** pannello, hello **HostnameFilter** casella di testo, aggiungere nomi hello degli endpoint di archiviazione (è possibile cercare questi nomi nel portale di Azure classico hello). Ad esempio, se hello nome dell'account di archiviazione di Azure è **contosodata**, è consigliabile aggiungere hello seguente toohello **HostnameFilter** casella di testo:

```
contosodata.blob.core.windows.net contosodata.table.core.windows.net contosodata.queue.core.windows.net
```

> [!NOTE]
> Un carattere di spazio separa i nomi host hello.
> 
> 

Quando si è pronti toostart la raccolta dei dati di traccia, fare clic su hello **Start With** pulsante.

Per ulteriori informazioni su Microsoft Message Analyzer hello **Proxy Web** di traccia, vedere <a href="http://technet.microsoft.com/library/jj674814.aspx" target="_blank">Provider PEF WebProxy</a> su TechNet.

Hello incorporato **Proxy Web** traccia in Microsoft Message Analyzer è basata sul Fiddler; può acquisire il traffico HTTPS sul lato client e visualizzare messaggi HTTPS non crittografati. Hello **Proxy Web** funziona tramite la configurazione di un proxy locale per tutto il traffico HTTP e HTTPS che fornisce accesso toounencrypted messaggi di traccia.

#### <a name="diagnosing-network-issues-using-microsoft-message-analyzer"></a>Diagnosi dei problemi di rete con Microsoft Message Analyzer
Inoltre toousing hello Microsoft Message Analyzer **Proxy Web** dettagli toocapture traccia di hello traffico HTTP/HTTPs tra un'applicazione hello client e servizio di archiviazione hello, è possibile inoltre utilizzare hello predefinito  **Livello di collegamento locale** toocapture informazioni sul pacchetto di rete di traccia. In questo modo si toocapture dati simili toothat che è possibile acquisire con Wireshark e diagnosticare problemi di rete, ad esempio pacchetti ignorati.

Hello schermata riportata di seguito viene illustrato un esempio **il livello di collegamento locale** traccia con alcuni **informativo** messaggi hello **DiagnosisTypes** colonna. Fare clic su un'icona hello **DiagnosisTypes** colonna Mostra i dettagli di hello del messaggio hello. In questo esempio, il server di hello ritrasmesso messaggio &#305; perché non ha ricevuto un acknowledgement da client hello:

![][9]

Quando si crea la sessione di traccia hello in Microsoft Message Analyzer, è possibile specificare filtri tooreduce hello livello rumore nella traccia hello. In hello **acquisire / traccia** pagina in cui viene definita la traccia hello, fare clic su hello **configura** collegamento troppo Avanti**PacketCapture-Microsoft-Windows-NDIS**. Hello seguente schermata mostra una configurazione che consente di filtrare il traffico TCP per gli indirizzi IP hello dei tre servizi di archiviazione:

![][10]

Per ulteriori informazioni su hello traccia Microsoft messaggio Analyzer locale livello di collegamento, vedere <a href="http://technet.microsoft.com/library/jj659264.aspx" target="_blank">Provider PEF-NDIS-PacketCapture</a> su TechNet.

### <a name="appendix-4"></a>Appendice 4: Utilizzando i dati di metrica e di log tooview di Excel
Molti strumenti consentono di dati di metrica di archiviazione di hello toodownload dall'archiviazione tabelle di Azure in un formato delimitato da virgole che rende i dati di hello tooload semplice in Excel per la visualizzazione e analisi. I dati della registrazione dell'archiviazione provenienti dai BLOB di Azure sono già in un formato delimitato che può essere caricato in Excel. Tuttavia, sarà necessario intestazioni di colonna appropriata tooadd basato sede informazioni hello in <a href="http://msdn.microsoft.com/library/azure/hh343259.aspx" target="_blank">formato di archiviazione Analitica Log</a> e <a href="http://msdn.microsoft.com/library/azure/hh343264.aspx" target="_blank">Schema di tabella delle metriche di archiviazione Analitica</a>.

tooimport i dati di registrazione archiviazione in Excel dopo aver scaricano dall'archiviazione blob:

* In hello **dati** menu, fare clic su **dal testo**.
* Sfoglia file di log toohello tooview desiderato e fare clic su **importazione**.
* Nel passaggio 1 di hello **importazione guidata testo**selezionare **delimitato**.

Nel passaggio 1 di hello **importazione guidata testo**selezionare **punto e virgola** come hello solo delimitatore e scegliere di virgolette doppie come hello **qualificatore di testo**. Quindi fare clic su **fine** scegliere dove tooplace hello dati nella cartella di lavoro.

### <a name="appendix-5"></a>Appendice 5: Monitoraggio con Application Insights per Visual Studio Team Services
È possibile utilizzare anche funzionalità di hello Application Insights per Visual Studio Team Services durante il monitoraggio delle prestazioni e disponibilità. Questo strumento consente di:

* Assicurarsi che il servizio Web sia disponibile e reattivo. Se l'app è un sito web o un'app di dispositivo che usa un servizio web, può verificare l'URL ogni pochi minuti da posizioni di tutto il mondo hello e consentono di sapere se si verifica un problema.
* Diagnosticare rapidamente eventuali problemi di prestazioni o eccezioni del servizio Web. Sapere se la CPU o altre risorse vengono estese, ricavare analisi dello stack dalle eccezioni ed eseguire facilmente la ricerca delle tracce nei log. Se hello scende di prestazioni dell'app sotto limiti accettabili, è possibile inviare un messaggio di posta elettronica. L'utente può monitorare i servizi Web sia .NET che Java.

In hello fase di scrittura di Application Insights è in anteprima. Per altre informazioni, vedere <a href="http://msdn.microsoft.com/library/azure/dn481095.aspx" target="_blank">Application Insights per Visual Studio Team Services su MSDN</a>.

<!--Anchors-->
[Introduzione]: #introduction
[Organizzazione di questa guida]: #how-this-guide-is-organized

[monitoraggio del servizio di archiviazione]: #monitoring-your-storage-service
[Monitoraggio dello stato del servizio]: #monitoring-service-health
[Monitoraggio della capacità]: #monitoring-capacity
[Monitoraggio della disponibilità]: #monitoring-availability
[Monitoraggio delle prestazioni]: #monitoring-performance

[la diagnosi dei problemi di archiviazione]: #diagnosing-storage-issues
[Problemi di stato del servizio]: #service-health-issues
[Problemi di prestazioni]: #performance-issues
[Diagnostica degli errori]: #diagnosing-errors
[Problemi dell'emulatore di archiviazione]: #storage-emulator-issues
[Strumenti di registrazione dell'archiviazione]: #storage-logging-tools
[Uso degli strumenti di registrazione in rete]: #using-network-logging-tools

[traccia End-to-end]: #end-to-end-tracing
[Correlazione dei dati di log]: #correlating-log-data
[ID richiesta client]: #client-request-id
[ID richiesta Server]: #server-request-id
[Timestamp]: #timestamps

[le indicazioni di Troubleshooting]: #troubleshooting-guidance
[metrica Mostra AverageE2ELatency alta e bassa AverageServerLatency]: #metrics-show-high-AverageE2ELatency-and-low-AverageServerLatency
[Metrica Mostra AverageE2ELatency bassa e bassa AverageServerLatency ma hello client si è verificato ad alta latenza]: #metrics-show-low-AverageE2ELatency-and-low-AverageServerLatency
[Le metriche indicano un valore AverageServerLatency alto]: #metrics-show-high-AverageServerLatency
[Si stanno verificando ritardi imprevisti nel recapito dei messaggi di una coda]: #you-are-experiencing-unexpected-delays-in-message-delivery

[metriche mostrano un aumento PercentThrottlingError]: #metrics-show-an-increase-in-PercentThrottlingError
[Aumento temporaneo di PercentThrottlingError]: #transient-increase-in-PercentThrottlingError
[Aumento permanente di PercentThrottlingError]: #permanent-increase-in-PercentThrottlingError
[metriche mostrano un aumento PercentTimeoutError]: #metrics-show-an-increase-in-PercentTimeoutError
[Le metriche indicano un aumento di PercentNetworkError]: #metrics-show-an-increase-in-PercentNetworkError

[client hello è la ricezione di messaggi HTTP 403 (accesso negato)]: #the-client-is-receiving-403-messages
[client hello è la ricezione di messaggi HTTP 404 (non trovato)]: #the-client-is-receiving-404-messages
[eliminato in precedenza oggetto hello client Hello o un altro processo]: #client-previously-deleted-the-object
[Si è verificato un problema di autenticazione della firma di accesso condiviso]: #SAS-authorization-issue
[Il codice JavaScript sul lato client non dispone dell'autorizzazione tooaccess hello oggetto]: #JavaScript-code-does-not-have-permission
[Errore della rete]: #network-failure
[client hello è la ricezione di messaggi HTTP 409 (conflitto)]: #the-client-is-receiving-409-messages

[metrica Mostra PercentSuccess bassa o voci di log analitica sono operazioni con stato delle transazioni di ClientOtherErrors]: #metrics-show-low-percent-success
[Le metriche della capacità indicano un aumento imprevisto dell'uso della capacità di archiviazione]: #capacity-metrics-show-an-unexpected-increase
[Si stanno verificando riavvii imprevisti delle macchine virtuali con un numero elevato di VHD allegati]: #you-are-experiencing-unexpected-reboots
[Il problema si verifica di utilizzare l'emulatore di archiviazione hello per lo sviluppo o test]: #your-issue-arises-from-using-the-storage-emulator
[Funzionalità "X" non funziona nell'emulatore di archiviazione hello]: #feature-X-is-not-working
[Errore "valore hello per una delle intestazioni HTTP hello non è nel formato corretto hello" quando utilizzando hello emulatore di archiviazione]: #error-HTTP-header-not-correct-format
[Emulatore di archiviazione in esecuzione hello richiede privilegi amministrativi]: #storage-emulator-requires-administrative-privileges
[Si sono verificati problemi di installazione hello Azure SDK per .NET]: #you-are-encountering-problems-installing-the-Windows-Azure-SDK
[Si è verificato un problema diverso con un servizio di archiviazione]: #you-have-a-different-issue-with-a-storage-service

[appendici]: #appendices
[appendice 1: il traffico HTTP e HTTPS toocapture tramite Fiddler]: #appendix-1
[appendice 2: il traffico di rete utilizzando Wireshark toocapture]: #appendix-2
[appendice 3: il traffico di rete utilizzando Microsoft Message Analyzer toocapture]: #appendix-3
[Appendice 4: Utilizzando i dati di metrica e di log tooview di Excel]: #appendix-4
[appendice 5: monitoraggio con Application Insights per Visual Studio Team Services]: #appendix-5

<!--Image references-->
[1]: ./media/storage-monitoring-diagnosing-troubleshooting-classic-portal/overview.png
[2]: ./media/storage-monitoring-diagnosing-troubleshooting-classic-portal/portal-screenshot.png
[3]: ./media/storage-monitoring-diagnosing-troubleshooting-classic-portal/hour-minute-metrics.png
[4]: ./media/storage-monitoring-diagnosing-troubleshooting-classic-portal/high-e2e-latency.png
[5]: ./media/storage-monitoring-diagnosing-troubleshooting-classic-portal/fiddler-screenshot.png
[6]: ./media/storage-monitoring-diagnosing-troubleshooting-classic-portal/wireshark-screenshot-1.png
[7]: ./media/storage-monitoring-diagnosing-troubleshooting-classic-portal/wireshark-screenshot-2.png
[8]: ./media/storage-monitoring-diagnosing-troubleshooting-classic-portal/wireshark-screenshot-3.png
[9]: ./media/storage-monitoring-diagnosing-troubleshooting-classic-portal/mma-screenshot-1.png
[10]: ./media/storage-monitoring-diagnosing-troubleshooting-classic-portal/mma-screenshot-2.png
