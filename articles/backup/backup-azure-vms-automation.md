---
title: aaaDeploy e gestire i backup per le macchine virtuali distribuite di gestione risorse mediante PowerShell | Documenti Microsoft
description: Utilizzare PowerShell toodeploy e gestire i backup in Azure per macchine virtuali distribuite di gestione risorse
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 68606e4f-536d-4eac-9f80-8a198ea94d52
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/28/2017
ms.author: markgal;trinadhk
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 486fb3ae1902403fe6bf303df57244b76677ab17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azurermrecoveryservicesbackup-cmdlets-tooback-up-virtual-machines"></a>Utilizzare AzureRM.RecoveryServices.Backup cmdlet tooback backup di macchine virtuali
> [!div class="op_single_selector"]
> * [Gestione risorse](backup-azure-vms-automation.md)
> * [Classico](backup-azure-vms-classic-automation.md)
>
>

Questo articolo illustra come tooback i cmdlet di Azure PowerShell toouse backup e ripristinare una macchina virtuale di Azure (VM) da servizi di ripristino di un insieme di credenziali. Un insieme di credenziali di servizi di ripristino è una risorsa di gestione risorse di Azure ed è utilizzato tooprotect dati e risorse in servizi di Backup di Azure e Azure Site Recovery. È possibile utilizzare un tooprotect insieme di credenziali di servizi di ripristino distribuito Service Manager di Azure le macchine virtuali e macchine virtuali distribuite di gestione risorse di Azure.

> [!NOTE]
> Azure offre due modelli di distribuzione per creare e usare le risorse: [Resource Manager e distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md). In questo articolo è per l'utilizzo con macchine virtuali create utilizzando il modello di gestione risorse hello.
>
>

In questo articolo illustra utilizzando PowerShell tooprotect una macchina virtuale e ripristino di dati da un punto di ripristino.

## <a name="concepts"></a>Concetti
Se non si ha familiarità con il servizio di Backup di Azure, per una panoramica del servizio di hello, hello estrarre [che cos'è Azure Backup?](backup-introduction-to-azure-backup.md) Prima di iniziare, assicurarsi che riguardano essentials hello su hello prerequisiti necessari toowork con Backup di Azure e hello limitazioni di hello VM soluzione di backup corrente.

toouse PowerShell in modo efficace, si tratta di toounderstand necessario hello gerarchia di oggetti e da dove toostart.

![Gerarchia di oggetti dei servizi di ripristino](./media/backup-azure-vms-arm-automation/recovery-services-object-hierarchy.png)

hello tooview AzureRm.RecoveryServices.Backup Guida di riferimento, vedere hello [Backup di Azure - cmdlet di servizi di ripristino](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup) in hello libreria di Azure.

## <a name="setup-and-registration"></a>Installazione e registrazione
toobegin:

1. [Scaricare hello la versione più recente di PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) (hello versione minima richiesta è: 1.4.0)
2. Trovare i cmdlet di PowerShell di Azure Backup hello disponibili digitando hello comando seguente:

```
PS C:\> Get-Command *azurermrecoveryservices*

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Backup-AzureRmRecoveryServicesBackupItem           1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Disable-AzureRmRecoveryServicesBackupProtection    1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Enable-AzureRmRecoveryServicesBackupProtection     1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupContainer         1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupItem              1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupJob               1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupJobDetails        1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupManagementServer  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupProperties        1.4.0      AzureRM.RecoveryServices
Cmdlet          Get-AzureRmRecoveryServicesBackupProtectionPolicy  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRMRecoveryServicesBackupRecoveryPoint     1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupRetentionPolic... 1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupSchedulePolicy... 1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesVault                   1.4.0      AzureRM.RecoveryServices
Cmdlet          Get-AzureRmRecoveryServicesVaultSettingsFile       1.4.0      AzureRM.RecoveryServices
Cmdlet          New-AzureRmRecoveryServicesBackupProtectionPolicy  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          New-AzureRmRecoveryServicesVault                   1.4.0      AzureRM.RecoveryServices
Cmdlet          Remove-AzureRmRecoveryServicesProtectionPolicy     1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Remove-AzureRmRecoveryServicesVault                1.4.0      AzureRM.RecoveryServices
Cmdlet          Restore-AzureRMRecoveryServicesBackupItem          1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Set-AzureRmRecoveryServicesBackupProperties        1.4.0      AzureRM.RecoveryServices
Cmdlet          Set-AzureRmRecoveryServicesBackupProtectionPolicy  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Set-AzureRmRecoveryServicesVaultContext            1.4.0      AzureRM.RecoveryServices
Cmdlet          Stop-AzureRmRecoveryServicesBackupJob              1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Unregister-AzureRmRecoveryServicesBackupContainer  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Unregister-AzureRmRecoveryServicesBackupManagem... 1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Wait-AzureRmRecoveryServicesBackupJob              1.4.0      AzureRM.RecoveryServices.Backup
```


con PowerShell, è possibile automatizzare Hello seguenti attività:

* Creare un insieme di credenziali di Servizi di ripristino
* Eseguire il backup delle VM di Azure
* Attivare un processo di backup
* Monitorare un processo di backup
* Ripristinare una macchina virtuale di Azure

## <a name="create-a-recovery-services-vault"></a>Creare un insieme di credenziali di Servizi di ripristino
Hello alla procedura seguente per facilitare la creazione di un insieme di credenziali di servizi di ripristino. Un insieme di credenziali dei servizi di ripristino è diverso da un insieme di credenziali di backup.

1. Se si utilizza Azure Backup per hello prima volta, è necessario utilizzare hello  **[registro AzureRmResourceProvider](http://docs.microsoft.com/powershell/module/azurerm.resources/register-azurermresourceprovider)**  provider di servizi di ripristino di Azure di cmdlet tooregister hello con la sottoscrizione.

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. Hello insieme di credenziali di servizi di ripristino è una risorsa di gestione delle risorse, pertanto è necessario tooplace all'interno di un gruppo di risorse. È possibile utilizzare un gruppo di risorse esistente o creare un gruppo di risorse con hello  **[New AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup)**  cmdlet. Quando si crea un gruppo di risorse, specificare nome hello e il percorso per il gruppo di risorse hello.  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. Hello utilizzare  **[New AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault)**  hello toocreate cmdlet dell'insieme di credenziali di servizi di ripristino. Assicurarsi che toospecify hello stesso percorso per l'insieme di credenziali hello utilizzata per il gruppo di risorse hello.

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. Specificare il tipo di hello di toouse di ridondanza di archiviazione; è possibile utilizzare [archiviazione con ridondanza locale (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) o [archiviazione con ridondanza geografica (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage). Hello riportato di seguito hello - BackupStorageRedundancy per testvault impostazione tooGeoRedundant.

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testvault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -Vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

   > [!TIP]
   > Molti cmdlet di Azure Backup richiede l'oggetto insieme di credenziali di servizi di ripristino hello come input. Per questo motivo, è utile toostore hello servizi di ripristino di Backup dell'insieme di credenziali oggetto in una variabile.
   >
   >

## <a name="view-hello-vaults-in-a-subscription"></a>Visualizza gli insiemi di credenziali hello in una sottoscrizione
Utilizzare  **[Get AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/get-azurermrecoveryservicesvault)**  elenco hello tooview di tutti gli insiemi di credenziali nella sottoscrizione corrente hello. È possibile utilizzare questo toocheck di comando che è stato creato un nuovo insieme di credenziali o toosee hello gli insiemi di credenziali disponibili nella sottoscrizione hello.

Eseguire hello tooview di comando, Get-AzureRmRecoveryServicesVault, tutti gli insiemi di credenziali nella sottoscrizione hello. Hello riportato di seguito informazioni hello visualizzate per ogni insieme di credenziali.

```
PS C:\> Get-AzureRmRecoveryServicesVault
Name              : Contoso-vault
ID                : /subscriptions/1234
Type              : Microsoft.RecoveryServices/vaults
Location          : WestUS
ResourceGroupName : Contoso-docs-rg
SubscriptionId    : 1234-567f-8910-abc
Properties        : Microsoft.Azure.Commands.RecoveryServices.ARSVaultProperties
```


## <a name="back-up-azure-vms"></a>Eseguire il backup delle VM di Azure
Utilizzare un tooprotect insieme di credenziali di servizi di ripristino le macchine virtuali. Prima di applicare la protezione di hello, impostare il contesto di insieme di credenziali hello (tipo hello dei dati protetti nell'insieme di credenziali hello) e verificare i criteri di protezione hello. criteri di protezione Hello sono pianificazione hello quando esegue i processi di backup hello e il periodo di conservazione di ogni snapshot di backup.

### <a name="set-vault-context"></a>Impostazione del contesto dell'insieme di credenziali
Prima di abilitare la protezione per una macchina virtuale, utilizzare  **[Set AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)**  contesto di tooset hello insieme di credenziali. Dopo aver impostato il contesto di insieme di credenziali hello, si applica cmdlet successivi tooall. esempio Hello Imposta contesto di insieme di credenziali hello per insieme di credenziali hello *testvault*.

```
PS C:\> Get-AzureRmRecoveryServicesVault -Name "testvault" | Set-AzureRmRecoveryServicesVaultContext
```

### <a name="create-a-protection-policy"></a>Creare i criteri di protezione
Quando si crea un insieme di credenziali di Servizi di ripristino, questo è dotato di protezione predefinita e criteri di conservazione. criteri di protezione predefinito Hello avvia un processo di backup ogni giorno a un'ora specificata. criteri di conservazione predefiniti Hello mantiene il punto di ripristino giornaliero hello per 30 giorni. È possibile utilizzare predefinito hello tooquickly criteri proteggere la macchina virtuale e modificare il criterio di hello in un secondo momento con diversi dettagli.

Utilizzare  **[Get AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupprotectionpolicy)**  criteri di protezione hello tooview nell'insieme di credenziali hello. È possibile utilizzare questo tooget cmdlet criteri specifici o criteri di hello tooview associata a un tipo di carico di lavoro. Hello di esempio seguente ottiene i criteri per il tipo di carico di lavoro, AzureVM.

```
PS C:\> Get-AzureRmRecoveryServicesBackupProtectionPolicy -WorkloadType "AzureVM"
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
DefaultPolicy        AzureVM            AzureVM              4/14/2016 5:00:00 PM
```

> [!NOTE]
> fuso orario di Hello del campo BackupTime hello in PowerShell è UTC. Tuttavia, se l'ora del backup hello viene visualizzato nel portale di Azure hello, hello è fuso orario locale tooyour adattata.
>
>

I criteri di protezione del backup sono associati almeno a un criterio di conservazione. I criteri di conservazione definiscono per quanto tempo un punto di recupero viene mantenuto prima dell'eliminazione. Utilizzare  **[Get AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupretentionpolicyobject)**  criteri di conservazione predefiniti tooview hello.  Analogamente è possibile utilizzare  **[Get AzureRmRecoveryServicesBackupSchedulePolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupschedulepolicyobject)**  tooobtain hello pianificazione criterio. Hello  **[New AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)**  cmdlet crea un oggetto PowerShell che contiene informazioni sui criteri di backup. Hello gli oggetti Criteri di conservazione e pianificazione vengono utilizzati come input toohello  **[New AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)**  cmdlet. Hello esempio archivia il criterio di pianificazione hello e criteri di conservazione hello nelle variabili. esempio Hello utilizza tali parametri di hello toodefine di variabili durante la creazione di un criterio di protezione, *NewPolicy*.

```
PS C:\> $schPol = Get-AzureRmRecoveryServicesBackupSchedulePolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> New-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy" -WorkloadType "AzureVM" -RetentionPolicy $retPol -SchedulePolicy $schPol
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
NewPolicy           AzureVM            AzureVM              4/24/2016 1:30:00 AM
```


### <a name="enable-protection"></a>Abilitare la protezione
Dopo aver definito i criteri di protezione backup hello, è comunque necessario abilitare i criteri di hello per un elemento. Utilizzare  **[Enable AzureRmRecoveryServicesBackupProtection](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/enable-azurermrecoveryservicesbackupprotection)**  tooenable protezione. Abilitazione della protezione, sono necessari due oggetti - elemento hello e criteri di hello. Dopo aver associato all'insieme di credenziali hello criteri hello, flusso di lavoro backup hello viene attivato in fase di hello è definito nella pianificazione dei criteri hello.

Hello seguendo l'esempio Abilita protezione per elemento hello, V2VM, applicando i criteri di hello, NewPolicy. protezione di hello tooenable nelle macchine virtuali di gestione risorse non crittografati

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

protezione hello tooenable crittografati macchine virtuali (crittografate utilizzando BEK e KEK), è necessario toogive hello Azure Backup autorizzazione tooread chiavi e segreti dall'insieme di credenziali chiave.

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToKeys backup,get,list -PermissionsToSecrets get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

protezione hello tooenable crittografati macchine virtuali (crittografate utilizzando solo BEK), è necessario toogive hello Azure Backup service autorizzazione tooread i segreti dall'insieme di credenziali chiave.

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToSecrets backup,get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

> [!NOTE]
> Se si utilizza il cloud di Azure per enti pubblici hello, quindi utilizzare hello valore ff281ffe-705c-4f53-9f37-a40e6f2c68f3 per il parametro hello **- ServicePrincipalName** in [Set-AzureRmKeyVaultAccessPolicy](https://docs.microsoft.com/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) cmdlet .
>
>

Macchine virtuali classiche

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V1VM" -ServiceName "ServiceName1"
```

### <a name="modify-a-protection-policy"></a>Modificare i criteri di protezione
criteri di protezione hello toomodify, utilizzare [Set AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/set-azurermrecoveryservicesbackupprotectionpolicy) oggetti SchedulePolicy o RetentionPolicy di hello toomodify.

Hello esempio seguente modifica hello ripristino punto memorizzazione too365 giorni.

```
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol.DailySchedule.DurationCountInDays = 365
PS C:\> $pol= Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Set-AzureRmRecoveryServicesBackupProtectionPolicy -Policy $pol  -RetentionPolicy $RetPol
```

## <a name="trigger-a-backup"></a>Attivare un backup
È possibile utilizzare  **[Backup AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/backup-azurermrecoveryservicesbackupitem)**  tootrigger un processo di backup. In caso di backup iniziale hello, è un backup completo. I backup successivi saranno incrementali. Toouse assicurarsi di essere  **[Set AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)**  contesto insieme di credenziali di hello tooset prima attivazione hello processo di backup. Hello di esempio seguente si presuppone che il contesto dell'insieme di credenziali è stato impostato.

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer -ContainerType "AzureVM" -Status "Registered" -FriendlyName "V2VM"
PS C:\> $item = Get-AzureRmRecoveryServicesBackupItem -Container $namedContainer -WorkloadType "AzureVM"
PS C:\> $job = Backup-AzureRmRecoveryServicesBackupItem -Item $item
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM              Backup               InProgress            4/23/2016 5:00:30 PM                       cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

> [!NOTE]
> fuso orario di Hello dei campi di StartTime ed EndTime hello in PowerShell è UTC. Tuttavia, se hello ora viene visualizzata nel portale di Azure hello, hello è fuso orario locale tooyour adattata.
>
>

## <a name="monitoring-a-backup-job"></a>Monitoraggio di un processo di backup
È possibile monitorare operazioni a esecuzione prolungata, ad esempio i processi di backup, senza utilizzare hello portale di Azure. stato hello tooget di un processo in corso, utilizzare hello  **[Get AzureRmRecoveryservicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjob)**  cmdlet. Questo cmdlet Ottiene i processi di backup per un insieme di credenziali specifico hello e tale insieme di credenziali è specificato nel contesto dell'insieme di credenziali di hello. Hello seguente esempio ottiene hello stato di un processo in corso sotto forma di matrice e archivia lo stato di hello nella variabile di hello $joblist.

```
PS C:\> $joblist = Get-AzureRmRecoveryservicesBackupJob –Status "InProgress"
PS C:\> $joblist[0]
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM             Backup               InProgress            4/23/2016 5:00:30 PM           cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

Anziché il polling di questi processi per il completamento, che è necessario codice aggiuntivo - utilizzare hello  **[attesa AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)**  cmdlet. Questo cmdlet sospende l'esecuzione di hello finché non viene completato il processo di hello o hello specificato viene raggiunto il valore di timeout.

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $joblist[0] -Timeout 43200
```

## <a name="restore-an-azure-vm"></a>Ripristinare una macchina virtuale di Azure
È presente una differenza fondamentale tra hello il ripristino di una macchina virtuale utilizzando hello portale di Azure e il ripristino di una macchina virtuale usando PowerShell. Con PowerShell, l'operazione di ripristino hello è stata completata una volta creati i dischi hello e informazioni di configurazione da punto di ripristino hello.

> [!NOTE]
> operazione di ripristino Hello non crea una macchina virtuale.
>
>

toocreate una macchina virtuale dal disco, vedere la sezione hello, [hello crea macchina virtuale da dischi stored](backup-azure-vms-automation.md#create-a-vm-from-stored-disks). di seguito sono riportati i passaggi di base di Hello toorestore una macchina virtuale di Azure:

* Selezionare hello VM
* Scegliere un punto di ripristino
* Ripristinare i dischi hello
* Creare VM hello da dischi stored

Hello figura seguente illustra la gerarchia di oggetti hello da hello RecoveryServicesVault toohello BackupRecoveryPoint verso il basso.

![Gerarchia di oggetti dei servizi di ripristino con BackupContainer](./media/backup-azure-vms-arm-automation/backuprecoverypoint-only.png)

toorestore dati di backup, identificare l'elemento backup hello e punto di ripristino hello che contiene i dati in un momento hello. Hello utilizzare  **[ripristino AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)**  cmdlet toorestore dati hello insieme di credenziali di account del cliente toohello.

### <a name="select-hello-vm"></a>Selezionare hello VM
tooget hello PowerShell oggetto che identifica hello destra eseguire il backup elemento, iniziare dal contenitore hello nell'insieme di credenziali hello e proseguite verso il basso la gerarchia di oggetti hello. contenitore di hello tooselect che rappresenta una macchina virtuale, utilizzare hello hello  **[Get AzureRmRecoveryServicesBackupContainer](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)**  cmdlet e inoltrare tramite pipe che toohello  **[ Get-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)**  cmdlet.

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer  -ContainerType "AzureVM" –Status "Registered" -FriendlyName "V2VM"
PS C:\> $backupitem = Get-AzureRmRecoveryServicesBackupItem –Container $namedContainer  –WorkloadType "AzureVM"
```

### <a name="choose-a-recovery-point"></a>Scegliere un punto di ripristino
Hello utilizzare  **[Get AzureRmRecoveryServicesBackupRecoveryPoint](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)**  toolist cmdlet punti di ripristino per backup dell'elemento hello. Scegliere quindi toorestore punto di ripristino hello. Se si è certi che toouse punto di ripristino, è una buona norma toochoose hello RecoveryPointType più recente = punto AppConsistent nell'elenco di hello.

In hello lo script seguente, hello variabile, **$rp**, è una matrice di punti di ripristino per hello selezionato backup dell'elemento, da hello ultimi sette giorni. Matrice di Hello viene ordinato in ordine inverso di tempo con punto di ripristino più recente di hello in corrispondenza dell'indice 0. Utilizzare l'indicizzazione di un punto di ripristino hello toopick standard matrice di PowerShell. Nell'esempio hello $rp [0] seleziona il punto di ripristino più recente hello.

```
PS C:\> $startDate = (Get-Date).AddDays(-7)
PS C:\> $endDate = Get-Date
PS C:\> $rp = Get-AzureRmRecoveryServicesBackupRecoveryPoint -Item $backupitem -StartDate $startdate.ToUniversalTime() -EndDate $enddate.ToUniversalTime()
PS C:\> $rp[0]
RecoveryPointAdditionalInfo :
SourceVMStorageType         : NormalStorage
Name                        : 15260861925810
ItemName                    : VM;iaasvmcontainer;RGName1;V2VM
RecoveryPointId             : /subscriptions/XX/resourceGroups/ RGName1/providers/Microsoft.RecoveryServices/vaults/testvault/backupFabrics/Azure/protectionContainers/IaasVMContainer;iaasvmcontainer;RGName1;V2VM/protectedItems/VM;iaasvmcontainer; RGName1;V2VM/recoveryPoints/15260861925810
RecoveryPointType           : AppConsistent
RecoveryPointTime           : 4/23/2016 5:02:04 PM
WorkloadType                : AzureVM
ContainerName               : IaasVMContainer;iaasvmcontainer; RGName1;V2VM
ContainerType               : AzureVM
BackupManagementType        : AzureVM
```



### <a name="restore-hello-disks"></a>Ripristinare i dischi hello
Hello utilizzare  **[ripristino AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)**  toorestore cmdlet dati dell'elemento di backup e configurazione tooa punto di ripristino. Dopo aver identificato un punto di ripristino, utilizzarlo come valore di hello per hello **- RecoveryPoint** parametro. Nel codice di esempio precedente hello, **$rp [0]** stato toouse punto di ripristino hello. Nel seguente esempio di codice, hello **$rp [0]** è toouse punto di ripristino hello per ripristinare il disco hello.

i dischi hello toorestore e informazioni di configurazione:

```
PS C:\> $restorejob = Restore-AzureRmRecoveryServicesBackupItem -RecoveryPoint $rp[0] -StorageAccountName "DestAccount" -StorageAccountResourceGroupName "DestRG"
PS C:\> $restorejob
WorkloadName     Operation          Status               StartTime                 EndTime            JobID
------------     ---------          ------               ---------                 -------          ----------
V2VM              Restore           InProgress           4/23/2016 5:00:30 PM                        cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

Hello utilizzare  **[attesa AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)**  toowait cmdlet per toocomplete processo di ripristino hello.

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $restorejob -Timeout 43200
```

Una volta completato il processo di ripristino hello, utilizzare hello  **[Get AzureRmRecoveryServicesBackupJobDetails](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjobdetails)**  dettagli hello tooget di cmdlet di hello operazione di ripristino. proprietà JobDetails Hello è hello toorebuild necessari di hello informazioni macchina virtuale.

```
PS C:\> $restorejob = Get-AzureRmRecoveryServicesBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmRecoveryServicesBackupJobDetails -Job $restorejob
```

Dopo aver ripristinato i dischi di hello, andare hello di toocreate successiva sezione toohello macchina virtuale.

## <a name="create-a-vm-from-restored-disks"></a>Creare una macchina virtuale da dischi ripristinati
Dopo aver ripristinato i dischi di hello, utilizzare toocreate questi passaggi e configurare la macchina virtuale hello dal disco.

> [!NOTE]
> toocreate crittografati macchine virtuali da dischi ripristinati, il ruolo di Azure deve disporre dell'autorizzazione tooperform hello action **Microsoft.KeyVault/vaults/deploy/action**. Se il ruolo non dispone di questa autorizzazione, crearne uno personalizzato con questa azione. Per altre informazioni, vedere [Ruoli personalizzati nel Controllo degli accessi in base al ruolo di Azure](../active-directory/role-based-access-control-custom-roles.md).
>
>

1. Hello query ripristinato proprietà del disco per i dettagli dei processi hello.

  ```
  PS C:\> $properties = $details.properties
  PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
  PS C:\> $containerName = $properties["Config Blob Container Name"]
  PS C:\> $blobName = $properties["Config Blob Name"]
  ```

2. Impostare il contesto di archiviazione di Azure hello e ripristinare i file di configurazione JSON hello.

    ```
    PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName "testvault"
    PS C:\> $destination_path = "C:\vmconfig.json"
    PS C:\> Get-AzureStorageBlobContent -Container $containerName -Blob $blobName -Destination $destination_path
    PS C:\> $obj = ((Get-Content -Path $destination_path -Raw -Encoding Unicode)).TrimEnd([char]0x00) | ConvertFrom-Json
    ```

3. Utilizzare configurazione di macchina virtuale di hello JSON configuration file toocreate hello.

    ```
   PS C:\> $vm = New-AzureRmVMConfig -VMSize $obj.'properties.hardwareProfile'.vmSize -VMName "testrestore"
    ```

4. Collegare un disco del sistema operativo hello e i dischi dati. A seconda della configurazione di hello delle macchine virtuali, fare clic su hello collegamento pertinente tooview rispettivi cmdlet: 
    - [Macchine virtuali non gestiti, non crittografato](#non-managed-non-encrypted-vms)
    - [Macchine virtuali non gestiti, crittografate (solo BEK)](#non-managed-encrypted-vms-bek-only)
    - [Macchine virtuali non gestiti, crittografate (BEK e KEK)](#non-managed-encrypted-vms-bek-and-kek)
    - [Macchine virtuali gestite e non crittografati](#managed-non-encrypted-vms)
    - [Macchine virtuali gestite, crittografate (BEK e KEK)](#managed-encrypted-vms-bek-and-kek)
    
    #### <a name="non-managed-non-encrypted-vms"></a>Macchine virtuali non gestite, non crittografate

    Utilizzare seguente esempio per le macchine virtuali non gestiti, non crittografato hello.

    ```
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.'properties.StorageProfile'.osDisk.vhd.Uri -CreateOption "Attach"
    PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.'properties.StorageProfile'.OsDisk.OsType
    PS C:\> foreach($dd in $obj.'properties.StorageProfile'.DataDisks)
    {
    $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.vhd.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption "Attach"
    }
    ```

    #### <a name="non-managed-encrypted-vms-bek-only"></a>Macchine virtuali non gestite, crittografate (solo con BEK)

    Per macchine virtuali non gestiti, crittografate (crittografate utilizzando solo BEK), l'insieme di credenziali a chiave segreta toohello toorestore hello è necessario prima di collegare i dischi. Per ulteriori informazioni, vedere l'articolo hello [ripristinare una macchina virtuale crittografata da un punto di ripristino di Backup di Azure](backup-azure-restore-key-secret.md). Hello seguente esempio viene illustrata la modalità di tooattach del sistema operativo e i dischi di dati per le macchine virtuali di crittografia.

    ```
    PS C:\> $dekUrl = "https://ContosoKeyVault.vault.azure.net:443/secrets/ContosoSecret007/xx000000xx0849999f3xx30000003163"
    PS C:\> $keyVaultId = "/subscriptions/abcdedf007-4xyz-1a2b-0000-12a2b345675c/resourceGroups/ContosoRG108/providers/Microsoft.KeyVault/vaults/ContosoKeyVault"
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.'properties.storageProfile'.osDisk.vhd.uri -DiskEncryptionKeyUrl $dekUrl -DiskEncryptionKeyVaultId $keyVaultId -CreateOption "Attach" -Windows
    PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.'properties.storageProfile'.osDisk.osType
    PS C:\> foreach($dd in $obj.'properties.storageProfile'.dataDisks)
     {
     $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.vhd.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption "Attach"
     }
    ```

    #### <a name="non-managed-encrypted-vms-bek-and-kek"></a>Macchine virtuali non gestite, crittografate (con BEK e KEK)

    Per macchine virtuali non gestiti, crittografate (crittografate utilizzando BEK e KEK), è necessario toorestore hello chiave e il segreto toohello insieme di credenziali chiave prima di collegare i dischi. Per ulteriori informazioni, vedere l'articolo hello [ripristinare una macchina virtuale crittografata da un punto di ripristino di Backup di Azure](backup-azure-restore-key-secret.md). Hello seguente esempio viene illustrata la modalità di tooattach del sistema operativo e i dischi di dati per le macchine virtuali di crittografia.

    ```
    PS C:\> $dekUrl = "https://ContosoKeyVault.vault.azure.net:443/secrets/ContosoSecret007/xx000000xx0849999f3xx30000003163"
    PS C:\> $kekUrl = "https://ContosoKeyVault.vault.azure.net:443/keys/ContosoKey007/x9xxx00000x0000x9b9949999xx0x006"
    PS C:\> $keyVaultId = "/subscriptions/abcdedf007-4xyz-1a2b-0000-12a2b345675c/resourceGroups/ContosoRG108/providers/Microsoft.KeyVault/vaults/ContosoKeyVault"
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.'properties.storageProfile'.osDisk.vhd.uri -DiskEncryptionKeyUrl $dekUrl -DiskEncryptionKeyVaultId $keyVaultId -KeyEncryptionKeyUrl $kekUrl -KeyEncryptionKeyVaultId $keyVaultId -CreateOption "Attach" -Windows
    PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.'properties.storageProfile'.osDisk.osType
    PS C:\> foreach($dd in $obj.'properties.storageProfile'.dataDisks)
     {
     $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.vhd.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption "Attach"
     }
    ```

    #### <a name="managed-non-encrypted-vms"></a>Macchine virtuali gestite, non crittografate

    Per le macchine virtuali non crittografato a gestito, sarà necessario dischi toocreate gestiti dall'archiviazione blob e quindi collegare i dischi di hello. Per informazioni dettagliate, vedere l'articolo hello [collegare un tooa disco dati macchina virtuale di Windows con PowerShell](../virtual-machines/windows/attach-disk-ps.md). Hello codice di esempio seguente viene illustrato come tooattach hello dischi dati per le macchine virtuali gestite non crittografato.

    ```
    PS C:\> $storageType = "StandardLRS"
    PS C:\> $osDiskName = $vm.Name + "_osdisk"
    PS C:\> $osVhdUri = $obj.'properties.storageProfile'.osDisk.vhd.uri
    PS C:\> $diskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location "West US" -CreateOption Import -SourceUri $osVhdUri
    PS C:\> $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk $diskConfig -ResourceGroupName "test"
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -CreateOption "Attach" -Windows
    PS C:\> foreach($dd in $obj.'properties.storageProfile'.dataDisks)
     {
     $dataDiskName = $vm.Name + $dd.name ;
     $dataVhdUri = $dd.vhd.uri ;
     $dataDiskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location "West US" -CreateOption Import -SourceUri $dataVhdUri ;
     $dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk $dataDiskConfig -ResourceGroupName "test" ;
     Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -ManagedDiskId $dataDisk2.Id -Lun $dd.Lun -CreateOption "Attach"
    }
    ```

    #### <a name="managed-encrypted-vms-bek-and-kek"></a>Macchine virtuali gestite, crittografate (con BEK e KEK)

    Per gestito crittografati le macchine virtuali (crittografate utilizzando BEK e KEK), verranno necessari dischi toocreate gestiti dall'archiviazione blob e quindi collegare i dischi di hello. Per informazioni dettagliate, vedere l'articolo hello [collegare un tooa disco dati macchina virtuale di Windows con PowerShell](../virtual-machines/windows/attach-disk-ps.md). Hello codice di esempio seguente viene illustrato come tooattach hello dischi dati per le macchine virtuali crittografate gestite.

     ```
    PS C:\> $dekUrl = "https://ContosoKeyVault.vault.azure.net:443/secrets/ContosoSecret007/xx000000xx0849999f3xx30000003163"
    PS C:\> $kekUrl = "https://ContosoKeyVault.vault.azure.net:443/keys/ContosoKey007/x9xxx00000x0000x9b9949999xx0x006"
    PS C:\> $keyVaultId = "/subscriptions/abcdedf007-4xyz-1a2b-0000-12a2b345675c/resourceGroups/ContosoRG108/providers/Microsoft.KeyVault/vaults/ContosoKeyVault"
    PS C:\> $storageType = "StandardLRS"
    PS C:\> $osDiskName = $vm.Name + "_osdisk"
    PS C:\> $osVhdUri = $obj.'properties.storageProfile'.osDisk.vhd.uri
    PS C:\> $diskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location "West US" -CreateOption Import -SourceUri $osVhdUri
    PS C:\> $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk $diskConfig -ResourceGroupName "test"
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -DiskEncryptionKeyUrl $dekUrl -DiskEncryptionKeyVaultId $keyVaultId -KeyEncryptionKeyUrl $kekUrl -KeyEncryptionKeyVaultId $keyVaultId -CreateOption "Attach" -Windows
    PS C:\> foreach($dd in $obj.'properties.storageProfile'.dataDisks)
     {
     $dataDiskName = $vm.Name + $dd.name ;
     $dataVhdUri = $dd.vhd.uri ;
     $dataDiskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location "West US" -CreateOption Import -SourceUri $dataVhdUri ;
     $dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk $dataDiskConfig -ResourceGroupName "test" ;
     Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -ManagedDiskId $dataDisk2.Id -Lun $dd.Lun -CreateOption "Attach"
     }
    ```

5. Configurare le impostazioni di rete hello.

    ```
    PS C:\> $nicName="p1234"
    PS C:\> $pip = New-AzureRmPublicIpAddress -Name $nicName -ResourceGroupName "test" -Location "WestUS" -AllocationMethod Dynamic
    PS C:\> $vnet = Get-AzureRmVirtualNetwork -Name "testvNET" -ResourceGroupName "test"
    PS C:\> $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName "test" -Location "WestUS" -SubnetId $vnet.Subnets[$subnetindex].Id -PublicIpAddressId $pip.Id
    PS C:\> $vm=Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
    ```
6. Creare una macchina virtuale hello.

    ```    
    PS C:\> New-AzureRmVM -ResourceGroupName "test" -Location "WestUS" -VM $vm
    ```

## <a name="next-steps"></a>Passaggi successivi
Se si preferisce toouse tooengage di PowerShell con le risorse di Azure, vedere articolo PowerShell hello [distribuire e gestire Backup per Windows Server](backup-client-automation.md). Se si gestiscono i backup DPM, vedere l'articolo hello [distribuire e gestire Backup per DPM](backup-dpm-automation.md). Entrambi gli articoli prevedono due versioni: una per le distribuzioni con Resource Manager, l'altra per le distribuzioni classiche.  
