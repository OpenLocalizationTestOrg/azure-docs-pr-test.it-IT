---
title: Distribuire e gestire il backup per le VM di Azure con PowerShell | Documentazione Microsoft
description: Informazioni su come distribuire e gestire Backup di Azure mediante PowerShell.
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
ms.openlocfilehash: 5f0f06adb8177ce2d17aa0b40666470279c04e22
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="use-azurermbackup-cmdlets-to-back-up-virtual-machines"></a><span data-ttu-id="2437f-103">Usare i cmdlet AzureRM.Backup per eseguire il backup di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="2437f-103">Use AzureRM.Backup cmdlets to back up virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2437f-104">Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="2437f-104">Resource Manager</span></span>](backup-azure-vms-automation.md)
> * [<span data-ttu-id="2437f-105">Classico</span><span class="sxs-lookup"><span data-stu-id="2437f-105">Classic</span></span>](backup-azure-vms-classic-automation.md)
>
>

<span data-ttu-id="2437f-106">Questo articolo descrive come usare Azure PowerShell per il backup e il ripristino delle macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="2437f-106">This article shows you how to use Azure PowerShell for backup and recovery of Azure VMs.</span></span> <span data-ttu-id="2437f-107">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: Gestione risorse e la distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="2437f-107">Azure has two different deployment models for creating and working with resources: Resource Manager and Classic.</span></span> <span data-ttu-id="2437f-108">Questo articolo illustra l'uso del modello di distribuzione classica per il backup di dati nell'insieme di credenziali di backup.</span><span class="sxs-lookup"><span data-stu-id="2437f-108">This article covers using the Classic deployment model to back up data to a Backup vault.</span></span> <span data-ttu-id="2437f-109">Se nella sottoscrizione non è stato creato un insieme di credenziali di backup, vedere la versione relativa a Resource Manager di questo articolo, [Usare i cmdlet AzureRM.RecoveryServices.Backup per eseguire il backup di macchine virtuali](backup-azure-vms-automation.md).</span><span class="sxs-lookup"><span data-stu-id="2437f-109">If you have not created a Backup vault in your subscription, see the Resource Manager version of this article, [Use AzureRM.RecoveryServices.Backup cmdlets to back up virtual machines](backup-azure-vms-automation.md).</span></span> <span data-ttu-id="2437f-110">Microsoft consiglia di usare il modello di Gestione risorse per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="2437f-110">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2437f-111">È ora possibile aggiornare gli insiemi di credenziali di Backup ad insiemi di credenziali dei servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="2437f-111">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="2437f-112">Per altre informazioni, vedere l'articolo [Aggiornare un insieme di credenziali di Backup a un insieme di credenziali di Servizi di ripristino](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="2437f-112">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="2437f-113">Microsoft consiglia di aggiornare gli insiemi di credenziali di Backup a insiemi di credenziali dei servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="2437f-113">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="2437f-114">Dopo il 15 ottobre 2017 non sarà possibile usare PowerShell per creare insiemi di credenziali di backup.</span><span class="sxs-lookup"><span data-stu-id="2437f-114">After October 15, 2017, you can’t use PowerShell to create Backup vaults.</span></span> <span data-ttu-id="2437f-115">**Entro il 1° novembre 2017**:</span><span class="sxs-lookup"><span data-stu-id="2437f-115">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="2437f-116">Tutti gli insiemi di credenziali di backup rimanenti verranno aggiornati automaticamente a insiemi di credenziali dei servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="2437f-116">All remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="2437f-117">e non sarà più possibile accedere ai dati di backup nel portale classico.</span><span class="sxs-lookup"><span data-stu-id="2437f-117">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="2437f-118">Sarà possibile invece usare il portale di Azure per accedere ai dati di backup negli insiemi di credenziali di servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="2437f-118">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

## <a name="concepts"></a><span data-ttu-id="2437f-119">Concetti</span><span class="sxs-lookup"><span data-stu-id="2437f-119">Concepts</span></span>
<span data-ttu-id="2437f-120">Questo articolo fornisce informazioni specifiche per i cmdlet di PowerShell usati per eseguire il backup di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="2437f-120">This article provides information specific to the PowerShell cmdlets used to back up virtual machines.</span></span> <span data-ttu-id="2437f-121">Per informazioni introduttive sulla protezione delle macchine virtuali di Azure, vedere [Pianificare l'infrastruttura di backup delle macchine virtuali in Azure](backup-azure-vms-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2437f-121">For introductory information about protecting Azure VMs, please see [Plan your VM backup infrastructure in Azure](backup-azure-vms-introduction.md).</span></span>

> [!NOTE]
> <span data-ttu-id="2437f-122">Prima di iniziare, vedere i [prerequisiti](backup-azure-vms-prepare.md) necessari per usare Backup di Azure e le [limitazioni](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm) della soluzione corrente di backup delle VM.</span><span class="sxs-lookup"><span data-stu-id="2437f-122">Before you start, read the [prerequisites](backup-azure-vms-prepare.md) required to work with Azure Backup, and the [limitations](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm) of the current VM backup solution.</span></span>
>
>

<span data-ttu-id="2437f-123">Per un uso efficace di PowerShell, è opportuno comprendere la gerarchia degli oggetti e da dove iniziare.</span><span class="sxs-lookup"><span data-stu-id="2437f-123">To use PowerShell effectively, take a moment to understand the hierarchy of objects and from where to start.</span></span>

![Gerarchia oggetti](./media/backup-azure-vms-classic-automation/object-hierarchy.png)

<span data-ttu-id="2437f-125">I due flussi più importanti sono quelli relativi all'attivazione della protezione per una macchina virtuale e al ripristino dei dati da un punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="2437f-125">The two most important flows are enabling protection for a VM, and restoring data from a recovery point.</span></span> <span data-ttu-id="2437f-126">Questo articolo fornisce le informazioni necessarie per acquisire familiarità con l'uso dei cmdlet di PowerShell per abilitare questi due scenari.</span><span class="sxs-lookup"><span data-stu-id="2437f-126">The focus of this article is to help you become adept at working with the PowerShell cmdlets to enable these two scenarios.</span></span>

## <a name="setup-and-registration"></a><span data-ttu-id="2437f-127">Installazione e registrazione</span><span class="sxs-lookup"><span data-stu-id="2437f-127">Setup and Registration</span></span>
<span data-ttu-id="2437f-128">Per iniziare:</span><span class="sxs-lookup"><span data-stu-id="2437f-128">To begin:</span></span>

1. <span data-ttu-id="2437f-129">[Scaricare la versione più recente di PowerShell](https://github.com/Azure/azure-powershell/releases) (la versione minima richiesta è: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="2437f-129">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>
2. <span data-ttu-id="2437f-130">Cercare i cmdlet PowerShell di Azure Backup disponibili digitando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="2437f-130">Find the Azure Backup PowerShell cmdlets available by typing the following command:</span></span>

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

<span data-ttu-id="2437f-131">Le attività di installazione e registrazione seguenti possono essere automatizzate tramite PowerShell:</span><span class="sxs-lookup"><span data-stu-id="2437f-131">The following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="2437f-132">Creare un insieme di credenziali per il backup</span><span class="sxs-lookup"><span data-stu-id="2437f-132">Create a backup vault</span></span>
* <span data-ttu-id="2437f-133">Registrazione delle macchine virtuali nel servizio Backup di Azure</span><span class="sxs-lookup"><span data-stu-id="2437f-133">Registering the VMs with the Azure Backup service</span></span>

### <a name="create-a-backup-vault"></a><span data-ttu-id="2437f-134">Creare un insieme di credenziali per il backup</span><span class="sxs-lookup"><span data-stu-id="2437f-134">Create a backup vault</span></span>
> [!WARNING]
> <span data-ttu-id="2437f-135">I clienti che usano il servizio Backup di Azure per la prima volta, dovranno registrare il provider di Backup di Azure da usare con la propria sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="2437f-135">For customers using Azure Backup for the first time, you need to register the Azure Backup provider to be used with your subscription.</span></span> <span data-ttu-id="2437f-136">A tale scopo, eseguire il comando seguente: Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Backup"</span><span class="sxs-lookup"><span data-stu-id="2437f-136">This can be done by running the following command: Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Backup"</span></span>
>
>

<span data-ttu-id="2437f-137">È possibile creare un nuovo insieme di credenziali per il backup usando il cmdlet **New-AzureRmBackupVault** .</span><span class="sxs-lookup"><span data-stu-id="2437f-137">You can create a new backup vault using the **New-AzureRmBackupVault** cmdlet.</span></span> <span data-ttu-id="2437f-138">L’archivio di backup è una risorsa ARM, pertanto è necessario inserirlo all'interno di un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="2437f-138">The backup vault is an ARM resource, so you need to place it within a Resource Group.</span></span> <span data-ttu-id="2437f-139">Eseguire i comandi seguenti in una console di Azure PowerShell con privilegi elevati:</span><span class="sxs-lookup"><span data-stu-id="2437f-139">In an elevated Azure PowerShell console, run the following commands:</span></span>

```
PS C:\> New-AzureRmResourceGroup –Name “test-rg” –Location “West US”
PS C:\> $backupvault = New-AzureRmBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GeoRedundant
```

<span data-ttu-id="2437f-140">È possibile ottenere un elenco di tutti gli insiemi di credenziali per il backup in una determinata sottoscrizione usando il cmdlet **Get-AzureRmBackupVault** .</span><span class="sxs-lookup"><span data-stu-id="2437f-140">You can get a list of all the backup vaults in a given subscription using the **Get-AzureRmBackupVault** cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="2437f-141">È consigliabile archiviare l'oggetto insieme di credenziali di backup in una variabile.</span><span class="sxs-lookup"><span data-stu-id="2437f-141">It is convenient to store the backup vault object into a variable.</span></span> <span data-ttu-id="2437f-142">L'oggetto insieme di credenziali è necessario come input per molti cmdlet di Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="2437f-142">The vault object is needed as an input for many Azure Backup cmdlets.</span></span>
>
>

### <a name="registering-the-vms"></a><span data-ttu-id="2437f-143">Registrazione delle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="2437f-143">Registering the VMs</span></span>
<span data-ttu-id="2437f-144">Il primo passaggio per la configurazione del backup nel servizio Backup di Azure prevede la registrazione del computer o della macchina virtuale in un insieme di credenziali del servizio Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="2437f-144">The first step towards configuring backup with Azure Backup is to register your machine or VM with an Azure Backup vault.</span></span> <span data-ttu-id="2437f-145">Il cmdlet **Register-AzureRmBackupContainer** accetta le informazioni di input di una macchina virtuale IaaS di Azure e le registra nell'insieme di credenziali specificato.</span><span class="sxs-lookup"><span data-stu-id="2437f-145">The **Register-AzureRmBackupContainer** cmdlet takes the input information of an Azure IaaS virtual machine and registers it with the specified vault.</span></span> <span data-ttu-id="2437f-146">L'operazione di registrazione associa la macchina virtuale di Azure all'insieme di credenziali di backup e tiene traccia della macchina virtuale per la durata del backup.</span><span class="sxs-lookup"><span data-stu-id="2437f-146">The register operation associates the Azure virtual machine with the backup vault and tracks the VM through the backup lifecycle.</span></span>

<span data-ttu-id="2437f-147">L'operazione di registrazione della macchina virtuale con il servizio Backup di Azure crea un oggetto contenitore di livello superiore.</span><span class="sxs-lookup"><span data-stu-id="2437f-147">Registering your VM with the Azure Backup service creates a top-level container object.</span></span> <span data-ttu-id="2437f-148">Un contenitore in genere contiene più elementi di cui si può eseguire il backup, ma nel caso delle macchine virtuali sarà presente un solo elemento di backup per il contenitore.</span><span class="sxs-lookup"><span data-stu-id="2437f-148">A container typically contains multiple items that can be backed up, but in the case of VMs there will be only one backup item for the container.</span></span>

```
PS C:\> $registerjob = Register-AzureRmBackupContainer -Vault $backupvault -Name "testvm" -ServiceName "testvm"
```

## <a name="backup-azure-vms"></a><span data-ttu-id="2437f-149">Macchine virtuali del servizio Backup di Azure</span><span class="sxs-lookup"><span data-stu-id="2437f-149">Backup Azure VMs</span></span>
### <a name="create-a-protection-policy"></a><span data-ttu-id="2437f-150">Creare i criteri di protezione</span><span class="sxs-lookup"><span data-stu-id="2437f-150">Create a protection policy</span></span>
<span data-ttu-id="2437f-151">Non è obbligatorio creare nuovi criteri di protezione per avviare il backup delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="2437f-151">It is not mandatory to create a new protection policy to start backup of your VMs.</span></span> <span data-ttu-id="2437f-152">Insieme di credenziali include 'criteri predefiniti' che possono essere usati per abilitare rapidamente la protezione e che possono essere modificati in un secondo momento per impostare i dettagli corretti.</span><span class="sxs-lookup"><span data-stu-id="2437f-152">The vault comes with a 'Default Policy' that can be used to quickly enable protection, and then edited later with the right details.</span></span> <span data-ttu-id="2437f-153">È possibile ottenere un elenco dei criteri disponibili usando il cmdlet **Get-AzureRmBackupProtectionPolicy** :</span><span class="sxs-lookup"><span data-stu-id="2437f-153">You can get a list of the policies available in the vault by using the **Get-AzureRmBackupProtectionPolicy** cmdlet:</span></span>

```
PS C:\> Get-AzureRmBackupProtectionPolicy -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DefaultPolicy             AzureVM            Daily              26-Aug-15 12:30:00 AM
```

> [!NOTE]
> <span data-ttu-id="2437f-154">Il fuso orario del campo BackupTime in PowerShell è UTC.</span><span class="sxs-lookup"><span data-stu-id="2437f-154">The timezone of the BackupTime field in PowerShell is UTC.</span></span> <span data-ttu-id="2437f-155">Tuttavia, quando l'orario di backup viene visualizzato nel portale di Azure, il fuso orario è allineato a quello del sistema locale assieme alla differenza dall'ora UTC.</span><span class="sxs-lookup"><span data-stu-id="2437f-155">However, when the backup time is shown in the Azure portal, the timezone is aligned to your local system along with the UTC offset.</span></span>
>
>

<span data-ttu-id="2437f-156">I criteri di backup sono associati ai criteri di conservazione.</span><span class="sxs-lookup"><span data-stu-id="2437f-156">A backup policy is associated with at least one retention policy.</span></span> <span data-ttu-id="2437f-157">I criteri di conservazione definiscono per quanto tempo un punto di ripristino viene mantenuto nel servizio Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="2437f-157">The retention policy defines how long a recovery point is kept with Azure Backup.</span></span> <span data-ttu-id="2437f-158">Il cmdlet **New-AzureRmBackupRetentionPolicy** crea oggetti PowerShell che includono le informazioni relative ai criteri di conservazione.</span><span class="sxs-lookup"><span data-stu-id="2437f-158">The **New-AzureRmBackupRetentionPolicy** cmdlet creates PowerShell objects that hold retention policy information.</span></span> <span data-ttu-id="2437f-159">Questi oggetti di criteri di conservazione vengono usati come input per il cmdlet *New-AzureRmBackupProtectionPolicy* o direttamente con il cmdlet *Enable-AzureRmBackupProtection*.</span><span class="sxs-lookup"><span data-stu-id="2437f-159">These retention policy objects are used as inputs to the *New-AzureRmBackupProtectionPolicy* cmdlet, or directly with the *Enable-AzureRmBackupProtection* cmdlet.</span></span>

<span data-ttu-id="2437f-160">I criteri di backup consentono di definire quando viene eseguito il backup di un elemento e con quale frequenza.</span><span class="sxs-lookup"><span data-stu-id="2437f-160">A backup policy defines when and how often the backup of an item is done.</span></span> <span data-ttu-id="2437f-161">Il cmdlet **New-AzureRmBackupProtectionPolicy** crea un oggetto PowerShell che contiene le informazioni relative ai criteri di backup.</span><span class="sxs-lookup"><span data-stu-id="2437f-161">The **New-AzureRmBackupProtectionPolicy** cmdlet creates a PowerShell object that holds backup policy information.</span></span> <span data-ttu-id="2437f-162">I criteri di backup vengono usati come input per il cmdlet *Enable-AzureRmBackupProtection* .</span><span class="sxs-lookup"><span data-stu-id="2437f-162">The backup policy is used as an input to the *Enable-AzureRmBackupProtection* cmdlet.</span></span>

```
PS C:\> $Daily = New-AzureRmBackupRetentionPolicyObject -DailyRetention -Retention 30
PS C:\> $newpolicy = New-AzureRmBackupProtectionPolicy -Name DailyBackup01 -Type AzureVM -Daily -BackupTime ([datetime]"3:30 PM") -RetentionPolicy $Daily -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DailyBackup01             AzureVM            Daily              01-Sep-15 3:30:00 PM
```

### <a name="enable-protection"></a><span data-ttu-id="2437f-163">Abilitare la protezione</span><span class="sxs-lookup"><span data-stu-id="2437f-163">Enable protection</span></span>
<span data-ttu-id="2437f-164">Per abilitare la protezione sono necessari due oggetti, l'elemento e i criteri, ed entrambi devono appartenere allo stesso insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="2437f-164">Enabling protection involves two objects - the Item and the Policy, and both need to belong to the same vault.</span></span> <span data-ttu-id="2437f-165">Dopo aver associato i criteri all'elemento, il flusso di lavoro di backup verrà avviato in base alla pianificazione del backup.</span><span class="sxs-lookup"><span data-stu-id="2437f-165">Once the policy has been associated with the item, the backup workflow will kick in at the defined schedule.</span></span>

```
PS C:\> Get-AzureRmBackupContainer -Type AzureVM -Status Registered -Vault $backupvault | Get-AzureRmBackupItem | Enable-AzureRmBackupProtection -Policy $newpolicy
```

### <a name="initial-backup"></a><span data-ttu-id="2437f-166">Backup iniziale</span><span class="sxs-lookup"><span data-stu-id="2437f-166">Initial backup</span></span>
<span data-ttu-id="2437f-167">La pianificazione del backup esegue la copia iniziale completa dell'elemento e la copia incrementale per i backup successivi.</span><span class="sxs-lookup"><span data-stu-id="2437f-167">The backup schedule will take care of doing the full initial copy for the item and the incremental copy for the subsequent backups.</span></span> <span data-ttu-id="2437f-168">Se si vuole forzare il backup iniziale in modo che venga eseguito a una determinata ora o immediatamente, usare il cmdlet **Backup-AzureRmBackupItem** :</span><span class="sxs-lookup"><span data-stu-id="2437f-168">However, if you want to force the initial backup to happen at a certain time or even immediately then use the **Backup-AzureRmBackupItem** cmdlet:</span></span>

```
PS C:\> $container = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -Name "testvm"
PS C:\> $backupjob = Get-AzureRmBackupItem -Container $container | Backup-AzureRmBackupItem
PS C:\> $backupjob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

> [!NOTE]
> <span data-ttu-id="2437f-169">Il fuso orario dei campi StartTime ed EndTime visualizzati in PowerShell è UTC.</span><span class="sxs-lookup"><span data-stu-id="2437f-169">The timezone of the StartTime and EndTime fields shown in PowerShell is UTC.</span></span> <span data-ttu-id="2437f-170">Tuttavia, quando le informazioni corrispondenti vengono visualizzate nel portale di Azure, il fuso orario è allineato a quello dell'orologio del sistema locale.</span><span class="sxs-lookup"><span data-stu-id="2437f-170">However, when the similar information is shown in the Azure portal, the timezone is aligned to your local system clock.</span></span>
>
>

### <a name="monitoring-a-backup-job"></a><span data-ttu-id="2437f-171">Monitoraggio di un processo di backup</span><span class="sxs-lookup"><span data-stu-id="2437f-171">Monitoring a backup job</span></span>
<span data-ttu-id="2437f-172">La maggior parte delle operazioni a esecuzione prolungata in Azure Backup è modellata come processo.</span><span class="sxs-lookup"><span data-stu-id="2437f-172">Most long-running operations in Azure Backup are modelled as a job.</span></span> <span data-ttu-id="2437f-173">Questo consente di semplificare il monitoraggio dell'avanzamento senza dover tenere aperto continuamente il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2437f-173">This makes it easy to track progress without having to keep the Azure portal open at all times.</span></span>

<span data-ttu-id="2437f-174">Per ottenere lo stato più recente di un processo in corso, usare il cmdlet **Get-AzureRmBackupJob** .</span><span class="sxs-lookup"><span data-stu-id="2437f-174">To get the latest status of an in-progress job, use the **Get-AzureRmBackupJob** cmdlet.</span></span>

```
PS C:\> $joblist = Get-AzureRmBackupJob -Vault $backupvault -Status InProgress
PS C:\> $joblist[0]

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

<span data-ttu-id="2437f-175">Invece di eseguire il poll dei processi per ottenere lo stato di completamento, operazione non necessaria che prevede codice aggiuntivo, è più facile usare il cmdlet **Wait-AzureRmBackupJob** .</span><span class="sxs-lookup"><span data-stu-id="2437f-175">Instead of polling these jobs for completion - which is unnecessary, additional code - it is simpler to use the **Wait-AzureRmBackupJob** cmdlet.</span></span> <span data-ttu-id="2437f-176">Se usato in uno script, il cmdlet sospende l'esecuzione fino al completamento del processo o fino a quando non viene raggiunto il valore di timeout specificato.</span><span class="sxs-lookup"><span data-stu-id="2437f-176">When used in a script, the cmdlet will pause the execution until either the job completes or the specified timeout value is reached.</span></span>

```
PS C:\> Wait-AzureRmBackupJob -Job $joblist[0] -Timeout 43200
```


## <a name="restore-an-azure-vm"></a><span data-ttu-id="2437f-177">Ripristinare una macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="2437f-177">Restore an Azure VM</span></span>
<span data-ttu-id="2437f-178">Per ripristinare i dati di backup, è necessario identificare l'elemento sottoposto a backup e il punto di ripristino che contiene i dati temporizzati.</span><span class="sxs-lookup"><span data-stu-id="2437f-178">In order to restore backup data, you need to identify the backed-up Item and the Recovery Point that holds the point-in-time data.</span></span> <span data-ttu-id="2437f-179">Queste informazioni vengono fornite al cmdlet Restore-AzureRmBackupItem per avviare un ripristino dei dati dall'insieme di credenziali all'account del cliente.</span><span class="sxs-lookup"><span data-stu-id="2437f-179">This information is supplied to the Restore-AzureRmBackupItem cmdlet to initiate a restore of data from the vault to the customer's account.</span></span>

### <a name="select-the-vm"></a><span data-ttu-id="2437f-180">Selezionare la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="2437f-180">Select the VM</span></span>
<span data-ttu-id="2437f-181">Per ottenere l'oggetto PowerShell che individua l'elemento di backup corretto, è necessario iniziare dal contenitore nell'insieme di credenziali, quindi procedere verso il basso nella gerarchia degli oggetti.</span><span class="sxs-lookup"><span data-stu-id="2437f-181">To get the PowerShell object that identifies the right backup Item, you need to start from the Container in the vault, and work your way down object hierarchy.</span></span> <span data-ttu-id="2437f-182">Per selezionare il contenitore che rappresenta la VM, usare il cmdlet **Get-AzureRmBackupContainer** e inviarlo tramite pipe al cmdlet **Get-AzureRmBackupItem**.</span><span class="sxs-lookup"><span data-stu-id="2437f-182">To select the container that represents the VM, use the **Get-AzureRmBackupContainer** cmdlet and pipe that to the **Get-AzureRmBackupItem** cmdlet.</span></span>

```
PS C:\> $backupitem = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -name "testvm" | Get-AzureRmBackupItem
```

### <a name="choose-a-recovery-point"></a><span data-ttu-id="2437f-183">Scegliere un punto di ripristino</span><span class="sxs-lookup"><span data-stu-id="2437f-183">Choose a recovery point</span></span>
<span data-ttu-id="2437f-184">A questo punto è possibile visualizzare l'elenco di tutti i punti di ripristino per l'elemento di backup usando il cmdlet **Get-AzureRmBackupRecoveryPoint** e scegliere il punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="2437f-184">You can now list all the recovery points for the backup item using the **Get-AzureRmBackupRecoveryPoint** cmdlet, and choose the recovery point to restore.</span></span> <span data-ttu-id="2437f-185">In genere, gli utenti selezionano il punto di ripristino *AppConsistent* più recente nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="2437f-185">Typically users pick the most recent *AppConsistent* point in the list.</span></span>

```
PS C:\> $rp =  Get-AzureRmBackupRecoveryPoint -Item $backupitem
PS C:\> $rp

RecoveryPointId    RecoveryPointType  RecoveryPointTime      ContainerName
---------------    -----------------  -----------------      -------------
15273496567119     AppConsistent      01-Sep-15 12:27:38 PM  iaasvmcontainer;testvm;testv...
```

<span data-ttu-id="2437f-186">La variabile ```$rp``` è una matrice di punti di ripristino per l'elemento di backup selezionato, in ordine cronologico inverso: il punto di ripristino più recente è all'indice 0.</span><span class="sxs-lookup"><span data-stu-id="2437f-186">The variable ```$rp``` is an array of recovery points for the selected backup item, sorted in reverse order of time - the latest recovery point is at index 0.</span></span> <span data-ttu-id="2437f-187">Per scegliere il punto di ripristino, usare l'indicizzazione standard della matrice di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2437f-187">Use standard PowerShell array indexing to pick the recovery point.</span></span> <span data-ttu-id="2437f-188">Ad esempio, ```$rp[0]``` selezionerà l'ultimo punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="2437f-188">For example: ```$rp[0]``` will select the latest recovery point.</span></span>

### <a name="restoring-disks"></a><span data-ttu-id="2437f-189">Ripristino dei dischi</span><span class="sxs-lookup"><span data-stu-id="2437f-189">Restoring disks</span></span>
<span data-ttu-id="2437f-190">Le operazioni di ripristino eseguite tramite il portale di Azure e tramite Azure PowerShell presentano una differenza importante.</span><span class="sxs-lookup"><span data-stu-id="2437f-190">There is a key difference between the restore operations done through the Azure portal and through Azure PowerShell.</span></span> <span data-ttu-id="2437f-191">Con PowerShell, l'operazione di ripristino si arresta una volta ripristinati i dischi e le informazioni di configurazione dal punto di ripristino</span><span class="sxs-lookup"><span data-stu-id="2437f-191">With PowerShell, the restore operation stops at restoring the disks and config information from the recovery point.</span></span> <span data-ttu-id="2437f-192">e non crea una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="2437f-192">It does not create a virtual machine.</span></span>

> [!WARNING]
> <span data-ttu-id="2437f-193">Il cmdlet Restore-AzureRmBackupItem non crea una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="2437f-193">The Restore-AzureRmBackupItem does not create a VM.</span></span> <span data-ttu-id="2437f-194">Ripristina semplicemente i dischi nell'account di archiviazione specificato.</span><span class="sxs-lookup"><span data-stu-id="2437f-194">It only restores the disks to the specified storage account.</span></span> <span data-ttu-id="2437f-195">L'operazione di ripristino tramite il portale di Azure prevede un comportamento diverso.</span><span class="sxs-lookup"><span data-stu-id="2437f-195">This is not the same behavior you will experience in the Azure portal.</span></span>
>
>

```
PS C:\> $restorejob = Restore-AzureRmBackupItem -StorageAccountName "DestAccount" -RecoveryPoint $rp[0]
PS C:\> $restorejob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Restore         InProgress      01-Sep-15 1:14:01 PM   01-Jan-01 12:00:00 AM
```

<span data-ttu-id="2437f-196">È possibile ottenere i dettagli dell'operazione di ripristino usando il cmdlet **Get-AzureRmBackupJobDetails** al termine del processo di ripristino.</span><span class="sxs-lookup"><span data-stu-id="2437f-196">You can get the details of the restore operation using the **Get-AzureRmBackupJobDetails** cmdlet once the Restore job has completed.</span></span> <span data-ttu-id="2437f-197">La proprietà *ErrorDetails* conterrà le informazioni necessarie per ricreare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="2437f-197">The *ErrorDetails* property will have the information needed to rebuild the VM.</span></span>

```
PS C:\> $restorejob = Get-AzureRmBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmBackupJobDetails -Job $restorejob
```

### <a name="build-the-vm"></a><span data-ttu-id="2437f-198">Creare la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="2437f-198">Build the VM</span></span>
<span data-ttu-id="2437f-199">È possibile creare la macchina virtuale dai dischi ripristinati tramite i cmdlet di PowerShell per la gestione del servizio Azure precedenti, i nuovi modelli di Azure Resource Manager o il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2437f-199">Building the VM out of the restored disks can be done using the older Azure Service Management PowerShell cmdlets, the new Azure Resource Manager templates, or even using the Azure portal.</span></span> <span data-ttu-id="2437f-200">Questo esempio rapido mostra come eseguire l'operazione usando i cmdlet per la gestione del servizio Azure.</span><span class="sxs-lookup"><span data-stu-id="2437f-200">In a quick example, we will show how to get there using the Azure Service Management cmdlets.</span></span>

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

<span data-ttu-id="2437f-201">Per altre informazioni su come creare una macchina virtuale dai dischi ripristinati, vedere i cmdlet seguenti:</span><span class="sxs-lookup"><span data-stu-id="2437f-201">For more information on how to build a VM from the restored disks, read about the following cmdlets:</span></span>

* [<span data-ttu-id="2437f-202">Add-AzureDisk</span><span class="sxs-lookup"><span data-stu-id="2437f-202">Add-AzureDisk</span></span>](https://msdn.microsoft.com/library/azure/dn495252.aspx)
* [<span data-ttu-id="2437f-203">New-AzureVMConfig</span><span class="sxs-lookup"><span data-stu-id="2437f-203">New-AzureVMConfig</span></span>](https://msdn.microsoft.com/library/azure/dn495159.aspx)
* [<span data-ttu-id="2437f-204">New-AzureVM</span><span class="sxs-lookup"><span data-stu-id="2437f-204">New-AzureVM</span></span>](https://msdn.microsoft.com/library/azure/dn495254.aspx)

## <a name="code-samples"></a><span data-ttu-id="2437f-205">Esempi di codice</span><span class="sxs-lookup"><span data-stu-id="2437f-205">Code samples</span></span>
### <a name="1-get-the-completion-status-of-job-sub-tasks"></a><span data-ttu-id="2437f-206">1. Ottenere lo stato di completamento delle sottoattività dei processi</span><span class="sxs-lookup"><span data-stu-id="2437f-206">1. Get the completion status of job sub-tasks</span></span>
<span data-ttu-id="2437f-207">Per monitorare lo stato di completamento delle singole sottoattività si può usare il cmdlet **Get-AzureRmBackupJobDetails** :</span><span class="sxs-lookup"><span data-stu-id="2437f-207">To track the completion status of individual sub-tasks, you can use the **Get-AzureRmBackupJobDetails** cmdlet:</span></span>

```
PS C:\> $details = Get-AzureRmBackupJobDetails -JobId $backupjob.InstanceId -Vault $backupvault
PS C:\> $details.SubTasks

Name                                                        Status
----                                                        ------
Take Snapshot                                               Completed
Transfer data to Backup vault                               InProgress
```

### <a name="2-create-a-dailyweekly-report-of-backup-jobs"></a><span data-ttu-id="2437f-208">2. Creare un report settimanale o giornaliero dei processi di backup</span><span class="sxs-lookup"><span data-stu-id="2437f-208">2. Create a daily/weekly report of backup jobs</span></span>
<span data-ttu-id="2437f-209">In genere, gli amministratori vogliono sapere quali processi di backup sono stati eseguiti nelle ultime 24 ore e conoscerne lo stato.</span><span class="sxs-lookup"><span data-stu-id="2437f-209">Administrators typically want to know what backup jobs ran in the last 24 hours, the status of those backup jobs.</span></span> <span data-ttu-id="2437f-210">Inoltre, conoscere la quantità di dati trasferiti consente agli amministratori di valutare l'utilizzo mensile di dati.</span><span class="sxs-lookup"><span data-stu-id="2437f-210">Additionally, the amount of data transferred gives administrators a way to estimate their monthly data usage.</span></span> <span data-ttu-id="2437f-211">Lo script seguente estrae i dati non elaborati dal servizio Azure Backup e visualizza le informazioni nella console di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2437f-211">The script below pulls the raw data from the Azure Backup service and displays the information in the PowerShell console.</span></span>

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
    $dailyjoblist = Get-AzureRmBackupJob -Vault $backupvault -From $startdate -To $enddate -Type AzureVM -Operation Backup
    Write-Progress -Activity "Getting job information for the last $numberofdays days" -Status "Day -$i" -PercentComplete ([int]([decimal]$i*100/$numberofdays))

    foreach( $job in $dailyjoblist )
    {
        #Extract the information for the reports
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

<span data-ttu-id="2437f-212">Se si vogliono aggiungere funzionalità per la creazione di grafici all'output del report, leggere il post [Charting with PowerShell](http://blogs.technet.com/b/richard_macdonald/archive/2009/04/28/3231887.aspx)</span><span class="sxs-lookup"><span data-stu-id="2437f-212">If you want to add charting capabilities to this report output, learn from the TechNet blog post [Charting with PowerShell](http://blogs.technet.com/b/richard_macdonald/archive/2009/04/28/3231887.aspx)</span></span>

## <a name="next-steps"></a><span data-ttu-id="2437f-213">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2437f-213">Next steps</span></span>
<span data-ttu-id="2437f-214">Se si preferisce usare PowerShell per interagire con le risorse di Azure, vedere l'articolo relativo a PowerShell per la protezione di Windows Server, [Distribuire e gestire il backup per Windows Server](backup-client-automation-classic.md).</span><span class="sxs-lookup"><span data-stu-id="2437f-214">If you prefer using PowerShell to engage with your Azure resources, check out the PowerShell article for protecting Windows Server, [Deploy and Manage Backup for Windows Server](backup-client-automation-classic.md).</span></span> <span data-ttu-id="2437f-215">È disponibile anche un articolo relativo a PowerShell per la gestione dei backup di DPM, [Distribuire e gestire il backup per DPM](backup-dpm-automation-classic.md).</span><span class="sxs-lookup"><span data-stu-id="2437f-215">There is also a PowerShell article for managing DPM backups, [Deploy and Manage Backup for DPM](backup-dpm-automation-classic.md).</span></span> <span data-ttu-id="2437f-216">Entrambi gli articoli prevedono due versioni: una per la distribuzione con Resource Manager, l’altra per la distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="2437f-216">Both of these articles have a version for Resource Manager deployments as well as Classic deployments.</span></span>
