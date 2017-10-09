---
title: soluzione di dati nel Log Analitica aaaWire | Documenti Microsoft
description: I dati in transito sono dati consolidati di rete e sulle prestazioni provenienti da computer con agenti OMS, inclusi Operations Manager e gli agenti connessi a Windows. Dati di rete vengono combinati con toohelp di dati del log correlare i dati.
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: fc3d7127-0baa-4772-858a-5ba995d1519b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: banders
ms.openlocfilehash: adafdf98dfbda9d87759643a1a606a84eafd1348
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="wire-data-20-preview-solution-in-log-analytics"></a>Soluzione Wire Data 2.0 (anteprima) in Log Analytics

![Simbolo di Wire Data](./media/log-analytics-wire-data/wire-data2-symbol.png)

I dati in transito sono dati di rete e sulle prestazioni consolidati provenienti da computer con agenti OMS, tra cui agenti Operations Manager, connessi a Windows e Linux. Dati di rete vengono combinati con altri toohelp di dati del log correlare i dati.

Gli agenti tooOMS, hello soluzione Wire Data Usa inoltre agenti Dependency Microsoft installato nei computer dell'infrastruttura IT. Tooand dipendenza agenti monitoraggio rete dati inviati dai computer per la rete livelli 2 e 3 in hello [modello OSI](https://en.wikipedia.org/wiki/OSI_model), tra cui hello diversi protocolli e porte usati. I dati vengono quindi inviati tooLog Analitica tramite agenti.

> [!NOTE]
> È possibile aggiungere una versione precedente di hello di aree di lavoro toonew soluzione i dati in transito hello. Se si dispone di soluzione Wire Data originale hello abilitato, è possibile continuare toouse è. Tuttavia, toouse Wire Data 2.0, è necessario innanzitutto rimuovere la versione originale di hello.

Per impostazione predefinita, Log Analytics raccoglie i dati registrati sulle prestazioni di CPU, memoria, dischi e rete dai contatori integrati in Windows. Raccolta di rete e altri dati viene eseguita tempo reale per ogni agente, inclusi subnet e protocolli a livello di applicazione usati dal computer hello. È possibile aggiungere altri contatori delle prestazioni nella pagina Impostazioni hello nella scheda Logs hello.

Se è stato usato [sFlow](http://www.sflow.org/) o altro software con [protocollo NetFlow di Cisco](http://www.cisco.com/c/en/us/products/collateral/ios-nx-os-software/ios-netflow/prod_white_paper0900aecd80406232.html), quindi hello statistiche e i dati visualizzati dai dati in transito saranno tooyou familiarità.

Alcuni dei tipi di hello di query di ricerca Log predefinite includono:

- Agenti che forniscono dati in transito
- Indirizzo IP degli agenti che forniscono dati in transito
- Comunicazioni in uscita da parte degli indirizzi IP
- Numero di byte inviati dai protocolli applicativi
- Numero di byte inviati da un servizio dell’applicazione
- Byte ricevuti da protocolli diversi
- Byte totali inviati e ricevuti per versione IP
- Latenza media per le connessioni misurate in modo affidabile
- Processi dei computer che hanno avviato o ricevuto traffico di rete
- Quantità di traffico di rete per un processo

Quando esegue la ricerca utilizzando i dati in transito, è possibile filtrare e gruppo dati tooview informazioni hello agenti principali e sui protocolli principali. In alternativa, è possibile visualizzare quando determinati computer (indirizzi IP/indirizzi MAC) hanno comunicato tra loro, per quanto tempo e quanti dati sono stati inviati, visualizzando essenzialmente metadati relativi al traffico di rete basati sulla ricerca.

La visualizzazione di metadati, tuttavia, non è necessariamente utile per una risoluzione dei problemi approfondita. I dati in transito in Log Analytics non sono un'acquisizione completa dei dati di rete e non sono quindi destinati a una risoluzione dei problemi approfondita a livello di pacchetto. Hello vantaggio dell'utilizzo dell'agente di hello, confrontare i metodi di raccolta tooother, che non siano tooinstall Appliance, riconfigurare i commutatori di rete o eseguire complesse configurazioni. Dati in transito si basano semplicemente sull'agente-installazione agente hello in un computer e monitorerà il proprio traffico di rete. Un altro vantaggio è quando si desidera che i carichi di lavoro toomonitor in esecuzione nei provider di cloud o provider di servizi o Microsoft Azure, dove utente hello non proprietario hello livello infrastruttura.

## <a name="connected-sources"></a>Origini connesse

I dati in transito Ottiene i dati da Microsoft Dependency Agent hello. Hello Dependency Agent dipende da hello agente OMS per il relativo tooLog connessioni Analitica. Ciò significa che un server deve essere hello agente OMS è installato e configurato prima, e quindi si installa hello Dependency Agent. Hello nella tabella seguente vengono descritte hello connesso origini che supporta la soluzione Wire Data hello.

| **Origine connessa** | **Supportato** | **Descrizione** |
| --- | --- | --- |
| Agenti di Windows | Sì | Wire Data analizza e raccoglie i dati da computer agente Windows. <br><br> In aggiunta toohello [agente OMS](log-analytics-windows-agents.md), gli agenti di Windows richiedono hello Microsoft Dependency Agent. Vedere hello [i sistemi operativi supportati](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems) per un elenco completo delle versioni del sistema operativo. |
| Agenti Linux | Sì | Wire Data analizza e raccoglie i dati da computer agente Linux.<br><br> In aggiunta toohello [agente OMS](log-analytics-linux-agents.md), gli agenti Linux richiedono hello Microsoft Dependency Agent. Vedere hello [i sistemi operativi supportati](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems) per un elenco completo delle versioni del sistema operativo. |
| Gruppo di gestione di System Center Operations Manager | Sì | Wire Data analizza e raccoglie i dati dagli agenti Windows e Linux in un [gruppo di gestione di System Center Operations Manager](log-analytics-om-agents.md) connesso. <br><br> È necessaria una connessione diretta da hello System Center Operations Manager agent computer tooLog Analitica. Dati viene inoltrati da hello gestione gruppo tooLog Analitica. |
| Account di archiviazione di Azure | No | I dati in transito raccoglie i dati dai computer agente, pertanto non sono presenti dati da esso toocollect da archiviazione di Azure. |

In Windows hello Microsoft Monitoring Agent (MMA) viene utilizzato da System Center Operations Manager sia Analitica Log toogather e inviare i dati. A seconda del contesto di hello, agente hello viene chiamato hello agente System Center Operations Manager, agente OMS, agente di Log Analitica, MMA o agente diretto. System Center Operations Manager e Log Analitica forniscono leggermente diverse versioni di hello MMA. Queste versioni ogni possono segnalare tooSystem Center Operations Manager, tooLog Analitica o tooboth.

In Linux, hello agente OMS per Linux raccoglie e invia dati tooLog Analitica. È possibile utilizzare i dati in transito in server con agenti direttamente a OMS o in server che sono collegati tooLog Analitica tramite gruppi di gestione di System Center Operations Manager.

In questo articolo fa riferimento a tooall agenti, se Linux o Windows, se connessi tooa gruppo di gestione di System Center Operations Manager o direttamente tooLog Analitica sono denominati hello _agente OMS_. Nome di distribuzione specifico hello dell'agente di hello verrà utilizzata solo se è necessario per il contesto.

Hello Dependency Agent non trasmette i dati se stesso e non richiede alcun toofirewalls modifiche o le porte. dati Hello in dati in transito sono sempre trasmessi dal hello OMS agent tooLog Analitica, sia direttamente o tramite hello OMS Gateway.

![Diagramma degli agenti](./media/log-analytics-wire-data/agents.png)

Se non è un utente di System Center Operations Manager con un tooLog gruppo connesso gestione Analitica:

- Quando gli agenti di System Center Operations Manager è possono accedere hello Internet tooconnect tooLog Analitica, è richiesta alcuna configurazione aggiuntive.
- Quando gli agenti di System Center Operations Manager non è possibile accedere Log Analitica su hello Internet, è necessario tooconfigure hello OMS Gateway toowork con System Center Operations Manager.

Se si utilizza hello agente diretto, è necessario tooconfigure hello OMS agente tooconnect tooLog Analitica o tooyour OMS Gateway. È possibile scaricare hello OMS Gateway da hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=52666).

## <a name="prerequisites"></a>Prerequisiti

- Richiede hello [Insight & Analitica](https://www.microsoft.com/cloud-platform/operations-management-suite-pricing) offerta di soluzione.
- Se si utilizza hello versione precedente di hello soluzione Wire Data, è necessario innanzitutto rimuoverlo. Tuttavia, tutti i dati acquisiti tramite soluzione Wire Data originale hello è ancora disponibile in transito dati 2.0 e ricerca nei log.
- Privilegi di amministratore sono necessari tooinstall o disinstallare hello Dependency Agent.
- Hello Dependency Agent deve essere installato in un computer con sistema operativo a 64 bit.

### <a name="operating-systems"></a>Sistemi operativi

Hello nelle sezioni seguenti vengono elencano i sistemi operativi supportato hello per hello Dependency Agent. Wire Data non supporta architetture a 32 bit per i sistemi operativi.

#### <a name="windows-server"></a>Windows Server

- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2 SP1,

#### <a name="windows-desktop"></a>Desktop di Windows

- Windows 10
- Windows 8.1
- Windows 8
- Windows 7

#### <a name="red-hat-enterprise-linux-centos-linux-and-oracle-linux-with-rhel-kernel"></a>Red Hat Enterprise Linux, CentOS Linux e Oracle Linux (con il kernel RHEL)

- Sono supportate solo versioni predefinita e SMP del kernel Linux.
- Le versioni del kernel non standard, ad esempio PAE e Xen, non sono supportate per le distribuzioni Linux. Ad esempio, un sistema con stringa di versione di hello di _2.6.16.21-0.8-xen_ non è supportata.
- I kernel personalizzati, tra cui le ricompilazioni dei kernel standard, non sono supportati.
- Il kernel CentOSPlus non è supportato.
- Unbreakable Enterprise Kernel (UEK) di Oracle è illustrato in una sezione successiva di questo articolo.

#### <a name="red-hat-linux-7"></a>Red Hat Linux 7

| **Versione del sistema operativo** | **Versione del kernel** |
| --- | --- |
| 7.0 | 3.10.0-123 |
| 7.1 | 3.10.0-229 |
| 7,2 | 3.10.0-327 |
| 7.3 | 3.10.0-514 |

#### <a name="red-hat-linux-6"></a>Red Hat Linux 6

| **Versione del sistema operativo** | **Versione del kernel** |
| --- | --- |
| 6.0 | 2.6.32-71 |
| 6.1 | 2.6.32-131 |
| 6.2 | 2.6.32-220 |
| 6.3 | 2.6.32-279 |
| 6.4 | 2.6.32-358 |
| 6,5 | 2.6.32-431 |
| 6.6 | 2.6.32-504 |
| 6.7 | 2.6.32-573 |
| 6.8 | 2.6.32-642 |

#### <a name="red-hat-linux-5"></a>Red Hat Linux 5

| **Versione del sistema operativo** | **Versione del kernel** |
| --- | --- |
| 5.8 | 2.6.18-308 |
| 5.9 | 2.6.18-348 |
| 5.10 | 2.6.18-371 |
| 5.11 | 2.6.18-398 <br> 2.6.18-400 <br>2.6.18-402 <br>2.6.18-404 <br>2.6.18-406 <br> 2.6.18-407 <br> 2.6.18-408 <br> 2.6.18-409 <br> 2.6.18-410 <br> 2.6.18-411 <br> 2.6.18-412 <br> 2.6.18-416 <br> 2.6.18-417 <br> 2.6.18-419 |

#### <a name="oracle-enterprise-linux-with-unbreakable-enterprise-kernel"></a>Oracle Enterprise Linux con Unbreakable Enterprise Kernel

#### <a name="oracle-linux-6"></a>Oracle Linux 6

| **Versione del sistema operativo** | **Versione del kernel** |
| --- | --- |
| 6.2 | Oracle 2.6.32-300 (UEK R1) |
| 6.3 | Oracle 2.6.39-200 (UEK R2) |
| 6.4 | Oracle 2.6.39-400 (UEK R2) |
| 6,5 | Oracle 2.6.39-400 (UEK R2 i386) |
| 6.6 | Oracle 2.6.39-400 (UEK R2 i386) |

#### <a name="oracle-linux-5"></a>Oracle Linux 5

| **Versione del sistema operativo** | **Versione del kernel** |
| --- | --- |
| 5.8 | Oracle 2.6.32-300 (UEK R1) |
| 5.9 | Oracle 2.6.39-300 (UEK R2) |
| 5.10 | Oracle 2.6.39-400 (UEK R2) |
| 5.11 | Oracle 2.6.39-400 (UEK R2) |

#### <a name="suse-linux-enterprise-server"></a>SUSE Linux Enterprise Server

#### <a name="suse-linux-11"></a>SUSE Linux 11

| **Versione del sistema operativo** | **Versione del kernel** |
| --- | --- |
| 11 | 2.6.27 |
| 11 SP1 | 2.6.32 |
| 11 SP2 | 3.0.13 |
| 11 SP3 | 3.0.76 |
| 11 SP4 | 3.0.101 |

#### <a name="suse-linux-10"></a>SUSE Linux 10

| **Versione del sistema operativo** | **Versione del kernel** |
| --- | --- |
| 10 SP4 | 2.6.16.60 |

#### <a name="dependency-agent-downloads"></a>Download di Dependency Agent

| **File** | **Sistema operativo** | **Versione** | **SHA-256** |
| --- | --- | --- | --- |
| [InstallDependencyAgent-Windows.exe](https://aka.ms/dependencyagentwindows) | Windows | 9.0.5 | 73B3F6A2A76A08D58F72A550947FF839B588591C48E6EDDD6DDF73AA3FD82B43 |
| [InstallDependencyAgent-Linux64.bin](https://aka.ms/dependencyagentlinux) | Linux | 9.0.5 | A1BAD0B36EBF79F2B69113A07FCF48C68D90BD169C722689F9C83C69FC032371 |



## <a name="configuration"></a>Configurazione

Eseguire hello seguente soluzione Wire Data di passaggi tooconfigure hello per le aree di lavoro.

1. Abilitare soluzioni Analitica Log attività hello hello [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.WireData2OMS?tab=Overview) o tramite il processo di hello descritto in [soluzioni aggiungere Log Analitica da hello Solutions Gallery](log-analytics-add-solutions.md).
2. Installare hello Dependency Agent in ogni computer in cui si desidera tooget dati. Hello Dependency Agent consente di monitorare router adiacenti tooimmediate connessioni, pertanto potrebbe non essere necessario un agente in ogni computer.

### <a name="install-hello-dependency-agent-on-windows"></a>Installare hello Dependency Agent in Windows

Privilegi di amministratore sono necessari tooinstall o disinstallare l'agente di hello.

Hello Dependency Agent viene installato nei computer che eseguono Windows tramite InstallDependencyAgent Windows.exe. Se si esegue il file eseguibile senza opzioni, viene avviata una procedura guidata è possibile seguire tooinstall in modo interattivo.

Utilizzare i seguenti passaggi tooinstall hello Dependency Agent in ogni computer che eseguono Windows hello:

1. Installazione hello agente OMS tramite istruzioni hello in [toohello computer Windows di connettersi servizio Analitica di Log in Azure](log-analytics-windows-agents.md).
2. Scaricare l'agente di Windows hello utilizzando hello collegamento nella sezione precedente di hello e quindi eseguirlo usando hello comando seguente: InstallDependencyAgent Windows.exe
3. Eseguire l'agente hello guidata tooinstall hello.
4. Se hello Dependency Agent non riesce toostart, controllare i registri di hello per informazioni dettagliate sull'errore. Per gli agenti di Windows, directory di log hello è %Programfiles%\Microsoft agent\logs. dipendenza.

#### <a name="windows-command-line"></a>Riga di comando di Windows

Utilizzare le opzioni da hello seguente tabella tooinstall dalla riga di comando. un elenco dei flag di installazione hello, eseguire l'installazione hello utilizzando hello toosee /? come segue.

InstallDependencyAgent-Windows.exe /?

| **Flag** | **Descrizione** |
| --- | --- |
| <code>/?</code> | Ottenere un elenco di opzioni della riga di comando hello. |
| <code>/S</code> | Eseguire un'installazione invisibile all'utente senza prompt per l'utente. |

Per impostazione predefinita, i file per agente dipendenza Windows hello vengono inseriti in c:\Programmi\Microsoft dipendenza Agent.

### <a name="install-hello-dependency-agent-on-linux"></a>Installare hello Dependency Agent in Linux

Accesso alla directory radice è necessario tooinstall o configurare l'agente di hello.

Hello Dependency Agent viene installato nei computer Linux tramite Linux64.bin InstallDependencyAgent, uno script della shell con un file autoestraente binario. È possibile eseguire il file hello utilizzando _sh_ o aggiungere eseguire autorizzazioni toohello file stesso.

Utilizzare hello seguendo i passaggi tooinstall hello Dependency Agent in ogni computer Linux:

1. Installazione hello agente OMS tramite istruzioni hello in [raccogliere e gestire i dati da computer Linux](log-analytics-agent-linux.md).
2. Scaricare l'agente Linux dipendenza hello utilizzando hello collegamento nella sezione precedente di hello e quindi installato come radice utilizzando hello comando seguente: sh InstallDependencyAgent Linux64.bin
3. Se hello Dependency Agent non riesce toostart, controllare i registri di hello per informazioni dettagliate sull'errore. Per gli agenti Linux, directory del registro hello è: /var/opt/microsoft/dependency-agent/log.

un elenco dei flag di installazione di hello, eseguire il programma di installazione di hello con hello toosee `-help` flag come indicato di seguito.

```
InstallDependencyAgent-Linux64.bin -help
```

| **Flag** | **Descrizione** |
| --- | --- |
| <code>-help</code> | Ottenere un elenco di opzioni della riga di comando hello. |
| <code>-s</code> | Eseguire un'installazione invisibile all'utente senza prompt per l'utente. |
| <code>--check</code> | Controllare le autorizzazioni e il sistema operativo hello ma non si installa l'agente di hello. |

File per hello Dependency Agent vengono posizionati in hello seguente directory:

| **File** | **Posizione** |
| --- | --- |
| File core | /opt/microsoft/dependency-agent |
| File di log | /var/opt/microsoft/dependency-agent/log |
| File di configurazione | /etc/opt/microsoft/dependency-agent/config |
| File eseguibili del servizio | /opt/microsoft/dependency-agent/bin/microsoft-dependency-agent<br><br>/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent-manager |
| File binary di archiviazione | /var/opt/microsoft/dependency-agent/storage |

### <a name="installation-script-examples"></a>Esempi di script di installazione

tooeasily distribuire hello Dependency Agent su più server contemporaneamente, ma consente toouse uno script. È possibile utilizzare hello seguente toodownload esempi di script e installare hello Dependency Agent in Windows o Linux.

#### <a name="powershell-script-for-windows"></a>Script di PowerShell per Windows

```PowerShell

Invoke-WebRequest &quot;https://aka.ms/dependencyagentwindows&quot; -OutFile InstallDependencyAgent-Windows.exe

.\InstallDependencyAgent-Windows.exe /S

```

#### <a name="shell-script-for-linux"></a>Script della shell per Linux

```
wget --content-disposition https://aka.ms/dependencyagentlinux -O InstallDependencyAgent-Linux64.bin
```

```
sh InstallDependencyAgent-Linux64.bin -s
```

### <a name="desired-state-configuration"></a>Configurazione dello stato desiderato

hello toodeploy Dependency Agent tramite configurazione dello stato desiderato, è possibile utilizzare modulo xPSDesiredStateConfiguration hello e un po' di codice hello seguente:

```
Import-DscResource -ModuleName xPSDesiredStateConfiguration

$DAPackageLocalPath = &quot;C:\InstallDependencyAgent-Windows.exe&quot;



Node $NodeName

{

    # Download and install hello Dependency Agent

    xRemoteFile DAPackage

    {

        Uri = &quot;https://aka.ms/dependencyagentwindows&quot;

        DestinationPath = $DAPackageLocalPath

        DependsOn = &quot;[Package]OI&quot;

    }

    xPackage DA

    {

        Ensure=&quot;Present&quot;

        Name = &quot;Dependency Agent&quot;

        Path = $DAPackageLocalPath

        Arguments = '/S'

        ProductId = &quot;&quot;

        InstalledCheckRegKey = &quot;HKEY\_LOCAL\_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\DependencyAgent&quot;

        InstalledCheckRegValueName = &quot;DisplayName&quot;

        InstalledCheckRegValueData = &quot;Dependency Agent&quot;

    }

}

```
### <a name="uninstall-hello-dependency-agent"></a>Disinstallare hello Dependency Agent

Utilizzare hello seguenti sezioni toohelp rimuovere hello Dependency Agent.

#### <a name="uninstall-hello-dependency-agent-on-windows"></a>Disinstallare hello Dependency Agent in Windows

Un amministratore può disinstallare agente dipendenza hello per Windows tramite il pannello di controllo.

Un amministratore può anche eseguire %Programfiles%\Microsoft dipendenza Agent\Uninstall.exe toouninstall hello Dependency Agent.

#### <a name="uninstall-hello-dependency-agent-on-linux"></a>Disinstallare hello Dependency Agent in Linux

Disinstalla toocompletely hello Dependency Agent da Linux, è necessario rimuovere l'agente di hello stesso e hello connettore, che viene installato automaticamente con l'agente di hello. È possibile disinstallare entrambi utilizzando hello singolo comando seguente:

```
rpm -e dependency-agent dependency-agent-connector
```

## <a name="management-packs"></a>Management Pack

Quando i dati in transito viene attivato in un'area di lavoro Log Analitica, un 300 KB management pack vengono inviati i server di Windows hello tooall nell'area di lavoro. Se si usano agenti di System Center Operations Manager in un [gruppo di gestione connesso](log-analytics-om-agents.md), hello management pack di monitoraggio delle dipendenze viene distribuito da System Center Operations Manager. Se gli agenti di hello siano connessi direttamente, Log Analitica recapita management pack di hello.

management pack di Hello è denominato Microsoft.IntelligencePacks.ApplicationDependencyMonitor. e viene inserito in %Programfiles%\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs\. origine dati Hello hello management pack utilizza è: % Program files%\Microsoft Monitoring Agent\Agent\Health Service State\Resources&lt;AutoGeneratedID&gt;\ Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll.

## <a name="using-hello-solution"></a>Utilizzo di soluzione hello

**Installazione e configurazione di soluzione hello**

Utilizzare hello tooinstall le informazioni seguenti e configurare la soluzione hello.

- Hello soluzione Wire Data acquisisce i dati dai computer che eseguono Windows Server 2012 R2, Windows 8.1 e sistemi operativi successivi.
- Nei computer in cui si desidera tooacquire i dati in transito da, è necessario Microsoft .NET Framework 4.0 o versione successiva.
- Aggiungere hello i dati in transito soluzione tooyour Log Analitica area di lavoro hello processo descritto in [soluzioni aggiungere Log Analitica da hello Solutions Gallery](log-analytics-add-solutions.md). Non è richiesta alcuna ulteriore configurazione.
- Se si desiderano tooview i dati in transito per una soluzione specifica, è necessario soluzione hello toohave già aggiunto tooyour dell'area di lavoro.

Dopo che gli agenti installati e installare la soluzione hello, riquadro hello Wire Data 2.0 viene visualizzata nell'area di lavoro.

> [!NOTE]
> Attualmente, è necessario utilizzare i dati in transito tooview portale OMS hello. Non è possibile utilizzare i dati in transito hello tooview portale Azure.

![Riquadro Wire Data](./media/log-analytics-wire-data/wire-data-tile.png)

## <a name="using-hello-wire-data-20-solution"></a>Con la soluzione Wire Data 2.0 hello

Nel portale OMS hello, fare clic su hello **Wire Data 2.0** riquadro tooopen hello i dati in transito dashboard. dashboard Hello include pannelli hello in hello nella tabella seguente. Ogni pannello elenca backup too10 elementi corrispondenti ai criteri del pannello per hello specificato intervallo di ambito e tempo. È possibile eseguire una ricerca di log che restituisce tutti i record facendo **tutti** nella parte inferiore di hello del pannello hello oppure facendo clic sull'intestazione di blade hello.

| **Pannello** | **Descrizione** |
| --- | --- |
| Agenti che acquisiscono il traffico di rete | Mostra il numero di hello di agenti che acquisisce il traffico di rete ed elenca hello primi 10 computer che sono di acquisizione del traffico. Fare clic su una ricerca di log per hello numero toorun <code>Type:WireData &#124; measure Sum(TotalBytes) by Computer &#124; top 500000</code>. Fare clic su un computer in hello elenco toorun restituzione hello totale dei byte acquisita una ricerca di log. |
| Subnet locali | Mostra il numero di hello di subnet locali che gli agenti sono individuati.  Fare clic su una ricerca di log per hello numero toorun <code>Type:WireData &#124; Measure Sum(TotalBytes) by LocalSubnet</code> che elenca tutte le subnet con numero di hello di byte inviati in ciascuna di esse. Fare clic su una subnet in hello elenco toorun restituzione hello il numero totale di byte inviati in subnet hello una ricerca di log. |
| Protocolli a livello dell'applicazione | Mostra il numero di hello di protocolli a livello di applicazione in uso, come individuata dagli agenti. Fare clic su una ricerca di log per hello numero toorun <code>Type:WireData &#124; Measure Sum(TotalBytes) by ApplicationProtocol</code>. Fare clic su un protocollo toorun restituzione hello il numero totale di byte inviati tramite il protocollo hello una ricerca di log. |

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Dashboard di Wire Data](./media/log-analytics-wire-data/wire-data-dash.png)

È possibile utilizzare hello **agenti che acquisiscono il traffico di rete** toodetermine pannello quanta larghezza di banda di rete utilizzata dai computer. Questo pannello consentono facilmente hello trova _chattiest_ computer nell'ambiente in uso. Tali computer potrebbero essere sovraccaricati, presentare un funzionamento anomalo o usare una quantità di risorse di rete superiore alla norma.

![Esempio di ricerca log](./media/log-analytics-wire-data/log-search-example01.png)

Analogamente, è possibile utilizzare hello **subnet locali** toodetermine pannello quanto il traffico di rete si sposta le subnet. Gli utenti spesso definiscono le subnet per aree critiche per le applicazioni. Questo pannello offre un quadro di tali aree.

![Esempio di ricerca log](./media/log-analytics-wire-data/log-search-example02.png)

Hello **protocolli a livello di applicazione** pannello è utile perché è utile sapere quali protocolli sono in uso. Ad esempio, si potrebbe pensare che SSH toonot essere in uso nell'ambiente di rete. Visualizzazione delle informazioni disponibili nel pannello hello rapidamente confermare o disprove la previsione.

![Esempio di ricerca log](./media/log-analytics-wire-data/log-search-example03.png)

In questo esempio, è possibile analizzare i SSH dettagli toosee i computer che utilizzano SSH e molti altri dettagli di comunicazione.

![Risultati della ricerca su SSH](./media/log-analytics-wire-data/ssh-details.png)

È inoltre utile tooknow se il traffico di protocollo è aumentando o riducendo il tempo. Se, ad esempio, quantità hello di dati trasmessi da un'applicazione sta aumentando, che potrebbero essere un elemento di che è necessario essere consapevoli oppure che potrebbero trovare degno di nota.

## <a name="input-data"></a>Dati di input

Raccoglie i dati in transito metadati sul traffico di rete usano agenti hello che è stata abilitata. Ogni agente invia dati ogni 15 secondi circa.

## <a name="output-data"></a>Dati di output

Per ogni tipo di dati di input vene creato un record con tipo _WireData_. Record di WireData hanno le proprietà visualizzate in hello nella tabella seguente:

| Proprietà | Descrizione |
|---|---|
| Computer | Nome del computer in cui sono stati raccolti i dati |
| TimeGenerated | Ora del record di hello |
| LocalIP | Indirizzo IP del computer locale hello |
| SessionState | Sessione connessa o disconnessa |
| ReceivedBytes | Quantità di byte ricevuta |
| ProtocolName | Nome del protocollo di rete hello utilizzato |
| IPVersion | Versione IP |
| Direzione | In ingresso o in uscita |
| MaliciousIP | Indirizzo IP di un'origine dannosa nota |
| Severity | Gravità del software dannoso sospetto |
| RemoteIPCountry | Paese dell'indirizzo IP remoto hello |
| ManagementGroupName | Nome del gruppo di gestione di Operations Manager hello |
| SourceSystem | Origine in cui sono stati raccolti i dati |
| SessionStartTime | Data e ora di inizio della sessione |
| SessionEndTime | Data e ora di fine della sessione |
| LocalSubnet | Subnet in cui sono stati raccolti i dati |
| LocalPortNumber | Numero di porta locale |
| RemoteIP | Indirizzo IP remoto utilizzato dal computer remoto hello |
| RemotePortNumber | Numero di porta utilizzato dall'indirizzo IP remoto hello |
| SessionID | Valore univoco che identifica la sessione di comunicazione tra due indirizzi IP |
| SentBytes | Numero di byte inviati |
| TotalBytes | Numero totale dei byte inviati durante la sessione |
| ApplicationProtocol | Tipo di protocollo di rete usato   |
| ProcessID | ID processo Windows |
| ProcessName | Percorso e il nome del processo di hello |
| RemoteIPLongitude | Valore di longitudine dell'indirizzo IP |
| RemoteIPLatitude | Valore di latitudine dell'indirizzo IP |


## <a name="next-steps"></a>Passaggi successivi

- [Ricerca dei registri](log-analytics-log-searches.md) tooview dettagliate record di ricerca di dati di rete.
