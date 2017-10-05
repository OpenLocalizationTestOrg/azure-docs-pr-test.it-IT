---
title: Backup automatico per macchine virtuali SQL Server 2014 in Azure | Documentazione Microsoft
description: "Viene illustrata la funzionalità di backup automatico per macchine virtuali SQL Server 2014 in esecuzione in Azure. Questo articolo si applica alle macchine virtuali che usano Resource Manager."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: bdc63fd1-db49-4e76-87d5-b5c6a890e53c
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 91aab896dd5f06c950ee0ed8f36cc6a953d91611
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="automated-backup-for-sql-server-2014-virtual-machines-resource-manager"></a><span data-ttu-id="18c3a-104">Backup automatico per macchine virtuali SQL Server 2014 (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="18c3a-104">Automated Backup for SQL Server 2014 Virtual Machines (Resource Manager)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="18c3a-105">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="18c3a-105">SQL Server 2014</span></span>](virtual-machines-windows-sql-automated-backup.md)
> * [<span data-ttu-id="18c3a-106">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="18c3a-106">SQL Server 2016</span></span>](virtual-machines-windows-sql-automated-backup-v2.md)

<span data-ttu-id="18c3a-107">Backup automatico Configura automaticamente il [backup gestito in Microsoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) per tutti i database nuovi ed esistenti in una macchina virtuale di Azure con SQL Server 2014 Standard o Enterprise in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="18c3a-107">Automated Backup automatically configures [Managed Backup to Microsoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) for all existing and new databases on an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> <span data-ttu-id="18c3a-108">In questo modo è possibile configurare i backup periodici del database che utilizzano l'archiviazione BLOB di Azure durevole.</span><span class="sxs-lookup"><span data-stu-id="18c3a-108">This enables you to configure regular database backups that utilize durable Azure blob storage.</span></span> <span data-ttu-id="18c3a-109">Il backup automatico dipende dall' [estensione dell'agente IaaS di SQL Server](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="18c3a-109">Automated Backup depends on the [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="18c3a-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="18c3a-110">Prerequisites</span></span>
<span data-ttu-id="18c3a-111">Per usare il backup automatico, tenere in considerazione i seguenti prerequisiti:</span><span class="sxs-lookup"><span data-stu-id="18c3a-111">To use Automated Backup, consider the following prerequisites:</span></span>

<span data-ttu-id="18c3a-112">**Sistema operativo**:</span><span class="sxs-lookup"><span data-stu-id="18c3a-112">**Operating System**:</span></span>

- <span data-ttu-id="18c3a-113">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="18c3a-113">Windows Server 2012</span></span>
- <span data-ttu-id="18c3a-114">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="18c3a-114">Windows Server 2012 R2</span></span>
- <span data-ttu-id="18c3a-115">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="18c3a-115">Windows Server 2016</span></span>

<span data-ttu-id="18c3a-116">**Versione/edizione di SQL Server**:</span><span class="sxs-lookup"><span data-stu-id="18c3a-116">**SQL Server version/edition**:</span></span>

- <span data-ttu-id="18c3a-117">SQL Server 2014 Standard</span><span class="sxs-lookup"><span data-stu-id="18c3a-117">SQL Server 2014 Standard</span></span>
- <span data-ttu-id="18c3a-118">SQL Server 2014 Enterprise</span><span class="sxs-lookup"><span data-stu-id="18c3a-118">SQL Server 2014 Enterprise</span></span>

> [!IMPORTANT]
> <span data-ttu-id="18c3a-119">Il backup automatico funziona con SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="18c3a-119">Automated Backup works with SQL Server 2014.</span></span> <span data-ttu-id="18c3a-120">Se si usa SQL Server 2016, è possibile usare il backup automatico versione 2 per eseguire il backup dei database.</span><span class="sxs-lookup"><span data-stu-id="18c3a-120">If you are using SQL Server 2016, you can use Automated Backup v2 to back up your databases.</span></span> <span data-ttu-id="18c3a-121">Per altre informazioni, vedere [Automated Backup v2 for SQL Server 2016 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup-v2.md) (Backup automatico versione 2 per macchine virtuali SQL Server 2016 in Azure).</span><span class="sxs-lookup"><span data-stu-id="18c3a-121">For more information, see [Automated Backup v2 for SQL Server 2016 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup-v2.md).</span></span>

<span data-ttu-id="18c3a-122">**Configurazione del database**:</span><span class="sxs-lookup"><span data-stu-id="18c3a-122">**Database configuration**:</span></span>

- <span data-ttu-id="18c3a-123">I database di destinazione devono usare il modello di recupero con registrazione completa.</span><span class="sxs-lookup"><span data-stu-id="18c3a-123">Target databases must use the full recovery model.</span></span> <span data-ttu-id="18c3a-124">Per altre informazioni sull'impatto del modello di recupero con registrazione completa sui backup, vedere [Backup con il modello di recupero con registrazione completa](https://technet.microsoft.com/library/ms190217.aspx).</span><span class="sxs-lookup"><span data-stu-id="18c3a-124">For more information about the impact of the full recovery model on backups, see [Backup Under the Full Recovery Model](https://technet.microsoft.com/library/ms190217.aspx).</span></span>
- <span data-ttu-id="18c3a-125">I database di destinazione devono trovarsi nell'istanza predefinita di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="18c3a-125">Target databases must be on the default SQL Server instance.</span></span> <span data-ttu-id="18c3a-126">L'estensione SQL Server IaaS non supporta le istanze denominate.</span><span class="sxs-lookup"><span data-stu-id="18c3a-126">The SQL Server IaaS Extension does not support named instances.</span></span>

<span data-ttu-id="18c3a-127">**Modello di distribuzione di Azure**:</span><span class="sxs-lookup"><span data-stu-id="18c3a-127">**Azure deployment model**:</span></span>

- <span data-ttu-id="18c3a-128">Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="18c3a-128">Resource Manager</span></span>

<span data-ttu-id="18c3a-129">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="18c3a-129">**Azure PowerShell**:</span></span>

- <span data-ttu-id="18c3a-130">[Installare i comandi di Azure PowerShell più recenti](/powershell/azure/overview) se si prevede di configurare il backup automatico con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="18c3a-130">[Install the latest Azure PowerShell commands](/powershell/azure/overview) if you plan to configure Automated Backup with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="18c3a-131">Il backup automatico si basa sull'estensione dell'agente IaaS di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="18c3a-131">Automated Backup relies on the SQL Server IaaS Agent Extension.</span></span> <span data-ttu-id="18c3a-132">Per impostazione predefinita, le attuali immagini della raccolta di macchine virtuali di SQL aggiungono questa estensione.</span><span class="sxs-lookup"><span data-stu-id="18c3a-132">Current SQL virtual machine gallery images add this extension by default.</span></span> <span data-ttu-id="18c3a-133">Per altre informazioni, vedere [Estensione Agente IaaS di SQL Server](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="18c3a-133">For more information, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="18c3a-134">Impostazioni</span><span class="sxs-lookup"><span data-stu-id="18c3a-134">Settings</span></span>

<span data-ttu-id="18c3a-135">Nella seguente tabella sono descritte le opzioni che possono essere configurate per il backup automatico.</span><span class="sxs-lookup"><span data-stu-id="18c3a-135">The following table describes the options that can be configured for Automated Backup.</span></span> <span data-ttu-id="18c3a-136">I passaggi di configurazione effettivi variano a seconda che venga usato il portale di Azure o i comandi di Windows PowerShell di Azure.</span><span class="sxs-lookup"><span data-stu-id="18c3a-136">The actual configuration steps vary depending on whether you use the Azure portal or Azure Windows PowerShell commands.</span></span>

| <span data-ttu-id="18c3a-137">Impostazione</span><span class="sxs-lookup"><span data-stu-id="18c3a-137">Setting</span></span> | <span data-ttu-id="18c3a-138">Intervallo (impostazione predefinita)</span><span class="sxs-lookup"><span data-stu-id="18c3a-138">Range (Default)</span></span> | <span data-ttu-id="18c3a-139">Descrizione</span><span class="sxs-lookup"><span data-stu-id="18c3a-139">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="18c3a-140">**Backup automatico**</span><span class="sxs-lookup"><span data-stu-id="18c3a-140">**Automated Backup**</span></span> | <span data-ttu-id="18c3a-141">Enable/Disable (disabilitato)</span><span class="sxs-lookup"><span data-stu-id="18c3a-141">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="18c3a-142">Abilita o disabilita il backup automatico per una macchina virtuale di Azure in cui viene eseguito SQL Server 2014 Standard o Enterprise.</span><span class="sxs-lookup"><span data-stu-id="18c3a-142">Enables or disables Automated Backup for an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> |
| <span data-ttu-id="18c3a-143">**Periodo di conservazione**</span><span class="sxs-lookup"><span data-stu-id="18c3a-143">**Retention Period**</span></span> | <span data-ttu-id="18c3a-144">1-30 giorni (30 giorni)</span><span class="sxs-lookup"><span data-stu-id="18c3a-144">1-30 days (30 days)</span></span> | <span data-ttu-id="18c3a-145">Numero di giorni di conservazione di un backup.</span><span class="sxs-lookup"><span data-stu-id="18c3a-145">The number of days to retain a backup.</span></span> |
| <span data-ttu-id="18c3a-146">**Storage Account**</span><span class="sxs-lookup"><span data-stu-id="18c3a-146">**Storage Account**</span></span> | <span data-ttu-id="18c3a-147">Account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="18c3a-147">Azure storage account</span></span> | <span data-ttu-id="18c3a-148">Account di archiviazione di Azure da usare per archiviare i file del backup automatico nell'archiviazione BLOB.</span><span class="sxs-lookup"><span data-stu-id="18c3a-148">An Azure storage account to use for storing Automated Backup files in blob storage.</span></span> <span data-ttu-id="18c3a-149">In questa posizione viene creato un contenitore per archiviare tutti i file di backup.</span><span class="sxs-lookup"><span data-stu-id="18c3a-149">A container is created at this location to store all backup files.</span></span> <span data-ttu-id="18c3a-150">La convenzione di denominazione dei file di backup include la data, l'ora e il nome del computer.</span><span class="sxs-lookup"><span data-stu-id="18c3a-150">The backup file naming convention includes the date, time, and machine name.</span></span> |
| <span data-ttu-id="18c3a-151">**Crittografia**</span><span class="sxs-lookup"><span data-stu-id="18c3a-151">**Encryption**</span></span> | <span data-ttu-id="18c3a-152">Enable/Disable (disabilitato)</span><span class="sxs-lookup"><span data-stu-id="18c3a-152">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="18c3a-153">Abilita o disabilita la crittografia.</span><span class="sxs-lookup"><span data-stu-id="18c3a-153">Enables or disables encryption.</span></span> <span data-ttu-id="18c3a-154">Quando è abilitata la crittografia, i certificati usati per ripristinare il backup sono contenuti nell'account di archiviazione specificato, nello stesso contenitore `automaticbackup` con la stessa convenzione di denominazione.</span><span class="sxs-lookup"><span data-stu-id="18c3a-154">When encryption is enabled, the certificates used to restore the backup are located in the specified storage account in the same `automaticbackup` container using the same naming convention.</span></span> <span data-ttu-id="18c3a-155">Se la password viene modificata, viene generato un nuovo certificato con tale password, ma il certificato precedente viene mantenuto per ripristinare i backup precedenti.</span><span class="sxs-lookup"><span data-stu-id="18c3a-155">If the password changes, a new certificate is generated with that password, but the old certificate remains to restore prior backups.</span></span> |
| <span data-ttu-id="18c3a-156">**Password**</span><span class="sxs-lookup"><span data-stu-id="18c3a-156">**Password**</span></span> | <span data-ttu-id="18c3a-157">Testo della password</span><span class="sxs-lookup"><span data-stu-id="18c3a-157">Password text</span></span> | <span data-ttu-id="18c3a-158">Password per le chiavi di crittografia.</span><span class="sxs-lookup"><span data-stu-id="18c3a-158">A password for encryption keys.</span></span> <span data-ttu-id="18c3a-159">Questa impostazione è necessaria solo se la crittografia è abilitata.</span><span class="sxs-lookup"><span data-stu-id="18c3a-159">This is only required if encryption is enabled.</span></span> <span data-ttu-id="18c3a-160">Per ripristinare un backup crittografato, è necessario disporre della password corretta e del certificato correlato usato al momento dell'esecuzione del backup.</span><span class="sxs-lookup"><span data-stu-id="18c3a-160">In order to restore an encrypted backup, you must have the correct password and related certificate that was used at the time the backup was taken.</span></span> |

## <a name="configuration-in-the-portal"></a><span data-ttu-id="18c3a-161">Configurazione nel Portale</span><span class="sxs-lookup"><span data-stu-id="18c3a-161">Configuration in the Portal</span></span>

<span data-ttu-id="18c3a-162">È possibile usare il portale di Azure per configurare il backup automatico durante il provisioning o per le macchine virtuali di SQL Server 2014 esistenti.</span><span class="sxs-lookup"><span data-stu-id="18c3a-162">You can use the Azure portal to configure Automated Backup during provisioning or for existing SQL Server 2014 VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="18c3a-163">Nuove VM</span><span class="sxs-lookup"><span data-stu-id="18c3a-163">New VMs</span></span>

<span data-ttu-id="18c3a-164">Usare il portale di Azure per configurare il backup automatico quando si crea una nuova macchina virtuale di SQL Server 2014 nel modello di distribuzione di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="18c3a-164">Use the Azure portal to configure Automated Backup when you create a new SQL Server 2014 Virtual Machine in the Resource Manager deployment model.</span></span>

<span data-ttu-id="18c3a-165">Nel pannello **Impostazioni di SQL Server** selezionare **Backup automatico**.</span><span class="sxs-lookup"><span data-stu-id="18c3a-165">In the **SQL Server settings** blade, select **Automated backup**.</span></span> <span data-ttu-id="18c3a-166">Nella seguente schermata del Portale di Azure viene mostrato il pannello **Backup automatico di SQL** .</span><span class="sxs-lookup"><span data-stu-id="18c3a-166">The following Azure portal screenshot shows the **SQL Automated Backup** blade.</span></span>

![Configurazione del backup automatico di SQL nel Portale di Azure](./media/virtual-machines-windows-sql-automated-backup/azure-sql-arm-autobackup.png)

<span data-ttu-id="18c3a-168">Per il contesto, vedere l'argomento completo sul [provisioning di una macchina virtuale di SQL Server in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="18c3a-168">For context, see the complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="18c3a-169">VM esistenti</span><span class="sxs-lookup"><span data-stu-id="18c3a-169">Existing VMs</span></span>

<span data-ttu-id="18c3a-170">Per le macchine virtuali SQL Server esistenti, selezionare la macchina virtuale SQL Server.</span><span class="sxs-lookup"><span data-stu-id="18c3a-170">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="18c3a-171">Dopodiché, selezionare la sezione **Configurazione di SQL Server** del pannello **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="18c3a-171">Then select the **SQL Server configuration** section of the **Settings** blade.</span></span>

![Backup automatico di SQL per le VM esistenti](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-existing-vms.png)

<span data-ttu-id="18c3a-173">Nel pannello **Configurazione di SQL Server** fare clic sul pulsante **Modifica** nella sezione dei backup automatici.</span><span class="sxs-lookup"><span data-stu-id="18c3a-173">In the **SQL Server configuration** blade, click the **Edit** button in the Automated backup section.</span></span>

![Configurare il backup automatico di SQL per le VM esistenti](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-configuration.png)

<span data-ttu-id="18c3a-175">Al termine, fare clic sul pulsante **OK** in fondo al pannello **Configurazione di SQL Server** per salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="18c3a-175">When finished, click the **OK** button on the bottom of the **SQL Server configuration** blade to save your changes.</span></span>

<span data-ttu-id="18c3a-176">Se si intende abilitare il backup automatico per la prima volta, Azure configura l'agente IaaS di SQL Server in background.</span><span class="sxs-lookup"><span data-stu-id="18c3a-176">If you are enabling Automated Backup for the first time, Azure configures the SQL Server IaaS Agent in the background.</span></span> <span data-ttu-id="18c3a-177">Durante questo periodo, nel portale di Azure potrebbe non essere visualizzata l'informazione relativa alla configurazione del backup automatico.</span><span class="sxs-lookup"><span data-stu-id="18c3a-177">During this time, the Azure portal might not show that Automated Backup is configured.</span></span> <span data-ttu-id="18c3a-178">Attendere alcuni minuti per l'installazione e la configurazione dell'agente.</span><span class="sxs-lookup"><span data-stu-id="18c3a-178">Wait several minutes for the agent to be installed, configured.</span></span> <span data-ttu-id="18c3a-179">A questo punto, nel portale di Azure verranno visualizzate le nuove impostazioni.</span><span class="sxs-lookup"><span data-stu-id="18c3a-179">After that the Azure portal will reflect the new settings.</span></span>

> [!NOTE]
> <span data-ttu-id="18c3a-180">È inoltre possibile configurare il backup automatico mediante un modello.</span><span class="sxs-lookup"><span data-stu-id="18c3a-180">You can also configure Automated Backup using a template.</span></span> <span data-ttu-id="18c3a-181">Per altre informazioni, vedere l'articolo relativo al [modello di avvio rapido di Azure per il backup automatico](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autobackup-update).</span><span class="sxs-lookup"><span data-stu-id="18c3a-181">For more information, see [Azure quickstart template for Automated Backup](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autobackup-update).</span></span>

## <a name="configuration-with-powershell"></a><span data-ttu-id="18c3a-182">Configurazione con PowerShell</span><span class="sxs-lookup"><span data-stu-id="18c3a-182">Configuration with PowerShell</span></span>

<span data-ttu-id="18c3a-183">È possibile usare PowerShell per configurare Backup automatico.</span><span class="sxs-lookup"><span data-stu-id="18c3a-183">You can use PowerShell to configure Automated Backup.</span></span> <span data-ttu-id="18c3a-184">Prima di iniziare, è necessario eseguire queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="18c3a-184">Before you begin, you must:</span></span>

- <span data-ttu-id="18c3a-185">[Scaricare e installare la versione di Azure PowerShell più recente](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="18c3a-185">[Download and install the latest Azure PowerShell](http://aka.ms/webpi-azps).</span></span>
- <span data-ttu-id="18c3a-186">Aprire Windows PowerShell e associarlo al proprio account.</span><span class="sxs-lookup"><span data-stu-id="18c3a-186">Open Windows PowerShell and associate it with your account.</span></span> <span data-ttu-id="18c3a-187">A tale scopo, seguire la procedura descritta nella sezione per la [configurazione della sottoscrizione](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) dell'argomento sul provisioning.</span><span class="sxs-lookup"><span data-stu-id="18c3a-187">You can do this by following the steps in the [Configure your subscription](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) section of the provisioning topic.</span></span>

### <a name="install-the-sql-iaas-extension"></a><span data-ttu-id="18c3a-188">Installare l'estensione di SQL IaaS</span><span class="sxs-lookup"><span data-stu-id="18c3a-188">Install the SQL IaaS Extension</span></span>
<span data-ttu-id="18c3a-189">Se è stato eseguito il provisioning di una macchina virtuale di SQL Server dal portale di Azure, l'estensione di SQL Server IaaS dovrebbe già essere installata.</span><span class="sxs-lookup"><span data-stu-id="18c3a-189">If you provisioned a SQL Server virtual machine from the Azure portal, the SQL Server IaaS Extension should already be installed.</span></span> <span data-ttu-id="18c3a-190">È possibile verificarlo eseguendo il comando **Get-AzureRmVM** ed esaminando la proprietà **Extensions**.</span><span class="sxs-lookup"><span data-stu-id="18c3a-190">You can determine if it is installed for your VM by calling **Get-AzureRmVM** command and examining the **Extensions** property.</span></span>

```powershell
$vmname = "vmname"
$resourcegroupname = "resourcegroupname"

(Get-AzureRmVM -Name $vmname -ResourceGroupName $resourcegroupname).Extensions
```

<span data-ttu-id="18c3a-191">Se l'estensione Agente IaaS di SQL Server è installata, verrà visualizzata come "SqlIaaSAgent" o "SQLIaaSExtension".</span><span class="sxs-lookup"><span data-stu-id="18c3a-191">If the SQL Server IaaS Agent extension is installed, you should see it listed as “SqlIaaSAgent” or “SQLIaaSExtension”.</span></span> <span data-ttu-id="18c3a-192">La proprietà **ProvisioningState** per l'estensione deve inoltre mostrare lo stato "Succeeded".</span><span class="sxs-lookup"><span data-stu-id="18c3a-192">**ProvisioningState** for the extension should also show “Succeeded”.</span></span>

<span data-ttu-id="18c3a-193">Nel caso in cui l'estensione non sia installata o non ne sia stato eseguito il provisioning, è possibile installarla con il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="18c3a-193">If it is not installed or failed to be provisioned, you can install it with the following command.</span></span> <span data-ttu-id="18c3a-194">Oltre al nome della macchina virtuale e al gruppo di risorse, è necessario anche specificare l'area (**$region**) in cui si trova la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="18c3a-194">In addition to the VM name and resource group, you must also specify the region (**$region**) that your VM is located in.</span></span>

```powershell
$region = “EASTUS2”
Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region
```

### <span data-ttu-id="18c3a-195"><a id="verifysettings"></a> Verificare le impostazioni correnti</span><span class="sxs-lookup"><span data-stu-id="18c3a-195"><a id="verifysettings"></a> Verify current settings</span></span>

<span data-ttu-id="18c3a-196">Se si è abilitato il backup automatico durante il provisioning, è possibile usare PowerShell per verificare la configurazione corrente.</span><span class="sxs-lookup"><span data-stu-id="18c3a-196">If you enabled automated backup during provisioning, you can use PowerShell to check your current configuration.</span></span> <span data-ttu-id="18c3a-197">Eseguire il comando **Get-AzureRmVMSqlServerExtension** ed esaminare la proprietà **AutoBackupSettings**:</span><span class="sxs-lookup"><span data-stu-id="18c3a-197">Run the **Get-AzureRmVMSqlServerExtension** command and examine the **AutoBackupSettings** property:</span></span>

```powershell
(Get-AzureRmVMSqlServerExtension -VMName $vmname -ResourceGroupName $resourcegroupname).AutoBackupSettings
```

<span data-ttu-id="18c3a-198">L'output dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="18c3a-198">You should get output similar to the following:</span></span>

```
Enable                      : False
EnableEncryption            : False
RetentionPeriod             : -1
StorageUrl                  : NOTSET
StorageAccessKey            : 
Password                    : 
BackupSystemDbs             : False
BackupScheduleType          : 
FullBackupFrequency         : 
FullBackupStartTime         : 
FullBackupWindowHours       : 
LogBackupFrequency          : 
```

<span data-ttu-id="18c3a-199">Se l'output indica che **Enable** è impostato su **False**, è necessario abilitare il backup automatico.</span><span class="sxs-lookup"><span data-stu-id="18c3a-199">If your output shows that **Enable** is set to **False**, then you have to enable automated backup.</span></span> <span data-ttu-id="18c3a-200">I passaggi per farlo sono identici a quelli per abilitare e configurare Backup automatico.</span><span class="sxs-lookup"><span data-stu-id="18c3a-200">The good news is that you enable and configure Automated Backup in the same way.</span></span> <span data-ttu-id="18c3a-201">Per altre informazioni, vedere la sezione seguente.</span><span class="sxs-lookup"><span data-stu-id="18c3a-201">See the next section for this information.</span></span>

> [!NOTE] 
> <span data-ttu-id="18c3a-202">Se si verificano le impostazioni subito dopo una modifica, è possibile che vengano visualizzati i valori precedenti.</span><span class="sxs-lookup"><span data-stu-id="18c3a-202">If you check the settings immediately after making a change, it is possible that you will get back the old configuration values.</span></span> <span data-ttu-id="18c3a-203">Attendere alcuni minuti e verificare nuovamente le impostazioni per assicurarsi che siano state applicate le modifiche.</span><span class="sxs-lookup"><span data-stu-id="18c3a-203">Wait a few minutes and check the settings again to make sure that your changes were applied.</span></span>

### <a name="configure-automated-backup"></a><span data-ttu-id="18c3a-204">Configurare Backup automatico</span><span class="sxs-lookup"><span data-stu-id="18c3a-204">Configure Automated Backup</span></span>
<span data-ttu-id="18c3a-205">È possibile usare PowerShell per abilitare Backup automatico e per modificarne configurazione e comportamento in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="18c3a-205">You can use PowerShell to enable Automated Backup as well as to modify its configuration and behavior at any time.</span></span>

<span data-ttu-id="18c3a-206">In primo luogo, selezionare o creare un account di archiviazione per i file di backup.</span><span class="sxs-lookup"><span data-stu-id="18c3a-206">First, select or create a storage account for the backup files.</span></span> <span data-ttu-id="18c3a-207">Lo script seguente consente di selezionare un account di archiviazione o di crearne uno.</span><span class="sxs-lookup"><span data-stu-id="18c3a-207">The following script selects a storage account or creates it if it does not exist.</span></span>

```powershell
$storage_accountname = “yourstorageaccount”
$storage_resourcegroupname = $resourcegroupname

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region }
```

> [!NOTE]
> <span data-ttu-id="18c3a-208">Backup automatico non supporta l'archiviazione di backup nell'archiviazione Premium, ma può ottenere i backup da dischi di macchine virtuali che usano l'archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="18c3a-208">Automated Backup does not support storing backups in premium storage, but it can take backups from VM disks which use Premium Storage.</span></span>

<span data-ttu-id="18c3a-209">Eseguire quindi il comando **New-AzureVMSqlServerAutoBackupConfig** per abilitare e configurare le impostazioni di Backup automatico per archiviare i backup nell'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="18c3a-209">Then use the **New-AzureRmVMSqlServerAutoBackupConfig** command to enable and configure the Automated Backup settings to store backups in the Azure storage account.</span></span> <span data-ttu-id="18c3a-210">In questo esempio, viene impostata su 10 giorni la conservazione dei backup.</span><span class="sxs-lookup"><span data-stu-id="18c3a-210">In this example, the backups are set to be retained for 10 days.</span></span> <span data-ttu-id="18c3a-211">Il secondo comando, **Set-AzureRmVMSqlServerExtension** aggiorna la macchina virtuale di Azure specificata con queste impostazioni.</span><span class="sxs-lookup"><span data-stu-id="18c3a-211">The second command, **Set-AzureRmVMSqlServerExtension**, updates the specified Azure VM with these settings.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

<span data-ttu-id="18c3a-212">Potrebbero essere necessari diversi minuti per installare e configurare l'agente IaaS di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="18c3a-212">It could take several minutes to install and configure the SQL Server IaaS Agent.</span></span>

> [!NOTE]
> <span data-ttu-id="18c3a-213">Sono presenti altre impostazioni per **New-AzureRmVMSqlServerAutoBackupConfig** che si applicano solo a SQL Server 2016 e Automated Backup v2.</span><span class="sxs-lookup"><span data-stu-id="18c3a-213">There are other settings for **New-AzureRmVMSqlServerAutoBackupConfig** that apply only to SQL Server 2016 and Automated Backup v2.</span></span> <span data-ttu-id="18c3a-214">SQL Server 2014 non supporta le seguenti impostazioni: **BackupSystemDbs**, **BackupScheduleType**, **FullBackupFrequency**, **FullBackupStartHour**, **FullBackupWindowInHours** e **LogBackupFrequencyInMinutes**.</span><span class="sxs-lookup"><span data-stu-id="18c3a-214">SQL Server 2014 does not support the following settings: **BackupSystemDbs**, **BackupScheduleType**, **FullBackupFrequency**, **FullBackupStartHour**, **FullBackupWindowInHours**, and **LogBackupFrequencyInMinutes**.</span></span> <span data-ttu-id="18c3a-215">Se si tenta di configurare queste impostazioni in una macchina virtuale di SQL Server 2014, non si verificano errori ma le impostazioni non vengono applicate.</span><span class="sxs-lookup"><span data-stu-id="18c3a-215">If you attempt to configure these settings on a SQL Server 2014 virtual machine, there is no error, but the settings do not get applied.</span></span> <span data-ttu-id="18c3a-216">Se si desidera usare queste impostazioni in una macchina virtuale di SQL Server 2016, vedere [Backup automatico v2 per macchine virtuali SQL Server 2016 in Azure](virtual-machines-windows-sql-automated-backup-v2.md).</span><span class="sxs-lookup"><span data-stu-id="18c3a-216">If you want to use these settings on a SQL Server 2016 virtual machine, see [Automated Backup v2 for SQL Server 2016 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup-v2.md).</span></span>

<span data-ttu-id="18c3a-217">Per abilitare la crittografia, modificare lo script precedente in modo da passare il parametro **EnableEncryption** e una password (stringa sicura) per il parametro **CertificatePassword**.</span><span class="sxs-lookup"><span data-stu-id="18c3a-217">To enable encryption, modify the previous script to pass the **EnableEncryption** parameter along with a password (secure string) for the **CertificatePassword** parameter.</span></span> <span data-ttu-id="18c3a-218">Il seguente script abilita le impostazioni del backup automatico nell'esempio precedente e aggiunge la crittografia.</span><span class="sxs-lookup"><span data-stu-id="18c3a-218">The following script enables the Automated Backup settings in the previous example and adds encryption.</span></span>

```powershell
$password = "P@ssw0rd"
$encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -EnableEncryption -CertificatePassword $encryptionpassword `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

<span data-ttu-id="18c3a-219">Per confermare l'applicazione delle impostazioni, [verificare la configurazione di Backup automatico](#verifysettings).</span><span class="sxs-lookup"><span data-stu-id="18c3a-219">To confirm your settings are applied, [verify the Automated Backup configuration](#verifysettings).</span></span>

### <a name="disable-automated-backup"></a><span data-ttu-id="18c3a-220">Disabilitare Backup automatico</span><span class="sxs-lookup"><span data-stu-id="18c3a-220">Disable Automated Backup</span></span>

<span data-ttu-id="18c3a-221">Per disabilitare Backup automatico, eseguire lo stesso script senza il parametro **-Enable** per il comando **New-AzureRmVMSqlServerAutoBackupConfig**.</span><span class="sxs-lookup"><span data-stu-id="18c3a-221">To disable Automated Backup, run the same script without the **-Enable** parameter to the **New-AzureRmVMSqlServerAutoBackupConfig** command.</span></span> <span data-ttu-id="18c3a-222">L'assenza del parametro **-Enable** segnala il comando per disabilitare la funzionalità.</span><span class="sxs-lookup"><span data-stu-id="18c3a-222">The absence of the **-Enable** parameter signals the command to disable the feature.</span></span> <span data-ttu-id="18c3a-223">Come per l'installazione, la disabilitazione del backup automatico può richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="18c3a-223">As with installation, it can take several minutes to disable Automated Backup.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

### <a name="example-script"></a><span data-ttu-id="18c3a-224">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="18c3a-224">Example script</span></span>

<span data-ttu-id="18c3a-225">Lo script seguente fornisce un set di variabili da personalizzare per abilitare e configurare Backup automatico per la propria macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="18c3a-225">The following script provides a set of variables that you can customize to enable and configure Automated Backup for your VM.</span></span> <span data-ttu-id="18c3a-226">In questo caso, potrebbe essere necessario personalizzare lo script in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="18c3a-226">In your case, you might need to customize the script based on your requirements.</span></span> <span data-ttu-id="18c3a-227">Ad esempio, potrebbe essere necessario apportare modifiche se si desidera disabilitare il backup dei database di sistema o abilitare la crittografia.</span><span class="sxs-lookup"><span data-stu-id="18c3a-227">For example, you would have to make changes if you wanted to disable the backup of system databases or enable encryption.</span></span>

```powershell
$vmname = "yourvmname"
$resourcegroupname = "vmresourcegroupname"
$region = “Azure region name such as EASTUS2”
$storage_accountname = “storageaccountname”
$storage_resourcegroupname = $resourcegroupname
$retentionperiod = 10

# ResourceGroupName is the resource group which is hosting the VM where you are deploying the SQL IaaS Extension

Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region

# Creates/use a storage account to store the backups

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region }

# Configure Automated Backup settings

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays $retentionperiod -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

# Apply the Automated Backup settings to the VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="18c3a-228">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="18c3a-228">Next steps</span></span>

<span data-ttu-id="18c3a-229">Backup automatico configura backup gestito in Macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="18c3a-229">Automated Backup configures Managed Backup on Azure VMs.</span></span> <span data-ttu-id="18c3a-230">Pertanto è importante [esaminare la documentazione per il backup gestito](https://msdn.microsoft.com/library/dn449496.aspx) per comprendere il comportamento e le implicazioni.</span><span class="sxs-lookup"><span data-stu-id="18c3a-230">So it is important to [review the documentation for Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) to understand the behavior and implications.</span></span>

<span data-ttu-id="18c3a-231">È possibile trovare ulteriori indicazioni sul backup e sul ripristino per SQL Server in macchine virtuali di Azure nell'argomento seguente: [Backup e ripristino per SQL Server in Macchine virtuali di Azure](virtual-machines-windows-sql-backup-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="18c3a-231">You can find additional backup and restore guidance for SQL Server on Azure VMs in the following topic: [Backup and Restore for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).</span></span>

<span data-ttu-id="18c3a-232">Per informazioni sulle altre attività di automazione disponibili, vedere [Estensione Agente IaaS di SQL Server](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="18c3a-232">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

<span data-ttu-id="18c3a-233">Per altre informazioni sull'esecuzione di SQL Server nelle VM di Azure, vedere [Panoramica di SQL Server nelle macchine virtuali di Azure](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="18c3a-233">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

