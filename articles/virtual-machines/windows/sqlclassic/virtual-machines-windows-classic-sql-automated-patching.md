---
title: aaaAutomated patch per macchine virtuali di SQL Server (versione classica) | Documenti Microsoft
description: "Vengono illustrate funzionalità di patch automatizzate hello per SQL Server le macchine virtuali in esecuzione in Azure utilizzando la modalità di distribuzione classica hello."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 737b2f65-08b9-4f54-b867-e987730265a8
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 2ef06b95705fc457605d6eb2fbc0afd490321843
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-classic"></a><span data-ttu-id="088dd-103">Applicazione automatica delle patch per SQL Server in macchine virtuali di Azure (distribuzione classica)</span><span class="sxs-lookup"><span data-stu-id="088dd-103">Automated Patching for SQL Server in Azure Virtual Machines (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="088dd-104">Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="088dd-104">Resource Manager</span></span>](../sql/virtual-machines-windows-sql-automated-patching.md)
> * [<span data-ttu-id="088dd-105">Classico</span><span class="sxs-lookup"><span data-stu-id="088dd-105">Classic</span></span>](../classic/sql-automated-patching.md)
> 
> 

<span data-ttu-id="088dd-106">L'applicazione automatica delle patch stabilisce un periodo di manutenzione per una macchina virtuale di Azure su cui è in esecuzione SQL Server.</span><span class="sxs-lookup"><span data-stu-id="088dd-106">Automated Patching establishes a maintenance window for an Azure Virtual Machine running SQL Server.</span></span> <span data-ttu-id="088dd-107">Gli aggiornamenti automatici possono essere installati solo durante questo periodo di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="088dd-107">Automated Updates can only be installed during this maintenance window.</span></span> <span data-ttu-id="088dd-108">Per SQL Server, in questo modo che gli aggiornamenti del sistema e tutti i riavvii associati in fase di possibili migliore hello per database hello.</span><span class="sxs-lookup"><span data-stu-id="088dd-108">For SQL Server, this ensures that system updates and any associated restarts occur at hello best possible time for hello database.</span></span> <span data-ttu-id="088dd-109">L'applicazione di patch automatizzati dipende hello [estensione di SQL Server IaaS Agent](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="088dd-109">Automated Patching depends on hello [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="088dd-110">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="088dd-110">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="088dd-111">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="088dd-111">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="088dd-112">Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="088dd-112">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="088dd-113">tooview hello Gestione risorse di questo articolo, vedere [applicazione automatica di patch per SQL Server in Gestione risorse di macchine virtuali Azure](../sql/virtual-machines-windows-sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="088dd-113">tooview hello Resource Manager version of this article, see [Automated Patching for SQL Server in Azure Virtual Machines Resource Manager](../sql/virtual-machines-windows-sql-automated-patching.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="088dd-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="088dd-114">Prerequisites</span></span>
<span data-ttu-id="088dd-115">toouse automatica di patch, prendere in considerazione hello seguenti prerequisiti:</span><span class="sxs-lookup"><span data-stu-id="088dd-115">toouse Automated Patching, consider hello following prerequisites:</span></span>

<span data-ttu-id="088dd-116">**Sistema operativo**:</span><span class="sxs-lookup"><span data-stu-id="088dd-116">**Operating System**:</span></span>

* <span data-ttu-id="088dd-117">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="088dd-117">Windows Server 2012</span></span>
* <span data-ttu-id="088dd-118">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="088dd-118">Windows Server 2012 R2</span></span>
* <span data-ttu-id="088dd-119">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="088dd-119">Windows Server 2016</span></span>

<span data-ttu-id="088dd-120">**Versione di SQL Server**:</span><span class="sxs-lookup"><span data-stu-id="088dd-120">**SQL Server version**:</span></span>

* <span data-ttu-id="088dd-121">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="088dd-121">SQL Server 2012</span></span>
* <span data-ttu-id="088dd-122">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="088dd-122">SQL Server 2014</span></span>
* <span data-ttu-id="088dd-123">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="088dd-123">SQL Server 2016</span></span>

<span data-ttu-id="088dd-124">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="088dd-124">**Azure PowerShell**:</span></span>

* <span data-ttu-id="088dd-125">[Installare i comandi di PowerShell di Azure più recenti hello](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="088dd-125">[Install hello latest Azure PowerShell commands](/powershell/azure/overview).</span></span>

<span data-ttu-id="088dd-126">**Estensione di SQL Server IaaS**:</span><span class="sxs-lookup"><span data-stu-id="088dd-126">**SQL Server IaaS Extension**:</span></span>

* <span data-ttu-id="088dd-127">[Installare l'estensione di SQL Server IaaS hello](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="088dd-127">[Install hello SQL Server IaaS Extension](../classic/sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="088dd-128">Impostazioni</span><span class="sxs-lookup"><span data-stu-id="088dd-128">Settings</span></span>
<span data-ttu-id="088dd-129">Hello nella tabella seguente descrive le opzioni di hello che possono essere configurate per l'applicazione automatica di patch.</span><span class="sxs-lookup"><span data-stu-id="088dd-129">hello following table describes hello options that can be configured for Automated Patching.</span></span> <span data-ttu-id="088dd-130">Per le macchine virtuali classiche, è necessario utilizzare PowerShell tooconfigure queste impostazioni.</span><span class="sxs-lookup"><span data-stu-id="088dd-130">For classic VMs, you must use PowerShell tooconfigure these settings.</span></span>

| <span data-ttu-id="088dd-131">Impostazione</span><span class="sxs-lookup"><span data-stu-id="088dd-131">Setting</span></span> | <span data-ttu-id="088dd-132">Valori possibili</span><span class="sxs-lookup"><span data-stu-id="088dd-132">Possible values</span></span> | <span data-ttu-id="088dd-133">Descrizione</span><span class="sxs-lookup"><span data-stu-id="088dd-133">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="088dd-134">**Applicazione automatica delle patch**</span><span class="sxs-lookup"><span data-stu-id="088dd-134">**Automated Patching**</span></span> |<span data-ttu-id="088dd-135">Enable/Disable (disabilitato)</span><span class="sxs-lookup"><span data-stu-id="088dd-135">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="088dd-136">Abilita o disabilita l'applicazione automatica delle patch per una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="088dd-136">Enables or disables Automated Patching for an Azure virtual machine.</span></span> |
| <span data-ttu-id="088dd-137">**Pianificazione della manutenzione**</span><span class="sxs-lookup"><span data-stu-id="088dd-137">**Maintenance schedule**</span></span> |<span data-ttu-id="088dd-138">Ogni giorno, lunedì, martedì, mercoledì, giovedì, venerdì, sabato, domenica</span><span class="sxs-lookup"><span data-stu-id="088dd-138">Everyday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday</span></span> |<span data-ttu-id="088dd-139">pianificazione di Hello per scaricare e installare gli aggiornamenti di Microsoft Windows e SQL Server per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="088dd-139">hello schedule for downloading and installing Windows, SQL Server, and Microsoft updates for your virtual machine.</span></span> |
| <span data-ttu-id="088dd-140">**Ora di inizio manutenzione**</span><span class="sxs-lookup"><span data-stu-id="088dd-140">**Maintenance start hour**</span></span> |<span data-ttu-id="088dd-141">0-24</span><span class="sxs-lookup"><span data-stu-id="088dd-141">0-24</span></span> |<span data-ttu-id="088dd-142">Hello avvio locale ora tooupdate hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="088dd-142">hello local start time tooupdate hello virtual machine.</span></span> |
| <span data-ttu-id="088dd-143">**Durata dell'intervallo di manutenzione**</span><span class="sxs-lookup"><span data-stu-id="088dd-143">**Maintenance window duration**</span></span> |<span data-ttu-id="088dd-144">30-180</span><span class="sxs-lookup"><span data-stu-id="088dd-144">30-180</span></span> |<span data-ttu-id="088dd-145">numero di Hello di minuti consentiti toocomplete hello download e installazione degli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="088dd-145">hello number of minutes permitted toocomplete hello download and installation of updates.</span></span> |
| <span data-ttu-id="088dd-146">**Categoria delle patch**</span><span class="sxs-lookup"><span data-stu-id="088dd-146">**Patch Category**</span></span> |<span data-ttu-id="088dd-147">Importante</span><span class="sxs-lookup"><span data-stu-id="088dd-147">Important</span></span> |<span data-ttu-id="088dd-148">categoria di Hello di toodownload gli aggiornamenti e installare.</span><span class="sxs-lookup"><span data-stu-id="088dd-148">hello category of updates toodownload and install.</span></span> |

## <a name="configuration-with-powershell"></a><span data-ttu-id="088dd-149">Configurazione con PowerShell</span><span class="sxs-lookup"><span data-stu-id="088dd-149">Configuration with PowerShell</span></span>
<span data-ttu-id="088dd-150">Nell'esempio seguente di hello, PowerShell è usato tooconfigure applicazione automatica di patch in una VM esistente di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="088dd-150">In hello following example, PowerShell is used tooconfigure Automated Patching on an existing SQL Server VM.</span></span> <span data-ttu-id="088dd-151">Hello **New-AzureVMSqlServerAutoPatchingConfig** comando Configura una nuova finestra di manutenzione per gli aggiornamenti automatici.</span><span class="sxs-lookup"><span data-stu-id="088dd-151">hello **New-AzureVMSqlServerAutoPatchingConfig** command configures a new maintenance window for automatic updates.</span></span>

    $aps = New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoPatchingSettings $aps | Update-AzureVM

<span data-ttu-id="088dd-152">In base a questo esempio, hello nella tabella seguente vengono descritti hello pratiche effetti sulla destinazione hello macchina virtuale di Azure:</span><span class="sxs-lookup"><span data-stu-id="088dd-152">Based on this example, hello following table describes hello practical effect on hello target Azure VM:</span></span>

| <span data-ttu-id="088dd-153">.</span><span class="sxs-lookup"><span data-stu-id="088dd-153">Parameter</span></span> | <span data-ttu-id="088dd-154">Effetto</span><span class="sxs-lookup"><span data-stu-id="088dd-154">Effect</span></span> |
| --- | --- |
| <span data-ttu-id="088dd-155">**DayOfWeek**</span><span class="sxs-lookup"><span data-stu-id="088dd-155">**DayOfWeek**</span></span> |<span data-ttu-id="088dd-156">Patch installate ogni giovedì.</span><span class="sxs-lookup"><span data-stu-id="088dd-156">Patches installed every Thursday.</span></span> |
| <span data-ttu-id="088dd-157">**MaintenanceWindowStartingHour**</span><span class="sxs-lookup"><span data-stu-id="088dd-157">**MaintenanceWindowStartingHour**</span></span> |<span data-ttu-id="088dd-158">Inizio degli aggiornamenti alle ore 11:00.</span><span class="sxs-lookup"><span data-stu-id="088dd-158">Begin updates at 11:00am.</span></span> |
| <span data-ttu-id="088dd-159">**MaintenanceWindowsDuration**</span><span class="sxs-lookup"><span data-stu-id="088dd-159">**MaintenanceWindowsDuration**</span></span> |<span data-ttu-id="088dd-160">Le patch devono essere installate entro 120 minuti.</span><span class="sxs-lookup"><span data-stu-id="088dd-160">Patches must be installed within 120 minutes.</span></span> <span data-ttu-id="088dd-161">In base a ora di inizio hello, devono essere completate entro le 13.00.</span><span class="sxs-lookup"><span data-stu-id="088dd-161">Based on hello start time, they must complete by 1:00pm.</span></span> |
| <span data-ttu-id="088dd-162">**PatchCategory**</span><span class="sxs-lookup"><span data-stu-id="088dd-162">**PatchCategory**</span></span> |<span data-ttu-id="088dd-163">Hello solo possibile impostazione per questo parametro è "Importante".</span><span class="sxs-lookup"><span data-stu-id="088dd-163">hello only possible setting for this parameter is “Important”.</span></span> |

<span data-ttu-id="088dd-164">Potrebbe richiedere diversi minuti tooinstall e configurare hello agente IaaS di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="088dd-164">It could take several minutes tooinstall and configure hello SQL Server IaaS Agent.</span></span>

<span data-ttu-id="088dd-165">toodisable patch automatizzate, esecuzione hello stesso script senza hello - Enable parametro toohello New-AzureVMSqlServerAutoPatchingConfig.</span><span class="sxs-lookup"><span data-stu-id="088dd-165">toodisable Automated Patching, run hello same script without hello -Enable parameter toohello New-AzureVMSqlServerAutoPatchingConfig.</span></span> <span data-ttu-id="088dd-166">Come con l'installazione, può richiedere diversi minuti toodisable applicazione automatica di patch.</span><span class="sxs-lookup"><span data-stu-id="088dd-166">As with installation, it can take several minutes toodisable Automated Patching.</span></span>

## <a name="next-steps"></a><span data-ttu-id="088dd-167">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="088dd-167">Next steps</span></span>
<span data-ttu-id="088dd-168">Per informazioni sulle altre attività di automazione disponibili, vedere [Estensione Agente IaaS di SQL Server](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="088dd-168">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span></span>

<span data-ttu-id="088dd-169">Per altre informazioni sull'esecuzione di SQL Server nelle VM di Azure, vedere [Panoramica di SQL Server nelle macchine virtuali di Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="088dd-169">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

