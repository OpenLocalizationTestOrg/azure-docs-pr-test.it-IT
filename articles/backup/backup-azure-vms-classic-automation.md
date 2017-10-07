---
title: aaaDeploy e gestire il backup per le macchine virtuali di Azure tramite PowerShell | Documenti Microsoft
description: Informazioni su come toodeploy e gestire il Backup di Azure tramite PowerShell.
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 2e24b1d9-4375-4049-a28d-e3bc01152f32
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/2/2017
ms.author: markgal;trinadhk;jimpark
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f3ecd3f94c5e3e8fc8018e8786302edd4847744b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azurermbackup-cmdlets-tooback-up-virtual-machines"></a>Utilizzare AzureRM.Backup cmdlet tooback backup di macchine virtuali
> [!div class="op_single_selector"]
> * [Gestione risorse](backup-azure-vms-automation.md)
> * [Classico](backup-azure-vms-classic-automation.md)
>
>

In questo articolo illustra come toouse Azure PowerShell per il backup e ripristino di macchine virtuali di Azure. Azure offre due diversi modelli di distribuzione per creare e usare le risorse: Gestione risorse e la distribuzione classica. In questo articolo viene illustrato l'utilizzo di hello Classic distribuzione modello tooback le credenziali di Backup di dati tooa. Se non è stato creato un insieme di credenziali di Backup nella sottoscrizione, vedere la versione di gestione risorse hello di questo articolo, [tooback cmdlet AzureRM.RecoveryServices.Backup utilizzare backup di macchine virtuali](backup-azure-vms-automation.md). Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.

> [!IMPORTANT]
> È ora possibile aggiornare i servizi archivi di Backup gli insiemi di credenziali tooRecovery. Per informazioni dettagliate, vedere l'articolo hello [aggiornare un tooa insieme di credenziali di Backup dell'insieme di credenziali di servizi di ripristino](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft incoraggia gli utenti tooupgrade insiemi di credenziali di servizi tooRecovery insiemi di credenziali di Backup.<br/> Dopo 15 ottobre 2017, è possibile utilizzare gli insiemi di credenziali di PowerShell toocreate Backup. **Entro il 1° novembre 2017**:
>- Tutti gli archivi di Backup rimanenti verrà automaticamente aggiornato tooRecovery servizi insiemi di credenziali.
>- Si sarà in grado di tooaccess ai dati di backup nel portale classico hello. Utilizzare invece hello Azure tooaccess portale i dati di backup in insiemi di servizi di ripristino.
>

## <a name="concepts"></a>Concetti
Questo articolo fornisce informazioni specifica toohello i cmdlet di PowerShell utilizzato tooback backup di macchine virtuali. Per informazioni introduttive sulla protezione delle macchine virtuali di Azure, vedere [Pianificare l'infrastruttura di backup delle macchine virtuali in Azure](backup-azure-vms-introduction.md).

> [!NOTE]
> Prima di iniziare, leggere hello [prerequisiti](backup-azure-vms-prepare.md) toowork obbligatorio con Backup di Azure e hello [limitazioni](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm) di hello VM soluzione di backup corrente.
>
>

toouse PowerShell in modo efficace, richiedere una gerarchia di hello toounderstand momento di oggetti e da dove toostart.

![Gerarchia oggetti](./media/backup-azure-vms-classic-automation/object-hierarchy.png)

Hello due flussi più importanti sono abilitazione della protezione per una macchina virtuale e il ripristino dei dati da un punto di ripristino. lo stato attivo Hello di questo articolo è toohelp diventare esperti nell'uso tooenable i cmdlet di PowerShell hello questi due scenari.

## <a name="setup-and-registration"></a>Installazione e registrazione
toobegin:

1. [Scaricare la versione più recente di PowerShell](https://github.com/Azure/azure-powershell/releases) (la versione minima richiesta è: 1.0.0)
2. Trovare i cmdlet di PowerShell di Azure Backup hello disponibili digitando hello comando seguente:

```
PS C:\> Get-Command *azurermbackup*

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Backup-AzureRmBackupItem                           1.0.1      AzureRM.Backup
Cmdlet          Disable-AzureRmBackupProtection                    1.0.1      AzureRM.Backup
Cmdlet          Enable-AzureRmBackupContainerReregistration        1.0.1      AzureRM.Backup
Cmdlet          Enable-AzureRmBackupProtection                     1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupContainer                         1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupItem                              1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupJob                               1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupJobDetails                        1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupProtectionPolicy                  1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupRecoveryPoint                     1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupVault                             1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupVaultCredentials                  1.0.1      AzureRM.Backup
Cmdlet          New-AzureRmBackupProtectionPolicy                  1.0.1      AzureRM.Backup
Cmdlet          New-AzureRmBackupRetentionPolicyObject             1.0.1      AzureRM.Backup
Cmdlet          New-AzureRmBackupVault                             1.0.1      AzureRM.Backup
Cmdlet          Register-AzureRmBackupContainer                    1.0.1      AzureRM.Backup
Cmdlet          Remove-AzureRmBackupProtectionPolicy               1.0.1      AzureRM.Backup
Cmdlet          Remove-AzureRmBackupVault                          1.0.1      AzureRM.Backup
Cmdlet          Restore-AzureRmBackupItem                          1.0.1      AzureRM.Backup
Cmdlet          Set-AzureRmBackupProtectionPolicy                  1.0.1      AzureRM.Backup
Cmdlet          Set-AzureRmBackupVault                             1.0.1      AzureRM.Backup
Cmdlet          Stop-AzureRmBackupJob                              1.0.1      AzureRM.Backup
Cmdlet          Unregister-AzureRmBackupContainer                  1.0.1      AzureRM.Backup
Cmdlet          Wait-AzureRmBackupJob                              1.0.1      AzureRM.Backup
```

Hello seguente programma di installazione e le attività di registrazione può essere automatizzata con PowerShell:

* Creare un insieme di credenziali per il backup
* La registrazione delle macchine virtuali hello con hello servizio Azure Backup

### <a name="create-a-backup-vault"></a>Creare un insieme di credenziali per il backup
> [!WARNING]
> Per i clienti che usano Azure Backup per hello prima volta, è necessario tooregister hello Azure Backup provider toobe utilizzato con la sottoscrizione. Questa operazione può essere eseguita tramite l'esecuzione di hello comando seguente: "Microsoft.Backup" Register AzureRmResourceProvider - ProviderNamespace
>
>

È possibile creare un nuovo insieme di credenziali di backup utilizzando hello **New AzureRmBackupVault** cmdlet. insieme di credenziali backup Hello è una risorsa ARM, pertanto è necessario tooplace all'interno di un gruppo di risorse. In una console di Azure PowerShell con privilegi elevata, eseguire hello seguenti comandi:

```
PS C:\> New-AzureRmResourceGroup –Name “test-rg” –Location “West US”
PS C:\> $backupvault = New-AzureRmBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GeoRedundant
```

È possibile ottenere un elenco di tutti gli archivi di backup hello in una specifica sottoscrizione utilizzando hello **Get AzureRmBackupVault** cmdlet.

> [!NOTE]
> È utile toostore hello insieme di credenziali backup oggetto in una variabile. oggetto insieme di credenziali di Hello è necessario come input per molti cmdlet di Azure Backup.
>
>

### <a name="registering-hello-vms"></a>Registrazione di macchine virtuali hello
primo passaggio di Hello verso la configurazione di backup con Backup di Azure è tooregister il computer o macchina virtuale con un insieme di credenziali di Backup di Azure. Hello **registro AzureRmBackupContainer** cmdlet accetta hello informazioni di input di una macchina virtuale IaaS di Azure e lo registra con insieme di credenziali specificato hello. operazione register Hello associa hello macchina virtuale di Azure con credenziali di backup hello e tiene traccia hello VM del ciclo di vita backup hello.

Registrazione di una macchina virtuale con hello servizio Backup di Azure crea un oggetto contenitore di livello superiore. Un contenitore contiene in genere più elementi che sono possibile eseguire backup, ma in caso di hello di macchine virtuali saranno presenti un solo elemento di backup per il contenitore di hello.

```
PS C:\> $registerjob = Register-AzureRmBackupContainer -Vault $backupvault -Name "testvm" -ServiceName "testvm"
```

## <a name="backup-azure-vms"></a>Macchine virtuali del servizio Backup di Azure
### <a name="create-a-protection-policy"></a>Creare i criteri di protezione
Non è obbligatorio toocreate un nuovo backup di toostart criteri di protezione delle macchine virtuali. insieme di credenziali Hello viene fornito con un 'criteri predefiniti' può essere utilizzato tooquickly l'abilitazione della protezione e quindi modificati in seguito con i dettagli a destra di hello. È possibile ottenere un elenco di criteri di hello disponibili nell'insieme di credenziali hello utilizzando hello **Get AzureRmBackupProtectionPolicy** cmdlet:

```
PS C:\> Get-AzureRmBackupProtectionPolicy -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DefaultPolicy             AzureVM            Daily              26-Aug-15 12:30:00 AM
```

> [!NOTE]
> fuso orario di Hello del campo BackupTime hello in PowerShell è UTC. Tuttavia, quando l'ora del backup hello viene visualizzato nel portale di Azure hello, fuso orario di hello è allineato tooyour sistema locale insieme a offset UTC di hello.
>
>

I criteri di backup sono associati ai criteri di conservazione. criteri di conservazione Hello definiscono quanto tempo viene conservato un punto di ripristino con Backup di Azure. Hello **New AzureRmBackupRetentionPolicy** cmdlet crea oggetti di PowerShell che includono informazioni sui criteri di conservazione. Questi oggetti Criteri di conservazione vengono utilizzati come input toohello *New AzureRmBackupProtectionPolicy* cmdlet o direttamente con hello *Enable AzureRmBackupProtection* cmdlet.

Un criterio di backup definisce quando e con quale frequenza hello backup di un elemento viene eseguito. Hello **New AzureRmBackupProtectionPolicy** cmdlet crea un oggetto PowerShell che contiene informazioni sui criteri di backup. Hello criteri di backup viene utilizzato come un input toohello *Enable AzureRmBackupProtection* cmdlet.

```
PS C:\> $Daily = New-AzureRmBackupRetentionPolicyObject -DailyRetention -Retention 30
PS C:\> $newpolicy = New-AzureRmBackupProtectionPolicy -Name DailyBackup01 -Type AzureVM -Daily -BackupTime ([datetime]"3:30 PM") -RetentionPolicy $Daily -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DailyBackup01             AzureVM            Daily              01-Sep-15 3:30:00 PM
```

### <a name="enable-protection"></a>Abilitare la protezione
Abilitazione della protezione include due oggetti: hello elemento e hello criteri ed entrambi toohello toobelong necessità stesso insieme di credenziali. Dopo aver associato hello elemento criteri hello, flusso di lavoro backup hello verrà attivato in base alla pianificazione definita hello.

```
PS C:\> Get-AzureRmBackupContainer -Type AzureVM -Status Registered -Vault $backupvault | Get-AzureRmBackupItem | Enable-AzureRmBackupProtection -Policy $newpolicy
```

### <a name="initial-backup"></a>Backup iniziale
pianificazione del backup Hello si occuperà di operazione di copia iniziale completa di hello per elemento hello e copia incrementale hello per i successivi backup hello. Tuttavia, se si desidera tooforce hello iniziale backup toohappen a una determinata ora o anche immediatamente utilizzare hello **Backup AzureRmBackupItem** cmdlet:

```
PS C:\> $container = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -Name "testvm"
PS C:\> $backupjob = Get-AzureRmBackupItem -Container $container | Backup-AzureRmBackupItem
PS C:\> $backupjob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

> [!NOTE]
> Hello fuso orario di hello StartTime ed EndTime campi mostrati in PowerShell è l'ora UTC. Tuttavia, quando informazioni simili hello sono visibile nel portale di Azure hello, fuso orario hello è allineato tooyour orologio di sistema locale.
>
>

### <a name="monitoring-a-backup-job"></a>Monitoraggio di un processo di backup
La maggior parte delle operazioni a esecuzione prolungata in Azure Backup è modellata come processo. Questo rende facile tootrack lo stato di avanzamento senza tookeep hello Apri portale di Azure in qualsiasi momento.

stato più recente di hello tooget di un processo in corso, utilizzare hello **Get AzureRmBackupJob** cmdlet.

```
PS C:\> $joblist = Get-AzureRmBackupJob -Vault $backupvault -Status InProgress
PS C:\> $joblist[0]

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

Anziché il polling di questi processi per il completamento, che è il codice non necessario, altro - è più semplice hello toouse **attesa AzureRmBackupJob** cmdlet. Quando utilizzato in uno script, hello cmdlet rimarrà in pausa esecuzione hello finché non viene completato il processo di hello o hello specificato viene raggiunto il valore di timeout.

```
PS C:\> Wait-AzureRmBackupJob -Job $joblist[0] -Timeout 43200
```


## <a name="restore-an-azure-vm"></a>Ripristinare una macchina virtuale di Azure
Nei dati di backup toorestore ordine, è necessario tooidentify hello backup elemento e il punto di ripristino hello contenente dati in un momento hello. Queste informazioni sono fornite toohello ripristino AzureRmBackupItem cmdlet tooinitiate un ripristino dei dati dall'account del cliente toohello insieme di credenziali di hello.

### <a name="select-hello-vm"></a>Selezionare hello VM
oggetto che identifica PowerShell di hello tooget hello destra backup dell'elemento, necessario toostart da hello contenitore nell'insieme di credenziali hello e creare i livelli inferiori gerarchia di oggetti. contenitore di hello tooselect che rappresenta una macchina virtuale, utilizzare hello hello **Get AzureRmBackupContainer** cmdlet e inoltrare tramite pipe che toohello **Get AzureRmBackupItem** cmdlet.

```
PS C:\> $backupitem = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -name "testvm" | Get-AzureRmBackupItem
```

### <a name="choose-a-recovery-point"></a>Scegliere un punto di ripristino
È ora possibile elencare tutti i punti di ripristino di hello per hello backup dell'elemento utilizzando hello **Get AzureRmBackupRecoveryPoint** cmdlet e scegliere toorestore punto di ripristino hello. Gli utenti sceglie in genere più recente di hello *AppConsistent* scegliere nell'elenco di hello.

```
PS C:\> $rp =  Get-AzureRmBackupRecoveryPoint -Item $backupitem
PS C:\> $rp

RecoveryPointId    RecoveryPointType  RecoveryPointTime      ContainerName
---------------    -----------------  -----------------      -------------
15273496567119     AppConsistent      01-Sep-15 12:27:38 PM  iaasvmcontainer;testvm;testv...
```

variabile Hello ```$rp``` è una matrice di punti di ripristino per hello selezionato backup dell'elemento, ordinati in ordine inverso di tempo, il punto di ripristino più recente hello in corrispondenza dell'indice 0. Utilizzare l'indicizzazione di un punto di ripristino hello toopick standard matrice di PowerShell. Ad esempio: ```$rp[0]``` selezionerà il punto di ripristino più recente hello.

### <a name="restoring-disks"></a>Ripristino dei dischi
Non c'è una differenza chiave tra le operazioni di ripristino hello eseguita tramite hello portale di Azure e Azure PowerShell. Con PowerShell, l'operazione di ripristino hello si arresta al ripristino di dischi hello e le informazioni di configurazione da punto di ripristino hello. e non crea una macchina virtuale.

> [!WARNING]
> Hello ripristino AzureRmBackupItem non crea una macchina virtuale. Consente di ripristinare solo i dischi hello toohello specificato l'account di archiviazione. Questo non è hello stesso comportamento si verificheranno in hello portale di Azure.
>
>

```
PS C:\> $restorejob = Restore-AzureRmBackupItem -StorageAccountName "DestAccount" -RecoveryPoint $rp[0]
PS C:\> $restorejob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Restore         InProgress      01-Sep-15 1:14:01 PM   01-Jan-01 12:00:00 AM
```

È possibile ottenere i dettagli di hello dell'operazione di ripristino hello utilizzando hello **Get AzureRmBackupJobDetails** cmdlet, dopo aver completato il processo di ripristino hello. Hello *ErrorDetails* proprietà sarà disponibili informazioni di hello necessari toorebuild hello macchina virtuale.

```
PS C:\> $restorejob = Get-AzureRmBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmBackupJobDetails -Job $restorejob
```

### <a name="build-hello-vm"></a>Compilare hello VM
Hello creazione macchina virtuale da dischi hello ripristinato può essere eseguita tramite il cmdlet PowerShell di Azure Service Management meno recenti di hello, hello nuovi modelli di gestione risorse di Azure o anche utilizzando hello portale di Azure. In un semplice esempio viene illustrato come tooget qui utilizzando i cmdlet di gestione del servizio Azure hello.

```
$properties  = $details.Properties

$storageAccountName = $properties["Target Storage Account Name"]
$containerName = $properties["Config Blob Container Name"]
$blobName = $properties["Config Blob Name"]

$keys = Get-AzureStorageKey -StorageAccountName $storageAccountName
$storageAccountKey = $keys.Primary
$storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey


$destination_path = "C:\Users\admin\Desktop\vmconfig.xml"
Get-AzureStorageBlobContent -Container $containerName -Blob $blobName -Destination $destination_path -Context $storageContext


$obj = [xml](((Get-Content -Path $destination_path -Encoding UniCode)).TrimEnd([char]0x00))
$pvr = $obj.PersistentVMRole
$os = $pvr.OSVirtualHardDisk
$dds = $pvr.DataVirtualHardDisks
$osDisk = Add-AzureDisk -MediaLocation $os.MediaLink -OS $os.OS -DiskName "panbhaosdisk"
$vm = New-AzureVMConfig -Name $pvr.RoleName -InstanceSize $pvr.RoleSize -DiskName $osDisk.DiskName

if (!($dds -eq $null))
{
    foreach($d in $dds.DataVirtualHardDisk)
    {
        $lun = 0
        if(!($d.Lun -eq $null))
        {
            $lun = $d.Lun
        }
        $name = "panbhadataDisk" + $lun
        Add-AzureDisk -DiskName $name -MediaLocation $d.MediaLink
        $vm | Add-AzureDataDisk -Import -DiskName $name -LUN $lun
    }
}

New-AzureVM -ServiceName "panbhasample" -Location "SouthEast Asia" -VM $vm
```

Per ulteriori informazioni sulla modalità di ripristino dei dischi toobuild una macchina virtuale da hello, conoscenza hello seguente cmdlet:

* [Add-AzureDisk](https://msdn.microsoft.com/library/azure/dn495252.aspx)
* [New-AzureVMConfig](https://msdn.microsoft.com/library/azure/dn495159.aspx)
* [New-AzureVM](https://msdn.microsoft.com/library/azure/dn495254.aspx)

## <a name="code-samples"></a>Esempi di codice
### <a name="1-get-hello-completion-status-of-job-sub-tasks"></a>1. Ottenere lo stato di completamento hello secondaria delle attività di processo
stato di completamento hello tootrack delle singole attività secondarie, è possibile utilizzare hello **Get AzureRmBackupJobDetails** cmdlet:

```
PS C:\> $details = Get-AzureRmBackupJobDetails -JobId $backupjob.InstanceId -Vault $backupvault
PS C:\> $details.SubTasks

Name                                                        Status
----                                                        ------
Take Snapshot                                               Completed
Transfer data tooBackup vault                               InProgress
```

### <a name="2-create-a-dailyweekly-report-of-backup-jobs"></a>2. Creare un report settimanale o giornaliero dei processi di backup
In genere, gli amministratori vogliono tooknow quali i processi di backup è stati eseguiti in hello ultime 24 ore, lo stato di hello di questi processi di backup. Inoltre, quantità hello di dati trasferiti offre agli amministratori un modo tooestimate dell'utilizzo dei dati mensili. script Hello riportato di seguito vengono utilizzati i dati non elaborati hello hello servizio Backup di Azure e visualizza le informazioni di hello nella console di PowerShell hello.

```
param(  [Parameter(Mandatory=$True,Position=1)]
        [string]$backupvaultname,

        [Parameter(Mandatory=$False,Position=2)]
        [int]$numberofdays = 7)


#Initialize variables
$DAILYBACKUPSTATS = @()
$backupvault = Get-AzureRmBackupVault -Name $backupvaultname
$enddate = ([datetime]::Today).AddDays(1)
$startdate = ([datetime]::Today)

for( $i = 1; $i -le $numberofdays; $i++ )
{
    # We query one day at a time because pulling 7 days of data might be too much
    $dailyjoblist = Get-AzureRmBackupJob -Vault $backupvault -From $startdate -too$enddate -Type AzureVM -Operation Backup
    Write-Progress -Activity "Getting job information for hello last $numberofdays days" -Status "Day -$i" -PercentComplete ([int]([decimal]$i*100/$numberofdays))

    foreach( $job in $dailyjoblist )
    {
        #Extract hello information for hello reports
        $newstatsobj = New-Object System.Object
        $newstatsobj | Add-Member -Type NoteProperty -Name Date -Value $startdate
        $newstatsobj | Add-Member -Type NoteProperty -Name VMName -Value $job.WorkloadName
        $newstatsobj | Add-Member -Type NoteProperty -Name Duration -Value $job.Duration
        $newstatsobj | Add-Member -Type NoteProperty -Name Status -Value $job.Status

        $details = Get-AzureRmBackupJobDetails -Job $job
        $newstatsobj | Add-Member -Type NoteProperty -Name BackupSize -Value $details.Properties["Backup Size"]
        $DAILYBACKUPSTATS += $newstatsobj
    }

    $enddate = $enddate.AddDays(-1)
    $startdate = $startdate.AddDays(-1)
}

$DAILYBACKUPSTATS | Out-GridView
```

Se si desidera tooadd l'output del report toothis funzionalità di creazione di grafici, informazioni dal post di blog di TechNet hello [grafici con PowerShell](http://blogs.technet.com/b/richard_macdonald/archive/2009/04/28/3231887.aspx)

## <a name="next-steps"></a>Passaggi successivi
Se si preferisce utilizzare PowerShell tooengage con le risorse di Azure, consultare l'articolo PowerShell hello per la protezione di Windows Server, [distribuire e gestire Backup per Windows Server](backup-client-automation-classic.md). È disponibile anche un articolo relativo a PowerShell per la gestione dei backup di DPM, [Distribuire e gestire il backup per DPM](backup-dpm-automation-classic.md). Entrambi gli articoli prevedono due versioni: una per la distribuzione con Resource Manager, l’altra per la distribuzione classica.
