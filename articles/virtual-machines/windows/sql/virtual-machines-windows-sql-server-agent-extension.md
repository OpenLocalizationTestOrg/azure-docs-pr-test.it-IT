---
title: "Automatizzare le attività di gestione in macchine virtuali SQL (Resource Manager) | Microsoft Docs"
description: "Questo argomento descrive come gestire l'estensione di SQL Server Agent, che consente di automatizzare attività di amministrazione di SQL Server specifiche. Queste includono il backup automatizzato, l'applicazione automatica delle patch e l'integrazione dell'insieme di credenziali delle chiavi di Azure. Questo argomento usa il modello di distribuzione Resource Manager."
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
ms.openlocfilehash: 7152d184bb6d1d4b81aeb47e2c7c9160ada36023
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="automate-management-tasks-on-azure-virtual-machines-with-the-sql-server-agent-extension-resource-manager"></a><span data-ttu-id="d3d81-105">Automatizzare le attività di gestione in macchine virtuali SQL con l'estensione SQL Server Agent (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="d3d81-105">Automate management tasks on Azure Virtual Machines with the SQL Server Agent Extension (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d3d81-106">Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="d3d81-106">Resource Manager</span></span>](virtual-machines-windows-sql-server-agent-extension.md)
> * [<span data-ttu-id="d3d81-107">Classico</span><span class="sxs-lookup"><span data-stu-id="d3d81-107">Classic</span></span>](../classic/sql-server-agent-extension.md)
> 
> 

<span data-ttu-id="d3d81-108">L'Estensione Agente IaaS di SQL Server (SQLIaaSExtension) viene eseguita su macchine virtuali di Azure per automatizzare le attività di amministrazione.</span><span class="sxs-lookup"><span data-stu-id="d3d81-108">The SQL Server IaaS Agent Extension (SQLIaaSExtension) runs on Azure virtual machines to automate administration tasks.</span></span> <span data-ttu-id="d3d81-109">Questo argomento fornisce una panoramica dei servizi supportati dall'estensione e delle istruzioni per l'installazione, lo stato e la rimozione.</span><span class="sxs-lookup"><span data-stu-id="d3d81-109">This topic provides an overview of the services supported by the extension as well as instructions for installation, status, and removal.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="d3d81-110">Per visualizzare la versione classica di questo articolo, vedere [Estensione Agente IaaS di SQL Server (distribuzione classica)](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="d3d81-110">To view the classic version of this article, see [SQL Server Agent Extension for SQL Server VMs Classic](../classic/sql-server-agent-extension.md).</span></span>

## <a name="supported-services"></a><span data-ttu-id="d3d81-111">Servizi supportati</span><span class="sxs-lookup"><span data-stu-id="d3d81-111">Supported services</span></span>
<span data-ttu-id="d3d81-112">L'Estensione Agente IaaS di SQL Server supporta le attività di amministrazione seguenti:</span><span class="sxs-lookup"><span data-stu-id="d3d81-112">The SQL Server IaaS Agent Extension supports the following administration tasks:</span></span>

| <span data-ttu-id="d3d81-113">Funzionalità di amministrazione</span><span class="sxs-lookup"><span data-stu-id="d3d81-113">Administration feature</span></span> | <span data-ttu-id="d3d81-114">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d3d81-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d3d81-115">**Backup automatico di SQL**</span><span class="sxs-lookup"><span data-stu-id="d3d81-115">**SQL Automated Backup**</span></span> |<span data-ttu-id="d3d81-116">Consente di automatizzare la pianificazione delle operazioni di backup per tutti i database correlati all'istanza predefinita di SQL Server nella VM.</span><span class="sxs-lookup"><span data-stu-id="d3d81-116">Automates the scheduling of backups for all databases for the default instance of SQL Server in the VM.</span></span> <span data-ttu-id="d3d81-117">Per altre informazioni, vedere [Backup automatico per SQL Server nelle macchine virtuali di Azure (Resource Manager)](virtual-machines-windows-sql-automated-backup.md).</span><span class="sxs-lookup"><span data-stu-id="d3d81-117">For more information, see [Automated backup for SQL Server in Azure Virtual Machines (Resource Manager)](virtual-machines-windows-sql-automated-backup.md).</span></span> |
| <span data-ttu-id="d3d81-118">**Applicazione automatica delle patch di SQL**</span><span class="sxs-lookup"><span data-stu-id="d3d81-118">**SQL Automated Patching**</span></span> |<span data-ttu-id="d3d81-119">Consente di configurare una finestra di manutenzione durante la quale eseguire gli aggiornamenti della VM, evitandone l'esecuzione durante i periodi di picco del carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="d3d81-119">Configures a maintenance window during which updates to your VM can take place, so  you can avoid updates during peak times for your workload.</span></span> <span data-ttu-id="d3d81-120">Per altre informazioni, vedere [Applicazione automatica delle patch per SQL Server nelle macchine virtuali di Azure (Resource Manager)](virtual-machines-windows-sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="d3d81-120">For more information, see [Automated patching for SQL Server in Azure Virtual Machines (Resource Manager)](virtual-machines-windows-sql-automated-patching.md).</span></span> |
| <span data-ttu-id="d3d81-121">**Integrazione dell'insieme di credenziali delle chiavi di Azure**</span><span class="sxs-lookup"><span data-stu-id="d3d81-121">**Azure Key Vault Integration**</span></span> |<span data-ttu-id="d3d81-122">Consente di installare e configurare automaticamente l'insieme di credenziali delle chiavi di Azure nella VM di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d3d81-122">Enables you to automatically install and configure Azure Key Vault on your SQL Server VM.</span></span> <span data-ttu-id="d3d81-123">Per altre informazioni, vedere [Configurare l'integrazione dell'insieme di credenziali delle chiavi di Azure per SQL Server in Macchine virtuali di Azure (Resource Manager)](virtual-machines-windows-ps-sql-keyvault.md).</span><span class="sxs-lookup"><span data-stu-id="d3d81-123">For more information, see [Configure Azure Key Vault Integration for SQL Server on Azure VMs (Resource Manager)](virtual-machines-windows-ps-sql-keyvault.md).</span></span> |

<span data-ttu-id="d3d81-124">Dopo averlo installato e messo in esecuzione, l'estensione dell'agente IaaS di SQL Server rende disponibili queste funzionalità di amministrazione nel pannello SQL Server della macchina virtuale nel portale di Azure e tramite Azure PowerShell per le immagini del marketplace di SQL Server e Azure PowerShell per le installazioni manuali dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="d3d81-124">Once installed and running, the SQL Server IaaS Agent Extension makes these administration features available on the SQL Server panel of the virtual machine in the Azure Portal and through Azure PowerShell for SQL Server marketplace images, and through Azure PowerShell for manual installations of the extension.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d3d81-125">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d3d81-125">Prerequisites</span></span>
<span data-ttu-id="d3d81-126">Requisiti per l'uso dell'Estensione Agente IaaS di SQL Server nella VM:</span><span class="sxs-lookup"><span data-stu-id="d3d81-126">Requirements to use the SQL Server IaaS Agent Extension on your VM:</span></span>

<span data-ttu-id="d3d81-127">**Sistema operativo**:</span><span class="sxs-lookup"><span data-stu-id="d3d81-127">**Operating System**:</span></span>

* <span data-ttu-id="d3d81-128">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="d3d81-128">Windows Server 2012</span></span>
* <span data-ttu-id="d3d81-129">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="d3d81-129">Windows Server 2012 R2</span></span>
* <span data-ttu-id="d3d81-130">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="d3d81-130">Windows Server 2016</span></span>

<span data-ttu-id="d3d81-131">**Versioni di SQL Server**:</span><span class="sxs-lookup"><span data-stu-id="d3d81-131">**SQL Server versions**:</span></span>

* <span data-ttu-id="d3d81-132">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="d3d81-132">SQL Server 2012</span></span>
* <span data-ttu-id="d3d81-133">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="d3d81-133">SQL Server 2014</span></span>
* <span data-ttu-id="d3d81-134">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="d3d81-134">SQL Server 2016</span></span>

<span data-ttu-id="d3d81-135">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="d3d81-135">**Azure PowerShell**:</span></span>

* [<span data-ttu-id="d3d81-136">Scaricare e configurare i comandi di Azure PowerShell più recenti</span><span class="sxs-lookup"><span data-stu-id="d3d81-136">Download and configure the latest Azure PowerShell commands</span></span>](/powershell/azure/overview)

## <a name="installation"></a><span data-ttu-id="d3d81-137">Installare</span><span class="sxs-lookup"><span data-stu-id="d3d81-137">Installation</span></span>
<span data-ttu-id="d3d81-138">L'Estensione Agente IaaS di SQL Server viene installata automaticamente quando si esegue il provisioning di una delle immagini della galleria di macchine virtuali SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d3d81-138">The SQL Server IaaS Agent Extension is automatically installed when you provision one of the SQL Server virtual machine gallery images.</span></span> <span data-ttu-id="d3d81-139">Se è necessario reinstallare manualmente l'estensione in una di queste macchine virtuali di SQL Server, usare il comando PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="d3d81-139">If you need to reinstall the extension manually on one of these SQL Server VMs, use the following PowerShell command:</span></span>

```powershell
Set-AzureRmVMSqlServerExtension -ResourceGroupName "resourcegroupname" -VMName "vmname" -Name "SQLIaasExtension" -Version "1.2" -Location "East US 2"
```

<span data-ttu-id="d3d81-140">È possibile anche installare l'estensione SQL Server IaaS Agent in una macchina virtuale Windows Server con il solo sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="d3d81-140">It is also possible to install the SQL Server IaaS Agent Extension on an OS-only Windows Server virtual machine.</span></span> <span data-ttu-id="d3d81-141">Questa soluzione è supportata solo se SQL Server è stato installato manualmente sul computer.</span><span class="sxs-lookup"><span data-stu-id="d3d81-141">This is only supported if you have also manually installed SQL Server on that machine.</span></span> <span data-ttu-id="d3d81-142">Installare quindi l'estensione manualmente usando lo stesso cmdlet di PowerShell **Set-AzureVMSqlServerExtension**.</span><span class="sxs-lookup"><span data-stu-id="d3d81-142">Then install the extension manually by using the same **Set-AzureVMSqlServerExtension** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="d3d81-143">Se si installa manualmente l'estensione Agente IaaS di SQL Server in una macchina virtuale Windows Server con il solo sistema operativo, non è possibile gestire le impostazioni di configurazione di SQL Server tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d3d81-143">If you manually install the SQL Server IaaS Agent Extension on an OS-only Windows Server VM, you can not manage the SQL Server configuration settings through the Azure portal.</span></span> <span data-ttu-id="d3d81-144">In questo scenario è necessario eseguire tutte le modifiche con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d3d81-144">In this scenario, you must make all changes with PowerShell.</span></span>

## <a name="status"></a><span data-ttu-id="d3d81-145">Stato</span><span class="sxs-lookup"><span data-stu-id="d3d81-145">Status</span></span>
<span data-ttu-id="d3d81-146">Un modo per verificare che l'estensione sia installata consiste nel visualizzare lo stato dell'agente nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d3d81-146">One way to verify that the extension is installed is to view the agent status in the Azure Portal.</span></span> <span data-ttu-id="d3d81-147">Selezionare **Tutte le impostazioni** nel pannello della macchina virtuale e quindi fare clic su **Estensioni**.</span><span class="sxs-lookup"><span data-stu-id="d3d81-147">Select **All settings** in the virtual machine blade, and then click on **Extensions**.</span></span> <span data-ttu-id="d3d81-148">Verrà elencata l'estensione **SQLIaaSExtension** .</span><span class="sxs-lookup"><span data-stu-id="d3d81-148">You should see the **SQLIaaSExtension** extension listed.</span></span>

![Estensione Agente IaaS di SQL Server nel portale di Azure](./media/virtual-machines-windows-sql-server-agent-extension/azure-rm-sql-server-iaas-agent-portal.png)

<span data-ttu-id="d3d81-150">È anche possibile usare il cmdlet di Azure PowerShell **Get-AzureVMSqlServerExtension** .</span><span class="sxs-lookup"><span data-stu-id="d3d81-150">You can also use the **Get-AzureVMSqlServerExtension** Azure Powershell cmdlet.</span></span>

    Get-AzureRmVMSqlServerExtension -VMName "vmname" -ResourceGroupName "resourcegroupname"

<span data-ttu-id="d3d81-151">Il comando precedente conferma l'installazione dell'agente e ne fornisce informazioni generali sullo stato.</span><span class="sxs-lookup"><span data-stu-id="d3d81-151">The previous command confirms the agent is installed and provides general status information.</span></span> <span data-ttu-id="d3d81-152">È inoltre possibile ottenere informazioni specifiche sullo stato del backup e dell'applicazione di patch in modalità automatizzata con i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="d3d81-152">You can also get specific status information about Automated Backup and Patching with the following commands.</span></span>

    $sqlext = Get-AzureRmVMSqlServerExtension -VMName "vmname" -ResourceGroupName "resourcegroupname"
    $sqlext.AutoPatchingSettings
    $sqlext.AutoBackupSettings

## <a name="removal"></a><span data-ttu-id="d3d81-153">Rimozione</span><span class="sxs-lookup"><span data-stu-id="d3d81-153">Removal</span></span>
<span data-ttu-id="d3d81-154">Nel portale di Azure è possibile disinstallare l'estensione facendo clic sui puntini di sospensione nel pannello **Estensioni** delle proprietà della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d3d81-154">In the Azure Portal, you can uninstall the extension by clicking the ellipsis on the **Extensions** blade of your virtual machine properties.</span></span> <span data-ttu-id="d3d81-155">Fare quindi clic su **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="d3d81-155">Then click **Delete**.</span></span>

![Disinstallare l'Estensione Agente IaaS di SQL Server nel portale di Azure](./media/virtual-machines-windows-sql-server-agent-extension/azure-rm-sql-server-iaas-agent-uninstall.png)

<span data-ttu-id="d3d81-157">È anche possibile usare il cmdlet di PowerShell **Remove-AzureRmVMSqlServerExtension** .</span><span class="sxs-lookup"><span data-stu-id="d3d81-157">You can also use the **Remove-AzureRmVMSqlServerExtension** Powershell cmdlet.</span></span>

    Remove-AzureRmVMSqlServerExtension -ResourceGroupName "resourcegroupname" -VMName "vmname" -Name "SQLIaasExtension"

## <a name="next-steps"></a><span data-ttu-id="d3d81-158">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d3d81-158">Next Steps</span></span>
<span data-ttu-id="d3d81-159">Iniziare a usare uno dei servizi supportati dall'estensione.</span><span class="sxs-lookup"><span data-stu-id="d3d81-159">Begin using one of the services supported by the extension.</span></span> <span data-ttu-id="d3d81-160">Per altre informazioni, vedere gli argomenti citati nella sezione [Servizi supportati](#supported-services) di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="d3d81-160">For more details, see the topics referenced in the [Supported services](#supported-services) section of this article.</span></span>

<span data-ttu-id="d3d81-161">Per altre informazioni sull'esecuzione di SQL Server in Macchine virtuali di Azure, vedere [Panoramica di SQL Server in Macchine virtuali di Azure](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d3d81-161">For more information about running SQL Server on Azure Virtual Machines, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

