---
title: aaaAutomated Backup per SQL Server le macchine virtuali (classico) | Documenti Microsoft
description: "Vengono illustrate funzionalità Backup automatizzato hello per SQL Server in esecuzione in Azure VM con Gestione risorse. "
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 3333e830-8a60-42f5-9f44-8e02e9868d7b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 5d8f0412578c2d86edc6e54093a5da4891d3847e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-for-sql-server-in-azure-virtual-machines-classic"></a><span data-ttu-id="dbe6a-103">Backup automatico per SQL Server in macchine virtuali di Azure (distribuzione classica)</span><span class="sxs-lookup"><span data-stu-id="dbe6a-103">Automated Backup for SQL Server in Azure Virtual Machines (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="dbe6a-104">Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="dbe6a-104">Resource Manager</span></span>](../sql/virtual-machines-windows-sql-automated-backup.md)
> * [<span data-ttu-id="dbe6a-105">Classico</span><span class="sxs-lookup"><span data-stu-id="dbe6a-105">Classic</span></span>](../classic/sql-automated-backup.md)
> 
> 

<span data-ttu-id="dbe6a-106">Backup automatizzato configura automaticamente [tooMicrosoft Backup gestito Azure](https://msdn.microsoft.com/library/dn449496.aspx) per tutti i database nuovi ed esistenti in una macchina virtuale di Azure che esegue SQL Server 2014 Standard o Enterprise.</span><span class="sxs-lookup"><span data-stu-id="dbe6a-106">Automated Backup automatically configures [Managed Backup tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) for all existing and new databases on an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> <span data-ttu-id="dbe6a-107">In questo modo tooconfigure normali backup di database che utilizzano l'archiviazione blob di Azure durevole.</span><span class="sxs-lookup"><span data-stu-id="dbe6a-107">This enables you tooconfigure regular database backups that utilize durable Azure blob storage.</span></span> <span data-ttu-id="dbe6a-108">Backup automatizzato dipende hello [estensione di SQL Server IaaS Agent](../classic/sql-server-agent-extension.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dbe6a-108">Automated Backup depends on hello [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="dbe6a-109">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="dbe6a-109">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="dbe6a-110">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="dbe6a-110">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="dbe6a-111">Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="dbe6a-111">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="dbe6a-112">tooview hello Gestione risorse di questo articolo, vedere [Backup automatizzato per SQL Server in Gestione risorse di macchine virtuali Azure](../sql/virtual-machines-windows-sql-automated-backup.md).</span><span class="sxs-lookup"><span data-stu-id="dbe6a-112">tooview hello Resource Manager version of this article, see [Automated Backup for SQL Server in Azure Virtual Machines Resource Manager](../sql/virtual-machines-windows-sql-automated-backup.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dbe6a-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="dbe6a-113">Prerequisites</span></span>
<span data-ttu-id="dbe6a-114">toouse Backup automatizzato, prendere in considerazione hello seguenti prerequisiti:</span><span class="sxs-lookup"><span data-stu-id="dbe6a-114">toouse Automated Backup, consider hello following prerequisites:</span></span>

<span data-ttu-id="dbe6a-115">**Sistema operativo**:</span><span class="sxs-lookup"><span data-stu-id="dbe6a-115">**Operating System**:</span></span>

* <span data-ttu-id="dbe6a-116">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="dbe6a-116">Windows Server 2012</span></span>
* <span data-ttu-id="dbe6a-117">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="dbe6a-117">Windows Server 2012 R2</span></span>
* <span data-ttu-id="dbe6a-118">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="dbe6a-118">Windows Server 2016</span></span>

<span data-ttu-id="dbe6a-119">**Versione/edizione di SQL Server**:</span><span class="sxs-lookup"><span data-stu-id="dbe6a-119">**SQL Server version/edition**:</span></span>

* <span data-ttu-id="dbe6a-120">SQL Server 2014 Standard</span><span class="sxs-lookup"><span data-stu-id="dbe6a-120">SQL Server 2014 Standard</span></span>
* <span data-ttu-id="dbe6a-121">SQL Server 2014 Enterprise</span><span class="sxs-lookup"><span data-stu-id="dbe6a-121">SQL Server 2014 Enterprise</span></span>

> [!NOTE]
> <span data-ttu-id="dbe6a-122">SQL Server 2016 non supporta ancora il backup automatizzato.</span><span class="sxs-lookup"><span data-stu-id="dbe6a-122">SQL Server 2016 is not yet supported for Automated Backup.</span></span>
> 
> 

<span data-ttu-id="dbe6a-123">**Configurazione del database**:</span><span class="sxs-lookup"><span data-stu-id="dbe6a-123">**Database configuration**:</span></span>

* <span data-ttu-id="dbe6a-124">Database di destinazione devono utilizzare il modello di recupero con registrazione completa hello.</span><span class="sxs-lookup"><span data-stu-id="dbe6a-124">Target databases must use hello full recovery model.</span></span>

<span data-ttu-id="dbe6a-125">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="dbe6a-125">**Azure PowerShell**:</span></span>

* <span data-ttu-id="dbe6a-126">[Installare i comandi di PowerShell di Azure più recenti hello](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="dbe6a-126">[Install hello latest Azure PowerShell commands](/powershell/azure/overview).</span></span>

<span data-ttu-id="dbe6a-127">**Estensione di SQL Server IaaS**:</span><span class="sxs-lookup"><span data-stu-id="dbe6a-127">**SQL Server IaaS Extension**:</span></span>

* <span data-ttu-id="dbe6a-128">[Installare l'estensione di SQL Server IaaS hello](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="dbe6a-128">[Install hello SQL Server IaaS Extension](../classic/sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="dbe6a-129">Impostazioni</span><span class="sxs-lookup"><span data-stu-id="dbe6a-129">Settings</span></span>
<span data-ttu-id="dbe6a-130">Hello nella tabella seguente vengono descritte hello opzioni che possono essere configurate per il Backup automatizzato.</span><span class="sxs-lookup"><span data-stu-id="dbe6a-130">hello following table describes hello options that can be configured for Automated Backup.</span></span> <span data-ttu-id="dbe6a-131">Per le macchine virtuali classiche, è necessario utilizzare PowerShell tooconfigure queste impostazioni.</span><span class="sxs-lookup"><span data-stu-id="dbe6a-131">For classic VMs, you must use PowerShell tooconfigure these settings.</span></span>

| <span data-ttu-id="dbe6a-132">Impostazione</span><span class="sxs-lookup"><span data-stu-id="dbe6a-132">Setting</span></span> | <span data-ttu-id="dbe6a-133">Intervallo (impostazione predefinita)</span><span class="sxs-lookup"><span data-stu-id="dbe6a-133">Range (Default)</span></span> | <span data-ttu-id="dbe6a-134">Descrizione</span><span class="sxs-lookup"><span data-stu-id="dbe6a-134">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dbe6a-135">**Backup automatico**</span><span class="sxs-lookup"><span data-stu-id="dbe6a-135">**Automated Backup**</span></span> |<span data-ttu-id="dbe6a-136">Enable/Disable (disabilitato)</span><span class="sxs-lookup"><span data-stu-id="dbe6a-136">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="dbe6a-137">Abilita o disabilita il backup automatico per una macchina virtuale di Azure in cui viene eseguito SQL Server 2014 Standard o Enterprise.</span><span class="sxs-lookup"><span data-stu-id="dbe6a-137">Enables or disables Automated Backup for an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> |
| <span data-ttu-id="dbe6a-138">**Periodo di conservazione**</span><span class="sxs-lookup"><span data-stu-id="dbe6a-138">**Retention Period**</span></span> |<span data-ttu-id="dbe6a-139">1-30 giorni (30 giorni)</span><span class="sxs-lookup"><span data-stu-id="dbe6a-139">1-30 days (30 days)</span></span> |<span data-ttu-id="dbe6a-140">numero di Hello di giorni tooretain una copia di backup.</span><span class="sxs-lookup"><span data-stu-id="dbe6a-140">hello number of days tooretain a backup.</span></span> |
| <span data-ttu-id="dbe6a-141">**Storage Account**</span><span class="sxs-lookup"><span data-stu-id="dbe6a-141">**Storage Account**</span></span> |<span data-ttu-id="dbe6a-142">Account di archiviazione di Azure (account di archiviazione hello creato per hello specificato VM)</span><span class="sxs-lookup"><span data-stu-id="dbe6a-142">Azure storage account (hello storage account created for hello specified VM)</span></span> |<span data-ttu-id="dbe6a-143">Toouse un account di archiviazione di Azure per archiviare i file di Backup automatizzato nell'archiviazione blob.</span><span class="sxs-lookup"><span data-stu-id="dbe6a-143">An Azure storage account toouse for storing Automated Backup files in blob storage.</span></span> <span data-ttu-id="dbe6a-144">Un contenitore viene creato in questo percorso toostore tutti i file di backup.</span><span class="sxs-lookup"><span data-stu-id="dbe6a-144">A container is created at this location toostore all backup files.</span></span> <span data-ttu-id="dbe6a-145">file di backup Hello convenzione di denominazione include hello data, ora e nome del computer.</span><span class="sxs-lookup"><span data-stu-id="dbe6a-145">hello backup file naming convention includes hello date, time, and machine name.</span></span> |
| <span data-ttu-id="dbe6a-146">**Crittografia**</span><span class="sxs-lookup"><span data-stu-id="dbe6a-146">**Encryption**</span></span> |<span data-ttu-id="dbe6a-147">Enable/Disable (disabilitato)</span><span class="sxs-lookup"><span data-stu-id="dbe6a-147">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="dbe6a-148">Abilita o disabilita la crittografia.</span><span class="sxs-lookup"><span data-stu-id="dbe6a-148">Enables or disables encryption.</span></span> <span data-ttu-id="dbe6a-149">Quando è abilitata la crittografia, certificati hello backup hello toorestore utilizzati si trovano in hello specificato l'account di archiviazione in hello automaticbackup stesso contenitore usando hello stessa convenzione di denominazione.</span><span class="sxs-lookup"><span data-stu-id="dbe6a-149">When encryption is enabled, hello certificates used toorestore hello backup are located in hello specified storage account in hello same automaticbackup container using hello same naming convention.</span></span> <span data-ttu-id="dbe6a-150">Se la modifica di password hello, viene generato un nuovo certificato con la password, ma vecchio certificato hello rimane toorestore eventuale backup precedente.</span><span class="sxs-lookup"><span data-stu-id="dbe6a-150">If hello password changes, a new certificate is generated with that password, but hello old certificate remains toorestore prior backups.</span></span> |
| <span data-ttu-id="dbe6a-151">**Password**</span><span class="sxs-lookup"><span data-stu-id="dbe6a-151">**Password**</span></span> |<span data-ttu-id="dbe6a-152">Testo della password (nessuno)</span><span class="sxs-lookup"><span data-stu-id="dbe6a-152">Password text (None)</span></span> |<span data-ttu-id="dbe6a-153">Password per le chiavi di crittografia.</span><span class="sxs-lookup"><span data-stu-id="dbe6a-153">A password for encryption keys.</span></span> <span data-ttu-id="dbe6a-154">Questa impostazione è necessaria solo se la crittografia è abilitata.</span><span class="sxs-lookup"><span data-stu-id="dbe6a-154">This is only required if encryption is enabled.</span></span> <span data-ttu-id="dbe6a-155">In ordine toorestore un backup crittografato, è necessario disporre la password corretta hello e del certificato correlato che è stato utilizzato in fase di hello hello del backup.</span><span class="sxs-lookup"><span data-stu-id="dbe6a-155">In order toorestore an encrypted backup, you must have hello correct password and related certificate that was used at hello time hello backup was taken.</span></span> | <span data-ttu-id="dbe6a-156">**Backup system databases** (Backup dei database di sistema)</span><span class="sxs-lookup"><span data-stu-id="dbe6a-156">**Backup system databases**</span></span> | <span data-ttu-id="dbe6a-157">Enable/Disable (disabilitato)</span><span class="sxs-lookup"><span data-stu-id="dbe6a-157">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="dbe6a-158">Eseguire backup completi di database master, modello e MSDB</span><span class="sxs-lookup"><span data-stu-id="dbe6a-158">Take full backups of Master, Model, and MSDB</span></span> |
| <span data-ttu-id="dbe6a-159">**Configure backup schedule** (Configura la pianificazione dei backup)</span><span class="sxs-lookup"><span data-stu-id="dbe6a-159">**Configure backup schedule**</span></span> | <span data-ttu-id="dbe6a-160">Manual/Automated (Automated) (Manuale/Automatizzato - Automatizzato)</span><span class="sxs-lookup"><span data-stu-id="dbe6a-160">Manual/Automated (Automated)</span></span> | <span data-ttu-id="dbe6a-161">Selezionare **automatizzata** tooautomatically sfruttare e accedere in base all'aumento delle dimensioni del log.</span><span class="sxs-lookup"><span data-stu-id="dbe6a-161">Select **Automated** tooautomatically take full and log backups based on log growth.</span></span> <span data-ttu-id="dbe6a-162">Selezionare **manuale** pianificazione hello toospecify per full e i backup del log.</span><span class="sxs-lookup"><span data-stu-id="dbe6a-162">Select **Manual** toospecify hello schedule for full and log backups.</span></span> |

## <a name="configuration-with-powershell"></a><span data-ttu-id="dbe6a-163">Configurazione con PowerShell</span><span class="sxs-lookup"><span data-stu-id="dbe6a-163">Configuration with PowerShell</span></span>
<span data-ttu-id="dbe6a-164">Nel seguente esempio di PowerShell di hello, Backup automatizzato è configurato per una VM esistente di SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="dbe6a-164">In hello following PowerShell example, Automated Backup is configured for an existing SQL Server 2014 VM.</span></span> <span data-ttu-id="dbe6a-165">Hello **New AzureVMSqlServerAutoBackupConfig** comando Configura backup toostore le impostazioni del Backup automatizzato hello nell'account di archiviazione Azure hello specificata dalla variabile hello $storageaccount.</span><span class="sxs-lookup"><span data-stu-id="dbe6a-165">hello **New-AzureVMSqlServerAutoBackupConfig** command configures hello Automated Backup settings toostore backups in hello Azure storage account specified by hello $storageaccount variable.</span></span> <span data-ttu-id="dbe6a-166">Questi backup verranno conservati per 10 giorni.</span><span class="sxs-lookup"><span data-stu-id="dbe6a-166">These backups will be retained for 10 days.</span></span> <span data-ttu-id="dbe6a-167">Hello **Set AzureVMSqlServerExtension** comando hello aggiornamenti specificato macchina virtuale di Azure con queste impostazioni.</span><span class="sxs-lookup"><span data-stu-id="dbe6a-167">hello **Set-AzureVMSqlServerExtension** command updates hello specified Azure VM with these settings.</span></span>

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

<span data-ttu-id="dbe6a-168">Potrebbe richiedere diversi minuti tooinstall e configurare hello agente IaaS di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="dbe6a-168">It could take several minutes tooinstall and configure hello SQL Server IaaS Agent.</span></span>

<span data-ttu-id="dbe6a-169">crittografia tooenable, modificare hello precedente script toopass hello parametro EnableEncryption e una password (stringa sicura) per il parametro CertificatePassword hello.</span><span class="sxs-lookup"><span data-stu-id="dbe6a-169">tooenable encryption, modify hello previous script toopass hello EnableEncryption parameter along with a password (secure string) for hello CertificatePassword parameter.</span></span> <span data-ttu-id="dbe6a-170">Hello seguente script abilita le impostazioni di Backup automatizzato hello nell'esempio precedente hello e aggiunge la crittografia.</span><span class="sxs-lookup"><span data-stu-id="dbe6a-170">hello following script enables hello Automated Backup settings in hello previous example and adds encryption.</span></span>

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $password = "P@ssw0rd"
    $encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force  
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10 -EnableEncryption -CertificatePassword $encryptionpassword

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

<span data-ttu-id="dbe6a-171">backup automatico toodisable, esecuzione hello stesso script senza hello **-abilitare** toohello parametro **New AzureVMSqlServerAutoBackupConfig**.</span><span class="sxs-lookup"><span data-stu-id="dbe6a-171">toodisable automatic backup, run hello same script without hello **-Enable** parameter toohello **New-AzureVMSqlServerAutoBackupConfig**.</span></span> <span data-ttu-id="dbe6a-172">Come per l'installazione, può richiedere diversi minuti toodisable Backup automatizzato.</span><span class="sxs-lookup"><span data-stu-id="dbe6a-172">As with installation, it can take several minutes toodisable Automated Backup.</span></span>

> [!NOTE]
> <span data-ttu-id="dbe6a-173">Disabilitazione e disinstallazione di SQL Server IaaS Agent hello non rimuove le impostazioni di Backup gestito di hello configurato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="dbe6a-173">Disabling and uninstalling hello SQL Server IaaS Agent does not remove hello previously configured Managed Backup settings.</span></span> <span data-ttu-id="dbe6a-174">È necessario disabilitare i Backup automatizzato prima di disabilitare o disinstallare hello agente IaaS di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="dbe6a-174">You should disable Automated Backup before disabling or uninstalling hello SQL Server IaaS Agent.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="dbe6a-175">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dbe6a-175">Next steps</span></span>
<span data-ttu-id="dbe6a-176">Backup automatico configura backup gestito in Macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="dbe6a-176">Automated Backup configures Managed Backup on Azure VMs.</span></span> <span data-ttu-id="dbe6a-177">È importante troppo[, vedere la documentazione di hello per il Backup gestito](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello comportamento e le implicazioni.</span><span class="sxs-lookup"><span data-stu-id="dbe6a-177">So it is important too[review hello documentation for Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello behavior and implications.</span></span>

<span data-ttu-id="dbe6a-178">È possibile trovare ulteriori backup e ripristino istruzioni for SQL Server in macchine virtuali di Azure nel seguente argomento hello: [di Backup e ripristino per SQL Server in macchine virtuali di Azure](../sql/virtual-machines-windows-sql-backup-recovery.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dbe6a-178">You can find additional backup and restore guidance for SQL Server on Azure VMs in hello following topic: [Backup and Restore for SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-backup-recovery.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span></span>

<span data-ttu-id="dbe6a-179">Per informazioni sulle altre attività di automazione disponibili, vedere [Estensione Agente IaaS di SQL Server](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="dbe6a-179">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span></span>

<span data-ttu-id="dbe6a-180">Per altre informazioni sull'esecuzione di SQL Server nelle VM di Azure, vedere [Panoramica di SQL Server nelle macchine virtuali di Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dbe6a-180">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

