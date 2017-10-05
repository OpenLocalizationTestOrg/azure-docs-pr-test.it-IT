---
title: "Automatizzare le attività di gestione in macchine virtuali SQL (distribuzione classica) | Microsoft Docs"
description: "Questo argomento descrive come gestire l'estensione di SQL Server Agent, che consente di automatizzare attività di amministrazione di SQL Server specifiche. Queste includono il backup automatizzato, l'applicazione automatica delle patch e l'integrazione di Azure Key Vault. In questo argomento viene usata la modalità di distribuzione classica."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a9bda2e7-cdba-427c-bc30-77cde4376f3a
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 30fa9128cd51a7498449c991b58500ad9acdd3d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="automate-management-tasks-on-azure-virtual-machines-with-the-sql-server-agent-extension-classic"></a><span data-ttu-id="d3ea8-105">Automatizzare le attività di gestione in macchine virtuali SQL con l'estensione SQL Server Agent (distribuzione classica)</span><span class="sxs-lookup"><span data-stu-id="d3ea8-105">Automate management tasks on Azure Virtual Machines with the SQL Server Agent Extension (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d3ea8-106">Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="d3ea8-106">Resource Manager</span></span>](../sql/virtual-machines-windows-sql-server-agent-extension.md)
> * [<span data-ttu-id="d3ea8-107">Classico</span><span class="sxs-lookup"><span data-stu-id="d3ea8-107">Classic</span></span>](../classic/sql-server-agent-extension.md)
> 
>
 
<span data-ttu-id="d3ea8-108">L'Estensione Agente IaaS di SQL Server (SQLIaaSAgent) viene eseguita sulle macchine virtuali di Azure per automatizzare le attività di amministrazione.</span><span class="sxs-lookup"><span data-stu-id="d3ea8-108">The SQL Server IaaS Agent Extension (SQLIaaSAgent) runs on Azure virtual machines to automate administration tasks.</span></span> <span data-ttu-id="d3ea8-109">Questo argomento fornisce una panoramica dei servizi supportati dall'estensione e delle istruzioni per l'installazione, lo stato e la rimozione.</span><span class="sxs-lookup"><span data-stu-id="d3ea8-109">This topic provides an overview of the services supported by the extension as well as instructions for installation, status, and removal.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="d3ea8-110">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="d3ea8-110">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="d3ea8-111">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="d3ea8-111">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="d3ea8-112">Microsoft consiglia di usare il modello di Gestione risorse per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="d3ea8-112">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="d3ea8-113">Per visualizzare la versione di Resource Manager di questo articolo, vedere [SQL Server Agent Extension for SQL Server VMs Gestione risorse](../sql/virtual-machines-windows-sql-server-agent-extension.md)(Estensione Agente IaaS per le VM SQL Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="d3ea8-113">To view the Resource Manager version of this article, see [SQL Server Agent Extension for SQL Server VMs Resource Manager](../sql/virtual-machines-windows-sql-server-agent-extension.md).</span></span>

## <a name="supported-services"></a><span data-ttu-id="d3ea8-114">Servizi supportati</span><span class="sxs-lookup"><span data-stu-id="d3ea8-114">Supported services</span></span>
<span data-ttu-id="d3ea8-115">L'Estensione Agente IaaS di SQL Server supporta le attività di amministrazione seguenti:</span><span class="sxs-lookup"><span data-stu-id="d3ea8-115">The SQL Server IaaS Agent Extension supports the following administration tasks:</span></span>

| <span data-ttu-id="d3ea8-116">Funzionalità di amministrazione</span><span class="sxs-lookup"><span data-stu-id="d3ea8-116">Administration feature</span></span> | <span data-ttu-id="d3ea8-117">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d3ea8-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d3ea8-118">**Backup automatico di SQL**</span><span class="sxs-lookup"><span data-stu-id="d3ea8-118">**SQL Automated Backup**</span></span> |<span data-ttu-id="d3ea8-119">Consente di automatizzare la pianificazione delle operazioni di backup per tutti i database correlati all'istanza predefinita di SQL Server nella VM.</span><span class="sxs-lookup"><span data-stu-id="d3ea8-119">Automates the scheduling of backups for all databases for the default instance of SQL Server in the VM.</span></span> <span data-ttu-id="d3ea8-120">Per altre informazioni, vedere [Backup automatico per SQL Server in macchine virtuali di Azure (distribuzione classica)](../classic/sql-automated-backup.md).</span><span class="sxs-lookup"><span data-stu-id="d3ea8-120">For more information, see [Automated backup for SQL Server in Azure Virtual Machines (Classic)](../classic/sql-automated-backup.md).</span></span> |
| <span data-ttu-id="d3ea8-121">**Applicazione automatica delle patch di SQL**</span><span class="sxs-lookup"><span data-stu-id="d3ea8-121">**SQL Automated Patching**</span></span> |<span data-ttu-id="d3ea8-122">Consente di configurare una finestra di manutenzione durante la quale eseguire gli aggiornamenti della VM, evitandone l'esecuzione durante i periodi di picco del carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="d3ea8-122">Configures a maintenance window during which updates to your VM can take place, so  you can avoid updates during peak times for your workload.</span></span> <span data-ttu-id="d3ea8-123">Per altre informazioni, vedere [Applicazione automatica delle patch per SQL Server in macchine virtuali di Azure (distribuzione classica)](../classic/sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="d3ea8-123">For more information, see [Automated patching for SQL Server in Azure Virtual Machines (Classic)](../classic/sql-automated-patching.md).</span></span> |
| <span data-ttu-id="d3ea8-124">**Integrazione di Azure Key Vault**</span><span class="sxs-lookup"><span data-stu-id="d3ea8-124">**Azure Key Vault Integration**</span></span> |<span data-ttu-id="d3ea8-125">Consente di installare e configurare automaticamente Azure Key Vault nella VM di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d3ea8-125">Enables you to automatically install and configure Azure Key Vault on your SQL Server VM.</span></span> <span data-ttu-id="d3ea8-126">Per altre informazioni, vedere [Configurare l'integrazione di Azure Key Vault per SQL Server in macchine virtuali di Azure (distribuzione classica)](../classic/ps-sql-keyvault.md).</span><span class="sxs-lookup"><span data-stu-id="d3ea8-126">For more information, see [Configure Azure Key Vault Integration for SQL Server on Azure VMs (Classic)](../classic/ps-sql-keyvault.md).</span></span> |

## <a name="prerequisites"></a><span data-ttu-id="d3ea8-127">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d3ea8-127">Prerequisites</span></span>
<span data-ttu-id="d3ea8-128">Requisiti per l'uso dell'Estensione Agente IaaS di SQL Server nella VM:</span><span class="sxs-lookup"><span data-stu-id="d3ea8-128">Requirements to use the SQL Server IaaS Agent Extension on your VM:</span></span>

### <a name="operating-system"></a><span data-ttu-id="d3ea8-129">Sistema operativo:</span><span class="sxs-lookup"><span data-stu-id="d3ea8-129">Operating System:</span></span>
* <span data-ttu-id="d3ea8-130">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="d3ea8-130">Windows Server 2012</span></span>
* <span data-ttu-id="d3ea8-131">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="d3ea8-131">Windows Server 2012 R2</span></span>
* <span data-ttu-id="d3ea8-132">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="d3ea8-132">Windows Server 2016</span></span>

### <a name="sql-server-versions"></a><span data-ttu-id="d3ea8-133">Versioni di SQL Server:</span><span class="sxs-lookup"><span data-stu-id="d3ea8-133">SQL Server versions:</span></span>
* <span data-ttu-id="d3ea8-134">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="d3ea8-134">SQL Server 2012</span></span>
* <span data-ttu-id="d3ea8-135">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="d3ea8-135">SQL Server 2014</span></span>
* <span data-ttu-id="d3ea8-136">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="d3ea8-136">SQL Server 2016</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="d3ea8-137">Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="d3ea8-137">Azure PowerShell:</span></span>
<span data-ttu-id="d3ea8-138">[Scaricare e configurare i comandi di Azure PowerShell più recenti](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d3ea8-138">[Download and configure the latest Azure PowerShell commands](/powershell/azure/overview).</span></span>

<span data-ttu-id="d3ea8-139">Avviare Windows PowerShell e connetterlo alla sottoscrizione di Azure mediante il comando **Add-AzureAccount** .</span><span class="sxs-lookup"><span data-stu-id="d3ea8-139">Start Windows PowerShell, and connect it to your Azure subscription with the **Add-AzureAccount** command.</span></span>

    Add-AzureAccount

<span data-ttu-id="d3ea8-140">Se si dispone di più sottoscrizioni, usare **Select-AzureSubscription** per selezionare la sottoscrizione contenente la VM di destinazione classica.</span><span class="sxs-lookup"><span data-stu-id="d3ea8-140">If you have multiple subscriptions, use **Select-AzureSubscription** to select the subscription that contains your target classic VM.</span></span>

    Select-AzureSubscription -SubscriptionName <subscriptionname>

<span data-ttu-id="d3ea8-141">A questo punto, usando il comando **Get-AzureVM** è possibile ottenere un elenco delle macchine virtuali classiche e dei nomi di servizio associati.</span><span class="sxs-lookup"><span data-stu-id="d3ea8-141">At this point, you can get a list of the classic virtual machines and their associated service names with the **Get-AzureVM** command.</span></span>

    Get-AzureVM

## <a name="installation"></a><span data-ttu-id="d3ea8-142">Installazione</span><span class="sxs-lookup"><span data-stu-id="d3ea8-142">Installation</span></span>
<span data-ttu-id="d3ea8-143">Per le VM classiche è necessario usare PowerShell per installare l'estensione di SQL Server IaaS Agent e configurarne i servizi associati.</span><span class="sxs-lookup"><span data-stu-id="d3ea8-143">For classic VMs, you must use PowerShell to install the SQL Server IaaS Agent Extension and configure its associated services.</span></span> <span data-ttu-id="d3ea8-144">Usare il cmdlet di PowerShell **Set-AzureVMSqlServerExtension** per installare l'estensione.</span><span class="sxs-lookup"><span data-stu-id="d3ea8-144">Use the **Set-AzureVMSqlServerExtension** PowerShell cmdlet to install the extension.</span></span> <span data-ttu-id="d3ea8-145">Ad esempio, il comando seguente installa l'estensione in una VM di Windows Server (distribuzione classica) denominandola "SQLIaaSExtension".</span><span class="sxs-lookup"><span data-stu-id="d3ea8-145">For example, the following command installs the extension on a Windows Server VM (classic) and names it "SQLIaaSExtension".</span></span>

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -ReferenceName "SQLIaasExtension" -Version "1.2" | Update-AzureVM

<span data-ttu-id="d3ea8-146">Se si esegue l'aggiornamento alla versione più recente dell'estensione dell'agente IaaS di SQL, è necessario riavviare la macchina virtuale dopo l'aggiornamento dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="d3ea8-146">If you update to the latest version of the SQL IaaS Agent Extension, you must restart your virtual machine after updating the extension.</span></span>

> [!NOTE]
> <span data-ttu-id="d3ea8-147">Le macchine virtuali classiche non dispongono di un'opzione per installare e configurare l'estensione di SQL Server IaaS Agent tramite il portale.</span><span class="sxs-lookup"><span data-stu-id="d3ea8-147">Classic virtual machines do not have an option to install and configure the SQL IaaS Agent Extension through the portal.</span></span>
> 
> 

## <a name="status"></a><span data-ttu-id="d3ea8-148">Stato</span><span class="sxs-lookup"><span data-stu-id="d3ea8-148">Status</span></span>
<span data-ttu-id="d3ea8-149">Un modo per verificare che l'estensione sia installata consiste nel visualizzare lo stato dell'agente nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d3ea8-149">One way to verify that the extension is installed is to view the agent status in the Azure Portal.</span></span> <span data-ttu-id="d3ea8-150">Selezionare una macchina virtuale elencata nel pannello della macchina virtuale e quindi fare clic su **Estensioni**.</span><span class="sxs-lookup"><span data-stu-id="d3ea8-150">Select a virtual machine listed in the virtual machine blade, and then click on **Extensions**.</span></span> <span data-ttu-id="d3ea8-151">Verrà elencata l'estensione **SQLIaaSAgent** .</span><span class="sxs-lookup"><span data-stu-id="d3ea8-151">You should see the **SQLIaaSAgent** extension listed.</span></span>

![Estensione Agente IaaS di SQL Server nel portale di Azure](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-portal.png)

<span data-ttu-id="d3ea8-153">È anche possibile usare il cmdlet di Azure PowerShell **Get-AzureVMSqlServerExtension** .</span><span class="sxs-lookup"><span data-stu-id="d3ea8-153">You can also use the **Get-AzureVMSqlServerExtension** Azure Powershell cmdlet.</span></span>

    Get-AzureVM –ServiceName "service" –Name "vmname" | Get-AzureVMSqlServerExtension

## <a name="removal"></a><span data-ttu-id="d3ea8-154">Rimozione</span><span class="sxs-lookup"><span data-stu-id="d3ea8-154">Removal</span></span>
<span data-ttu-id="d3ea8-155">Nel portale di Azure è possibile disinstallare l'estensione facendo clic sui puntini di sospensione nel pannello **Estensioni** delle proprietà della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d3ea8-155">In the Azure Portal, you can uninstall the extension by clicking the ellipsis on the **Extensions** blade of your virtual machine properties.</span></span> <span data-ttu-id="d3ea8-156">Fare clic su **Disinstalla**.</span><span class="sxs-lookup"><span data-stu-id="d3ea8-156">Then click **Uninstall**.</span></span>

![Disinstallare l'Estensione Agente IaaS di SQL Server nel portale di Azure](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-uninstall.png)

<span data-ttu-id="d3ea8-158">È anche possibile usare il cmdlet di PowerShell **Remove-AzureVMSqlServerExtension** .</span><span class="sxs-lookup"><span data-stu-id="d3ea8-158">You can also use the **Remove-AzureVMSqlServerExtension** Powershell cmdlet.</span></span>

    Get-AzureVM –ServiceName "service" –Name "vmname" | Remove-AzureVMSqlServerExtension | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="d3ea8-159">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d3ea8-159">Next Steps</span></span>
<span data-ttu-id="d3ea8-160">Iniziare a usare uno dei servizi supportati dall'estensione.</span><span class="sxs-lookup"><span data-stu-id="d3ea8-160">Begin using one of the services supported by the extension.</span></span> <span data-ttu-id="d3ea8-161">Per altre informazioni, vedere gli argomenti citati nella sezione [Servizi supportati](#supported-services) di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="d3ea8-161">For more details, see the topics referenced in the [Supported services](#supported-services) section of this article.</span></span>

<span data-ttu-id="d3ea8-162">Per altre informazioni sull'esecuzione di SQL Server in Macchine virtuali di Azure, vedere [Panoramica di SQL Server in Macchine virtuali di Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d3ea8-162">For more information about running SQL Server on Azure Virtual Machines, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

