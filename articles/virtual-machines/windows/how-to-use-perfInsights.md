---
title: aaaHow toouse PerfInsights in Microsoft Azure | Documenti Microsoft
description: Apprende come problemi di prestazioni toouse PerfInsights tootroubleshoot macchina virtuale di Windows.
services: virtual-machines-windows'
documentationcenter: 
author: genlin
manager: cshepard
editor: na
tags: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: genli
ms.openlocfilehash: f23ff7708c0c63bd02674b1bdc07753e8a89d9be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-perfinsights"></a>Come toouse PerfInsights 

[PerfInsights](http://aka.ms/perfinsightsdownload) è uno script automatico che consente di raccogliere informazioni diagnostiche, esegue i carichi dei / o e fornisce un toohelp di report di analisi di risoluzione dei problemi di prestazioni macchina virtuale Windows in Microsoft Azure. 

È consigliabile aprire questo script prima di aprire un ticket di supporto con Microsoft per problemi di prestazioni delle VM.

## <a name="supported-troubleshooting-scenarios"></a>Scenari per la risoluzione dei problemi supportati

PerfInsights può raccogliere e analizzare diversi tipi di informazioni che vengono raggruppate in scenari univoci.

### <a name="collect-disk-configuration"></a>Raccogliere la configurazione dei dischi 

Questo scenario raccoglie dati di configurazione del disco hello e altre informazioni importanti, inclusi hello seguenti elementi:

-   Log eventi

-   Stato della rete per tutte le connessioni in ingresso e in uscita

-   Impostazioni di configurazione della rete e del firewall

-   Elenco di attività per tutte le applicazioni che sono in esecuzione nel sistema hello

-   File di informazioni creato da msinfo32 per hello la macchina virtuale (VM)

-   Impostazioni di configurazione di database di Microsoft SQL Server (se hello VM viene identificato come un server che esegue SQL Server)

-   Contatori di affidabilità di archiviazione

-   Importanti hotfix di Windows

-   Driver di filtro installati

Si tratta di una raccolta di informazioni che non dovrebbero influire sul sistema hello passiva. 

>[!Note]
>Questo scenario viene inclusa automaticamente in ciascuno dei seguenti scenari hello.

### <a name="benchmarkstorage-performance-test"></a>Test delle prestazioni dell'archiviazione o di benchmark

Questo scenario esegue hello [diskspd](https://github.com/Microsoft/diskspd) benchmark test (IOPS e MBPS) per tutte le unità che sono associate toohello macchina virtuale. 

> [!Note]
> Questo scenario può influire sul sistema hello e non deve essere eseguito su un sistema di produzione in tempo reale. Se necessario, eseguire questo scenario in un tooavoid finestra di manutenzione dedicata dei problemi. Un maggiore carico di lavoro che è causato da un test di benchmark o di traccia potrebbe influire negativamente sulle prestazioni di hello della macchina virtuale.
>

### <a name="general-vm-slow-analysis"></a>Analisi generale della VM lenta 

Questo scenario viene eseguito un [contatore delle prestazioni](https://msdn.microsoft.com/library/windows/desktop/aa373083(v=vs.85).aspx) traccia mediante i contatori specificati nel file Generalcounters.txt hello hello. VM hello viene identificato come un server che esegue SQL Server, esegue una traccia del contatore delle prestazioni tramite contatori hello che si trovano nel file Sqlcounters.txt hello. Include anche i dati di diagnostica delle prestazioni.

### <a name="vm-slow-analysis-and-benchmark"></a>Analisi della VM lenta e benchmark

Questo scenario esegue una traccia dei [contatori delle prestazioni](https://msdn.microsoft.com/library/windows/desktop/aa373083(v=vs.85).aspx) seguita da un test di benchmark [diskspd](https://github.com/Microsoft/diskspd). 

> [!Note]
> Questo scenario può influire sul sistema hello e non deve essere eseguito su un sistema di produzione in tempo reale. Se necessario, eseguire questo scenario in un tooavoid finestra di manutenzione dedicata dei problemi. Un maggiore carico di lavoro che è causato da un test di benchmark o di traccia potrebbe influire negativamente sulle prestazioni di hello della macchina virtuale.
>

### <a name="azure-files-analysis"></a>Analisi di File di Azure 

Questo scenario esegue una speciale acquisizione dei contatori delle prestazioni insieme a una traccia di rete. L'acquisizione include tutti i contatori "Condivisioni SMB Client" hello. di seguito Hello sono alcuni chiave client Condivisione contatori delle prestazioni SMB che fanno parte di acquisizione hello:

| **Tipo**     | **Contatore Condivisioni client SMB** |
|--------------|-------------------------------|
| IOPS         | Richieste dati/sec             |
|              | Richieste di lettura/sec             |
|              | Richieste di scrittura/sec            |
| Latency      | Media secondi/richiesta dati         |
|              | Media secondi/lettura                 |
|              | Media secondi/scrittura                |
| Dimensioni I/O      | Avg. Bytes/Data Request (Media byte/richiesta dati)       |
|              | Media byte/Lettura               |
|              | Media byte/Scrittura              |
| Velocità effettiva   | Byte dati/sec                |
|              | Byte letti/sec                |
|              | Byte scritti/sec               |
| Lunghezza coda | Lunghezza media coda lettura        |
|              | Lunghezza media coda scrittura       |
|              | Lunghezza media coda dati        |

### <a name="custom-configuration"></a>Configurazione personalizzata 

Quando si esegue una configurazione personalizzata, si eseguono tutte le tracce (diagnostica delle prestazioni, contatore delle prestazioni, Xperf, rete, StorPort) in parallelo, a seconda del numero di tracce diverse selezionate. Al termine dell'analisi, lo strumento hello esegue benchmark diskspd hello, se è selezionato. 

> [!Note]
> Questo scenario può influire sul sistema hello e non deve essere eseguito su un sistema di produzione in tempo reale. Se necessario, eseguire questo scenario in un tooavoid finestra di manutenzione dedicata dei problemi. Un maggiore carico di lavoro che è causato da un test di benchmark o di traccia potrebbe influire negativamente sulle prestazioni di hello della macchina virtuale.
>

## <a name="what-kind-of-information-is-collected-by-hello-script"></a>Il tipo di informazioni raccolte da script hello?

Informazioni sulla macchina virtuale di Windows, dischi o archiviazione pool configurazione, vengono raccolti i contatori delle prestazioni, log e le tracce di diversi a seconda dello scenario di prestazioni hello utilizzato:

|Dati raccolti                              |  |  | Scenari delle prestazioni |  |  | |
|----------------------------------|----------------------------|------------------------------------|--------------------------|--------------------------------|----------------------|----------------------|
|                              | Raccogliere la configurazione dei dischi | Test delle prestazioni dell'archiviazione o di benchmark | Analisi generale della VM lenta | Analisi della VM lenta e benchmark | Analisi di File di Azure | Configurazione personalizzata |
| Informazioni dai log eventi      | Sì                        | Sì                                | Sì                      | Sì                            | Sì                  | Sì                  |
| Informazioni di sistema               | Sì                        | Sì                                | Sì                      | Sì                            | Sì                  | Sì                  |
| Mapping del volume                       | Sì                        | Sì                                | Sì                      | Sì                            | Sì                  | Sì                  |
| Mapping del disco                         | Sì                        | Sì                                | Sì                      | Sì                            | Sì                  | Sì                  |
| Attività in esecuzione                    | Sì                        | Sì                                | Sì                      | Sì                            | Sì                  | Sì                  |
| Contatori di affidabilità di archiviazione     | Sì                        | Sì                                | Sì                      | Sì                            | Sì                  | Sì                  |
| Informazioni sull'archiviazione              | Sì                        | Sì                                | Sì                      | Sì                            | Sì                  | Sì                  |
| Output di fsutil                    | Sì                        | Sì                                | Sì                      | Sì                            | Sì                  | Sì                  |
| Informazioni sul driver di filtro               | Sì                        | Sì                                | Sì                      | Sì                            | Sì                  | Sì                  |
| Output di netstat                   | Sì                        | Sì                                | Sì                      | Sì                            | Sì                  | Sì                  |
| Network configuration            | Sì                        | Sì                                | Sì                      | Sì                            | Sì                  | Sì                  |
| Configurazione del firewall           | Sì                        | Sì                                | Sì                      | Sì                            | Sì                  | Sì                  |
| Configurazione di SQL Server         | Sì                        | Sì                                | Sì                      | Sì                            | Sì                  | Sì                  |
| Tracce diagnostiche delle prestazioni * |                            |                                    | Sì                      |                                |                      | Sì                  |
| Traccia dei contatori delle prestazioni **     |                            |                                    |                          |                                |                      | Sì                  |
| Traccia del contatore SMB **             |                            |                                    |                          |                                | Sì                  |                      |
| Traccia del contatore SQL Server **      |                            |                                    |                          |                                |                      | Sì                  |
| Traccia di XPerf                      |                            |                                    |                          |                                |                      | Sì                  |
| Traccia di StorPort                   |                            |                                    |                          |                                |                      | Sì                  |
| Traccia di rete                    |                            |                                    |                          |                                | Sì                  | Sì                  |
| Traccia del benchmark diskspd ***      |                            | Sì                                |                          | Sì                            |                      |                      |
|       |                            |                         |                                                   |                      |                      |

### <a name="performance-diagnostics-trace-"></a>Traccia diagnostica delle prestazioni (*)

Esegue un motore basato su regole in dati toocollect in background hello e diagnosticare i problemi di prestazioni in corso. Hello segue le regole è attualmente supportata:

- Regola HighCpuUsage: rileva i periodi di utilizzo elevati della CPU e Mostra i consumer dell'utilizzo della CPU superiore hello durante tali periodi.
- Regola HighDiskUsage: rileva i periodi di utilizzo del disco nei dischi fisici e Mostra i consumer di utilizzo disco superiore hello durante tali periodi.
- Regola HighResolutionDiskMetric: visualizza le metriche relative a operazioni di I/O al secondo, velocità effettiva e latenza di I/O ogni 50 millisecondi per ogni disco fisico. È utile identificare i periodi di limitazione disco tooquickly.
- Regola HighMemoryUsage: rileva i periodi di utilizzo elevato della memoria e vengono visualizzati i consumer di utilizzo di memoria superiore hello durante tali periodi.

> [!NOTE] 
> Attualmente, sono supportate le versioni di Windows che includono hello .NET Framework 3.5 o versioni successive.

### <a name="performance-counter-trace-"></a>Traccia dei contatori delle prestazioni (**)

Hello raccoglie i contatori delle prestazioni seguenti:

- \Processo, \Processore, \Memoria, \Thread, \Disco fisico, \Disco logico
- \Cache\Pagine dirty, \Cache\Scritture Lazy scaricate su disco/sec, \Server\Errori in pool non di paging, \Server\Errori in pool di paging
- Contatori selezionati in \Interfaccia di rete, \IPv4\Datagrams (Datagrammi), \IPv6\Datagrams (Datagrammi), \TCPv4\Segmenti, \TCPv6\Segmenti, \Scheda di rete, \Piattaforma filtro Windows versione 4\Pacchetti, \Piattaforma filtro Windows versione 6\Pacchetti, \UDPv4\Datagrams (Datagrammi), \UDPv6\Datagrams (Datagrammi), \TCPv4\Connessione, \TCPv6\Connessione, \Criteri QoS di rete\Pacchetti, \Attività scheda di interfaccia di rete per processore, \Microsoft Winsock Base Service Provider

#### <a name="for-sql-server-instances"></a>Per le istanze di SQL Server
- \SQL Server:Buffer Manager, \SQLServer:Resource Pool Stats, \SQLServer:SQL Statistics\
- \SQLServer:Locks, \SQLServer:General Statistics
- \SQLServer:Metodi di accesso

#### <a name="for-azure-files"></a>Per File di Azure
\Condivisioni client SMB

### <a name="diskspd-benchmark-trace-"></a>Traccia del benchmark diskspd (***)
Il carico di lavoro di I/O diskspd testa [disco del sistema operativo (scrittura) e unità di pool (lettura/scrittura)]

## <a name="run-hello-perfinsights-on-your-vm"></a>Eseguire hello PerfInsights nella VM

### <a name="what-do-i-have-tooknow-before-i-run-hello-script"></a>Che cos'è tooknow prima di eseguire script hello? 

**Requisiti dello script**

1.  Questo script deve essere eseguito nella macchina virtuale che si è verificato il problema di prestazioni hello hello. 

2.  Hello sono supportati i seguenti sistemi operativi: Windows Server 2008 R2, 2012, 2012 R2, 2016; Windows 8.1 e Windows 10.

**Possibili problemi quando si esegue script hello in produzione, le macchine virtuali:**

1.  script Hello potrebbe compromettere le prestazioni di hello di hello VM quando viene utilizzata insieme a uno scenario "Benchmark" o "Personalizzato" hello che viene configurato tramite XPerf o DiskSpd. Prestare attenzione quando si esegue uno script hello in un ambiente di produzione.

2.  Quando si utilizzano script hello insieme a uno scenario "Benchmark" o "Personalizzato" hello che viene configurato con DiskSpd, verificare che altre attività in background non interferisce con il carico di lavoro di hello i/o su dischi hello testato.

3.  Per impostazione predefinita, script hello utilizza dati toocollect dell'unità di archiviazione temporanea hello. Se si tracciano rimane abilitati per un periodo più lungo, quantità hello di dati raccolti possono risultare pertinenti. Questo può ridurre la disponibilità di hello di spazio su disco temporaneo hello, pertanto influire sulle applicazioni che si basano su questa unità.

### <a name="how-do-i-run-perfinsights"></a>Come si esegue PerfInsights 

toorun hello script, seguire questi passaggi:

1. Scaricare [PerfInsights.zip](http://aka.ms/perfinsightsdownload).

2. Sbloccare il file PerfInsights.zip hello. toodo questo file di PerfInsights.zip hello pulsante destro del mouse, selezionare **proprietà**. In hello **generale** , selezionare **Unblock** e quindi selezionare **OK**. Questo garantirà che script hello viene eseguito senza alcuna protezione aggiuntiva richiesto.  

    ![Sblocco di file zip hello](media/how-to-use-perfInsights/unlock-file.png)

3.  Espandere hello compresso PerfInsights.zip file nell'unità temporanea (per impostazione predefinita, in genere l'unità D hello). Hello file compresso deve contenere i seguenti hello file e cartelle:

    ![file nella cartella zip hello](media/how-to-use-perfInsights/file-folder.png)

4.  Aprire Windows PowerShell come amministratore e quindi eseguire script PerfInsights.ps1 hello.

    ```
    cd <hello path of PerfInsights folder >
    Powershell.exe -ExecutionPolicy UnRestricted -NoProfile -File .\\PerfInsights.ps1
    ```

    È possibile avere tooenter "y" tooif si tooconfirm che viene chiesto di criteri di esecuzione toochange hello.

    Nella finestra di dialogo esclusione hello è hello opzione tooshare informazioni di diagnostica con il supporto Microsoft. È inoltre necessario consentire toocontinue contratto di licenza toohello. Verificare le selezioni e quindi fare clic su **Esegui script**.

    ![Finestra di dialogo Dichiarazione di non responsabilità](media/how-to-use-perfInsights/disclaimer.png)

5.  Invia il numero di case hello, se disponibile, quando si esegue script hello (questo vale per le statistiche). Fare quindi clic su **OK**.
    
    ![Immettere l'ID di supporto](media/how-to-use-perfInsights/enter-support-number.png)

6.  Selezionare l'unità di archiviazione temporanea. Hello Script può rilevare automaticamente lettera hello dell'unità di hello. Se si verificano problemi in questa fase, potrebbe essere richiesto unità hello tooselect (l'unità predefinita hello è D). I registri generati vengono archiviati in questo caso nel Registro di hello\_cartella insieme. Dopo aver immesso o accettare hello lettera di unità, fare clic su **OK**.

    ![Immettere l'unità](media/how-to-use-perfInsights/enter-drive.png)

7.  Selezionare uno scenario di risoluzione dei problemi hello fornito l'elenco.

       ![Selezionare gli scenari di supporto](media/how-to-use-perfInsights/select-scenarios.png)

8.  È anche possibile eseguire PerfInsights senza l'interfaccia utente.

    esempio Hello comando esecuzioni hello "Slow VM generale analysis" Risoluzione dei problemi di scenario senza un prompt dei comandi dell'interfaccia utente o acquisizione i dati per 30 secondi. Chiede tooconsent toohello stessa dichiarazione di non responsabilità e condizioni di licenza sono indicate nel passaggio 4.

        powershell.exe -ExecutionPolicy UnRestricted -NoProfile -Command ".\\PerfInsights.ps1 -NoGui -Scenario vmslow -TracingDuration 30"

    Se si desidera PerfInsights toorun in modalità invisibile all'utente, utilizzare il **- AcceptDisclaimerAndShareDiagnostics** parametro. Ad esempio, utilizzare hello comando seguente:

        powershell.exe -ExecutionPolicy UnRestricted -NoProfile -Command ".\\PerfInsights.ps1 -NoGui -Scenario vmslow -TracingDuration 30 -AcceptDisclaimerAndShareDiagnostics"

### <a name="how-do-i-troubleshoot-issues-while-running-hello-script"></a>Come risolvere i problemi durante l'esecuzione di script hello?

Se lo script hello termina in modo anomalo, è possibile pulire uno stato incoerente eseguendo script hello assieme hello - commutatore di pulizia, come indicato di seguito:

    powershell.exe -ExecutionPolicy UnRestricted -NoProfile -Command ".\\PerfInsights.ps1 -Cleanup"

Se si verificano problemi durante il rilevamento automatico di unità temporanea hello hello, potrebbe essere richiesto unità hello tooselect (l'unità predefinita hello è D).

![Immettere l'unità](media/how-to-use-perfInsights/enter-drive.png)

script Hello Disinstalla utilità hello e rimuove le cartelle temporanee.

### <a name="troubleshooting-other-script-issues"></a>Risoluzione di altri problemi di script 

Se si verificano problemi durante l'esecuzione di script hello, premere Ctrl + C toointerrupt l'esecuzione dello script hello. oggetti temporanei tooremove, nella sezione hello "Pulizia dopo l'interruzione anomala".

Se si continua l'errore di script tooexperience anche dopo diversi tentativi, si consiglia di eseguire script hello in "modalità debug" utilizzando hello "-Debug" opzione parametro all'avvio.

Dopo l'errore hello si verifica, l'output completo hello di copia della console di PowerShell, hello e inviarlo toohello l'agente di supporto di Microsoft che risponde si toohelp problemi hello.

### <a name="how-do-i-run-hello-script-in-custom-configuration-mode"></a>Come eseguire script hello in modalità di configurazione personalizzata

Selezionando hello **personalizzato** configurazione, è possibile abilitare più tracce in parallelo (utilizzare MAIUSC toomulti-select):

![Selezionare gli scenari](media/how-to-use-perfInsights/select-scenario.png)

Quando si seleziona diagnostica prestazioni hello, traccia del contatore delle prestazioni, XPerf traccia, traccia di rete o scenari di traccia Storport, seguono le istruzioni di hello nelle finestre di dialogo hello e provare un problema di prestazioni lente hello tooreproduce dopo l'avvio di tracce hello.

Hello seguendo la finestra di dialogo consente di avviare una traccia:

![Avviare una traccia](media/how-to-use-perfInsights/start-trace-message.png)

le tracce hello toostop che tooconfirm hello comando in una seconda finestra di dialogo.

![Arrestare una traccia](media/how-to-use-perfInsights/stop-trace-message.png)
![Arrestare una traccia](media/how-to-use-perfInsights/ok-trace-message.png)

Hello quando le tracce o vengono completate le operazioni, viene generato un nuovo file nell'unità d:\\log\_raccolta (o unità temporanea hello) denominata **CollectedData\_AAAA-MM-GG\_hh\_mm \_ss.zip.** È possibile inviare questo agente di supporto toohello file per l'analisi.

## <a name="review-hello-diagnostics-report-created-by-perfinsights"></a>Esaminare il rapporto diagnostica di hello creato da PerfInsights

All'interno di hello **CollectedData\_AAAA-MM-GG\_hh\_mm\_file ss.zip,** generata dal PerfInsights, è possibile trovare un rapporto HTML che descrive in dettaglio conclusioni hello di PerfInsights. tooreview hello report, espandere hello **CollectedData\_AAAA-MM-GG\_hh\_mm\_ss.zip** file e quindi aprire hello **report. HTML PerfInsights**file.

Seleziona hello **conclusioni** scheda.

![Scheda Risultati](media/how-to-use-perfInsights/findingtab.png)

**Note**

-   I messaggi in rosso sono problemi di configurazione noti che possono causare problemi di prestazioni.

-   I messaggi in giallo sono avvisi che rappresentano configurazioni non ottimali che non necessariamente causano problemi di prestazioni.

-   I messaggi in blu sono solo istruzioni informative.

Hello revisione collegamenti HTTP per tutti i messaggi di errore rossa tooget più informazioni dettagliate sui risultati hello e come possono influenzare le prestazioni di hello o procedure consigliate per ottimizzare le prestazioni delle configurazioni.

### <a name="disk-configuration-tab"></a>Scheda Disk Configuration (Configurazione dei dischi)

Hello **Panoramica** sezione visualizza diverse viste di configurazione dell'archiviazione hello, incluse le informazioni da Diskpart e spazi di archiviazione

Hello **Diskmap disponibile** e **VolumeMap** sezioni in una prospettiva doppia logica come i volumi e dischi fisici sono correlati tooeach altri.

In hello PhysicalDisk prospettiva Diskmap (disponibile), la tabella hello Mostra tutti i volumi logici che sono in esecuzione sul disco hello. Nell'esempio seguente di hello, PhysicalDrive2 esegue 2 volumi logici creati in più partizioni (J e H):

![Scheda dati](media/how-to-use-perfInsights/disktab.png)

In prospettiva Volume hello (*VolumeMap*), le tabelle di hello mostrano tutti i dischi fisici hello in ogni volume logico. Si noti che per i dischi RAID/dinamici è possibile eseguire un volume logico in più dischi fisici. Nel seguente esempio hello *c:\\montare* è configurato come un punto di montaggio *SpannedDisk* su dischi fisici \#2 e \#3:

![Scheda Volume](media/how-to-use-perfInsights/volumetab.png)

### <a name="sql-server-tab"></a>Scheda SQL Server

Se la destinazione hello VM ospita tutte le istanze di SQL Server, si noterà una scheda aggiuntiva nel report hello denominato **SQL Server**:

![Scheda per SQL](media/how-to-use-perfInsights/sqltab.png)

In questa sezione contiene "Overview" e le schede aggiuntive sub per ciascuna delle istanze di SQL Server hello ospitate in hello macchina virtuale.

la sezione "Overview" Hello contiene una tabella utile che riepiloga tutte hello fisico (dischi dati e sistema) che sono in esecuzione e che contengono una combinazione di file di dati e i file di log delle transazioni.

Nel seguente esempio, hello *Unitàfisica0* (in esecuzione l'unità C hello) viene visualizzato perché entrambi hello *modeldev* e *modellog* file si trovano nell'unità C hello, e sono di tipo diverso (ad esempio File di dati e Log delle transazioni, rispettivamente):

![Informazioni sui log](media/how-to-use-perfInsights/loginfo.png)

schede specifiche dell'istanza di SQL Server Hello contengono una sezione generale che consente di visualizzare le informazioni di base sull'istanza selezionata di hello e le sezioni aggiuntive per le informazioni avanzate, incluse le impostazioni, le configurazioni e le opzioni utente.

## <a name="references-toohello-external-tools-used"></a>Fa riferimento a toohello strumenti esterni utilizzati

### <a name="diskspd"></a>Diskspd

DISKSPD è un'archiviazione carico generatore e prestazioni test strumento hello Windows e Windows Server e infrastruttura di Server Cloud team di progettazione. Per altre informazioni, vedere [Diskspd](https://github.com/Microsoft/diskspd).

### <a name="xperf"></a>XPerf

Xperf è un tracce toocapture strumento da riga di comando da hello Kit di strumenti di prestazioni di Windows.

Per altre informazioni, vedere [Windows Performance Toolkit – Xperf](https://blogs.msdn.microsoft.com/ntdebugging/2008/04/03/windows-performance-toolkit-xperf/) (Windows Performance Toolkit - Xperf).

## <a name="next-steps"></a>Passaggi successivi

### <a name="upload-diagnostics-logs-and-reports-toomicrosoft-support-for-further-review"></a>Carica log di diagnostica e segnala tooMicrosoft supporto per un'ulteriore analisi

Quando si lavora con hello personale di supporto Microsoft, potrebbe essere richiesto tootransmit hello l'output generato dal processo di risoluzione dei problemi di PerfInsights tooassist hello.

l'agente di supporto Hello creerà un'area di lavoro DTM di e si riceverà un messaggio di posta elettronica che include un collegamento di toohello [portale DTM (https://filetransfer.support.microsoft.com/EFTClient/Account/Login.htm) e un ID utente univoco e una password.

Questo messaggio verrà inviato da **CTS Automated Diagnostics Services** (ctsadiag@microsoft.com).

![Esempio di messaggio hello](media/how-to-use-perfInsights/supportemail.png)

Per una maggiore sicurezza, sarà necessario toochange password su innanzitutto utilizzare.

Dopo l'accesso tooDTM, si noterà un hello tooupload finestra di dialogo **CollectedData\_AAAA-MM-GG\_hh\_mm\_ss.zip** file raccolti con PerfInsights.
