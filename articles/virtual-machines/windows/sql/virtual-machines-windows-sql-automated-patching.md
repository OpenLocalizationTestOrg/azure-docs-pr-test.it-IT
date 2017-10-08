---
title: aaaAutomated patch per macchine virtuali di SQL Server (gestione delle risorse) | Documenti Microsoft
description: "Vengono illustrate funzionalità di patch automatizzate hello per SQL Server le macchine virtuali in esecuzione in Azure tramite Gestione risorse."
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
ms.openlocfilehash: 8bb8d0fb265e69d7bbf1fa047f5ceef02e7c56fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-resource-manager"></a><span data-ttu-id="11fe4-103">Applicazione automatica delle patch per SQL Server nelle macchine virtuali di Azure (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="11fe4-103">Automated Patching for SQL Server in Azure Virtual Machines (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="11fe4-104">Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="11fe4-104">Resource Manager</span></span>](virtual-machines-windows-sql-automated-patching.md)
> * [<span data-ttu-id="11fe4-105">Classico</span><span class="sxs-lookup"><span data-stu-id="11fe4-105">Classic</span></span>](../classic/sql-automated-patching.md)
> 
> 

<span data-ttu-id="11fe4-106">L'applicazione automatica delle patch stabilisce un periodo di manutenzione per una macchina virtuale di Azure su cui è in esecuzione SQL Server.</span><span class="sxs-lookup"><span data-stu-id="11fe4-106">Automated Patching establishes a maintenance window for an Azure Virtual Machine running SQL Server.</span></span> <span data-ttu-id="11fe4-107">Gli aggiornamenti automatici possono essere installati solo durante questo periodo di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="11fe4-107">Automated Updates can only be installed during this maintenance window.</span></span> <span data-ttu-id="11fe4-108">Per SQL Server, questo rescriction garantisce che gli aggiornamenti del sistema e tutti i riavvii associati in fase di possibili migliore hello per database hello.</span><span class="sxs-lookup"><span data-stu-id="11fe4-108">For SQL Server, this rescriction ensures that system updates and any associated restarts occur at hello best possible time for hello database.</span></span> <span data-ttu-id="11fe4-109">L'applicazione di patch automatizzati dipende hello [estensione di SQL Server IaaS Agent](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="11fe4-109">Automated Patching depends on hello [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="11fe4-110">versione classica di hello tooview di questo articolo, vedere [applicazione automatica di patch per SQL Server in macchine virtuali di Azure classico](../classic/sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="11fe4-110">tooview hello classic version of this article, see [Automated Patching for SQL Server in Azure Virtual Machines Classic](../classic/sql-automated-patching.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="11fe4-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="11fe4-111">Prerequisites</span></span>
<span data-ttu-id="11fe4-112">toouse automatica di patch, prendere in considerazione hello seguenti prerequisiti:</span><span class="sxs-lookup"><span data-stu-id="11fe4-112">toouse Automated Patching, consider hello following prerequisites:</span></span>

<span data-ttu-id="11fe4-113">**Sistema operativo**:</span><span class="sxs-lookup"><span data-stu-id="11fe4-113">**Operating System**:</span></span>

* <span data-ttu-id="11fe4-114">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="11fe4-114">Windows Server 2012</span></span>
* <span data-ttu-id="11fe4-115">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="11fe4-115">Windows Server 2012 R2</span></span>
* <span data-ttu-id="11fe4-116">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="11fe4-116">Windows Server 2016</span></span>

<span data-ttu-id="11fe4-117">**Versione di SQL Server**:</span><span class="sxs-lookup"><span data-stu-id="11fe4-117">**SQL Server version**:</span></span>

* <span data-ttu-id="11fe4-118">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="11fe4-118">SQL Server 2012</span></span>
* <span data-ttu-id="11fe4-119">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="11fe4-119">SQL Server 2014</span></span>
* <span data-ttu-id="11fe4-120">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="11fe4-120">SQL Server 2016</span></span>

<span data-ttu-id="11fe4-121">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="11fe4-121">**Azure PowerShell**:</span></span>

* <span data-ttu-id="11fe4-122">[Installare i comandi di PowerShell di Azure più recenti hello](/powershell/azure/overview) se si prevede di tooconfigure applicazione automatica di patch con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="11fe4-122">[Install hello latest Azure PowerShell commands](/powershell/azure/overview) if you plan tooconfigure Automated Patching with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="11fe4-123">L'applicazione di patch automatizzato si basa su hello estensione agente IaaS di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="11fe4-123">Automated Patching relies on hello SQL Server IaaS Agent Extension.</span></span> <span data-ttu-id="11fe4-124">Per impostazione predefinita, le attuali immagini della raccolta di macchine virtuali di SQL aggiungono questa estensione.</span><span class="sxs-lookup"><span data-stu-id="11fe4-124">Current SQL virtual machine gallery images add this extension by default.</span></span> <span data-ttu-id="11fe4-125">Per altre informazioni, vedere [Estensione Agente IaaS di SQL Server](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="11fe4-125">For more information, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>
> 
> 

## <a name="settings"></a><span data-ttu-id="11fe4-126">Impostazioni</span><span class="sxs-lookup"><span data-stu-id="11fe4-126">Settings</span></span>
<span data-ttu-id="11fe4-127">Hello nella tabella seguente descrive le opzioni di hello che possono essere configurate per l'applicazione automatica di patch.</span><span class="sxs-lookup"><span data-stu-id="11fe4-127">hello following table describes hello options that can be configured for Automated Patching.</span></span> <span data-ttu-id="11fe4-128">passaggi di configurazione effettivi Hello variano a seconda che si utilizzi hello portale di Azure o i comandi di Windows PowerShell per Azure.</span><span class="sxs-lookup"><span data-stu-id="11fe4-128">hello actual configuration steps vary depending on whether you use hello Azure portal or Azure Windows PowerShell commands.</span></span>

| <span data-ttu-id="11fe4-129">Impostazione</span><span class="sxs-lookup"><span data-stu-id="11fe4-129">Setting</span></span> | <span data-ttu-id="11fe4-130">Valori possibili</span><span class="sxs-lookup"><span data-stu-id="11fe4-130">Possible values</span></span> | <span data-ttu-id="11fe4-131">Descrizione</span><span class="sxs-lookup"><span data-stu-id="11fe4-131">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="11fe4-132">**Applicazione automatica delle patch**</span><span class="sxs-lookup"><span data-stu-id="11fe4-132">**Automated Patching**</span></span> |<span data-ttu-id="11fe4-133">Enable/Disable (disabilitato)</span><span class="sxs-lookup"><span data-stu-id="11fe4-133">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="11fe4-134">Abilita o disabilita l'applicazione automatica delle patch per una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="11fe4-134">Enables or disables Automated Patching for an Azure virtual machine.</span></span> |
| <span data-ttu-id="11fe4-135">**Pianificazione della manutenzione**</span><span class="sxs-lookup"><span data-stu-id="11fe4-135">**Maintenance schedule**</span></span> |<span data-ttu-id="11fe4-136">Ogni giorno, lunedì, martedì, mercoledì, giovedì, venerdì, sabato, domenica</span><span class="sxs-lookup"><span data-stu-id="11fe4-136">Everyday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday</span></span> |<span data-ttu-id="11fe4-137">pianificazione di Hello per scaricare e installare gli aggiornamenti di Microsoft Windows e SQL Server per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="11fe4-137">hello schedule for downloading and installing Windows, SQL Server, and Microsoft updates for your virtual machine.</span></span> |
| <span data-ttu-id="11fe4-138">**Ora di inizio manutenzione**</span><span class="sxs-lookup"><span data-stu-id="11fe4-138">**Maintenance start hour**</span></span> |<span data-ttu-id="11fe4-139">0-24</span><span class="sxs-lookup"><span data-stu-id="11fe4-139">0-24</span></span> |<span data-ttu-id="11fe4-140">Hello avvio locale ora tooupdate hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="11fe4-140">hello local start time tooupdate hello virtual machine.</span></span> |
| <span data-ttu-id="11fe4-141">**Durata dell'intervallo di manutenzione**</span><span class="sxs-lookup"><span data-stu-id="11fe4-141">**Maintenance window duration**</span></span> |<span data-ttu-id="11fe4-142">30-180</span><span class="sxs-lookup"><span data-stu-id="11fe4-142">30-180</span></span> |<span data-ttu-id="11fe4-143">numero di Hello di minuti consentiti toocomplete hello download e installazione degli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="11fe4-143">hello number of minutes permitted toocomplete hello download and installation of updates.</span></span> |
| <span data-ttu-id="11fe4-144">**Categoria delle patch**</span><span class="sxs-lookup"><span data-stu-id="11fe4-144">**Patch Category**</span></span> |<span data-ttu-id="11fe4-145">Importante</span><span class="sxs-lookup"><span data-stu-id="11fe4-145">Important</span></span> |<span data-ttu-id="11fe4-146">categoria di Hello di toodownload gli aggiornamenti e installare.</span><span class="sxs-lookup"><span data-stu-id="11fe4-146">hello category of updates toodownload and install.</span></span> |

## <a name="configuration-in-hello-portal"></a><span data-ttu-id="11fe4-147">Configurazione di hello portale</span><span class="sxs-lookup"><span data-stu-id="11fe4-147">Configuration in hello Portal</span></span>
<span data-ttu-id="11fe4-148">È possibile utilizzare hello tooconfigure portale Azure patch automatizzate durante il provisioning o per le macchine virtuali esistenti.</span><span class="sxs-lookup"><span data-stu-id="11fe4-148">You can use hello Azure portal tooconfigure Automated Patching during provisioning or for existing VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="11fe4-149">Nuove VM</span><span class="sxs-lookup"><span data-stu-id="11fe4-149">New VMs</span></span>
<span data-ttu-id="11fe4-150">Hello utilizzare tooconfigure portale Azure quando si crea una nuova macchina virtuale di SQL Server nel modello di distribuzione di gestione risorse di hello patch automatizzate.</span><span class="sxs-lookup"><span data-stu-id="11fe4-150">Use hello Azure portal tooconfigure Automated Patching when you create a new SQL Server Virtual Machine in hello Resource Manager deployment model.</span></span>

<span data-ttu-id="11fe4-151">In hello **impostazioni di SQL Server** pannello seleziona **l'applicazione automatica di patch**.</span><span class="sxs-lookup"><span data-stu-id="11fe4-151">In hello **SQL Server settings** blade, select **Automated patching**.</span></span> <span data-ttu-id="11fe4-152">schermata del portale di Azure seguente Hello Mostra hello **patch automatizzate SQL** blade.</span><span class="sxs-lookup"><span data-stu-id="11fe4-152">hello following Azure portal screenshot shows hello **SQL Automated Patching** blade.</span></span>

![Applicazione automatizzata di patch SQL nel portale di Azure](./media/virtual-machines-windows-sql-automated-patching/azure-sql-arm-patching.png)

<span data-ttu-id="11fe4-154">Per contesto, vedere l'argomento completo hello in [provisioning di una macchina virtuale di SQL Server in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="11fe4-154">For context, see hello complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="11fe4-155">VM esistenti</span><span class="sxs-lookup"><span data-stu-id="11fe4-155">Existing VMs</span></span>
<span data-ttu-id="11fe4-156">Per le macchine virtuali SQL Server esistenti, selezionare la macchina virtuale SQL Server.</span><span class="sxs-lookup"><span data-stu-id="11fe4-156">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="11fe4-157">Selezionare quindi hello **configurazione di SQL Server** sezione di hello **impostazioni** blade.</span><span class="sxs-lookup"><span data-stu-id="11fe4-157">Then select hello **SQL Server configuration** section of hello **Settings** blade.</span></span>

![Applicazione automatizzata di patch SQL per le VM esistenti](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-existing-vms.png)

<span data-ttu-id="11fe4-159">In hello **configurazione di SQL Server** pannello, fare clic su hello **modifica** pulsante hello automatizzata sezione applicazione di patch.</span><span class="sxs-lookup"><span data-stu-id="11fe4-159">In hello **SQL Server configuration** blade, click hello **Edit** button in hello Automated patching section.</span></span>

![Configurare l'applicazione automatizzata di patch SQL per le VM esistenti](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-configuration.png)

<span data-ttu-id="11fe4-161">Al termine, fare clic su hello **OK** pulsante nella parte inferiore di hello di hello **configurazione di SQL Server** pannello toosave le modifiche.</span><span class="sxs-lookup"><span data-stu-id="11fe4-161">When finished, click hello **OK** button on hello bottom of hello **SQL Server configuration** blade toosave your changes.</span></span>

<span data-ttu-id="11fe4-162">Se si sta abilitando patch automatizzate per hello prima volta, Azure Configura hello agente IaaS di SQL Server in background hello.</span><span class="sxs-lookup"><span data-stu-id="11fe4-162">If you are enabling Automated Patching for hello first time, Azure configures hello SQL Server IaaS Agent in hello background.</span></span> <span data-ttu-id="11fe4-163">Durante questo periodo, hello portale di Azure potrebbe non visualizzare che viene configurato l'applicazione automatica di patch.</span><span class="sxs-lookup"><span data-stu-id="11fe4-163">During this time, hello Azure portal might not show that Automated Patching is configured.</span></span> <span data-ttu-id="11fe4-164">Attendere alcuni minuti per hello agente toobe installato, configurato.</span><span class="sxs-lookup"><span data-stu-id="11fe4-164">Wait several minutes for hello agent toobe installed, configured.</span></span> <span data-ttu-id="11fe4-165">Dopo tale hello Azure portal riflettono le nuove impostazioni hello.</span><span class="sxs-lookup"><span data-stu-id="11fe4-165">After that hello Azure portal reflects hello new settings.</span></span>

> [!NOTE]
> <span data-ttu-id="11fe4-166">È inoltre possibile configurare l'applicazione automatica delle patch mediante un modello.</span><span class="sxs-lookup"><span data-stu-id="11fe4-166">You can also configure Automated Patching using a template.</span></span> <span data-ttu-id="11fe4-167">Per altre informazioni, vedere l'articolo relativo al [modello di avvio rapido di Azure per l'applicazione automatica delle patch](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autopatching-update).</span><span class="sxs-lookup"><span data-stu-id="11fe4-167">For more information, see [Azure quickstart template for Automated Patching](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autopatching-update).</span></span>
> 
> 

## <a name="configuration-with-powershell"></a><span data-ttu-id="11fe4-168">Configurazione con PowerShell</span><span class="sxs-lookup"><span data-stu-id="11fe4-168">Configuration with PowerShell</span></span>
<span data-ttu-id="11fe4-169">Dopo il provisioning VM SQL, utilizzare PowerShell tooconfigure applicazione automatica di patch.</span><span class="sxs-lookup"><span data-stu-id="11fe4-169">After provisioning your SQL VM, use PowerShell tooconfigure Automated Patching.</span></span>

<span data-ttu-id="11fe4-170">Nell'esempio seguente di hello, PowerShell è usato tooconfigure applicazione automatica di patch in una VM esistente di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="11fe4-170">In hello following example, PowerShell is used tooconfigure Automated Patching on an existing SQL Server VM.</span></span> <span data-ttu-id="11fe4-171">Hello **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig** comando Configura una nuova finestra di manutenzione per gli aggiornamenti automatici.</span><span class="sxs-lookup"><span data-stu-id="11fe4-171">hello **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig** command configures a new maintenance window for automatic updates.</span></span>

    $vmname = "vmname"
    $resourcegroupname = "resourcegroupname"
    $aps = AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Set-AzureRmVMSqlServerExtension -AutoPatchingSettings $aps -VMName $vmname -ResourceGroupName $resourcegroupname

<span data-ttu-id="11fe4-172">In base a questo esempio, hello nella tabella seguente vengono descritti hello pratiche effetti sulla destinazione hello macchina virtuale di Azure:</span><span class="sxs-lookup"><span data-stu-id="11fe4-172">Based on this example, hello following table describes hello practical effect on hello target Azure VM:</span></span>

| <span data-ttu-id="11fe4-173">.</span><span class="sxs-lookup"><span data-stu-id="11fe4-173">Parameter</span></span> | <span data-ttu-id="11fe4-174">Effetto</span><span class="sxs-lookup"><span data-stu-id="11fe4-174">Effect</span></span> |
| --- | --- |
| <span data-ttu-id="11fe4-175">**DayOfWeek**</span><span class="sxs-lookup"><span data-stu-id="11fe4-175">**DayOfWeek**</span></span> |<span data-ttu-id="11fe4-176">Patch installate ogni giovedì.</span><span class="sxs-lookup"><span data-stu-id="11fe4-176">Patches installed every Thursday.</span></span> |
| <span data-ttu-id="11fe4-177">**MaintenanceWindowStartingHour**</span><span class="sxs-lookup"><span data-stu-id="11fe4-177">**MaintenanceWindowStartingHour**</span></span> |<span data-ttu-id="11fe4-178">Inizio degli aggiornamenti alle ore 11:00.</span><span class="sxs-lookup"><span data-stu-id="11fe4-178">Begin updates at 11:00am.</span></span> |
| <span data-ttu-id="11fe4-179">**MaintenanceWindowsDuration**</span><span class="sxs-lookup"><span data-stu-id="11fe4-179">**MaintenanceWindowsDuration**</span></span> |<span data-ttu-id="11fe4-180">Le patch devono essere installate entro 120 minuti.</span><span class="sxs-lookup"><span data-stu-id="11fe4-180">Patches must be installed within 120 minutes.</span></span> <span data-ttu-id="11fe4-181">In base a ora di inizio hello, devono essere completate entro le 13.00.</span><span class="sxs-lookup"><span data-stu-id="11fe4-181">Based on hello start time, they must complete by 1:00pm.</span></span> |
| <span data-ttu-id="11fe4-182">**PatchCategory**</span><span class="sxs-lookup"><span data-stu-id="11fe4-182">**PatchCategory**</span></span> |<span data-ttu-id="11fe4-183">Hello unica impostazione possibile per questo parametro è **importante**.</span><span class="sxs-lookup"><span data-stu-id="11fe4-183">hello only possible setting for this parameter is **Important**.</span></span> |

<span data-ttu-id="11fe4-184">Potrebbe richiedere diversi minuti tooinstall e configurare hello agente IaaS di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="11fe4-184">It could take several minutes tooinstall and configure hello SQL Server IaaS Agent.</span></span>

<span data-ttu-id="11fe4-185">toodisable patch automatizzate, esecuzione hello stesso script senza hello **-abilitare** parametro toohello **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig**.</span><span class="sxs-lookup"><span data-stu-id="11fe4-185">toodisable Automated Patching, run hello same script without hello **-Enable** parameter toohello **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig**.</span></span> <span data-ttu-id="11fe4-186">assenza di hello Hello **-abilitare** funzionalità di parametro segnali hello comando toodisable hello.</span><span class="sxs-lookup"><span data-stu-id="11fe4-186">hello absence of hello **-Enable** parameter signals hello command toodisable hello feature.</span></span>

## <a name="next-steps"></a><span data-ttu-id="11fe4-187">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="11fe4-187">Next steps</span></span>
<span data-ttu-id="11fe4-188">Per informazioni sulle altre attività di automazione disponibili, vedere [Estensione Agente IaaS di SQL Server](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="11fe4-188">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

<span data-ttu-id="11fe4-189">Per altre informazioni sull'esecuzione di SQL Server nelle VM di Azure, vedere [Panoramica di SQL Server nelle macchine virtuali di Azure](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="11fe4-189">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

