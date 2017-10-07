---
title: aaaTroubleshooting archiviazione di Azure con diagnostica & Message Analyzer | Documenti Microsoft
description: Esercitazione che illustra la risoluzione dei problemi end-to-end mediante Analisi archiviazione di Azure, AzCopy e Microsoft Message Analyzer
services: storage
documentationcenter: dotnet
author: robinsh
manager: timlt
ms.assetid: 6b23cba5-0d53-439e-870b-de8e406107d8
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: robinsh
ms.openlocfilehash: 74ee126bab30b9a45f4904a065b6fe3006f76101
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="end-to-end-troubleshooting-using-azure-storage-metrics-and-logging-azcopy-and-message-analyzer"></a>Risoluzione dei problemi end-to-end con le metriche e la registrazione di Archiviazione di Azure, AzCopy e Message Analyzer
[!INCLUDE [storage-selector-portal-e2e-troubleshooting](../../includes/storage-selector-portal-e2e-troubleshooting.md)]

## <a name="overview"></a>Panoramica
Diagnostica e risoluzione dei problemi sono competenze fondamentali per la creazione e il supporto di applicazioni client con Archiviazione di Microsoft Azure. A causa di natura toohello distribuito di un'applicazione Azure, la diagnosi e la risoluzione dei problemi di prestazioni può essere più complessi in ambienti tradizionali.

In questa esercitazione verrà illustrato come client tooidentify alcuni errori che potrebbero influire sulle prestazioni e risolvere gli errori da end-to-end utilizzando gli strumenti forniti da Microsoft e di archiviazione di Azure in un'applicazione client hello toooptimize ordine.

Questa esercitazione offre un'esplorazione pratica di uno scenario di risoluzione dei problemi end-to-end. Per un'applicazione di archiviazione di Azure tootroubleshooting Guida concettuale approfondita, vedere [Monitor, diagnosticare e risolvere i problemi di archiviazione di Microsoft Azure](storage-monitoring-diagnosing-troubleshooting.md).

## <a name="tools-for-troubleshooting-azure-storage-applications"></a>Strumenti per la risoluzione dei problemi delle applicazioni di archiviazione di Azure
tootroubleshoot di applicazioni client che usano l'archiviazione di Microsoft Azure, è possibile utilizzare una combinazione di strumenti toodetermine quando si è verificato un problema e può essere determinato quali hello problema hello. Questi strumenti comprendono:

* **Analisi archiviazione di Azure**. [Analisi archiviazione di Azure](http://msdn.microsoft.com/library/azure/hh343270.aspx) fornisce metriche e registrazioni per Archiviazione di Azure.

  * **metriche di archiviazione** tengono traccia delle metriche relative alle transazioni e alla capacità per l'account di archiviazione. Uso delle metriche, è possibile determinare le prestazioni dell'applicazione secondo tooa diverse misure diverse. Vedere [Schema di tabella delle metriche di archiviazione Analitica](http://msdn.microsoft.com/library/azure/hh343264.aspx) per ulteriori informazioni sui tipi di hello delle metriche monitorate dall'archiviazione Analitica.
  * **Registrazione archiviazione** registra ogni registro toohello Azure Storage services tooa sul lato server richiesta. Hello log tracce dati dettagliati per ogni richiesta, inclusa l'operazione hello eseguite stato hello dell'operazione hello e informazioni sulla latenza. Vedere [formato di archiviazione Analitica Log](http://msdn.microsoft.com/library/azure/hh343259.aspx) per ulteriori informazioni sui dati di richiesta e risposta hello scritto toohello log dall'archiviazione Analitica.

> [!NOTE]
> Account di archiviazione con un tipo di replica di archiviazione con ridondanza della zona (ZRS) non dispone delle metriche hello o abilitata al momento la funzionalità di registrazione.
>
>

* **Portale di Azure classico**. È possibile configurare le metriche e registrazione per l'account di archiviazione in hello [portale di Azure classico](https://manage.windowsazure.com). È possibile visualizzare i grafici che mostrano le prestazioni dell'applicazione nel tempo e configurare gli avvisi toonotify che se nell'applicazione viene eseguita in modo diverso rispetto a previsto per una metrica specificata.

    Vedere [monitorare un account di archiviazione nel portale di Azure hello](storage-monitor-storage-account.md) per informazioni sulla configurazione del monitoraggio nel portale di Azure classico hello.
* **AzCopy**. Log del server per l'archiviazione di Azure vengono archiviati come BLOB, pertanto è possibile utilizzare AzCopy toocopy hello BLOB tooa locale directory del registro per l'analisi utilizzando Microsoft Message Analyzer. Vedere [trasferire i dati con l'utilità della riga di comando di AzCopy hello](storage-use-azcopy.md) per ulteriori informazioni su AzCopy.
* **Microsoft Message Analyzer**. Message Analyzer è uno strumento che utilizza i file di log e visualizza i dati di log in un formato visivo che rende facile toofilter, ricerca e gruppo di registrare i dati in set utili che è possibile utilizzare tooanalyze errori e problemi di prestazioni. Per altre informazioni su Message Analyzer, vedere [la guida operativa di Microsoft Message Analyzer](http://technet.microsoft.com/library/jj649776.aspx) .

## <a name="about-hello-sample-scenario"></a>Su scenario di esempio hello
In questa esercitazione verrà esaminato uno scenario in cui le metriche di Archiviazione di Azure indicano una bassa percentuale di operazioni riuscite per un'applicazione che chiama Archiviazione di Azure. Hello metrica frequenza bassa percentuale di successo (visualizzate come **PercentSuccess** nel portale di Azure classico hello e nelle tabelle di metrica hello) tiene traccia delle operazioni eseguite con esito positivo, ma che restituiscono un codice di stato HTTP è maggiore di 299. Nei file di log di archiviazione sul lato server hello, queste operazioni vengono registrate con lo stato delle transazioni **ClientOtherErrors**. Per ulteriori informazioni su metrica bassa percentuale di successo hello, vedere [metrica Mostra PercentSuccess bassa o voci di log analitica sono operazioni con lo stato delle transazioni di ClientOtherErrors](storage-monitoring-diagnosing-troubleshooting.md#metrics-show-low-percent-success).

Le operazioni di Archiviazione di Azure possono restituire codici di stato HTTP maggiori di 299 in condizioni di funzionalità normali. Ma in alcuni casi questi errori indicano che è in grado di toooptimize l'applicazione client per prestazioni migliorate.

In questo scenario, si vedrà un toobe frequenza bassa percentuale di successo un valore inferiore al 100%. È possibile scegliere un metrica livello diverso, tuttavia, in base alle esigenze tooyour. Durante il test dell'applicazione è consigliabile definire una tolleranza di base per le metriche delle prestazioni chiave. Ad esempio, sulla base dei test è possibile che si stabilisca che l'applicazione deve avere una percentuale di operazioni riuscite costante del 90% o 85%. Se i dati di metrica mostrano che l'applicazione hello è allontanarsi dalle tale numero, è possibile esaminare che possono causare hello aumento.

Per questo scenario di esempio, una volta è stata stabilita metrica relativa al tasso percentuale di successo hello è inferiore al 100%, verrà esaminare hello registri toofind hello errori correlati toohello metriche e usarli toofigure il causa percentuale di successo percentuale inferiore di hello. Verrà esaminato in particolare gli errori nell'intervallo di 400 hello. esaminando in dettaglio gli errori 404 (Non trovato).

### <a name="some-causes-of-400-range-errors"></a>Alcune cause degli errori della fascia 400
esempio Hello riportato di seguito viene illustrato un campionamento di alcuni errori di 400 intervallo per le richieste nel servizio di archiviazione Blob di Azure e le possibili cause. Uno di questi errori, nonché gli errori in hello 300 intervallo e hello 500, possono contribuire frequenza bassa percentuale di successo tooa.

Si noti che hello elencati di seguito non sono complete. Vedere [lo stato e codici di errore](http://msdn.microsoft.com/library/azure/dd179382.aspx) per informazioni dettagliate sugli errori generali di archiviazione di Azure e su tooeach specifico di errori dei servizi di archiviazione hello.

**Esempi di codice di stato 404 (Non trovato)**

Si verifica quando un'operazione di lettura in un contenitore o blob non hello blob o contenitore non è stato trovato.

* Si verifica se un contenitore o BLOB è stato eliminato da un altro client prima di questa richiesta.
* Si verifica se si utilizza una chiamata di API che consente di creare blob o contenitore hello dopo aver controllato l'esistenza. Hello CreateIfNotExists APIs rendere HEAD toocheck prima di chiamare l'esistenza di hello di hello contenitore o blob; Se non esiste, viene restituito un errore 404, e viene effettuata una chiamata PUT secondo toowrite hello contenitore o blob.

**Esempi di codice di stato 409 (Conflitto)**

* Si verifica se si utilizza un toocreate API di creare un nuovo contenitore o blob, senza prima verificare esistenza e un contenitore o blob con lo stesso nome esiste già.
* Si verifica se un contenitore è stato eliminato e si tenta un nuovo contenitore con stesso nome prima che venga completata l'operazione di eliminazione hello hello toocreate.
* Si verifica se si specifica un lease in un contenitore o BLOB ed è già presente un lease.

**Esempi di codice di stato 412 (Condizione preliminare non riuscita)**

* Si verifica quando non è stata soddisfatta la condizione di hello specificata da un'intestazione condizionale.
* Si verifica quando l'ID lease hello specificato non corrisponde all'ID di lease hello nella hello contenitore o blob.

## <a name="generate-log-files-for-analysis"></a>Generare file di log per l'analisi
In questa esercitazione si userà Message Analyzer toowork con tre diversi tipi di file di log, anche se è possibile scegliere toowork con uno qualsiasi di questi elementi:

* Hello **log server**, che viene creato quando si abilita la registrazione di archiviazione di Azure. log del server Hello contiene dati relativi a ogni operazione viene chiamato su uno dei servizi di archiviazione di Azure hello - blob, coda, tabella e file. log del server di Hello indica quale operazione è stato chiamato e il codice di stati restituiti, nonché altri dettagli sull'hello richiesta e risposta.
* Hello **log del client .NET**, che viene creato quando si abilita la registrazione dal lato client all'interno dell'applicazione .NET. log Hello del client include informazioni dettagliate su come client hello Prepara hello richiesta e riceve ed elabora la risposta hello.
* Hello **log di traccia di rete HTTP**, che raccoglie i dati sui dati di richiesta e risposta HTTP/HTTPS, incluso per le operazioni nel servizio di archiviazione Azure. In questa esercitazione, si verrà generato di traccia di rete hello tramite Message Analyzer.

### <a name="configure-server-side-logging-and-metrics"></a>Configurare le metriche e la registrazione sul lato server
In primo luogo, è necessario tooconfigure la registrazione di archiviazione di Azure e le misure, in modo che si dispone di dati da hello client applicazione tooanalyze. È possibile configurare la registrazione e metrica in diversi modi: tramite hello [portale di Azure classico](https://manage.windowsazure.com), usando PowerShell, o a livello di codice. Per informazioni dettagliate sulla configurazione di registrazione e metrica, vedere [Enabling Storage Metrics and Viewing Metrics Data](http://msdn.microsoft.com/library/azure/dn782843.aspx) (Abilitazione delle metriche di archiviazione e visualizzazione dei dati di metrica) e [Enabling Storage Logging and Accessing Log Data](http://msdn.microsoft.com/library/azure/dn782840.aspx) (Abilitazione della registrazione e accesso ai dati del log di archiviazione).

**Tramite hello portale classico di Azure**

tooconfigure registrazione e metrica per l'account di archiviazione usando il portale di hello, seguire le istruzioni di hello in [monitorare un account di archiviazione nel portale di Azure hello](storage-monitor-storage-account.md).

> [!NOTE]
> Non è possibile tooset metrica al minuto utilizzando hello portale classico di Azure. Tuttavia, è consigliabile impostare li hello a scopo di questa esercitazione e per analizzare i problemi di prestazioni con l'applicazione. È possibile impostare le metriche al minuto mediante PowerShell, come illustrato di seguito, oppure a livello di codice o tramite hello portale classico di Azure.
>
> Si noti che hello portale classico di Azure non è possibile visualizzare le metriche al minuto, solo le metriche orarie.
>
>

**Tramite PowerShell**

tooget introduttiva a PowerShell per Azure, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).

1. Hello utilizzare [Add-AzureAccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0) tooadd cmdlet toohello finestra di PowerShell dell'account dell'utente di Azure:

    ```powershell
     Add-AzureAccount
    ```

2. In hello **Accedi tooMicrosoft Azure** finestra, indirizzo di posta elettronica di tipo hello e la password associata al proprio account. Azure autentica e Salva le informazioni sulle credenziali hello e chiude la finestra hello.
3. Impostare hello predefinito storage account toohello account di archiviazione in uso per l'esercitazione hello tramite l'esecuzione di questi comandi nella finestra di PowerShell hello:

    ```powershell
    $SubscriptionName = 'Your subscription name'
    $StorageAccountName = 'yourstorageaccount'
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
    ```

4. Abilitare la registrazione per hello servizio Blob di archiviazione:

    ```powershell
    Set-AzureStorageServiceLoggingProperty -ServiceType Blob -LoggingOperations Read,Write,Delete -PassThru -RetentionDays 7 -Version 1.0
    ```

5. Abilitare metriche di archiviazione per il servizio Blob, rendendo tooset che hello **- MetricsType** troppo`Minute`:

    ```powershell
    Set-AzureStorageServiceMetricsProperty -ServiceType Blob -MetricsType Minute -MetricsLevel ServiceAndApi -PassThru -RetentionDays 7 -Version 1.0
    ```

### <a name="configure-net-client-side-logging"></a>Configurare la registrazione sul lato client .NET
tooconfigure sul lato client la registrazione per un'applicazione .NET, abilitare la diagnostica .NET nel file di configurazione dell'applicazione hello (Web. config o App. config). Vedere [registrazione con hello libreria Client di archiviazione .NET sul lato Client](http://msdn.microsoft.com/library/azure/dn782839.aspx) e [registrazione con Microsoft Azure Storage SDK per Java hello sul lato Client](http://msdn.microsoft.com/library/azure/dn782844.aspx) per informazioni dettagliate.

log lato client Hello include informazioni dettagliate su come client hello Prepara hello richiesta e riceve ed elabora la risposta hello.

Libreria Client di archiviazione Hello archivia i dati di log lato client nel percorso di hello specificato nel file di configurazione dell'applicazione hello (Web. config o App. config).

### <a name="collect-a-network-trace"></a>Raccogliere una traccia di rete
È possibile utilizzare Message Analyzer toocollect una traccia di rete HTTP/HTTPS, mentre è in esecuzione l'applicazione client. Messaggio Usa analizzatore [Fiddler](http://www.telerik.com/fiddler) su hello back-end. Prima di raccogliere la traccia di rete hello, si consiglia di configurare il traffico HTTPS Fiddler toorecord non crittografato:

1. Installare [Fiddler](http://www.telerik.com/download/fiddler).
2. Avviare Fiddler.
3. Selezionare **Tools | Fiddler Options** (Strumenti | Opzioni Fiddler).
4. Nella finestra di dialogo Opzioni hello, assicurarsi che **acquisire connette HTTPS** e **decrittografare il traffico HTTPS** sono entrambe selezionate, come illustrato di seguito.

![Configurare le opzioni Fiddler](./media/storage-e2e-troubleshooting-classic-portal/fiddler-options-1.png)

Per esercitazione hello, raccogliere e salvare una traccia di rete prima di tutto in Message Analyzer, quindi creare una traccia di analisi della sessione tooanalyze hello e hello registri. toocollect una traccia di rete in Message Analyzer:

1. In Message Analyzer selezionare **File | Quick Trace | Unencrypted HTTPS** (File | Traccia rapida | HTTPS non crittografato).
2. traccia Hello inizierà immediatamente. Selezionare **arrestare** toostop hello traccia in modo che sia possibile configurarlo tootrace solo traffico di archiviazione.
3. Selezionare **modifica** sessione di traccia tooedit hello.
4. Seleziona hello **configura** collegamento toohello a destra di hello **Pef-Microsoft-WebProxy** provider ETW.
5. In hello **impostazioni avanzate** finestra di dialogo, fare clic su hello **Provider** scheda.
6. In hello **filtro Hostname** , specificare gli endpoint di archiviazione, separati da spazi. Ad esempio, è possibile specificare gli endpoint come segue: modificare `storagesample` toohello nome dell'account di archiviazione:

    ```   
    storagesample.blob.core.windows.net storagesample.queue.core.windows.net storagesample.table.core.windows.net
    ```

7. Uscire dalla finestra di dialogo hello e fare clic su **riavviare** toobegin di raccolta traccia di hello con filtro di nome host hello sul posto, in modo che solo il traffico di rete di archiviazione di Azure è incluso nella traccia hello.

> [!NOTE]
> Dopo aver completato la raccolta la traccia di rete, è consigliabile ripristinare le impostazioni di hello modificate del traffico HTTPS toodecrypt Fiddler. Nella finestra di dialogo Opzioni Fiddler hello, deselezionare hello **acquisire connette HTTPS** e **decrittografare il traffico HTTPS** caselle di controllo.
>
>

Vedere [con funzionalità di traccia di rete hello](http://technet.microsoft.com/library/jj674819.aspx) su Technet per ulteriori dettagli.

## <a name="review-metrics-data-in-hello-azure-classic-portal"></a>Esaminare i dati di metrica in hello portale classico di Azure
Dopo l'applicazione è stata eseguita per un periodo di tempo, è possibile esaminare i grafici di metriche di hello visualizzati nel hello portale di Azure classico tooobserve come l'esecuzione del servizio. In primo luogo, aggiungeremo hello **percentuale di completamento** pagina monitoraggio toohello metrica:

1. Passare toohello Dashboard dell'account di archiviazione in hello [portale di Azure classico](https://manage.windowsazure.com), quindi selezionare **monitoraggio** hello tooview pagina di monitoraggio.
2. Fare clic su **Aggiungi metriche** toodisplay hello **Scegli metriche** finestra di dialogo.
3. Scorrere verso il basso hello toofind **percentuale di completamento** gruppo, espandere il nodo, quindi selezionare **aggregazione**, come illustrato nell'immagine di hello riportata di seguito. Questa metrica aggrega i dati delle percentuali di operazioni riuscite da tutte le operazioni BLOB.

![Scegli metriche](./media/storage-e2e-troubleshooting-classic-portal/choose-metrics-portal-1.png)

Nel portale di Azure classico hello, si noterà ora **percentuale di completamento** in hello grafico di monitoraggio, insieme a eventuali altre metriche vengono aggiunte (backup toosix possono essere visualizzati sul grafico hello contemporaneamente). Nell'immagine hello riportato di seguito, è possibile visualizzare che la velocità di percentuale di successo hello è leggermente inferiore al 100%, ovvero scenario hello che analizzeremo successivamente dall'analisi dei log hello in Message Analyzer:

![Grafico delle metriche nel portale](./media/storage-e2e-troubleshooting-classic-portal/portal-metrics-chart-1.png)

Per ulteriori informazioni sull'aggiunta di pagina di monitoraggio toohello metriche, vedere [procedura: aggiungere una tabella delle metriche di metriche toohello](storage-monitor-storage-account.md#add-metrics-charts-to-the-portal-dashboard).

> [!NOTE]
> Dopo aver abilitato la metrica di archiviazione potrebbe richiedere del tempo per il tooappear di dati di metrica in hello portale classico di Azure. Questo avviene perché metrica oraria per hello ora precedente non viene visualizzata nel portale di Azure classico hello fino a quando non hello è trascorso l'ora corrente. Inoltre, le metriche al minuto non vengono visualizzate nel portale di Azure classico hello. A seconda di quando si abilita metriche, potrà richiedere i dati di metrica toosee tootwo ore.
>
>

## <a name="use-azcopy-toocopy-server-logs-tooa-local-directory"></a>Utilizzare directory locale di AzCopy toocopy server log tooa
Archiviazione di Azure scrive tooblobs di dati del Registro di server, mentre la metrica viene scritta tootables. BLOB dei log sono disponibili in hello noto `$logs` contenitore per l'account di archiviazione. BLOB dei log sono denominate in modo gerarchico per anno, mese, giorno e ora, in modo che l'intervallo di tempo desiderato tooinvestigate di hello consentono di individuare facilmente. Ad esempio, in hello `storagesample` account, il contenitore di hello per BLOB dei log hello per da 8-09: 00, 01/02/2015 `https://storagesample.blob.core.windows.net/$logs/blob/2015/01/08/0800`. BLOB di singoli Hello in questo contenitore sono denominati in sequenza, a partire da `000000.log`.

È possibile utilizzare toodownload strumento da riga di comando di AzCopy hello questi log lato server file tooa nel percorso desiderato nel computer locale. Ad esempio, è possibile utilizzare i seguenti file di comando toodownload hello log per operazioni di blob che hanno portato posizionare su hello 2 gennaio 2015 toohello cartella `C:\Temp\Logs\Server`; sostituire `<storageaccountname>` con nome hello dell'account di archiviazione, e `<storageaccountkey>` con il chiave di accesso account:

```azcopy
AzCopy.exe /Source:http://<storageaccountname>.blob.core.windows.net/$logs /Dest:C:\Temp\Logs\Server /Pattern:"blob/2015/01/02" /SourceKey:<storageaccountkey> /S /V
```

AzCopy è disponibile per il download hello [download di Azure](https://azure.microsoft.com/downloads/) pagina. Per informazioni dettagliate sull'uso di AzCopy, vedere [trasferire i dati con l'utilità della riga di comando di AzCopy hello](storage-use-azcopy.md).

Per altre informazioni sul download dei log sul lato server, vedere [Download dei dati di log di Registrazione archiviazione](http://msdn.microsoft.com/library/azure/dn782840.aspx#DownloadingStorageLogginglogdata).

## <a name="use-microsoft-message-analyzer-tooanalyze-log-data"></a>Utilizzare i dati di log di Microsoft Message Analyzer tooanalyze
Microsoft Message Analyzer è uno strumento per l'acquisizione, la visualizzazione e l'analisi del traffico di messaggistica del protocollo, degli eventi e di altri messaggi del sistema o dell'applicazione in scenari di diagnostica e risoluzione dei problemi. Message Analyzer anche consente tooload, aggregazione e analizzare i dati di log e salvare i file di traccia. Per altre informazioni su Message Analyzer, vedere la [guida operativa di Microsoft Message Analyzer](http://technet.microsoft.com/library/jj649776.aspx).

Message Analyzer include risorse di archiviazione di Azure che consentono di tooanalyze server, client e i registri di rete. In questa sezione verrà illustrato come toouse tooaddress tali strumenti hello problema di bassa percentuale di successo in hello i log di archiviazione.

### <a name="download-and-install-message-analyzer-and-hello-azure-storage-assets"></a>Scaricare e installare Analizzatore messaggi hello risorse di archiviazione di Azure
1. Scaricare [Message Analyzer](http://www.microsoft.com/download/details.aspx?id=44226) da hello Microsoft Download Center ed eseguire l'installazione guidata di hello.
2. Avviare Message Analyzer.
3. Da hello **strumenti** dal menu **gestione Asset**. In hello **gestione Asset** finestra di dialogo Seleziona **Scarica**, quindi filtrare in base **di archiviazione di Azure**. Risorse di archiviazione di Azure hello, verrà visualizzato come illustrato nell'immagine di hello riportata di seguito.
4. Fare clic su **sincronizzazione tutti visualizzati gli elementi** hello tooinstall risorse di archiviazione di Azure. le risorse disponibili Hello includono:
   * **Regole colore archiviazione Azure:** regole colore di archiviazione di Azure consentono di filtri speciali toodefine che utilizzano il colore, testo, e tipo di carattere stili toohighlight messaggi che contengono informazioni specifiche in una traccia.
   * **Grafici di Archiviazione di Azure:** i grafici di Archiviazione di Azure sono grafici predefiniti in cui vengono riportati i dati di log del server. Si noti che toouse grafici di archiviazione di Azure in questo momento, è possibile solo carico hello server log in hello Analysis griglia.
   * **Parser di archiviazione Azure:** hello del client di archiviazione di Azure hello analisi archiviazione di Azure parser, server e HTTP in ordine toodisplay li registra in hello Analysis griglia.
   * **I filtri di archiviazione Azure:** i filtri di archiviazione di Azure sono i criteri predefiniti che è possibile utilizzare tooquery i dati in analisi griglia hello.
   * **Layout della visualizzazione di archiviazione Azure:** layout della visualizzazione di archiviazione di Azure sono raggruppamenti nella griglia Analysis hello e layout di colonne predefinite.
5. Dopo aver installato gli asset hello, riavviare Message Analyzer.

![Gestione asset di Message Analyzer](./media/storage-e2e-troubleshooting-classic-portal/mma-start-page-1.png)

> [!NOTE]
> Installare tutti gli asset di archiviazione di Azure hello scopo hello di questa esercitazione.
>
>

### <a name="import-your-log-files-into-message-analyzer"></a>Importare i file di log in Message Analyzer
È possibile importare tutti i file di log salvati (lato server, lato client e rete) in un'unica sessione di Microsoft Message Analyzer per l'analisi.

1. In hello **File** Microsoft Message Analyzer, scegliere **nuova sessione**, quindi fare clic su **sessione vuoto**. In hello **nuova sessione** finestra di dialogo immettere un nome per la sessione di analisi. In hello **i dettagli di sessione** pannello, fare clic su hello **file** pulsante.
2. data di tooload hello rete traccia generati dal Message Analyzer, fare clic su **Aggiungi file**, toohello percorso in cui è stato salvato il file .matp dalla sessione di analisi web, file .matp hello select, e fare clic su **aprire**.
3. dati di log lato server hello tooload, fare clic su **Aggiungi file**individuare toohello percorso in cui sono stati scaricati i registri sul lato server, selezionare il file di log hello per intervallo di tempo hello tooanalyze desiderato e fare clic su **aprire**. Quindi, nel hello **i dettagli di sessione** pannello, hello set **configurazione del Registro di testo** elenco a discesa per ogni file di log sul lato server troppo**AzureStorageLog** tooensure da Microsoft Message Analyzer è possibile analizzare il file di log hello correttamente.
4. dati di log lato client hello tooload, fare clic su **Aggiungi file**individuare toohello percorso in cui sono stati salvati i log lato client, selezionare i file di log hello tooanalyze desiderato e fare clic su **aprire**. Quindi, nel hello **i dettagli di sessione** pannello, hello set **configurazione del Registro di testo** elenco a discesa per ogni file di log lato client troppo**AzureStorageClientDotNetV4** tooensure che Microsoft Message Analyzer è possibile analizzare il file di log hello correttamente.
5. Fare clic su **avviare** in hello **nuova sessione** finestra di dialogo tooload e analisi hello dati del log. Consente di visualizzare i dati di log Hello nella griglia di analisi Analizzatore messaggi hello.

immagine Hello riportata di seguito viene illustrato un esempio di sessione configurato con un server, client e file di log di traccia di rete.

![Configurare la sessione di Message Analyzer](./media/storage-e2e-troubleshooting-classic-portal/configure-mma-session-1.png)

Si noti che Message Analyzer carica i file di log in memoria. Se si dispone di un ampio set di dati del log, è opportuno toofilter in ordine tooget hello migliori prestazioni da Message Analyzer.

Innanzitutto, determinare l'intervallo di tempo hello che si è interessati a esaminare e mantenere ridotte al massimo questo periodo di tempo. In molti casi sarà necessario tooreview un periodo di minuti o ore al massimo. Importare hello set più piccolo dei log in grado di soddisfare le proprie esigenze.

Se si dispone ancora di una grande quantità di dati del log, quindi è consigliabile toospecify un toofilter filtro sessione i dati dei log prima di caricarli. In hello **filtro sessione** casella, seleziona hello **libreria** pulsante toochoose un filtro predefinito; ad esempio, scegliere **filtro I globale tempo** da hello i filtri di archiviazione di Azure toofilter in un intervallo di tempo. È quindi possibile modificare hello toospecify criteri filtro di hello avvio e interruzione timestamp per intervallo hello si desidera toosee. È possibile filtrare anche utilizzando un codice di stato specifico. ad esempio, è possibile scegliere tooload solo voci del registro in cui il codice di stato hello è 404.

Per altre informazioni sull'importazione dei dati di log in Microsoft Message Analyzer, vedere [l'argomento relativo al recupero dei dati dei messaggi su](http://technet.microsoft.com/library/dn772437.aspx) TechNet.

### <a name="use-hello-client-request-id-toocorrelate-log-file-data"></a>Utilizzare hello client richiesta ID toocorrelate dati del file registro
Hello Azure Storage Client Library genera automaticamente un ID richiesta client univoci per ogni richiesta. Questo valore viene scritto toohello client log, log server hello e traccia di rete hello, è possibile utilizzarlo toocorrelate dati in tutte e tre i registri in Message Analyzer. Vedere [ID richiesta Client](storage-monitoring-diagnosing-troubleshooting.md#client-request-id) per ulteriori informazioni su client hello ID richiesta.

Hello nelle sezioni seguenti vengono descrivono come toouse preconfigurato e viste di un layout personalizzato toocorrelate e raggruppamento dei dati basano su richiesta del client hello ID.

### <a name="select-a-view-layout-toodisplay-in-hello-analysis-grid"></a>Selezionare un toodisplay layout visualizzazione nella griglia Analysis hello
Risorse di archiviazione Hello per Message Analyzer includono layout visualizzazione di archiviazione di Azure che sono configurati in precedenza viste che è possibile utilizzare toodisplay i dati con le colonne e i raggruppamenti utili per scenari diversi. È anche possibile creare layout di visualizzazione personalizzati e salvarli per riutilizzarli in futuro.

immagine di Hello seguente vengono illustrati hello **visualizzazione Layout** menu, disponibile selezionando **visualizzazione Layout** dalla barra multifunzione di hello barra degli strumenti. layout della visualizzazione Hello per l'archiviazione di Azure sono raggruppate sotto hello **di archiviazione di Azure** nodo nel menu hello. È possibile cercare `Azure Storage` in toofilter casella di ricerca hello nell'archiviazione di Azure consente di visualizzare solo i layout. È inoltre possibile selezionare hello star Avanti tooa visualizzazione layout toomake it a preferito e visualizzarlo nella parte superiore di hello del menu hello.

![Menu Visualizza layout](./media/storage-e2e-troubleshooting-classic-portal/view-layout-menu.png)

toobegin, con l'istruzione select **raggruppati per modulo e ClientRequestID**. In questo layout di visualizzazione sono raggruppati i dati dei tre log prima in base all'ID richiesta client, quindi in base al file di log di origine (o **Modulo** in Message Analyzer). Questa visualizzazione consente di eseguire il drill-down in un particolare ID richiesta client e visualizzare i dati dei tre file di log per tale ID richiesta client.

immagine di Hello riportata di seguito viene illustrato questo layout visualizzazione applicata toohello registro dati di esempio, un subset di colonne visualizzate. È possibile visualizzare per un ID richiesta client specifico, hello Analysis griglia visualizza i dati di log client hello e log del server di traccia di rete.

![Layout di visualizzazione di Archiviazione di Azure](./media/storage-e2e-troubleshooting-classic-portal/view-layout-client-request-id-module.png)

> [!NOTE]
> Diversi file di log sono colonne diverse, pertanto quando dati da più file di log viene visualizzati nella griglia di analisi di hello, alcune colonne non possono contenere i dati per una determinata riga. Nell'immagine hello precedente, ad esempio, le righe di log client non Mostra tutti i dati per hello **Timestamp**, **TimeElapsed**, **origine**, e **destinazione** colonne, perché queste colonne non sono presenti nel log hello del client, ma presenti nella traccia di rete hello. Analogamente, hello **Timestamp** colonna vengono visualizzati i dati timestamp log hello del server, ma non vengono visualizzati dati per hello **TimeElapsed**, **origine**, e  **Destinazione** colonne, che non fanno parte del log di hello del server.
>
>

Inoltre layout della visualizzazione di toousing hello archiviazione di Azure, è possibile anche definire e salvare layout personalizzati della visualizzazione. È possibile selezionare altri campi desiderati per il raggruppamento di dati e salvare il raggruppamento di hello come parte di oltre il layout personalizzato.

### <a name="apply-color-rules-toohello-analysis-grid"></a>Applicare toohello regole colore della griglia di analisi
Risorse di archiviazione Hello includono anche le regole di colore, che offrono che un oggetto visivo significa tooidentify diversi tipi di errori di analisi griglia hello. Hello predefiniti regole colore si applicano tooHTTP errori, pertanto verranno visualizzati solo per la traccia di log e di rete server hello.

Selezionare le regole colore, tooapply **regole colore** dalla barra multifunzione di hello barra degli strumenti. Si noterà che le regole colore hello archiviazione di Azure nel menu hello. Per hello esercitazione, selezionare **gli errori del Client (codice di stato compreso tra 400 e 499)**, come illustrato nell'immagine di hello riportata di seguito.

![Layout di visualizzazione di Archiviazione di Azure](./media/storage-e2e-troubleshooting-classic-portal/color-rules-menu.png)

Inoltre le regole dei colori hello toousing di archiviazione di Azure, è anche possibile definire e salvare le regole colore.

### <a name="group-and-filter-log-data-toofind-400-range-errors"></a>Raggruppamento e il filtro log dati toofind 400-errori di intervallo
Successivamente, si sarà raggruppare e filtrare hello log dati toofind tutti gli errori di intervallo hello 400.

1. Individuare hello **StatusCode** colonna nella griglia Analysis, colonna di hello pulsante destro del mouse sull'intestazione e seleziona hello **gruppo**.
2. Successivamente, a un gruppo in hello **ClientRequestId** colonna. Si noterà che i dati hello hello che Analysis griglia ora è organizzata in base allo stato del codice e da una richiesta client ID.
3. Visualizza finestra degli strumenti di filtro di visualizzazione hello se non è già visualizzato. Nella barra multifunzione di hello, selezionare **finestre degli strumenti**, quindi **filtro di visualizzazione**.
4. toofilter hello log toodisplay intervalli 400 solo errori di dati, aggiungere hello toohello di criteri di filtro seguenti **filtro di visualizzazione** finestra e fare clic su **applica**:

    ```   
    (AzureStorageLog.StatusCode >= 400 && AzureStorageLog.StatusCode <=499) || (HTTP.StatusCode >= 400 && HTTP.StatusCode <= 499)
    ```

immagine di Hello seguente mostra risultati hello di questo raggruppamento e filtro. Espansione hello **ClientRequestID** campo sotto hello raggruppamento per il codice di stato 409, ad esempio, viene illustrata un'operazione che ha generato il codice di stato.

![Layout di visualizzazione di Archiviazione di Azure](./media/storage-e2e-troubleshooting-classic-portal/400-range-errors1.png)

Dopo aver applicato il filtro, si noterà che le righe dal log di hello client vengono escluse, come hello log del client non include un **StatusCode** colonna. verrà quindi restituito toohello log tooexamine hello client le operazioni dei client che ha portato toothem toobegin con, verrà esaminato server hello ed 404 errori toolocate di rete registri traccia.

> [!NOTE]
> È possibile filtrare hello **StatusCode** colonna e visualizzare i dati da tutti i tre log, ad esempio hello log client, se si aggiunge un filtro toohello espressione che include le voci di log in cui il codice di stato hello è null. tooconstruct questa espressione di filtro, utilizzare:
>
> <code>&#42;StatusCode >= 400 or !&#42;StatusCode</code>
>
> Questo filtro restituisce tutte le righe da client hello solo le righe dal log di hello del server e di log HTTP e log in cui il codice di stato di hello è maggiore di 400. Se si applica il layout di visualizzazione toohello raggruppato per ID richiesta client e il modulo, è possibile cercare o scorrere hello log toofind voci quelli in cui sono rappresentati tutte e tre i registri.   
>
>

### <a name="filter-log-data-toofind-404-errors"></a>Filtrare 404 errori toofind dati di log
Risorse di archiviazione Hello includono filtri predefiniti che è possibile utilizzare toonarrow registra dati toofind hello errori o le tendenze che si sta cercando. Successivamente, si applicherà due filtri predefiniti: uno che filtra server hello e registri di traccia di rete per gli 404 errori e uno che filtra i dati di hello su un intervallo di tempo specificato.

1. Visualizza finestra degli strumenti di filtro di visualizzazione hello se non è già visualizzato. Nella barra multifunzione di hello, selezionare **finestre degli strumenti**, quindi **filtro di visualizzazione**.
2. Nella finestra di filtro di visualizzazione hello selezionare **libreria**e cercare `Azure Storage` hello toofind i filtri di archiviazione di Azure. Filtro selezionare hello per **404 (non trovato) di messaggi in tutti i log**.
3. Hello visualizzazione **libreria** menu Nuovo, quindi individuare e selezionare hello **filtro temporale globale**.
4. Modificare il timestamp di hello nell'intervallo di hello filtro toohello desiderato tooview. Ciò consentirà di intervallo di hello toonarrow di tooanalyze di dati.
5. Il filtro dovrebbe essere visualizzato simile toohello riportato di seguito viene riportato di seguito. Fare clic su **applica** tooapply hello filtro toohello Analysis griglia.

    ```   
    ((AzureStorageLog.StatusCode == 404 || HTTP.StatusCode == 404)) And
    (#Timestamp >= 2014-10-20T16:36:38 and #Timestamp <= 2014-10-20T16:36:39)
    ```

![Layout di visualizzazione di Archiviazione di Azure](./media/storage-e2e-troubleshooting-classic-portal/404-filtered-errors1.png)

### <a name="analyze-your-log-data"></a>Analizzare i dati di log
Ora che si sono raggruppati e filtrati i dati, è possibile esaminare i dettagli di hello delle singole richieste che hanno generato 404 errori. Nel layout di visualizzazione corrente hello, dati hello vengono raggruppati per ID richiesta client, quindi dall'origine di log. Poiché si Filtra per le richieste in cui hello StatusCode campo 404, verranno esaminati solo i server hello e i dati di traccia di rete, non i dati di log relativi ai client di hello.

immagine Hello seguente mostra una richiesta specifica in cui un'operazione Get Blob ha restituito un errore 404 perché non esisteva blob hello. Si noti che alcune colonne sono state rimosse dalla visualizzazione standard di hello nei dati rilevanti hello toodisplay dell'ordine.

![Log della traccia di rete e del server filtrati](./media/storage-e2e-troubleshooting-classic-portal/server-filtered-404-error.png)

Successivamente, si sarà correlare questo ID richiesta client hello client log dati toosee stava richiedendo quali client hello azioni quando si è verificato l'errore hello. È possibile visualizzare una nuova visualizzazione griglia di analisi per questa sessione tooview hello client log dati, che viene aperto in una seconda scheda:

1. Innanzitutto, copiare il valore di hello di hello **ClientRequestId** Appunti toohello campo. È possibile farlo selezionando una riga, individuazione hello **ClientRequestId** campo, facendo clic sul valore dei dati hello e scegliendo **copia 'ClientRequestId'**.
2. Nella barra multifunzione di hello, selezionare **nuovo visualizzatore**, quindi selezionare **griglia Analysis** tooopen una nuova scheda nuovo hello scheda Visualizza tutti i dati nei file di registro, senza il raggruppamento, filtro o le regole colore.
3. Nella barra multifunzione di hello, selezionare **visualizzazione Layout**, quindi selezionare **tutte le colonne di Client .NET** in hello **di archiviazione di Azure** sezione. Questa visualizzazione Mostra i dati dal log hello del client, nonché hello i registri di traccia di rete e del server. Per impostazione predefinita l'ordinamento in hello **MessageNumber** colonna.
4. Cercare quindi log hello del client richiesta ID client hello. Nella barra multifunzione di hello, selezionare **Trova messaggi**, quindi specificare un filtro personalizzato sull'ID di richiesta client hello in hello **trovare** campo. Usare questa sintassi per il filtro di hello, specificando il proprio ID richiesta client:

    ```  
    *ClientRequestId == "398bac41-7725-484b-8a69-2a9e48fc669a"
    ```

Message Analyzer individua e seleziona hello prima voce di registro in cui i criteri di ricerca hello corrisponde richiesta ID client hello. Nel Registro di hello client, esistono diverse voci per ogni ID richiesta client, pertanto è consigliabile toogroup usarle in hello **ClientRequestId** toomake campo è più facile toosee li tutti insieme. immagine di Hello riportata di seguito mostra tutti i messaggi hello in client hello di log per hello specificato ID di richiesta client.

![Log del client con errori 404](./media/storage-e2e-troubleshooting-classic-portal/client-log-analysis-grid1.png)

Utilizza dati hello visualizzati nel layout della visualizzazione hello in queste due schede, è possibile analizzare hello richiesta dati toodetermine ciò che potrebbe essere causato l'errore hello. È anche possibile esaminare le richieste che hanno preceduto questo uno toosee se un evento precedente hanno potuto condurre errore 404 toohello. Ad esempio, è possibile esaminare le voci di log client hello precedono questa toodetermine di ID richiesta client se blob hello potrebbe essere stata eliminata o se l'errore hello scaduto dall'applicazione client toohello che chiama un'API CreateIfNotExists in un contenitore o blob. Nel Registro di client hello, è possibile trovare l'indirizzo del blob hello in hello **descrizione** campo; nel server di hello e registri di traccia di rete, questa informazione viene visualizzata in hello **riepilogo** campo.

Quando si conosce l'indirizzo di hello del blob hello che hanno restituito errori hello 404, è possibile esaminare ulteriormente. Se si esegue la ricerca voci di log hello per altri messaggi associati con operazioni su hello stesso blob, è possibile verificare se il client hello eliminato in precedenza entità hello.

## <a name="analyze-other-types-of-storage-errors"></a>Analizzare altri tipi di errori di archiviazione
Ora che si ha familiarità con i dati dei log di tooanalyze Message Analyzer, è possibile analizzare gli altri tipi di errori durante l'utilizzo di visualizzazione layout, le regole colore e la ricerca filtro. Hello tabelle seguente sono elencati alcuni problemi che si possono verificarsi e i criteri di filtro è possibile utilizzare toolocate hello li. Per ulteriori informazioni sulla creazione di filtri e hello Message Analyzer filtro lingua, vedere [filtraggio dei dati di messaggio](http://technet.microsoft.com/library/jj819365.aspx).

| tooInvestigate... | Usare l'espressione di filtro... | Espressione si applica tooLog (Client, Server, rete, tutti) |
| --- | --- | --- |
| Ritardi imprevisti nel recapito dei messaggi in una coda |AzureStorageClientDotNetV4.Description   contains "Retrying failed operation." |Client |
| Aumento di PercentThrottlingError HTTP |HTTP.Response.StatusCode   == 500 &#124;&#124; HTTP.Response.StatusCode == 503 |Rete |
| Aumento di PercentTimeoutError |HTTP.Response.StatusCode   == 500 |Rete |
| Aumento di PercentTimeoutError (tutti) |*StatusCode   == 500 |Tutti |
| Aumento di PercentNetworkError |AzureStorageClientDotNetV4.EventLogEntry.Level   < 2 |Client |
| Messaggi HTTP 403 (Accesso negato) |HTTP.Response.StatusCode   == 403 |Rete |
| Messaggi HTTP 404 (Non trovato) |HTTP.Response.StatusCode   == 404 |Rete |
| 404 (tutti) |*StatusCode   == 404 |Tutti |
| Problema di autorizzazione della firma di accesso condiviso |AzureStorageLog.RequestStatus ==  "SASAuthorizationError" |Rete |
| Messaggi HTTP 409 (Conflitto) |HTTP.Response.StatusCode   == 409 |Rete |
| 409 (tutti) |*StatusCode   == 409 |Tutti |
| Un valore PercentSuccess basso o le voci del log di analisi contengono operazioni con stato della transazione ClientOtherErrors |AzureStorageLog.RequestStatus ==   "ClientOtherError" |Server |
| Avviso Nagle |((AzureStorageLog.EndToEndLatencyMS   - AzureStorageLog.ServerLatencyMS) > (AzureStorageLog.ServerLatencyMS *   1.5)) e (AzureStorageLog.RequestPacketSize <1460) e (AzureStorageLog.EndToEndLatencyMS -   AzureStorageLog.ServerLatencyMS >= 200) |Server |
| Intervallo di tempo nei log del server e di rete |#Timestamp   >= 2014-10-20T16:36:38 e #Timestamp <= 2014-10-20T16:36:39 |Server, Rete |
| Intervallo di tempo nei log del server |AzureStorageLog.Timestamp   >= 2014-10-20T16:36:38 e AzureStorageLog.Timestamp <=   2014-10-20T16:36:39 |Server |

## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni sugli scenari end-to-end di risoluzione dei problemi di archiviazione di Azure, vedere le risorse seguenti:

* [Monitoraggio, diagnosi e risoluzione dei problemi del servizio di archiviazione di Microsoft Azure](storage-monitoring-diagnosing-troubleshooting.md)
* [Analisi archiviazione](http://msdn.microsoft.com/library/azure/hh343270.aspx)
* [Monitoraggio di un account di archiviazione nel portale di Azure hello](storage-monitor-storage-account.md)
* [Trasferimento dati con hello utilità della riga di comando AzCopy](storage-use-azcopy.md)
* [Guida operativa di Microsoft Message Analyzer](http://technet.microsoft.com/library/jj649776.aspx)
