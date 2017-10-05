---
title: Applicazione automatica delle patch per VM SQL Server (Resource Manager) | Documentazione Microsoft
description: "Viene illustrata la funzionalità di applicazione automatica delle patch per le macchine virtuali di SQL Server in esecuzione in Azure che usano Resource Manager."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: 58232e92-318f-456b-8f0a-2201a541e08d
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 7d501ab45a85010a8dbfd6135d77f18f1743354e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-resource-manager"></a><span data-ttu-id="ed6f8-103">Applicazione automatica delle patch per SQL Server nelle macchine virtuali di Azure (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="ed6f8-103">Automated Patching for SQL Server in Azure Virtual Machines (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ed6f8-104">Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="ed6f8-104">Resource Manager</span></span>](virtual-machines-windows-sql-automated-patching.md)
> * [<span data-ttu-id="ed6f8-105">Classico</span><span class="sxs-lookup"><span data-stu-id="ed6f8-105">Classic</span></span>](../classic/sql-automated-patching.md)
> 
> 

<span data-ttu-id="ed6f8-106">L'applicazione automatica delle patch stabilisce un periodo di manutenzione per una macchina virtuale di Azure su cui è in esecuzione SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ed6f8-106">Automated Patching establishes a maintenance window for an Azure Virtual Machine running SQL Server.</span></span> <span data-ttu-id="ed6f8-107">Gli aggiornamenti automatici possono essere installati solo durante questo periodo di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="ed6f8-107">Automated Updates can only be installed during this maintenance window.</span></span> <span data-ttu-id="ed6f8-108">Per SQL Server, questa restrizione verifica che gli aggiornamenti di sistema e i riavvii associati vengano eseguiti nel momento migliore per il database.</span><span class="sxs-lookup"><span data-stu-id="ed6f8-108">For SQL Server, this rescriction ensures that system updates and any associated restarts occur at the best possible time for the database.</span></span> <span data-ttu-id="ed6f8-109">L'applicazione automatica delle patch dipende dall' [estensione dell'agente IaaS di SQL Server](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="ed6f8-109">Automated Patching depends on the [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="ed6f8-110">Per visualizzare la versione classica di questo articolo, vedere [Applicazione automatica delle patch per SQL Server in Macchine virtuali di Azure (distribuzione classica)](../classic/sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="ed6f8-110">To view the classic version of this article, see [Automated Patching for SQL Server in Azure Virtual Machines Classic](../classic/sql-automated-patching.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ed6f8-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ed6f8-111">Prerequisites</span></span>
<span data-ttu-id="ed6f8-112">Per usare l'applicazione automatica delle patch, tenere in considerazione i seguenti prerequisiti:</span><span class="sxs-lookup"><span data-stu-id="ed6f8-112">To use Automated Patching, consider the following prerequisites:</span></span>

<span data-ttu-id="ed6f8-113">**Sistema operativo**:</span><span class="sxs-lookup"><span data-stu-id="ed6f8-113">**Operating System**:</span></span>

* <span data-ttu-id="ed6f8-114">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="ed6f8-114">Windows Server 2012</span></span>
* <span data-ttu-id="ed6f8-115">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="ed6f8-115">Windows Server 2012 R2</span></span>
* <span data-ttu-id="ed6f8-116">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="ed6f8-116">Windows Server 2016</span></span>

<span data-ttu-id="ed6f8-117">**Versione di SQL Server**:</span><span class="sxs-lookup"><span data-stu-id="ed6f8-117">**SQL Server version**:</span></span>

* <span data-ttu-id="ed6f8-118">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="ed6f8-118">SQL Server 2012</span></span>
* <span data-ttu-id="ed6f8-119">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="ed6f8-119">SQL Server 2014</span></span>
* <span data-ttu-id="ed6f8-120">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="ed6f8-120">SQL Server 2016</span></span>

<span data-ttu-id="ed6f8-121">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="ed6f8-121">**Azure PowerShell**:</span></span>

* <span data-ttu-id="ed6f8-122">[Installare i comandi di Azure PowerShell più recenti](/powershell/azure/overview) se si prevede di configurare l'applicazione automatica delle patch con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ed6f8-122">[Install the latest Azure PowerShell commands](/powershell/azure/overview) if you plan to configure Automated Patching with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="ed6f8-123">L'applicazione automatica delle patch si basa sull'estensione dell'agente IaaS di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ed6f8-123">Automated Patching relies on the SQL Server IaaS Agent Extension.</span></span> <span data-ttu-id="ed6f8-124">Per impostazione predefinita, le attuali immagini della raccolta di macchine virtuali di SQL aggiungono questa estensione.</span><span class="sxs-lookup"><span data-stu-id="ed6f8-124">Current SQL virtual machine gallery images add this extension by default.</span></span> <span data-ttu-id="ed6f8-125">Per altre informazioni, vedere [Estensione Agente IaaS di SQL Server](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="ed6f8-125">For more information, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>
> 
> 

## <a name="settings"></a><span data-ttu-id="ed6f8-126">Impostazioni</span><span class="sxs-lookup"><span data-stu-id="ed6f8-126">Settings</span></span>
<span data-ttu-id="ed6f8-127">Nella seguente tabella sono descritte le opzioni che possono essere configurate per l'applicazione automatica delle patch.</span><span class="sxs-lookup"><span data-stu-id="ed6f8-127">The following table describes the options that can be configured for Automated Patching.</span></span> <span data-ttu-id="ed6f8-128">I passaggi di configurazione effettivi variano a seconda che venga usato il portale di Azure o i comandi di Windows PowerShell di Azure.</span><span class="sxs-lookup"><span data-stu-id="ed6f8-128">The actual configuration steps vary depending on whether you use the Azure portal or Azure Windows PowerShell commands.</span></span>

| <span data-ttu-id="ed6f8-129">Impostazione</span><span class="sxs-lookup"><span data-stu-id="ed6f8-129">Setting</span></span> | <span data-ttu-id="ed6f8-130">Valori possibili</span><span class="sxs-lookup"><span data-stu-id="ed6f8-130">Possible values</span></span> | <span data-ttu-id="ed6f8-131">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ed6f8-131">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed6f8-132">**Applicazione automatica delle patch**</span><span class="sxs-lookup"><span data-stu-id="ed6f8-132">**Automated Patching**</span></span> |<span data-ttu-id="ed6f8-133">Enable/Disable (disabilitato)</span><span class="sxs-lookup"><span data-stu-id="ed6f8-133">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="ed6f8-134">Abilita o disabilita l'applicazione automatica delle patch per una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ed6f8-134">Enables or disables Automated Patching for an Azure virtual machine.</span></span> |
| <span data-ttu-id="ed6f8-135">**Pianificazione della manutenzione**</span><span class="sxs-lookup"><span data-stu-id="ed6f8-135">**Maintenance schedule**</span></span> |<span data-ttu-id="ed6f8-136">Ogni giorno, lunedì, martedì, mercoledì, giovedì, venerdì, sabato, domenica</span><span class="sxs-lookup"><span data-stu-id="ed6f8-136">Everyday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday</span></span> |<span data-ttu-id="ed6f8-137">Pianificazione per il download e l'installazione degli aggiornamenti di Windows, SQL Server e Microsoft per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ed6f8-137">The schedule for downloading and installing Windows, SQL Server, and Microsoft updates for your virtual machine.</span></span> |
| <span data-ttu-id="ed6f8-138">**Ora di inizio manutenzione**</span><span class="sxs-lookup"><span data-stu-id="ed6f8-138">**Maintenance start hour**</span></span> |<span data-ttu-id="ed6f8-139">0-24</span><span class="sxs-lookup"><span data-stu-id="ed6f8-139">0-24</span></span> |<span data-ttu-id="ed6f8-140">Ora di inizio locale per aggiornare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ed6f8-140">The local start time to update the virtual machine.</span></span> |
| <span data-ttu-id="ed6f8-141">**Durata dell'intervallo di manutenzione**</span><span class="sxs-lookup"><span data-stu-id="ed6f8-141">**Maintenance window duration**</span></span> |<span data-ttu-id="ed6f8-142">30-180</span><span class="sxs-lookup"><span data-stu-id="ed6f8-142">30-180</span></span> |<span data-ttu-id="ed6f8-143">Numero di minuti consentito per completare il download e l'installazione degli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="ed6f8-143">The number of minutes permitted to complete the download and installation of updates.</span></span> |
| <span data-ttu-id="ed6f8-144">**Categoria delle patch**</span><span class="sxs-lookup"><span data-stu-id="ed6f8-144">**Patch Category**</span></span> |<span data-ttu-id="ed6f8-145">Importante</span><span class="sxs-lookup"><span data-stu-id="ed6f8-145">Important</span></span> |<span data-ttu-id="ed6f8-146">Categoria degli aggiornamenti da scaricare e installare.</span><span class="sxs-lookup"><span data-stu-id="ed6f8-146">The category of updates to download and install.</span></span> |

## <a name="configuration-in-the-portal"></a><span data-ttu-id="ed6f8-147">Configurazione nel Portale</span><span class="sxs-lookup"><span data-stu-id="ed6f8-147">Configuration in the Portal</span></span>
<span data-ttu-id="ed6f8-148">È possibile usare il portale di Azure per configurare l'applicazione automatica delle patch durante il provisioning o per le VM esistenti.</span><span class="sxs-lookup"><span data-stu-id="ed6f8-148">You can use the Azure portal to configure Automated Patching during provisioning or for existing VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="ed6f8-149">Nuove VM</span><span class="sxs-lookup"><span data-stu-id="ed6f8-149">New VMs</span></span>
<span data-ttu-id="ed6f8-150">Usare il portale di Azure per configurare l'applicazione automatica delle patch quando si crea una nuova macchina virtuale di SQL Server nel modello di distribuzione di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ed6f8-150">Use the Azure portal to configure Automated Patching when you create a new SQL Server Virtual Machine in the Resource Manager deployment model.</span></span>

<span data-ttu-id="ed6f8-151">Nel pannello **Impostazioni di SQL Server** selezionare **Applicazione automatica delle patch**.</span><span class="sxs-lookup"><span data-stu-id="ed6f8-151">In the **SQL Server settings** blade, select **Automated patching**.</span></span> <span data-ttu-id="ed6f8-152">Nella seguente schermata del Portale di Azure viene mostrato il pannello **Applicazione automatica delle patch di SQL** .</span><span class="sxs-lookup"><span data-stu-id="ed6f8-152">The following Azure portal screenshot shows the **SQL Automated Patching** blade.</span></span>

![Applicazione automatizzata di patch SQL nel portale di Azure](./media/virtual-machines-windows-sql-automated-patching/azure-sql-arm-patching.png)

<span data-ttu-id="ed6f8-154">Per il contesto, vedere l'argomento completo sul [provisioning di una macchina virtuale di SQL Server in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="ed6f8-154">For context, see the complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="ed6f8-155">VM esistenti</span><span class="sxs-lookup"><span data-stu-id="ed6f8-155">Existing VMs</span></span>
<span data-ttu-id="ed6f8-156">Per le macchine virtuali SQL Server esistenti, selezionare la macchina virtuale SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ed6f8-156">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="ed6f8-157">Dopodiché, selezionare la sezione **Configurazione di SQL Server** del pannello **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="ed6f8-157">Then select the **SQL Server configuration** section of the **Settings** blade.</span></span>

![Applicazione automatizzata di patch SQL per le VM esistenti](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-existing-vms.png)

<span data-ttu-id="ed6f8-159">Nel pannello **Configurazione di SQL Server** fare clic sul pulsante **Modifica** nella sezione delle patch.</span><span class="sxs-lookup"><span data-stu-id="ed6f8-159">In the **SQL Server configuration** blade, click the **Edit** button in the Automated patching section.</span></span>

![Configurare l'applicazione automatizzata di patch SQL per le VM esistenti](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-configuration.png)

<span data-ttu-id="ed6f8-161">Al termine, fare clic sul pulsante **OK** in fondo al pannello **Configurazione di SQL Server** per salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="ed6f8-161">When finished, click the **OK** button on the bottom of the **SQL Server configuration** blade to save your changes.</span></span>

<span data-ttu-id="ed6f8-162">Se si intende abilitare l'applicazione automatica delle patch per la prima volta, Azure configura l'agente IaaS di SQL Server in background.</span><span class="sxs-lookup"><span data-stu-id="ed6f8-162">If you are enabling Automated Patching for the first time, Azure configures the SQL Server IaaS Agent in the background.</span></span> <span data-ttu-id="ed6f8-163">Durante questo periodo, nel portale di Azure potrebbe non essere visualizzata l'informazione relativa alla configurazione dell'applicazione automatica delle patch.</span><span class="sxs-lookup"><span data-stu-id="ed6f8-163">During this time, the Azure portal might not show that Automated Patching is configured.</span></span> <span data-ttu-id="ed6f8-164">Attendere alcuni minuti per l'installazione e la configurazione dell'agente.</span><span class="sxs-lookup"><span data-stu-id="ed6f8-164">Wait several minutes for the agent to be installed, configured.</span></span> <span data-ttu-id="ed6f8-165">A questo punto, nel portale di Azure vengono visualizzate le nuove impostazioni.</span><span class="sxs-lookup"><span data-stu-id="ed6f8-165">After that the Azure portal reflects the new settings.</span></span>

> [!NOTE]
> <span data-ttu-id="ed6f8-166">È inoltre possibile configurare l'applicazione automatica delle patch mediante un modello.</span><span class="sxs-lookup"><span data-stu-id="ed6f8-166">You can also configure Automated Patching using a template.</span></span> <span data-ttu-id="ed6f8-167">Per altre informazioni, vedere l'articolo relativo al [modello di avvio rapido di Azure per l'applicazione automatica delle patch](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autopatching-update).</span><span class="sxs-lookup"><span data-stu-id="ed6f8-167">For more information, see [Azure quickstart template for Automated Patching](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autopatching-update).</span></span>
> 
> 

## <a name="configuration-with-powershell"></a><span data-ttu-id="ed6f8-168">Configurazione con PowerShell</span><span class="sxs-lookup"><span data-stu-id="ed6f8-168">Configuration with PowerShell</span></span>
<span data-ttu-id="ed6f8-169">Dopo il provisioning della VM di SQL, usare PowerShell per configurare l'applicazione automatica delle patch.</span><span class="sxs-lookup"><span data-stu-id="ed6f8-169">After provisioning your SQL VM, use PowerShell to configure Automated Patching.</span></span>

<span data-ttu-id="ed6f8-170">Nell'esempio seguente, PowerShell viene utilizzato per configurare l'applicazione automatizzata di patch in una macchina virtuale di SQL Server esistente.</span><span class="sxs-lookup"><span data-stu-id="ed6f8-170">In the following example, PowerShell is used to configure Automated Patching on an existing SQL Server VM.</span></span> <span data-ttu-id="ed6f8-171">Il comando **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig** configura un nuovo periodo di manutenzione per gli aggiornamenti automatici.</span><span class="sxs-lookup"><span data-stu-id="ed6f8-171">The **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig** command configures a new maintenance window for automatic updates.</span></span>

    $vmname = "vmname"
    $resourcegroupname = "resourcegroupname"
    $aps = AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Set-AzureRmVMSqlServerExtension -AutoPatchingSettings $aps -VMName $vmname -ResourceGroupName $resourcegroupname

<span data-ttu-id="ed6f8-172">In base a questo esempio, nella tabella seguente vengono descritti gli effetti pratici sulla macchina virtuale di Azure di destinazione:</span><span class="sxs-lookup"><span data-stu-id="ed6f8-172">Based on this example, the following table describes the practical effect on the target Azure VM:</span></span>

| <span data-ttu-id="ed6f8-173">Parametro</span><span class="sxs-lookup"><span data-stu-id="ed6f8-173">Parameter</span></span> | <span data-ttu-id="ed6f8-174">Effetto</span><span class="sxs-lookup"><span data-stu-id="ed6f8-174">Effect</span></span> |
| --- | --- |
| <span data-ttu-id="ed6f8-175">**DayOfWeek**</span><span class="sxs-lookup"><span data-stu-id="ed6f8-175">**DayOfWeek**</span></span> |<span data-ttu-id="ed6f8-176">Patch installate ogni giovedì.</span><span class="sxs-lookup"><span data-stu-id="ed6f8-176">Patches installed every Thursday.</span></span> |
| <span data-ttu-id="ed6f8-177">**MaintenanceWindowStartingHour**</span><span class="sxs-lookup"><span data-stu-id="ed6f8-177">**MaintenanceWindowStartingHour**</span></span> |<span data-ttu-id="ed6f8-178">Inizio degli aggiornamenti alle ore 11:00.</span><span class="sxs-lookup"><span data-stu-id="ed6f8-178">Begin updates at 11:00am.</span></span> |
| <span data-ttu-id="ed6f8-179">**MaintenanceWindowsDuration**</span><span class="sxs-lookup"><span data-stu-id="ed6f8-179">**MaintenanceWindowsDuration**</span></span> |<span data-ttu-id="ed6f8-180">Le patch devono essere installate entro 120 minuti.</span><span class="sxs-lookup"><span data-stu-id="ed6f8-180">Patches must be installed within 120 minutes.</span></span> <span data-ttu-id="ed6f8-181">In base all'ora di inizio, devono essere completate entro le ore 13:00.</span><span class="sxs-lookup"><span data-stu-id="ed6f8-181">Based on the start time, they must complete by 1:00pm.</span></span> |
| <span data-ttu-id="ed6f8-182">**PatchCategory**</span><span class="sxs-lookup"><span data-stu-id="ed6f8-182">**PatchCategory**</span></span> |<span data-ttu-id="ed6f8-183">L'unica impostazione possibile per questo parametro è **Important**.</span><span class="sxs-lookup"><span data-stu-id="ed6f8-183">The only possible setting for this parameter is **Important**.</span></span> |

<span data-ttu-id="ed6f8-184">Potrebbero essere necessari diversi minuti per installare e configurare l'agente IaaS di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ed6f8-184">It could take several minutes to install and configure the SQL Server IaaS Agent.</span></span>

<span data-ttu-id="ed6f8-185">Per disabilitare l'applicazione automatica delle patch, eseguire lo stesso script senza il parametro **-Enable** per **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig**.</span><span class="sxs-lookup"><span data-stu-id="ed6f8-185">To disable Automated Patching, run the same script without the **-Enable** parameter to the **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig**.</span></span> <span data-ttu-id="ed6f8-186">L'assenza del parametro **-Enable** segnala il comando per disabilitare la funzionalità.</span><span class="sxs-lookup"><span data-stu-id="ed6f8-186">The absence of the **-Enable** parameter signals the command to disable the feature.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ed6f8-187">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ed6f8-187">Next steps</span></span>
<span data-ttu-id="ed6f8-188">Per informazioni sulle altre attività di automazione disponibili, vedere [Estensione Agente IaaS di SQL Server](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="ed6f8-188">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

<span data-ttu-id="ed6f8-189">Per altre informazioni sull'esecuzione di SQL Server nelle VM di Azure, vedere [Panoramica di SQL Server nelle macchine virtuali di Azure](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ed6f8-189">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

