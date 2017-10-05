---
title: Applicazione automatica delle patch per macchine virtuali SQL Server (distribuzione classica) | Microsoft Docs
description: "Informazioni sulla funzionalità di applicazione automatica delle patch per macchine virtuali SQL Server in esecuzione in Azure con il modello di distribuzione classica."
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
ms.openlocfilehash: 1959871141f196ba80ffd7b37e62e5ea5b42dba3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-classic"></a><span data-ttu-id="ce8b8-103">Applicazione automatica delle patch per SQL Server in macchine virtuali di Azure (distribuzione classica)</span><span class="sxs-lookup"><span data-stu-id="ce8b8-103">Automated Patching for SQL Server in Azure Virtual Machines (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ce8b8-104">Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="ce8b8-104">Resource Manager</span></span>](../sql/virtual-machines-windows-sql-automated-patching.md)
> * [<span data-ttu-id="ce8b8-105">Classico</span><span class="sxs-lookup"><span data-stu-id="ce8b8-105">Classic</span></span>](../classic/sql-automated-patching.md)
> 
> 

<span data-ttu-id="ce8b8-106">L'applicazione automatica delle patch stabilisce un periodo di manutenzione per una macchina virtuale di Azure su cui è in esecuzione SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ce8b8-106">Automated Patching establishes a maintenance window for an Azure Virtual Machine running SQL Server.</span></span> <span data-ttu-id="ce8b8-107">Gli aggiornamenti automatici possono essere installati solo durante questo periodo di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="ce8b8-107">Automated Updates can only be installed during this maintenance window.</span></span> <span data-ttu-id="ce8b8-108">Per SQL Server, gli aggiornamenti di sistema e i riavvii associati vengono eseguiti nel momento migliore per il database.</span><span class="sxs-lookup"><span data-stu-id="ce8b8-108">For SQL Server, this ensures that system updates and any associated restarts occur at the best possible time for the database.</span></span> <span data-ttu-id="ce8b8-109">L'applicazione automatica delle patch dipende dall' [estensione dell'agente IaaS di SQL Server](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="ce8b8-109">Automated Patching depends on the [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="ce8b8-110">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ce8b8-110">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ce8b8-111">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="ce8b8-111">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="ce8b8-112">Microsoft consiglia di usare il modello di Gestione risorse per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="ce8b8-112">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="ce8b8-113">Per visualizzare la versione Resource Manager di questo articolo, vedere [Applicazione automatica delle patch per SQL Server in macchine virtuali di Azure (Resource Manager)](../sql/virtual-machines-windows-sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="ce8b8-113">To view the Resource Manager version of this article, see [Automated Patching for SQL Server in Azure Virtual Machines Resource Manager](../sql/virtual-machines-windows-sql-automated-patching.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ce8b8-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ce8b8-114">Prerequisites</span></span>
<span data-ttu-id="ce8b8-115">Per usare l'applicazione automatica delle patch, tenere in considerazione i seguenti prerequisiti:</span><span class="sxs-lookup"><span data-stu-id="ce8b8-115">To use Automated Patching, consider the following prerequisites:</span></span>

<span data-ttu-id="ce8b8-116">**Sistema operativo**:</span><span class="sxs-lookup"><span data-stu-id="ce8b8-116">**Operating System**:</span></span>

* <span data-ttu-id="ce8b8-117">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="ce8b8-117">Windows Server 2012</span></span>
* <span data-ttu-id="ce8b8-118">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="ce8b8-118">Windows Server 2012 R2</span></span>
* <span data-ttu-id="ce8b8-119">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="ce8b8-119">Windows Server 2016</span></span>

<span data-ttu-id="ce8b8-120">**Versione di SQL Server**:</span><span class="sxs-lookup"><span data-stu-id="ce8b8-120">**SQL Server version**:</span></span>

* <span data-ttu-id="ce8b8-121">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="ce8b8-121">SQL Server 2012</span></span>
* <span data-ttu-id="ce8b8-122">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="ce8b8-122">SQL Server 2014</span></span>
* <span data-ttu-id="ce8b8-123">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="ce8b8-123">SQL Server 2016</span></span>

<span data-ttu-id="ce8b8-124">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="ce8b8-124">**Azure PowerShell**:</span></span>

* <span data-ttu-id="ce8b8-125">[Installare i comandi di Azure PowerShell più recenti](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ce8b8-125">[Install the latest Azure PowerShell commands](/powershell/azure/overview).</span></span>

<span data-ttu-id="ce8b8-126">**Estensione di SQL Server IaaS**:</span><span class="sxs-lookup"><span data-stu-id="ce8b8-126">**SQL Server IaaS Extension**:</span></span>

* <span data-ttu-id="ce8b8-127">[Installare l'estensione di SQL Server IaaS](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="ce8b8-127">[Install the SQL Server IaaS Extension](../classic/sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="ce8b8-128">Impostazioni</span><span class="sxs-lookup"><span data-stu-id="ce8b8-128">Settings</span></span>
<span data-ttu-id="ce8b8-129">Nella seguente tabella sono descritte le opzioni che possono essere configurate per l'applicazione automatica delle patch.</span><span class="sxs-lookup"><span data-stu-id="ce8b8-129">The following table describes the options that can be configured for Automated Patching.</span></span> <span data-ttu-id="ce8b8-130">Nella macchine virtuali classiche, per configurare queste impostazioni è necessario usare PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ce8b8-130">For classic VMs, you must use PowerShell to configure these settings.</span></span>

| <span data-ttu-id="ce8b8-131">Impostazione</span><span class="sxs-lookup"><span data-stu-id="ce8b8-131">Setting</span></span> | <span data-ttu-id="ce8b8-132">Valori possibili</span><span class="sxs-lookup"><span data-stu-id="ce8b8-132">Possible values</span></span> | <span data-ttu-id="ce8b8-133">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ce8b8-133">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ce8b8-134">**Applicazione automatica delle patch**</span><span class="sxs-lookup"><span data-stu-id="ce8b8-134">**Automated Patching**</span></span> |<span data-ttu-id="ce8b8-135">Enable/Disable (disabilitato)</span><span class="sxs-lookup"><span data-stu-id="ce8b8-135">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="ce8b8-136">Abilita o disabilita l'applicazione automatica delle patch per una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ce8b8-136">Enables or disables Automated Patching for an Azure virtual machine.</span></span> |
| <span data-ttu-id="ce8b8-137">**Pianificazione della manutenzione**</span><span class="sxs-lookup"><span data-stu-id="ce8b8-137">**Maintenance schedule**</span></span> |<span data-ttu-id="ce8b8-138">Ogni giorno, lunedì, martedì, mercoledì, giovedì, venerdì, sabato, domenica</span><span class="sxs-lookup"><span data-stu-id="ce8b8-138">Everyday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday</span></span> |<span data-ttu-id="ce8b8-139">Pianificazione per il download e l'installazione degli aggiornamenti di Windows, SQL Server e Microsoft per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ce8b8-139">The schedule for downloading and installing Windows, SQL Server, and Microsoft updates for your virtual machine.</span></span> |
| <span data-ttu-id="ce8b8-140">**Ora di inizio manutenzione**</span><span class="sxs-lookup"><span data-stu-id="ce8b8-140">**Maintenance start hour**</span></span> |<span data-ttu-id="ce8b8-141">0-24</span><span class="sxs-lookup"><span data-stu-id="ce8b8-141">0-24</span></span> |<span data-ttu-id="ce8b8-142">Ora di inizio locale per aggiornare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ce8b8-142">The local start time to update the virtual machine.</span></span> |
| <span data-ttu-id="ce8b8-143">**Durata dell'intervallo di manutenzione**</span><span class="sxs-lookup"><span data-stu-id="ce8b8-143">**Maintenance window duration**</span></span> |<span data-ttu-id="ce8b8-144">30-180</span><span class="sxs-lookup"><span data-stu-id="ce8b8-144">30-180</span></span> |<span data-ttu-id="ce8b8-145">Numero di minuti consentito per completare il download e l'installazione degli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="ce8b8-145">The number of minutes permitted to complete the download and installation of updates.</span></span> |
| <span data-ttu-id="ce8b8-146">**Categoria delle patch**</span><span class="sxs-lookup"><span data-stu-id="ce8b8-146">**Patch Category**</span></span> |<span data-ttu-id="ce8b8-147">Importante</span><span class="sxs-lookup"><span data-stu-id="ce8b8-147">Important</span></span> |<span data-ttu-id="ce8b8-148">Categoria degli aggiornamenti da scaricare e installare.</span><span class="sxs-lookup"><span data-stu-id="ce8b8-148">The category of updates to download and install.</span></span> |

## <a name="configuration-with-powershell"></a><span data-ttu-id="ce8b8-149">Configurazione con PowerShell</span><span class="sxs-lookup"><span data-stu-id="ce8b8-149">Configuration with PowerShell</span></span>
<span data-ttu-id="ce8b8-150">Nell'esempio seguente, PowerShell viene utilizzato per configurare l'applicazione automatizzata di patch in una macchina virtuale di SQL Server esistente.</span><span class="sxs-lookup"><span data-stu-id="ce8b8-150">In the following example, PowerShell is used to configure Automated Patching on an existing SQL Server VM.</span></span> <span data-ttu-id="ce8b8-151">Il comando **New-AzureVMSqlServerAutoPatchingConfig** configura un nuovo periodo di manutenzione per gli aggiornamenti automatici.</span><span class="sxs-lookup"><span data-stu-id="ce8b8-151">The **New-AzureVMSqlServerAutoPatchingConfig** command configures a new maintenance window for automatic updates.</span></span>

    $aps = New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoPatchingSettings $aps | Update-AzureVM

<span data-ttu-id="ce8b8-152">In base a questo esempio, nella tabella seguente vengono descritti gli effetti pratici sulla macchina virtuale di Azure di destinazione:</span><span class="sxs-lookup"><span data-stu-id="ce8b8-152">Based on this example, the following table describes the practical effect on the target Azure VM:</span></span>

| <span data-ttu-id="ce8b8-153">Parametro</span><span class="sxs-lookup"><span data-stu-id="ce8b8-153">Parameter</span></span> | <span data-ttu-id="ce8b8-154">Effetto</span><span class="sxs-lookup"><span data-stu-id="ce8b8-154">Effect</span></span> |
| --- | --- |
| <span data-ttu-id="ce8b8-155">**DayOfWeek**</span><span class="sxs-lookup"><span data-stu-id="ce8b8-155">**DayOfWeek**</span></span> |<span data-ttu-id="ce8b8-156">Patch installate ogni giovedì.</span><span class="sxs-lookup"><span data-stu-id="ce8b8-156">Patches installed every Thursday.</span></span> |
| <span data-ttu-id="ce8b8-157">**MaintenanceWindowStartingHour**</span><span class="sxs-lookup"><span data-stu-id="ce8b8-157">**MaintenanceWindowStartingHour**</span></span> |<span data-ttu-id="ce8b8-158">Inizio degli aggiornamenti alle ore 11:00.</span><span class="sxs-lookup"><span data-stu-id="ce8b8-158">Begin updates at 11:00am.</span></span> |
| <span data-ttu-id="ce8b8-159">**MaintenanceWindowsDuration**</span><span class="sxs-lookup"><span data-stu-id="ce8b8-159">**MaintenanceWindowsDuration**</span></span> |<span data-ttu-id="ce8b8-160">Le patch devono essere installate entro 120 minuti.</span><span class="sxs-lookup"><span data-stu-id="ce8b8-160">Patches must be installed within 120 minutes.</span></span> <span data-ttu-id="ce8b8-161">In base all'ora di inizio, devono essere completate entro le ore 13:00.</span><span class="sxs-lookup"><span data-stu-id="ce8b8-161">Based on the start time, they must complete by 1:00pm.</span></span> |
| <span data-ttu-id="ce8b8-162">**PatchCategory**</span><span class="sxs-lookup"><span data-stu-id="ce8b8-162">**PatchCategory**</span></span> |<span data-ttu-id="ce8b8-163">L'unica impostazione possibile per questo parametro è "Important".</span><span class="sxs-lookup"><span data-stu-id="ce8b8-163">The only possible setting for this parameter is “Important”.</span></span> |

<span data-ttu-id="ce8b8-164">Potrebbero essere necessari diversi minuti per installare e configurare l'agente IaaS di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ce8b8-164">It could take several minutes to install and configure the SQL Server IaaS Agent.</span></span>

<span data-ttu-id="ce8b8-165">Per disabilitare l’applicazione automatizzata di patch, eseguire lo stesso script senza il parametro -Enable per New-AzureVMSqlServerAutoPatchingConfig.</span><span class="sxs-lookup"><span data-stu-id="ce8b8-165">To disable Automated Patching, run the same script without the -Enable parameter to the New-AzureVMSqlServerAutoPatchingConfig.</span></span> <span data-ttu-id="ce8b8-166">Come per l'installazione, la disabilitazione dell’applicazione automatizzata di patch può richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="ce8b8-166">As with installation, it can take several minutes to disable Automated Patching.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce8b8-167">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ce8b8-167">Next steps</span></span>
<span data-ttu-id="ce8b8-168">Per informazioni sulle altre attività di automazione disponibili, vedere [Estensione Agente IaaS di SQL Server](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="ce8b8-168">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span></span>

<span data-ttu-id="ce8b8-169">Per altre informazioni sull'esecuzione di SQL Server nelle VM di Azure, vedere [Panoramica di SQL Server nelle macchine virtuali di Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ce8b8-169">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

