---
title: aaaAutomated Backup per SQL Server 2014 macchine virtuali di Azure | Documenti Microsoft
description: "Vengono illustrate funzionalità Backup automatizzato hello per VM di SQL Server 2014 in esecuzione in Azure. Questo articolo è specifico tooVMs utilizzando hello Gestione risorse."
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
ms.openlocfilehash: c6803d8ef9f80e44a2f87918d87e099f1b562483
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-for-sql-server-2014-virtual-machines-resource-manager"></a><span data-ttu-id="47f91-104">Backup automatico per macchine virtuali SQL Server 2014 (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="47f91-104">Automated Backup for SQL Server 2014 Virtual Machines (Resource Manager)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="47f91-105">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="47f91-105">SQL Server 2014</span></span>](virtual-machines-windows-sql-automated-backup.md)
> * [<span data-ttu-id="47f91-106">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="47f91-106">SQL Server 2016</span></span>](virtual-machines-windows-sql-automated-backup-v2.md)

<span data-ttu-id="47f91-107">Backup automatizzato configura automaticamente [tooMicrosoft Backup gestito Azure](https://msdn.microsoft.com/library/dn449496.aspx) per tutti i database nuovi ed esistenti in una macchina virtuale di Azure che esegue SQL Server 2014 Standard o Enterprise.</span><span class="sxs-lookup"><span data-stu-id="47f91-107">Automated Backup automatically configures [Managed Backup tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) for all existing and new databases on an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> <span data-ttu-id="47f91-108">In questo modo tooconfigure normali backup di database che utilizzano l'archiviazione blob di Azure durevole.</span><span class="sxs-lookup"><span data-stu-id="47f91-108">This enables you tooconfigure regular database backups that utilize durable Azure blob storage.</span></span> <span data-ttu-id="47f91-109">Backup automatizzato dipende hello [estensione di SQL Server IaaS Agent](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="47f91-109">Automated Backup depends on hello [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="47f91-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="47f91-110">Prerequisites</span></span>
<span data-ttu-id="47f91-111">toouse Backup automatizzato, prendere in considerazione hello seguenti prerequisiti:</span><span class="sxs-lookup"><span data-stu-id="47f91-111">toouse Automated Backup, consider hello following prerequisites:</span></span>

<span data-ttu-id="47f91-112">**Sistema operativo**:</span><span class="sxs-lookup"><span data-stu-id="47f91-112">**Operating System**:</span></span>

- <span data-ttu-id="47f91-113">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="47f91-113">Windows Server 2012</span></span>
- <span data-ttu-id="47f91-114">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="47f91-114">Windows Server 2012 R2</span></span>
- <span data-ttu-id="47f91-115">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="47f91-115">Windows Server 2016</span></span>

<span data-ttu-id="47f91-116">**Versione/edizione di SQL Server**:</span><span class="sxs-lookup"><span data-stu-id="47f91-116">**SQL Server version/edition**:</span></span>

- <span data-ttu-id="47f91-117">SQL Server 2014 Standard</span><span class="sxs-lookup"><span data-stu-id="47f91-117">SQL Server 2014 Standard</span></span>
- <span data-ttu-id="47f91-118">SQL Server 2014 Enterprise</span><span class="sxs-lookup"><span data-stu-id="47f91-118">SQL Server 2014 Enterprise</span></span>

> [!IMPORTANT]
> <span data-ttu-id="47f91-119">Il backup automatico funziona con SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="47f91-119">Automated Backup works with SQL Server 2014.</span></span> <span data-ttu-id="47f91-120">Se si utilizza SQL Server 2016, è possibile utilizzare Backup automatizzato v2 tooback backup dei database.</span><span class="sxs-lookup"><span data-stu-id="47f91-120">If you are using SQL Server 2016, you can use Automated Backup v2 tooback up your databases.</span></span> <span data-ttu-id="47f91-121">Per altre informazioni, vedere [Automated Backup v2 for SQL Server 2016 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup-v2.md) (Backup automatico versione 2 per macchine virtuali SQL Server 2016 in Azure).</span><span class="sxs-lookup"><span data-stu-id="47f91-121">For more information, see [Automated Backup v2 for SQL Server 2016 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup-v2.md).</span></span>

<span data-ttu-id="47f91-122">**Configurazione del database**:</span><span class="sxs-lookup"><span data-stu-id="47f91-122">**Database configuration**:</span></span>

- <span data-ttu-id="47f91-123">Database di destinazione devono utilizzare il modello di recupero con registrazione completa hello.</span><span class="sxs-lookup"><span data-stu-id="47f91-123">Target databases must use hello full recovery model.</span></span> <span data-ttu-id="47f91-124">Per ulteriori informazioni sull'impatto hello del modello di recupero con registrazione completa hello sui backup, vedere [hello Backup nel modello di recupero completo](https://technet.microsoft.com/library/ms190217.aspx).</span><span class="sxs-lookup"><span data-stu-id="47f91-124">For more information about hello impact of hello full recovery model on backups, see [Backup Under hello Full Recovery Model](https://technet.microsoft.com/library/ms190217.aspx).</span></span>
- <span data-ttu-id="47f91-125">Database di destinazione devono essere nell'istanza di SQL Server predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="47f91-125">Target databases must be on hello default SQL Server instance.</span></span> <span data-ttu-id="47f91-126">Hello estensione IaaS di SQL Server non supporta le istanze denominate.</span><span class="sxs-lookup"><span data-stu-id="47f91-126">hello SQL Server IaaS Extension does not support named instances.</span></span>

<span data-ttu-id="47f91-127">**Modello di distribuzione di Azure**:</span><span class="sxs-lookup"><span data-stu-id="47f91-127">**Azure deployment model**:</span></span>

- <span data-ttu-id="47f91-128">Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="47f91-128">Resource Manager</span></span>

<span data-ttu-id="47f91-129">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="47f91-129">**Azure PowerShell**:</span></span>

- <span data-ttu-id="47f91-130">[Installare i comandi di PowerShell di Azure più recenti hello](/powershell/azure/overview) se si prevede di tooconfigure Backup automatizzato con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="47f91-130">[Install hello latest Azure PowerShell commands](/powershell/azure/overview) if you plan tooconfigure Automated Backup with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="47f91-131">Backup automatizzato si basa su hello estensione agente IaaS di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="47f91-131">Automated Backup relies on hello SQL Server IaaS Agent Extension.</span></span> <span data-ttu-id="47f91-132">Per impostazione predefinita, le attuali immagini della raccolta di macchine virtuali di SQL aggiungono questa estensione.</span><span class="sxs-lookup"><span data-stu-id="47f91-132">Current SQL virtual machine gallery images add this extension by default.</span></span> <span data-ttu-id="47f91-133">Per altre informazioni, vedere [Estensione Agente IaaS di SQL Server](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="47f91-133">For more information, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="47f91-134">Impostazioni</span><span class="sxs-lookup"><span data-stu-id="47f91-134">Settings</span></span>

<span data-ttu-id="47f91-135">Hello nella tabella seguente vengono descritte hello opzioni che possono essere configurate per il Backup automatizzato.</span><span class="sxs-lookup"><span data-stu-id="47f91-135">hello following table describes hello options that can be configured for Automated Backup.</span></span> <span data-ttu-id="47f91-136">passaggi di configurazione effettivi Hello variano a seconda che si utilizzi hello portale di Azure o i comandi di Windows PowerShell per Azure.</span><span class="sxs-lookup"><span data-stu-id="47f91-136">hello actual configuration steps vary depending on whether you use hello Azure portal or Azure Windows PowerShell commands.</span></span>

| <span data-ttu-id="47f91-137">Impostazione</span><span class="sxs-lookup"><span data-stu-id="47f91-137">Setting</span></span> | <span data-ttu-id="47f91-138">Intervallo (impostazione predefinita)</span><span class="sxs-lookup"><span data-stu-id="47f91-138">Range (Default)</span></span> | <span data-ttu-id="47f91-139">Descrizione</span><span class="sxs-lookup"><span data-stu-id="47f91-139">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="47f91-140">**Backup automatico**</span><span class="sxs-lookup"><span data-stu-id="47f91-140">**Automated Backup**</span></span> | <span data-ttu-id="47f91-141">Enable/Disable (disabilitato)</span><span class="sxs-lookup"><span data-stu-id="47f91-141">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="47f91-142">Abilita o disabilita il backup automatico per una macchina virtuale di Azure in cui viene eseguito SQL Server 2014 Standard o Enterprise.</span><span class="sxs-lookup"><span data-stu-id="47f91-142">Enables or disables Automated Backup for an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> |
| <span data-ttu-id="47f91-143">**Periodo di conservazione**</span><span class="sxs-lookup"><span data-stu-id="47f91-143">**Retention Period**</span></span> | <span data-ttu-id="47f91-144">1-30 giorni (30 giorni)</span><span class="sxs-lookup"><span data-stu-id="47f91-144">1-30 days (30 days)</span></span> | <span data-ttu-id="47f91-145">numero di Hello di giorni tooretain una copia di backup.</span><span class="sxs-lookup"><span data-stu-id="47f91-145">hello number of days tooretain a backup.</span></span> |
| <span data-ttu-id="47f91-146">**Storage Account**</span><span class="sxs-lookup"><span data-stu-id="47f91-146">**Storage Account**</span></span> | <span data-ttu-id="47f91-147">Account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="47f91-147">Azure storage account</span></span> | <span data-ttu-id="47f91-148">Toouse un account di archiviazione di Azure per archiviare i file di Backup automatizzato nell'archiviazione blob.</span><span class="sxs-lookup"><span data-stu-id="47f91-148">An Azure storage account toouse for storing Automated Backup files in blob storage.</span></span> <span data-ttu-id="47f91-149">Un contenitore viene creato in questo percorso toostore tutti i file di backup.</span><span class="sxs-lookup"><span data-stu-id="47f91-149">A container is created at this location toostore all backup files.</span></span> <span data-ttu-id="47f91-150">file di backup Hello convenzione di denominazione include hello data, ora e nome del computer.</span><span class="sxs-lookup"><span data-stu-id="47f91-150">hello backup file naming convention includes hello date, time, and machine name.</span></span> |
| <span data-ttu-id="47f91-151">**Crittografia**</span><span class="sxs-lookup"><span data-stu-id="47f91-151">**Encryption**</span></span> | <span data-ttu-id="47f91-152">Enable/Disable (disabilitato)</span><span class="sxs-lookup"><span data-stu-id="47f91-152">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="47f91-153">Abilita o disabilita la crittografia.</span><span class="sxs-lookup"><span data-stu-id="47f91-153">Enables or disables encryption.</span></span> <span data-ttu-id="47f91-154">Quando la crittografia è abilitata, hello i certificati utilizzati toorestore hello backup si trovano in hello specificato dell'account di archiviazione in hello stesso `automaticbackup` contenitore usando hello stessa convenzione di denominazione.</span><span class="sxs-lookup"><span data-stu-id="47f91-154">When encryption is enabled, hello certificates used toorestore hello backup are located in hello specified storage account in hello same `automaticbackup` container using hello same naming convention.</span></span> <span data-ttu-id="47f91-155">Se la modifica di password hello, viene generato un nuovo certificato con la password, ma vecchio certificato hello rimane toorestore eventuale backup precedente.</span><span class="sxs-lookup"><span data-stu-id="47f91-155">If hello password changes, a new certificate is generated with that password, but hello old certificate remains toorestore prior backups.</span></span> |
| <span data-ttu-id="47f91-156">**Password**</span><span class="sxs-lookup"><span data-stu-id="47f91-156">**Password**</span></span> | <span data-ttu-id="47f91-157">Testo della password</span><span class="sxs-lookup"><span data-stu-id="47f91-157">Password text</span></span> | <span data-ttu-id="47f91-158">Password per le chiavi di crittografia.</span><span class="sxs-lookup"><span data-stu-id="47f91-158">A password for encryption keys.</span></span> <span data-ttu-id="47f91-159">Questa impostazione è necessaria solo se la crittografia è abilitata.</span><span class="sxs-lookup"><span data-stu-id="47f91-159">This is only required if encryption is enabled.</span></span> <span data-ttu-id="47f91-160">In ordine toorestore un backup crittografato, è necessario disporre la password corretta hello e del certificato correlato che è stato utilizzato in fase di hello hello del backup.</span><span class="sxs-lookup"><span data-stu-id="47f91-160">In order toorestore an encrypted backup, you must have hello correct password and related certificate that was used at hello time hello backup was taken.</span></span> |

## <a name="configuration-in-hello-portal"></a><span data-ttu-id="47f91-161">Configurazione di hello portale</span><span class="sxs-lookup"><span data-stu-id="47f91-161">Configuration in hello Portal</span></span>

<span data-ttu-id="47f91-162">È possibile utilizzare hello tooconfigure portale Azure Backup automatizzati durante il provisioning o per le macchine virtuali di esistente SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="47f91-162">You can use hello Azure portal tooconfigure Automated Backup during provisioning or for existing SQL Server 2014 VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="47f91-163">Nuove VM</span><span class="sxs-lookup"><span data-stu-id="47f91-163">New VMs</span></span>

<span data-ttu-id="47f91-164">Utilizzare hello tooconfigure portale Azure Backup automatizzato quando si crea una nuova macchina virtuale di SQL Server 2014 nel modello di distribuzione di gestione risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="47f91-164">Use hello Azure portal tooconfigure Automated Backup when you create a new SQL Server 2014 Virtual Machine in hello Resource Manager deployment model.</span></span>

<span data-ttu-id="47f91-165">In hello **impostazioni di SQL Server** pannello seleziona **backup automatizzato**.</span><span class="sxs-lookup"><span data-stu-id="47f91-165">In hello **SQL Server settings** blade, select **Automated backup**.</span></span> <span data-ttu-id="47f91-166">schermata del portale di Azure seguente Hello Mostra hello **Backup automatizzato SQL** blade.</span><span class="sxs-lookup"><span data-stu-id="47f91-166">hello following Azure portal screenshot shows hello **SQL Automated Backup** blade.</span></span>

![Configurazione del backup automatico di SQL nel Portale di Azure](./media/virtual-machines-windows-sql-automated-backup/azure-sql-arm-autobackup.png)

<span data-ttu-id="47f91-168">Per contesto, vedere l'argomento completo hello in [provisioning di una macchina virtuale di SQL Server in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="47f91-168">For context, see hello complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="47f91-169">VM esistenti</span><span class="sxs-lookup"><span data-stu-id="47f91-169">Existing VMs</span></span>

<span data-ttu-id="47f91-170">Per le macchine virtuali SQL Server esistenti, selezionare la macchina virtuale SQL Server.</span><span class="sxs-lookup"><span data-stu-id="47f91-170">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="47f91-171">Selezionare quindi hello **configurazione di SQL Server** sezione di hello **impostazioni** blade.</span><span class="sxs-lookup"><span data-stu-id="47f91-171">Then select hello **SQL Server configuration** section of hello **Settings** blade.</span></span>

![Backup automatico di SQL per le VM esistenti](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-existing-vms.png)

<span data-ttu-id="47f91-173">In hello **configurazione di SQL Server** pannello, fare clic su hello **modifica** pulsante hello automatizzata sezione backup.</span><span class="sxs-lookup"><span data-stu-id="47f91-173">In hello **SQL Server configuration** blade, click hello **Edit** button in hello Automated backup section.</span></span>

![Configurare il backup automatico di SQL per le VM esistenti](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-configuration.png)

<span data-ttu-id="47f91-175">Al termine, fare clic su hello **OK** pulsante nella parte inferiore di hello di hello **configurazione di SQL Server** pannello toosave le modifiche.</span><span class="sxs-lookup"><span data-stu-id="47f91-175">When finished, click hello **OK** button on hello bottom of hello **SQL Server configuration** blade toosave your changes.</span></span>

<span data-ttu-id="47f91-176">Se si sta abilitando Backup automatizzato per hello prima volta, Azure Configura hello agente IaaS di SQL Server in background hello.</span><span class="sxs-lookup"><span data-stu-id="47f91-176">If you are enabling Automated Backup for hello first time, Azure configures hello SQL Server IaaS Agent in hello background.</span></span> <span data-ttu-id="47f91-177">Durante questo periodo, hello portale di Azure potrebbe non visualizzare che Backup automatizzato è configurato.</span><span class="sxs-lookup"><span data-stu-id="47f91-177">During this time, hello Azure portal might not show that Automated Backup is configured.</span></span> <span data-ttu-id="47f91-178">Attendere alcuni minuti per hello agente toobe installato, configurato.</span><span class="sxs-lookup"><span data-stu-id="47f91-178">Wait several minutes for hello agent toobe installed, configured.</span></span> <span data-ttu-id="47f91-179">Dopo tale hello Azure portale rispecchierà le nuove impostazioni hello.</span><span class="sxs-lookup"><span data-stu-id="47f91-179">After that hello Azure portal will reflect hello new settings.</span></span>

> [!NOTE]
> <span data-ttu-id="47f91-180">È inoltre possibile configurare il backup automatico mediante un modello.</span><span class="sxs-lookup"><span data-stu-id="47f91-180">You can also configure Automated Backup using a template.</span></span> <span data-ttu-id="47f91-181">Per altre informazioni, vedere l'articolo relativo al [modello di avvio rapido di Azure per il backup automatico](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autobackup-update).</span><span class="sxs-lookup"><span data-stu-id="47f91-181">For more information, see [Azure quickstart template for Automated Backup](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autobackup-update).</span></span>

## <a name="configuration-with-powershell"></a><span data-ttu-id="47f91-182">Configurazione con PowerShell</span><span class="sxs-lookup"><span data-stu-id="47f91-182">Configuration with PowerShell</span></span>

<span data-ttu-id="47f91-183">È possibile utilizzare PowerShell tooconfigure Backup automatizzato.</span><span class="sxs-lookup"><span data-stu-id="47f91-183">You can use PowerShell tooconfigure Automated Backup.</span></span> <span data-ttu-id="47f91-184">Prima di iniziare, è necessario eseguire queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="47f91-184">Before you begin, you must:</span></span>

- <span data-ttu-id="47f91-185">[Scaricare e installare hello più recente di Azure PowerShell](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="47f91-185">[Download and install hello latest Azure PowerShell](http://aka.ms/webpi-azps).</span></span>
- <span data-ttu-id="47f91-186">Aprire Windows PowerShell e associarlo al proprio account.</span><span class="sxs-lookup"><span data-stu-id="47f91-186">Open Windows PowerShell and associate it with your account.</span></span> <span data-ttu-id="47f91-187">È possibile farlo attenendosi alla seguente procedura hello in hello [configura la sottoscrizione](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) sezione di hello provisioning argomento.</span><span class="sxs-lookup"><span data-stu-id="47f91-187">You can do this by following hello steps in hello [Configure your subscription](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) section of hello provisioning topic.</span></span>

### <a name="install-hello-sql-iaas-extension"></a><span data-ttu-id="47f91-188">Installare hello estensione SQL IaaS</span><span class="sxs-lookup"><span data-stu-id="47f91-188">Install hello SQL IaaS Extension</span></span>
<span data-ttu-id="47f91-189">Se eseguito il provisioning di una macchina virtuale di SQL Server dal portale di Azure hello, hello estensione IaaS di SQL Server deve essere già installato.</span><span class="sxs-lookup"><span data-stu-id="47f91-189">If you provisioned a SQL Server virtual machine from hello Azure portal, hello SQL Server IaaS Extension should already be installed.</span></span> <span data-ttu-id="47f91-190">È possibile determinare se è installato per la macchina virtuale tramite la chiamata **Get AzureRmVM** comando ed esaminando hello **estensioni** proprietà.</span><span class="sxs-lookup"><span data-stu-id="47f91-190">You can determine if it is installed for your VM by calling **Get-AzureRmVM** command and examining hello **Extensions** property.</span></span>

```powershell
$vmname = "vmname"
$resourcegroupname = "resourcegroupname"

(Get-AzureRmVM -Name $vmname -ResourceGroupName $resourcegroupname).Extensions
```

<span data-ttu-id="47f91-191">Se è installato l'estensione di SQL Server IaaS Agent hello, si dovrebbe che è elencato come "SqlIaaSAgent" o "SQLIaaSExtension".</span><span class="sxs-lookup"><span data-stu-id="47f91-191">If hello SQL Server IaaS Agent extension is installed, you should see it listed as “SqlIaaSAgent” or “SQLIaaSExtension”.</span></span> <span data-ttu-id="47f91-192">**ProvisioningState** per estensione hello deve inoltre visualizzare "Succeeded".</span><span class="sxs-lookup"><span data-stu-id="47f91-192">**ProvisioningState** for hello extension should also show “Succeeded”.</span></span>

<span data-ttu-id="47f91-193">Se non è installato o non è stato possibile toobe il provisioning, è possibile installarlo con hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="47f91-193">If it is not installed or failed toobe provisioned, you can install it with hello following command.</span></span> <span data-ttu-id="47f91-194">In aggiunta toohello VM nome e la risorsa gruppo, è necessario specificare anche area hello (**$region**) che la macchina virtuale si trova in.</span><span class="sxs-lookup"><span data-stu-id="47f91-194">In addition toohello VM name and resource group, you must also specify hello region (**$region**) that your VM is located in.</span></span>

```powershell
$region = “EASTUS2”
Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region
```

### <span data-ttu-id="47f91-195"><a id="verifysettings"></a> Verificare le impostazioni correnti</span><span class="sxs-lookup"><span data-stu-id="47f91-195"><a id="verifysettings"></a> Verify current settings</span></span>

<span data-ttu-id="47f91-196">Se è abilitato il backup automatizzato durante il provisioning, è possibile utilizzare PowerShell toocheck la configurazione corrente.</span><span class="sxs-lookup"><span data-stu-id="47f91-196">If you enabled automated backup during provisioning, you can use PowerShell toocheck your current configuration.</span></span> <span data-ttu-id="47f91-197">Eseguire hello **Get AzureRmVMSqlServerExtension** comando ed esaminare hello **AutoBackupSettings** proprietà:</span><span class="sxs-lookup"><span data-stu-id="47f91-197">Run hello **Get-AzureRmVMSqlServerExtension** command and examine hello **AutoBackupSettings** property:</span></span>

```powershell
(Get-AzureRmVMSqlServerExtension -VMName $vmname -ResourceGroupName $resourcegroupname).AutoBackupSettings
```

<span data-ttu-id="47f91-198">È necessario ottenere seguente toohello simili di output:</span><span class="sxs-lookup"><span data-stu-id="47f91-198">You should get output similar toohello following:</span></span>

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

<span data-ttu-id="47f91-199">Se l'output mostra che **abilitare** è troppo**False**, è necessario tooenable backup automatico.</span><span class="sxs-lookup"><span data-stu-id="47f91-199">If your output shows that **Enable** is set too**False**, then you have tooenable automated backup.</span></span> <span data-ttu-id="47f91-200">Hello buone notizie sono attivare e configurare il Backup automatizzato in hello allo stesso modo.</span><span class="sxs-lookup"><span data-stu-id="47f91-200">hello good news is that you enable and configure Automated Backup in hello same way.</span></span> <span data-ttu-id="47f91-201">Vedere hello sezione successiva per ottenere questa informazione.</span><span class="sxs-lookup"><span data-stu-id="47f91-201">See hello next section for this information.</span></span>

> [!NOTE] 
> <span data-ttu-id="47f91-202">Se si seleziona impostazioni hello immediatamente dopo aver apportato una modifica, è possibile che si otterranno nuovamente i valori di configurazione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="47f91-202">If you check hello settings immediately after making a change, it is possible that you will get back hello old configuration values.</span></span> <span data-ttu-id="47f91-203">Attendere alcuni minuti e verificare le impostazioni di hello nuovamente toomake assicurarsi che siano state applicate le modifiche.</span><span class="sxs-lookup"><span data-stu-id="47f91-203">Wait a few minutes and check hello settings again toomake sure that your changes were applied.</span></span>

### <a name="configure-automated-backup"></a><span data-ttu-id="47f91-204">Configurare Backup automatico</span><span class="sxs-lookup"><span data-stu-id="47f91-204">Configure Automated Backup</span></span>
<span data-ttu-id="47f91-205">È possibile utilizzare PowerShell tooenable Backup automatizzato, nonché toomodify la configurazione e il comportamento in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="47f91-205">You can use PowerShell tooenable Automated Backup as well as toomodify its configuration and behavior at any time.</span></span>

<span data-ttu-id="47f91-206">In primo luogo, selezionare o creare un account di archiviazione per hello i file di backup.</span><span class="sxs-lookup"><span data-stu-id="47f91-206">First, select or create a storage account for hello backup files.</span></span> <span data-ttu-id="47f91-207">Hello lo script seguente consente di selezionare un account di archiviazione o la crea se non esiste.</span><span class="sxs-lookup"><span data-stu-id="47f91-207">hello following script selects a storage account or creates it if it does not exist.</span></span>

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
> <span data-ttu-id="47f91-208">Backup automatico non supporta l'archiviazione di backup nell'archiviazione Premium, ma può ottenere i backup da dischi di macchine virtuali che usano l'archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="47f91-208">Automated Backup does not support storing backups in premium storage, but it can take backups from VM disks which use Premium Storage.</span></span>

<span data-ttu-id="47f91-209">Utilizzare quindi hello **New AzureRmVMSqlServerAutoBackupConfig** comando tooenable e configurare i backup toostore le impostazioni di Backup automatizzato hello in hello account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="47f91-209">Then use hello **New-AzureRmVMSqlServerAutoBackupConfig** command tooenable and configure hello Automated Backup settings toostore backups in hello Azure storage account.</span></span> <span data-ttu-id="47f91-210">In questo esempio, i backup di hello sono impostati toobe conservati per 10 giorni.</span><span class="sxs-lookup"><span data-stu-id="47f91-210">In this example, hello backups are set toobe retained for 10 days.</span></span> <span data-ttu-id="47f91-211">Hello secondo comando, **Set AzureRmVMSqlServerExtension**, hello aggiornamenti specificato macchina virtuale di Azure con queste impostazioni.</span><span class="sxs-lookup"><span data-stu-id="47f91-211">hello second command, **Set-AzureRmVMSqlServerExtension**, updates hello specified Azure VM with these settings.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

<span data-ttu-id="47f91-212">Potrebbe richiedere diversi minuti tooinstall e configurare hello agente IaaS di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="47f91-212">It could take several minutes tooinstall and configure hello SQL Server IaaS Agent.</span></span>

> [!NOTE]
> <span data-ttu-id="47f91-213">Sono presenti altre impostazioni per **New AzureRmVMSqlServerAutoBackupConfig** che si applicano solo tooSQL Server 2016 e Backup automatizzato v2.</span><span class="sxs-lookup"><span data-stu-id="47f91-213">There are other settings for **New-AzureRmVMSqlServerAutoBackupConfig** that apply only tooSQL Server 2016 and Automated Backup v2.</span></span> <span data-ttu-id="47f91-214">SQL Server 2014 non supporta hello seguenti impostazioni: **BackupSystemDbs**, **BackupScheduleType**, **FullBackupFrequency**,  **FullBackupStartHour**, **FullBackupWindowInHours**, e **LogBackupFrequencyInMinutes**.</span><span class="sxs-lookup"><span data-stu-id="47f91-214">SQL Server 2014 does not support hello following settings: **BackupSystemDbs**, **BackupScheduleType**, **FullBackupFrequency**, **FullBackupStartHour**, **FullBackupWindowInHours**, and **LogBackupFrequencyInMinutes**.</span></span> <span data-ttu-id="47f91-215">Se si tentano di tooconfigure queste impostazioni in una macchina virtuale di SQL Server 2014, non si verificano errori, ma non si devono applicare le impostazioni di hello.</span><span class="sxs-lookup"><span data-stu-id="47f91-215">If you attempt tooconfigure these settings on a SQL Server 2014 virtual machine, there is no error, but hello settings do not get applied.</span></span> <span data-ttu-id="47f91-216">Se si desiderano toouse queste impostazioni in una macchina virtuale di SQL Server 2016, vedere [v2 Backup automatizzato per SQL Server 2016 macchine virtuali di Azure](virtual-machines-windows-sql-automated-backup-v2.md).</span><span class="sxs-lookup"><span data-stu-id="47f91-216">If you want toouse these settings on a SQL Server 2016 virtual machine, see [Automated Backup v2 for SQL Server 2016 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup-v2.md).</span></span>

<span data-ttu-id="47f91-217">crittografia tooenable, modificare hello di hello precedente script toopass **EnableEncryption** parametro e una password (stringa sicura) per hello **CertificatePassword** parametro.</span><span class="sxs-lookup"><span data-stu-id="47f91-217">tooenable encryption, modify hello previous script toopass hello **EnableEncryption** parameter along with a password (secure string) for hello **CertificatePassword** parameter.</span></span> <span data-ttu-id="47f91-218">Hello seguente script abilita le impostazioni di Backup automatizzato hello nell'esempio precedente hello e aggiunge la crittografia.</span><span class="sxs-lookup"><span data-stu-id="47f91-218">hello following script enables hello Automated Backup settings in hello previous example and adds encryption.</span></span>

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

<span data-ttu-id="47f91-219">le impostazioni vengono applicate, tooconfirm [verificare la configurazione di Backup automatizzato hello](#verifysettings).</span><span class="sxs-lookup"><span data-stu-id="47f91-219">tooconfirm your settings are applied, [verify hello Automated Backup configuration](#verifysettings).</span></span>

### <a name="disable-automated-backup"></a><span data-ttu-id="47f91-220">Disabilitare Backup automatico</span><span class="sxs-lookup"><span data-stu-id="47f91-220">Disable Automated Backup</span></span>

<span data-ttu-id="47f91-221">Backup automatizzato, esecuzione hello stesso script senza hello toodisable **-abilitare** parametro toohello **New AzureRmVMSqlServerAutoBackupConfig** comando.</span><span class="sxs-lookup"><span data-stu-id="47f91-221">toodisable Automated Backup, run hello same script without hello **-Enable** parameter toohello **New-AzureRmVMSqlServerAutoBackupConfig** command.</span></span> <span data-ttu-id="47f91-222">assenza di hello Hello **-abilitare** funzionalità di parametro segnali hello comando toodisable hello.</span><span class="sxs-lookup"><span data-stu-id="47f91-222">hello absence of hello **-Enable** parameter signals hello command toodisable hello feature.</span></span> <span data-ttu-id="47f91-223">Come per l'installazione, può richiedere diversi minuti toodisable Backup automatizzato.</span><span class="sxs-lookup"><span data-stu-id="47f91-223">As with installation, it can take several minutes toodisable Automated Backup.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

### <a name="example-script"></a><span data-ttu-id="47f91-224">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="47f91-224">Example script</span></span>

<span data-ttu-id="47f91-225">Hello script riportato di seguito fornisce un set di variabili che è possibile personalizzare tooenable e configurare il Backup automatizzato per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="47f91-225">hello following script provides a set of variables that you can customize tooenable and configure Automated Backup for your VM.</span></span> <span data-ttu-id="47f91-226">Il caso, potrebbe essere necessario script hello toocustomize in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="47f91-226">In your case, you might need toocustomize hello script based on your requirements.</span></span> <span data-ttu-id="47f91-227">Ad esempio, si sarebbe sono state apportate modifiche toomake, se si desidera utilizzare backup hello toodisable dei database di sistema o abilitare la crittografia.</span><span class="sxs-lookup"><span data-stu-id="47f91-227">For example, you would have toomake changes if you wanted toodisable hello backup of system databases or enable encryption.</span></span>

```powershell
$vmname = "yourvmname"
$resourcegroupname = "vmresourcegroupname"
$region = “Azure region name such as EASTUS2”
$storage_accountname = “storageaccountname”
$storage_resourcegroupname = $resourcegroupname
$retentionperiod = 10

# ResourceGroupName is hello resource group which is hosting hello VM where you are deploying hello SQL IaaS Extension

Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region

# Creates/use a storage account toostore hello backups

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region }

# Configure Automated Backup settings

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays $retentionperiod -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

# Apply hello Automated Backup settings toohello VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="47f91-228">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="47f91-228">Next steps</span></span>

<span data-ttu-id="47f91-229">Backup automatico configura backup gestito in Macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="47f91-229">Automated Backup configures Managed Backup on Azure VMs.</span></span> <span data-ttu-id="47f91-230">È importante troppo[, vedere la documentazione di hello per il Backup gestito](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello comportamento e le implicazioni.</span><span class="sxs-lookup"><span data-stu-id="47f91-230">So it is important too[review hello documentation for Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello behavior and implications.</span></span>

<span data-ttu-id="47f91-231">È possibile trovare ulteriori backup e ripristino istruzioni for SQL Server in macchine virtuali di Azure nel seguente argomento hello: [di Backup e ripristino per SQL Server in macchine virtuali di Azure](virtual-machines-windows-sql-backup-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="47f91-231">You can find additional backup and restore guidance for SQL Server on Azure VMs in hello following topic: [Backup and Restore for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).</span></span>

<span data-ttu-id="47f91-232">Per informazioni sulle altre attività di automazione disponibili, vedere [Estensione Agente IaaS di SQL Server](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="47f91-232">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

<span data-ttu-id="47f91-233">Per altre informazioni sull'esecuzione di SQL Server nelle VM di Azure, vedere [Panoramica di SQL Server nelle macchine virtuali di Azure](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="47f91-233">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

