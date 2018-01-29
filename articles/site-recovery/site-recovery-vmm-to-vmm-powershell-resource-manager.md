---
title: Eseguire la replica di macchine virtuali Hyper-V in VMM in un sito secondario con PowerShell (Azure Resource Manager) | Microsoft Docs
description: Questo articolo descrive come distribuire Azure Site Recovery per coordinare la replica, il failover e il ripristino di macchine virtuali Hyper-V in cloud VMM in un sito VMM secondario tramite PowerShell (Resource Manager).
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
ms.date: 10/19/2017
ms.author: sutalasi
ms.openlocfilehash: c978c2e31e775f56824d765491f6d7b73648b8ae
ms.sourcegitcommit: 76a3cbac40337ce88f41f9c21a388e21bbd9c13f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/25/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-to-a-secondary-vmm-site-using-powershell-resource-manager"></a>Eseguire la replica di macchine virtuali Hyper-V in cloud VMM in un sito VMM secondario usando PowerShell (Resource Manager)

Questo articolo illustra come usare PowerShell per automatizzare attività comuni quando si configura Azure Site Recovery per replicare le macchine virtuali Hyper-V nei cloud VMM di System Center verso cloud VMM di System Center in un sito secondario.



## <a name="on-premises-prerequisites"></a>Prerequisiti locali
Elementi necessari nel sito locale primario e in quello secondario per distribuire questo scenario:

| **Prerequisiti** | **Dettagli** |
| --- | --- |
| **VMM** |È consigliabile eseguire la distribuzione di un server VMM nel sito primario e di un server VMM nel sito secondario.<br/><br/> È anche possibile eseguire la replica tra cloud in un singolo server VMM. A tale scopo, sono necessari almeno due cloud configurati sul server VMM.<br/><br/> I server VMM devono eseguire almeno System Center 2012 SP1 con gli aggiornamenti più recenti.<br/><br/> In ogni server VMM devono essere configurati uno o più cloud e in tutti i cloud deve essere impostato il profilo di capacità Hyper-V. <br/><br/>I cloud devono contenere uno o più gruppi host VMM. I server VMM devono disporre di accesso a Internet. |
| **Hyper-V** |I server Hyper-V devono eseguire almeno Windows Server 2012 con ruolo Hyper-V e con gli ultimi aggiornamenti installati.<br/><br/> Il server Hyper-V deve contenere una o più macchine virtuali.<br/><br/>  I server host Hyper-V devono trovarsi nei gruppi host disponibili nei cloud VMM primario e secondario.<br/><br/> Se si esegue Hyper-V in un cluster su Windows Server 2012 R2 è necessario installare l'[aggiornamento 2961977](https://support.microsoft.com/kb/2961977)<br/><br/> Se si esegue Hyper-V in un cluster basato su indirizzi IP statici in Windows Server 2012, il gestore del cluster non viene creato automaticamente. Sarà necessario configurare manualmente il broker del cluster. [Altre informazioni](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx). |
| **Provider** |Durante la distribuzione di Site Recovery, installare il provider di Azure Site Recovery in server VMM. Il provider comunica con Site Recovery su HTTPS 443 per coordinare la replica. La replica dei dati viene eseguita tra il server Hyper-V primario e quello secondario attraverso la rete LAN o una connessione VPN.<br/><br/> Il provider in esecuzione nel server VMM deve poter accedere a questi URL: *.hypervrecoverymanager.windowsazure.com; *.accesscontrol.windows.net; *.backup.windowsazure.com; *.blob.core.windows.net; *.store.core.windows.net.<br/><br/> Consentire anche la comunicazione del firewall dai server VMM agli [intervalli IP dei data center di Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653) e il protocollo HTTPS (443). |

### <a name="network-mapping-prerequisites"></a>Prerequisiti di mapping di rete
Il mapping di rete esegue il mapping tra reti di macchine virtuali di VMM nei server VMM primario e secondario per eseguire le attività seguenti:

* Posizionare in modo ottimale le macchine virtuali di replica in host Hyper-V secondari dopo il failover.
* Connettere le macchine virtuali di replica alle reti di macchine virtuali appropriate.
* Se non si configura il mapping di rete, le macchine virtuali di replica non verranno connesse ad alcuna rete dopo il failover.
* Se si vuole configurare il mapping di rete durante la distribuzione di Site Recovery, è necessario:

  * Accertarsi che le macchine virtuali nel server host Hyper-V di origine siano connesse a una rete VM di VMM. È necessario che tale rete sia collegata a una rete logica associata al cloud.
  * Verificare che per il cloud secondario in cui verrà eseguito il ripristino sia configurata una rete VM corrispondente, collegata a una rete logica associata al cloud secondario.

Nei seguenti articoli vengono fornite altre informazioni sulla configurazione delle reti VMM

* [Come configurare le reti logiche in VMM](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [Come configurare reti VM e gateway in VMM](http://go.microsoft.com/fwlink/p/?LinkId=386308)


### <a name="powershell-prerequisites"></a>Prerequisiti di PowerShell
Assicurarsi che Azure PowerShell sia pronto all'uso. Se già si utilizza PowerShell, è necessario eseguire l'aggiornamento alla versione 0.8.10 o successiva. Per informazioni sulla configurazione di PowerShell, vedere [Come installare e configurare Azure PowerShell](/powershell/azureps-cmdlets-docs). Dopo avere impostato e configurato PowerShell, è possibile vedere tutti i cmdlet disponibili per il servizio [qui](/powershell/azure/overview).

Per informazioni sui suggerimenti che facilitano l'uso dei cmdlet, ad esempio i valori dei parametri, sugli input e sugli output che vengono in genere gestiti in Azure PowerShell, vedere [Iniziare a utilizzare i cmdlet di Azure](/powershell/azure/get-started-azureps).

## <a name="step-1-set-the-subscription"></a>Passaggio 1: impostare la sottoscrizione
1. Da Azure PowerShell accedere all'account di Azure con i cmdlet seguenti

        $UserName = "<user@live.com>"
        $Password = "<password>"
        $SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
        $Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $SecurePassword
        Login-AzureRmAccount #-Credential $Cred
2. Ottenere un elenco delle sottoscrizioni. Verranno elencati anche i valori subscriptionID per ogni sottoscrizione. Annotare il valore subscriptionID della sottoscrizione in cui si vuole creare l'insieme di credenziali dei Servizi di ripristino    

        Get-AzureRmSubscription
3. Configurare la sottoscrizione in cui deve essere creato l'insieme di credenziali dei Servizi di ripristino, indicando l'ID della sottoscrizione

        Set-AzureRmContext –SubscriptionID <subscriptionId>

## <a name="step-2-create-a-recovery-services-vault"></a>Passaggio 2: Creare l'insieme di credenziali di Servizi di ripristino
1. Creare un gruppo di risorse di Azure Resource Manager, se non ne è già disponibile uno.

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. Creare un nuovo insieme di credenziali di Servizi di ripristino e salvare l'oggetto insieme di credenziali di Servizi di ripristino creato in una variabile. Verrà usato in seguito. È anche possibile recuperare l'oggetto insieme di credenziali dopo la creazione usando il cmdlet Get-AzureRMRecoveryServicesVault:

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-the-recovery-services-vault-context"></a>Passaggio 3: Impostare il contesto dell’insieme di credenziali di Servizi di ripristino
1. Se è stato già creato un insieme di credenziali, eseguire il comando seguente per ottenere l'insieme di credenziali.

       $vault = Get-AzureRmRecoveryServicesVault -Name #vaultname
2. Impostare il contesto dell'insieme eseguendo il comando seguente.

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-install-the-azure-site-recovery-provider"></a>Passaggio 4: installare il provider di Azure Site Recovery
1. Nel computer VMM, creare una directory eseguendo il comando seguente:

       New-Item c:\ASR -type directory
2. Estrarre i file utilizzando il provider scaricato eseguendo il comando seguente:

       pushd C:\ASR\
       .\AzureSiteRecoveryProvider.exe /x:. /q
3. Installare il provider utilizzando i comandi seguenti:

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

   Attendere la fine dell'installazione.
4. Registrare il server nell'insieme di credenziali utilizzando il comando seguente:

       $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
       pushd $BinPath
       $encryptionFilePath = "C:\temp\".\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

## <a name="step-5-create-and-associate-a-replication-policy"></a>Passaggio 5: Creare e associare un criterio di replica
1. Creare un criterio di replica per Hyper-V 2012 R2 eseguendo il comando seguente:

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $RepProvider = HyperVReplica2012R2
        $Recoverypoints = 24                    #specify the number of hours to retain recovery pints
        $AppConsistentSnapshotFrequency = 4 #specify the frequency (in hours) at which app consistent snapshots are taken
        $AuthMode = "Kerberos"  #options are "Kerberos" or "Certificate"
        $AuthPort = "8083"  #specify the port number that will be used for replication traffic on Hyper-V hosts
        $InitialRepMethod = "Online" #options are "Online" or "Offline"

        $policyresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider $RepProvider -ReplicationFrequencyInSeconds $Replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours $AppConsistentSnapshotFrequency -Authentication $AuthMode -ReplicationPort $AuthPort -ReplicationMethod $InitialRepMethod

    > [!NOTE]
    > Il cloud VMM può contenere host Hyper-V che eseguono versioni diverse di Windows Server (come indicato nei prerequisiti di Hyper-V), ma i criteri di replica sono specifici della versione del sistema operativo. Se si dispone di diversi host in esecuzione in versioni diverse del sistema operativo, creare criteri di replica individuali per ogni tipo di versione del sistema operativo. Ad esempio, se sono disponibili cinque host in esecuzione su Windows Server 2012 e tre su Windows Server 2012 R2, creare due criteri di replica, uno per ogni tipo di versione del sistema operativo.

1. Ottenere il contenitore di protezione principale (cloud VMM primario) e un contenitore di protezione di ripristino (ripristino cloud VMM) eseguendo i comandi seguenti:

       $PrimaryCloud = "testprimarycloud"
       $primaryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  

       $RecoveryCloud = "testrecoverycloud"
       $recoveryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $RecoveryCloud;  
2. Recuperare il criterio creato nel passaggio 1 usando il nome intuitivo del criterio

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. Avviare l'associazione del contenitore di protezione (cloud VMM) al criterio di replica:

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $primaryprotectionContainer -RecoveryProtectionContainer $recoveryprotectionContainer
4. Attendere il completamento del processo di associazione dei criteri. È possibile verificare se il processo è stato completata tramite il seguente frammento di PowerShell.

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }

   Al termine del processo, eseguire il comando seguente:

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

Per verificare il completamento dell'operazione, attenersi alla procedura descritta in [Monitorare l'attività](#monitor).

## <a name="step-6-configure-network-mapping"></a>Passaggio 6: Configurare il mapping di rete
1. Il primo comando ottiene i server per l'insieme di credenziali corrente di Azure Site Recovery. Il comando archivia i server di Microsoft Azure Site Recovery nella variabile di matrice $Servers.

        $Servers = Get-AzureRmSiteRecoveryServer
2. I comandi seguenti consentono di ottenere la rete di Site Recovery per il server VMM di origine e il server VMM di destinazione.

        $PrimaryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]        

        $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]

    > [!NOTE]
    > Il server VMM di origine può essere il primo o il secondo nella matrice di server. Controllare i nomi dei server VMM e ottenere le reti in modo appropriato


1. Il cmdlet finale crea un mapping tra la rete primaria e la rete di ripristino. Il cmdlet specifica la rete primaria come primo elemento di $PrimaryNetworks e la rete di ripristino come primo elemento di $RecoveryNetworks.

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $PrimaryNetworks[0] -RecoveryNetwork $RecoveryNetworks[0]

## <a name="step-7-configure-storage-mapping"></a>Passaggio 7: Configurare il mapping di archiviazione
1. Il comando seguente ottiene l'elenco di classificazioni di archiviazione nella variabile $storageclassifications.

        $storageclassifications = Get-AzureRmSiteRecoveryStorageClassification
2. I comandi seguenti ottengono la classificazione di origine nella variabile $SourceClassificaion e la classificazione di destinazione nella variabile $TargetClassification.

        $SourceClassificaion = $storageclassifications[0]

        $TargetClassification = $storageclassifications[1]

    > [!NOTE]
    > Le classificazioni di origine e di destinazione possono essere qualsiasi elemento nella matrice. Fare riferimento all'output del comando seguente per individuare l'indice delle classificazioni di origine e di destinazione nella matrice $storageclassifications.

    > Get-AzureRmSiteRecoveryStorageClassification | Select-Object -Property FriendlyName, Id | Format-Table


1. Il cmdlet seguente crea un mapping tra la classificazione di origine e quella di destinazione.

        New-AzureRmSiteRecoveryStorageClassificationMapping -PrimaryStorageClassification $SourceClassificaion -RecoveryStorageClassification $TargetClassification

## <a name="step-8-enable-protection-for-virtual-machines"></a>Passaggio 8: Abilitare la protezione per le macchine virtuali
Dopo la configurazione corretta di server, cloud e reti, sarà possibile abilitare la protezione per le macchine virtuali sul cloud.

1. Per abilitare la protezione, eseguire il comando seguente per ottenere il contenitore di protezione:

          $PrimaryProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloudName
2. Ottenere l'entità di protezione (VM) eseguendo il comando seguente:

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $PrimaryProtectionContainer
3. Abilitare la replica per la macchina virtuale eseguendo il comando seguente:

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable -Policy $policy

## <a name="test-your-deployment"></a>Testare la distribuzione
Per testare la distribuzione è possibile eseguire un failover di test per una singola macchina virtuale oppure creare un piano di ripristino costituito da più macchine virtuali ed eseguire un failover di test per il piano. Il failover di test consente di simulare il meccanismo di failover e di ripristino in una rete isolata.

> [!NOTE]
> È possibile creare un piano di ripristino per l'applicazione nel portale di Azure.
>
>

Per verificare il completamento dell'operazione, attenersi alla procedura descritta in [Monitorare l'attività](#monitor).

### <a name="run-a-test-failover"></a>Eseguire un failover di test
1. Eseguire il seguente cmdlet per ottenere la rete VM su cui si desidera testare il failover delle macchine virtuali.

       $Servers = Get-AzureRmSiteRecoveryServer
       $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]
2. Eseguire un failover di test di una macchina virtuale eseguendo le operazioni seguenti:

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMName -ProtectionContainer $PrimaryprotectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -VMNetwork $RecoveryNetworks[1]
3. Eseguire un failover di test di un piano di ripristino eseguendo le operazioni seguenti:

       $recoveryplanname = "test-recovery-plan"

       $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan -VMNetwork $RecoveryNetworks[1]

### <a name="run-a-planned-failover"></a>Eseguire un failover pianificato
1. Eseguire un failover pianificato di una macchina virtuale eseguendo le operazioni seguenti:

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity
2. Eseguire un failover pianificato di un piano di ripristino eseguendo le operazioni seguenti:

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan

### <a name="run-an-unplanned-failover"></a>Eseguire un failover non pianificato
1. Eseguire un failover non pianificato di una macchina virtuale eseguendo le operazioni seguenti:

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

2. Eseguire un failover non pianificato di un piano di ripristino eseguendo le operazioni seguenti:

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

## <a name=monitor></a> Monitorare l'attività
Utilizzare i comandi seguenti per monitorare l'attività. Si noti che è necessario attendere l'esecuzione dei processi per il completamento dell'elaborazione.

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
