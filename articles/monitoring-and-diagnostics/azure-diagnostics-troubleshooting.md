---
title: Diagnostica Azure aaaTroubleshooting | Documenti Microsoft
description: Risoluzione dei problemi per l'uso di Diagnostica di Azure nelle macchine virtuali di Azure, in Service Fabric o in Servizi cloud.
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: 66469bce-d457-4d1e-b550-a08d2be4d28c
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/12/2017
ms.author: robb
ms.openlocfilehash: daaf9fa4c40982eb9ba04030d7e8ea1ad9fe085b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-troubleshooting"></a>Risoluzione dei problemi di Diagnostica di Azure
Risoluzione dei problemi relativi a informazioni pertinenti toousing diagnostica Azure. Per altre informazioni su Diagnostica di Azure, vedere [Panoramica di Diagnostica di Azure](azure-diagnostics.md).

## <a name="logical-components"></a>Componenti logici
**Avvio di plug-in di diagnostica (DiagnosticsPluginLauncher.exe)**: avvia hello l'estensione diagnostica Azure. Serve come voce hello processo del punto.

**Plug-in di diagnostica (DiagnosticsPlugin.exe)**: processo principale che viene avviata dall'utilità di avvio di hello precedente e configura hello Agente monitoraggio, viene avviato e gestisce la durata. 

**Agente di monitoraggio (MonAgent\*.exe processi)**: questi processi hello bulk di lavoro hello; ad esempio, di monitoraggio, raccolta e il trasferimento dei dati di diagnostica di hello.  

## <a name="logartifact-paths"></a>Percorsi di log ed elementi
Ecco gli elementi e i registri di hello percorsi toosome importanti. Si continuiamo riferimento toothese in tutto il resto di hello del documento hello:
### <a name="cloud-services"></a>Servizi cloud
| Elemento | Path |
| --- | --- |
| **File di configurazione di Diagnostica di Azure** | %SystemDrive%\Packages\Plugins\Microsoft.Azure.Diagnostics.PaaSDiagnostics\<versione>\Config.txt |
| **File di log** | C:\Logs\Plugins\Microsoft.Azure.Diagnostics.PaaSDiagnostics\<versione>\ |
| **Archivio locale dei dati di diagnostica** | C:\Resources\Directory\<CloudServiceDeploymentID>.\<NomeRuolo>.DiagnosticStore\WAD0107\Tables |
| **File di configurazione dell'agente di monitoraggio** | C:\Resources\Directory\<CloudServiceDeploymentID>.\<NomeRuolo>.DiagnosticStore\WAD0107\Configuration\MaConfig.xml |
| **Pacchetto dell'estensione di diagnostica di Azure** | %SystemDrive%\Packages\Plugins\Microsoft.Azure.Diagnostics.PaaSDiagnostics\<versione> |
| **Percorso dell'utilità di raccolta dei log** | %SystemDrive%\Packages\GuestAgent\ |
| **File di log MonAgentHost** | C:\Resources\Directory\<CloudServiceDeploymentID>.\<RoleName>.DiagnosticStore\WAD0107\Configuration\MonAgentHost.<seq_num>.log |

### <a name="virtual-machines"></a>Macchine virtuali
| Elemento | Path |
| --- | --- |
| **File di configurazione di Diagnostica di Azure** | C:\Packages\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<versione>\RuntimeSettings |
| **File di log** | C:\Packages\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<versione>\Logs\ |
| **Archivio locale dei dati di diagnostica** | C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<VersioneDiagnostica>\WAD0107\Tables |
| **File di configurazione dell'agente di monitoraggio** | C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<VersioneDiagnostica>\WAD0107\Configuration\MaConfig.xml |
| **File di stato** | C:\Packages\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<versione>\Status |
| **Pacchetto dell'estensione di diagnostica di Azure** | C:\Packages\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<VersioneDiagnostica>|
| **Percorso dell'utilità di raccolta dei log** | C:\WindowsAzure\Packages |
| **File di log MonAgentHost** | C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<DiagnosticsVersion>\WAD0107\Configuration\MonAgentHost.<seq_num>.log |

## <a name="metric-data-doesnt-show-in-azure-portal"></a>I dati relativi alle metriche non sono visualizzati nel portale di Azure
Diagnostica di Microsoft Azure fornisce una serie di dati relativi alle metriche che possono essere visualizzati nel portale di Azure. Se si verificano problemi con visualizzare questi dati nel portale, account di archiviazione di diagnostica hello controllo -> WADMetrics\* tabella toosee se esistono record metrica corrispondenti hello. In questo caso, hello PartitionKey della tabella hello è hello ID di risorsa di macchina virtuale o un set di scalabilità della macchina virtuale e hello RowKey è il nome della metrica hello, ovvero il nome di contatore delle prestazioni.

Se l'ID di risorsa hello è errata, controllo configurazione di diagnostica -> metriche -> ResourceId toosee se l'ID di risorsa hello sia impostata correttamente.

Se non sono presenti dati di metrica specifica hello, controllo configurazione di diagnostica -> toosee PerformanceCounter metrica hello (contatore prestazioni) è incluso. Si abilita hello seguenti contatori per impostazione predefinita.
- \Processor(_Total)\% Processor Time
- \Memory\Available Bytes
- \ASP.NET Applications(__Total__)\Requests/Sec
- \ASP.NET Applications(__Total__)\Errors Total/Sec
- \ASP.NET\Requests Queued
- \ASP.NET\Requests Rejected
- \Processor(w3wp)\% Processor Time
- \Process(w3wp)\Private Bytes
- \Process(WaIISHost)\% Processor Time
- \Process(WaIISHost)\Private Bytes
- \Process(WaWorkerHost)\% Processor Time
- \Process(WaWorkerHost)\Private Bytes
- \Memory\Page Faults/sec
- \.NET CLR Memory(_Global_)\% Time in GC
- \LogicalDisk(C:)\Disk Write Bytes/sec
- \LogicalDisk(C:)\Disk Read Bytes/sec
- \LogicalDisk(D:)\Disk Write Bytes/sec
- \LogicalDisk(D:)\Disk Read Bytes/sec

Se la configurazione hello sia impostata correttamente ma non è ancora possibile visualizzare i dati di metrica hello, seguire le istruzioni di hello seguito per ulteriori indagini hello.


## <a name="azure-diagnostics-is-not-starting"></a>Mancato avvio di Diagnostica Azure
Esaminare **DiagnosticsPluginLauncher.log** e **DiagnosticsPlugin.log** file dal percorso di hello di hello fornito in precedenza per informazioni sui motivi per cui diagnostica non è stato possibile toostart i file di log. 

Se questi log indicano `Monitoring Agent not reporting success after launch`, significa che si è verificato un errore di avvio di MonAgentHost.exe. Esaminare i registri di hello per che nel percorso di hello indicato per `MonAgentHost log file` hello in precedenza nella sezione.

Hello l'ultima riga del file di log hello contiene codice di uscita hello.  

```
DiagnosticsPluginLauncher.exe Information: 0 : [4/16/2016 6:24:15 AM] DiagnosticPlugin exited with code 0
```
Se si trova un **negativo** codice di uscita, consultare toohello [tabella codici di uscita](#azure-diagnostics-plugin-exit-codes) in hello [riferimenti](#references).

## <a name="diagnostics-data-is-not-logged-tooazure-storage"></a>Dati di diagnostica viene registrato non tooAzure archiviazione
Determinare se i dati non vengono visualizzati o solo alcuni dati hello non vengono visualizzati.

### <a name="diagnostics-infrastructure-logs"></a>Log dell'infrastruttura di diagnostica
La diagnostica di Azure registra gli errori rilevati nei log dell'infrastruttura di diagnostica. Assicurarsi di avere abilitato ([come?](#how-to-check-diagnostics-extension-configuration)) acquisizione dei log di infrastruttura di diagnostica nella configurazione e di cercare rapidamente gli eventuali errori rilevanti che compaiono nella hello `DiagnosticInfrastructureLogsTable` tabella nell'account di archiviazione configurato.

### <a name="no-data-is-showing-up"></a>Non sono visualizzati dati
causa più comune di Hello di dati dell'evento manca completamente è informazioni sull'account di archiviazione definite in modo non corretto.

Soluzione: correggere la configurazione della diagnostica e reinstallare Diagnostica.

Se l'account di archiviazione di hello è configurato correttamente, remote desktop in marca e macchina hello DiagnosticsPlugin.exe e MonAgentCore.exe sono in esecuzione. Se non sono in esecuzione, seguire le istruzioni in [Mancato avvio di Diagnostica di Azure](#azure-diagnostics-is-not-starting). Se l'esecuzione di processi di hello, passare troppo[dati recupero acquisiti localmente](#is-data-getting-captured-locally) e seguire questa Guida da qui.

### <a name="part-of-hello-data-is-missing"></a>Parte di dati hello è mancante
Alcuni dati sono presenti ma una parte dei dati è mancante. Ciò significa che la raccolta dei dati hello / pipeline trasferimento sia impostata correttamente. Seguire le sottosezioni hello Ecco toonarrow verso il basso il problema hello:
#### <a name="is-collection-configured"></a>La raccolta è configurata: 
Configurazione di diagnostica contiene parte hello che indica per un particolare tipo di dati toobe raccolti. [Rivedere la configurazione di](#how-to-check-diagnostics-extension-configuration) toomake non desiderata per i dati è che non è stato configurato per la raccolta.
#### <a name="is-hello-host-generating-data"></a>Host hello genera dati:
- **I contatori delle prestazioni**: aprire perfmon e controllare il contatore hello.
- **I log di traccia**: utilizzare desktop remoto hello macchina virtuale e aggiungere il file di configurazione dell'applicazione di toohello TextWriterTraceListener.  Vedere tooset http://msdn.microsoft.com/library/sk36c28t.aspx listener del testo hello.  Verificare che hello `<trace>` elemento ha `<trace autoflush="true">`.<br />
Se i log di traccia non vengono generati, seguire le istruzioni in [Altre informazioni sui log di traccia mancanti](#more-about-trace-logs-missing).
- **Le tracce ETW**: utilizzare desktop remoto hello macchina virtuale e installare PerfView.  In PerfView eseguire File -> User Command -> Listen etwprovder1,etwprovider2 (File -> Comando utente -> Attesa etwprovder1,etwprovider2) e così via.  Si noti che il comando di ascolto hello è tra maiuscole e minuscole e tra hello elenco delimitato da virgole dei provider ETW non possono essere presenti spazi.  Se il comando hello non riesce toorun, è possibile fare clic su pulsante 'Log' hello in hello in basso a destra di hello Perfview strumento toosee che animale toorun tentativi e il risultato di hello.  Supponendo che sia corretto, che quindi una nuova finestra verrà visualizzata su e in pochi secondi hello input inizieranno visualizzare le tracce ETW.
- **I registri eventi**: hello VM utilizzare desktop remoto. Aprire `Event Viewer` e assicurarsi che sono presenti eventi hello.
#### <a name="is-data-getting-captured-locally"></a>I dati vengono acquisiti in locale:
Assicurarsi quindi hello recupero vengono acquisiti i dati in locale.
dati di Hello vengono archiviati in locale in `*.tsf` file [archivio locale di hello per i dati di diagnostica](#log-artifacts-path). I diversi tipi di log vengono raccolti in file `.tsf` diversi. i nomi di Hello sono nomi di tabella toohello simili nell'archiviazione di azure. Ad esempio, `Performance Counters` viene raccolto in `PerformanceCountersTable.tsf`, i log eventi vengono raccolti in `WindowsEventLogsTable.tsf`. Utilizzare le istruzioni hello [estrazione Log locale](#local-log-extraction) sezione file di raccolta locale tooopen hello e assicurarsi che vengono visualizzate recupero raccolti sul disco.

Se si non vedere i log di recupero raccolti in locale e si dispone già di verificare che l'host hello è la generazione di dati, è probabile che un problema di configurazione. Rivedere la configurazione con attenzione per sezione appropriata hello. Esaminare inoltre configurazione hello generato per MonitoringAgent [MaConfig.xml](#log-artifacts-path) e assicurarsi che sia presente una sezione che descrive l'origine di log rilevanti hello e che non vengono perse nella conversione tra una configurazione di diagnostica di azure e configurazione dell'agente di monitoraggio.
#### <a name="is-data-getting-transferred"></a>I dati vengono trasferiti:
Se si è verificato hello recupero vengono acquisiti i dati in locale, ma non viene comunque visualizzato, nell'account di archiviazione: 
- Prima di tutto, assicurarsi di aver fornito un account di archiviazione corretto e che sono non rollover hello etc.for chiavi account di archiviazione specificato. Per i servizi cloud, a volte gli utenti non aggiornano `useDevelopmentStorage=true`.
- Se l'account di archiviazione specificato è corretto. Assicurarsi che non si dispone delle alcune limitazioni di rete che non consentono componenti hello tooreach gli endpoint di archiviazione pubblico. Un modo toodo che tooremote desktop in hello computer e provare toowrite qualcosa toohello dell'account di archiviazione stesso manualmente.
- Infine, è possibile controllare gli errori segnalati dall'agente di monitoraggio. Agente di monitoraggio scrive il log in `maeventtable.tsf` si trova [archivio locale di hello per i dati di diagnostica](#log-artifacts-path). Seguire le istruzioni [estrazione Log locale](#local-log-extraction) sezione tooopen questo file e provare a scoprire se esistono `errors` che indica i file locali tooread di errori o scrivere toostorage.

### <a name="capturing--archiving-logs"></a>Acquisizione e archiviazione dei log
È parlato hello sopra passaggi, ma potrebbe non stabilire quali errato e sono pensare contattare il supporto tecnico. innanzitutto Hello che potrebbe essere richiesta è toocollect registri dal computer. È possibile risparmiare tempo eseguendo questa operazione autonomamente. Eseguire hello `CollectGuestLogs.exe` utilità in [percorso dell'utilità di raccolta Log](#log-artifacts-path) e genera un file zip con tutti i log di azure rilevanti in hello stessa cartella.

## <a name="diagnostics-data-tables-not-found"></a>Tabelle dei dati di diagnostica non trovate
tabelle di Hello in archiviazione di Azure che contiene gli eventi ETW vengono denominate usando hello seguente codice:

```C#
        if (String.IsNullOrEmpty(eventDestination)) {
            if (e == "DefaultEvents")
                tableName = "WADDefault" + MD5(provider);
            else
                tableName = "WADEvent" + MD5(provider) + eventId;
        }
        else
            tableName = "WAD" + eventDestination;
```

Di seguito è fornito un esempio:

```XML
        <EtwEventSourceProviderConfiguration provider="prov1">
          <Event id="1" />
          <Event id="2" eventDestination="dest1" />
          <DefaultEvents />
        </EtwEventSourceProviderConfiguration>
        <EtwEventSourceProviderConfiguration provider="prov2">
          <DefaultEvents eventDestination="dest2" />
        </EtwEventSourceProviderConfiguration>
```
```JSON
"EtwEventSourceProviderConfiguration": [
    {
        "provider": "prov1",
        "Event": [
            {
                "id": 1
            },
            {
                "id": 2,
                "eventDestination": "dest1"
            }
        ],
        "DefaultEvents": {
            "eventDestination": "DefaultEventDestination",
            "sinks": ""
        }
    },
    {
        "provider": "prov2",
        "DefaultEvents": {
            "eventDestination": "dest2"
        }
    }
]
```
Vengono generate 4 tabelle:

| Evento | Nome tabella |
| --- | --- |
| provider="prov1" &lt;Event id=v1" /&gt; |WADEvent+MD5(“prov1”)+”1” |
| provider="prov1" &lt;Event id="2" eventDestination="dest1" /&gt; |WADdest1 |
| provider="prov1" &lt;DefaultEvents /&gt; |WADDefault+MD5(“prov1”) |
| provider="prov2" &lt;DefaultEvents eventDestination="dest2" /&gt; |WADdest2 |

## <a name="references"></a>Riferimenti

### <a name="how-toocheck-diagnostics-extension-configuration"></a>La configurazione dell'estensione diagnostica toocheck
Hello toocheck modo più semplice la configurazione dell'estensione toonavigate toohttp://resources.azure.com, passare toohello virtuale computer o un servizio cloud in cui l'estensione diagnostica Azure hello (IaaSDiagnostics / PaaDiagnostics) in questione.

In alternativa, desktop remoto in computer hello ed esaminare il file di configurazione di diagnostica Azure hello descritto nella sezione appropriata hello [qui](#log-artifacts-path).

In caso cercare **Microsoft.Azure.Diagnostics** quindi per hello **xmlCfg** o **WadCfg** campo. 

In caso di macchine virtuali, se è presente, hello WadCfg campo significa hello configurazione è in JSON. Se il campo di xmlCfg hello è presente, significa hello configurazione è in formato XML e viene codificato base64. È necessario troppo[decodificarlo](http://www.bing.com/search?q=base64+decoder) toosee hello XML che è stato caricato dalla diagnostica.

Per il ruolo di servizio Cloud, se si seleziona configurazione hello dal disco, i dati di hello codificato in base64 pertanto sarà necessario troppo[decodificarlo](http://www.bing.com/search?q=base64+decoder) toosee hello XML che è stato caricato dalla diagnostica.

### <a name="azure-diagnostics-plugin-exit-codes"></a>Codici di uscita del plug-in Diagnostica di Azure
plug-in Hello restituisce hello seguenti codici di uscita:

| Codice di uscita | Descrizione |
| --- | --- |
| 0 |Completamento della procedura. |
| -1 |Errore generico. |
| -2 |File di rcf hello tooload non è possibile.<p>Questo errore dovrebbe essere eseguita solo se l'utilità di avvio del plug-in agente guest hello viene richiamata manualmente, in modo non corretto, in hello macchina virtuale. |
| -3 |Impossibile caricare il file di configurazione di diagnostica hello.<p><p>Soluzione: questo errore si verifica quando un file di configurazione non ha superato la convalida dello schema. soluzione hello è un file di configurazione che è conforme allo schema di hello tooprovide. |
| -4 |Un'altra istanza di hello monitoraggio diagnostica agente sta già usando directory delle risorse locali hello.<p><p>Soluzione: specificare un valore diverso per **LocalResourceDirectory**. |
| -6 |utilità di avvio del plug-in agente guest Hello tentato diagnostica toolaunch con una riga di comando non valida.<p><p>Questo errore dovrebbe essere eseguita solo se l'utilità di avvio del plug-in agente guest hello viene richiamata manualmente, in modo non corretto, in hello macchina virtuale. |
| -10 |plug-in di diagnostica Hello terminato con un'eccezione non gestita. |
| -11 |l'agente guest Hello è processo hello toocreate Impossibile responsabile per l'avvio e il monitoraggio hello agente di monitoraggio.<p><p>Soluzione: Verificare che le risorse di sistema sufficienti siano disponibili toolaunch nuovi processi.<p> |
| -101 |Argomenti non validi durante la chiamata hello plug-in di diagnostica.<p><p>Questo errore dovrebbe essere eseguita solo se l'utilità di avvio del plug-in agente guest hello viene richiamata manualmente, in modo non corretto, in hello macchina virtuale. |
| -102 |il processo di plug-in di Hello è Impossibile tooinitialize stesso.<p><p>Soluzione: Verificare che le risorse di sistema sufficienti siano disponibili toolaunch nuovi processi. |
| -103 |il processo di plug-in di Hello è Impossibile tooinitialize stesso. In particolare è oggetto di logger non è possibile toocreate hello.<p><p>Soluzione: Verificare che le risorse di sistema sufficienti siano disponibili toolaunch nuovi processi. |
| -104 |File di rcf hello tooload Impossibile fornito dall'agente guest hello.<p><p>Questo errore dovrebbe essere eseguita solo se l'utilità di avvio del plug-in agente guest hello viene richiamata manualmente, in modo non corretto, in hello macchina virtuale. |
| -105 |Impossibile aprire il file di configurazione della diagnostica hello plug-in di diagnostica Hello.<p><p>Questo errore dovrebbe essere eseguita solo se plug-in di diagnostica hello viene richiamata manualmente, in modo non corretto, in hello macchina virtuale. |
| -106 |Impossibile leggere il file di configurazione di diagnostica hello.<p><p>Soluzione: questo errore si verifica quando un file di configurazione non ha superato la convalida dello schema. Soluzione hello è pertanto tooprovide un file di configurazione che è conforme allo schema di hello. Vedere [come configurazione dell'estensione diagnostica toocheck](#how-to-check-diagnostics-extension-configuration). |
| -107 |Hello risorsa directory pass toohello agente di monitoraggio non è valido.<p><p>Questo errore dovrebbe essere eseguita solo se hello agente di monitoraggio viene richiamata manualmente, in modo non corretto, in hello VM.</p> |
| -108 |Non è possibile tooconvert hello file di configurazione nel file di configurazione dell'agente di monitoraggio hello.<p><p>Questo errore dovrebbe essere eseguita solo se il plug-in di diagnostica hello manualmente viene richiamato con un file di configurazione non valida. |
| -110 |Errore di configurazione generale di Diagnostica.<p><p>Questo errore dovrebbe essere eseguita solo se il plug-in di diagnostica hello manualmente viene richiamato con un file di configurazione non valida. |
| -111 |Agente di monitoraggio hello toostart non è possibile.<p><p>Soluzione: verificare che siano disponibili risorse di sistema sufficienti. |
| -112 |Errore generale: |

### <a name="local-log-extraction"></a>Estrazione dei log locali
agente di monitoraggio Hello raccoglie i log e elementi come `.tsf` file. Il file `.tsf` non è leggibile ma è possibile convertirlo in `.csv` come illustrato di seguito: 

```
<Azure diagnostics extension package>\Monitor\x64\table2csv.exe <relevantLogFile>.tsf
```
Un nuovo file denominato `<relevantLogFile>.csv` verrà creato in hello stesso percorso hello corrispondente `.tsf` file.

**Nota**: È sufficiente toorun questa utilità rispetto a file principale tsf hello (ad esempio, PerformanceCountersTable.tsf). Hello che accompagna i file (ad esempio, PerformanceCountersTables_\*\*001.tsf, PerformanceCountersTables_\*\*002. tsf e così via) verranno elaborate automaticamente.

### <a name="more-about-trace-logs-missing"></a>Altre informazioni sui log di traccia mancanti

**Nota:** principalmente toocloud servizi si applica solo a meno che non è stato configurato hello DiagnosticsMonitorTraceListener in un'applicazione in esecuzione nella VM IaaS. 

- Verificare che hello che diagnosticmonitortracelistener sia configurato in App. config o Web. config hello.  Questo è configurato per impostazione predefinita nei progetti del servizio cloud, ma alcuni clienti impostarlo come commento out che provoca il toonot istruzioni di traccia hello essere raccolti da diagnostica. 
- Se non ottenere registri dal metodo OnStart oppure eseguire hello rendere hello che DiagnosticMonitorTraceListener sia in App. config hello.  Per impostazione predefinita è presente nel file Web. config hello, ma che si applica solo toocode in esecuzione all'interno di w3wp.exe; Pertanto, è necessario in App. config toocapture tracce in esecuzione in WaIISHost.exe.
- Assicurarsi di usare Diagnostics.Trace.TraceXXX anziché Diagnostics.Debug.WriteXXX.  salve le istruzioni di Debug verranno rimossa da una build di rilascio.
- Assicurarsi che il codice compilato hello abbia effettivamente righe Trace hello (usare tooverify Reflector, ildasm o ILSpy).  Comandi Trace vengono rimossi dai dati binari hello compilato solo se si utilizza il simbolo di compilazione condizionale di hello TRACE.  Se tramite msbuild toobuild hello project, questo è un toorun problema comune in.

## <a name="known-issues-and-mitigations"></a>Problemi noti e prevenzione
Di seguito è riportato un elenco di problemi noti con le relative misure di prevenzione:

**1. Dipendenza di .NET 4.5:**

WAD presenta una dipendenza di runtime nel framework .NET 4.5 o versioni successive. In fase di hello di scrittura, tutti i computer il provisioning per i servizi cloud, nonché tutti ufficiale azure base immagini di macchina virtuale dispone di .NET 4.5 o successiva. È tuttavia ancora possibile tooland in una situazione in cui si tenta di toorun WAD in un computer che non dispone di .NET 4.5 o versioni successive. Ciò si verifica quando si crea il computer a partire da un'immagine o uno snapshot precedente o si usa un disco personalizzato.

Questa situazione si manifesta in genere come codice di uscita **255** durante l'esecuzione di DiagnosticsPluginLauncher.exe. Errore si verifica a causa di eccezione non gestita toohello: 
```
System.IO.FileLoadException: Could not load file or assembly 'System.Threading.Tasks, Version=1.5.11.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a' or one of its dependencies
```

**Prevenzione:** installare .NET 4.5 o versione successiva nel computer.

**2. I dati dei contatori delle prestazioni sono disponibili nell'archiviazione ma non vengono visualizzati nel portale**

Il portale delle macchine virtuali visualizza determinati contatori delle prestazioni per impostazione predefinita. Se non vengono visualizzati e si conosce il recupero di generazione dei dati hello perché è disponibile nel servizio di archiviazione. Controllare:
- Se dati hello nel servizio di archiviazione sono i nomi dei contatori in inglese. Se i nomi dei contatori di hello non sono in inglese, portale grafico metrica non saranno in grado di toorecognize è.
- Se si usano i caratteri jolly (\*) nei nomi di contatore delle prestazioni, portale hello non saranno in grado di toocorrelate hello configurato e raccolti contatore.

**Attenuazione**: modificare tooEnglish lingua del computer hello per gli account di sistema. Pannello di controllo -> area -> Amministrazione -> Copia impostazioni -> deselezionare "Iniziale e account di sistema" in modo che non lingua personalizzata hello applicato toosystem account. Verificare inoltre che se si desidera toobe portale l'esperienza di utilizzo primario non utilizzare caratteri jolly.
