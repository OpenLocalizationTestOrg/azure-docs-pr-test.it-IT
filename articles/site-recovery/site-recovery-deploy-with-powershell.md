---
title: aaaReplicate tooAzure di macchine virtuali Hyper-V nel portale classico di hello con PowerShell | Documenti Microsoft
description: Automatizzare la replica delle macchine virtuali Hyper-V nei cloud VMM tramite il ripristino del sito e PowerShell nel portale classico hello hello
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhiag
editor: tysonn
ms.assetid: 9011f567-e0b4-4306-951a-b30da19f5db6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: d6847b46ac227209e6890de4ab603b23f827360f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-vms-tooazure-with-powershell-in-hello-classic-portal"></a>Replicare tooAzure macchine virtuali Hyper-V con PowerShell nel portale classico hello
> [!div class="op_single_selector"]
> * [Portale di Azure](site-recovery-vmm-to-azure.md)
> * [PowerShell - Gestione risorse](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [Portale classico](site-recovery-vmm-to-azure-classic.md)
> * [PowerShell - Classico](site-recovery-deploy-with-powershell.md)
>
>

## <a name="overview"></a>Panoramica
Azure Site Recovery favorisce strategia ripristino emergenza e continuità tooyour aziendale gestendo la replica, il failover e ripristino delle macchine virtuali in un numero di scenari di distribuzione. Per un elenco completo di distribuzione di scenari di vedere hello [Panoramica di Azure Site Recovery](site-recovery-overview.md).

Questo articolo illustra come attività comuni di toouse PowerShell tooautomate occorre tooperform per la configurazione di macchine virtuali di Azure Site Recovery tooreplicate Hyper-V nel servizio di archiviazione tooAzure cloud System Center VMM.

articolo Hello sono inclusi i prerequisiti per lo scenario di hello e Mostra è come tooset di un insieme di credenziali di Site Recovery, installa hello Provider di Azure Site Recovery nel server VMM di origine hello, registrare hello server nell'insieme di credenziali hello, aggiungere un account di archiviazione di Azure, installare hello Azure Agente di servizi di ripristino in server host Hyper-V, configurare le impostazioni di protezione per i cloud VMM che verranno applicati tooall protetto le macchine virtuali e quindi abilitare la protezione per le macchine virtuali. Completare test toomake failover hello che tutto funzioni come previsto.

Se si verificano problemi durante l'impostazione di questo scenario, è possibile pubblicare domande sul hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

> [!NOTE]
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.
>
>

## <a name="before-you-start"></a>Prima di iniziare
Assicurarsi che siano rispettati i prerequisiti seguenti:

### <a name="azure-prerequisites"></a>Prerequisiti di Azure
* È necessario un account [Microsoft Azure](https://azure.microsoft.com/) . È possibile iniziare con una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).
* È necessario un toostore replicati dati dell'account di archiviazione di Azure. account di Hello deve replica geografica abilitata. Dovrebbe essere nella stessa area dell'insieme di credenziali di Azure Site Recovery hello hello e associato hello stessa sottoscrizione. [Altre informazioni sull'Archiviazione di Azure](../storage/common/storage-introduction.md).
* È necessario assicurarsi che le macchine virtuali da tooprotect rispettino toomake [macchina virtuale di Azure prerequisiti](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

### <a name="vmm-prerequisites"></a>Prerequisiti di VMM
* È necessario un server VMM in esecuzione su System Center 2012 R2.
* È necessario almeno un cloud nel server VMM si desidera tooprotect hello. cloud Hello deve contenere:
  * Uno o più gruppi host VMM.
  * Uno o più cluster o server host Hyper-V in ogni gruppo host.
  * Uno o più macchine virtuali nel server Hyper-V di origine hello.

### <a name="hyper-v-prerequisites"></a>Prerequisiti di Hyper-V
* Hello Server host Hyper-V deve essere in esecuzione almeno **Windows Server 2012** con ruolo Hyper-V o **Microsoft Hyper-V Server 2012** e avere hello installati aggiornamenti più recenti.
* Se si esegue Hyper-V in un cluster, si noti che il gestore del cluster non viene creato automaticamente se viene usato un cluster basato su indirizzi IP statici. È necessario un gestore cluster hello tooconfigure manualmente. toodo questa operazione, in Server Manager > Gestione Cluster di Failover, connettersi toohello cluster, fare clic su **Configura ruolo** e selezionare **gestore Replica Hyper-V** in hello **selezionare il ruolo**schermata della procedura guidata disponibilità elevata hello.
* Qualsiasi server host Hyper-V o cluster di cui si desidera toomanage protezione deve essere incluso in un cloud VMM.

### <a name="network-mapping-prerequisites"></a>Prerequisiti di mapping di rete
Quando si proteggono macchine virtuali nella rete di Azure viene eseguito il mapping tra le reti VM nel server VMM di origine hello e seguente hello tooenable di reti di Azure di destinazione:

* Tutti i computer in cui eseguire il failover su hello stesso può connettersi tooeach altri, indipendentemente dal piano di ripristino si trovano in rete.
* Se un gateway di rete è configurato nella rete Azure di destinazione hello, macchine virtuali possono connettersi le macchine virtuali tooother locale.
* Se non si configura rete mapping solo le macchine virtuali che il failover hello stesso piano di ripristino saranno in grado di tooconnect tooeach altri dopo tooAzure di failover.

Se si desidera che il mapping di rete toodeploy, occorre seguente hello:

* Hello le macchine virtuali da tooprotect nel server VMM di origine hello deve essere una rete VM tooa connesso. La rete deve essere collegato tooa la rete logica associata al cloud hello.
* Le macchine virtuali toowhich replicata una rete di Azure possono connettersi dopo il failover. Selezionare la rete in fase di hello di failover. rete Hello devono trovarsi in hello stessa area la sottoscrizione di Azure Site Recovery.

### <a name="powershell-prerequisites"></a>Prerequisiti di PowerShell
Assicurarsi di disporre di Azure PowerShell pronto toogo. Se si sta già usando PowerShell, è necessario tooupgrade tooversion 0.8.10 o versione successiva. Per informazioni sull'impostazione di PowerShell, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azureps-cmdlets-docs). Dopo aver impostato e configurato PowerShell, è possibile visualizzare tutti i cmdlet disponibili di hello per servizio hello [qui](/powershell/azure/overview).

toolearn sui suggerimenti che consentono di utilizzare i cmdlet di hello, ad esempio come i valori dei parametri, input e output vengono in genere gestiti in Azure PowerShell, vedere [Introduzione ai cmdlet di Azure](/powershell/azure/get-started-azureps).

## <a name="step-1-set-hello-subscription"></a>Passaggio 1: Impostare una sottoscrizione di hello
In PowerShell, eseguire questi cmdlet:

```
$UserName = "<user@live.com>"
$Password = "<password>"
$AzureSubscriptionName = "prod_sub1"

$SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
$Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $securePassword
Add-AzureAccount -Credential $Cred;
$AzureSubscription = Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

```

Sostituire gli elementi di hello all'interno di hello "< >" con le informazioni specifiche.

## <a name="step-2-create-a-site-recovery-vault"></a>Passaggio 2: creare un insieme di credenziali di Ripristino sito
In PowerShell, sostituire gli elementi di hello all'interno di hello "< >" con le informazioni specifiche ed eseguire questi comandi:

```

$VaultName = "<testvault123>"
$VaultGeo  = "<Southeast Asia>"
$OutputPathForSettingsFile = "<c:\>"

```


```
New-AzureSiteRecoveryVault -Location $VaultGeo -Name $VaultName;
$vault = Get-AzureSiteRecoveryVault -Name $VaultName;

```

## <a name="step-3-generate-a-vault-registration-key"></a>Passaggio 3: generare una chiave di registrazione dell'insieme di credenziali
Generare una chiave di registrazione nell'insieme di credenziali hello. Dopo aver scaricato hello Provider di Azure Site Recovery e installarlo nel server VMM hello, si utilizzerà il server VMM di hello tooregister chiave nell'insieme di credenziali hello.

1. Ottenere file di impostazioni dell'insieme di credenziali hello e impostare il contesto di hello:

   ```

   $VaultName = "<testvault123>"
   $VaultGeo  = "<Southeast Asia>"
   $OutputPathForSettingsFile = "<c:\>"

   $VaultSetingsFile = Get-AzureSiteRecoveryVaultSettingsFile -Location $VaultGeo -Name $VaultName -Path $OutputPathForSettingsFile;

   ```
2. Imposta il contesto di insieme di credenziali di hello eseguendo hello seguenti comandi:

   ```

   $VaultSettingFilePath = $vaultSetingsFile.FilePath
   $VaultContext = Import-AzureSiteRecoveryVaultSettingsFile -Path $VaultSettingFilePath -ErrorAction Stop

   ```

## <a name="step-4-install-hello-azure-site-recovery-provider"></a>Passaggio 4: Installare il Provider di Azure Site Recovery hello
1. Nel computer VMM hello, creare una directory eseguendo hello comando seguente:

   ```

   pushd C:\ASR\

   ```
2. Estrarre il file hello utilizzando provider hello scaricato eseguendo hello comando seguente

   ```

   AzureSiteRecoveryProvider.exe /x:. /q

   ```
3. Installare il provider di hello utilizzando hello seguenti comandi:

   ```

   .\SetupDr.exe /i

   ```

   ```

   $installationRegPath = "hklm:\software\Microsoft\Microsoft System Center Virtual Machine Manager Server\DRAdapter"
   do
   {
     $isNotInstalled = $true;
     if(Test-Path $installationRegPath)
     {
         $isNotInstalled = $false;
     }
   }While($isNotInstalled)

   ```

   Attendere toofinish installazione hello.
4. Registrare server hello in hello insieme di credenziali hello comando seguente:

   ```

   $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
   pushd $BinPath
   $encryptionFilePath = "C:\temp\"
   .\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

   ```

## <a name="step-5-create-an-azure-storage-account"></a>Passaggio 5: creare un account di archiviazione di Azure
Se non si dispone di un account di archiviazione di Azure, è possibile creare un account di replica geografica abilitata eseguendo hello comando seguente:

```

$StorageAccountName = "teststorageacc1"
$StorageAccountGeo  = "Southeast Asia"

New-AzureStorageAccount -StorageAccountName $StorageAccountName -Label $StorageAccountName -Location $StorageAccountGeo;

```

Si noti che l'account di archiviazione hello deve essere nella stessa area geografica del servizio Azure Site Recovery hello hello e associato hello stessa sottoscrizione.

## <a name="step-6-install-hello-azure-recovery-services-agent"></a>Passaggio 6: Installare hello Azure Recovery Services Agent
Da hello portale di Azure, installare l'agente servizi di ripristino di Azure hello in ogni server host Hyper-V presenti nei cloud VMM hello desiderate tooprotect.

Eseguire hello comando seguente in tutti gli host VMM:

```

marsagentinstaller.exe /q /nu

```


## <a name="step-7-configure-cloud-protection-settings"></a>Passaggio 7: configurare le impostazioni di protezione del cloud
1. Creare un tooAzure profilo di protezione cloud eseguendo hello comando seguente:

   ```

   $ReplicationFrequencyInSeconds = "300";
   $ProfileResult = New-AzureSiteRecoveryProtectionProfileObject -ReplicationProvider HyperVReplica -RecoveryAzureSubscription $AzureSubscriptionName -RecoveryAzureStorageAccount $StorageAccountName -ReplicationFrequencyInSeconds     $ReplicationFrequencyInSeconds;

   ```
2. Ottenere un contenitore di protezione eseguendo hello seguenti comandi:

   ```

   $PrimaryCloud = "testcloud"
   $protectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $PrimaryCloud;

   ```
3. Avviare associazione hello del contenitore di protezione hello cloud hello:

   ```

   $associationJob = Start-AzureSiteRecoveryProtectionProfileAssociationJob -ProtectionProfile $profileResult -PrimaryProtectionContainer $protectionContainer;        

   ```
4. Al termine, il processo di hello eseguire hello comando seguente:

        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
        $isJobLeftForProcessing = $true;
        }


1. Dopo il processo di hello ha terminato l'elaborazione, eseguire hello comando seguente:

        Do
        {
        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        Write-Host "Job State:{0}, StateDescription:{1}" -f Job.State, $job.StateDescription;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
            $isJobLeftForProcessing = $true;
        }

        if($isJobLeftForProcessing)
        {
            Start-Sleep -Seconds 60
        }
        }While($isJobLeftForProcessing)



completamento hello toocheck dell'operazione di hello, seguire i passaggi hello [monitorare l'attività](#monitor).

## <a name="step-8-configure-network-mapping"></a>Passaggio 8: configurare il mapping di rete
Prima di iniziare il mapping di rete verificare che le macchine virtuali nel server VMM di origine hello rete VM tooa connesso. Inoltre, creare una o più rete virtuali di Azure. Si noti che più reti VM possono essere mappate tooa singola rete di Azure.

Si noti che se la rete di destinazione hello dispone di più subnet e una di queste subnet è hello stesso nome di subnet nella macchina virtuale di origine che hello si trova, quindi hello macchina virtuale di replica sarà connessa toothat subnet di destinazione dopo il failover. Se non è presente una subnet di destinazione con un nome corrispondente, macchina virtuale hello sarà toohello connessi prima subnet nella rete hello.

Hello primo comando Ottiene i server per insieme di credenziali di hello corrente Azure Site Recovery. comando Hello archivia i server di Microsoft Azure Site Recovery hello nella variabile di matrice hello $Servers.

    $Servers = Get-AzureSiteRecoveryServer


Hello secondo comando Recupera hello sito ripristino rete per il primo server di hello nella matrice hello $Servers. comando Hello archivia reti hello nella variabile di hello $Networks.

    $Networks = Get-AzureSiteRecoveryNetwork -Server $Servers[0]

Hello terzo comando recupera le sottoscrizioni di Azure tramite il cmdlet Get-AzureSubscription hello e il valore viene archiviato nella variabile hello $Subscriptions.

    $Subscriptions = Get-AzureSubscription



Hello quarto comando recupera le reti virtuali di Azure tramite il cmdlet Get-AzureVNetSite hello e tale valore nella variabile hello $AzureVmNetworks.

    $AzureVmNetworks = Get-AzureVNetSite



Hello finale cmdlet crea un mapping tra la rete primaria hello e di rete di macchina virtuale di Azure hello. cmdlet di Hello specifica rete primaria hello come primo elemento di hello di $Networks. cmdlet di Hello specifica una rete di macchina virtuale al primo elemento hello di $AzureVmNetworks utilizzando il relativo ID. comando Hello include l'ID sottoscrizione Azure.

    New-AzureSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureSubscriptionId $Subscriptions[0].SubscriptionId -AzureVMNetworkId $AzureVmNetworks[0].Id


## <a name="step-9-enable-protection-for-virtual-machines"></a>Passaggio 9: abilitare la protezione per le macchine virtuali
Dopo aver configurate correttamente i server, cloud e reti, è possibile abilitare la protezione per le macchine virtuali nel cloud hello. Si noti hello segue:

Le macchine virtuali devono soddisfare [i prerequisiti delle macchine virtuali di Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

per la macchina virtuale hello, è necessario impostare del sistema operativo di tooenable protezione hello e proprietà del disco del sistema operativo. Quando si crea una macchina virtuale in VMM utilizzando un modello di macchina virtuale è possibile impostare proprietà hello. È inoltre possibile impostare queste proprietà per le macchine virtuali esistenti in hello **generale** e **configurazione Hardware** schede delle proprietà di hello macchina virtuale. Se le proprietà non impostate in VMM sarà in grado di tooconfigure nel portale di Azure Site Recovery hello.

1. protezione tooenable, eseguire hello contenitore di protezione hello tooget comando seguente:

     $ProtectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $CloudName
2. Ottenere entità di protezione hello (VM) eseguendo hello comando seguente:

        $protectionEntity = Get-AzureSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer



1. Abilitare hello ripristino di emergenza per hello VM eseguendo hello comando seguente:

        $jobResult = Set-AzureSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity     -Protection Enable -Force



## <a name="test-your-deployment"></a>Testare la distribuzione
pianificare la distribuzione, è possibile eseguire un failover di test per una singola macchina virtuale o creare un piano di ripristino costituita da più macchine virtuali ed eseguire un failover di test per hello tootest. Il failover di test consente di simulare il meccanismo di failover e di ripristino in una rete isolata. Si noti che:

* Se si desidera tooconnect toohello macchina virtuale di Azure tramite Desktop remoto dopo il failover hello, abilitare connessione Desktop remoto sulla macchina virtuale hello prima di eseguire il failover di test hello.
* Dopo il failover, si utilizzerà una macchina di virtuale toohello pubblica del tooconnect indirizzo IP in Azure tramite Desktop remoto. Se si desidera toodo, assicurarsi che tutti i criteri che impediscono la connessione tooa virtual machine tramite un indirizzo pubblico dominio non è.

completamento hello toocheck dell'operazione di hello, seguire i passaggi hello [monitorare l'attività](#monitor).

### <a name="create-a-recovery-plan"></a>Creare un piano di ripristino
1. Creare un file XML come modello per il piano di ripristino utilizzando i seguenti dati hello e quindi salvarlo come "C:\RPTemplatePath.xml".
2. Modificare il nodo di RecoveryPlan hello Id, nome, PrimaryServerId e SecondaryServerId.
3. Modificare il nodo di ProtectionEntity hello PrimaryProtectionEntityId (vmid da VMM).
4. È possibile aggiungere ulteriori macchine virtuali mediante l'aggiunta di più nodi ProtectionEntity.

        <#
        <?xml version="1.0" encoding="utf-16"?>
        <RecoveryPlan Id="d0323b26-5be2-471b-addc-0a8742796610" Name="rp-test"     PrimaryServerId="9350a530-d5af-435b-9f2b-b941b5d9fcd5"     SecondaryServerId="21a9403c-6ec1-44f2-b744-b4e50b792387" Description=""     Version="V2014_07">
          <Actions />
          <ActionGroups>
            <ShutdownAllActionGroup Id="ShutdownAllActionGroup">
              <PreActionSequence />
              <PostActionSequence />
            </ShutdownAllActionGroup>
            <FailoverAllActionGroup Id="FailoverAllActionGroup">
              <PreActionSequence />
              <PostActionSequence />
            </FailoverAllActionGroup>
            <BootActionGroup Id="DefaultActionGroup">
              <PreActionSequence />
              <PostActionSequence />
              <ProtectionEntity PrimaryProtectionEntityId="d4c8ce92-a613-4c63-9b03-    cf163cc36ef8" />
            </BootActionGroup>
          </ActionGroups>
          <ActionGroupSequence>
            <ActionGroup Id="ShutdownAllActionGroup" ActionId="ShutdownAllActionGroup"     Before="FailoverAllActionGroup" />
            <ActionGroup Id="FailoverAllActionGroup" ActionId="FailoverAllActionGroup"     After="ShutdownAllActionGroup" Before="DefaultActionGroup" />
            <ActionGroup Id="DefaultActionGroup" ActionId="DefaultActionGroup" After="FailoverAllActionGroup"/>
          </ActionGroupSequence>
        </RecoveryPlan>
        #>



1. Inserire dati hello nel modello hello:

        $TemplatePath = "C:\RPTemplatePath.xml";



1. Creare hello RecoveryPlan:

        $RPCreationJob = New-AzureSiteRecoveryRecoveryPlan -File $TemplatePath -WaitForCompletion;

### <a name="run-a-test-failover"></a>Eseguire un failover di test
1. Ottenere l'oggetto RecoveryPlan hello eseguendo hello comando seguente:

     $RPObject = Get-AzureSiteRecoveryRecoveryPlan -Name $RPName;
2. Avviare il failover di test hello eseguendo hello comando seguente:

        $jobIDResult = Start-AzureSiteRecoveryTestFailoverJob -RecoveryPlan $RPObject -Direction PrimaryToRecovery;


## <a name=monitor></a> Monitorare l'attività
Utilizzare hello attività hello toomonitor di comandi seguenti. Si noti la presenza di toowait tra i processi per hello toofinish di elaborazione.

    Do
    {
            $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
            Write-Host "Job State:{0}, StateDescription:{1}" -f Job.State, $job.StateDescription;
            if($job -eq $null -or $job.StateDescription -ne "Completed")
            {
                $isJobLeftForProcessing = $true;
            }

        if($isJobLeftForProcessing)
            {
                Start-Sleep -Seconds 60
            }
    }While($isJobLeftForProcessing)



## <a name="next-steps"></a>Passaggi successivi
[Altre informazioni](/powershell/azure/overview) sui cmdlet PowerShell per Azure Site Recovery. </a>.
