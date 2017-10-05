---
title: Distribuire e gestire i backup per le macchine virtuali distribuite con Resource Manager usando PowerShell | Microsoft Docs
description: Utilizzare PowerShell per distribuire e gestire i backup per le macchine virtuali distribuite con Resource Manager in Azure
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
ms.openlocfilehash: 861346a50df6641abb9e454644228146e14b4078
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="use-azurermrecoveryservicesbackup-cmdlets-to-back-up-virtual-machines"></a><span data-ttu-id="60c6a-103">Usare i cmdlet AzureRM.RecoveryServices.Backup per eseguire il backup di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="60c6a-103">Use AzureRM.RecoveryServices.Backup cmdlets to back up virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="60c6a-104">Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="60c6a-104">Resource Manager</span></span>](backup-azure-vms-automation.md)
> * [<span data-ttu-id="60c6a-105">Classico</span><span class="sxs-lookup"><span data-stu-id="60c6a-105">Classic</span></span>](backup-azure-vms-classic-automation.md)
>
>

<span data-ttu-id="60c6a-106">In questo articolo viene illustrato come usare i cmdlet di Azure PowerShell per eseguire il backup e ripristinare una macchina virtuale (VM) di Azure da un insieme di credenziali dei servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="60c6a-106">This article shows you how to use Azure PowerShell cmdlets to back up and recover an Azure virtual machine (VM) from a Recovery Services vault.</span></span> <span data-ttu-id="60c6a-107">Un insieme di credenziali dei servizi di ripristino è una risorsa di Resource Manager di Azure e viene utilizzato per proteggere i dati e asset nei servizi di Backup di Azure e di Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="60c6a-107">A Recovery Services vault is an Azure Resource Manager resource and is used to protect data and assets in both Azure Backup and Azure Site Recovery services.</span></span> <span data-ttu-id="60c6a-108">È possibile usare un insieme di credenziali di Servizi di ripristino per proteggere le macchine virtuali distribuite con Service Manager di Azure e Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="60c6a-108">You can use a Recovery Services vault to protect Azure Service Manager-deployed VMs, and Azure Resource Manager-deployed VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="60c6a-109">Azure offre due modelli di distribuzione per creare e usare le risorse: [Resource Manager e distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="60c6a-109">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="60c6a-110">Questo articolo si riferisce alle VM create tramite il modello Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="60c6a-110">This article is for use with VMs created using the Resource Manager model.</span></span>
>
>

<span data-ttu-id="60c6a-111">In questo articolo viene illustrato come usare PowerShell per proteggere una macchina virtuale e ripristinare i dati da un punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="60c6a-111">This article walks you through using PowerShell to protect a VM, and restore data from a recovery point.</span></span>

## <a name="concepts"></a><span data-ttu-id="60c6a-112">Concetti</span><span class="sxs-lookup"><span data-stu-id="60c6a-112">Concepts</span></span>
<span data-ttu-id="60c6a-113">Se non si ha familiarità con il servizio di Backup di Azure, vedere l'argomento [Che cos'è Backup di Azure?](backup-introduction-to-azure-backup.md) per una panoramica sul servizio</span><span class="sxs-lookup"><span data-stu-id="60c6a-113">If you are not familiar with the Azure Backup service, for an overview of the service, check out [What is Azure Backup?](backup-introduction-to-azure-backup.md)</span></span> <span data-ttu-id="60c6a-114">Prima di iniziare, assicurarsi di avere gli elementi di base per i prerequisiti necessari per usare il servizio Backup di Azure, e le limitazioni della soluzione attuale di backup della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="60c6a-114">Before you start, ensure that you cover the essentials about the prerequisites needed to work with Azure Backup, and the limitations of the current VM backup solution.</span></span>

<span data-ttu-id="60c6a-115">Per un utilizzo efficace di PowerShell, è necessario comprendere la gerarchia degli oggetti e da dove iniziare.</span><span class="sxs-lookup"><span data-stu-id="60c6a-115">To use PowerShell effectively, it is necessary to understand the hierarchy of objects and from where to start.</span></span>

![Gerarchia di oggetti dei servizi di ripristino](./media/backup-azure-vms-arm-automation/recovery-services-object-hierarchy.png)

<span data-ttu-id="60c6a-117">Per visualizzare il riferimento al cmdlet AzureRm.RecoveryServices.Backup di PowerShell, vedere [Azure Backup - Recovery Services Cmdlets (Backup di Azure: i cmdlet dei servizi di ripristino)](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup) nella libreria di Azure.</span><span class="sxs-lookup"><span data-stu-id="60c6a-117">To view the AzureRm.RecoveryServices.Backup PowerShell cmdlet reference, see the [Azure Backup - Recovery Services Cmdlets](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup) in the Azure library.</span></span>

## <a name="setup-and-registration"></a><span data-ttu-id="60c6a-118">Installazione e registrazione</span><span class="sxs-lookup"><span data-stu-id="60c6a-118">Setup and Registration</span></span>
<span data-ttu-id="60c6a-119">Per iniziare:</span><span class="sxs-lookup"><span data-stu-id="60c6a-119">To begin:</span></span>

1. <span data-ttu-id="60c6a-120">[Scaricare la versione più recente di PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) (la versione minima richiesta è: 1.4.0)</span><span class="sxs-lookup"><span data-stu-id="60c6a-120">[Download the latest version of PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) (the minimum version required is: 1.4.0)</span></span>
2. <span data-ttu-id="60c6a-121">Cercare i cmdlet PowerShell di Azure Backup disponibili digitando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="60c6a-121">Find the Azure Backup PowerShell cmdlets available by typing the following command:</span></span>

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


<span data-ttu-id="60c6a-122">Le attività seguenti possono essere automatizzate tramite PowerShell:</span><span class="sxs-lookup"><span data-stu-id="60c6a-122">The following tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="60c6a-123">Creare un insieme di credenziali di Servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="60c6a-123">Create a Recovery Services vault</span></span>
* <span data-ttu-id="60c6a-124">Eseguire il backup delle VM di Azure</span><span class="sxs-lookup"><span data-stu-id="60c6a-124">Back up Azure VMs</span></span>
* <span data-ttu-id="60c6a-125">Attivare un processo di backup</span><span class="sxs-lookup"><span data-stu-id="60c6a-125">Trigger a backup job</span></span>
* <span data-ttu-id="60c6a-126">Monitorare un processo di backup</span><span class="sxs-lookup"><span data-stu-id="60c6a-126">Monitor a backup job</span></span>
* <span data-ttu-id="60c6a-127">Ripristinare una macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="60c6a-127">Restore an Azure VM</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="60c6a-128">Creare un insieme di credenziali di Servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="60c6a-128">Create a recovery services vault</span></span>
<span data-ttu-id="60c6a-129">Nei passaggi seguenti viene descritto come creare un insieme di credenziali dei servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="60c6a-129">The following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="60c6a-130">Un insieme di credenziali dei servizi di ripristino è diverso da un insieme di credenziali di backup.</span><span class="sxs-lookup"><span data-stu-id="60c6a-130">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="60c6a-131">Se si sta usando Backup di Azure per la prima volta, è necessario usare il cmdlet **[Register-AzureRmResourceProvider](http://docs.microsoft.com/powershell/module/azurerm.resources/register-azurermresourceprovider)** per registrare il provider dei Servizi di ripristino di Azure con la propria sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="60c6a-131">If you are using Azure Backup for the first time, you must use the **[Register-AzureRmResourceProvider](http://docs.microsoft.com/powershell/module/azurerm.resources/register-azurermresourceprovider)** cmdlet to register the Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="60c6a-132">L'insieme di credenziali dei Servizi di ripristino è una risorsa Resource Manager, pertanto è necessario inserirlo all'interno di un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="60c6a-132">The Recovery Services vault is a Resource Manager resource, so you need to place it within a resource group.</span></span> <span data-ttu-id="60c6a-133">È possibile usare un gruppo di risorse esistente o crearne uno con il cmdlet **[New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup)**.</span><span class="sxs-lookup"><span data-stu-id="60c6a-133">You can use an existing resource group, or create a resource group with the **[New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup)** cmdlet.</span></span> <span data-ttu-id="60c6a-134">Quando si crea un nuovo gruppo di risorse, è necessario specificare il nome e il percorso per il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="60c6a-134">When creating a resource group, specify the name and location for the resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. <span data-ttu-id="60c6a-135">Usare il cmdlet **[New-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault)** per creare un nuovo insieme di credenziali dei Servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="60c6a-135">Use the **[New-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault)** cmdlet to create the Recovery Services vault.</span></span> <span data-ttu-id="60c6a-136">Assicurarsi di specificare per l'insieme di credenziali lo stesso percorso usato per il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="60c6a-136">Be sure to specify the same location for the vault as was used for the resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. <span data-ttu-id="60c6a-137">Specificare il tipo di ridondanza di archiviazione da usare, ad esempio [archiviazione con ridondanza locale (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) o [archiviazione con ridondanza geografica (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="60c6a-137">Specify the type of storage redundancy to use; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="60c6a-138">Nell'esempio seguente l'opzione BackupStorageRedundancy per testvault è impostata su GeoRedundant.</span><span class="sxs-lookup"><span data-stu-id="60c6a-138">The following example shows the -BackupStorageRedundancy option for testvault is set to GeoRedundant.</span></span>

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testvault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -Vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

   > [!TIP]
   > <span data-ttu-id="60c6a-139">Molti cmdlet di Backup di Azure richiedono l'oggetto dell'insieme di credenziali dei servizi di ripristino come input.</span><span class="sxs-lookup"><span data-stu-id="60c6a-139">Many Azure Backup cmdlets require the Recovery Services vault object as an input.</span></span> <span data-ttu-id="60c6a-140">Per questo motivo, è utile archiviare l'oggetto dell'insieme di credenziali dei servizi di ripristino di Backup in una variabile.</span><span class="sxs-lookup"><span data-stu-id="60c6a-140">For this reason, it is convenient to store the Backup Recovery Services vault object in a variable.</span></span>
   >
   >

## <a name="view-the-vaults-in-a-subscription"></a><span data-ttu-id="60c6a-141">Visualizzare gli insiemi di credenziali in un abbonamento</span><span class="sxs-lookup"><span data-stu-id="60c6a-141">View the vaults in a subscription</span></span>
<span data-ttu-id="60c6a-142">Usare **[Get-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/get-azurermrecoveryservicesvault)** per visualizzare l'elenco di tutti gli insiemi di credenziali della sottoscrizione corrente.</span><span class="sxs-lookup"><span data-stu-id="60c6a-142">Use **[Get-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/get-azurermrecoveryservicesvault)** to view the list of all vaults in the current subscription.</span></span> <span data-ttu-id="60c6a-143">È possibile usare questo comando per verificare che sia stato creato un nuovo insieme di credenziali o per vedere gli insiemi di credenziali nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="60c6a-143">You can use this command to check that a new vault was created, or to see the available vaults in the subscription.</span></span>

<span data-ttu-id="60c6a-144">Eseguire il comando Get-AzureRmRecoveryServicesVault per visualizzare tutti gli insiemi di credenziali disponibili nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="60c6a-144">Run the command, Get-AzureRmRecoveryServicesVault, to view all vaults in the subscription.</span></span> <span data-ttu-id="60c6a-145">L'esempio seguente mostra le informazioni visualizzate per ogni insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="60c6a-145">The following example shows the information displayed for each vault.</span></span>

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


## <a name="back-up-azure-vms"></a><span data-ttu-id="60c6a-146">Eseguire il backup delle VM di Azure</span><span class="sxs-lookup"><span data-stu-id="60c6a-146">Back up Azure VMs</span></span>
<span data-ttu-id="60c6a-147">Usare un insieme di credenziali di Servizi di ripristino per proteggere le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="60c6a-147">Use a Recovery Services vault to protect your virtual machines.</span></span> <span data-ttu-id="60c6a-148">Prima di applicare la protezione, impostare il contesto dell'insieme di credenziali (tipo di dati protetti nell'insieme di credenziali) e verificare i criteri di protezione.</span><span class="sxs-lookup"><span data-stu-id="60c6a-148">Before you apply the protection, set the vault context (the type of data protected in the vault), and verify the protection policy.</span></span> <span data-ttu-id="60c6a-149">I criteri di protezione rappresentano la pianificazione per l'esecuzione dei processi di backup e il periodo di conservazione di ogni snapshot del backup.</span><span class="sxs-lookup"><span data-stu-id="60c6a-149">The protection policy is the schedule when the backup jobs run, and how long each backup snapshot is retained.</span></span>

### <a name="set-vault-context"></a><span data-ttu-id="60c6a-150">Impostazione del contesto dell'insieme di credenziali</span><span class="sxs-lookup"><span data-stu-id="60c6a-150">Set vault context</span></span>
<span data-ttu-id="60c6a-151">Prima di abilitare la protezione per una macchina virtuale, usare **[Set AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)** per impostare il contesto dell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="60c6a-151">Before enabling protection on a VM, use **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)** to set the vault context.</span></span> <span data-ttu-id="60c6a-152">Una volta impostato il contesto dell'insieme di credenziali, si applica a tutti i cmdlet successivi.</span><span class="sxs-lookup"><span data-stu-id="60c6a-152">Once the vault context is set, it applies to all subsequent cmdlets.</span></span> <span data-ttu-id="60c6a-153">L'esempio seguente imposta il contesto per l'insieme di credenziali, *testvault*.</span><span class="sxs-lookup"><span data-stu-id="60c6a-153">The following example sets the vault context for the vault, *testvault*.</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesVault -Name "testvault" | Set-AzureRmRecoveryServicesVaultContext
```

### <a name="create-a-protection-policy"></a><span data-ttu-id="60c6a-154">Creare i criteri di protezione</span><span class="sxs-lookup"><span data-stu-id="60c6a-154">Create a protection policy</span></span>
<span data-ttu-id="60c6a-155">Quando si crea un insieme di credenziali di Servizi di ripristino, questo è dotato di protezione predefinita e criteri di conservazione.</span><span class="sxs-lookup"><span data-stu-id="60c6a-155">When you create a Recovery Services vault, it comes with default protection and retention policies.</span></span> <span data-ttu-id="60c6a-156">I criteri di protezione predefinita attivano un processo di backup ogni giorno all'ora specificata.</span><span class="sxs-lookup"><span data-stu-id="60c6a-156">The default protection policy triggers a backup job each day at a specified time.</span></span> <span data-ttu-id="60c6a-157">I criteri di conservazione predefiniti consentono di mantenere il punto di recupero giornaliero per 30 giorni.</span><span class="sxs-lookup"><span data-stu-id="60c6a-157">The default retention policy retains the daily recovery point for 30 days.</span></span> <span data-ttu-id="60c6a-158">È possibile usare i criteri predefiniti per proteggere rapidamente la macchina virtuale e modificare i criteri in un secondo momento con dettagli diversi.</span><span class="sxs-lookup"><span data-stu-id="60c6a-158">You can use the default policy to quickly protect your VM and edit the policy later with different details.</span></span>

<span data-ttu-id="60c6a-159">Per visualizzare l'elenco dei criteri di protezione disponibili nell'insieme di credenziali, usare **[Get-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupprotectionpolicy)**.</span><span class="sxs-lookup"><span data-stu-id="60c6a-159">Use **[Get-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupprotectionpolicy)** to view the protection policies in the vault.</span></span> <span data-ttu-id="60c6a-160">È possibile usare questo cmdlet per ottenere un criterio specifico o per visualizzare i criteri associati a un tipo di carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="60c6a-160">You can use this cmdlet to get a specific policy, or to view the policies associated with a workload type.</span></span> <span data-ttu-id="60c6a-161">L'esempio seguente ottiene i criteri per il tipo di carico di lavoro AzureVM.</span><span class="sxs-lookup"><span data-stu-id="60c6a-161">The following example gets policies for workload type, AzureVM.</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesBackupProtectionPolicy -WorkloadType "AzureVM"
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
DefaultPolicy        AzureVM            AzureVM              4/14/2016 5:00:00 PM
```

> [!NOTE]
> <span data-ttu-id="60c6a-162">Il fuso orario del campo BackupTime in PowerShell è UTC.</span><span class="sxs-lookup"><span data-stu-id="60c6a-162">The timezone of the BackupTime field in PowerShell is UTC.</span></span> <span data-ttu-id="60c6a-163">Tuttavia, l'orario di backup nel portale di Azure è allineato al fuso orario locale.</span><span class="sxs-lookup"><span data-stu-id="60c6a-163">However, when the backup time is shown in the Azure portal, the time is adjusted to your local timezone.</span></span>
>
>

<span data-ttu-id="60c6a-164">I criteri di protezione del backup sono associati almeno a un criterio di conservazione.</span><span class="sxs-lookup"><span data-stu-id="60c6a-164">A backup protection policy is associated with at least one retention policy.</span></span> <span data-ttu-id="60c6a-165">I criteri di conservazione definiscono per quanto tempo un punto di recupero viene mantenuto prima dell'eliminazione.</span><span class="sxs-lookup"><span data-stu-id="60c6a-165">Retention policy defines how long a recovery point is kept before it is deleted.</span></span> <span data-ttu-id="60c6a-166">Per visualizzare il criterio di conservazione predefinito usare **[Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupretentionpolicyobject)**.</span><span class="sxs-lookup"><span data-stu-id="60c6a-166">Use **[Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupretentionpolicyobject)** to view the default retention policy.</span></span>  <span data-ttu-id="60c6a-167">Nello stesso modo, per ottenere il criterio di pianificazione predefinito usare **[Get-AzureRmRecoveryServicesBackupSchedulePolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupschedulepolicyobject)**.</span><span class="sxs-lookup"><span data-stu-id="60c6a-167">Similarly you can use **[Get-AzureRmRecoveryServicesBackupSchedulePolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupschedulepolicyobject)** to obtain the default schedule policy.</span></span> <span data-ttu-id="60c6a-168">Il cmdlet **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)** crea un oggetto di PowerShell che contiene le informazioni relative ai criteri di backup.</span><span class="sxs-lookup"><span data-stu-id="60c6a-168">The **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)** cmdlet creates a PowerShell object that holds backup policy information.</span></span> <span data-ttu-id="60c6a-169">Gli oggetti dei criteri di conservazione e di pianificazione vengono usati come input per il cmdlet **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)**.</span><span class="sxs-lookup"><span data-stu-id="60c6a-169">The schedule and retention policy objects are used as inputs to the **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)** cmdlet.</span></span> <span data-ttu-id="60c6a-170">Nell'esempio seguente i criteri di pianificazione e i criteri di conservazione vengono archiviati nelle variabili.</span><span class="sxs-lookup"><span data-stu-id="60c6a-170">The following example stores the schedule policy and the retention policy in variables.</span></span> <span data-ttu-id="60c6a-171">L'esempio usa tali variabili per definire i parametri durante la creazione di un criterio di protezione, *NewPolicy*.</span><span class="sxs-lookup"><span data-stu-id="60c6a-171">The example uses those variables to define the parameters when creating a protection policy, *NewPolicy*.</span></span>

```
PS C:\> $schPol = Get-AzureRmRecoveryServicesBackupSchedulePolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> New-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy" -WorkloadType "AzureVM" -RetentionPolicy $retPol -SchedulePolicy $schPol
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
NewPolicy           AzureVM            AzureVM              4/24/2016 1:30:00 AM
```


### <a name="enable-protection"></a><span data-ttu-id="60c6a-172">Abilitare la protezione</span><span class="sxs-lookup"><span data-stu-id="60c6a-172">Enable protection</span></span>
<span data-ttu-id="60c6a-173">Dopo aver definito i criteri di protezione di backup è comunque necessario abilitare i criteri per un elemento.</span><span class="sxs-lookup"><span data-stu-id="60c6a-173">Once you have defined the backup protection policy, you still must enable the policy for an item.</span></span> <span data-ttu-id="60c6a-174">Per abilitare la protezione usare **[Enable-AzureRmRecoveryServicesBackupProtection](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/enable-azurermrecoveryservicesbackupprotection)**.</span><span class="sxs-lookup"><span data-stu-id="60c6a-174">Use **[Enable-AzureRmRecoveryServicesBackupProtection](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/enable-azurermrecoveryservicesbackupprotection)** to enable protection.</span></span> <span data-ttu-id="60c6a-175">Per abilitare la protezione sono necessari due oggetti, l'elemento e i criteri.</span><span class="sxs-lookup"><span data-stu-id="60c6a-175">Enabling protection requires two objects - the item and the policy.</span></span> <span data-ttu-id="60c6a-176">Dopo aver associato i criteri all'insieme di credenziali, il flusso di lavoro di backup verrà attivato al momento definito nella pianificazione dei criteri.</span><span class="sxs-lookup"><span data-stu-id="60c6a-176">Once the policy has been associated with the vault, the backup workflow is triggered at the time defined in the policy schedule.</span></span>

<span data-ttu-id="60c6a-177">L'esempio seguente abilita la protezione per l'elemento V2VM usando i criteri NewPolicy.</span><span class="sxs-lookup"><span data-stu-id="60c6a-177">The following example enables protection for the item, V2VM, using the policy, NewPolicy.</span></span> <span data-ttu-id="60c6a-178">Per abilitare la protezione in macchine virtuali di Resource Manager non crittografate</span><span class="sxs-lookup"><span data-stu-id="60c6a-178">To enable the protection on non-encrypted Resource Manager VMs</span></span>

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

<span data-ttu-id="60c6a-179">Per abilitare la protezione in macchine virtuali crittografate con BEK e KEK, è necessario assegnare le autorizzazioni per il servizio di Backup di Azure per la lettura di chiavi e segreti dal Key Vault.</span><span class="sxs-lookup"><span data-stu-id="60c6a-179">To enable the protection on encrypted VMs (encrypted using BEK and KEK), you need to give the Azure Backup service permission to read keys and secrets from key vault.</span></span>

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToKeys backup,get,list -PermissionsToSecrets get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

<span data-ttu-id="60c6a-180">Per abilitare la protezione in macchine virtuali crittografate (solo con BEK), è necessario assegnare le autorizzazioni per il servizio di Backup di Azure per la lettura di segreti dall'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="60c6a-180">To enable the protection on encrypted VMs (encrypted using BEK only), you need to give the Azure Backup service permission to read secrets from key vault.</span></span>

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToSecrets backup,get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

> [!NOTE]
> <span data-ttu-id="60c6a-181">Se si usa il cloud di Azure per enti pubblici, usare il valore ff281ffe-705c-4f53-9f37-a40e6f2c68f3 per il parametro **-ServicePrincipalName** nel cmdlet [Set-AzureRmKeyVaultAccessPolicy](https://docs.microsoft.com/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy).</span><span class="sxs-lookup"><span data-stu-id="60c6a-181">If you are using the Azure Government cloud, then use the value ff281ffe-705c-4f53-9f37-a40e6f2c68f3 for the parameter **-ServicePrincipalName** in [Set-AzureRmKeyVaultAccessPolicy](https://docs.microsoft.com/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) cmdlet.</span></span>
>
>

<span data-ttu-id="60c6a-182">Macchine virtuali classiche</span><span class="sxs-lookup"><span data-stu-id="60c6a-182">For classic VMs</span></span>

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V1VM" -ServiceName "ServiceName1"
```

### <a name="modify-a-protection-policy"></a><span data-ttu-id="60c6a-183">Modificare i criteri di protezione</span><span class="sxs-lookup"><span data-stu-id="60c6a-183">Modify a protection policy</span></span>
<span data-ttu-id="60c6a-184">Per modificare i criteri di protezione, usare [Set-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/set-azurermrecoveryservicesbackupprotectionpolicy) per modificare gli oggetti SchedulePolicy o RetentionPolicy.</span><span class="sxs-lookup"><span data-stu-id="60c6a-184">To modify the protection policy, use [Set-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/set-azurermrecoveryservicesbackupprotectionpolicy) to modify the SchedulePolicy or RetentionPolicy objects.</span></span>

<span data-ttu-id="60c6a-185">Nell'esempio seguente viene modificato il punto di recupero a 365 giorni.</span><span class="sxs-lookup"><span data-stu-id="60c6a-185">The following example changes the recovery point retention to 365 days.</span></span>

```
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol.DailySchedule.DurationCountInDays = 365
PS C:\> $pol= Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Set-AzureRmRecoveryServicesBackupProtectionPolicy -Policy $pol  -RetentionPolicy $RetPol
```

## <a name="trigger-a-backup"></a><span data-ttu-id="60c6a-186">Attivare un backup</span><span class="sxs-lookup"><span data-stu-id="60c6a-186">Trigger a backup</span></span>
<span data-ttu-id="60c6a-187">È possibile usare **[Backup-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/backup-azurermrecoveryservicesbackupitem)** per attivare un processo di backup.</span><span class="sxs-lookup"><span data-stu-id="60c6a-187">You can use **[Backup-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/backup-azurermrecoveryservicesbackupitem)** to trigger a backup job.</span></span> <span data-ttu-id="60c6a-188">Se si tratta del backup iniziale, è un backup completo.</span><span class="sxs-lookup"><span data-stu-id="60c6a-188">If it is the initial backup, it is a full backup.</span></span> <span data-ttu-id="60c6a-189">I backup successivi saranno incrementali.</span><span class="sxs-lookup"><span data-stu-id="60c6a-189">Subsequent backups take an incremental copy.</span></span> <span data-ttu-id="60c6a-190">Per impostare il contesto dell'insieme di credenziali prima di attivare il processo di backup, usare **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)**.</span><span class="sxs-lookup"><span data-stu-id="60c6a-190">Be sure to use **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)** to set the vault context before triggering the backup job.</span></span> <span data-ttu-id="60c6a-191">L'esempio seguente presuppone che sia stato impostato il contesto dell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="60c6a-191">The following example assumes vault context was set.</span></span>

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer -ContainerType "AzureVM" -Status "Registered" -FriendlyName "V2VM"
PS C:\> $item = Get-AzureRmRecoveryServicesBackupItem -Container $namedContainer -WorkloadType "AzureVM"
PS C:\> $job = Backup-AzureRmRecoveryServicesBackupItem -Item $item
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM              Backup               InProgress            4/23/2016 5:00:30 PM                       cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

> [!NOTE]
> <span data-ttu-id="60c6a-192">Il fuso orario dei campi StartTime ed EndTime in PowerShell è UTC.</span><span class="sxs-lookup"><span data-stu-id="60c6a-192">The timezone of the StartTime and EndTime fields in PowerShell is UTC.</span></span> <span data-ttu-id="60c6a-193">Tuttavia, l'orario visualizzato nel portale di Azure è allineato al fuso orario locale.</span><span class="sxs-lookup"><span data-stu-id="60c6a-193">However, when the time is shown in the Azure portal, the time is adjusted to your local timezone.</span></span>
>
>

## <a name="monitoring-a-backup-job"></a><span data-ttu-id="60c6a-194">Monitoraggio di un processo di backup</span><span class="sxs-lookup"><span data-stu-id="60c6a-194">Monitoring a backup job</span></span>
<span data-ttu-id="60c6a-195">È possibile monitorare le operazioni a esecuzione prolungata, ad esempio i processi di backup, senza usare il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="60c6a-195">You can monitor long-running operations, such as backup jobs, without using the Azure portal.</span></span> <span data-ttu-id="60c6a-196">Per ottenere lo stato di un processo in corso, usare il cmdlet **[Get-AzureRmRecoveryservicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjob)**.</span><span class="sxs-lookup"><span data-stu-id="60c6a-196">To get the status of an in-progress job, use the **[Get-AzureRmRecoveryservicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjob)** cmdlet.</span></span> <span data-ttu-id="60c6a-197">Questo cmdlet ottiene i processi di backup per un insieme di credenziali specifico e tale insieme di credenziali è indicato nel relativo contesto.</span><span class="sxs-lookup"><span data-stu-id="60c6a-197">This cmdlet gets the backup jobs for a specific vault, and that vault is specified in the vault context.</span></span> <span data-ttu-id="60c6a-198">L'esempio seguente ottiene lo stato di un processo in corso sotto forma di matrice e archivia lo stato nella variabile $joblist.</span><span class="sxs-lookup"><span data-stu-id="60c6a-198">The following example gets the status of an in-progress job as an array, and stores the status in the $joblist variable.</span></span>

```
PS C:\> $joblist = Get-AzureRmRecoveryservicesBackupJob –Status "InProgress"
PS C:\> $joblist[0]
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM             Backup               InProgress            4/23/2016 5:00:30 PM           cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

<span data-ttu-id="60c6a-199">Invece di eseguire il polling dei processi per ottenere lo stato di completamento, operazione non necessaria che prevede codice aggiuntivo, usare il cmdlet **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)**.</span><span class="sxs-lookup"><span data-stu-id="60c6a-199">Instead of polling these jobs for completion - which is unnecessary additional code - use the **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)** cmdlet.</span></span> <span data-ttu-id="60c6a-200">Questo cmdlet sospende l'esecuzione fino al completamento del processo o fino a quando non viene raggiunto il valore di timeout specificato.</span><span class="sxs-lookup"><span data-stu-id="60c6a-200">This cmdlet pauses the execution until either the job completes or the specified timeout value is reached.</span></span>

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $joblist[0] -Timeout 43200
```

## <a name="restore-an-azure-vm"></a><span data-ttu-id="60c6a-201">Ripristinare una macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="60c6a-201">Restore an Azure VM</span></span>
<span data-ttu-id="60c6a-202">C'è una differenza chiave tra il ripristino di una macchina virtuale tramite il portale di Azure e il ripristino di una macchina virtuale tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="60c6a-202">There is a key difference between the restoring a VM using the Azure portal and restoring a VM using PowerShell.</span></span> <span data-ttu-id="60c6a-203">Con PowerShell l'operazione di ripristino è completata quando sono stati creati i dischi e le informazioni sulla configurazione dal punto di ripristino</span><span class="sxs-lookup"><span data-stu-id="60c6a-203">With PowerShell, the restore operation is complete once the disks and configuration information from the recovery point are created.</span></span>

> [!NOTE]
> <span data-ttu-id="60c6a-204">L'operazione di ripristino non crea una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="60c6a-204">The restore operation does not create a virtual machine.</span></span>
>
>

<span data-ttu-id="60c6a-205">Per creare una macchina virtuale dal disco, vedere la sezione [Creare la macchina virtuale da dischi archiviati](backup-azure-vms-automation.md#create-a-vm-from-stored-disks).</span><span class="sxs-lookup"><span data-stu-id="60c6a-205">To create a virtual machine from disk, see the section, [Create the VM from stored disks](backup-azure-vms-automation.md#create-a-vm-from-stored-disks).</span></span> <span data-ttu-id="60c6a-206">I passaggi di base per ripristinare una macchina virtuale di Azure sono:</span><span class="sxs-lookup"><span data-stu-id="60c6a-206">The basic steps to restore an Azure VM are:</span></span>

* <span data-ttu-id="60c6a-207">Selezionare la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="60c6a-207">Select the VM</span></span>
* <span data-ttu-id="60c6a-208">Scegliere un punto di ripristino</span><span class="sxs-lookup"><span data-stu-id="60c6a-208">Choose a recovery point</span></span>
* <span data-ttu-id="60c6a-209">Ripristinare i dischi</span><span class="sxs-lookup"><span data-stu-id="60c6a-209">Restore the disks</span></span>
* <span data-ttu-id="60c6a-210">Creare la macchina virtuale da dischi archiviati</span><span class="sxs-lookup"><span data-stu-id="60c6a-210">Create the VM from stored disks</span></span>

<span data-ttu-id="60c6a-211">Il grafico seguente mostra la gerarchia degli oggetti da RecoveryServicesVault fino a BackupRecoveryPoint.</span><span class="sxs-lookup"><span data-stu-id="60c6a-211">The following graphic shows the object hierarchy from the RecoveryServicesVault down to the BackupRecoveryPoint.</span></span>

![Gerarchia di oggetti dei servizi di ripristino con BackupContainer](./media/backup-azure-vms-arm-automation/backuprecoverypoint-only.png)

<span data-ttu-id="60c6a-213">Per ripristinare i dati di backup, identificare l'elemento sottoposto a backup e il punto di ripristino che contiene i dati temporizzati.</span><span class="sxs-lookup"><span data-stu-id="60c6a-213">To restore backup data, identify the backed-up item and the recovery point that holds the point-in-time data.</span></span> <span data-ttu-id="60c6a-214">Usare il cmdlet **[Restore-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)** per ripristinare i dati dall'insieme di credenziali nell'account del cliente.</span><span class="sxs-lookup"><span data-stu-id="60c6a-214">Use the **[Restore-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)** cmdlet to restore data from the vault to the customer's account.</span></span>

### <a name="select-the-vm"></a><span data-ttu-id="60c6a-215">Selezionare la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="60c6a-215">Select the VM</span></span>
<span data-ttu-id="60c6a-216">Per ottenere l'oggetto di PowerShell che identifica l'elemento di backup corretto, iniziare dal contenitore nell'insieme di credenziali e procedere verso il basso nella gerarchia degli oggetti.</span><span class="sxs-lookup"><span data-stu-id="60c6a-216">To get the PowerShell object that identifies the right backup item, start from the container in the vault, and work your way down the object hierarchy.</span></span> <span data-ttu-id="60c6a-217">Per selezionare il contenitore che rappresenta la macchina virtuale, usare il cmdlet **[Get-AzureRmRecoveryServicesBackupContainer](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)** e inviarlo tramite pipe al cmdlet **[Get-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)**.</span><span class="sxs-lookup"><span data-stu-id="60c6a-217">To select the container that represents the VM, use the **[Get-AzureRmRecoveryServicesBackupContainer](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)** cmdlet and pipe that to the **[Get-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)** cmdlet.</span></span>

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer  -ContainerType "AzureVM" –Status "Registered" -FriendlyName "V2VM"
PS C:\> $backupitem = Get-AzureRmRecoveryServicesBackupItem –Container $namedContainer  –WorkloadType "AzureVM"
```

### <a name="choose-a-recovery-point"></a><span data-ttu-id="60c6a-218">Scegliere un punto di ripristino</span><span class="sxs-lookup"><span data-stu-id="60c6a-218">Choose a recovery point</span></span>
<span data-ttu-id="60c6a-219">Usare il cmdlet **[Get-AzureRmRecoveryServicesBackupRecoveryPoint](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)** per elencare tutti i punti di recupero dell'elemento di backup.</span><span class="sxs-lookup"><span data-stu-id="60c6a-219">Use the **[Get-AzureRmRecoveryServicesBackupRecoveryPoint](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)** cmdlet to list all recovery points for the backup item.</span></span> <span data-ttu-id="60c6a-220">Quindi scegliere il punto di ripristino per ripristinare.</span><span class="sxs-lookup"><span data-stu-id="60c6a-220">Then choose the recovery point to restore.</span></span> <span data-ttu-id="60c6a-221">Se non si sa quale punto di ripristino usare, è consigliabile scegliere il punto più recente RecoveryPointType = AppConsistent nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="60c6a-221">If you are unsure which recovery point to use, it is a good practice to choose the most recent RecoveryPointType = AppConsistent point in the list.</span></span>

<span data-ttu-id="60c6a-222">Nello script seguente la variabile **$rp** è una matrice di punti di recupero per l'elemento di backup selezionato negli ultimi sette giorni.</span><span class="sxs-lookup"><span data-stu-id="60c6a-222">In the following script, the variable, **$rp**, is an array of recovery points for the selected backup item, from the past seven days.</span></span> <span data-ttu-id="60c6a-223">La matrice viene ordinata in ordine inverso di tempo con il punto di ripristino più recente in posizione 0 nell'indice.</span><span class="sxs-lookup"><span data-stu-id="60c6a-223">The array is sorted in reverse order of time with the latest recovery point at index 0.</span></span> <span data-ttu-id="60c6a-224">Per scegliere il punto di ripristino, usare l'indicizzazione standard della matrice di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="60c6a-224">Use standard PowerShell array indexing to pick the recovery point.</span></span> <span data-ttu-id="60c6a-225">Nell'esempio $rp [0] seleziona il punto di ripristino più recente.</span><span class="sxs-lookup"><span data-stu-id="60c6a-225">In the example, $rp[0] selects the latest recovery point.</span></span>

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



### <a name="restore-the-disks"></a><span data-ttu-id="60c6a-226">Ripristinare i dischi</span><span class="sxs-lookup"><span data-stu-id="60c6a-226">Restore the disks</span></span>
<span data-ttu-id="60c6a-227">Per ripristinare i dati e la configurazione di un elemento di backup a un punto di recupero, usare il cmdlet **[Restore-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)**.</span><span class="sxs-lookup"><span data-stu-id="60c6a-227">Use the **[Restore-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)** cmdlet to restore a backup item's data and configuration to a recovery point.</span></span> <span data-ttu-id="60c6a-228">Dopo aver identificato un punto di ripristino, usarlo come valore per il parametro **-RecoveryPoint** .</span><span class="sxs-lookup"><span data-stu-id="60c6a-228">Once you have identified a recovery point, use it as the value for the **-RecoveryPoint** parameter.</span></span> <span data-ttu-id="60c6a-229">Nell'esempio di codice precedente **$rp [0]** è il punto di ripristino da usare.</span><span class="sxs-lookup"><span data-stu-id="60c6a-229">In the previous sample code, **$rp[0]** was the recovery point to use.</span></span> <span data-ttu-id="60c6a-230">Nell'esempio di codice seguente **$rp[0]** è il punto di ripristino da usare per il ripristino del disco.</span><span class="sxs-lookup"><span data-stu-id="60c6a-230">In the following sample code, **$rp[0]** is the recovery point to use for restoring the disk.</span></span>

<span data-ttu-id="60c6a-231">Per ripristinare i dischi e le informazioni di configurazione:</span><span class="sxs-lookup"><span data-stu-id="60c6a-231">To restore the disks and configuration information:</span></span>

```
PS C:\> $restorejob = Restore-AzureRmRecoveryServicesBackupItem -RecoveryPoint $rp[0] -StorageAccountName "DestAccount" -StorageAccountResourceGroupName "DestRG"
PS C:\> $restorejob
WorkloadName     Operation          Status               StartTime                 EndTime            JobID
------------     ---------          ------               ---------                 -------          ----------
V2VM              Restore           InProgress           4/23/2016 5:00:30 PM                        cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

<span data-ttu-id="60c6a-232">Usare il cmdlet **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)** per attendere il completamento del processo di ripristino.</span><span class="sxs-lookup"><span data-stu-id="60c6a-232">Use the **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)** cmdlet to wait for the Restore job to complete.</span></span>

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $restorejob -Timeout 43200
```

<span data-ttu-id="60c6a-233">Dopo il completamento del processo di ripristino, usare il cmdlet **[Get-AzureRmRecoveryServicesBackupJobDetails](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjobdetails)** per ottenere i dettagli dell'operazione di ripristino.</span><span class="sxs-lookup"><span data-stu-id="60c6a-233">Once the Restore job has completed, use the **[Get-AzureRmRecoveryServicesBackupJobDetails](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjobdetails)** cmdlet to get the details of the restore operation.</span></span> <span data-ttu-id="60c6a-234">La proprietà JobDetails contiene le informazioni necessarie per ricreare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="60c6a-234">The JobDetails property has the information needed to rebuild the VM.</span></span>

```
PS C:\> $restorejob = Get-AzureRmRecoveryServicesBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmRecoveryServicesBackupJobDetails -Job $restorejob
```

<span data-ttu-id="60c6a-235">Dopo aver ripristinato i dischi, passare alla sezione successiva per creare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="60c6a-235">Once you restore the disks, go to the next section to create the VM.</span></span>

## <a name="create-a-vm-from-restored-disks"></a><span data-ttu-id="60c6a-236">Creare una macchina virtuale da dischi ripristinati</span><span class="sxs-lookup"><span data-stu-id="60c6a-236">Create a VM from restored disks</span></span>
<span data-ttu-id="60c6a-237">Dopo aver ripristinato i dischi, seguire questa procedura per creare e configurare la macchina virtuale dal disco.</span><span class="sxs-lookup"><span data-stu-id="60c6a-237">After you have restored the disks, use these steps to create and configure the virtual machine from disk.</span></span>

> [!NOTE]
> <span data-ttu-id="60c6a-238">Per creare macchine virtuali crittografate da dischi ripristinati, il ruolo di Azure deve disporre dell'autorizzazione per eseguire l'azione, ovvero **Microsoft.KeyVault/vaults/deploy/action**.</span><span class="sxs-lookup"><span data-stu-id="60c6a-238">To create encrypted VMs from restored disks, your Azure role must have permission to perform the action, **Microsoft.KeyVault/vaults/deploy/action**.</span></span> <span data-ttu-id="60c6a-239">Se il ruolo non dispone di questa autorizzazione, crearne uno personalizzato con questa azione.</span><span class="sxs-lookup"><span data-stu-id="60c6a-239">If your role does not have this permission, create a custom role with this action.</span></span> <span data-ttu-id="60c6a-240">Per altre informazioni, vedere [Ruoli personalizzati nel Controllo degli accessi in base al ruolo di Azure](../active-directory/role-based-access-control-custom-roles.md).</span><span class="sxs-lookup"><span data-stu-id="60c6a-240">For more information, see [Custom Roles in Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span></span>
>
>

1. <span data-ttu-id="60c6a-241">Ricercare i dettagli del processo nelle proprietà del disco ripristinato.</span><span class="sxs-lookup"><span data-stu-id="60c6a-241">Query the restored disk properties for the job details.</span></span>

  ```
  PS C:\> $properties = $details.properties
  PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
  PS C:\> $containerName = $properties["Config Blob Container Name"]
  PS C:\> $blobName = $properties["Config Blob Name"]
  ```

2. <span data-ttu-id="60c6a-242">Impostare il contesto di archiviazione di Azure e ripristinare il file di configurazione JSON.</span><span class="sxs-lookup"><span data-stu-id="60c6a-242">Set the Azure storage context and restore the JSON configuration file.</span></span>

    ```
    PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName "testvault"
    PS C:\> $destination_path = "C:\vmconfig.json"
    PS C:\> Get-AzureStorageBlobContent -Container $containerName -Blob $blobName -Destination $destination_path
    PS C:\> $obj = ((Get-Content -Path $destination_path -Raw -Encoding Unicode)).TrimEnd([char]0x00) | ConvertFrom-Json
    ```

3. <span data-ttu-id="60c6a-243">Usare il file di configurazione JSON per creare la configurazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="60c6a-243">Use the JSON configuration file to create the VM configuration.</span></span>

    ```
   PS C:\> $vm = New-AzureRmVMConfig -VMSize $obj.'properties.hardwareProfile'.vmSize -VMName "testrestore"
    ```

4. <span data-ttu-id="60c6a-244">Collegare il disco del sistema operativo e i dischi dei dati.</span><span class="sxs-lookup"><span data-stu-id="60c6a-244">Attach the OS disk and data disks.</span></span> <span data-ttu-id="60c6a-245">A seconda della configurazione delle macchine virtuali, fare clic sul collegamento per visualizzare i rispettivi cmdlet pertinente:</span><span class="sxs-lookup"><span data-stu-id="60c6a-245">Depending on the configuration of your VMs, click on the relevant link to view respective cmdlets:</span></span> 
    - [<span data-ttu-id="60c6a-246">Macchine virtuali non gestiti, non crittografato</span><span class="sxs-lookup"><span data-stu-id="60c6a-246">Non-managed, non-encrypted VMs</span></span>](#non-managed-non-encrypted-vms)
    - [<span data-ttu-id="60c6a-247">Macchine virtuali non gestiti, crittografate (solo BEK)</span><span class="sxs-lookup"><span data-stu-id="60c6a-247">Non-managed, encrypted VMs (BEK only)</span></span>](#non-managed-encrypted-vms-bek-only)
    - [<span data-ttu-id="60c6a-248">Macchine virtuali non gestiti, crittografate (BEK e KEK)</span><span class="sxs-lookup"><span data-stu-id="60c6a-248">Non-managed, encrypted VMs (BEK and KEK)</span></span>](#non-managed-encrypted-vms-bek-and-kek)
    - [<span data-ttu-id="60c6a-249">Macchine virtuali gestite e non crittografati</span><span class="sxs-lookup"><span data-stu-id="60c6a-249">Managed, non-encrypted VMs</span></span>](#managed-non-encrypted-vms)
    - [<span data-ttu-id="60c6a-250">Macchine virtuali gestite, crittografate (BEK e KEK)</span><span class="sxs-lookup"><span data-stu-id="60c6a-250">Managed, encrypted VMs (BEK and KEK)</span></span>](#managed-encrypted-vms-bek-and-kek)
    
    #### <a name="non-managed-non-encrypted-vms"></a><span data-ttu-id="60c6a-251">Macchine virtuali non gestite, non crittografate</span><span class="sxs-lookup"><span data-stu-id="60c6a-251">Non-managed, non-encrypted VMs</span></span>

    <span data-ttu-id="60c6a-252">Usare l'esempio seguente per macchine virtuali non gestite e non crittografate.</span><span class="sxs-lookup"><span data-stu-id="60c6a-252">Use the following sample for non-managed, non-encrypted VMs.</span></span>

    ```
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.'properties.StorageProfile'.osDisk.vhd.Uri -CreateOption "Attach"
    PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.'properties.StorageProfile'.OsDisk.OsType
    PS C:\> foreach($dd in $obj.'properties.StorageProfile'.DataDisks)
    {
    $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.vhd.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption "Attach"
    }
    ```

    #### <a name="non-managed-encrypted-vms-bek-only"></a><span data-ttu-id="60c6a-253">Macchine virtuali non gestite, crittografate (solo con BEK)</span><span class="sxs-lookup"><span data-stu-id="60c6a-253">Non-managed, encrypted VMs (BEK only)</span></span>

    <span data-ttu-id="60c6a-254">Per le macchine virtuali non gestite e crittografate (solo con BEK), è necessario ripristinare il segreto nell'insieme di credenziali delle chiavi prima di collegare i dischi.</span><span class="sxs-lookup"><span data-stu-id="60c6a-254">For non-managed, encrypted VMs (encrypted using BEK only), you need to restore the secret to the key vault before you can attach disks.</span></span> <span data-ttu-id="60c6a-255">Per altre informazioni, vedere l'articolo [Ripristinare una macchina virtuale codificata da un punto di ripristino di Backup di Azure](backup-azure-restore-key-secret.md).</span><span class="sxs-lookup"><span data-stu-id="60c6a-255">For more information, please see the article, [Restore an encrypted virtual machine from an Azure Backup recovery point](backup-azure-restore-key-secret.md).</span></span> <span data-ttu-id="60c6a-256">L'esempio seguente illustra come collegare dischi del sistema operativo e i dati per le macchine virtuali crittografate.</span><span class="sxs-lookup"><span data-stu-id="60c6a-256">The following sample shows how to attach OS and data disks for encrypted VMs.</span></span>

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

    #### <a name="non-managed-encrypted-vms-bek-and-kek"></a><span data-ttu-id="60c6a-257">Macchine virtuali non gestite, crittografate (con BEK e KEK)</span><span class="sxs-lookup"><span data-stu-id="60c6a-257">Non-managed, encrypted VMs (BEK and KEK)</span></span>

    <span data-ttu-id="60c6a-258">Per le macchine virtuali non gestite e crittografate (con BEK e KEK), è necessario ripristinare la chiave e il segreto nell'insieme di credenziali delle chiavi prima di collegare i dischi.</span><span class="sxs-lookup"><span data-stu-id="60c6a-258">For non-managed, encrypted VMs (encrypted using BEK and KEK), you need to restore the key and secret to the key vault before you can attach disks.</span></span> <span data-ttu-id="60c6a-259">Per altre informazioni, vedere l'articolo [Ripristinare una macchina virtuale codificata da un punto di ripristino di Backup di Azure](backup-azure-restore-key-secret.md).</span><span class="sxs-lookup"><span data-stu-id="60c6a-259">For more information, please see the article, [Restore an encrypted virtual machine from an Azure Backup recovery point](backup-azure-restore-key-secret.md).</span></span> <span data-ttu-id="60c6a-260">L'esempio seguente illustra come collegare dischi del sistema operativo e i dati per le macchine virtuali crittografate.</span><span class="sxs-lookup"><span data-stu-id="60c6a-260">The following sample shows how to attach OS and data disks for encrypted VMs.</span></span>

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

    #### <a name="managed-non-encrypted-vms"></a><span data-ttu-id="60c6a-261">Macchine virtuali gestite, non crittografate</span><span class="sxs-lookup"><span data-stu-id="60c6a-261">Managed, non-encrypted VMs</span></span>

    <span data-ttu-id="60c6a-262">Per macchine virtuali gestite e non crittografate, è necessario creare dischi gestiti dall'archiviazione BLOB e quindi collegarli.</span><span class="sxs-lookup"><span data-stu-id="60c6a-262">For managed non-encrypted VMs, you'll need to create managed disks from blob storage, and then attach the disks.</span></span> <span data-ttu-id="60c6a-263">Per informazioni dettagliate, vedere l'articolo [Collegare un disco dati a una macchina virtuale Windows con PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="60c6a-263">For in-depth information, see the article, [Attach a data disk to a Windows VM using PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span></span> <span data-ttu-id="60c6a-264">Il codice di esempio seguente illustra come collegare dischi dati per macchine virtuali non crittografate.</span><span class="sxs-lookup"><span data-stu-id="60c6a-264">The following sample code shows how to attach the data disks for managed non-encrypted VMs.</span></span>

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

    #### <a name="managed-encrypted-vms-bek-and-kek"></a><span data-ttu-id="60c6a-265">Macchine virtuali gestite, crittografate (con BEK e KEK)</span><span class="sxs-lookup"><span data-stu-id="60c6a-265">Managed, encrypted VMs (BEK and KEK)</span></span>

    <span data-ttu-id="60c6a-266">Per le macchine virtuali gestite e crittografate (con BEK e KEK) , è necessario creare dischi gestiti dall'archiviazione BLOB e quindi collegarli.</span><span class="sxs-lookup"><span data-stu-id="60c6a-266">For managed encrypted VMs (encrypted using BEK and KEK), you'll need to create managed disks from blob storage, and then attach the disks.</span></span> <span data-ttu-id="60c6a-267">Per informazioni dettagliate, vedere l'articolo [Collegare un disco dati a una macchina virtuale Windows con PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="60c6a-267">For in-depth information, see the article, [Attach a data disk to a Windows VM using PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span></span> <span data-ttu-id="60c6a-268">Il codice di esempio seguente illustra come collegare dischi di dati per le macchine virtuali crittografate.</span><span class="sxs-lookup"><span data-stu-id="60c6a-268">The following sample code shows how to attach the data disks for managed encrypted VMs.</span></span>

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

5. <span data-ttu-id="60c6a-269">Configurare le impostazioni di rete.</span><span class="sxs-lookup"><span data-stu-id="60c6a-269">Set the Network settings.</span></span>

    ```
    PS C:\> $nicName="p1234"
    PS C:\> $pip = New-AzureRmPublicIpAddress -Name $nicName -ResourceGroupName "test" -Location "WestUS" -AllocationMethod Dynamic
    PS C:\> $vnet = Get-AzureRmVirtualNetwork -Name "testvNET" -ResourceGroupName "test"
    PS C:\> $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName "test" -Location "WestUS" -SubnetId $vnet.Subnets[$subnetindex].Id -PublicIpAddressId $pip.Id
    PS C:\> $vm=Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
    ```
6. <span data-ttu-id="60c6a-270">Creare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="60c6a-270">Create the virtual machine.</span></span>

    ```    
    PS C:\> New-AzureRmVM -ResourceGroupName "test" -Location "WestUS" -VM $vm
    ```

## <a name="next-steps"></a><span data-ttu-id="60c6a-271">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="60c6a-271">Next steps</span></span>
<span data-ttu-id="60c6a-272">Se si preferisce usare PowerShell per coinvolgere le risorse di Azure, vedere l'articolo PowerShell [Distribuire e gestire il backup in Azure per server Windows/client Windows mediante PowerShell](backup-client-automation.md).</span><span class="sxs-lookup"><span data-stu-id="60c6a-272">If you prefer to use PowerShell to engage with your Azure resources, see the PowerShell article, [Deploy and Manage Backup for Windows Server](backup-client-automation.md).</span></span> <span data-ttu-id="60c6a-273">Se si gestiscono i backup DPM, vedere l'articolo [Distribuire e gestire il backup per DPM](backup-dpm-automation.md).</span><span class="sxs-lookup"><span data-stu-id="60c6a-273">If you manage DPM backups, see the article, [Deploy and Manage Backup for DPM](backup-dpm-automation.md).</span></span> <span data-ttu-id="60c6a-274">Entrambi gli articoli prevedono due versioni: una per le distribuzioni con Resource Manager, l'altra per le distribuzioni classiche.</span><span class="sxs-lookup"><span data-stu-id="60c6a-274">Both of these articles have a version for Resource Manager deployments and Classic deployments.</span></span>  
