---
title: Gestire i nodi di calcolo del cluster HPC Pack | Microsoft Docs
description: Informazioni sugli strumenti di script di PowerShell per aggiungere, rimuovere, avviare e arrestare i nodi di calcolo del cluster HPC Pack 2012 R2 in Azure
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 4193f03b-94e9-4704-a7ad-379abde063a9
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: dc9f354191b9e80ff6a01bd401a874c6998bda79
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="manage-the-number-and-availability-of-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="26c1a-103">Gestire il numero e la disponibilità dei nodi di calcolo in un cluster HPC Pack in Azure</span><span class="sxs-lookup"><span data-stu-id="26c1a-103">Manage the number and availability of compute nodes in an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="26c1a-104">Se è stato creato un cluster HPC Pack 2012 R2 nelle macchine virtuali di Azure, potrebbe essere utile conoscere il modo in cui aggiungere, rimuovere, avviare (provisioning) o arrestare (deprovisioning) facilmente alcune macchine virtuali dei nodi di calcolo nel cluster.</span><span class="sxs-lookup"><span data-stu-id="26c1a-104">If you created an HPC Pack 2012 R2 cluster in Azure VMs, you might want ways to easily add, remove, start (provision), or stop (deprovision) some compute node VMs in the cluster.</span></span> <span data-ttu-id="26c1a-105">Per eseguire queste attività, eseguire gli script di Azure PowerShell installati nella VM del nodo head.</span><span class="sxs-lookup"><span data-stu-id="26c1a-105">To do these tasks, run Azure PowerShell scripts that are installed on the head node VM.</span></span> <span data-ttu-id="26c1a-106">Questi script consentono di controllare il numero e la disponibilità delle risorse del cluster HPC Pack in modo da poter controllare i costi.</span><span class="sxs-lookup"><span data-stu-id="26c1a-106">These scripts help you control the number and availability of your HPC Pack cluster resources so you can control costs.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="26c1a-107">Questo articolo si applica solo ai cluster HPC Pack 2012 R2 in Azure creati con il modello di distribuzione classico.</span><span class="sxs-lookup"><span data-stu-id="26c1a-107">This article applies only to HPC Pack 2012 R2 clusters in Azure created using the classic deployment model.</span></span> <span data-ttu-id="26c1a-108">Microsoft consiglia di usare il modello di Gestione risorse per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="26c1a-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>
> <span data-ttu-id="26c1a-109">Gli script di PowerShell descritti in questo articolo non sono disponibili in HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="26c1a-109">In addition, the PowerShell scripts described in this article are not available in HPC Pack 2016.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="26c1a-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="26c1a-110">Prerequisites</span></span>
* <span data-ttu-id="26c1a-111">**Cluster HPC Pack 2012 R2 in macchine virtuali di Azure** - Creare un cluster HPC Pack 2012 R2 nel modello di distribuzione classico.</span><span class="sxs-lookup"><span data-stu-id="26c1a-111">**HPC Pack 2012 R2 cluster in Azure VMs**: Create an HPC Pack 2012 R2 cluster in the classic deployment model.</span></span> <span data-ttu-id="26c1a-112">È possibile automatizzare ad esempio la distribuzione usando l'immagine di macchina virtuale di HPC Pack 2012 R2 in Azure Marketplace e uno script di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="26c1a-112">For example, you can automate the deployment by using the HPC Pack 2012 R2 VM image in the Azure Marketplace and an Azure PowerShell script.</span></span> <span data-ttu-id="26c1a-113">Per informazioni e indicazioni sui prerequisiti, vedere [Creare un cluster HPC con lo script di distribuzione IaaS di HPC Pack](hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="26c1a-113">For information and prerequisites, see [Create an HPC Cluster with the HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md).</span></span>
  
    <span data-ttu-id="26c1a-114">Dopo la distribuzione, trovare gli script di gestione dei nodi nella cartella %CCP\_HOME%bin nel nodo head.</span><span class="sxs-lookup"><span data-stu-id="26c1a-114">After deployment, find the node management scripts in the %CCP\_HOME%bin folder on the head node.</span></span> <span data-ttu-id="26c1a-115">Eseguire ogni script come amministratore.</span><span class="sxs-lookup"><span data-stu-id="26c1a-115">Run each of the scripts as an administrator.</span></span>
* <span data-ttu-id="26c1a-116">**File delle impostazioni di pubblicazione o certificato di gestione di Azure** - È necessario eseguire una di queste operazioni sul nodo head:</span><span class="sxs-lookup"><span data-stu-id="26c1a-116">**Azure publish settings file or management certificate**: You need to do one of the following on the head node:</span></span>
  
  * <span data-ttu-id="26c1a-117">**Importare il file delle impostazioni di pubblicazione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="26c1a-117">**Import the Azure publish settings file**.</span></span> <span data-ttu-id="26c1a-118">A questo scopo, eseguire i cmdlet di Azure PowerShell seguenti nel nodo head:</span><span class="sxs-lookup"><span data-stu-id="26c1a-118">To do this, run the following Azure PowerShell cmdlets on the head node:</span></span>
    
    ```PowerShell
    Get-AzurePublishSettingsFile
    
    Import-AzurePublishSettingsFile –PublishSettingsFile <publish settings file>
    ```
  * <span data-ttu-id="26c1a-119">**Configurare il certificato di gestione di Azure nel nodo head**.</span><span class="sxs-lookup"><span data-stu-id="26c1a-119">**Configure the Azure management certificate on the head node**.</span></span> <span data-ttu-id="26c1a-120">Se si dispone del file con estensione cer, importarlo nell'archivio certificati CurrentUser\My certificate e quindi eseguire il seguente cmdlet di Azure PowerShell per l'ambiente Azure (AzureCloud o AzureChinaCloud):</span><span class="sxs-lookup"><span data-stu-id="26c1a-120">If you have the .cer file, import it in the CurrentUser\My certificate store and then run the following Azure PowerShell cmdlet for your Azure environment (either AzureCloud or AzureChinaCloud):</span></span>
    
    ```PowerShell
    Set-AzureSubscription -SubscriptionName <Sub Name> -SubscriptionId <Sub ID> -Certificate (Get-Item Cert:\CurrentUser\My\<Cert Thrumbprint>) -Environment <AzureCloud | AzureChinaCloud>
    ```

## <a name="add-compute-node-vms"></a><span data-ttu-id="26c1a-121">Aggiungere le macchine virtuali dei nodi di calcolo</span><span class="sxs-lookup"><span data-stu-id="26c1a-121">Add compute node VMs</span></span>
<span data-ttu-id="26c1a-122">Aggiungere nodi di calcolo con lo script **Add-HpcIaaSNode.ps1** .</span><span class="sxs-lookup"><span data-stu-id="26c1a-122">Add compute nodes with the **Add-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="26c1a-123">Sintassi</span><span class="sxs-lookup"><span data-stu-id="26c1a-123">Syntax</span></span>
```PowerShell
Add-HPCIaaSNode.ps1 [-ServiceName] <String> [-ImageName] <String>
 [-Quantity] <Int32> [-InstanceSize] <String> [-DomainUserName] <String> [[-DomainUserPassword] <String>]
 [[-NodeNameSeries] <String>] [<CommonParameters>]

```
### <a name="parameters"></a><span data-ttu-id="26c1a-124">Parametri</span><span class="sxs-lookup"><span data-stu-id="26c1a-124">Parameters</span></span>
* <span data-ttu-id="26c1a-125">**ServiceName** - Nome del servizio cloud a cui vengono aggiunte le nuove macchine virtuali dei nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="26c1a-125">**ServiceName**: Name of the cloud service that new compute node VMs are added to.</span></span>
* <span data-ttu-id="26c1a-126">**ImageName** - Nome dell'immagine della macchina virtuale di Azure, che si può ottenere nel portale di Azure classico o con il cmdlet di Azure PowerShell **Get-AzureVMImage**.</span><span class="sxs-lookup"><span data-stu-id="26c1a-126">**ImageName**: Azure VM image name, which can be obtained through the Azure classic portal or Azure PowerShell cmdlet **Get-AzureVMImage**.</span></span> <span data-ttu-id="26c1a-127">L'immagine deve soddisfare i seguenti requisiti:</span><span class="sxs-lookup"><span data-stu-id="26c1a-127">The image must meet the following requirements:</span></span>
  
  1. <span data-ttu-id="26c1a-128">Deve essere installato un sistema operativo Windows.</span><span class="sxs-lookup"><span data-stu-id="26c1a-128">A Windows operating system must be installed.</span></span>
  2. <span data-ttu-id="26c1a-129">HPC Pack deve essere installato nel ruolo del nodo di calcolo.</span><span class="sxs-lookup"><span data-stu-id="26c1a-129">HPC Pack must be installed in the compute node role.</span></span>
  3. <span data-ttu-id="26c1a-130">L'immagine deve essere un'immagine privata nella categoria utente, non un'immagine di macchina virtuale di Azure pubblica.</span><span class="sxs-lookup"><span data-stu-id="26c1a-130">The image must be a private image in the User category, not a public Azure VM image.</span></span>
* <span data-ttu-id="26c1a-131">**Quantity** - Numero delle macchine virtuali dei nodi di calcolo da aggiungere.</span><span class="sxs-lookup"><span data-stu-id="26c1a-131">**Quantity**: Number of compute node VMs to be added.</span></span>
* <span data-ttu-id="26c1a-132">**InstanceSize** - Dimensioni delle macchine virtuali dei nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="26c1a-132">**InstanceSize**: Size of the compute node VMs.</span></span>
* <span data-ttu-id="26c1a-133">**DomainUserName** - Nome utente di dominio, da usare per aggiungere le nuove macchine virtuali al dominio.</span><span class="sxs-lookup"><span data-stu-id="26c1a-133">**DomainUserName**: Domain user name, which is used to join the new VMs to the domain.</span></span>
* <span data-ttu-id="26c1a-134">**DomainUserPassword** - Password dell'utente di dominio.</span><span class="sxs-lookup"><span data-stu-id="26c1a-134">**DomainUserPassword**: Password of the domain user.</span></span>
* <span data-ttu-id="26c1a-135">**NodeNameSeries** (facoltativo) - Modello di denominazione per i nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="26c1a-135">**NodeNameSeries** (optional): Naming pattern for the compute nodes.</span></span> <span data-ttu-id="26c1a-136">Il formato deve essere &lt;*Nome\_Radice*&gt;&lt;*Numero\_Iniziale*&gt;%.</span><span class="sxs-lookup"><span data-stu-id="26c1a-136">The format must be &lt;*Root\_Name*&gt;&lt;*Start\_Number*&gt;%.</span></span> <span data-ttu-id="26c1a-137">Ad esempio, MyCN%10% significa una serie di nomi dei nodi di calcolo a partire da MyCN11.</span><span class="sxs-lookup"><span data-stu-id="26c1a-137">For example, MyCN%10% means a series of the compute node names starting from MyCN11.</span></span> <span data-ttu-id="26c1a-138">Se non specificato, lo script usa la serie di nomi dei nodi di calcolo configurata nel cluster HPC.</span><span class="sxs-lookup"><span data-stu-id="26c1a-138">If not specified, the script uses the configured node naming series in the HPC cluster.</span></span>

### <a name="example"></a><span data-ttu-id="26c1a-139">Esempio</span><span class="sxs-lookup"><span data-stu-id="26c1a-139">Example</span></span>
<span data-ttu-id="26c1a-140">L'esempio seguente aggiunge 20 VM dei nodi di calcolo di grandi dimensioni nel servizio cloud *hpcservice1* in base all'immagine di VM *hpccnimage1*.</span><span class="sxs-lookup"><span data-stu-id="26c1a-140">The following example adds 20 size Large compute node VMs in the cloud service *hpcservice1*, based on the VM image *hpccnimage1*.</span></span>

```PowerShell
Add-HPCIaaSNode.ps1 –ServiceName hpcservice1 –ImageName hpccniamge1
–Quantity 20 –InstanceSize Large –DomainUserName <username>
-DomainUserPassword <password>
```


## <a name="remove-compute-node-vms"></a><span data-ttu-id="26c1a-141">Rimuovere le macchine virtuali dei nodi di calcolo</span><span class="sxs-lookup"><span data-stu-id="26c1a-141">Remove compute node VMs</span></span>
<span data-ttu-id="26c1a-142">Rimuovere i nodi di calcolo con lo script **Remove-HpcIaaSNode.ps1** .</span><span class="sxs-lookup"><span data-stu-id="26c1a-142">Remove compute nodes with the **Remove-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="26c1a-143">Sintassi</span><span class="sxs-lookup"><span data-stu-id="26c1a-143">Syntax</span></span>
```PowerShell
Remove-HPCIaaSNode.ps1 -Name <String[]> [-DeleteVHD] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]

Remove-HPCIaaSNode.ps1 -Node <Object> [-DeleteVHD] [-Force] [-Confirm] [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="26c1a-144">Parametri</span><span class="sxs-lookup"><span data-stu-id="26c1a-144">Parameters</span></span>
* <span data-ttu-id="26c1a-145">**Name** - Nomi dei nodi del cluster da rimuovere.</span><span class="sxs-lookup"><span data-stu-id="26c1a-145">**Name**: Names of cluster nodes to be removed.</span></span> <span data-ttu-id="26c1a-146">Sono supportati caratteri jolly.</span><span class="sxs-lookup"><span data-stu-id="26c1a-146">Wildcards are supported.</span></span> <span data-ttu-id="26c1a-147">Il nome del set di parametri è Name.</span><span class="sxs-lookup"><span data-stu-id="26c1a-147">The parameter set name is Name.</span></span> <span data-ttu-id="26c1a-148">Non è possibile specificare entrambi i parametri **Name** e **Node**.</span><span class="sxs-lookup"><span data-stu-id="26c1a-148">You can't specify both the **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="26c1a-149">**Node** - Oggetto HpcNode relativo ai nodi da rimuovere, che si può ottenere tramite il cmdlet di PowerShell per HPC [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span><span class="sxs-lookup"><span data-stu-id="26c1a-149">**Node**: The HpcNode object for the nodes to be removed, which can be obtained through the HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="26c1a-150">Il nome del set di parametri è Node.</span><span class="sxs-lookup"><span data-stu-id="26c1a-150">The parameter set name is Node.</span></span> <span data-ttu-id="26c1a-151">Non è possibile specificare entrambi i parametri **Name** e **Node**.</span><span class="sxs-lookup"><span data-stu-id="26c1a-151">You can't specify both the **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="26c1a-152">**DeleteVHD** (facoltativo) - Impostazione per eliminare i dischi associati per le macchine virtuali rimosse.</span><span class="sxs-lookup"><span data-stu-id="26c1a-152">**DeleteVHD** (optional): Setting to delete the associated disks for the VMs that are removed.</span></span>
* <span data-ttu-id="26c1a-153">**Force** (facoltativo) - Impostazione per impostare offline i nodi HPC prima di rimuoverli.</span><span class="sxs-lookup"><span data-stu-id="26c1a-153">**Force** (optional): Setting to force HPC nodes offline before removing them.</span></span>
* <span data-ttu-id="26c1a-154">**Confirm** (facoltativo) - Richiesta di conferma prima dell'esecuzione di un comando.</span><span class="sxs-lookup"><span data-stu-id="26c1a-154">**Confirm** (optional): Prompt for confirmation before executing the command.</span></span>
* <span data-ttu-id="26c1a-155">**WhatIf** - Impostazione per descrivere le conseguenze dell'esecuzione di un comando senza eseguirlo effettivamente.</span><span class="sxs-lookup"><span data-stu-id="26c1a-155">**WhatIf**: Setting to describe what would happen if you executed the command without actually executing the command.</span></span>

### <a name="example"></a><span data-ttu-id="26c1a-156">Esempio</span><span class="sxs-lookup"><span data-stu-id="26c1a-156">Example</span></span>
<span data-ttu-id="26c1a-157">L'esempio seguente porta forzatamente offline i nodi con nomi che iniziano con *HPCNode-CN-* e quindi rimuove i nodi e i dischi associati corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="26c1a-157">The following example forces offline the nodes with names beginning *HPCNode-CN-* and them removes the nodes and their associated disks.</span></span>

```PowerShell
Remove-HPCIaaSNode.ps1 –Name HPCNodeCN-* –DeleteVHD -Force
```

## <a name="start-compute-node-vms"></a><span data-ttu-id="26c1a-158">Avviare le macchine virtuali dei nodi di calcolo</span><span class="sxs-lookup"><span data-stu-id="26c1a-158">Start compute node VMs</span></span>
<span data-ttu-id="26c1a-159">Avviare i nodi di calcolo con lo script **Start-HpcIaaSNode.ps1** .</span><span class="sxs-lookup"><span data-stu-id="26c1a-159">Start compute nodes with the **Start-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="26c1a-160">Sintassi</span><span class="sxs-lookup"><span data-stu-id="26c1a-160">Syntax</span></span>
```PowerShell
Start-HPCIaaSNode.ps1 -Name <String[]> [<CommonParameters>]

Start-HPCIaaSNode.ps1 -Node <Object> [<CommonParameters>]
```
### <a name="parameters"></a><span data-ttu-id="26c1a-161">Parametri</span><span class="sxs-lookup"><span data-stu-id="26c1a-161">Parameters</span></span>
* <span data-ttu-id="26c1a-162">**Name** - Nomi dei nodi del cluster da avviare.</span><span class="sxs-lookup"><span data-stu-id="26c1a-162">**Name**: Names of the cluster nodes to be started.</span></span> <span data-ttu-id="26c1a-163">Sono supportati caratteri jolly.</span><span class="sxs-lookup"><span data-stu-id="26c1a-163">Wildcards are supported.</span></span> <span data-ttu-id="26c1a-164">Il nome del set di parametri è Name.</span><span class="sxs-lookup"><span data-stu-id="26c1a-164">The parameter set name is Name.</span></span> <span data-ttu-id="26c1a-165">Non è possibile specificare entrambi i parametri **Name** e **Node**.</span><span class="sxs-lookup"><span data-stu-id="26c1a-165">You cannot specify both the **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="26c1a-166">**Node**- Oggetto HpcNode relativo ai nodi da avviare, che può essere ottenuto tramite il cmdlet di PowerShell per HPC [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span><span class="sxs-lookup"><span data-stu-id="26c1a-166">**Node**- The HpcNode object for the nodes to be started, which can be obtained through the HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="26c1a-167">Il nome del set di parametri è Node.</span><span class="sxs-lookup"><span data-stu-id="26c1a-167">The parameter set name is Node.</span></span> <span data-ttu-id="26c1a-168">Non è possibile specificare entrambi i parametri **Name** e **Node**.</span><span class="sxs-lookup"><span data-stu-id="26c1a-168">You cannot specify both the **Name** and **Node** parameters.</span></span>

### <a name="example"></a><span data-ttu-id="26c1a-169">Esempio</span><span class="sxs-lookup"><span data-stu-id="26c1a-169">Example</span></span>
<span data-ttu-id="26c1a-170">L'esempio seguente avvia i nodi i cui nomi iniziano con *HPCNode-CN-*.</span><span class="sxs-lookup"><span data-stu-id="26c1a-170">The following example starts nodes with names beginning *HPCNode-CN-*.</span></span>

```PowerShell
Start-HPCIaaSNode.ps1 –Name HPCNodeCN-*
```

## <a name="stop-compute-node-vms"></a><span data-ttu-id="26c1a-171">Arrestare le macchine virtuali dei nodi di calcolo</span><span class="sxs-lookup"><span data-stu-id="26c1a-171">Stop compute node VMs</span></span>
<span data-ttu-id="26c1a-172">Arrestare i nodi di calcolo con lo script **Stop-HpcIaaSNode.ps1** .</span><span class="sxs-lookup"><span data-stu-id="26c1a-172">Stop compute nodes with the **Stop-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="26c1a-173">Sintassi</span><span class="sxs-lookup"><span data-stu-id="26c1a-173">Syntax</span></span>
```PowerShell
Stop-HPCIaaSNode.ps1 -Name <String[]> [-Force] [<CommonParameters>]

Stop-HPCIaaSNode.ps1 -Node <Object> [-Force] [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="26c1a-174">Parametri</span><span class="sxs-lookup"><span data-stu-id="26c1a-174">Parameters</span></span>
* <span data-ttu-id="26c1a-175">**Name**- Nomi dei nodi del cluster da arrestare.</span><span class="sxs-lookup"><span data-stu-id="26c1a-175">**Name**- Names of the cluster nodes to be stopped.</span></span> <span data-ttu-id="26c1a-176">Sono supportati caratteri jolly.</span><span class="sxs-lookup"><span data-stu-id="26c1a-176">Wildcards are supported.</span></span> <span data-ttu-id="26c1a-177">Il nome del set di parametri è Name.</span><span class="sxs-lookup"><span data-stu-id="26c1a-177">The parameter set name is Name.</span></span> <span data-ttu-id="26c1a-178">Non è possibile specificare entrambi i parametri **Name** e **Node**.</span><span class="sxs-lookup"><span data-stu-id="26c1a-178">You cannot specify both the **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="26c1a-179">**Node** - Oggetto HpcNode relativo ai nodi da arrestare, che si può ottenere tramite il cmdlet di PowerShell per HPC [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span><span class="sxs-lookup"><span data-stu-id="26c1a-179">**Node**: The HpcNode object for the nodes to be stopped, which can be obtained through the HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="26c1a-180">Il nome del set di parametri è Node.</span><span class="sxs-lookup"><span data-stu-id="26c1a-180">The parameter set name is Node.</span></span> <span data-ttu-id="26c1a-181">Non è possibile specificare entrambi i parametri **Name** e **Node**.</span><span class="sxs-lookup"><span data-stu-id="26c1a-181">You cannot specify both the **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="26c1a-182">**Force** (facoltativo) - Impostazione per impostare offline i nodi HPC prima di arrestarli.</span><span class="sxs-lookup"><span data-stu-id="26c1a-182">**Force** (optional): Setting to force HPC nodes offline before stopping them.</span></span>

### <a name="example"></a><span data-ttu-id="26c1a-183">Esempio</span><span class="sxs-lookup"><span data-stu-id="26c1a-183">Example</span></span>
<span data-ttu-id="26c1a-184">L'esempio seguente imposta offline i nodi i cui nomi iniziano con *HPCNode-CN-* e li arresta.</span><span class="sxs-lookup"><span data-stu-id="26c1a-184">The following example forces offline nodes with names beginning *HPCNode-CN-* and then stops the nodes.</span></span>

```PowerShell
Stop-HPCIaaSNode.ps1 –Name HPCNodeCN-* -Force
```

## <a name="next-steps"></a><span data-ttu-id="26c1a-185">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="26c1a-185">Next steps</span></span>
* <span data-ttu-id="26c1a-186">Per aumentare o ridurre automaticamente i nodi del cluster in base al carico di lavoro corrente dei processi e delle attività del cluster, vedere l'articolo [Aumentare e ridurre automaticamente le risorse del cluster HPC Pack in Azure in base al carico di lavoro del cluster](hpcpack-cluster-node-autogrowshrink.md).</span><span class="sxs-lookup"><span data-stu-id="26c1a-186">To automatically grow or shrink the cluster nodes according to the current workload of jobs and tasks on the cluster, see [Automatically grow and shrink the HPC Pack cluster resources in Azure according to the cluster workload](hpcpack-cluster-node-autogrowshrink.md).</span></span>

