---
title: le macchine virtuali Hyper-V con PowerShell e Azure Resource Manager aaaReplicate | Documenti Microsoft
description: Automatizzare la replica di macchine virtuali Hyper-V tooAzure hello con Azure Site Recovery tramite PowerShell e Gestione risorse di Azure.
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhiag
editor: 
ms.assetid: 05e0d76e-c3f5-4845-8052-094019b6d102
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: 4fb15ce2e9ad54f1dd6f54ff769eb912aa4b0272
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-between-on-premises-hyper-v-virtual-machines-and-azure-by-using-powershell-and-azure-resource-manager"></a>Eseguire la replica tra macchine virtuali Hyper-V locali e Azure con PowerShell e Azure Resource Manager
> [!div class="op_single_selector"]
> * [Portale di Azure](site-recovery-hyper-v-site-to-azure.md)
> * [PowerShell - Gestione risorse](site-recovery-deploy-with-powershell-resource-manager.md)
> * [Portale classico](site-recovery-hyper-v-site-to-azure-classic.md)
>
>

## <a name="overview"></a>Panoramica
Azure Site Recovery contribuisce tooyour business emergenza e continuità strategia di ripristino gestendo la replica, il failover e ripristino delle macchine virtuali in un numero di scenari di distribuzione. Per un elenco completo degli scenari di distribuzione, vedere hello [Panoramica di Azure Site Recovery](site-recovery-overview.md).

Azure PowerShell è un modulo che fornisce i cmdlet toomanage Azure tramite Windows PowerShell. Può funzionare con due tipi di moduli: hello modulo di Azureprofile, o un modulo di gestione risorse di Azure hello.

I cmdlet di PowerShell per Site Recovery disponibili con Azure PowerShell per Azure Resource Manager consentono di proteggere e ripristinare i server in Azure.

Questo articolo viene descritto come Windows PowerShell, con Gestione risorse di Azure, toodeploy Site Recovery tooconfigure toouse e orchestrano tooAzure di protezione di server. esempio Hello utilizzato in questo articolo mostra come eseguire il failover, tooprotect e ripristinare le macchine virtuali in tooAzure un host Hyper-V, tramite Azure PowerShell con Gestione risorse di Azure.

> [!NOTE]
> Hello cmdlet PowerShell di ripristino del sito attualmente consentono di hello tooconfigure seguenti: un tooanother del sito di Virtual Machine Manager, un tooAzure sito Virtual Machine Manager e un tooAzure sito Hyper-V.
>
>

Non occorre toobe un toouse esperti di PowerShell in questo articolo, ma è necessario toounderstand hello concetti, ad esempio le sessioni, cmdlet e i moduli. Per altre informazioni su Windows PowerShell, vedere [Introduzione a Windows PowerShell](http://technet.microsoft.com/library/hh857337.aspx).

Altrei informazioni sono disponibili in [Uso di Azure PowerShell con Azure Resource Manager](../powershell-azure-resource-manager.md).

> [!NOTE]
> I partner Microsoft che fanno parte del programma di Provider di soluzioni Cloud (CSP) hello è possono configurare e gestire la protezione dei server dei clienti rispettivi CSP sottoscrizioni (tenant) tootheir clienti.
>
>

## <a name="before-you-start"></a>Prima di iniziare
Assicurarsi che siano rispettati i prerequisiti seguenti:

* Account [Microsoft Azure](https://azure.microsoft.com/) . È possibile iniziare con una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/). Inoltre, è possibile leggere le informazioni sui [prezzi di Azure Site Recovery Manager](https://azure.microsoft.com/pricing/details/site-recovery/).
* Azure PowerShell 1.0. Per informazioni su questa versione e come tooinstall, vedere [Azure PowerShell 1.0.](https://azure.microsoft.com/)
* Hello [AzureRM.SiteRecovery](https://www.powershellgallery.com/packages/AzureRM.SiteRecovery/) e [AzureRM.RecoveryServices](https://www.powershellgallery.com/packages/AzureRM.RecoveryServices/) moduli. È possibile ottenere versioni più recenti di hello di questi moduli da hello [PowerShell gallery](https://www.powershellgallery.com/)

Questo articolo illustra come toouse Azure Powershell con Gestione risorse di Azure tooconfigure e gestire la protezione dei server. esempio Hello utilizzato in questo articolo illustra come una macchina virtuale, in esecuzione in un host Hyper-V, tooAzure tooprotect. Hello seguenti prerequisiti è toothis specifico esempio. Per un set più completo di requisiti per hello vari scenari di ripristino del sito, consultare la documentazione del toohello riguardano toothat scenario.

* Host Hyper-V che esegue Windows Server 2012 R2 o Microsoft Hyper-V Server 2012 R2 contenente una o più macchine virtuali.
* Server Hyper-V connesso toohello Internet, direttamente o tramite un proxy.
* salve le macchine virtuali da tooprotect devono essere conformi ai [prerequisiti per le macchine virtuali](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

## <a name="step-1-sign-in-tooyour-azure-account"></a>Passaggio 1: Accedi tooyour account Azure
1. Aprire la console di PowerShell ed eseguire questo comando toosign in tooyour account Azure. cmdlet di Hello viene visualizzata una pagina web che richiederà le credenziali dell'account.

        Login-AzureRmAccount

    In alternativa, è possibile includere le credenziali dell'account come un parametro toohello `Login-AzureRmAccount` cmdlet utilizzando hello `-Credential` parametro.

    Nel caso di utilizzo per conto di un tenant di partner CSP, specificare come tenant, cliente hello utilizzando il nome di dominio primario tenantID o tenant.

        Login-AzureRmAccount -Tenant "fabrikam.com"
2. Un account può disporre di più sottoscrizioni, pertanto è necessario associare la sottoscrizione di hello da toouse con account hello.

        Select-AzureRmSubscription -SubscriptionName $SubscriptionName
3. Verificare che la sottoscrizione sia registrata toouse hello provider di Azure per servizi di ripristino e il ripristino del sito, utilizzando hello seguenti comandi:

   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices`
   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`

   Nell'output di hello di questi comandi, se hello **RegistrationState** è troppo**registrati**, è possibile procedere tooStep 2. In caso contrario, è consigliabile registrare provider mancante hello nella sottoscrizione.

   tooregister hello del provider di Azure per il ripristino del sito e i servizi di ripristino, eseguire hello seguenti comandi:

       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.SiteRecovery
       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.RecoveryServices

   Verificare che il provider di hello registrato correttamente utilizzando i seguenti comandi hello: `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices` e `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`.

## <a name="step-2-set-up-hello-recovery-services-vault"></a>Passaggio 2: Configurare hello che insieme di credenziali di servizi di ripristino
1. Creare un gruppo di risorse di gestione risorse di Azure in cui si crea l'insieme di credenziali hello oppure utilizzare un gruppo di risorse esistente. È possibile creare un nuovo gruppo di risorse utilizzando hello comando seguente:

        New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Geo  

    dove hello $ResourceGroupName variabile contiene il nome di hello hello del gruppo di risorse da toocreate e variabile hello $Geo contiene hello Azure area nella quale gruppo di risorse hello toocreate (ad esempio, "Brasile meridionale").

    È possibile ottenere un elenco di gruppi di risorse nella sottoscrizione tramite hello `Get-AzureRmResourceGroup` cmdlet.
2. Creare un nuovo insieme di credenziali di Servizi di ripristino di Azure, come segue:

        $vault = New-AzureRmRecoveryServicesVault -Name <string> -ResourceGroupName <string> -Location <string>

    È possibile recuperare un elenco di insiemi di credenziali esistenti utilizzando hello `Get-AzureRmRecoveryServicesVault` cmdlet.

> [!NOTE]
> Se si desiderano operazioni tooperform su insiemi di credenziali per il ripristino del sito creati tramite portale classico hello o modulo PowerShell di Azure Service Management hello, è possibile recuperare un elenco di tali archivi utilizzando hello `Get-AzureRmSiteRecoveryVault` cmdlet. Per tutte le nuove operazioni, occorre creare un nuovo insieme di credenziali di Servizi di ripristino. insiemi di credenziali di Site Recovery Hello creata in precedenza sono supportati, ma non dispone di funzionalità più recenti di hello.
>
>

## <a name="step-3-set-hello-recovery-services-vault-context"></a>Passaggio 3: Impostare hello contesto insieme di credenziali di servizi di ripristino
1. Imposta il contesto di insieme di credenziali di hello eseguendo hello comando seguente:

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-create-a-hyper-v-site-and-generate-a-new-vault-registration-key-for-hello-site"></a>Passaggio 4: Creare un sito Hyper-V e generare una nuova chiave di registrazione dell'insieme di credenziali per il sito hello.
1. Creare un nuovo sito Hyper-V, come segue:

        $sitename = "MySite"                #Specify site friendly name
        New-AzureRmSiteRecoverySite -Name $sitename

    Questo cmdlet consente di avviare un sito di ripristino del sito processo toocreate hello e restituisce un oggetto processo di ripristino del sito. Attendere toocomplete processo hello e verificare che il processo di hello è stata completata correttamente.

    È possibile recuperare l'oggetto processo hello e quindi controllare lo stato corrente di hello del processo di hello, tramite il cmdlet Get-AzureRmSiteRecoveryJob hello.
2. Generare e scaricare una chiave di registrazione per il sito di hello, come indicato di seguito:

        $SiteIdentifier = Get-AzureRmSiteRecoverySite -Name $sitename | Select -ExpandProperty SiteIdentifier
        Get-AzureRmRecoveryServicesVaultSettingsFile -Vault $vault -SiteIdentifier $SiteIdentifier -SiteFriendlyName $sitename -Path $Path

    Hello copia scaricato toohello chiave Hyper-V host. È necessario il sito toohello host di hello tooregister chiave hello Hyper-V.

## <a name="step-5-install-hello-azure-site-recovery-provider-and-azure-recovery-services-agent-on-your-hyper-v-host"></a>Passaggio 5: Installare il provider di Azure Site Recovery hello e agente di servizi di ripristino di Azure nell'host Hyper-V
1. Scaricare la versione più recente di hello del provider di hello dal programma di installazione hello [Microsoft](https://aka.ms/downloaddra).
2. Programma di installazione hello esecuzione sull'host Hyper-V e alla fine hello installazione hello continuare toohello passaggio di registrazione.
3. Quando richiesto, specificare hello scaricato chiave di registrazione del sito e completare la registrazione del sito toohello host Hyper-V di hello.
4. Verificare che ospitano hello Hyper-V sia toohello registrato tramite hello comando seguente:

        $server =  Get-AzureRmSiteRecoveryServer -FriendlyName $server-friendlyname

## <a name="step-6-create-a-replication-policy-and-associate-it-with-hello-protection-container"></a>Passaggio 6: Creare un criterio di replica e associarlo al contenitore di protezione hello
1. Creare un criterio di replica come segue:

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify hello number of recovery points
        $storageaccountID = Get-AzureRmStorageAccount -Name "mystorea" -ResourceGroupName "MyRG" | Select -ExpandProperty Id

        $PolicyResult = New-AzureRmSiteRecoveryPolicy -Name $PolicyName -ReplicationProvider “HyperVReplicaAzure” -ReplicationFrequencyInSeconds $ReplicationFrequencyInSeconds  -RecoveryPoints $Recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId $storageaccountID

    Controllo hello restituito tooensure processo di creazione dei criteri di replica hello ha esito positivo.

   > [!IMPORTANT]
   > Hello account di archiviazione specificato deve essere in hello stessa area Azure nell'insieme di credenziali di servizi di ripristino e deve essere abilitata la replica geografica.
   >
   > * Se hello specificato ripristino account di archiviazione è di tipo di archiviazione di Azure (versione classica), il failover di hello protetto macchine Ripristina hello macchina tooAzure IaaS (classico).
   > * Se hello specificato l'account di archiviazione di ripristino è di tipo di archiviazione di Azure (Azure Resource Manager), il failover di hello protetto macchine Ripristina hello macchina tooAzure IaaS (Gestione risorse di Azure).
   >
   >
2. Ottenere hello protezione contenitore toohello sito corrispondente, come indicato di seguito:

        $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer
3. Avviare l'associazione hello del contenitore di protezione hello con criteri di replica hello, come indicato di seguito:

     $Policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $PolicyName   $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy $Policy -PrimaryProtectionContainer $protectionContainer

   Attendere toocomplete processo di associazione hello e verificare che siano stati completati.

## <a name="step-7-enable-protection-for-virtual-machines"></a>Passaggio 7: Abilitare la protezione per le macchine virtuali
1. Ottenere hello protezione entità corrispondente toohello macchina virtuale che si desidera tooprotect, come indicato di seguito:

        $VMFriendlyName = "Fabrikam-app"                    #Name of hello VM
        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName
2. Iniziare a proteggere hello macchina virtuale, come indicato di seguito:

        $Ostype = "Windows"                                 # "Windows" or "Linux"
        $DRjob = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity -Policy $Policy -Protection Enable -RecoveryAzureStorageAccountId $storageaccountID  -OS $OStype -OSDiskName $protectionEntity.Disks[0].Name

   > [!IMPORTANT]
   > Hello account di archiviazione specificato deve essere in hello stessa area Azure nell'insieme di credenziali di servizi di ripristino e deve essere abilitata la replica geografica.
   >
   > * Se hello specificato ripristino account di archiviazione è di tipo di archiviazione di Azure (versione classica), il failover di hello protetto macchine Ripristina hello macchina tooAzure IaaS (classico).
   > * Se hello specificato l'account di archiviazione di ripristino è di tipo di archiviazione di Azure (Azure Resource Manager), il failover di hello protetto macchine Ripristina hello macchina tooAzure IaaS (Gestione risorse di Azure).
   >
   > Se hello macchina virtuale che si sta proteggendo ha più di un disco collegato tooit, specificare disco del sistema operativo hello utilizzando hello *OSDiskName* parametro.
   >
   >
3. Attendere hello macchine virtuali tooreach uno stato protetto dopo la replica iniziale hello. Questo può richiedere alcuni minuti, a seconda di fattori, ad esempio quantità hello di toobe dati replicati e hello tooAzure larghezza di banda disponibile a monte. lo stato del processo Hello e StateDescription vengono aggiornati come indicato di seguito, al momento hello VM raggiungere uno stato protetto.

        PS C:\> $DRjob = Get-AzureRmSiteRecoveryJob -Job $DRjob

        PS C:\> $DRjob | Select-Object -ExpandProperty State
        Succeeded

        PS C:\> $DRjob | Select-Object -ExpandProperty StateDescription
        Completed
4. Aggiornare le proprietà di ripristino, ad esempio hello dimensioni del ruolo VM e hello rete Azure tooattach hello del network interface card tooupon failover della macchina virtuale.

        PS C:\> $nw1 = Get-AzureRmVirtualNetwork -Name "FailoverNw" -ResourceGroupName "MyRG"

        PS C:\> $VMFriendlyName = "Fabrikam-App"

        PS C:\> $VM = Get-AzureRmSiteRecoveryVM -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName

        PS C:\> $UpdateJob = Set-AzureRmSiteRecoveryVM -VirtualMachine $VM -PrimaryNic $VM.NicDetailsList[0].NicId -RecoveryNetworkId $nw1.Id -RecoveryNicSubnetName $nw1.Subnets[0].Name

        PS C:\> $UpdateJob = Get-AzureRmSiteRecoveryJob -Job $UpdateJob

        PS C:\> $UpdateJob

        Name             : b8a647e0-2cb9-40d1-84c4-d0169919e2c5
        ID               : /Subscriptions/a731825f-4bf2-4f81-a611-c331b272206e/resourceGroups/MyRG/providers/Microsoft.RecoveryServices/vault
                           s/MyVault/replicationJobs/b8a647e0-2cb9-40d1-84c4-d0169919e2c5
        Type             : Microsoft.RecoveryServices/vaults/replicationJobs
        JobType          : UpdateVmProperties
        DisplayName      : Update hello virtual machine
        ClientRequestId  : 805a22a3-be86-441c-9da8-f32685673112-2015-12-10 17:55:51Z-P
        State            : Succeeded
        StateDescription : Completed
        StartTime        : 10-12-2015 17:55:53 +00:00
        EndTime          : 10-12-2015 17:55:54 +00:00
        TargetObjectId   : 289682c6-c5e6-42dc-a1d2-5f9621f78ae6
        TargetObjectType : ProtectionEntity
        TargetObjectName : Fabrikam-App
        AllowedActions   : {Restart}
        Tasks            : {UpdateVmPropertiesTask}
        Errors           : {}



## <a name="step-8-run-a-test-failover"></a>Passaggio 8: Eseguire un failover di test
1. Eseguire un processo di failover di test come segue:

        $nw = Get-AzureRmVirtualNetwork -Name "TestFailoverNw" -ResourceGroupName "MyRG" #Specify Azure vnet name and resource group

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMFriendlyName -ProtectionContainer $protectionContainer

        $TFjob = Start-AzureRmSiteRecoveryTestFailoverJob -ProtectionEntity $protectionEntity -Direction PrimaryToRecovery -AzureVMNetworkId $nw.Id
2. Verificare che il test hello che creazione macchina virtuale in Azure. (processo di failover di test hello viene sospeso, dopo la creazione di test hello VM in Azure. Hello del processo termina con la pulizia artefatti hello creato dopo il ripristino processo hello, come illustrato nel passaggio successivo hello.)
3. Hello completa test failover, come indicato di seguito:

        $TFjob = Resume-AzureRmSiteRecoveryJob -Job $TFjob

## <a name="next-steps"></a>Passaggi successivi
[Altre informazioni](https://msdn.microsoft.com/library/azure/mt637930.aspx) sui cmdlet PowerShell per Azure Site Recovery con Azure Resource Manager.
