---
title: "attività di gestione aaaAutomate nelle macchine virtuali di SQL (gestione delle risorse) | Documenti Microsoft"
description: "In questo argomento viene descritto come toomanage hello estensione agente SQL Server, che consente di automatizzare attività di amministrazione di SQL Server specifiche. Queste includono il backup automatizzato, l'applicazione automatica delle patch e l'integrazione dell'insieme di credenziali delle chiavi di Azure. In questo argomento Usa la modalità di distribuzione di gestione risorse hello."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: effe4e2f-35b5-490a-b5ef-b06746083da4
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/07/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ae917612c4af59f12c0b083440673bdc555e9d56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="automate-management-tasks-on-azure-virtual-machines-with-hello-sql-server-agent-extension-resource-manager"></a><span data-ttu-id="d001a-105">Automatizzare le attività di gestione in macchine virtuali di Azure con hello estensione di SQL Server Agent (gestione delle risorse)</span><span class="sxs-lookup"><span data-stu-id="d001a-105">Automate management tasks on Azure Virtual Machines with hello SQL Server Agent Extension (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d001a-106">Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="d001a-106">Resource Manager</span></span>](virtual-machines-windows-sql-server-agent-extension.md)
> * [<span data-ttu-id="d001a-107">Classico</span><span class="sxs-lookup"><span data-stu-id="d001a-107">Classic</span></span>](../classic/sql-server-agent-extension.md)
> 
> 

<span data-ttu-id="d001a-108">Hello estensione agente IaaS di SQL Server (SQLIaaSExtension) viene eseguito su macchine virtuali di Azure tooautomate attività di amministrazione.</span><span class="sxs-lookup"><span data-stu-id="d001a-108">hello SQL Server IaaS Agent Extension (SQLIaaSExtension) runs on Azure virtual machines tooautomate administration tasks.</span></span> <span data-ttu-id="d001a-109">In questo argomento viene fornita una panoramica di servizi di hello supportati dall'estensione hello, nonché istruzioni per l'installazione, stato e rimozione.</span><span class="sxs-lookup"><span data-stu-id="d001a-109">This topic provides an overview of hello services supported by hello extension as well as instructions for installation, status, and removal.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="d001a-110">versione classica di hello tooview di questo articolo, vedere [estensione di SQL Server Agent per le macchine virtuali classiche di SQL Server](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="d001a-110">tooview hello classic version of this article, see [SQL Server Agent Extension for SQL Server VMs Classic](../classic/sql-server-agent-extension.md).</span></span>

## <a name="supported-services"></a><span data-ttu-id="d001a-111">Servizi supportati</span><span class="sxs-lookup"><span data-stu-id="d001a-111">Supported services</span></span>
<span data-ttu-id="d001a-112">Estensione di SQL Server IaaS Agent Hello supporta hello seguenti attività di amministrazione:</span><span class="sxs-lookup"><span data-stu-id="d001a-112">hello SQL Server IaaS Agent Extension supports hello following administration tasks:</span></span>

| <span data-ttu-id="d001a-113">Funzionalità di amministrazione</span><span class="sxs-lookup"><span data-stu-id="d001a-113">Administration feature</span></span> | <span data-ttu-id="d001a-114">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d001a-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d001a-115">**Backup automatico di SQL**</span><span class="sxs-lookup"><span data-stu-id="d001a-115">**SQL Automated Backup**</span></span> |<span data-ttu-id="d001a-116">Consente di automatizzare hello pianificazione dei backup per tutti i database per l'istanza predefinita di hello di SQL Server in VM hello.</span><span class="sxs-lookup"><span data-stu-id="d001a-116">Automates hello scheduling of backups for all databases for hello default instance of SQL Server in hello VM.</span></span> <span data-ttu-id="d001a-117">Per altre informazioni, vedere [Backup automatico per SQL Server nelle macchine virtuali di Azure (Resource Manager)](virtual-machines-windows-sql-automated-backup.md).</span><span class="sxs-lookup"><span data-stu-id="d001a-117">For more information, see [Automated backup for SQL Server in Azure Virtual Machines (Resource Manager)](virtual-machines-windows-sql-automated-backup.md).</span></span> |
| <span data-ttu-id="d001a-118">**Applicazione automatica delle patch di SQL**</span><span class="sxs-lookup"><span data-stu-id="d001a-118">**SQL Automated Patching**</span></span> |<span data-ttu-id="d001a-119">Configura una finestra di manutenzione durante gli aggiornamenti inserisce tooyour macchina virtuale può richiedere, pertanto è possibile evitare gli aggiornamenti durante le ore di punta per il carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="d001a-119">Configures a maintenance window during which updates tooyour VM can take place, so  you can avoid updates during peak times for your workload.</span></span> <span data-ttu-id="d001a-120">Per altre informazioni, vedere [Applicazione automatica delle patch per SQL Server nelle macchine virtuali di Azure (Resource Manager)](virtual-machines-windows-sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="d001a-120">For more information, see [Automated patching for SQL Server in Azure Virtual Machines (Resource Manager)](virtual-machines-windows-sql-automated-patching.md).</span></span> |
| <span data-ttu-id="d001a-121">**Integrazione di Azure Key Vault**</span><span class="sxs-lookup"><span data-stu-id="d001a-121">**Azure Key Vault Integration**</span></span> |<span data-ttu-id="d001a-122">Abilita è tooautomatically installare e configurare l'insieme di credenziali chiave di Azure nella VM SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d001a-122">Enables you tooautomatically install and configure Azure Key Vault on your SQL Server VM.</span></span> <span data-ttu-id="d001a-123">Per altre informazioni, vedere [Configurare l'integrazione dell'insieme di credenziali delle chiavi di Azure per SQL Server in Macchine virtuali di Azure (Resource Manager)](virtual-machines-windows-ps-sql-keyvault.md).</span><span class="sxs-lookup"><span data-stu-id="d001a-123">For more information, see [Configure Azure Key Vault Integration for SQL Server on Azure VMs (Resource Manager)](virtual-machines-windows-ps-sql-keyvault.md).</span></span> |

<span data-ttu-id="d001a-124">Dopo aver installato e in esecuzione, hello estensione di SQL Server IaaS Agent disponibili queste funzionalità di amministrazione nel Pannello di SQL Server hello di hello macchina virtuale nel portale di Azure hello e tramite Azure PowerShell per le immagini di SQL Server marketplace e tramite Azure PowerShell per le installazioni manuali dell'estensione hello.</span><span class="sxs-lookup"><span data-stu-id="d001a-124">Once installed and running, hello SQL Server IaaS Agent Extension makes these administration features available on hello SQL Server panel of hello virtual machine in hello Azure Portal and through Azure PowerShell for SQL Server marketplace images, and through Azure PowerShell for manual installations of hello extension.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d001a-125">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d001a-125">Prerequisites</span></span>
<span data-ttu-id="d001a-126">Requisiti toouse hello estensione agente IaaS di SQL Server nella VM:</span><span class="sxs-lookup"><span data-stu-id="d001a-126">Requirements toouse hello SQL Server IaaS Agent Extension on your VM:</span></span>

<span data-ttu-id="d001a-127">**Sistema operativo**:</span><span class="sxs-lookup"><span data-stu-id="d001a-127">**Operating System**:</span></span>

* <span data-ttu-id="d001a-128">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="d001a-128">Windows Server 2012</span></span>
* <span data-ttu-id="d001a-129">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="d001a-129">Windows Server 2012 R2</span></span>
* <span data-ttu-id="d001a-130">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="d001a-130">Windows Server 2016</span></span>

<span data-ttu-id="d001a-131">**Versioni di SQL Server**:</span><span class="sxs-lookup"><span data-stu-id="d001a-131">**SQL Server versions**:</span></span>

* <span data-ttu-id="d001a-132">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="d001a-132">SQL Server 2012</span></span>
* <span data-ttu-id="d001a-133">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="d001a-133">SQL Server 2014</span></span>
* <span data-ttu-id="d001a-134">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="d001a-134">SQL Server 2016</span></span>

<span data-ttu-id="d001a-135">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="d001a-135">**Azure PowerShell**:</span></span>

* [<span data-ttu-id="d001a-136">Scaricare e configurare i comandi di PowerShell di Azure più recenti hello</span><span class="sxs-lookup"><span data-stu-id="d001a-136">Download and configure hello latest Azure PowerShell commands</span></span>](/powershell/azure/overview)

## <a name="installation"></a><span data-ttu-id="d001a-137">Installazione</span><span class="sxs-lookup"><span data-stu-id="d001a-137">Installation</span></span>
<span data-ttu-id="d001a-138">Hello estensione agente IaaS di SQL Server viene installato automaticamente quando si esegue il provisioning di una delle immagini della raccolta di macchine virtuali SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="d001a-138">hello SQL Server IaaS Agent Extension is automatically installed when you provision one of hello SQL Server virtual machine gallery images.</span></span> <span data-ttu-id="d001a-139">Se è necessario estensione hello tooreinstall manualmente su una di queste macchine virtuali di SQL Server, utilizzare hello comando PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="d001a-139">If you need tooreinstall hello extension manually on one of these SQL Server VMs, use hello following PowerShell command:</span></span>

```powershell
Set-AzureRmVMSqlServerExtension -ResourceGroupName "resourcegroupname" -VMName "vmname" -Name "SQLIaasExtension" -Version "1.2" -Location "East US 2"
```

<span data-ttu-id="d001a-140">È inoltre possibile tooinstall hello estensione agente IaaS di SQL Server in una macchina virtuale del sistema operativo Windows Server.</span><span class="sxs-lookup"><span data-stu-id="d001a-140">It is also possible tooinstall hello SQL Server IaaS Agent Extension on an OS-only Windows Server virtual machine.</span></span> <span data-ttu-id="d001a-141">Questa soluzione è supportata solo se SQL Server è stato installato manualmente sul computer.</span><span class="sxs-lookup"><span data-stu-id="d001a-141">This is only supported if you have also manually installed SQL Server on that machine.</span></span> <span data-ttu-id="d001a-142">Quindi installare hello estensione manualmente utilizzando hello stesso **Set AzureVMSqlServerExtension** cmdlet di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d001a-142">Then install hello extension manually by using hello same **Set-AzureVMSqlServerExtension** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="d001a-143">Se si installa manualmente hello estensione agente IaaS di SQL Server in una VM solo sistema operativo Windows Server, è possibile gestire non le impostazioni di configurazione di SQL Server hello tramite hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d001a-143">If you manually install hello SQL Server IaaS Agent Extension on an OS-only Windows Server VM, you can not manage hello SQL Server configuration settings through hello Azure portal.</span></span> <span data-ttu-id="d001a-144">In questo scenario è necessario eseguire tutte le modifiche con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d001a-144">In this scenario, you must make all changes with PowerShell.</span></span>

## <a name="status"></a><span data-ttu-id="d001a-145">Stato</span><span class="sxs-lookup"><span data-stu-id="d001a-145">Status</span></span>
<span data-ttu-id="d001a-146">Tooverify un modo che sia installato l'estensione hello è lo stato dell'agente hello tooview in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d001a-146">One way tooverify that hello extension is installed is tooview hello agent status in hello Azure Portal.</span></span> <span data-ttu-id="d001a-147">Selezionare **tutte le impostazioni** in hello pannello macchine virtuali e quindi fare clic su **estensioni**.</span><span class="sxs-lookup"><span data-stu-id="d001a-147">Select **All settings** in hello virtual machine blade, and then click on **Extensions**.</span></span> <span data-ttu-id="d001a-148">Dovrebbe essere hello **SQLIaaSExtension** estensione elencati.</span><span class="sxs-lookup"><span data-stu-id="d001a-148">You should see hello **SQLIaaSExtension** extension listed.</span></span>

![Estensione Agente IaaS di SQL Server nel portale di Azure](./media/virtual-machines-windows-sql-server-agent-extension/azure-rm-sql-server-iaas-agent-portal.png)

<span data-ttu-id="d001a-150">È inoltre possibile utilizzare hello **Get AzureVMSqlServerExtension** cmdlet Powershell di Azure.</span><span class="sxs-lookup"><span data-stu-id="d001a-150">You can also use hello **Get-AzureVMSqlServerExtension** Azure Powershell cmdlet.</span></span>

    Get-AzureRmVMSqlServerExtension -VMName "vmname" -ResourceGroupName "resourcegroupname"

<span data-ttu-id="d001a-151">comando precedente Hello conferma agente hello viene installato e fornisce informazioni sullo stato generale.</span><span class="sxs-lookup"><span data-stu-id="d001a-151">hello previous command confirms hello agent is installed and provides general status information.</span></span> <span data-ttu-id="d001a-152">È anche possibile ottenere informazioni specifiche sullo stato Backup automatizzato e l'applicazione di patch con hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="d001a-152">You can also get specific status information about Automated Backup and Patching with hello following commands.</span></span>

    $sqlext = Get-AzureRmVMSqlServerExtension -VMName "vmname" -ResourceGroupName "resourcegroupname"
    $sqlext.AutoPatchingSettings
    $sqlext.AutoBackupSettings

## <a name="removal"></a><span data-ttu-id="d001a-153">Rimozione</span><span class="sxs-lookup"><span data-stu-id="d001a-153">Removal</span></span>
<span data-ttu-id="d001a-154">Nel portale di Azure hello, è possibile disinstallare l'estensione hello facendo clic sui puntini di sospensione hello in hello **estensioni** pannello delle proprietà di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d001a-154">In hello Azure Portal, you can uninstall hello extension by clicking hello ellipsis on hello **Extensions** blade of your virtual machine properties.</span></span> <span data-ttu-id="d001a-155">Fare quindi clic su **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="d001a-155">Then click **Delete**.</span></span>

![Disinstallare hello estensione agente IaaS di SQL Server nel portale di Azure](./media/virtual-machines-windows-sql-server-agent-extension/azure-rm-sql-server-iaas-agent-uninstall.png)

<span data-ttu-id="d001a-157">È inoltre possibile utilizzare hello **Remove AzureRmVMSqlServerExtension** cmdlet di Powershell.</span><span class="sxs-lookup"><span data-stu-id="d001a-157">You can also use hello **Remove-AzureRmVMSqlServerExtension** Powershell cmdlet.</span></span>

    Remove-AzureRmVMSqlServerExtension -ResourceGroupName "resourcegroupname" -VMName "vmname" -Name "SQLIaasExtension"

## <a name="next-steps"></a><span data-ttu-id="d001a-158">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d001a-158">Next Steps</span></span>
<span data-ttu-id="d001a-159">Iniziare a utilizzare uno dei servizi di hello supportati dall'estensione hello.</span><span class="sxs-lookup"><span data-stu-id="d001a-159">Begin using one of hello services supported by hello extension.</span></span> <span data-ttu-id="d001a-160">Per ulteriori informazioni, vedere gli argomenti di hello elencati in hello [servizi supportati](#supported-services) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="d001a-160">For more details, see hello topics referenced in hello [Supported services](#supported-services) section of this article.</span></span>

<span data-ttu-id="d001a-161">Per altre informazioni sull'esecuzione di SQL Server in Macchine virtuali di Azure, vedere [Panoramica di SQL Server in Macchine virtuali di Azure](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d001a-161">For more information about running SQL Server on Azure Virtual Machines, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

