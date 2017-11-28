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
# <a name="use-azurermbackup-cmdlets-tooback-up-virtual-machines"></a><span data-ttu-id="50e09-103">Utilizzare AzureRM.Backup cmdlet tooback backup di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="50e09-103">Use AzureRM.Backup cmdlets tooback up virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="50e09-104">Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="50e09-104">Resource Manager</span></span>](backup-azure-vms-automation.md)
> * [<span data-ttu-id="50e09-105">Classico</span><span class="sxs-lookup"><span data-stu-id="50e09-105">Classic</span></span>](backup-azure-vms-classic-automation.md)
>
>

<span data-ttu-id="50e09-106">In questo articolo illustra come toouse Azure PowerShell per il backup e ripristino di macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="50e09-106">This article shows you how toouse Azure PowerShell for backup and recovery of Azure VMs.</span></span> <span data-ttu-id="50e09-107">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: Gestione risorse e la distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="50e09-107">Azure has two different deployment models for creating and working with resources: Resource Manager and Classic.</span></span> <span data-ttu-id="50e09-108">In questo articolo viene illustrato l'utilizzo di hello Classic distribuzione modello tooback le credenziali di Backup di dati tooa.</span><span class="sxs-lookup"><span data-stu-id="50e09-108">This article covers using hello Classic deployment model tooback up data tooa Backup vault.</span></span> <span data-ttu-id="50e09-109">Se non è stato creato un insieme di credenziali di Backup nella sottoscrizione, vedere la versione di gestione risorse hello di questo articolo, [tooback cmdlet AzureRM.RecoveryServices.Backup utilizzare backup di macchine virtuali](backup-azure-vms-automation.md).</span><span class="sxs-lookup"><span data-stu-id="50e09-109">If you have not created a Backup vault in your subscription, see hello Resource Manager version of this article, [Use AzureRM.RecoveryServices.Backup cmdlets tooback up virtual machines](backup-azure-vms-automation.md).</span></span> <span data-ttu-id="50e09-110">Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="50e09-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="50e09-111">È ora possibile aggiornare i servizi archivi di Backup gli insiemi di credenziali tooRecovery.</span><span class="sxs-lookup"><span data-stu-id="50e09-111">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="50e09-112">Per informazioni dettagliate, vedere l'articolo hello [aggiornare un tooa insieme di credenziali di Backup dell'insieme di credenziali di servizi di ripristino](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="50e09-112">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="50e09-113">Microsoft incoraggia gli utenti tooupgrade insiemi di credenziali di servizi tooRecovery insiemi di credenziali di Backup.</span><span class="sxs-lookup"><span data-stu-id="50e09-113">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="50e09-114">Dopo 15 ottobre 2017, è possibile utilizzare gli insiemi di credenziali di PowerShell toocreate Backup.</span><span class="sxs-lookup"><span data-stu-id="50e09-114">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="50e09-115">**Entro il 1° novembre 2017**:</span><span class="sxs-lookup"><span data-stu-id="50e09-115">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="50e09-116">Tutti gli archivi di Backup rimanenti verrà automaticamente aggiornato tooRecovery servizi insiemi di credenziali.</span><span class="sxs-lookup"><span data-stu-id="50e09-116">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="50e09-117">Si sarà in grado di tooaccess ai dati di backup nel portale classico hello.</span><span class="sxs-lookup"><span data-stu-id="50e09-117">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="50e09-118">Utilizzare invece hello Azure tooaccess portale i dati di backup in insiemi di servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="50e09-118">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="concepts"></a><span data-ttu-id="50e09-119">Concetti</span><span class="sxs-lookup"><span data-stu-id="50e09-119">Concepts</span></span>
<span data-ttu-id="50e09-120">Questo articolo fornisce informazioni specifica toohello i cmdlet di PowerShell utilizzato tooback backup di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="50e09-120">This article provides information specific toohello PowerShell cmdlets used tooback up virtual machines.</span></span> <span data-ttu-id="50e09-121">Per informazioni introduttive sulla protezione delle macchine virtuali di Azure, vedere [Pianificare l'infrastruttura di backup delle macchine virtuali in Azure](backup-azure-vms-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="50e09-121">For introductory information about protecting Azure VMs, please see [Plan your VM backup infrastructure in Azure](backup-azure-vms-introduction.md).</span></span>

> [!NOTE]
> <span data-ttu-id="50e09-122">Prima di iniziare, leggere hello [prerequisiti](backup-azure-vms-prepare.md) toowork obbligatorio con Backup di Azure e hello [limitazioni](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm) di hello VM soluzione di backup corrente.</span><span class="sxs-lookup"><span data-stu-id="50e09-122">Before you start, read hello [prerequisites](backup-azure-vms-prepare.md) required toowork with Azure Backup, and hello [limitations](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm) of hello current VM backup solution.</span></span>
>
>

<span data-ttu-id="50e09-123">toouse PowerShell in modo efficace, richiedere una gerarchia di hello toounderstand momento di oggetti e da dove toostart.</span><span class="sxs-lookup"><span data-stu-id="50e09-123">toouse PowerShell effectively, take a moment toounderstand hello hierarchy of objects and from where toostart.</span></span>

![Gerarchia oggetti](./media/backup-azure-vms-classic-automation/object-hierarchy.png)

<span data-ttu-id="50e09-125">Hello due flussi più importanti sono abilitazione della protezione per una macchina virtuale e il ripristino dei dati da un punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="50e09-125">hello two most important flows are enabling protection for a VM, and restoring data from a recovery point.</span></span> <span data-ttu-id="50e09-126">lo stato attivo Hello di questo articolo è toohelp diventare esperti nell'uso tooenable i cmdlet di PowerShell hello questi due scenari.</span><span class="sxs-lookup"><span data-stu-id="50e09-126">hello focus of this article is toohelp you become adept at working with hello PowerShell cmdlets tooenable these two scenarios.</span></span>

## <a name="setup-and-registration"></a><span data-ttu-id="50e09-127">Installazione e registrazione</span><span class="sxs-lookup"><span data-stu-id="50e09-127">Setup and Registration</span></span>
<span data-ttu-id="50e09-128">toobegin:</span><span class="sxs-lookup"><span data-stu-id="50e09-128">toobegin:</span></span>

1. <span data-ttu-id="50e09-129">[Scaricare la versione più recente di PowerShell](https://github.com/Azure/azure-powershell/releases) (la versione minima richiesta è: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="50e09-129">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>
2. <span data-ttu-id="50e09-130">Trovare i cmdlet di PowerShell di Azure Backup hello disponibili digitando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="50e09-130">Find hello Azure Backup PowerShell cmdlets available by typing hello following command:</span></span>

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

<span data-ttu-id="50e09-131">Hello seguente programma di installazione e le attività di registrazione può essere automatizzata con PowerShell:</span><span class="sxs-lookup"><span data-stu-id="50e09-131">hello following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="50e09-132">Creare un insieme di credenziali per il backup</span><span class="sxs-lookup"><span data-stu-id="50e09-132">Create a backup vault</span></span>
* <span data-ttu-id="50e09-133">La registrazione delle macchine virtuali hello con hello servizio Azure Backup</span><span class="sxs-lookup"><span data-stu-id="50e09-133">Registering hello VMs with hello Azure Backup service</span></span>

### <a name="create-a-backup-vault"></a><span data-ttu-id="50e09-134">Creare un insieme di credenziali per il backup</span><span class="sxs-lookup"><span data-stu-id="50e09-134">Create a backup vault</span></span>
> [!WARNING]
> <span data-ttu-id="50e09-135">Per i clienti che usano Azure Backup per hello prima volta, è necessario tooregister hello Azure Backup provider toobe utilizzato con la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="50e09-135">For customers using Azure Backup for hello first time, you need tooregister hello Azure Backup provider toobe used with your subscription.</span></span> <span data-ttu-id="50e09-136">Questa operazione può essere eseguita tramite l'esecuzione di hello comando seguente: "Microsoft.Backup" Register AzureRmResourceProvider - ProviderNamespace</span><span class="sxs-lookup"><span data-stu-id="50e09-136">This can be done by running hello following command: Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Backup"</span></span>
>
>

<span data-ttu-id="50e09-137">È possibile creare un nuovo insieme di credenziali di backup utilizzando hello **New AzureRmBackupVault** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="50e09-137">You can create a new backup vault using hello **New-AzureRmBackupVault** cmdlet.</span></span> <span data-ttu-id="50e09-138">insieme di credenziali backup Hello è una risorsa ARM, pertanto è necessario tooplace all'interno di un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="50e09-138">hello backup vault is an ARM resource, so you need tooplace it within a Resource Group.</span></span> <span data-ttu-id="50e09-139">In una console di Azure PowerShell con privilegi elevata, eseguire hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="50e09-139">In an elevated Azure PowerShell console, run hello following commands:</span></span>

```
PS C:\> New-AzureRmResourceGroup –Name “test-rg” –Location “West US”
PS C:\> $backupvault = New-AzureRmBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GeoRedundant
```

<span data-ttu-id="50e09-140">È possibile ottenere un elenco di tutti gli archivi di backup hello in una specifica sottoscrizione utilizzando hello **Get AzureRmBackupVault** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="50e09-140">You can get a list of all hello backup vaults in a given subscription using hello **Get-AzureRmBackupVault** cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="50e09-141">È utile toostore hello insieme di credenziali backup oggetto in una variabile.</span><span class="sxs-lookup"><span data-stu-id="50e09-141">It is convenient toostore hello backup vault object into a variable.</span></span> <span data-ttu-id="50e09-142">oggetto insieme di credenziali di Hello è necessario come input per molti cmdlet di Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="50e09-142">hello vault object is needed as an input for many Azure Backup cmdlets.</span></span>
>
>

### <a name="registering-hello-vms"></a><span data-ttu-id="50e09-143">Registrazione di macchine virtuali hello</span><span class="sxs-lookup"><span data-stu-id="50e09-143">Registering hello VMs</span></span>
<span data-ttu-id="50e09-144">primo passaggio di Hello verso la configurazione di backup con Backup di Azure è tooregister il computer o macchina virtuale con un insieme di credenziali di Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="50e09-144">hello first step towards configuring backup with Azure Backup is tooregister your machine or VM with an Azure Backup vault.</span></span> <span data-ttu-id="50e09-145">Hello **registro AzureRmBackupContainer** cmdlet accetta hello informazioni di input di una macchina virtuale IaaS di Azure e lo registra con insieme di credenziali specificato hello.</span><span class="sxs-lookup"><span data-stu-id="50e09-145">hello **Register-AzureRmBackupContainer** cmdlet takes hello input information of an Azure IaaS virtual machine and registers it with hello specified vault.</span></span> <span data-ttu-id="50e09-146">operazione register Hello associa hello macchina virtuale di Azure con credenziali di backup hello e tiene traccia hello VM del ciclo di vita backup hello.</span><span class="sxs-lookup"><span data-stu-id="50e09-146">hello register operation associates hello Azure virtual machine with hello backup vault and tracks hello VM through hello backup lifecycle.</span></span>

<span data-ttu-id="50e09-147">Registrazione di una macchina virtuale con hello servizio Backup di Azure crea un oggetto contenitore di livello superiore.</span><span class="sxs-lookup"><span data-stu-id="50e09-147">Registering your VM with hello Azure Backup service creates a top-level container object.</span></span> <span data-ttu-id="50e09-148">Un contenitore contiene in genere più elementi che sono possibile eseguire backup, ma in caso di hello di macchine virtuali saranno presenti un solo elemento di backup per il contenitore di hello.</span><span class="sxs-lookup"><span data-stu-id="50e09-148">A container typically contains multiple items that can be backed up, but in hello case of VMs there will be only one backup item for hello container.</span></span>

```
PS C:\> $registerjob = Register-AzureRmBackupContainer -Vault $backupvault -Name "testvm" -ServiceName "testvm"
```

## <a name="backup-azure-vms"></a><span data-ttu-id="50e09-149">Macchine virtuali del servizio Backup di Azure</span><span class="sxs-lookup"><span data-stu-id="50e09-149">Backup Azure VMs</span></span>
### <a name="create-a-protection-policy"></a><span data-ttu-id="50e09-150">Creare i criteri di protezione</span><span class="sxs-lookup"><span data-stu-id="50e09-150">Create a protection policy</span></span>
<span data-ttu-id="50e09-151">Non è obbligatorio toocreate un nuovo backup di toostart criteri di protezione delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="50e09-151">It is not mandatory toocreate a new protection policy toostart backup of your VMs.</span></span> <span data-ttu-id="50e09-152">insieme di credenziali Hello viene fornito con un 'criteri predefiniti' può essere utilizzato tooquickly l'abilitazione della protezione e quindi modificati in seguito con i dettagli a destra di hello.</span><span class="sxs-lookup"><span data-stu-id="50e09-152">hello vault comes with a 'Default Policy' that can be used tooquickly enable protection, and then edited later with hello right details.</span></span> <span data-ttu-id="50e09-153">È possibile ottenere un elenco di criteri di hello disponibili nell'insieme di credenziali hello utilizzando hello **Get AzureRmBackupProtectionPolicy** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="50e09-153">You can get a list of hello policies available in hello vault by using hello **Get-AzureRmBackupProtectionPolicy** cmdlet:</span></span>

```
PS C:\> Get-AzureRmBackupProtectionPolicy -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DefaultPolicy             AzureVM            Daily              26-Aug-15 12:30:00 AM
```

> [!NOTE]
> <span data-ttu-id="50e09-154">fuso orario di Hello del campo BackupTime hello in PowerShell è UTC.</span><span class="sxs-lookup"><span data-stu-id="50e09-154">hello timezone of hello BackupTime field in PowerShell is UTC.</span></span> <span data-ttu-id="50e09-155">Tuttavia, quando l'ora del backup hello viene visualizzato nel portale di Azure hello, fuso orario di hello è allineato tooyour sistema locale insieme a offset UTC di hello.</span><span class="sxs-lookup"><span data-stu-id="50e09-155">However, when hello backup time is shown in hello Azure portal, hello timezone is aligned tooyour local system along with hello UTC offset.</span></span>
>
>

<span data-ttu-id="50e09-156">I criteri di backup sono associati ai criteri di conservazione.</span><span class="sxs-lookup"><span data-stu-id="50e09-156">A backup policy is associated with at least one retention policy.</span></span> <span data-ttu-id="50e09-157">criteri di conservazione Hello definiscono quanto tempo viene conservato un punto di ripristino con Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="50e09-157">hello retention policy defines how long a recovery point is kept with Azure Backup.</span></span> <span data-ttu-id="50e09-158">Hello **New AzureRmBackupRetentionPolicy** cmdlet crea oggetti di PowerShell che includono informazioni sui criteri di conservazione.</span><span class="sxs-lookup"><span data-stu-id="50e09-158">hello **New-AzureRmBackupRetentionPolicy** cmdlet creates PowerShell objects that hold retention policy information.</span></span> <span data-ttu-id="50e09-159">Questi oggetti Criteri di conservazione vengono utilizzati come input toohello *New AzureRmBackupProtectionPolicy* cmdlet o direttamente con hello *Enable AzureRmBackupProtection* cmdlet.</span><span class="sxs-lookup"><span data-stu-id="50e09-159">These retention policy objects are used as inputs toohello *New-AzureRmBackupProtectionPolicy* cmdlet, or directly with hello *Enable-AzureRmBackupProtection* cmdlet.</span></span>

<span data-ttu-id="50e09-160">Un criterio di backup definisce quando e con quale frequenza hello backup di un elemento viene eseguito.</span><span class="sxs-lookup"><span data-stu-id="50e09-160">A backup policy defines when and how often hello backup of an item is done.</span></span> <span data-ttu-id="50e09-161">Hello **New AzureRmBackupProtectionPolicy** cmdlet crea un oggetto PowerShell che contiene informazioni sui criteri di backup.</span><span class="sxs-lookup"><span data-stu-id="50e09-161">hello **New-AzureRmBackupProtectionPolicy** cmdlet creates a PowerShell object that holds backup policy information.</span></span> <span data-ttu-id="50e09-162">Hello criteri di backup viene utilizzato come un input toohello *Enable AzureRmBackupProtection* cmdlet.</span><span class="sxs-lookup"><span data-stu-id="50e09-162">hello backup policy is used as an input toohello *Enable-AzureRmBackupProtection* cmdlet.</span></span>

```
PS C:\> $Daily = New-AzureRmBackupRetentionPolicyObject -DailyRetention -Retention 30
PS C:\> $newpolicy = New-AzureRmBackupProtectionPolicy -Name DailyBackup01 -Type AzureVM -Daily -BackupTime ([datetime]"3:30 PM") -RetentionPolicy $Daily -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DailyBackup01             AzureVM            Daily              01-Sep-15 3:30:00 PM
```

### <a name="enable-protection"></a><span data-ttu-id="50e09-163">Abilitare la protezione</span><span class="sxs-lookup"><span data-stu-id="50e09-163">Enable protection</span></span>
<span data-ttu-id="50e09-164">Abilitazione della protezione include due oggetti: hello elemento e hello criteri ed entrambi toohello toobelong necessità stesso insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="50e09-164">Enabling protection involves two objects - hello Item and hello Policy, and both need toobelong toohello same vault.</span></span> <span data-ttu-id="50e09-165">Dopo aver associato hello elemento criteri hello, flusso di lavoro backup hello verrà attivato in base alla pianificazione definita hello.</span><span class="sxs-lookup"><span data-stu-id="50e09-165">Once hello policy has been associated with hello item, hello backup workflow will kick in at hello defined schedule.</span></span>

```
PS C:\> Get-AzureRmBackupContainer -Type AzureVM -Status Registered -Vault $backupvault | Get-AzureRmBackupItem | Enable-AzureRmBackupProtection -Policy $newpolicy
```

### <a name="initial-backup"></a><span data-ttu-id="50e09-166">Backup iniziale</span><span class="sxs-lookup"><span data-stu-id="50e09-166">Initial backup</span></span>
<span data-ttu-id="50e09-167">pianificazione del backup Hello si occuperà di operazione di copia iniziale completa di hello per elemento hello e copia incrementale hello per i successivi backup hello.</span><span class="sxs-lookup"><span data-stu-id="50e09-167">hello backup schedule will take care of doing hello full initial copy for hello item and hello incremental copy for hello subsequent backups.</span></span> <span data-ttu-id="50e09-168">Tuttavia, se si desidera tooforce hello iniziale backup toohappen a una determinata ora o anche immediatamente utilizzare hello **Backup AzureRmBackupItem** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="50e09-168">However, if you want tooforce hello initial backup toohappen at a certain time or even immediately then use hello **Backup-AzureRmBackupItem** cmdlet:</span></span>

```
PS C:\> $container = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -Name "testvm"
PS C:\> $backupjob = Get-AzureRmBackupItem -Container $container | Backup-AzureRmBackupItem
PS C:\> $backupjob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

> [!NOTE]
> <span data-ttu-id="50e09-169">Hello fuso orario di hello StartTime ed EndTime campi mostrati in PowerShell è l'ora UTC.</span><span class="sxs-lookup"><span data-stu-id="50e09-169">hello timezone of hello StartTime and EndTime fields shown in PowerShell is UTC.</span></span> <span data-ttu-id="50e09-170">Tuttavia, quando informazioni simili hello sono visibile nel portale di Azure hello, fuso orario hello è allineato tooyour orologio di sistema locale.</span><span class="sxs-lookup"><span data-stu-id="50e09-170">However, when hello similar information is shown in hello Azure portal, hello timezone is aligned tooyour local system clock.</span></span>
>
>

### <a name="monitoring-a-backup-job"></a><span data-ttu-id="50e09-171">Monitoraggio di un processo di backup</span><span class="sxs-lookup"><span data-stu-id="50e09-171">Monitoring a backup job</span></span>
<span data-ttu-id="50e09-172">La maggior parte delle operazioni a esecuzione prolungata in Azure Backup è modellata come processo.</span><span class="sxs-lookup"><span data-stu-id="50e09-172">Most long-running operations in Azure Backup are modelled as a job.</span></span> <span data-ttu-id="50e09-173">Questo rende facile tootrack lo stato di avanzamento senza tookeep hello Apri portale di Azure in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="50e09-173">This makes it easy tootrack progress without having tookeep hello Azure portal open at all times.</span></span>

<span data-ttu-id="50e09-174">stato più recente di hello tooget di un processo in corso, utilizzare hello **Get AzureRmBackupJob** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="50e09-174">tooget hello latest status of an in-progress job, use hello **Get-AzureRmBackupJob** cmdlet.</span></span>

```
PS C:\> $joblist = Get-AzureRmBackupJob -Vault $backupvault -Status InProgress
PS C:\> $joblist[0]

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

<span data-ttu-id="50e09-175">Anziché il polling di questi processi per il completamento, che è il codice non necessario, altro - è più semplice hello toouse **attesa AzureRmBackupJob** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="50e09-175">Instead of polling these jobs for completion - which is unnecessary, additional code - it is simpler toouse hello **Wait-AzureRmBackupJob** cmdlet.</span></span> <span data-ttu-id="50e09-176">Quando utilizzato in uno script, hello cmdlet rimarrà in pausa esecuzione hello finché non viene completato il processo di hello o hello specificato viene raggiunto il valore di timeout.</span><span class="sxs-lookup"><span data-stu-id="50e09-176">When used in a script, hello cmdlet will pause hello execution until either hello job completes or hello specified timeout value is reached.</span></span>

```
PS C:\> Wait-AzureRmBackupJob -Job $joblist[0] -Timeout 43200
```


## <a name="restore-an-azure-vm"></a><span data-ttu-id="50e09-177">Ripristinare una macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="50e09-177">Restore an Azure VM</span></span>
<span data-ttu-id="50e09-178">Nei dati di backup toorestore ordine, è necessario tooidentify hello backup elemento e il punto di ripristino hello contenente dati in un momento hello.</span><span class="sxs-lookup"><span data-stu-id="50e09-178">In order toorestore backup data, you need tooidentify hello backed-up Item and hello Recovery Point that holds hello point-in-time data.</span></span> <span data-ttu-id="50e09-179">Queste informazioni sono fornite toohello ripristino AzureRmBackupItem cmdlet tooinitiate un ripristino dei dati dall'account del cliente toohello insieme di credenziali di hello.</span><span class="sxs-lookup"><span data-stu-id="50e09-179">This information is supplied toohello Restore-AzureRmBackupItem cmdlet tooinitiate a restore of data from hello vault toohello customer's account.</span></span>

### <a name="select-hello-vm"></a><span data-ttu-id="50e09-180">Selezionare hello VM</span><span class="sxs-lookup"><span data-stu-id="50e09-180">Select hello VM</span></span>
<span data-ttu-id="50e09-181">oggetto che identifica PowerShell di hello tooget hello destra backup dell'elemento, necessario toostart da hello contenitore nell'insieme di credenziali hello e creare i livelli inferiori gerarchia di oggetti.</span><span class="sxs-lookup"><span data-stu-id="50e09-181">tooget hello PowerShell object that identifies hello right backup Item, you need toostart from hello Container in hello vault, and work your way down object hierarchy.</span></span> <span data-ttu-id="50e09-182">contenitore di hello tooselect che rappresenta una macchina virtuale, utilizzare hello hello **Get AzureRmBackupContainer** cmdlet e inoltrare tramite pipe che toohello **Get AzureRmBackupItem** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="50e09-182">tooselect hello container that represents hello VM, use hello **Get-AzureRmBackupContainer** cmdlet and pipe that toohello **Get-AzureRmBackupItem** cmdlet.</span></span>

```
PS C:\> $backupitem = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -name "testvm" | Get-AzureRmBackupItem
```

### <a name="choose-a-recovery-point"></a><span data-ttu-id="50e09-183">Scegliere un punto di ripristino</span><span class="sxs-lookup"><span data-stu-id="50e09-183">Choose a recovery point</span></span>
<span data-ttu-id="50e09-184">È ora possibile elencare tutti i punti di ripristino di hello per hello backup dell'elemento utilizzando hello **Get AzureRmBackupRecoveryPoint** cmdlet e scegliere toorestore punto di ripristino hello.</span><span class="sxs-lookup"><span data-stu-id="50e09-184">You can now list all hello recovery points for hello backup item using hello **Get-AzureRmBackupRecoveryPoint** cmdlet, and choose hello recovery point toorestore.</span></span> <span data-ttu-id="50e09-185">Gli utenti sceglie in genere più recente di hello *AppConsistent* scegliere nell'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="50e09-185">Typically users pick hello most recent *AppConsistent* point in hello list.</span></span>

```
PS C:\> $rp =  Get-AzureRmBackupRecoveryPoint -Item $backupitem
PS C:\> $rp

RecoveryPointId    RecoveryPointType  RecoveryPointTime      ContainerName
---------------    -----------------  -----------------      -------------
15273496567119     AppConsistent      01-Sep-15 12:27:38 PM  iaasvmcontainer;testvm;testv...
```

<span data-ttu-id="50e09-186">variabile Hello ```$rp``` è una matrice di punti di ripristino per hello selezionato backup dell'elemento, ordinati in ordine inverso di tempo, il punto di ripristino più recente hello in corrispondenza dell'indice 0.</span><span class="sxs-lookup"><span data-stu-id="50e09-186">hello variable ```$rp``` is an array of recovery points for hello selected backup item, sorted in reverse order of time - hello latest recovery point is at index 0.</span></span> <span data-ttu-id="50e09-187">Utilizzare l'indicizzazione di un punto di ripristino hello toopick standard matrice di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="50e09-187">Use standard PowerShell array indexing toopick hello recovery point.</span></span> <span data-ttu-id="50e09-188">Ad esempio: ```$rp[0]``` selezionerà il punto di ripristino più recente hello.</span><span class="sxs-lookup"><span data-stu-id="50e09-188">For example: ```$rp[0]``` will select hello latest recovery point.</span></span>

### <a name="restoring-disks"></a><span data-ttu-id="50e09-189">Ripristino dei dischi</span><span class="sxs-lookup"><span data-stu-id="50e09-189">Restoring disks</span></span>
<span data-ttu-id="50e09-190">Non c'è una differenza chiave tra le operazioni di ripristino hello eseguita tramite hello portale di Azure e Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="50e09-190">There is a key difference between hello restore operations done through hello Azure portal and through Azure PowerShell.</span></span> <span data-ttu-id="50e09-191">Con PowerShell, l'operazione di ripristino hello si arresta al ripristino di dischi hello e le informazioni di configurazione da punto di ripristino hello.</span><span class="sxs-lookup"><span data-stu-id="50e09-191">With PowerShell, hello restore operation stops at restoring hello disks and config information from hello recovery point.</span></span> <span data-ttu-id="50e09-192">e non crea una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="50e09-192">It does not create a virtual machine.</span></span>

> [!WARNING]
> <span data-ttu-id="50e09-193">Hello ripristino AzureRmBackupItem non crea una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="50e09-193">hello Restore-AzureRmBackupItem does not create a VM.</span></span> <span data-ttu-id="50e09-194">Consente di ripristinare solo i dischi hello toohello specificato l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="50e09-194">It only restores hello disks toohello specified storage account.</span></span> <span data-ttu-id="50e09-195">Questo non è hello stesso comportamento si verificheranno in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="50e09-195">This is not hello same behavior you will experience in hello Azure portal.</span></span>
>
>

```
PS C:\> $restorejob = Restore-AzureRmBackupItem -StorageAccountName "DestAccount" -RecoveryPoint $rp[0]
PS C:\> $restorejob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Restore         InProgress      01-Sep-15 1:14:01 PM   01-Jan-01 12:00:00 AM
```

<span data-ttu-id="50e09-196">È possibile ottenere i dettagli di hello dell'operazione di ripristino hello utilizzando hello **Get AzureRmBackupJobDetails** cmdlet, dopo aver completato il processo di ripristino hello.</span><span class="sxs-lookup"><span data-stu-id="50e09-196">You can get hello details of hello restore operation using hello **Get-AzureRmBackupJobDetails** cmdlet once hello Restore job has completed.</span></span> <span data-ttu-id="50e09-197">Hello *ErrorDetails* proprietà sarà disponibili informazioni di hello necessari toorebuild hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="50e09-197">hello *ErrorDetails* property will have hello information needed toorebuild hello VM.</span></span>

```
PS C:\> $restorejob = Get-AzureRmBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmBackupJobDetails -Job $restorejob
```

### <a name="build-hello-vm"></a><span data-ttu-id="50e09-198">Compilare hello VM</span><span class="sxs-lookup"><span data-stu-id="50e09-198">Build hello VM</span></span>
<span data-ttu-id="50e09-199">Hello creazione macchina virtuale da dischi hello ripristinato può essere eseguita tramite il cmdlet PowerShell di Azure Service Management meno recenti di hello, hello nuovi modelli di gestione risorse di Azure o anche utilizzando hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="50e09-199">Building hello VM out of hello restored disks can be done using hello older Azure Service Management PowerShell cmdlets, hello new Azure Resource Manager templates, or even using hello Azure portal.</span></span> <span data-ttu-id="50e09-200">In un semplice esempio viene illustrato come tooget qui utilizzando i cmdlet di gestione del servizio Azure hello.</span><span class="sxs-lookup"><span data-stu-id="50e09-200">In a quick example, we will show how tooget there using hello Azure Service Management cmdlets.</span></span>

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

<span data-ttu-id="50e09-201">Per ulteriori informazioni sulla modalità di ripristino dei dischi toobuild una macchina virtuale da hello, conoscenza hello seguente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="50e09-201">For more information on how toobuild a VM from hello restored disks, read about hello following cmdlets:</span></span>

* [<span data-ttu-id="50e09-202">Add-AzureDisk</span><span class="sxs-lookup"><span data-stu-id="50e09-202">Add-AzureDisk</span></span>](https://msdn.microsoft.com/library/azure/dn495252.aspx)
* [<span data-ttu-id="50e09-203">New-AzureVMConfig</span><span class="sxs-lookup"><span data-stu-id="50e09-203">New-AzureVMConfig</span></span>](https://msdn.microsoft.com/library/azure/dn495159.aspx)
* [<span data-ttu-id="50e09-204">New-AzureVM</span><span class="sxs-lookup"><span data-stu-id="50e09-204">New-AzureVM</span></span>](https://msdn.microsoft.com/library/azure/dn495254.aspx)

## <a name="code-samples"></a><span data-ttu-id="50e09-205">Esempi di codice</span><span class="sxs-lookup"><span data-stu-id="50e09-205">Code samples</span></span>
### <a name="1-get-hello-completion-status-of-job-sub-tasks"></a><span data-ttu-id="50e09-206">1. Ottenere lo stato di completamento hello secondaria delle attività di processo</span><span class="sxs-lookup"><span data-stu-id="50e09-206">1. Get hello completion status of job sub-tasks</span></span>
<span data-ttu-id="50e09-207">stato di completamento hello tootrack delle singole attività secondarie, è possibile utilizzare hello **Get AzureRmBackupJobDetails** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="50e09-207">tootrack hello completion status of individual sub-tasks, you can use hello **Get-AzureRmBackupJobDetails** cmdlet:</span></span>

```
PS C:\> $details = Get-AzureRmBackupJobDetails -JobId $backupjob.InstanceId -Vault $backupvault
PS C:\> $details.SubTasks

Name                                                        Status
----                                                        ------
Take Snapshot                                               Completed
Transfer data tooBackup vault                               InProgress
```

### <a name="2-create-a-dailyweekly-report-of-backup-jobs"></a><span data-ttu-id="50e09-208">2. Creare un report settimanale o giornaliero dei processi di backup</span><span class="sxs-lookup"><span data-stu-id="50e09-208">2. Create a daily/weekly report of backup jobs</span></span>
<span data-ttu-id="50e09-209">In genere, gli amministratori vogliono tooknow quali i processi di backup è stati eseguiti in hello ultime 24 ore, lo stato di hello di questi processi di backup.</span><span class="sxs-lookup"><span data-stu-id="50e09-209">Administrators typically want tooknow what backup jobs ran in hello last 24 hours, hello status of those backup jobs.</span></span> <span data-ttu-id="50e09-210">Inoltre, quantità hello di dati trasferiti offre agli amministratori un modo tooestimate dell'utilizzo dei dati mensili.</span><span class="sxs-lookup"><span data-stu-id="50e09-210">Additionally, hello amount of data transferred gives administrators a way tooestimate their monthly data usage.</span></span> <span data-ttu-id="50e09-211">script Hello riportato di seguito vengono utilizzati i dati non elaborati hello hello servizio Backup di Azure e visualizza le informazioni di hello nella console di PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="50e09-211">hello script below pulls hello raw data from hello Azure Backup service and displays hello information in hello PowerShell console.</span></span>

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

<span data-ttu-id="50e09-212">Se si desidera tooadd l'output del report toothis funzionalità di creazione di grafici, informazioni dal post di blog di TechNet hello [grafici con PowerShell](http://blogs.technet.com/b/richard_macdonald/archive/2009/04/28/3231887.aspx)</span><span class="sxs-lookup"><span data-stu-id="50e09-212">If you want tooadd charting capabilities toothis report output, learn from hello TechNet blog post [Charting with PowerShell](http://blogs.technet.com/b/richard_macdonald/archive/2009/04/28/3231887.aspx)</span></span>

## <a name="next-steps"></a><span data-ttu-id="50e09-213">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="50e09-213">Next steps</span></span>
<span data-ttu-id="50e09-214">Se si preferisce utilizzare PowerShell tooengage con le risorse di Azure, consultare l'articolo PowerShell hello per la protezione di Windows Server, [distribuire e gestire Backup per Windows Server](backup-client-automation-classic.md).</span><span class="sxs-lookup"><span data-stu-id="50e09-214">If you prefer using PowerShell tooengage with your Azure resources, check out hello PowerShell article for protecting Windows Server, [Deploy and Manage Backup for Windows Server](backup-client-automation-classic.md).</span></span> <span data-ttu-id="50e09-215">È disponibile anche un articolo relativo a PowerShell per la gestione dei backup di DPM, [Distribuire e gestire il backup per DPM](backup-dpm-automation-classic.md).</span><span class="sxs-lookup"><span data-stu-id="50e09-215">There is also a PowerShell article for managing DPM backups, [Deploy and Manage Backup for DPM](backup-dpm-automation-classic.md).</span></span> <span data-ttu-id="50e09-216">Entrambi gli articoli prevedono due versioni: una per la distribuzione con Resource Manager, l’altra per la distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="50e09-216">Both of these articles have a version for Resource Manager deployments as well as Classic deployments.</span></span>
