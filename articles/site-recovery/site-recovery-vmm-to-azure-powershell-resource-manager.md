---
title: macchine virtuali aaaReplicate Hyper-V nei cloud VMM usando Azure Site Recovery e PowerShell di gestione risorse () | Documenti Microsoft
description: Replicare le macchine virtuali Hyper-V nei cloud VMM usando Azure Site Recovery e PowerShell
services: site-recovery
documentationcenter: 
author: Rajani-Janaki-Ram
manager: rochakm
editor: raynew
ms.assetid: 6ac509ad-5024-43d8-b621-d8fec019b9a9
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: rajanaki
ms.openlocfilehash: b0f641de4e10a600ead415ceb9bd488fb4d1659d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure-using-powershell-and-azure-resource-manager"></a>Replica delle macchine virtuali Hyper-V in VMM cloud tooAzure tramite PowerShell e Gestione risorse di Azure
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

articolo Hello sono inclusi i prerequisiti per scenario hello e Mostra

* Come tooset di un insieme di credenziali di servizi di ripristino
* Installare hello Provider di Azure Site Recovery nel server VMM di origine hello
* Registrare server hello nell'insieme di credenziali hello, aggiungere un account di archiviazione di Azure
* Installare l'agente di servizi di ripristino di Azure hello nei server host Hyper-V
* Configurare le impostazioni di protezione per i cloud VMM, che verrà applicato tooall protetto le macchine virtuali
* Abilitare la protezione di queste macchine virtuali
* Test toomake failover hello che tutto funzioni come previsto.

Se si verificano problemi durante l'impostazione di questo scenario, è possibile pubblicare domande sul hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

> [!NOTE]
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo di modello di distribuzione di gestione risorse di hello.
>
>

## <a name="before-you-start"></a>Prima di iniziare
Assicurarsi che siano rispettati i prerequisiti seguenti:

### <a name="azure-prerequisites"></a>Prerequisiti di Azure
* È necessario un account [Microsoft Azure](https://azure.microsoft.com/) . Se non si ha un account, creare un [account gratuito](https://azure.microsoft.com/free). Inoltre, per ulteriori informazioni hello [dei prezzi di Azure Site Recovery Manager](https://azure.microsoft.com/pricing/details/site-recovery/).
* Se si sta tentando di out scenario di hello replica tooa CSP sottoscrizione, è necessario un abbonamento di CSP. Ulteriori informazioni sul programma CSP hello in [come tooenroll nel programma CSP hello](https://msdn.microsoft.com/library/partnercenter/mt156995.aspx).
* È necessario un tooAzure di Azure v2 (Resource Manager) di archiviazione account toostore dati replicati. account di Hello deve replica geografica abilitata. Deve essere in hello stessa area hello servizio Azure Site Recovery e può essere associata a hello stessa sottoscrizione o hello CSP. toolearn più sulla configurazione di archiviazione di Azure, vedere hello [tooMicrosoft introduzione di archiviazione di Azure](../storage/common/storage-introduction.md) per riferimento.
* È necessario assicurarsi che le macchine virtuali da tooprotect rispettino hello toomake [macchina virtuale di Azure prerequisiti](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

> [!NOTE]
> Attualmente è possibile eseguire tramite Powershell solo le operazioni a livello di VM. Il supporto per le operazioni a livello di piano di ripristino sarà presto disponibile.  Per il momento, si è limitati tooperforming fail-passaggi solo a un livello di granularità 'protected VM' e non a livello di un piano di ripristino.
>
>

### <a name="vmm-prerequisites"></a>Prerequisiti di VMM
* È necessario un server VMM in esecuzione su System Center 2012 R2.
* Nei server VMM contenenti macchine virtuali desiderate tooprotect deve essere in esecuzione hello Provider di Azure Site Recovery. Viene installato durante la distribuzione di Azure Site Recovery hello.
* È necessario almeno un cloud nel server VMM si desidera tooprotect hello. cloud Hello deve contenere:
  * Uno o più gruppi host VMM.
  * Uno o più cluster o server host Hyper-V in ogni gruppo host.
  * Uno o più macchine virtuali nel server Hyper-V di origine hello.
* Per altre informazioni sulla configurazione dei cloud VMM:
  * Ulteriori informazioni sui cloud privati di VMM in [novità del Cloud privato con System Center 2012 R2 VMM](http://go.microsoft.com/fwlink/?LinkId=324952) e [cloud VMM 2012 e hello](http://go.microsoft.com/fwlink/?LinkId=324956).
  * Informazioni su [hello configurazione VMM cloud dell'infrastruttura](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)
  * Dopo avere definito gli elementi dell'infrastruttura cloud, leggere le informazioni su come creare i cloud privati in [Creazione di un cloud privato in VMM](http://go.microsoft.com/fwlink/p/?LinkId=324953) e [Procedura dettagliata: creazione di cloud privati con System Center 2012 SP1 VMM](http://go.microsoft.com/fwlink/p/?LinkId=324954).

### <a name="hyper-v-prerequisites"></a>Prerequisiti di Hyper-V
* Hello Server host Hyper-V deve essere in esecuzione almeno **Windows Server 2012** con ruolo Hyper-V o **Microsoft Hyper-V Server 2012** e avere hello installati aggiornamenti più recenti.
* Se si esegue Hyper-V in un cluster, si noti che il gestore del cluster non viene creato automaticamente se viene usato un cluster basato su indirizzi IP statici. È necessario un gestore cluster hello tooconfigure manualmente. Ad
* Per istruzioni, vedere [come gestore di Replica Hyper-V tooConfigure](http://blogs.technet.com/b/haroldwong/archive/2013/03/27/server-virtualization-series-hyper-v-replica-broker-explained-part-15-of-20-by-yung-chou.aspx).
* Qualsiasi server host Hyper-V o cluster di cui si desidera toomanage protezione deve essere incluso in un cloud VMM.

### <a name="network-mapping-prerequisites"></a>Prerequisiti di mapping di rete
Quando si proteggono macchine virtuali in Azure, viene eseguito il mapping di rete di hello reti di macchine virtuali hello nel server VMM di hello origine e destinazione reti Azure tooenable hello seguenti:

* Tutti i computer in cui eseguire il failover su hello stesso può connettersi tooeach altri, indipendentemente dal piano di ripristino si trovano in rete.
* Se un gateway di rete è configurato nella rete Azure di destinazione hello, macchine virtuali possono connettersi le macchine virtuali tooother locale.
* Se non si configura il mapping di rete, hello solo macchine virtuali che il failover hello stesso piano di ripristino saranno in grado di tooconnect tooeach altri dopo tooAzure di failover.

Se si desidera che il mapping di rete toodeploy, occorre seguente hello:

* Hello le macchine virtuali da tooprotect nel server VMM di origine hello deve essere una rete VM tooa connesso. La rete deve essere collegato tooa la rete logica associata al cloud hello.
* Le macchine virtuali toowhich replicata una rete di Azure possono connettersi dopo il failover. Selezionare la rete in fase di hello del failover. rete Hello devono trovarsi in hello stessa area la sottoscrizione di Azure Site Recovery.

Altre informazioni sul mapping di rete sono disponibili negli articoli seguenti:

* [Come tooconfigure reti logiche in VMM](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [Modalità VM tooconfigure reti e gateway in VMM](http://go.microsoft.com/fwlink/p/?LinkId=386308)
* [Come tooconfigure e monitorare reti virtuali in Azure](https://azure.microsoft.com/documentation/services/virtual-network/)

### <a name="powershell-prerequisites"></a>Prerequisiti di PowerShell
Assicurarsi di disporre di Azure PowerShell pronto toogo. Se si sta già usando PowerShell, è necessario tooupgrade tooversion 0.8.10 o versione successiva. Per informazioni sull'impostazione di PowerShell, vedere hello [tooinstall della Guida e configurare Azure PowerShell](/powershell/azureps-cmdlets-docs). Dopo aver impostato e configurato PowerShell, è possibile visualizzare tutti i cmdlet disponibili di hello per servizio hello [qui](/powershell/azure/overview).

toolearn sui suggerimenti che consentono di utilizzare i cmdlet di hello, ad esempio come i valori dei parametri, input e output vengono in genere gestiti in Azure PowerShell, vedere hello [Guida introduttiva ai cmdlet di Azure tooget](/powershell/azure/get-started-azureps).

## <a name="step-1-set-hello-subscription"></a>Passaggio 1: Impostare una sottoscrizione di hello
1. Da Azure powershell, account di accesso tooyour account di Azure: hello seguente cmdlet utilizzando

        $UserName = "<user@live.com>"
        $Password = "<password>"
        $SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
        $Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $SecurePassword
        Login-AzureRmAccount #-Credential $Cred
2. Ottenere un elenco delle sottoscrizioni. Questo ID sottoscrizione hello elencherà anche per ognuna delle sottoscrizioni hello. Annotare l'ID sottoscrizione hello di sottoscrizione hello in cui si desidera l'insieme di credenziali toocreate hello recovery services

        Get-AzureRmSubscription
3. Impostare hello sottoscrizione in cui hello credenziali di servizi di ripristino sono toobe creato da citare hello ID di sottoscrizione

        Set-AzureRmContext –SubscriptionID <subscriptionId>

## <a name="step-2-create-a-recovery-services-vault"></a>Passaggio 2: Creare l'insieme di credenziali di Servizi di ripristino
1. Creare un gruppo di risorse di Azure Resource Manager, qualora non ce ne sia già uno disponibile

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. Creare un nuovo insieme di credenziali di servizi di ripristino e salvare hello creato l'oggetto insieme di credenziali di ripristino automatico di sistema in una variabile (verrà utilizzata in un secondo momento). È inoltre possibile recuperare hello ripristino automatico di sistema dell'insieme di credenziali post di creazione di un oggetto utilizzando il cmdlet Get-AzureRMRecoveryServicesVault hello:-

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-hello-recovery-services-vault-context"></a>Passaggio 3: Impostare il contesto di archivio di servizi di ripristino hello

Impostare il contesto di insieme di credenziali hello eseguendo hello comando seguente.

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-install-hello-azure-site-recovery-provider"></a>Passaggio 4: Installare il Provider di Azure Site Recovery hello
1. Nel computer VMM hello, creare una directory eseguendo hello comando seguente:

       New-Item c:\ASR -type directory
2. Estrarre il file hello utilizzando provider hello scaricato eseguendo hello comando seguente

       pushd C:\ASR\
       .\AzureSiteRecoveryProvider.exe /x:. /q
3. Installare il provider di hello utilizzando hello seguenti comandi:

       .\SetupDr.exe /i
       $installationRegPath = "hklm:\software\Microsoft\Microsoft System Center Virtual Machine Manager Server\DRAdapter"
       do
       {
         $isNotInstalled = $true;
         if(Test-Path $installationRegPath)
         {
           $isNotInstalled = $false;
         }
       }While($isNotInstalled)

   Attendere toofinish installazione hello.
4. Registrare server hello in hello insieme di credenziali hello comando seguente:

       $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
       pushd $BinPath
       $encryptionFilePath = "C:\temp\".\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

## <a name="step-5-create-an-azure-storage-account"></a>Passaggio 5: creare un account di archiviazione di Azure

Se non si dispone di un account di archiviazione di Azure, creare un account di replica geografica abilitata in hello stessa area geografica di hello insieme di credenziali eseguendo hello comando seguente:

        $StorageAccountName = "teststorageacc1"    #StorageAccountname
        $StorageAccountGeo  = "Southeast Asia"     
        $ResourceGroupName =  “myRG”             #ResourceGroupName
        $RecoveryStorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Type “StandardGRS” -Location $StorageAccountGeo

Si noti che l'account di archiviazione hello deve essere nella stessa area geografica del servizio Azure Site Recovery hello hello e associato hello stessa sottoscrizione.

## <a name="step-6-install-hello-azure-recovery-services-agent"></a>Passaggio 6: Installare hello Azure Recovery Services Agent
1. Scaricare l'agente di servizi di ripristino di Azure hello in [http://aka.ms/latestmarsagent](http://aka.ms/latestmarsagent) e installazione su ogni server host Hyper-V disponibile in VMM hello cloud che si desidera tooprotect.
2. Eseguire hello comando seguente in tutti gli host VMM:

       marsagentinstaller.exe /q /nu

## <a name="step-7-configure-cloud-protection-settings"></a>Passaggio 7: configurare le impostazioni di protezione del cloud
1. Creare un tooAzure di criteri di replica eseguendo hello comando seguente:

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify hello number of recovery points

        $policryresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider HyperVReplicaAzure -ReplicationFrequencyInSeconds $replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId "/subscriptions/q1345667/resourceGroups/test/providers/Microsoft.Storage/storageAccounts/teststorageacc1"

1. Ottenere un contenitore di protezione eseguendo hello seguenti comandi:

       $PrimaryCloud = "testcloud"
       $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  
2. Ottenere hello criteri dettagli tooa variabile utilizzando processo hello che è stato creato e ricordare il nome di criterio descrittivo hello:

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. Avviare associazione hello del contenitore di protezione hello con criteri di replica hello:

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $protectionContainer  
4. Al termine, il processo di hello eseguire hello comando seguente:

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }
5. Dopo il processo di hello ha terminato l'elaborazione, eseguire hello comando seguente:

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

completamento hello toocheck dell'operazione di hello, seguire i passaggi hello [monitorare l'attività](#monitor).

## <a name="step-8-configure-network-mapping"></a>Passaggio 8: configurare il mapping di rete
Prima di iniziare il mapping di rete verificare che le macchine virtuali nel server VMM di origine hello rete VM tooa connesso. Inoltre, creare una o più rete virtuali di Azure.

Altre informazioni sulle modalità di rete tramite Gestione risorse di Azure e PowerShell, in toocreate un virtuale [creare una rete virtuale con una connessione VPN site-to-site tramite Gestione risorse di Azure e PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)

Si noti che più reti di macchine virtuali possono essere mappate tooa singola rete di Azure. Se la rete di destinazione hello dispone di più subnet e una di queste subnet è hello stesso nome di subnet nella macchina virtuale di origine che hello si trova, quindi hello macchina virtuale di replica sarà connessa toothat subnet di destinazione dopo il failover. Se non è presente alcuna subnet di destinazione con un nome corrispondente, macchina virtuale hello sarà toohello connessi prima subnet nella rete hello.

1. Hello primo comando Ottiene i server per insieme di credenziali di hello corrente Azure Site Recovery. comando Hello archivia i server di Microsoft Azure Site Recovery hello nella variabile di matrice hello $Servers.

        $Servers = Get-AzureRmSiteRecoveryServer
2. Hello secondo comando Recupera hello sito ripristino rete per il primo server di hello nella matrice hello $Servers. comando Hello archivia reti hello nella variabile di hello $Networks.

        $Networks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]

1. Hello terzo comando recupera le reti virtuali di Azure e quindi tale valore nella variabile hello $AzureVmNetworks.

        $AzureVmNetworks =  Get-AzureRmVirtualNetwork
2. Hello finale cmdlet crea un mapping tra la rete primaria hello e di rete di macchina virtuale di Azure hello. cmdlet di Hello specifica rete primaria hello come primo elemento di hello di $Networks. cmdlet di Hello specifica una rete di macchina virtuale al primo elemento hello di $AzureVmNetworks.

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureVMNetworkId $AzureVmNetworks[0]

## <a name="step-9-enable-protection-for-virtual-machines"></a>Passaggio 9: abilitare la protezione per le macchine virtuali
Dopo che le reti, cloud e i server hello sono configurate correttamente, è possibile abilitare la protezione per le macchine virtuali nel cloud hello.

 Si noti hello segue:

* Le macchine virtuali devono essere conformi ai requisiti di Azure. Archiviare queste [prerequisiti e supporto](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) nella Guida alla pianificazione di hello.
* per la macchina virtuale hello, è necessario impostare tooenable protezione, sistema operativo hello e proprietà del disco del sistema operativo. Quando si crea una macchina virtuale in VMM utilizzando un modello di macchina virtuale è possibile impostare proprietà hello. È inoltre possibile impostare queste proprietà per le macchine virtuali esistenti in hello **generale** e **configurazione Hardware** schede delle proprietà di hello macchina virtuale. Se le proprietà non impostate in VMM sarà in grado di tooconfigure nel portale di Azure Site Recovery hello.

1. protezione tooenable, eseguire hello contenitore di protezione hello tooget comando seguente:

          $ProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $CloudName
2. Ottenere entità di protezione hello (VM) eseguendo hello comando seguente:

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $protectionContainer
3. Abilitare hello ripristino di emergenza per hello VM eseguendo hello comando seguente:

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable –Force -Policy $policy -RecoveryAzureStorageAccountId  $storageID "/subscriptions/217653172865hcvkchgvd/resourceGroups/rajanirgps/providers/Microsoft.Storage/storageAccounts/teststorageacc1

## <a name="test-your-deployment"></a>Testare la distribuzione
tootest la distribuzione è possibile eseguire un test di failover per una singola macchina virtuale, o creare un piano di ripristino costituita da più macchine virtuali ed eseguire un test di failover per il piano di hello. Il failover di test consente di simulare il meccanismo di failover e di ripristino in una rete isolata. Si noti che:

* Se si desidera tooconnect toohello macchina virtuale di Azure tramite Desktop remoto dopo il failover hello, abilitare connessione Desktop remoto sulla macchina virtuale hello prima di eseguire il failover di test hello.
* Dopo il failover, si utilizzerà una macchina di virtuale toohello pubblica del tooconnect indirizzo IP in Azure tramite Desktop remoto. Se si desidera toodo, assicurarsi che tutti i criteri che impediscono la connessione tooa virtual machine tramite un indirizzo pubblico dominio non è.

completamento hello toocheck dell'operazione di hello, seguire i passaggi hello [monitorare l'attività](#monitor).

### <a name="run-a-test-failover"></a>Eseguire un failover di test
- Avviare il failover di test hello eseguendo hello comando seguente:

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-a-planned-failover"></a>Eseguire un failover pianificato
- Avviare il failover pianificato hello eseguendo hello comando seguente:

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-an-unplanned-failover"></a>Eseguire un failover non pianificato
- Avviare hello failover non pianificato eseguendo hello comando seguente:

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

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
[Altre informazioni](/powershell/module/azurerm.recoveryservices.backup/#recovery) su Azure Site Recovery con i cmdlet PowerShell per Azure Resource Manager.
