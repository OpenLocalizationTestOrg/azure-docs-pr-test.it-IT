---
title: "hello aaaDeploy servizio di mobilità di ripristino del sito con DSC di automazione di Azure | Documenti Microsoft"
description: "Viene descritto come toouse Automation DSC per Azure tooautomatically distribuire il servizio di mobilità di Azure Site Recovery hello e l'agente di Azure per la VM VMware e server fisico replica tooAzure"
services: site-recovery
documentationcenter: 
author: krnese
manager: lorenr
editor: 
ms.assetid: 1f8cd3ac-0522-48eb-a5f0-679ee9192ddb
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: krnese
ms.openlocfilehash: 52cdd13ceb61718a21137180c55db86919af5929
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-mobility-service-with-azure-automation-dsc-for-replication-of-vm"></a>Distribuzione di servizio di mobilità hello con DSC di automazione di Azure per la replica della macchina virtuale
In Operations Management Suite offriamo una soluzione completa per il backup e il ripristino di emergenza che può essere usata nell'ambito del piano di continuità aziendale.

Il percorso è iniziato da Hyper-V con la replica Hyper-V, Ma abbiamo toosupport espanso un programma di installazione eterogenea poiché i clienti dispongono di più piattaforme e hypervisor nel cloud a loro.

Se si eseguono i carichi di lavoro di VMware e/o di server fisici oggi, un server di gestione esegue tutti di hello componenti di Azure Site Recovery nell'ambiente toohandle hello comunicazioni e i dati della replica con Azure, quando la destinazione di Azure.

## <a name="deploy-hello-site-recovery-mobility-service-by-using-automation-dsc"></a>Distribuire il servizio di mobilità di ripristino del sito di hello tramite DSC di automazione
Per iniziare, è bene riepilogare le operazioni eseguite da questo server di gestione.

il server di gestione di Hello esegue diversi ruoli del server. Uno di questi ruoli è la *configurazione*, che coordina la comunicazione e gestisce i processi di ripristino e replica dei dati.

Inoltre, hello *processo* ruolo funge da gateway replica. Questo ruolo riceve i dati di replica dai computer di origine protetta ottimizzata con la memorizzazione nella cache, la compressione e crittografia e lo invia tooan account di archiviazione Azure. Una delle funzioni hello per ruolo processo hello è anche un'installazione toopush macchine tooprotected del servizio di mobilità hello ed eseguire l'individuazione automatica delle macchine virtuali VMware.

Se è presente un failback da Azure, hello *destinazione master* ruolo gestirà i dati di replica hello come parte di questa operazione.

Per i computer protetti hello, si affidano hello *servizio di mobilità*. Questo componente è tooevery distribuito machine (VM VMware o server fisico) che si desidera tooreplicate tooAzure. Scrive dati nel computer di hello acquisisce e li inoltra a server di gestione toohello (ruolo di processo).

Quando si gestiscono la continuità aziendale, è importante toounderstand i carichi di lavoro, l'infrastruttura e hello componenti coinvolti. È quindi possibile soddisfare i requisiti di hello per l'obiettivo del tempo di ripristino (RTO) e un obiettivo del punto di ripristino (RPO). In questo contesto, hello servizio di mobilità è tooensuring chiave che i carichi di lavoro siano protetti nel modo previsto.

Come possiamo garantire nel modo migliore che la configurazione sia affidabile e protetta usando alcuni componenti di Operations Management Suite?

In questo articolo viene fornito un esempio di come è possibile utilizzare Azure Automation DSC Desired State Configuration (), insieme a Site Recovery, tooensure che:

* il servizio di mobilità Hello e agente VM di Azure sono computer che eseguono Windows toohello distribuita che si desidera tooprotect.
* servizio di mobilità Hello e agente VM di Azure sono sempre in esecuzione quando la destinazione di replica hello Azure.

## <a name="prerequisites"></a>Prerequisiti
* Un programma di installazione di repository toostore hello richiesto
* Una passphrase tooregister di repository toostore hello richiesto con il server di gestione di hello

  > [!NOTE]
  > Per ogni server di gestione viene generata una passphrase univoca. Se si intende toodeploy più server di gestione, è necessario tooensure tale hello passphrase viene archiviata nel file passphrase.txt hello corretto.
  >
  >
* Windows Management Framework (WMF) 5.0 installato nei computer hello che si desidera tooenable per la protezione dati (un requisito per DSC di automazione)

  > [!NOTE]
  > Se si vuole toouse DSC per Windows macchine che dispongono di WMF 4.0 installato, vedere la sezione hello [DSC di utilizzo in ambienti disconnessi](## Use DSC in disconnected environments).
  

il servizio di mobilità Hello può essere installato tramite riga di comando hello e accetta diversi argomenti. Sono necessari i file binari hello toohave (dopo estrarli il programma di installazione) e archiviarli in una posizione in cui è possibile recuperare tramite una configurazione DSC.

## <a name="step-1-extract-binaries"></a>Passaggio 1: estrazione dei file binari
1. tooextract hello i file necessari per il programma di installazione, passare toohello seguenti directory nel server di gestione:

    **\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**

    In questa cartella dovrebbe essere presente un file MSI denominato:

    **Microsoft-ASR_UA_version_Windows_GA_date_Release.exe**

    Utilizzare hello installer hello tooextract di comando seguente:

    **.\Microsoft-ASR_UA_9.1.0.0_Windows_GA_02May2016_release.exe /q /x:C:\Users\Administrator\Desktop\Mobility_Service\Extract**
2. Selezionare tutti i file e li inviano tooa compressa (zip).

È ora i file binari hello che è necessario il programma di installazione di tooautomate hello del servizio di mobilità hello tramite DSC di automazione.

### <a name="passphrase"></a>Passphrase
Successivamente, è necessario toodetermine in cui si desidera tooplace questa cartella compressa. È possibile utilizzare un account di archiviazione di Azure, come illustrato più avanti, toostore hello passphrase è necessario per l'installazione di hello. agente Hello verrà quindi registrato con il server di gestione hello come parte del processo di hello.

passphrase Hello ottenuti quando è stato distribuito il server di gestione di hello può essere salvata i file di testo tooa come passphrase.txt.

Posizionare la cartella compressa hello sia hello passphrase in un contenitore dedicato in hello account di archiviazione di Azure.

![Percorso della cartella](./media/site-recovery-automate-mobilitysevice-install/folder-and-passphrase-location.png)

Se si preferiscono tookeep questi file in una condivisione in rete, è possibile farlo. È sufficiente tooensure che le risorse DSC hello che verrà utilizzato in un secondo momento può accedere e possono ottenere il programma di installazione di hello e la passphrase.

## <a name="step-2-create-hello-dsc-configuration"></a>Passaggio 2: Creare una configurazione DSC hello
il programma di installazione di Hello dipende da WMF 5.0. Per hello macchina toosuccessfully applicare la configurazione di hello DSC di automazione, WMF 5.0 deve toobe presente.

ambiente Hello utilizza hello seguente esempio di configurazione DSC:

```powershell
configuration ASRMobilityService {

    $RemoteFile = 'https://knrecstor01.blob.core.windows.net/asr/ASR.zip'
    $RemotePassphrase = 'https://knrecstor01.blob.core.windows.net/asr/passphrase.txt'
    $RemoteAzureAgent = 'http://go.microsoft.com/fwlink/p/?LinkId=394789'
    $LocalAzureAgent = 'C:\Temp\AzureVmAgent.msi'
    $TempDestination = 'C:\Temp\asr.zip'
    $LocalPassphrase = 'C:\Temp\Mobility_service\passphrase.txt'
    $Role = 'Agent'
    $Install = 'C:\Program Files (x86)\Microsoft Azure Site Recovery'
    $CSEndpoint = '10.0.0.115'
    $Arguments = '/Role "{0}" /InstallLocation "{1}" /CSEndpoint "{2}" /PassphraseFilePath "{3}"' -f $Role,$Install,$CSEndpoint,$LocalPassphrase

    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    node localhost {

        File Directory {
            DestinationPath = 'C:\Temp\ASRSetup\'
            Type = 'Directory'            
        }

        xRemoteFile Setup {
            URI = $RemoteFile
            DestinationPath = $TempDestination
            DependsOn = '[File]Directory'
        }

        xRemoteFile Passphrase {
            URI = $RemotePassphrase
            DestinationPath = $LocalPassphrase
            DependsOn = '[File]Directory'
        }

        xRemoteFile AzureAgent {
            URI = $RemoteAzureAgent
            DestinationPath = $LocalAzureAgent
            DependsOn = '[File]Directory'
        }

        Archive ASRzip {
            Path = $TempDestination
            Destination = 'C:\Temp\ASRSetup'
            DependsOn = '[xRemotefile]Setup'
        }

        Package Install {
            Path = 'C:\temp\ASRSetup\ASR\UNIFIEDAGENT.EXE'
            Ensure = 'Present'
            Name = 'Microsoft Azure Site Recovery mobility Service/Master Target Server'
            ProductId = '275197FC-14FD-4560-A5EB-38217F80CBD1'
            Arguments = $Arguments
            DependsOn = '[Archive]ASRzip'
        }

        Package AzureAgent {
            Path = 'C:\Temp\AzureVmAgent.msi'
            Ensure = 'Present'
            Name = 'Windows Azure VM Agent - 2.7.1198.735'
            ProductId = '5CF4D04A-F16C-4892-9196-6025EA61F964'
            Arguments = '/q /l "c:\temp\agentlog.txt'
            DependsOn = '[Package]Install'
        }

        Service ASRvx {
            Name = 'svagents'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service ASR {
            Name = 'InMage Scout Application Service'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service AzureAgentService {
            Name = 'WindowsAzureGuestAgent'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }

        Service AzureTelemetry {
            Name = 'WindowsAzureTelemetryService'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }
    }
}
```
configurazione di Hello eseguirà seguente hello:

* le variabili di Hello indicherà configurazione hello in tooget hello binari per il servizio di mobilità hello e agente VM di Azure hello, in cui tooget hello passphrase e toostore hello di output.
* Hello configurazione importerà risorsa xPSDesiredStateConfiguration DSC hello, in modo che è possibile utilizzare `xRemoteFile` file hello toodownload dal repository hello.
* configurazione di Hello creerà una directory in cui i file binari hello toostore.
* risorsa archive Hello estrarrà file hello dalla cartella compressa hello.
* il nome di risorsa di installazione del pacchetto Hello installerà il servizio di mobilità hello hello UNIFIEDAGENT. Programma di installazione EXE con gli argomenti specifici hello. (le variabili hello costruire argomenti hello necessaria tooreflect toobe modificato ambiente).
* il pacchetto di Hello AzureAgent risorse installerà l'agente VM di Azure hello, che è consigliabile in ogni macchina virtuale in esecuzione in Azure. agente VM di Azure Hello rende possibili tooadd estensioni toohello VM dopo il failover.
* Hello risorsa del servizio o risorse assicurerà che hello correlate a servizi di mobilità e hello servizi di Azure sono sempre in esecuzione.

Salvare la configurazione di hello come **ASRMobilityService**.

> [!NOTE]
> Tenere presente che tooreplace hello CSIP nel server di gestione vera e propria hello tooreflect configurazione, in modo che verrà connessa correttamente hello agente e utilizzerà la passphrase corretta hello.
>
>

## <a name="step-3-upload-tooautomation-dsc"></a>Passaggio 3: Caricare tooAutomation DSC
Poiché configurazione hello DSC apportate importerà un modulo di risorse DSC necessari (xPSDesiredStateConfiguration), è necessario tooimport in automazione di tale modulo prima di caricare la configurazione DSC hello.

Accedi con account di automazione, tooyour Sfoglia troppo**asset** > **moduli**, fare clic su **Sfoglia raccolta**.

Qui è possibile cercare il modulo hello e importarlo tooyour account.

![Importazione del modulo](./media/site-recovery-automate-mobilitysevice-install/search-and-import-module.png)

Al termine, andare tooyour macchina in cui i moduli di gestione risorse di Azure hello installati e procedere della configurazione DSC tooimport hello appena creato.

### <a name="import-cmdlets"></a>Cmdlet di importazione
In PowerShell, accedi tooyour sottoscrizione di Azure. Modificare l'ambiente di hello cmdlet tooreflect e acquisire le informazioni sull'account di automazione in una variabile:

```powershell
$AAAccount = Get-AzureRmAutomationAccount -ResourceGroupName 'KNOMS' -Name 'KNOMSAA'
```

Caricare hello configurazione tooAutomation DSC usando hello seguente cmdlet:

```powershell
$ImportArgs = @{
    SourcePath = 'C:\ASR\ASRMobilityService.ps1'
    Published = $true
    Description = 'DSC Config for Mobility Service'
}
$AAAccount | Import-AzureRmAutomationDscConfiguration @ImportArgs
```

### <a name="compile-hello-configuration-in-automation-dsc"></a>Compilare la configurazione hello in DSC di automazione
Successivamente, è necessario configurazione hello toocompile in DSC di automazione, in modo che è possibile avviare tooregister tooit di nodi. Ottenere questo risultato eseguendo hello seguente cmdlet:

```powershell
$AAAccount | Start-AzureRmAutomationDscCompilationJob -ConfigurationName ASRMobilityService
```

L'operazione può richiedere alcuni minuti, in quanto si distribuisce sostanzialmente servizio di pull DSC di hello configurazione toohello ospitato.

Dopo aver compilato la configurazione hello, è possibile recuperare informazioni sul processo hello tramite PowerShell (Get-AzureRmAutomationDscCompilationJob) o tramite hello [portale di Azure](https://portal.azure.com/).

![Recuperare il processo](./media/site-recovery-automate-mobilitysevice-install/retrieve-job.png)

Si dispone ora correttamente pubblicata e caricato il tooAutomation di configurazione DSC DSC.

## <a name="step-4-onboard-machines-tooautomation-dsc"></a>Passaggio 4: Caricare le macchine tooAutomation DSC
> [!NOTE]
> Uno dei prerequisiti di hello per il completamento di questo scenario è che i computer Windows vengono aggiornati con la versione più recente di hello di WMF. È possibile scaricare e installare la versione corretta di hello per la piattaforma di hello [area Download](https://www.microsoft.com/download/details.aspx?id=50395).
>
>

Si creerà un metaconfig si applicherà tooyour nodi DSC. toosucceed con questo oggetto, è necessario tooretrieve hello endpoint URL e hello chiave primaria per l'account di automazione selezionato in Azure. È possibile trovare questi valori in **chiavi** su hello **tutte le impostazioni** pannello hello account di automazione.

![Valori chiave](./media/site-recovery-automate-mobilitysevice-install/key-values.png)

In questo esempio, è necessario un server fisico di Windows Server 2012 R2 che si desidera tooprotect tramite il ripristino del sito.

### <a name="check-for-any-pending-file-rename-operations-in-hello-registry"></a>Verificare la presenza di eventuali operazioni di ridenominazione di file nel Registro di sistema hello in sospeso
Prima di iniziare server hello tooassociate con endpoint di hello DSC di automazione, è consigliabile verificare la disponibilità di eventuali operazioni di ridenominazione di file nel Registro di sistema hello in sospeso. Potrebbe impedire che il programma di installazione di hello completamento a causa di tooa il riavvio in sospeso.

Eseguire hello tooverify cmdlet che non vi sia alcun riavvio in sospeso nel server di hello seguenti:

```powershell
Get-ItemProperty 'HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\' | Select-Object -Property PendingFileRenameOperations
```
Se questa risulta vuota, verrà tooproceed OK. In caso contrario, è necessario risolvere il problema riavviando server hello durante una finestra di manutenzione.

configurazione di hello tooapply nel server di hello, avviare hello PowerShell Integrated Scripting Environment (ISE) ed eseguire lo script seguente hello. Questa è essenzialmente una configurazione locale di DSC che indicare hello Gestione configurazione locale del motore tooregister con hello servizio DSC di automazione e recuperare la configurazione specifica hello (ASRMobilityService.localhost).

```powershell
[DSCLocalConfigurationManager()]
configuration metaconfig {
    param (
        $URL,
        $Key
    )
    node localhost {
        Settings {
            RefreshFrequencyMins = '30'
            RebootNodeIfNeeded = $true
            RefreshMode = 'PULL'
            ActionAfterReboot = 'ContinueConfiguration'
            ConfigurationMode = 'ApplyAndMonitor'
            AllowModuleOverwrite = $true
        }

        ResourceRepositoryWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
        }

        ConfigurationRepositoryWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
            ConfigurationNames = 'ASRMobilityService.localhost'
        }

        ReportServerWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
        }
    }
}
metaconfig -URL 'https://we-agentservice-prod-1.azure-automation.net/accounts/<YOURAAAccountID>' -Key '<YOURAAAccountKey>'

Set-DscLocalConfigurationManager .\metaconfig -Force -Verbose
```

Questa configurazione genera hello Gestione configurazione locale tooregister motore stesso con DSC di automazione. Viene inoltre determinato funzionamento motore hello, come procedere se è presente una deviazione della configurazione (ApplyAndAutoCorrect) e come deve procedere con la configurazione di hello se è necessario un riavvio.

Dopo aver eseguito questo script, il nodo hello deve iniziare tooregister con DSC di automazione.

![Registrazione del nodo in corso](./media/site-recovery-automate-mobilitysevice-install/register-node.png)

Se si torna indietro toohello portale di Azure, è possibile visualizzare il nodo appena registrato hello è ora presente nel portale di hello.

![Nodo registrato nel portale di hello](./media/site-recovery-automate-mobilitysevice-install/registered-node.png)

Nel server di hello, è possibile eseguire hello tooverify cmdlet che hello nodo sia stato registrato correttamente PowerShell seguente:

```powershell
Get-DscLocalConfigurationManager
```

Dopo la configurazione di hello è stata estratta e applicata toohello server, è possibile verificare questa eseguendo hello seguente cmdlet:

```powershell
Get-DscConfigurationStatus
```

output di Hello mostra che il server hello è estratta correttamente la configurazione:

![Output](./media/site-recovery-automate-mobilitysevice-install/successful-config.png)

Inoltre, l'installazione del servizio di mobilità hello include il proprio log in cui è reperibile in *SystemDrive*\ProgramData\ASRSetupLogs.

La procedura è terminata. È ora correttamente distribuito e registrazione del servizio di mobilità hello computer hello che si desidera tooprotect tramite il ripristino del sito. DSC verrà assicurarsi che i servizi necessario hello sono sempre in esecuzione.

![Distribuzione completata](./media/site-recovery-automate-mobilitysevice-install/successful-install.png)

Dopo che il server di gestione di hello rileva una distribuzione corretta di hello, è possibile configurare la protezione e abilitare la replica nella macchina hello tramite il ripristino del sito.

## <a name="use-dsc-in-disconnected-environments"></a>Uso di DSC in ambienti non connessi
Se i computer non connesso toohello Internet, è possibile affidarsi toodeploy DSC e configurare il servizio di mobilità hello sui carichi di lavoro hello che si desidera tooprotect.

È possibile creare istanze del server di pull DSC nel proprio ambiente tooessentially funzionalità hello stesso che si ottiene da Automation DSC. Ovvero, i client hello effettuerà il pull configurazione hello (dopo la registrazione) toohello DSC endpoint. Tuttavia, un'altra opzione è toomanually push hello DSC configurazione tooyour macchine, locale o remoto.

Si noti che in questo esempio, un parametro aggiunto hello nome del computer. i file remoti Hello si trovano in una condivisione remota deve essere accessibile dai computer hello che si desidera tooprotect. fine Hello dello script di hello attivarne configurazione hello e quindi avvia il computer di destinazione toohello tooapply hello DSC configurazione.

### <a name="prerequisites"></a>Prerequisiti
Verificare che sia installato il modulo di PowerShell xPSDesiredStateConfiguration hello. Per i computer Windows in cui è installato WMF 5.0, è possibile installare modulo xPSDesiredStateConfiguration hello eseguendo i seguenti cmdlet nei computer di destinazione hello hello:

```powershell
Find-Module -Name xPSDesiredStateConfiguration | Install-Module
```

È anche possibile scaricare e salvare il modulo hello nel caso in cui è necessario toodistribute è tooWindows macchine che dispongono di WMF 4.0. Eseguire questo cmdlet su un computer in cui è presente PowerShellGet (WMF 5.0):

```powershell
Save-Module -Name xPSDesiredStateConfiguration -Path <location>
```

Inoltre, per WMF 4.0, assicurarsi che hello [Windows 8.1 update KB2883200](https://www.microsoft.com/download/details.aspx?id=40749) viene installato nei computer hello.

Hello configurazione seguente può essere inserita tooWindows macchine che dispongono di WMF 5.0 e WMF 4.0:

```powershell
configuration ASRMobilityService {
    param (
        [Parameter(Mandatory=$true)]
        [ValidateNotNullOrEmpty()]
        [System.String] $ComputerName
    )

    $RemoteFile = '\\myfileserver\share\asr.zip'
    $RemotePassphrase = '\\myfileserver\share\passphrase.txt'
    $RemoteAzureAgent = '\\myfileserver\share\AzureVmAgent.msi'
    $LocalAzureAgent = 'C:\Temp\AzureVmAgent.msi'
    $TempDestination = 'C:\Temp\asr.zip'
    $LocalPassphrase = 'C:\Temp\Mobility_service\passphrase.txt'
    $Role = 'Agent'
    $Install = 'C:\Program Files (x86)\Microsoft Azure Site Recovery'
    $CSEndpoint = '10.0.0.115'
    $Arguments = '/Role "{0}" /InstallLocation "{1}" /CSEndpoint "{2}" /PassphraseFilePath "{3}"' -f $Role,$Install,$CSEndpoint,$LocalPassphrase

    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    node $ComputerName {      
        File Directory {
            DestinationPath = 'C:\Temp\ASRSetup\'
            Type = 'Directory'            
        }

        xRemoteFile Setup {
            URI = $RemoteFile
            DestinationPath = $TempDestination
            DependsOn = '[File]Directory'
        }

        xRemoteFile Passphrase {
            URI = $RemotePassphrase
            DestinationPath = $LocalPassphrase
            DependsOn = '[File]Directory'
        }

        xRemoteFile AzureAgent {
            URI = $RemoteAzureAgent
            DestinationPath = $LocalAzureAgent
            DependsOn = '[File]Directory'
        }

        Archive ASRzip {
            Path = $TempDestination
            Destination = 'C:\Temp\ASRSetup'
            DependsOn = '[xRemotefile]Setup'
        }

        Package Install {
            Path = 'C:\temp\ASRSetup\ASR\UNIFIEDAGENT.EXE'
            Ensure = 'Present'
            Name = 'Microsoft Azure Site Recovery mobility Service/Master Target Server'
            ProductId = '275197FC-14FD-4560-A5EB-38217F80CBD1'
            Arguments = $Arguments
            DependsOn = '[Archive]ASRzip'
        }

        Package AzureAgent {
            Path = 'C:\Temp\AzureVmAgent.msi'
            Ensure = 'Present'
            Name = 'Windows Azure VM Agent - 2.7.1198.735'
            ProductId = '5CF4D04A-F16C-4892-9196-6025EA61F964'
            Arguments = '/q /l "c:\temp\agentlog.txt'
            DependsOn = '[Package]Install'
        }

        Service ASRvx {
            Name = 'svagents'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service ASR {
            Name = 'InMage Scout Application Service'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service AzureAgentService {
            Name = 'WindowsAzureGuestAgent'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }

        Service AzureTelemetry {
            Name = 'WindowsAzureTelemetryService'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }
    }
}
ASRMobilityService -ComputerName 'MyTargetComputerName'

Start-DscConfiguration .\ASRMobilityService -Wait -Force -Verbose
```

Se si desidera tooinstantiate il proprio server di pull DSC le funzionalità di hello toomimic rete aziendale che è possibile ottenere da Automation DSC, vedere [configurando un server di pull web DSC](https://msdn.microsoft.com/powershell/dsc/pullserver?f=255&MSPPError=-2147217396).

## <a name="optional-deploy-a-dsc-configuration-by-using-an-azure-resource-manager-template"></a>Facoltativo: distribuire una configurazione DSC usando il modello di Azure Resource Manager
In questo articolo è incentrata su come creare la propria tooautomatically configurazione DSC distribuire il servizio di mobilità hello e agente VM di Azure - hello e assicurarsi che vengano eseguiti in macchine hello che si desidera tooprotect. È necessario anche un modello di gestione risorse di Azure che consente di distribuire questo DSC configurazione tooa account nuovo o esistente automazione di Azure. modello Hello utilizzerà gli asset di automazione toocreate parametri di input contenenti variabili hello per l'ambiente.

Dopo aver distribuito il modello di hello, è possibile semplicemente fare riferimento toostep 4 in tooonboard questa guida per i computer.

modello Hello eseguirà seguente hello:

1. Usare un account di Automazione esistente e crearne uno nuovo
2. Accettare i parametri di input per:
   * ASRRemoteFile - percorso hello in cui sono memorizzati l'installazione del servizio di mobilità hello
   * ASRPassphrase - percorso hello in cui sono memorizzati file passphrase.txt hello
   * ASRCSEndpoint - indirizzo IP di hello del server di gestione
3. Importare il modulo PowerShell di hello xPSDesiredStateConfiguration
4. Creare e compilare una configurazione DSC hello

Hello tutti i passaggi precedenti, viene eseguito nell'ordine corretto hello, in modo che è possibile avviare l'onboarding di computer per la protezione.

modello di Hello, con le istruzioni per la distribuzione, si trova in [GitHub](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/DSC).

Distribuire il modello di hello tramite PowerShell:

```powershell
$RGDeployArgs = @{
    Name = 'DSC3'
    ResourceGroupName = 'KNOMS'
    TemplateFile = 'https://raw.githubusercontent.com/krnese/AzureDeploy/master/OMS/MSOMS/DSC/azuredeploy.json'
    OMSAutomationAccountName = 'KNOMSAA'
    ASRRemoteFile = 'https://knrecstor01.blob.core.windows.net/asr/ASR.zip'
    ASRRemotePassphrase = 'https://knrecstor01.blob.core.windows.net/asr/passphrase.txt'
    ASRCSEndpoint = '10.0.0.115'
    DSCJobGuid = [System.Guid]::NewGuid().ToString()
}
New-AzureRmResourceGroupDeployment @RGDeployArgs -Verbose
```

## <a name="next-steps"></a>Passaggi successivi
Dopo aver distribuito gli agenti di servizi di mobilità hello, è possibile [abilitare la replica](site-recovery-vmware-to-azure.md) per le macchine virtuali hello.
