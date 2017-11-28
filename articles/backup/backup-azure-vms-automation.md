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
# <a name="use-azurermrecoveryservicesbackup-cmdlets-tooback-up-virtual-machines"></a><span data-ttu-id="3be34-103">Utilizzare AzureRM.RecoveryServices.Backup cmdlet tooback backup di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="3be34-103">Use AzureRM.RecoveryServices.Backup cmdlets tooback up virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3be34-104">Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="3be34-104">Resource Manager</span></span>](backup-azure-vms-automation.md)
> * [<span data-ttu-id="3be34-105">Classico</span><span class="sxs-lookup"><span data-stu-id="3be34-105">Classic</span></span>](backup-azure-vms-classic-automation.md)
>
>

<span data-ttu-id="3be34-106">Questo articolo illustra come tooback i cmdlet di Azure PowerShell toouse backup e ripristinare una macchina virtuale di Azure (VM) da servizi di ripristino di un insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="3be34-106">This article shows you how toouse Azure PowerShell cmdlets tooback up and recover an Azure virtual machine (VM) from a Recovery Services vault.</span></span> <span data-ttu-id="3be34-107">Un insieme di credenziali di servizi di ripristino è una risorsa di gestione risorse di Azure ed è utilizzato tooprotect dati e risorse in servizi di Backup di Azure e Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="3be34-107">A Recovery Services vault is an Azure Resource Manager resource and is used tooprotect data and assets in both Azure Backup and Azure Site Recovery services.</span></span> <span data-ttu-id="3be34-108">È possibile utilizzare un tooprotect insieme di credenziali di servizi di ripristino distribuito Service Manager di Azure le macchine virtuali e macchine virtuali distribuite di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="3be34-108">You can use a Recovery Services vault tooprotect Azure Service Manager-deployed VMs, and Azure Resource Manager-deployed VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="3be34-109">Azure offre due modelli di distribuzione per creare e usare le risorse: [Resource Manager e distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="3be34-109">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="3be34-110">In questo articolo è per l'utilizzo con macchine virtuali create utilizzando il modello di gestione risorse hello.</span><span class="sxs-lookup"><span data-stu-id="3be34-110">This article is for use with VMs created using hello Resource Manager model.</span></span>
>
>

<span data-ttu-id="3be34-111">In questo articolo illustra utilizzando PowerShell tooprotect una macchina virtuale e ripristino di dati da un punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="3be34-111">This article walks you through using PowerShell tooprotect a VM, and restore data from a recovery point.</span></span>

## <a name="concepts"></a><span data-ttu-id="3be34-112">Concetti</span><span class="sxs-lookup"><span data-stu-id="3be34-112">Concepts</span></span>
<span data-ttu-id="3be34-113">Se non si ha familiarità con il servizio di Backup di Azure, per una panoramica del servizio di hello, hello estrarre [che cos'è Azure Backup?](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="3be34-113">If you are not familiar with hello Azure Backup service, for an overview of hello service, check out [What is Azure Backup?](backup-introduction-to-azure-backup.md)</span></span> <span data-ttu-id="3be34-114">Prima di iniziare, assicurarsi che riguardano essentials hello su hello prerequisiti necessari toowork con Backup di Azure e hello limitazioni di hello VM soluzione di backup corrente.</span><span class="sxs-lookup"><span data-stu-id="3be34-114">Before you start, ensure that you cover hello essentials about hello prerequisites needed toowork with Azure Backup, and hello limitations of hello current VM backup solution.</span></span>

<span data-ttu-id="3be34-115">toouse PowerShell in modo efficace, si tratta di toounderstand necessario hello gerarchia di oggetti e da dove toostart.</span><span class="sxs-lookup"><span data-stu-id="3be34-115">toouse PowerShell effectively, it is necessary toounderstand hello hierarchy of objects and from where toostart.</span></span>

![Gerarchia di oggetti dei servizi di ripristino](./media/backup-azure-vms-arm-automation/recovery-services-object-hierarchy.png)

<span data-ttu-id="3be34-117">hello tooview AzureRm.RecoveryServices.Backup Guida di riferimento, vedere hello [Backup di Azure - cmdlet di servizi di ripristino](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup) in hello libreria di Azure.</span><span class="sxs-lookup"><span data-stu-id="3be34-117">tooview hello AzureRm.RecoveryServices.Backup PowerShell cmdlet reference, see hello [Azure Backup - Recovery Services Cmdlets](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup) in hello Azure library.</span></span>

## <a name="setup-and-registration"></a><span data-ttu-id="3be34-118">Installazione e registrazione</span><span class="sxs-lookup"><span data-stu-id="3be34-118">Setup and Registration</span></span>
<span data-ttu-id="3be34-119">toobegin:</span><span class="sxs-lookup"><span data-stu-id="3be34-119">toobegin:</span></span>

1. <span data-ttu-id="3be34-120">[Scaricare hello la versione più recente di PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) (hello versione minima richiesta è: 1.4.0)</span><span class="sxs-lookup"><span data-stu-id="3be34-120">[Download hello latest version of PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) (hello minimum version required is: 1.4.0)</span></span>
2. <span data-ttu-id="3be34-121">Trovare i cmdlet di PowerShell di Azure Backup hello disponibili digitando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="3be34-121">Find hello Azure Backup PowerShell cmdlets available by typing hello following command:</span></span>

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


<span data-ttu-id="3be34-122">con PowerShell, è possibile automatizzare Hello seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="3be34-122">hello following tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="3be34-123">Creare un insieme di credenziali di Servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="3be34-123">Create a Recovery Services vault</span></span>
* <span data-ttu-id="3be34-124">Eseguire il backup delle VM di Azure</span><span class="sxs-lookup"><span data-stu-id="3be34-124">Back up Azure VMs</span></span>
* <span data-ttu-id="3be34-125">Attivare un processo di backup</span><span class="sxs-lookup"><span data-stu-id="3be34-125">Trigger a backup job</span></span>
* <span data-ttu-id="3be34-126">Monitorare un processo di backup</span><span class="sxs-lookup"><span data-stu-id="3be34-126">Monitor a backup job</span></span>
* <span data-ttu-id="3be34-127">Ripristinare una macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="3be34-127">Restore an Azure VM</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="3be34-128">Creare un insieme di credenziali di Servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="3be34-128">Create a recovery services vault</span></span>
<span data-ttu-id="3be34-129">Hello alla procedura seguente per facilitare la creazione di un insieme di credenziali di servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="3be34-129">hello following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="3be34-130">Un insieme di credenziali dei servizi di ripristino è diverso da un insieme di credenziali di backup.</span><span class="sxs-lookup"><span data-stu-id="3be34-130">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="3be34-131">Se si utilizza Azure Backup per hello prima volta, è necessario utilizzare hello  **[registro AzureRmResourceProvider](http://docs.microsoft.com/powershell/module/azurerm.resources/register-azurermresourceprovider)**  provider di servizi di ripristino di Azure di cmdlet tooregister hello con la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="3be34-131">If you are using Azure Backup for hello first time, you must use hello **[Register-AzureRmResourceProvider](http://docs.microsoft.com/powershell/module/azurerm.resources/register-azurermresourceprovider)** cmdlet tooregister hello Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="3be34-132">Hello insieme di credenziali di servizi di ripristino è una risorsa di gestione delle risorse, pertanto è necessario tooplace all'interno di un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="3be34-132">hello Recovery Services vault is a Resource Manager resource, so you need tooplace it within a resource group.</span></span> <span data-ttu-id="3be34-133">È possibile utilizzare un gruppo di risorse esistente o creare un gruppo di risorse con hello  **[New AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup)**  cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3be34-133">You can use an existing resource group, or create a resource group with hello **[New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup)** cmdlet.</span></span> <span data-ttu-id="3be34-134">Quando si crea un gruppo di risorse, specificare nome hello e il percorso per il gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="3be34-134">When creating a resource group, specify hello name and location for hello resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. <span data-ttu-id="3be34-135">Hello utilizzare  **[New AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault)**  hello toocreate cmdlet dell'insieme di credenziali di servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="3be34-135">Use hello **[New-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault)** cmdlet toocreate hello Recovery Services vault.</span></span> <span data-ttu-id="3be34-136">Assicurarsi che toospecify hello stesso percorso per l'insieme di credenziali hello utilizzata per il gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="3be34-136">Be sure toospecify hello same location for hello vault as was used for hello resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. <span data-ttu-id="3be34-137">Specificare il tipo di hello di toouse di ridondanza di archiviazione; è possibile utilizzare [archiviazione con ridondanza locale (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) o [archiviazione con ridondanza geografica (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="3be34-137">Specify hello type of storage redundancy toouse; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="3be34-138">Hello riportato di seguito hello - BackupStorageRedundancy per testvault impostazione tooGeoRedundant.</span><span class="sxs-lookup"><span data-stu-id="3be34-138">hello following example shows hello -BackupStorageRedundancy option for testvault is set tooGeoRedundant.</span></span>

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testvault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -Vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

   > [!TIP]
   > <span data-ttu-id="3be34-139">Molti cmdlet di Azure Backup richiede l'oggetto insieme di credenziali di servizi di ripristino hello come input.</span><span class="sxs-lookup"><span data-stu-id="3be34-139">Many Azure Backup cmdlets require hello Recovery Services vault object as an input.</span></span> <span data-ttu-id="3be34-140">Per questo motivo, è utile toostore hello servizi di ripristino di Backup dell'insieme di credenziali oggetto in una variabile.</span><span class="sxs-lookup"><span data-stu-id="3be34-140">For this reason, it is convenient toostore hello Backup Recovery Services vault object in a variable.</span></span>
   >
   >

## <a name="view-hello-vaults-in-a-subscription"></a><span data-ttu-id="3be34-141">Visualizza gli insiemi di credenziali hello in una sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="3be34-141">View hello vaults in a subscription</span></span>
<span data-ttu-id="3be34-142">Utilizzare  **[Get AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/get-azurermrecoveryservicesvault)**  elenco hello tooview di tutti gli insiemi di credenziali nella sottoscrizione corrente hello.</span><span class="sxs-lookup"><span data-stu-id="3be34-142">Use **[Get-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/get-azurermrecoveryservicesvault)** tooview hello list of all vaults in hello current subscription.</span></span> <span data-ttu-id="3be34-143">È possibile utilizzare questo toocheck di comando che è stato creato un nuovo insieme di credenziali o toosee hello gli insiemi di credenziali disponibili nella sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="3be34-143">You can use this command toocheck that a new vault was created, or toosee hello available vaults in hello subscription.</span></span>

<span data-ttu-id="3be34-144">Eseguire hello tooview di comando, Get-AzureRmRecoveryServicesVault, tutti gli insiemi di credenziali nella sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="3be34-144">Run hello command, Get-AzureRmRecoveryServicesVault, tooview all vaults in hello subscription.</span></span> <span data-ttu-id="3be34-145">Hello riportato di seguito informazioni hello visualizzate per ogni insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="3be34-145">hello following example shows hello information displayed for each vault.</span></span>

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


## <a name="back-up-azure-vms"></a><span data-ttu-id="3be34-146">Eseguire il backup delle VM di Azure</span><span class="sxs-lookup"><span data-stu-id="3be34-146">Back up Azure VMs</span></span>
<span data-ttu-id="3be34-147">Utilizzare un tooprotect insieme di credenziali di servizi di ripristino le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="3be34-147">Use a Recovery Services vault tooprotect your virtual machines.</span></span> <span data-ttu-id="3be34-148">Prima di applicare la protezione di hello, impostare il contesto di insieme di credenziali hello (tipo hello dei dati protetti nell'insieme di credenziali hello) e verificare i criteri di protezione hello.</span><span class="sxs-lookup"><span data-stu-id="3be34-148">Before you apply hello protection, set hello vault context (hello type of data protected in hello vault), and verify hello protection policy.</span></span> <span data-ttu-id="3be34-149">criteri di protezione Hello sono pianificazione hello quando esegue i processi di backup hello e il periodo di conservazione di ogni snapshot di backup.</span><span class="sxs-lookup"><span data-stu-id="3be34-149">hello protection policy is hello schedule when hello backup jobs run, and how long each backup snapshot is retained.</span></span>

### <a name="set-vault-context"></a><span data-ttu-id="3be34-150">Impostazione del contesto dell'insieme di credenziali</span><span class="sxs-lookup"><span data-stu-id="3be34-150">Set vault context</span></span>
<span data-ttu-id="3be34-151">Prima di abilitare la protezione per una macchina virtuale, utilizzare  **[Set AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)**  contesto di tooset hello insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="3be34-151">Before enabling protection on a VM, use **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)** tooset hello vault context.</span></span> <span data-ttu-id="3be34-152">Dopo aver impostato il contesto di insieme di credenziali hello, si applica cmdlet successivi tooall.</span><span class="sxs-lookup"><span data-stu-id="3be34-152">Once hello vault context is set, it applies tooall subsequent cmdlets.</span></span> <span data-ttu-id="3be34-153">esempio Hello Imposta contesto di insieme di credenziali hello per insieme di credenziali hello *testvault*.</span><span class="sxs-lookup"><span data-stu-id="3be34-153">hello following example sets hello vault context for hello vault, *testvault*.</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesVault -Name "testvault" | Set-AzureRmRecoveryServicesVaultContext
```

### <a name="create-a-protection-policy"></a><span data-ttu-id="3be34-154">Creare i criteri di protezione</span><span class="sxs-lookup"><span data-stu-id="3be34-154">Create a protection policy</span></span>
<span data-ttu-id="3be34-155">Quando si crea un insieme di credenziali di Servizi di ripristino, questo è dotato di protezione predefinita e criteri di conservazione.</span><span class="sxs-lookup"><span data-stu-id="3be34-155">When you create a Recovery Services vault, it comes with default protection and retention policies.</span></span> <span data-ttu-id="3be34-156">criteri di protezione predefinito Hello avvia un processo di backup ogni giorno a un'ora specificata.</span><span class="sxs-lookup"><span data-stu-id="3be34-156">hello default protection policy triggers a backup job each day at a specified time.</span></span> <span data-ttu-id="3be34-157">criteri di conservazione predefiniti Hello mantiene il punto di ripristino giornaliero hello per 30 giorni.</span><span class="sxs-lookup"><span data-stu-id="3be34-157">hello default retention policy retains hello daily recovery point for 30 days.</span></span> <span data-ttu-id="3be34-158">È possibile utilizzare predefinito hello tooquickly criteri proteggere la macchina virtuale e modificare il criterio di hello in un secondo momento con diversi dettagli.</span><span class="sxs-lookup"><span data-stu-id="3be34-158">You can use hello default policy tooquickly protect your VM and edit hello policy later with different details.</span></span>

<span data-ttu-id="3be34-159">Utilizzare  **[Get AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupprotectionpolicy)**  criteri di protezione hello tooview nell'insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="3be34-159">Use **[Get-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupprotectionpolicy)** tooview hello protection policies in hello vault.</span></span> <span data-ttu-id="3be34-160">È possibile utilizzare questo tooget cmdlet criteri specifici o criteri di hello tooview associata a un tipo di carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="3be34-160">You can use this cmdlet tooget a specific policy, or tooview hello policies associated with a workload type.</span></span> <span data-ttu-id="3be34-161">Hello di esempio seguente ottiene i criteri per il tipo di carico di lavoro, AzureVM.</span><span class="sxs-lookup"><span data-stu-id="3be34-161">hello following example gets policies for workload type, AzureVM.</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesBackupProtectionPolicy -WorkloadType "AzureVM"
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
DefaultPolicy        AzureVM            AzureVM              4/14/2016 5:00:00 PM
```

> [!NOTE]
> <span data-ttu-id="3be34-162">fuso orario di Hello del campo BackupTime hello in PowerShell è UTC.</span><span class="sxs-lookup"><span data-stu-id="3be34-162">hello timezone of hello BackupTime field in PowerShell is UTC.</span></span> <span data-ttu-id="3be34-163">Tuttavia, se l'ora del backup hello viene visualizzato nel portale di Azure hello, hello è fuso orario locale tooyour adattata.</span><span class="sxs-lookup"><span data-stu-id="3be34-163">However, when hello backup time is shown in hello Azure portal, hello time is adjusted tooyour local timezone.</span></span>
>
>

<span data-ttu-id="3be34-164">I criteri di protezione del backup sono associati almeno a un criterio di conservazione.</span><span class="sxs-lookup"><span data-stu-id="3be34-164">A backup protection policy is associated with at least one retention policy.</span></span> <span data-ttu-id="3be34-165">I criteri di conservazione definiscono per quanto tempo un punto di recupero viene mantenuto prima dell'eliminazione.</span><span class="sxs-lookup"><span data-stu-id="3be34-165">Retention policy defines how long a recovery point is kept before it is deleted.</span></span> <span data-ttu-id="3be34-166">Utilizzare  **[Get AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupretentionpolicyobject)**  criteri di conservazione predefiniti tooview hello.</span><span class="sxs-lookup"><span data-stu-id="3be34-166">Use **[Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupretentionpolicyobject)** tooview hello default retention policy.</span></span>  <span data-ttu-id="3be34-167">Analogamente è possibile utilizzare  **[Get AzureRmRecoveryServicesBackupSchedulePolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupschedulepolicyobject)**  tooobtain hello pianificazione criterio.</span><span class="sxs-lookup"><span data-stu-id="3be34-167">Similarly you can use **[Get-AzureRmRecoveryServicesBackupSchedulePolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupschedulepolicyobject)** tooobtain hello default schedule policy.</span></span> <span data-ttu-id="3be34-168">Hello  **[New AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)**  cmdlet crea un oggetto PowerShell che contiene informazioni sui criteri di backup.</span><span class="sxs-lookup"><span data-stu-id="3be34-168">hello **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)** cmdlet creates a PowerShell object that holds backup policy information.</span></span> <span data-ttu-id="3be34-169">Hello gli oggetti Criteri di conservazione e pianificazione vengono utilizzati come input toohello  **[New AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)**  cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3be34-169">hello schedule and retention policy objects are used as inputs toohello **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)** cmdlet.</span></span> <span data-ttu-id="3be34-170">Hello esempio archivia il criterio di pianificazione hello e criteri di conservazione hello nelle variabili.</span><span class="sxs-lookup"><span data-stu-id="3be34-170">hello following example stores hello schedule policy and hello retention policy in variables.</span></span> <span data-ttu-id="3be34-171">esempio Hello utilizza tali parametri di hello toodefine di variabili durante la creazione di un criterio di protezione, *NewPolicy*.</span><span class="sxs-lookup"><span data-stu-id="3be34-171">hello example uses those variables toodefine hello parameters when creating a protection policy, *NewPolicy*.</span></span>

```
PS C:\> $schPol = Get-AzureRmRecoveryServicesBackupSchedulePolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> New-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy" -WorkloadType "AzureVM" -RetentionPolicy $retPol -SchedulePolicy $schPol
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
NewPolicy           AzureVM            AzureVM              4/24/2016 1:30:00 AM
```


### <a name="enable-protection"></a><span data-ttu-id="3be34-172">Abilitare la protezione</span><span class="sxs-lookup"><span data-stu-id="3be34-172">Enable protection</span></span>
<span data-ttu-id="3be34-173">Dopo aver definito i criteri di protezione backup hello, è comunque necessario abilitare i criteri di hello per un elemento.</span><span class="sxs-lookup"><span data-stu-id="3be34-173">Once you have defined hello backup protection policy, you still must enable hello policy for an item.</span></span> <span data-ttu-id="3be34-174">Utilizzare  **[Enable AzureRmRecoveryServicesBackupProtection](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/enable-azurermrecoveryservicesbackupprotection)**  tooenable protezione.</span><span class="sxs-lookup"><span data-stu-id="3be34-174">Use **[Enable-AzureRmRecoveryServicesBackupProtection](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/enable-azurermrecoveryservicesbackupprotection)** tooenable protection.</span></span> <span data-ttu-id="3be34-175">Abilitazione della protezione, sono necessari due oggetti - elemento hello e criteri di hello.</span><span class="sxs-lookup"><span data-stu-id="3be34-175">Enabling protection requires two objects - hello item and hello policy.</span></span> <span data-ttu-id="3be34-176">Dopo aver associato all'insieme di credenziali hello criteri hello, flusso di lavoro backup hello viene attivato in fase di hello è definito nella pianificazione dei criteri hello.</span><span class="sxs-lookup"><span data-stu-id="3be34-176">Once hello policy has been associated with hello vault, hello backup workflow is triggered at hello time defined in hello policy schedule.</span></span>

<span data-ttu-id="3be34-177">Hello seguendo l'esempio Abilita protezione per elemento hello, V2VM, applicando i criteri di hello, NewPolicy.</span><span class="sxs-lookup"><span data-stu-id="3be34-177">hello following example enables protection for hello item, V2VM, using hello policy, NewPolicy.</span></span> <span data-ttu-id="3be34-178">protezione di hello tooenable nelle macchine virtuali di gestione risorse non crittografati</span><span class="sxs-lookup"><span data-stu-id="3be34-178">tooenable hello protection on non-encrypted Resource Manager VMs</span></span>

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

<span data-ttu-id="3be34-179">protezione hello tooenable crittografati macchine virtuali (crittografate utilizzando BEK e KEK), è necessario toogive hello Azure Backup autorizzazione tooread chiavi e segreti dall'insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="3be34-179">tooenable hello protection on encrypted VMs (encrypted using BEK and KEK), you need toogive hello Azure Backup service permission tooread keys and secrets from key vault.</span></span>

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToKeys backup,get,list -PermissionsToSecrets get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

<span data-ttu-id="3be34-180">protezione hello tooenable crittografati macchine virtuali (crittografate utilizzando solo BEK), è necessario toogive hello Azure Backup service autorizzazione tooread i segreti dall'insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="3be34-180">tooenable hello protection on encrypted VMs (encrypted using BEK only), you need toogive hello Azure Backup service permission tooread secrets from key vault.</span></span>

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToSecrets backup,get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

> [!NOTE]
> <span data-ttu-id="3be34-181">Se si utilizza il cloud di Azure per enti pubblici hello, quindi utilizzare hello valore ff281ffe-705c-4f53-9f37-a40e6f2c68f3 per il parametro hello **- ServicePrincipalName** in [Set-AzureRmKeyVaultAccessPolicy](https://docs.microsoft.com/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) cmdlet .</span><span class="sxs-lookup"><span data-stu-id="3be34-181">If you are using hello Azure Government cloud, then use hello value ff281ffe-705c-4f53-9f37-a40e6f2c68f3 for hello parameter **-ServicePrincipalName** in [Set-AzureRmKeyVaultAccessPolicy](https://docs.microsoft.com/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) cmdlet.</span></span>
>
>

<span data-ttu-id="3be34-182">Macchine virtuali classiche</span><span class="sxs-lookup"><span data-stu-id="3be34-182">For classic VMs</span></span>

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V1VM" -ServiceName "ServiceName1"
```

### <a name="modify-a-protection-policy"></a><span data-ttu-id="3be34-183">Modificare i criteri di protezione</span><span class="sxs-lookup"><span data-stu-id="3be34-183">Modify a protection policy</span></span>
<span data-ttu-id="3be34-184">criteri di protezione hello toomodify, utilizzare [Set AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/set-azurermrecoveryservicesbackupprotectionpolicy) oggetti SchedulePolicy o RetentionPolicy di hello toomodify.</span><span class="sxs-lookup"><span data-stu-id="3be34-184">toomodify hello protection policy, use [Set-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/set-azurermrecoveryservicesbackupprotectionpolicy) toomodify hello SchedulePolicy or RetentionPolicy objects.</span></span>

<span data-ttu-id="3be34-185">Hello esempio seguente modifica hello ripristino punto memorizzazione too365 giorni.</span><span class="sxs-lookup"><span data-stu-id="3be34-185">hello following example changes hello recovery point retention too365 days.</span></span>

```
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol.DailySchedule.DurationCountInDays = 365
PS C:\> $pol= Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Set-AzureRmRecoveryServicesBackupProtectionPolicy -Policy $pol  -RetentionPolicy $RetPol
```

## <a name="trigger-a-backup"></a><span data-ttu-id="3be34-186">Attivare un backup</span><span class="sxs-lookup"><span data-stu-id="3be34-186">Trigger a backup</span></span>
<span data-ttu-id="3be34-187">È possibile utilizzare  **[Backup AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/backup-azurermrecoveryservicesbackupitem)**  tootrigger un processo di backup.</span><span class="sxs-lookup"><span data-stu-id="3be34-187">You can use **[Backup-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/backup-azurermrecoveryservicesbackupitem)** tootrigger a backup job.</span></span> <span data-ttu-id="3be34-188">In caso di backup iniziale hello, è un backup completo.</span><span class="sxs-lookup"><span data-stu-id="3be34-188">If it is hello initial backup, it is a full backup.</span></span> <span data-ttu-id="3be34-189">I backup successivi saranno incrementali.</span><span class="sxs-lookup"><span data-stu-id="3be34-189">Subsequent backups take an incremental copy.</span></span> <span data-ttu-id="3be34-190">Toouse assicurarsi di essere  **[Set AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)**  contesto insieme di credenziali di hello tooset prima attivazione hello processo di backup.</span><span class="sxs-lookup"><span data-stu-id="3be34-190">Be sure toouse **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)** tooset hello vault context before triggering hello backup job.</span></span> <span data-ttu-id="3be34-191">Hello di esempio seguente si presuppone che il contesto dell'insieme di credenziali è stato impostato.</span><span class="sxs-lookup"><span data-stu-id="3be34-191">hello following example assumes vault context was set.</span></span>

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer -ContainerType "AzureVM" -Status "Registered" -FriendlyName "V2VM"
PS C:\> $item = Get-AzureRmRecoveryServicesBackupItem -Container $namedContainer -WorkloadType "AzureVM"
PS C:\> $job = Backup-AzureRmRecoveryServicesBackupItem -Item $item
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM              Backup               InProgress            4/23/2016 5:00:30 PM                       cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

> [!NOTE]
> <span data-ttu-id="3be34-192">fuso orario di Hello dei campi di StartTime ed EndTime hello in PowerShell è UTC.</span><span class="sxs-lookup"><span data-stu-id="3be34-192">hello timezone of hello StartTime and EndTime fields in PowerShell is UTC.</span></span> <span data-ttu-id="3be34-193">Tuttavia, se hello ora viene visualizzata nel portale di Azure hello, hello è fuso orario locale tooyour adattata.</span><span class="sxs-lookup"><span data-stu-id="3be34-193">However, when hello time is shown in hello Azure portal, hello time is adjusted tooyour local timezone.</span></span>
>
>

## <a name="monitoring-a-backup-job"></a><span data-ttu-id="3be34-194">Monitoraggio di un processo di backup</span><span class="sxs-lookup"><span data-stu-id="3be34-194">Monitoring a backup job</span></span>
<span data-ttu-id="3be34-195">È possibile monitorare operazioni a esecuzione prolungata, ad esempio i processi di backup, senza utilizzare hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="3be34-195">You can monitor long-running operations, such as backup jobs, without using hello Azure portal.</span></span> <span data-ttu-id="3be34-196">stato hello tooget di un processo in corso, utilizzare hello  **[Get AzureRmRecoveryservicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjob)**  cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3be34-196">tooget hello status of an in-progress job, use hello **[Get-AzureRmRecoveryservicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjob)** cmdlet.</span></span> <span data-ttu-id="3be34-197">Questo cmdlet Ottiene i processi di backup per un insieme di credenziali specifico hello e tale insieme di credenziali è specificato nel contesto dell'insieme di credenziali di hello.</span><span class="sxs-lookup"><span data-stu-id="3be34-197">This cmdlet gets hello backup jobs for a specific vault, and that vault is specified in hello vault context.</span></span> <span data-ttu-id="3be34-198">Hello seguente esempio ottiene hello stato di un processo in corso sotto forma di matrice e archivia lo stato di hello nella variabile di hello $joblist.</span><span class="sxs-lookup"><span data-stu-id="3be34-198">hello following example gets hello status of an in-progress job as an array, and stores hello status in hello $joblist variable.</span></span>

```
PS C:\> $joblist = Get-AzureRmRecoveryservicesBackupJob –Status "InProgress"
PS C:\> $joblist[0]
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM             Backup               InProgress            4/23/2016 5:00:30 PM           cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

<span data-ttu-id="3be34-199">Anziché il polling di questi processi per il completamento, che è necessario codice aggiuntivo - utilizzare hello  **[attesa AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)**  cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3be34-199">Instead of polling these jobs for completion - which is unnecessary additional code - use hello **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)** cmdlet.</span></span> <span data-ttu-id="3be34-200">Questo cmdlet sospende l'esecuzione di hello finché non viene completato il processo di hello o hello specificato viene raggiunto il valore di timeout.</span><span class="sxs-lookup"><span data-stu-id="3be34-200">This cmdlet pauses hello execution until either hello job completes or hello specified timeout value is reached.</span></span>

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $joblist[0] -Timeout 43200
```

## <a name="restore-an-azure-vm"></a><span data-ttu-id="3be34-201">Ripristinare una macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="3be34-201">Restore an Azure VM</span></span>
<span data-ttu-id="3be34-202">È presente una differenza fondamentale tra hello il ripristino di una macchina virtuale utilizzando hello portale di Azure e il ripristino di una macchina virtuale usando PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3be34-202">There is a key difference between hello restoring a VM using hello Azure portal and restoring a VM using PowerShell.</span></span> <span data-ttu-id="3be34-203">Con PowerShell, l'operazione di ripristino hello è stata completata una volta creati i dischi hello e informazioni di configurazione da punto di ripristino hello.</span><span class="sxs-lookup"><span data-stu-id="3be34-203">With PowerShell, hello restore operation is complete once hello disks and configuration information from hello recovery point are created.</span></span>

> [!NOTE]
> <span data-ttu-id="3be34-204">operazione di ripristino Hello non crea una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3be34-204">hello restore operation does not create a virtual machine.</span></span>
>
>

<span data-ttu-id="3be34-205">toocreate una macchina virtuale dal disco, vedere la sezione hello, [hello crea macchina virtuale da dischi stored](backup-azure-vms-automation.md#create-a-vm-from-stored-disks).</span><span class="sxs-lookup"><span data-stu-id="3be34-205">toocreate a virtual machine from disk, see hello section, [Create hello VM from stored disks](backup-azure-vms-automation.md#create-a-vm-from-stored-disks).</span></span> <span data-ttu-id="3be34-206">di seguito sono riportati i passaggi di base di Hello toorestore una macchina virtuale di Azure:</span><span class="sxs-lookup"><span data-stu-id="3be34-206">hello basic steps toorestore an Azure VM are:</span></span>

* <span data-ttu-id="3be34-207">Selezionare hello VM</span><span class="sxs-lookup"><span data-stu-id="3be34-207">Select hello VM</span></span>
* <span data-ttu-id="3be34-208">Scegliere un punto di ripristino</span><span class="sxs-lookup"><span data-stu-id="3be34-208">Choose a recovery point</span></span>
* <span data-ttu-id="3be34-209">Ripristinare i dischi hello</span><span class="sxs-lookup"><span data-stu-id="3be34-209">Restore hello disks</span></span>
* <span data-ttu-id="3be34-210">Creare VM hello da dischi stored</span><span class="sxs-lookup"><span data-stu-id="3be34-210">Create hello VM from stored disks</span></span>

<span data-ttu-id="3be34-211">Hello figura seguente illustra la gerarchia di oggetti hello da hello RecoveryServicesVault toohello BackupRecoveryPoint verso il basso.</span><span class="sxs-lookup"><span data-stu-id="3be34-211">hello following graphic shows hello object hierarchy from hello RecoveryServicesVault down toohello BackupRecoveryPoint.</span></span>

![Gerarchia di oggetti dei servizi di ripristino con BackupContainer](./media/backup-azure-vms-arm-automation/backuprecoverypoint-only.png)

<span data-ttu-id="3be34-213">toorestore dati di backup, identificare l'elemento backup hello e punto di ripristino hello che contiene i dati in un momento hello.</span><span class="sxs-lookup"><span data-stu-id="3be34-213">toorestore backup data, identify hello backed-up item and hello recovery point that holds hello point-in-time data.</span></span> <span data-ttu-id="3be34-214">Hello utilizzare  **[ripristino AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)**  cmdlet toorestore dati hello insieme di credenziali di account del cliente toohello.</span><span class="sxs-lookup"><span data-stu-id="3be34-214">Use hello **[Restore-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)** cmdlet toorestore data from hello vault toohello customer's account.</span></span>

### <a name="select-hello-vm"></a><span data-ttu-id="3be34-215">Selezionare hello VM</span><span class="sxs-lookup"><span data-stu-id="3be34-215">Select hello VM</span></span>
<span data-ttu-id="3be34-216">tooget hello PowerShell oggetto che identifica hello destra eseguire il backup elemento, iniziare dal contenitore hello nell'insieme di credenziali hello e proseguite verso il basso la gerarchia di oggetti hello.</span><span class="sxs-lookup"><span data-stu-id="3be34-216">tooget hello PowerShell object that identifies hello right backup item, start from hello container in hello vault, and work your way down hello object hierarchy.</span></span> <span data-ttu-id="3be34-217">contenitore di hello tooselect che rappresenta una macchina virtuale, utilizzare hello hello  **[Get AzureRmRecoveryServicesBackupContainer](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)**  cmdlet e inoltrare tramite pipe che toohello  **[ Get-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)**  cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3be34-217">tooselect hello container that represents hello VM, use hello **[Get-AzureRmRecoveryServicesBackupContainer](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)** cmdlet and pipe that toohello **[Get-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)** cmdlet.</span></span>

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer  -ContainerType "AzureVM" –Status "Registered" -FriendlyName "V2VM"
PS C:\> $backupitem = Get-AzureRmRecoveryServicesBackupItem –Container $namedContainer  –WorkloadType "AzureVM"
```

### <a name="choose-a-recovery-point"></a><span data-ttu-id="3be34-218">Scegliere un punto di ripristino</span><span class="sxs-lookup"><span data-stu-id="3be34-218">Choose a recovery point</span></span>
<span data-ttu-id="3be34-219">Hello utilizzare  **[Get AzureRmRecoveryServicesBackupRecoveryPoint](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)**  toolist cmdlet punti di ripristino per backup dell'elemento hello.</span><span class="sxs-lookup"><span data-stu-id="3be34-219">Use hello **[Get-AzureRmRecoveryServicesBackupRecoveryPoint](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)** cmdlet toolist all recovery points for hello backup item.</span></span> <span data-ttu-id="3be34-220">Scegliere quindi toorestore punto di ripristino hello.</span><span class="sxs-lookup"><span data-stu-id="3be34-220">Then choose hello recovery point toorestore.</span></span> <span data-ttu-id="3be34-221">Se si è certi che toouse punto di ripristino, è una buona norma toochoose hello RecoveryPointType più recente = punto AppConsistent nell'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="3be34-221">If you are unsure which recovery point toouse, it is a good practice toochoose hello most recent RecoveryPointType = AppConsistent point in hello list.</span></span>

<span data-ttu-id="3be34-222">In hello lo script seguente, hello variabile, **$rp**, è una matrice di punti di ripristino per hello selezionato backup dell'elemento, da hello ultimi sette giorni.</span><span class="sxs-lookup"><span data-stu-id="3be34-222">In hello following script, hello variable, **$rp**, is an array of recovery points for hello selected backup item, from hello past seven days.</span></span> <span data-ttu-id="3be34-223">Matrice di Hello viene ordinato in ordine inverso di tempo con punto di ripristino più recente di hello in corrispondenza dell'indice 0.</span><span class="sxs-lookup"><span data-stu-id="3be34-223">hello array is sorted in reverse order of time with hello latest recovery point at index 0.</span></span> <span data-ttu-id="3be34-224">Utilizzare l'indicizzazione di un punto di ripristino hello toopick standard matrice di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3be34-224">Use standard PowerShell array indexing toopick hello recovery point.</span></span> <span data-ttu-id="3be34-225">Nell'esempio hello $rp [0] seleziona il punto di ripristino più recente hello.</span><span class="sxs-lookup"><span data-stu-id="3be34-225">In hello example, $rp[0] selects hello latest recovery point.</span></span>

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



### <a name="restore-hello-disks"></a><span data-ttu-id="3be34-226">Ripristinare i dischi hello</span><span class="sxs-lookup"><span data-stu-id="3be34-226">Restore hello disks</span></span>
<span data-ttu-id="3be34-227">Hello utilizzare  **[ripristino AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)**  toorestore cmdlet dati dell'elemento di backup e configurazione tooa punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="3be34-227">Use hello **[Restore-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)** cmdlet toorestore a backup item's data and configuration tooa recovery point.</span></span> <span data-ttu-id="3be34-228">Dopo aver identificato un punto di ripristino, utilizzarlo come valore di hello per hello **- RecoveryPoint** parametro.</span><span class="sxs-lookup"><span data-stu-id="3be34-228">Once you have identified a recovery point, use it as hello value for hello **-RecoveryPoint** parameter.</span></span> <span data-ttu-id="3be34-229">Nel codice di esempio precedente hello, **$rp [0]** stato toouse punto di ripristino hello.</span><span class="sxs-lookup"><span data-stu-id="3be34-229">In hello previous sample code, **$rp[0]** was hello recovery point toouse.</span></span> <span data-ttu-id="3be34-230">Nel seguente esempio di codice, hello **$rp [0]** è toouse punto di ripristino hello per ripristinare il disco hello.</span><span class="sxs-lookup"><span data-stu-id="3be34-230">In hello following sample code, **$rp[0]** is hello recovery point toouse for restoring hello disk.</span></span>

<span data-ttu-id="3be34-231">i dischi hello toorestore e informazioni di configurazione:</span><span class="sxs-lookup"><span data-stu-id="3be34-231">toorestore hello disks and configuration information:</span></span>

```
PS C:\> $restorejob = Restore-AzureRmRecoveryServicesBackupItem -RecoveryPoint $rp[0] -StorageAccountName "DestAccount" -StorageAccountResourceGroupName "DestRG"
PS C:\> $restorejob
WorkloadName     Operation          Status               StartTime                 EndTime            JobID
------------     ---------          ------               ---------                 -------          ----------
V2VM              Restore           InProgress           4/23/2016 5:00:30 PM                        cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

<span data-ttu-id="3be34-232">Hello utilizzare  **[attesa AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)**  toowait cmdlet per toocomplete processo di ripristino hello.</span><span class="sxs-lookup"><span data-stu-id="3be34-232">Use hello **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)** cmdlet toowait for hello Restore job toocomplete.</span></span>

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $restorejob -Timeout 43200
```

<span data-ttu-id="3be34-233">Una volta completato il processo di ripristino hello, utilizzare hello  **[Get AzureRmRecoveryServicesBackupJobDetails](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjobdetails)**  dettagli hello tooget di cmdlet di hello operazione di ripristino.</span><span class="sxs-lookup"><span data-stu-id="3be34-233">Once hello Restore job has completed, use hello **[Get-AzureRmRecoveryServicesBackupJobDetails](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjobdetails)** cmdlet tooget hello details of hello restore operation.</span></span> <span data-ttu-id="3be34-234">proprietà JobDetails Hello è hello toorebuild necessari di hello informazioni macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3be34-234">hello JobDetails property has hello information needed toorebuild hello VM.</span></span>

```
PS C:\> $restorejob = Get-AzureRmRecoveryServicesBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmRecoveryServicesBackupJobDetails -Job $restorejob
```

<span data-ttu-id="3be34-235">Dopo aver ripristinato i dischi di hello, andare hello di toocreate successiva sezione toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3be34-235">Once you restore hello disks, go toohello next section toocreate hello VM.</span></span>

## <a name="create-a-vm-from-restored-disks"></a><span data-ttu-id="3be34-236">Creare una macchina virtuale da dischi ripristinati</span><span class="sxs-lookup"><span data-stu-id="3be34-236">Create a VM from restored disks</span></span>
<span data-ttu-id="3be34-237">Dopo aver ripristinato i dischi di hello, utilizzare toocreate questi passaggi e configurare la macchina virtuale hello dal disco.</span><span class="sxs-lookup"><span data-stu-id="3be34-237">After you have restored hello disks, use these steps toocreate and configure hello virtual machine from disk.</span></span>

> [!NOTE]
> <span data-ttu-id="3be34-238">toocreate crittografati macchine virtuali da dischi ripristinati, il ruolo di Azure deve disporre dell'autorizzazione tooperform hello action **Microsoft.KeyVault/vaults/deploy/action**.</span><span class="sxs-lookup"><span data-stu-id="3be34-238">toocreate encrypted VMs from restored disks, your Azure role must have permission tooperform hello action, **Microsoft.KeyVault/vaults/deploy/action**.</span></span> <span data-ttu-id="3be34-239">Se il ruolo non dispone di questa autorizzazione, crearne uno personalizzato con questa azione.</span><span class="sxs-lookup"><span data-stu-id="3be34-239">If your role does not have this permission, create a custom role with this action.</span></span> <span data-ttu-id="3be34-240">Per altre informazioni, vedere [Ruoli personalizzati nel Controllo degli accessi in base al ruolo di Azure](../active-directory/role-based-access-control-custom-roles.md).</span><span class="sxs-lookup"><span data-stu-id="3be34-240">For more information, see [Custom Roles in Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span></span>
>
>

1. <span data-ttu-id="3be34-241">Hello query ripristinato proprietà del disco per i dettagli dei processi hello.</span><span class="sxs-lookup"><span data-stu-id="3be34-241">Query hello restored disk properties for hello job details.</span></span>

  ```
  PS C:\> $properties = $details.properties
  PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
  PS C:\> $containerName = $properties["Config Blob Container Name"]
  PS C:\> $blobName = $properties["Config Blob Name"]
  ```

2. <span data-ttu-id="3be34-242">Impostare il contesto di archiviazione di Azure hello e ripristinare i file di configurazione JSON hello.</span><span class="sxs-lookup"><span data-stu-id="3be34-242">Set hello Azure storage context and restore hello JSON configuration file.</span></span>

    ```
    PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName "testvault"
    PS C:\> $destination_path = "C:\vmconfig.json"
    PS C:\> Get-AzureStorageBlobContent -Container $containerName -Blob $blobName -Destination $destination_path
    PS C:\> $obj = ((Get-Content -Path $destination_path -Raw -Encoding Unicode)).TrimEnd([char]0x00) | ConvertFrom-Json
    ```

3. <span data-ttu-id="3be34-243">Utilizzare configurazione di macchina virtuale di hello JSON configuration file toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="3be34-243">Use hello JSON configuration file toocreate hello VM configuration.</span></span>

    ```
   PS C:\> $vm = New-AzureRmVMConfig -VMSize $obj.'properties.hardwareProfile'.vmSize -VMName "testrestore"
    ```

4. <span data-ttu-id="3be34-244">Collegare un disco del sistema operativo hello e i dischi dati.</span><span class="sxs-lookup"><span data-stu-id="3be34-244">Attach hello OS disk and data disks.</span></span> <span data-ttu-id="3be34-245">A seconda della configurazione di hello delle macchine virtuali, fare clic su hello collegamento pertinente tooview rispettivi cmdlet:</span><span class="sxs-lookup"><span data-stu-id="3be34-245">Depending on hello configuration of your VMs, click on hello relevant link tooview respective cmdlets:</span></span> 
    - [<span data-ttu-id="3be34-246">Macchine virtuali non gestiti, non crittografato</span><span class="sxs-lookup"><span data-stu-id="3be34-246">Non-managed, non-encrypted VMs</span></span>](#non-managed-non-encrypted-vms)
    - [<span data-ttu-id="3be34-247">Macchine virtuali non gestiti, crittografate (solo BEK)</span><span class="sxs-lookup"><span data-stu-id="3be34-247">Non-managed, encrypted VMs (BEK only)</span></span>](#non-managed-encrypted-vms-bek-only)
    - [<span data-ttu-id="3be34-248">Macchine virtuali non gestiti, crittografate (BEK e KEK)</span><span class="sxs-lookup"><span data-stu-id="3be34-248">Non-managed, encrypted VMs (BEK and KEK)</span></span>](#non-managed-encrypted-vms-bek-and-kek)
    - [<span data-ttu-id="3be34-249">Macchine virtuali gestite e non crittografati</span><span class="sxs-lookup"><span data-stu-id="3be34-249">Managed, non-encrypted VMs</span></span>](#managed-non-encrypted-vms)
    - [<span data-ttu-id="3be34-250">Macchine virtuali gestite, crittografate (BEK e KEK)</span><span class="sxs-lookup"><span data-stu-id="3be34-250">Managed, encrypted VMs (BEK and KEK)</span></span>](#managed-encrypted-vms-bek-and-kek)
    
    #### <a name="non-managed-non-encrypted-vms"></a><span data-ttu-id="3be34-251">Macchine virtuali non gestite, non crittografate</span><span class="sxs-lookup"><span data-stu-id="3be34-251">Non-managed, non-encrypted VMs</span></span>

    <span data-ttu-id="3be34-252">Utilizzare seguente esempio per le macchine virtuali non gestiti, non crittografato hello.</span><span class="sxs-lookup"><span data-stu-id="3be34-252">Use hello following sample for non-managed, non-encrypted VMs.</span></span>

    ```
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.'properties.StorageProfile'.osDisk.vhd.Uri -CreateOption "Attach"
    PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.'properties.StorageProfile'.OsDisk.OsType
    PS C:\> foreach($dd in $obj.'properties.StorageProfile'.DataDisks)
    {
    $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.vhd.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption "Attach"
    }
    ```

    #### <a name="non-managed-encrypted-vms-bek-only"></a><span data-ttu-id="3be34-253">Macchine virtuali non gestite, crittografate (solo con BEK)</span><span class="sxs-lookup"><span data-stu-id="3be34-253">Non-managed, encrypted VMs (BEK only)</span></span>

    <span data-ttu-id="3be34-254">Per macchine virtuali non gestiti, crittografate (crittografate utilizzando solo BEK), l'insieme di credenziali a chiave segreta toohello toorestore hello è necessario prima di collegare i dischi.</span><span class="sxs-lookup"><span data-stu-id="3be34-254">For non-managed, encrypted VMs (encrypted using BEK only), you need toorestore hello secret toohello key vault before you can attach disks.</span></span> <span data-ttu-id="3be34-255">Per ulteriori informazioni, vedere l'articolo hello [ripristinare una macchina virtuale crittografata da un punto di ripristino di Backup di Azure](backup-azure-restore-key-secret.md).</span><span class="sxs-lookup"><span data-stu-id="3be34-255">For more information, please see hello article, [Restore an encrypted virtual machine from an Azure Backup recovery point](backup-azure-restore-key-secret.md).</span></span> <span data-ttu-id="3be34-256">Hello seguente esempio viene illustrata la modalità di tooattach del sistema operativo e i dischi di dati per le macchine virtuali di crittografia.</span><span class="sxs-lookup"><span data-stu-id="3be34-256">hello following sample shows how tooattach OS and data disks for encrypted VMs.</span></span>

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

    #### <a name="non-managed-encrypted-vms-bek-and-kek"></a><span data-ttu-id="3be34-257">Macchine virtuali non gestite, crittografate (con BEK e KEK)</span><span class="sxs-lookup"><span data-stu-id="3be34-257">Non-managed, encrypted VMs (BEK and KEK)</span></span>

    <span data-ttu-id="3be34-258">Per macchine virtuali non gestiti, crittografate (crittografate utilizzando BEK e KEK), è necessario toorestore hello chiave e il segreto toohello insieme di credenziali chiave prima di collegare i dischi.</span><span class="sxs-lookup"><span data-stu-id="3be34-258">For non-managed, encrypted VMs (encrypted using BEK and KEK), you need toorestore hello key and secret toohello key vault before you can attach disks.</span></span> <span data-ttu-id="3be34-259">Per ulteriori informazioni, vedere l'articolo hello [ripristinare una macchina virtuale crittografata da un punto di ripristino di Backup di Azure](backup-azure-restore-key-secret.md).</span><span class="sxs-lookup"><span data-stu-id="3be34-259">For more information, please see hello article, [Restore an encrypted virtual machine from an Azure Backup recovery point](backup-azure-restore-key-secret.md).</span></span> <span data-ttu-id="3be34-260">Hello seguente esempio viene illustrata la modalità di tooattach del sistema operativo e i dischi di dati per le macchine virtuali di crittografia.</span><span class="sxs-lookup"><span data-stu-id="3be34-260">hello following sample shows how tooattach OS and data disks for encrypted VMs.</span></span>

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

    #### <a name="managed-non-encrypted-vms"></a><span data-ttu-id="3be34-261">Macchine virtuali gestite, non crittografate</span><span class="sxs-lookup"><span data-stu-id="3be34-261">Managed, non-encrypted VMs</span></span>

    <span data-ttu-id="3be34-262">Per le macchine virtuali non crittografato a gestito, sarà necessario dischi toocreate gestiti dall'archiviazione blob e quindi collegare i dischi di hello.</span><span class="sxs-lookup"><span data-stu-id="3be34-262">For managed non-encrypted VMs, you'll need toocreate managed disks from blob storage, and then attach hello disks.</span></span> <span data-ttu-id="3be34-263">Per informazioni dettagliate, vedere l'articolo hello [collegare un tooa disco dati macchina virtuale di Windows con PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="3be34-263">For in-depth information, see hello article, [Attach a data disk tooa Windows VM using PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span></span> <span data-ttu-id="3be34-264">Hello codice di esempio seguente viene illustrato come tooattach hello dischi dati per le macchine virtuali gestite non crittografato.</span><span class="sxs-lookup"><span data-stu-id="3be34-264">hello following sample code shows how tooattach hello data disks for managed non-encrypted VMs.</span></span>

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

    #### <a name="managed-encrypted-vms-bek-and-kek"></a><span data-ttu-id="3be34-265">Macchine virtuali gestite, crittografate (con BEK e KEK)</span><span class="sxs-lookup"><span data-stu-id="3be34-265">Managed, encrypted VMs (BEK and KEK)</span></span>

    <span data-ttu-id="3be34-266">Per gestito crittografati le macchine virtuali (crittografate utilizzando BEK e KEK), verranno necessari dischi toocreate gestiti dall'archiviazione blob e quindi collegare i dischi di hello.</span><span class="sxs-lookup"><span data-stu-id="3be34-266">For managed encrypted VMs (encrypted using BEK and KEK), you'll need toocreate managed disks from blob storage, and then attach hello disks.</span></span> <span data-ttu-id="3be34-267">Per informazioni dettagliate, vedere l'articolo hello [collegare un tooa disco dati macchina virtuale di Windows con PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="3be34-267">For in-depth information, see hello article, [Attach a data disk tooa Windows VM using PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span></span> <span data-ttu-id="3be34-268">Hello codice di esempio seguente viene illustrato come tooattach hello dischi dati per le macchine virtuali crittografate gestite.</span><span class="sxs-lookup"><span data-stu-id="3be34-268">hello following sample code shows how tooattach hello data disks for managed encrypted VMs.</span></span>

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

5. <span data-ttu-id="3be34-269">Configurare le impostazioni di rete hello.</span><span class="sxs-lookup"><span data-stu-id="3be34-269">Set hello Network settings.</span></span>

    ```
    PS C:\> $nicName="p1234"
    PS C:\> $pip = New-AzureRmPublicIpAddress -Name $nicName -ResourceGroupName "test" -Location "WestUS" -AllocationMethod Dynamic
    PS C:\> $vnet = Get-AzureRmVirtualNetwork -Name "testvNET" -ResourceGroupName "test"
    PS C:\> $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName "test" -Location "WestUS" -SubnetId $vnet.Subnets[$subnetindex].Id -PublicIpAddressId $pip.Id
    PS C:\> $vm=Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
    ```
6. <span data-ttu-id="3be34-270">Creare una macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="3be34-270">Create hello virtual machine.</span></span>

    ```    
    PS C:\> New-AzureRmVM -ResourceGroupName "test" -Location "WestUS" -VM $vm
    ```

## <a name="next-steps"></a><span data-ttu-id="3be34-271">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3be34-271">Next steps</span></span>
<span data-ttu-id="3be34-272">Se si preferisce toouse tooengage di PowerShell con le risorse di Azure, vedere articolo PowerShell hello [distribuire e gestire Backup per Windows Server](backup-client-automation.md).</span><span class="sxs-lookup"><span data-stu-id="3be34-272">If you prefer toouse PowerShell tooengage with your Azure resources, see hello PowerShell article, [Deploy and Manage Backup for Windows Server](backup-client-automation.md).</span></span> <span data-ttu-id="3be34-273">Se si gestiscono i backup DPM, vedere l'articolo hello [distribuire e gestire Backup per DPM](backup-dpm-automation.md).</span><span class="sxs-lookup"><span data-stu-id="3be34-273">If you manage DPM backups, see hello article, [Deploy and Manage Backup for DPM](backup-dpm-automation.md).</span></span> <span data-ttu-id="3be34-274">Entrambi gli articoli prevedono due versioni: una per le distribuzioni con Resource Manager, l'altra per le distribuzioni classiche.</span><span class="sxs-lookup"><span data-stu-id="3be34-274">Both of these articles have a version for Resource Manager deployments and Classic deployments.</span></span>  
