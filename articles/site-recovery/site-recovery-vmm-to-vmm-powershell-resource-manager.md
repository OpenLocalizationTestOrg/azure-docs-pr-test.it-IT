---
title: le macchine virtuali Hyper-V nel sito secondario di VMM tooa con PowerShell (Gestione risorse di Azure) aaaReplicate | Documenti Microsoft
description: Viene descritto come replica tooorchestrate di Azure Site Recovery toodeploy, failover e il ripristino delle macchine virtuali Hyper-V in VMM cloud sito VMM secondario tooa tramite PowerShell, Gestione risorse)
services: site-recovery
documentationcenter: 
author: sujaytalasila
manager: rochakm
editor: raynew
ms.assetid: 9d38e9c3-217c-4e44-830c-575e9a4141f2
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: sutalasi
ms.openlocfilehash: a769dcc68d66c18b9dc47539071f4d0e0f1db70f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site-using-powershell-resource-manager"></a>Replicare le macchine virtuali Hyper-V in VMM cloud tooa sito VMM secondario tramite PowerShell, Gestione risorse)
> [!div class="op_single_selector"]
> * [Portale di Azure](site-recovery-vmm-to-vmm.md)
> * [Portale classico](site-recovery-vmm-to-vmm-classic.md)
> * [PowerShell - Gestione risorse](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

Benvenuti tooAzure Site Recovery. Se si desidera tooreplicate locale Hyper-V le macchine virtuali gestite nel sito secondario tooa cloud di System Center Virtual Machine Manager (VMM), usare questo articolo.

Questo articolo illustra in che modo toouse PowerShell tooautomate comuni attività è necessario tooperform quando si configura macchine virtuali di Azure Site Recovery tooreplicate Hyper-V nei cloud VMM di System Center VMM cloud tooSystem Center nel sito secondario.

articolo Hello sono inclusi i prerequisiti per scenario hello e Mostra

* Come tooset di un insieme di credenziali di servizi di ripristino
* Installare hello Provider di Azure Site Recovery nel server VMM di origine hello e server VMM di destinazione hello
* Registrare i server VMM hello nell'insieme di credenziali hello
* Configurare i criteri di replica per hello Cloud VMM. le impostazioni di replica Hello nei criteri hello saranno applicati tooall protetto le macchine virtuali
* Abilitare la protezione per le macchine virtuali hello.
* Test del failover delle macchine virtuali hello singolarmente o come parte del ripristino di un piano toomake che tutto funzioni come previsto.
* Eseguire un pianificato o un failover non pianificato di macchine virtuali, singolarmente o come parte di un toomake piano di ripristino che tutto funzioni come previsto.

Se si verificano problemi durante l'impostazione di questo scenario, è possibile pubblicare domande sul hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

> [!NOTE]
> Azure offre due diversi [modelli di distribuzione](../azure-resource-manager/resource-manager-deployment-model.md) per creare e usare le risorse: Azure Resource Manager e la distribuzione classica. Azure offre inoltre due portali: hello portale di Azure classico che supporta il modello di distribuzione classica hello e hello portale di Azure con il supporto per entrambi i modelli di distribuzione. Questo articolo descrive il modello di distribuzione di gestione risorse di hello.
>
>

## <a name="on-premises-prerequisites"></a>Prerequisiti locali
Ecco cosa è necessario in hello primario e secondario locale siti toodeploy questo scenario:

| **Prerequisiti** | **Dettagli** |
| --- | --- |
| **VMM** |È consigliabile che distribuire un server VMM nel sito primario di hello e un server VMM nel sito secondario hello.<br/><br/> È possibile anche [eseguire la replica tra cloud in un singolo server VMM](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment). toodo questo è necessario almeno due cloud configurati nei server VMM hello.<br/><br/> Server VMM devono essere in esecuzione almeno System Center 2012 SP1 con gli aggiornamenti più recenti di hello.<br/><br/> Ogni server VMM deve avere uno o più cloud configurati e tutte le aree è necessario impostare il profilo di capacità Hyper-V hello. <br/><br/>I cloud devono contenere uno o più gruppi host VMM.<br/><br/>Ulteriori informazioni sull'impostazione dei cloud VMM in [hello configurazione VMM cloud dell'infrastruttura](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric), e [procedura dettagliata: creazione di cloud privati con System Center 2012 SP1 VMM](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx).<br/><br/> I server VMM devono disporre di accesso a Internet. |
| **Hyper-V** |Server Hyper-V deve essere in esecuzione almeno Windows Server 2012 con il ruolo Hyper-V hello e avere hello installati aggiornamenti più recenti.<br/><br/> Il server Hyper-V deve contenere una o più macchine virtuali.<br/><br/>  Server host Hyper-V devono essere distribuiti nei gruppi host nei cloud VMM primario e secondario di hello.<br/><br/> Se si esegue Hyper-V in un cluster su Windows Server 2012 R2 è necessario installare l'[aggiornamento 2961977](https://support.microsoft.com/kb/2961977)<br/><br/> Se si esegue Hyper-V in un cluster basato su indirizzi IP statici in Windows Server 2012, il gestore del cluster non viene creato automaticamente. È necessario un gestore cluster hello tooconfigure manualmente. [Altre informazioni](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx). |
| **Provider** |Durante la distribuzione di Site Recovery hello Provider di Azure Site Recovery viene installato nel server VMM. Hello Provider comunica con il ripristino del sito tramite replica tooorchestrate HTTPS 443. La replica dei dati si verifica tra i server di Hyper-V primari e secondari di hello su hello LAN o una connessione VPN.<br/><br/> Hello Provider in esecuzione nel server VMM hello deve accedere URL toothese: *. c o m; *. accesscontrol.windows.net; *. backup.windowsazure.com; *. n e t; *. store.core.windows.net.<br/><br/> Inoltre consentire le comunicazioni di firewall da hello VMM server toohello [intervalli IP Data Center di Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653) e consentire il protocollo HTTPS (443) di hello. |

### <a name="network-mapping-prerequisites"></a>Prerequisiti di mapping di rete
Rete viene eseguito il mapping tra i server VMM primari e secondari di hello per le reti VM di VMM:

* Posizionare in modo ottimale le macchine virtuali di replica in host Hyper-V secondari dopo il failover.
* Connettere le reti VM di tooappropriate macchine virtuali di replica.
* Se non si configura rete mapping replica le macchine virtuali non saranno connesse tooany rete dopo il failover.
* Se si desidera tooset rete mapping durante il ripristino del sito distribuzione qui è ciò che è necessario:

  * Assicurarsi che le macchine virtuali di origine hello server host Hyper-V siano connesso tooa rete VM di VMM. La rete deve essere collegato tooa la rete logica associata al cloud hello.
  * Verificare che i cloud secondario hello che verrà utilizzato per il ripristino sia configurata una rete VM corrispondente. Rete VM deve essere collegato tooa la rete logica associata a cloud secondario hello.

Ulteriori informazioni sulla configurazione delle reti VMM in hello di sotto di articoli

* [Come tooconfigure reti logiche in VMM](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [Modalità VM tooconfigure reti e gateway in VMM](http://go.microsoft.com/fwlink/p/?LinkId=386308)

[Altre informazioni](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) sul funzionamento del mapping di rete.

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
1. Creare un gruppo di risorse di Azure Resource Manager, se non ne è già disponibile uno.

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. Creare un nuovo insieme di credenziali di servizi di ripristino e salvare hello creato l'oggetto insieme di credenziali di ripristino automatico di sistema in una variabile (verrà utilizzata in un secondo momento). È inoltre possibile recuperare hello ripristino automatico di sistema dell'insieme di credenziali post di creazione di un oggetto utilizzando il cmdlet Get-AzureRMRecoveryServicesVault hello:-

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-hello-recovery-services-vault-context"></a>Passaggio 3: Impostare il contesto di archivio di servizi di ripristino hello
1. Se si dispone di un insieme di credenziali già creato, eseguire hello di sotto dell'insieme di credenziali di comando tooget hello.

       $vault = Get-AzureRmRecoveryServicesVault -Name #vaultname
2. Impostare il contesto di insieme di credenziali hello eseguendo hello comando seguente.

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

## <a name="step-5-create-and-associate-a-replication-policy"></a>Passaggio 5: Creare e associare un criterio di replica
1. Creare un criterio di replica Hyper-V 2012 R2 eseguendo hello comando seguente:

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $RepProvider = HyperVReplica2012R2
        $Recoverypoints = 24                    #specify hello number of hours tooretain recovery pints
        $AppConsistentSnapshotFrequency = 4 #specify hello frequency (in hours) at which app consistent snapshots are taken
        $AuthMode = "Kerberos"  #options are "Kerberos" or "Certificate"
        $AuthPort = "8083"  #specify hello port number that will be used for replication traffic on Hyper-V hosts
        $InitialRepMethod = "Online" #options are "Online" or "Offline"

        $policyresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider $RepProvider -ReplicationFrequencyInSeconds $Replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours $AppConsistentSnapshotFrequency -Authentication $AuthMode -ReplicationPort $AuthPort -ReplicationMethod $InitialRepMethod

    > [!NOTE]
    > Hello cloud VMM può contenere host Hyper-V che eseguono versioni diverse di Windows Server (come indicato nei prerequisiti di Hyper-V hello), ma i criteri di replica hello sono versione del sistema operativo specifico. Se si dispone di diversi host in esecuzione in versioni diverse del sistema operativo, creare criteri di replica individuali per ogni tipo di versione del sistema operativo. Ad esempio: se si dispone di cinque host in esecuzione su Windows Server 2012 e tre su Windows Server 2012 R2, creare due criteri di replica, uno per ogni tipo di versione del sistema operativo.

1. Ottenere il contenitore di protezione primaria hello (Cloud VMM primario) e il contenitore di protezione recovery (ripristino di VMM Cloud) eseguendo hello seguenti comandi:

       $PrimaryCloud = "testprimarycloud"
       $primaryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  

       $RecoveryCloud = "testrecoverycloud"
       $recoveryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $RecoveryCloud;  
2. Recupero dei criteri di hello creato nel passaggio 1 con nome descrittivo di hello del criterio di hello

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. Avviare associazione hello del contenitore di protezione hello (Cloud VMM) con il criterio di replica hello:

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $primaryprotectionContainer -RecoveryProtectionContainer $recoveryprotectionContainer
4. Attendere hello criteri associazione processo toocomplete. È possibile verificare se il processo di hello è stata completata con hello seguente frammento di PowerShell.

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }

   Dopo il processo di hello ha terminato l'elaborazione, eseguire hello comando seguente:

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

completamento hello toocheck dell'operazione di hello, seguire i passaggi hello [monitorare l'attività](#monitor).

## <a name="step-6-configure-network-mapping"></a>Passaggio 6: Configurare il mapping di rete
1. Hello primo comando Ottiene i server per insieme di credenziali di hello corrente Azure Site Recovery. comando Hello archivia i server di Microsoft Azure Site Recovery hello nella variabile di matrice hello $Servers.

        $Servers = Get-AzureRmSiteRecoveryServer
2. Hello seguito comandi ottenere hello sito ripristino rete per server VMM di origine hello e hello destinazione VMM.

        $PrimaryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]        

        $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]

    > [!NOTE]
    > server VMM di origine Hello può essere hello prima o una matrice di hello secondo hello in un server. Controllare i nomi di hello del server VMM hello e recuperare le reti di hello in modo appropriato


1. Hello finale cmdlet crea un mapping tra la rete primaria hello e rete ripristino hello. cmdlet di Hello specifica rete primaria hello come primo elemento di hello della rete di ripristino $PrimaryNetworks e hello come primo elemento di hello di $RecoveryNetworks.

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $PrimaryNetworks[0] -RecoveryNetwork $RecoveryNetworks[0]

## <a name="step-7-configure-storage-mapping"></a>Passaggio 7: Configurare il mapping di archiviazione
1. Hello comando seguente ottiene l'elenco di hello di classificazioni di archiviazione nella variabile $storageclassifications.

        $storageclassifications = Get-AzureRmSiteRecoveryStorageClassification
2. Hello seguito comandi ottenere la classificazione di origine hello nella variabile $SourceClassificaion e la classificazione di destinazione nella variabile $TargetClassification.

        $SourceClassificaion = $storageclassifications[0]

        $TargetClassification = $storageclassifications[1]

    > [!NOTE]
    > le classificazioni di origine e destinazione Hello possono essere qualsiasi elemento nella matrice hello. Fare riferimento toohello output di hello seguito indice hello toofigure di comando di classificazioni di origine e di destinazione nella matrice $storageclassifications.

    > Get-AzureRmSiteRecoveryStorageClassification | Select-Object -Property FriendlyName, Id | Format-Table


1. Hello seguito cmdlet crea un mapping tra la classificazione di destinazione hello e classificazione di origine hello.

        New-AzureRmSiteRecoveryStorageClassificationMapping -PrimaryStorageClassification $SourceClassificaion -RecoveryStorageClassification $TargetClassification

## <a name="step-8-enable-protection-for-virtual-machines"></a>Passaggio 8: Abilitare la protezione per le macchine virtuali
Dopo che le reti, cloud e i server hello sono configurate correttamente, è possibile abilitare la protezione per le macchine virtuali nel cloud hello.

1. protezione tooenable, eseguire hello contenitore di protezione hello tooget comando seguente:

          $PrimaryProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloudName
2. Ottenere entità di protezione hello (VM) eseguendo hello comando seguente:

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $PrimaryProtectionContainer
3. Abilitare la replica per hello VM eseguendo hello comando seguente:

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable -Policy $policy

## <a name="test-your-deployment"></a>Testare la distribuzione
pianificare la distribuzione, è possibile eseguire un failover di test per una singola macchina virtuale o creare un piano di ripristino costituita da più macchine virtuali ed eseguire un failover di test per hello tootest. Il failover di test consente di simulare il meccanismo di failover e di ripristino in una rete isolata.

> [!NOTE]
> È possibile creare un piano di ripristino per l'applicazione nel portale di Azure.
>
>

completamento hello toocheck dell'operazione di hello, seguire i passaggi hello [monitorare l'attività](#monitor).

### <a name="run-a-test-failover"></a>Eseguire un failover di test
1. Eseguire hello seguito cmdlet tooget hello VM rete toowhich desiderato tootest failover le macchine virtuali.

       $Servers = Get-AzureRmSiteRecoveryServer
       $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]
2. Eseguire un failover di test di una macchina virtuale eseguendo hello seguenti:

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMName -ProtectionContainer $PrimaryprotectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -VMNetwork $RecoveryNetworks[1]
3. Eseguire un failover di test di un piano di ripristino eseguendo hello seguenti:

       $recoveryplanname = "test-recovery-plan"

       $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan -VMNetwork $RecoveryNetworks[1]

### <a name="run-a-planned-failover"></a>Eseguire un failover pianificato
1. Eseguire un failover pianificato di una macchina virtuale eseguendo hello seguenti:

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity
2. Eseguire un failover pianificato di un piano di ripristino eseguendo hello seguenti:

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan

### <a name="run-an-unplanned-failover"></a>Eseguire un failover non pianificato
1. Eseguire un failover non pianificato di una macchina virtuale eseguendo hello seguenti:

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

2. eseguire un failover non pianificato di un piano di ripristino eseguendo hello seguenti:

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

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
