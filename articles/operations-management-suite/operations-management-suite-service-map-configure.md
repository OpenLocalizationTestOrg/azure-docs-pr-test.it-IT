---
title: Mappa del servizio in Operations Management Suite aaaConfigure | Documenti Microsoft
description: "Mappa del servizio è una soluzione di Operations Management Suite che individua automaticamente i componenti dell'applicazione in Windows e mappe e i sistemi Linux hello la comunicazione tra servizi. Questo articolo fornisce informazioni dettagliate su come distribuire Mapping dei servizi nell'ambiente e su come usarlo in svariati scenari."
services: operations-management-suite
documentationcenter: 
author: daveirwin1
manager: jwhit
editor: tysonn
ms.assetid: d3d66b45-9874-4aad-9c00-124734944b2e
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/18/2016
ms.author: daseidma;bwren;dairwin
ms.openlocfilehash: 3127f4440f2886370f8ff617c405c6d70a926eb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-service-map-in-operations-management-suite"></a>Configurare Mapping dei servizi in Operations Management Suite
Mappa del servizio consente di individuare automaticamente i componenti dell'applicazione nei sistemi Windows e Linux e mappe hello la comunicazione tra servizi. È possibile utilizzarlo tooview i server come si immaginano - come sistemi interconnessi che offrono servizi critici. Mapping dei servizi mostra le connessioni fra i server, i processi e le porte di tutte le architetture connesse via TCP senza il bisogno di alcuna configurazione a parte l'installazione di un agente.

Questo articolo descrive i dettagli di hello di configurazione degli agenti di mappa del servizio e di caricamento. Per informazioni sull'utilizzo di mappa del servizio, vedere [utilizzare soluzioni di mapping servizio hello in Operations Management Suite](operations-management-suite-service-map.md).

## <a name="dependency-agent-downloads"></a>Download di Dependency Agent
| File | OS | Versione | SHA-256 |
|:--|:--|:--|:--|
| [InstallDependencyAgent-Windows.exe](https://aka.ms/dependencyagentwindows) | Windows | 9.0.5 | 73B3F6A2A76A08D58F72A550947FF839B588591C48E6EDDD6DDF73AA3FD82B43 |
| [InstallDependencyAgent-Linux64.bin](https://aka.ms/dependencyagentlinux) | Linux | 9.0.5 | A1BAD0B36EBF79F2B69113A07FCF48C68D90BD169C722689F9C83C69FC032371 |


## <a name="connected-sources"></a>Origini connesse
Mappa del servizio ottiene i dati da Microsoft Dependency Agent hello. Hello Dependency Agent dipende da hello agente OMS per il relativo tooOperations connessioni Management Suite. Ciò significa che un server deve avere hello agente OMS è installato e configurato prima e quindi hello che Dependency Agent può essere installato. Hello nella tabella seguente vengono descritte hello connesso origini che supporta la soluzione di hello mappa del servizio.

| Origine connessa | Supportato | Descrizione |
|:--|:--|:--|
| Agenti di Windows | Sì | L'elenco dei servizi analizza e raccoglie i dati dai computer agente Windows. <br><br>In aggiunta toohello [agente OMS](../log-analytics/log-analytics-windows-agents.md), gli agenti di Windows richiedono hello Microsoft Dependency Agent. Vedere hello [i sistemi operativi supportati](#supported-operating-systems) per un elenco completo delle versioni del sistema operativo. |
| Agenti Linux | Sì | L'elenco dei servizi analizza e raccoglie i dati dai computer agente Linux. <br><br>In aggiunta toohello [agente OMS](../log-analytics/log-analytics-linux-agents.md), gli agenti Linux richiedono hello Microsoft Dependency Agent. Vedere hello [i sistemi operativi supportati](#supported-operating-systems) per un elenco completo delle versioni del sistema operativo. |
| Gruppo di gestione di System Center Operations Manager | Sì | Mapping dei servizi analizza e raccoglie i dati dagli agenti Windows e Linux in un [gruppo di gestione System Center Operations Manager](../log-analytics/log-analytics-om-agents.md) connesso. <br><br>È necessaria una connessione diretta da hello System Center Operations Manager agent computer tooOperations Management Suite. Dati viene inoltrati dal repository di hello gestione gruppo toohello Operations Management Suite.|
| Account di archiviazione di Azure | No | Mappa del servizio raccoglie i dati dai computer agente, pertanto non sono presenti dati da esso toocollect da archiviazione di Azure. |

Mapping dei servizi supporta solo piattaforme a 64 bit.

In Windows hello Microsoft Monitoring Agent (MMA) viene utilizzato da System Center Operations Manager e Operations Management Suite toogather e invia i dati di monitoraggio. (Questo agente viene denominato hello agente System Center Operations Manager, agente OMS, agente di Log Analitica, MMA o agente diretto, a seconda del contesto di hello). System Center Operations Manager e Operations Management Suite fornire versioni diverse di out-hello casella di hello MMA. Queste versioni ogni possono segnalare tooboth tooSystem Center Operations Manager o tooOperations Management Suite.  

In Linux, hello agente OMS per Linux raccoglie e invia dati tooOperations Management Suite di monitoraggio. È possibile utilizzare mappa del servizio in server con agenti direttamente a OMS o in server che sono collegati tooOperations Management Suite tramite gruppi di gestione di System Center Operations Manager.  

In questo articolo, si farà riferimento se gli agenti tooall - Linux o Windows, se connesso tooa gruppo di gestione di System Center Operations Manager o direttamente tooOperations Management Suite: hello "OMS agente". Nome di distribuzione specifico hello dell'agente di hello verrà utilizzata solo se è necessario per il contesto.

agente di mapping servizio Hello non trasmette i dati se stesso e non richiede alcun toofirewalls modifiche o le porte. dati di Hello nella mappa del servizio vengono sempre trasmessi da hello agente OMS tooOperations Management Suite, direttamente o tramite hello OMS Gateway.

![Agenti di Mapping dei servizi](media/oms-service-map/agents.png)

Se non è un cliente di System Center Operations Manager con un tooOperations gruppo connesso gestione Management Suite:

- Se gli agenti di System Center Operations Manager possono accedere hello Internet tooconnect tooOperations Management Suite, non è richiesta alcuna configurazione aggiuntiva.  
- Se gli agenti di System Center Operations Manager non è possibile accedere a Operations Management Suite tramite hello Internet, è necessario tooconfigure hello OMS Gateway toowork con System Center Operations Manager.
  
Se si utilizza hello agente diretto di OMS, è necessario tooconfigure hello agente OMS stesso tooconnect tooOperations Management Suite o tooyour OMS Gateway. Hello OMS Gateway può essere scaricato da hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=52666).

### <a name="management-packs"></a>Management Pack
Quando si mappa del servizio viene attivata in un'area di lavoro di Operations Management Suite, un 300 KB management pack viene inviato i server di Windows hello tooall nell'area di lavoro. Se si usano agenti di System Center Operations Manager in un [gruppo di gestione connesso](../log-analytics/log-analytics-om-agents.md), hello management pack di mappa del servizio viene distribuito da System Center Operations Manager. Se gli agenti di hello siano connessi direttamente, Operations Management Suite offre management pack di hello.

management pack di Hello è denominato Microsoft.IntelligencePacks.ApplicationDependencyMonitor. È scritta too%Programfiles%\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs\. origine dati utilizzata dal management pack di hello Hello è % Program files%\Microsoft Monitoring Agent\Agent\Health Service State\Resources\<AutoGeneratedID > \ Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll.

## <a name="installation"></a>Installazione
### <a name="install-hello-dependency-agent-on-microsoft-windows"></a>Installare hello Dependency Agent su Microsoft Windows
Privilegi di amministratore sono necessari tooinstall o disinstallare l'agente di hello.

Hello Dependency Agent viene installato nei computer Windows tramite InstallDependencyAgent Windows.exe. Se si esegue il file eseguibile senza opzioni, viene avviata una procedura guidata è possibile seguire tooinstall in modo interattivo.  

Utilizzare i seguenti passaggi tooinstall hello Dependency Agent in ogni computer Windows hello:

1.  Installazione hello agente OMS tramite istruzioni hello in [toohello computer Windows di connettersi servizio Analitica di Log in Azure](../log-analytics/log-analytics-windows-agents.md).
2.  Scarica agente Windows hello ed eseguirlo tramite hello comando seguente: <br>`InstallDependencyAgent-Windows.exe`
3.  Eseguire l'agente hello guidata tooinstall hello.
4.  Se hello Dependency Agent non riesce toostart, controllare i registri di hello per informazioni dettagliate sull'errore. Per gli agenti di Windows, directory di log hello è %Programfiles%\Microsoft agent\logs. dipendenza. 

#### <a name="windows-command-line"></a>Riga di comando di Windows
Utilizzare le opzioni da hello seguente tabella tooinstall dalla riga di comando. un elenco dei flag di installazione hello, eseguire l'installazione hello utilizzando hello toosee /? come segue.

    InstallDependencyAgent-Windows.exe /?

| Flag | Descrizione |
|:--|:--|
| /? | Ottenere un elenco di opzioni della riga di comando hello. |
| /S | Eseguire un'installazione invisibile all'utente senza prompt per l'utente. |

Per impostazione predefinita, i file per agente dipendenza Windows hello vengono inseriti in c:\Programmi\Microsoft dipendenza Agent.

### <a name="install-hello-dependency-agent-on-linux"></a>Installare hello Dependency Agent in Linux
Accesso alla directory radice è necessario tooinstall o configurare l'agente di hello.

Hello Dependency Agent viene installato nei computer Linux tramite Linux64.bin InstallDependencyAgent, uno script della shell con un file autoestraente binario. È possibile eseguire il file hello utilizzando sh o aggiungere eseguire autorizzazioni toohello file stesso.
 
Utilizzare hello seguendo i passaggi tooinstall hello Dependency Agent in ogni computer Linux:

1.  Installazione hello agente OMS tramite istruzioni hello in [raccogliere e gestire i dati da computer Linux](https://technet.microsoft.com/library/mt622052.aspx).
2.  Installare l'agente Linux dipendenza hello come radice utilizzando hello comando seguente:<br>`sh InstallDependencyAgent-Linux64.bin`
3.  Se hello Dependency Agent non riesce toostart, controllare i registri di hello per informazioni dettagliate sull'errore. Per gli agenti Linux, directory di log hello è /var/opt/microsoft/dependency-agent/log.

un elenco dei flag di installazione di hello, eseguire il programma di installazione hello con toosee hello - Guida flag come indicato di seguito.

    InstallDependencyAgent-Linux64.bin -help

| Flag | Descrizione |
|:--|:--|
| -help | Ottenere un elenco di opzioni della riga di comando hello. |
| -s | Eseguire un'installazione invisibile all'utente senza prompt per l'utente. |
| --check | Controllare le autorizzazioni e il sistema operativo hello ma non si installa l'agente di hello. |

File per hello Dependency Agent vengono posizionati in hello seguente directory:

| File | Località |
|:--|:--|
| File core | /opt/microsoft/dependency-agent |
| File di log | /var/opt/microsoft/dependency-agent/log |
| File di configurazione | /etc/opt/microsoft/dependency-agent/config |
| File eseguibili del servizio | /opt/microsoft/dependency-agent/bin/microsoft-dependency-agent<br>/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent-manager |
| File binary di archiviazione | /var/opt/microsoft/dependency-agent/storage |

## <a name="installation-script-examples"></a>Esempi di script di installazione
tooeasily distribuire hello Dependency Agent su più server contemporaneamente, ma consente toouse uno script. È possibile utilizzare hello seguente toodownload esempi di script e installare hello Dependency Agent in Windows o Linux.

### <a name="powershell-script-for-windows"></a>Script di PowerShell per Windows
```PowerShell
Invoke-WebRequest "https://aka.ms/dependencyagentwindows" -OutFile InstallDependencyAgent-Windows.exe

.\InstallDependencyAgent-Windows.exe /S
```

### <a name="shell-script-for-linux"></a>Script della shell per Linux
```
wget --content-disposition https://aka.ms/dependencyagentlinux -O InstallDependencyAgent-Linux64.bin
sh InstallDependencyAgent-Linux64.bin -s
```

## <a name="desired-state-configuration"></a>Configurazione dello stato desiderato
hello toodeploy Dependency Agent tramite configurazione dello stato desiderato, è possibile utilizzare modulo xPSDesiredStateConfiguration hello e un po' di codice hello seguente:
```
configuration ServiceMap {

Import-DscResource -ModuleName xPSDesiredStateConfiguration

$DAPackageLocalPath = "C:\InstallDependencyAgent-Windows.exe"

Node localhost
{ 
    # Download and install hello Dependency Agent
    xRemoteFile DAPackage 
    {
        Uri = "https://aka.ms/dependencyagentwindows"
        DestinationPath = $DAPackageLocalPath
    }

    xPackage DA
    {
        Ensure="Present"
        Name = "Dependency Agent"
        Path = $DAPackageLocalPath
        Arguments = '/S'
        ProductId = ""
        InstalledCheckRegKey = "HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\DependencyAgent"
        InstalledCheckRegValueName = "DisplayName"
        InstalledCheckRegValueData = "Dependency Agent"
        DependsOn = "[xRemoteFile]DAPackage"
    }
  }
}
```

## <a name="uninstallation"></a>Disinstallazione
### <a name="uninstall-hello-dependency-agent-on-windows"></a>Disinstallare hello Dependency Agent in Windows
Un amministratore può disinstallare agente dipendenza hello per Windows tramite il pannello di controllo.

Un amministratore può anche eseguire %Programfiles%\Microsoft dipendenza Agent\Uninstall.exe toouninstall hello Dependency Agent.

### <a name="uninstall-hello-dependency-agent-on-linux"></a>Disinstallare hello Dependency Agent in Linux
Disinstalla toocompletely hello Dependency Agent da Linux, è necessario rimuovere l'agente di hello stesso e hello connettore, che viene installato automaticamente con l'agente di hello. È possibile disinstallare entrambi utilizzando hello singolo comando seguente:

    rpm -e dependency-agent dependency-agent-connector

## <a name="troubleshooting"></a>Risoluzione dei problemi
Se si verificano problemi di installazione o esecuzione di Mapping dei servizi, questa sezione può essere d'aiuto. Se si non riesce a risolvere il problema, contattare il supporto tecnico Microsoft.

### <a name="dependency-agent-installation-problems"></a>Problemi di installazione di Dependency Agent
#### <a name="installer-asks-for-a-reboot"></a>Il programma di installazione richiede il riavvio
Hello Dependency Agent *in genere* non richiedono un riavvio durante l'installazione o disinstallazione. Tuttavia, in alcuni casi rari, Windows Server richiede un riavvio toocontinue con un'installazione. Ciò si verifica quando una dipendenza, in genere hello Microsoft Visual C++ Redistributable, richiede un riavvio a causa di un file bloccato.

#### <a name="message-unable-tooinstall-dependency-agent-visual-studio-runtime-libraries-failed-tooinstall-code--codenumber-appears"></a>Messaggio "Impossibile tooinstall Dependency Agent: le librerie di Runtime di Visual Studio non è stato possibile tooinstall (codice = [code_number])" viene visualizzato

Hello Microsoft Dependency Agent si basa su librerie di runtime di Microsoft Visual Studio hello. Se si verifica un problema durante l'installazione delle librerie di hello, si riceverà un messaggio. 

programmi di installazione della libreria runtime Hello creare log nella cartella %LOCALAPPDATA%\temp hello. file Hello è dd_vcredist_arch_yyyymmddhhmmss.log, in cui *arch* è "x86" o "amd64" e *aaaammgghhmmss* è hello data e l'ora di creazione log hello (24 ore). log Hello fornisce dettagli sul problema hello che sta bloccando l'installazione.

Potrebbe essere utile tooinstall hello [librerie di runtime più recente](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads) manualmente prima.

Hello nella tabella seguente vengono elencati i numeri di codice e le soluzioni consigliate.

| Codice | Descrizione | Risoluzione |
|:--|:--|:--|
| 0x17 | programma di installazione di Hello libreria richiede un aggiornamento di Windows che non è stato installato. | Cercare nel Registro di installazione hello più recente della libreria.<br><br>Se un riferimento troppo "Windows8.1-KB2999226-x64" è seguito da una riga "errore 0x80240017: pacchetto MSU tooexecute non riuscito," non si dispone di hello prerequisiti tooinstall KB2999226. Seguire le istruzioni di hello nella sezione relativa ai prerequisiti hello [Universal C Runtime in Windows](https://support.microsoft.com/kb/2999226). Potrebbe essere necessario toorun Windows Update e riavviato più volte nei prerequisiti per l'ordine tooinstall hello.<br><br>Eseguire nuovamente il programma di installazione di hello Microsoft Dependency Agent. |

### <a name="post-installation-issues"></a>Problemi successivi all'installazione
#### <a name="server-doesnt-appear-in-service-map"></a>Il server non viene visualizzato in Mapping dei servizi
Se l'installazione dell'agente di dipendenza ha avuto esito positivo, ma non vengono visualizzate in hello soluzione mappa del servizio del server:
* Hello Dependency Agent sia installato correttamente? È possibile convalidarlo controllando toosee se è installato il servizio hello e in esecuzione.<br><br>
**Windows**: cercare hello servizio denominato "Microsoft Dependency agente".<br>
**Linux**: cercare hello esecuzione processo di "microsoft dependency agent."

* Trovano in hello [libero tariffario di Operations Management Suite/Log Analitica](https://docs.microsoft.com/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers)? piano gratuito hello consente per i server di toofive univoco mappa del servizio. Tutti i server successivi non verranno visualizzati nella mappa del servizio, anche se hello cinque precedenti non inviano dati.

* È il log del server di invio e prestazioni dati tooOperations Management Suite? Passare tooLog ricerca ed eseguire hello seguente query per il computer: 

        * Computer="<your computer name here>" | measure count() by Type
        
  Sono stati ottenuti un'ampia gamma di eventi nei risultati di hello? È recente dati hello? In questo caso, l'agente OMS è funzioni correttamente e la comunicazione con hello servizio Operations Management Suite. In caso contrario, controllare hello agente OMS nel server: [risoluzione dei problemi dell'agente OMS per Windows](https://support.microsoft.com/help/3126513/how-to-troubleshoot-operations-management-suite-onboarding-issues) o [agente OMS per la risoluzione dei problemi di Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md).

#### <a name="server-appears-in-service-map-but-has-no-processes"></a>Il server viene visualizzato in Mapping dei servizi, ma non dispone di alcun processo
Se si visualizza il server nella mappa del servizio, ma non contiene alcun dato di processo o una connessione, che indica che hello Dependency Agent sia installato e in esecuzione, ma non è stato caricato il driver kernel hello. 

Controllare il file di C:\Program Files\Microsoft dipendenza Agent\logs\wrapper.log hello (Windows) o /var/opt/microsoft/dependency-agent/log/service.log (Linux). ultime righe di Hello del file hello dovrebbe essere indicato perché non è stato caricato i kernel hello. Ad esempio, il kernel hello potrebbe non essere supportato in Linux se è stato aggiornato il kernel.

## <a name="data-collection"></a>Raccolta dei dati
È possibile prevedere tootransmit ogni agente circa 25 MB al giorno, a seconda della complessità delle dipendenze del sistema. I dati sulle dipendenze di Mapping dei servizi vengono inviati da ogni agente ogni 15 secondi.  

Hello Dependency Agent utilizza in genere 0,1 percento della memoria di sistema e 0,1 percento della CPU di sistema.

## <a name="supported-azure-regions"></a>Aree di Azure supportate
Mappa del servizio è attualmente disponibile in hello seguenti aree di Azure:
- Stati Uniti Orientali
- Europa occidentale
- Stati Uniti centro-occidentali


## <a name="supported-operating-systems"></a>Sistemi operativi supportati
Hello nelle sezioni seguenti vengono elencano i sistemi operativi supportato hello per hello Dependency Agent. Mapping dei servizi non supporta le architetture a 32 bit per i sistemi operativi.

### <a name="windows-server"></a>Windows Server
- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2 SP1,

### <a name="windows-desktop"></a>Desktop di Windows
- Windows 10
- Windows 8.1
- Windows 8
- Windows 7

### <a name="red-hat-enterprise-linux-centos-linux-and-oracle-linux-with-rhel-kernel"></a>Red Hat Enterprise Linux, CentOS Linux e Oracle Linux (con il kernel RHEL)
- Sono supportate solo versioni predefinita e SMP del kernel Linux.
- Le versioni del kernel non standard, ad esempio PAE e Xen, non sono supportate per le distribuzioni Linux. Ad esempio, un sistema con stringa di versione di hello di "2.6.16.21-0.8-xen" non è supportato.
- I kernel personalizzati, tra cui le ricompilazioni dei kernel standard, non sono supportati.
- Il kernel CentOSPlus non è supportato.
- Unbreakable Enterprise Kernel (UEK) di Oracle è illustrato in una sezione successiva di questo articolo.


#### <a name="red-hat-linux-7"></a>Red Hat Linux 7
| Versione del sistema operativo | Versione del kernel |
|:--|:--|
| 7.0 | 3.10.0-123 |
| 7.1 | 3.10.0-229 |
| 7,2 | 3.10.0-327 |
| 7.3 | 3.10.0-514 |

#### <a name="red-hat-linux-6"></a>Red Hat Linux 6
| Versione del sistema operativo | Versione del kernel |
|:--|:--|
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
| Versione del sistema operativo | Versione del kernel |
|:--|:--|
| 5.8 | 2.6.18-308 |
| 5.9 | 2.6.18-348 |
| 5.10 | 2.6.18-371 |
| 5.11 | 2.6.18-398<br>2.6.18-400<br>2.6.18-402<br>2.6.18-404<br>2.6.18-406<br>2.6.18-407<br>2.6.18-408<br>2.6.18-409<br>2.6.18-410<br>2.6.18-411<br>2.6.18-412<br>2.6.18-416<br>2.6.18-417<br>2.6.18-419 |

#### <a name="oracle-enterprise-linux-with-unbreakable-enterprise-kernel"></a>Oracle Enterprise Linux con Unbreakable Enterprise Kernel

#### <a name="oracle-linux-6"></a>Oracle Linux 6
| Versione del sistema operativo | Versione del kernel
|:--|:--|
| 6.2 | Oracle 2.6.32-300 (UEK R1) |
| 6.3 | Oracle 2.6.39-200 (UEK R2) |
| 6.4 | Oracle 2.6.39-400 (UEK R2) |
| 6,5 | Oracle 2.6.39-400 (UEK R2 i386) |
| 6.6 | Oracle 2.6.39-400 (UEK R2 i386) |

#### <a name="oracle-linux-5"></a>Oracle Linux 5

| Versione del sistema operativo | Versione del kernel
|:--|:--|
| 5.8 | Oracle 2.6.32-300 (UEK R1) |
| 5.9 | Oracle 2.6.39-300 (UEK R2) |
| 5.10 | Oracle 2.6.39-400 (UEK R2) |
| 5.11 | Oracle 2.6.39-400 (UEK R2) |

#### <a name="suse-linux-enterprise-server"></a>SUSE Linux Enterprise Server

#### <a name="suse-linux-11"></a>SUSE Linux 11
| Versione del sistema operativo | Versione del kernel
|:--|:--|
| 11 | 2.6.27 |
| 11 SP1 | 2.6.32 |
| 11 SP2 | 3.0.13 |
| 11 SP3 | 3.0.76 |
| 11 SP4 | 3.0.101 |

#### <a name="suse-linux-10"></a>SUSE Linux 10
| Versione del sistema operativo | Versione del kernel
|:--|:--|
| 10 SP4 | 2.6.16.60 |

## <a name="diagnostic-and-usage-data"></a>Dati di diagnostica e di utilizzo
Microsoft raccoglie automaticamente i dati di utilizzo e prestazioni tramite l'utilizzo di hello servizio mappa del servizio. Microsoft utilizza questo tooprovide dati e migliorare la qualità di hello, sicurezza e integrità del servizio di mapping servizio hello. Dati includono informazioni sulla configurazione di hello del software, ad esempio sistema operativo e versione. Include inoltre l'indirizzo IP, nome DNS e nome della workstation in funzionalità di risoluzione dei problemi di ordine tooprovide accurata ed efficiente. Non vengono raccolti nomi, indirizzi o altre informazioni di contatto.

Per ulteriori informazioni sulla raccolta dei dati e sull'utilizzo, vedere hello [informativa sulla Privacy di servizi Online Microsoft](https://go.microsoft.com/fwlink/?LinkId=512132).



## <a name="next-steps"></a>Passaggi successivi
- Informazioni su come troppo[utilizzare mappa servizio](operations-management-suite-service-map.md) dopo che è stato distribuito e configurato.
