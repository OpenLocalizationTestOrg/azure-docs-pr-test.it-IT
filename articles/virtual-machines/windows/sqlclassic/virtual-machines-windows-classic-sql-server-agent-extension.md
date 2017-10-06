---
title: "attività di gestione aaaAutomate nelle macchine virtuali di SQL (versione classica) | Documenti Microsoft"
description: "In questo argomento viene descritto come toomanage hello estensione agente SQL Server, che consente di automatizzare attività di amministrazione di SQL Server specifiche. Queste includono il backup automatizzato, l'applicazione automatica delle patch e l'integrazione dell'insieme di credenziali delle chiavi di Azure. In questo argomento Usa la modalità di distribuzione classica hello."
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
ms.openlocfilehash: a1dc011e0526845701eaf0c365007938f9ee32ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="automate-management-tasks-on-azure-virtual-machines-with-hello-sql-server-agent-extension-classic"></a><span data-ttu-id="270b1-105">Automatizzare le attività di gestione in macchine virtuali di Azure con hello estensione di SQL Server Agent (versione classica)</span><span class="sxs-lookup"><span data-stu-id="270b1-105">Automate management tasks on Azure Virtual Machines with hello SQL Server Agent Extension (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="270b1-106">Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="270b1-106">Resource Manager</span></span>](../sql/virtual-machines-windows-sql-server-agent-extension.md)
> * [<span data-ttu-id="270b1-107">Classico</span><span class="sxs-lookup"><span data-stu-id="270b1-107">Classic</span></span>](../classic/sql-server-agent-extension.md)
> 
>
 
<span data-ttu-id="270b1-108">Hello estensione agente IaaS di SQL Server (SQLIaaSAgent) viene eseguito su macchine virtuali di Azure tooautomate attività di amministrazione.</span><span class="sxs-lookup"><span data-stu-id="270b1-108">hello SQL Server IaaS Agent Extension (SQLIaaSAgent) runs on Azure virtual machines tooautomate administration tasks.</span></span> <span data-ttu-id="270b1-109">In questo argomento viene fornita una panoramica di servizi di hello supportati dall'estensione hello, nonché istruzioni per l'installazione, stato e rimozione.</span><span class="sxs-lookup"><span data-stu-id="270b1-109">This topic provides an overview of hello services supported by hello extension as well as instructions for installation, status, and removal.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="270b1-110">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="270b1-110">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="270b1-111">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="270b1-111">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="270b1-112">Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="270b1-112">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="270b1-113">tooview hello Gestione risorse di questo articolo, vedere [estensione Gestione risorse per SQL Server le macchine virtuali di SQL Server Agent](../sql/virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="270b1-113">tooview hello Resource Manager version of this article, see [SQL Server Agent Extension for SQL Server VMs Resource Manager](../sql/virtual-machines-windows-sql-server-agent-extension.md).</span></span>

## <a name="supported-services"></a><span data-ttu-id="270b1-114">Servizi supportati</span><span class="sxs-lookup"><span data-stu-id="270b1-114">Supported services</span></span>
<span data-ttu-id="270b1-115">Estensione di SQL Server IaaS Agent Hello supporta hello seguenti attività di amministrazione:</span><span class="sxs-lookup"><span data-stu-id="270b1-115">hello SQL Server IaaS Agent Extension supports hello following administration tasks:</span></span>

| <span data-ttu-id="270b1-116">Funzionalità di amministrazione</span><span class="sxs-lookup"><span data-stu-id="270b1-116">Administration feature</span></span> | <span data-ttu-id="270b1-117">Descrizione</span><span class="sxs-lookup"><span data-stu-id="270b1-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="270b1-118">**Backup automatico di SQL**</span><span class="sxs-lookup"><span data-stu-id="270b1-118">**SQL Automated Backup**</span></span> |<span data-ttu-id="270b1-119">Consente di automatizzare hello pianificazione dei backup per tutti i database per l'istanza predefinita di hello di SQL Server in VM hello.</span><span class="sxs-lookup"><span data-stu-id="270b1-119">Automates hello scheduling of backups for all databases for hello default instance of SQL Server in hello VM.</span></span> <span data-ttu-id="270b1-120">Per altre informazioni, vedere [Backup automatico per SQL Server in macchine virtuali di Azure (distribuzione classica)](../classic/sql-automated-backup.md).</span><span class="sxs-lookup"><span data-stu-id="270b1-120">For more information, see [Automated backup for SQL Server in Azure Virtual Machines (Classic)](../classic/sql-automated-backup.md).</span></span> |
| <span data-ttu-id="270b1-121">**Applicazione automatica delle patch di SQL**</span><span class="sxs-lookup"><span data-stu-id="270b1-121">**SQL Automated Patching**</span></span> |<span data-ttu-id="270b1-122">Configura una finestra di manutenzione durante gli aggiornamenti inserisce tooyour macchina virtuale può richiedere, pertanto è possibile evitare gli aggiornamenti durante le ore di punta per il carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="270b1-122">Configures a maintenance window during which updates tooyour VM can take place, so  you can avoid updates during peak times for your workload.</span></span> <span data-ttu-id="270b1-123">Per altre informazioni, vedere [Applicazione automatica delle patch per SQL Server in macchine virtuali di Azure (distribuzione classica)](../classic/sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="270b1-123">For more information, see [Automated patching for SQL Server in Azure Virtual Machines (Classic)](../classic/sql-automated-patching.md).</span></span> |
| <span data-ttu-id="270b1-124">**Integrazione di Azure Key Vault**</span><span class="sxs-lookup"><span data-stu-id="270b1-124">**Azure Key Vault Integration**</span></span> |<span data-ttu-id="270b1-125">Abilita è tooautomatically installare e configurare l'insieme di credenziali chiave di Azure nella VM SQL Server.</span><span class="sxs-lookup"><span data-stu-id="270b1-125">Enables you tooautomatically install and configure Azure Key Vault on your SQL Server VM.</span></span> <span data-ttu-id="270b1-126">Per altre informazioni, vedere [Configurare l'integrazione di Azure Key Vault per SQL Server in macchine virtuali di Azure (distribuzione classica)](../classic/ps-sql-keyvault.md).</span><span class="sxs-lookup"><span data-stu-id="270b1-126">For more information, see [Configure Azure Key Vault Integration for SQL Server on Azure VMs (Classic)](../classic/ps-sql-keyvault.md).</span></span> |

## <a name="prerequisites"></a><span data-ttu-id="270b1-127">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="270b1-127">Prerequisites</span></span>
<span data-ttu-id="270b1-128">Requisiti toouse hello estensione agente IaaS di SQL Server nella VM:</span><span class="sxs-lookup"><span data-stu-id="270b1-128">Requirements toouse hello SQL Server IaaS Agent Extension on your VM:</span></span>

### <a name="operating-system"></a><span data-ttu-id="270b1-129">Sistema operativo:</span><span class="sxs-lookup"><span data-stu-id="270b1-129">Operating System:</span></span>
* <span data-ttu-id="270b1-130">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="270b1-130">Windows Server 2012</span></span>
* <span data-ttu-id="270b1-131">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="270b1-131">Windows Server 2012 R2</span></span>
* <span data-ttu-id="270b1-132">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="270b1-132">Windows Server 2016</span></span>

### <a name="sql-server-versions"></a><span data-ttu-id="270b1-133">Versioni di SQL Server:</span><span class="sxs-lookup"><span data-stu-id="270b1-133">SQL Server versions:</span></span>
* <span data-ttu-id="270b1-134">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="270b1-134">SQL Server 2012</span></span>
* <span data-ttu-id="270b1-135">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="270b1-135">SQL Server 2014</span></span>
* <span data-ttu-id="270b1-136">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="270b1-136">SQL Server 2016</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="270b1-137">Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="270b1-137">Azure PowerShell:</span></span>
<span data-ttu-id="270b1-138">[Scaricare e configurare i comandi di PowerShell di Azure più recenti hello](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="270b1-138">[Download and configure hello latest Azure PowerShell commands](/powershell/azure/overview).</span></span>

<span data-ttu-id="270b1-139">Avviare Windows PowerShell e connetterla tooyour sottoscrizione di Azure con hello **Add-AzureAccount** comando.</span><span class="sxs-lookup"><span data-stu-id="270b1-139">Start Windows PowerShell, and connect it tooyour Azure subscription with hello **Add-AzureAccount** command.</span></span>

    Add-AzureAccount

<span data-ttu-id="270b1-140">Se si dispone di più sottoscrizioni, usare **Select-AzureSubscription** sottoscrizione hello tooselect che contiene la destinazione VM classico.</span><span class="sxs-lookup"><span data-stu-id="270b1-140">If you have multiple subscriptions, use **Select-AzureSubscription** tooselect hello subscription that contains your target classic VM.</span></span>

    Select-AzureSubscription -SubscriptionName <subscriptionname>

<span data-ttu-id="270b1-141">A questo punto, è possibile ottenere un elenco di macchine virtuali classiche hello e i relativi nomi di servizio associato con hello **Get-AzureVM** comando.</span><span class="sxs-lookup"><span data-stu-id="270b1-141">At this point, you can get a list of hello classic virtual machines and their associated service names with hello **Get-AzureVM** command.</span></span>

    Get-AzureVM

## <a name="installation"></a><span data-ttu-id="270b1-142">Installazione</span><span class="sxs-lookup"><span data-stu-id="270b1-142">Installation</span></span>
<span data-ttu-id="270b1-143">Per le macchine virtuali classiche, è necessario usare PowerShell tooinstall hello estensione agente IaaS di SQL Server e configurare i servizi associati.</span><span class="sxs-lookup"><span data-stu-id="270b1-143">For classic VMs, you must use PowerShell tooinstall hello SQL Server IaaS Agent Extension and configure its associated services.</span></span> <span data-ttu-id="270b1-144">Hello utilizzare **Set AzureVMSqlServerExtension** estensione hello tooinstall cmdlet di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="270b1-144">Use hello **Set-AzureVMSqlServerExtension** PowerShell cmdlet tooinstall hello extension.</span></span> <span data-ttu-id="270b1-145">Ad esempio, hello comando seguente installa estensione hello in una VM di Windows Server (versione classica) e gli assegna il "SQLIaaSExtension".</span><span class="sxs-lookup"><span data-stu-id="270b1-145">For example, hello following command installs hello extension on a Windows Server VM (classic) and names it "SQLIaaSExtension".</span></span>

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -ReferenceName "SQLIaasExtension" -Version "1.2" | Update-AzureVM

<span data-ttu-id="270b1-146">Se si aggiorna toohello la versione più recente di hello estensione agente IaaS di SQL Server, è necessario riavviare la macchina virtuale dopo l'aggiornamento dell'estensione hello.</span><span class="sxs-lookup"><span data-stu-id="270b1-146">If you update toohello latest version of hello SQL IaaS Agent Extension, you must restart your virtual machine after updating hello extension.</span></span>

> [!NOTE]
> <span data-ttu-id="270b1-147">Macchine virtuali classiche non è un'opzione tooinstall e configurare hello estensione SQL IaaS Agent tramite il portale di hello.</span><span class="sxs-lookup"><span data-stu-id="270b1-147">Classic virtual machines do not have an option tooinstall and configure hello SQL IaaS Agent Extension through hello portal.</span></span>
> 
> 

## <a name="status"></a><span data-ttu-id="270b1-148">Stato</span><span class="sxs-lookup"><span data-stu-id="270b1-148">Status</span></span>
<span data-ttu-id="270b1-149">Tooverify un modo che sia installato l'estensione hello è lo stato dell'agente hello tooview in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="270b1-149">One way tooverify that hello extension is installed is tooview hello agent status in hello Azure Portal.</span></span> <span data-ttu-id="270b1-150">Selezionare una macchina virtuale elencata nel pannello macchine virtuali hello e quindi fare clic su **estensioni**.</span><span class="sxs-lookup"><span data-stu-id="270b1-150">Select a virtual machine listed in hello virtual machine blade, and then click on **Extensions**.</span></span> <span data-ttu-id="270b1-151">Dovrebbe essere hello **SQLIaaSAgent** estensione elencati.</span><span class="sxs-lookup"><span data-stu-id="270b1-151">You should see hello **SQLIaaSAgent** extension listed.</span></span>

![Estensione Agente IaaS di SQL Server nel portale di Azure](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-portal.png)

<span data-ttu-id="270b1-153">È inoltre possibile utilizzare hello **Get AzureVMSqlServerExtension** cmdlet Powershell di Azure.</span><span class="sxs-lookup"><span data-stu-id="270b1-153">You can also use hello **Get-AzureVMSqlServerExtension** Azure Powershell cmdlet.</span></span>

    Get-AzureVM –ServiceName "service" –Name "vmname" | Get-AzureVMSqlServerExtension

## <a name="removal"></a><span data-ttu-id="270b1-154">Rimozione</span><span class="sxs-lookup"><span data-stu-id="270b1-154">Removal</span></span>
<span data-ttu-id="270b1-155">Nel portale di Azure hello, è possibile disinstallare l'estensione hello facendo clic sui puntini di sospensione hello in hello **estensioni** pannello delle proprietà di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="270b1-155">In hello Azure Portal, you can uninstall hello extension by clicking hello ellipsis on hello **Extensions** blade of your virtual machine properties.</span></span> <span data-ttu-id="270b1-156">Fare clic su **Disinstalla**.</span><span class="sxs-lookup"><span data-stu-id="270b1-156">Then click **Uninstall**.</span></span>

![Disinstallare hello estensione agente IaaS di SQL Server nel portale di Azure](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-uninstall.png)

<span data-ttu-id="270b1-158">È inoltre possibile utilizzare hello **Remove AzureVMSqlServerExtension** cmdlet di Powershell.</span><span class="sxs-lookup"><span data-stu-id="270b1-158">You can also use hello **Remove-AzureVMSqlServerExtension** Powershell cmdlet.</span></span>

    Get-AzureVM –ServiceName "service" –Name "vmname" | Remove-AzureVMSqlServerExtension | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="270b1-159">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="270b1-159">Next Steps</span></span>
<span data-ttu-id="270b1-160">Iniziare a utilizzare uno dei servizi di hello supportati dall'estensione hello.</span><span class="sxs-lookup"><span data-stu-id="270b1-160">Begin using one of hello services supported by hello extension.</span></span> <span data-ttu-id="270b1-161">Per ulteriori informazioni, vedere gli argomenti di hello elencati in hello [servizi supportati](#supported-services) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="270b1-161">For more details, see hello topics referenced in hello [Supported services](#supported-services) section of this article.</span></span>

<span data-ttu-id="270b1-162">Per altre informazioni sull'esecuzione di SQL Server in Macchine virtuali di Azure, vedere [Panoramica di SQL Server in Macchine virtuali di Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="270b1-162">For more information about running SQL Server on Azure Virtual Machines, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

